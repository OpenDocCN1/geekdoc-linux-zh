
实施 FCP 磁盘的客户可能还想考虑 N 端口虚拟化。通过 N 端口虚拟化，LUN 可以直接分配给虚拟机，而不是所有运行在 VM 下的虚拟机。N 端口虚拟化首次在 IBM System z9 上支持，不支持 z990 或 z980 型号。详情参见《Fibre Channel Protocol for Linux and vVM on IBM System z, SG24-7266》。

使用 SAN/SCSI 存储时，使用来自多个阵列和所有集群的磁盘非常重要。这将提供更好的 I/O 并发和负载均衡。图 4-2 展示了分配磁盘的正确方法。错误的方法是按顺序在一个 Rank 中分配所有存储，例如从 5100 到 510F。

### 4.3.6 OCR 和投票磁盘（Voting disks）的安装

Oracle 支持两种存储 Oracle 集群文件的方法：使用原始设备（Raw）块设备或共享文件系统，例如 Oracle 集群文件系统 2 (`OCFS2`)。`OCFS2` 是一种基于区的数据的集群文件系统，集群中的所有节点都可以对其访问和写入。`OCFS2` 仅支持 Linux 2.6 及以上版本的内核。

Oracle 集群至少需要两个设备：一个用于 Oracle 集群注册表 (`OCR`)，另一个用于投票磁盘 (`Voting disks`)。如果您正在格式化 ECKD 类型的 DASD 以作为原始或块分区，则必须使用 4 KB 的块大小对其进行格式化。

对于测试系统，通常使用一个分区同时存放 `OCR` 和投票磁盘。对于生产系统，建议每个大小的至少使用 280 MB 空间，并配置多个投票磁盘（必须为奇数）。

- 两个 `OCR`：每个 256 MB 或 512 MB
- 三个投票磁盘：每个 256 MB 或 768 MB

Oracle 确保设备包含至少 256 MB 的可用磁盘空间。因此，建议每个设备大小至少为 280 MB，以考虑到分区创建产生的影响。

### 4.3.7 共享数据库磁盘安装

可以使用以下存储选项创建 Oracle RAC：

- 使用 Oracle ASM 用于数据文件，`OCR` 和投票磁盘放置在原始设备或块设备上
- 标准原始设备或块设备（不使用 Oracle ASM）

为 Oracle 使用的不同类型 I/O 设置多个磁盘组是一个非常好主意。例如，设置一组磁盘用于数据库文件，另一组磁盘用于重做日志（`redo logs`）。

如果创建 ASM 数据库，Oracle 建议将闪回恢复区域（Flash Recovery Area）放置在与数据库文件不同的磁盘组上。这可以防止系统活动数据与备份恢复数据位于同一块物理磁盘上。

## 4.4 为 Oracle RAC 格式化分区磁盘

格式化工具 `dasdfmt` 提供了以不同块大小格式化 DASD 设备选项。在 z/VM 系统上，应使用 4096 的 `dasdfmt` 块大小：

```
# dasdfmt -f /dev/dasda -b 4096 -p
# dasdfmt -f /dev/dasdb -b 4096 -p
# dasdfmt -f /dev/dasdc -b 4096 -p
```

下一步是在每个磁盘设备上创建一个分区。您本应该在每个磁盘上只创建一个分区，但在测试环境中，人们会在每个磁盘上创建多个分区。无论您使用 ECKD 磁盘 (`fdsd`) 还是 SCSI/FCP 磁盘 (`fdisk`)，创建分区的命令都是相似的：

```
# fdsd -a /dev/dasda
# fdsd -a /dev/dasdb
# fdisk /dev/sda
```

对于 Oracle RAC，您首先需要对 `OCR`、投票磁盘以及任何 Oracle ASM 数据库磁盘进行格式化分区。

对于非数据库文件系统，您可以使用 `pvcreate` 命令创建物理卷（physical volume）。`pvcreate` 命令在每个磁盘或分区的开头写入卷组描述符。

因此，如果您想创建一个涉及三块磁盘的文件系统，您将输入类似下面的命令，将您想要在卷组中使用的每个设备标记为物理卷：

```
# pvcreate /dev/dasdal /dev/dasb1 /dev/dasc1
```

然后下一步是为物理卷创建卷组（volume group）：

```
# vgcreate orabinvg /dev/dasdal /dev/dasb1 /dev/dasc1
```

要显示此卷组的属性，可以使用以下命令：

```
# vgdisplay orabinvg
```

下一步是创建一个可以被 Oracle 挂载并使用的逻辑文件系统。

在此示例中，我们使用了三块磁盘和一个具有三条条带（stripes）的 LV，块大小为 32 KB，LV 大为 6.8 GB：

```
# lvcreate -i13 -I32 -L6.8G -orabinlv orarang
```

显示新创建的 LV 的属性，运行：

```
# lvsdisplay /dev/orabvg/orablv
```

要为 oracle 逻辑卷创建 ext3 文件系统，您需要运行 `mkfs`。

建议使用 ext3 文件系统类型：

```
# mkfs.ext3 /dev/orabvg/orablv -b 4096
```

为 oracle home 创建挂载点，挂载文件系统并验证新创建文件的大小：

```
# mkdir -p /oracle
# mount /dev/orabvg/orablv /oracle
# df -h
```

为了使更改永久生效，您需要更新 `fstab`。我们建议先备份此文件：

```
# vi /etc/fstab
/dev/orabvg/orablv /oracle ext3 defaults
```

## 4.5 在原始/块设备上安装 Oracle ASM

Oracle 自动存储管理 (`ASM`) 是 Oracle 10g 中的一项新功能。

建议使用 `oracleasm-support` 2.0.1 驱动，因为它们提供了对回环（loopback）、MD、LVM 和 device-mapper 设备的支持

你可以从以下 Oracle 网站下载 RPM 包：

`http://www.oracle.com/technology/tech/linux/asmlib/index.html`

然后运行以下命令：

```bash
# ls *.rpm
oracleasm-2.6.9-55.0.12.EL-2.0.3-1.s390x.rpm
oracleasmilib-2.0.2-1.s390x.rpm
oracleasm-support-2.0.3-1.s390x.rpm
[root@oralin2 tmp]# rpm -ivh oracleasm-support-2.0.3-1.s390x.rpm
Preparing...
###########################
1:oracleasm-support [100%]
###########################################
[root@oralin2 tmp]# rpm -ivh oracleasm-2.6.9-55.0.12.EL-2.0.3-1.s390x.rpm
Preparing...
###########################################
1:oracleasm-2.6.9-55.0.12 [100%]
###########################################
[root@oralin2 tmp]# rpm -ivh oracleasmilib-2.0.2-1.s390x.rpm
Preparing...
###########################################
1:oracleasmilib [100%]
###########################################
```

下一步是配置 ASM 内核。当我们尝试配置 ASM 内核时，收到了错误，因为我们的 Linux 内核版本与 ASMLib 内核 RPM 版本不匹配：

```bash
[root@oralin2 tmp]# /etc/init.d/oracleasm configure
Configuring the Oracle library driver.

这将配置 Oracle ASM 库驱动程序的启动属性。以下问题将决定驱动程序是否在启动时加载以及它具有什么权限。当前值将显示在括号 ('[]') 中。在不输入答案的情况下按 <ENTER> 将保留该值。Ctrl-C 将取消。

拥有驱动接口的默认用户 [: oracle
拥有驱动接口的默认组 [: dba
启动时启动 Oracle ASM 库驱动程序 (y/n) [n]: y
启动时修复 Oracle ASM 磁盘的权限 (y/n) [y]: y

写入 Oracle ASM 库驱动配置: [ OK ]
创建 /dev/oracleasm 挂点: [ OK ]
加载模块 "oracleasm": Unable to load module "oracleasm"
[FAILED]
```
