
/dev/hda1 * 1 7 52888+ 83 Linux
/dev/hda2 8 3779 28516320 83 Linux
/dev/hda3 3780 3883 786240 82 Linux swap
磁盘 /dev/hdb：240 个磁头，63 个扇区，7753 个柱面
单位 = 15120 * 512 字节的柱面

设备 启动 开始 结束 块数 Id 系统
/dev/hdb1 * 1 14 10580+ 83 Linux
/dev/hdb2 15 7649 57720600 83 Linux
/dev/hdb3 7650 7753 786240 82 Linux swap

你可能会看到几种不同类型的磁盘，例如 /dev/hdxx，它们是 IDE 磁盘，/dev/sdxx 它们是 SCSI 或 SAN 磁盘，以及 /dev/id0 或 /dev/ida 磁盘，它们是 RAID 磁盘。此外，如果你运行的是 EMC PowerPath 或 Veritas Volume Manager 等软件，你会看到不同的设备名称。

如果看不到要用于 ASM 的分区，你必须先使用 fdisk 或 parted 创建这些分区，然后才能用 ASM 配置它们。一旦看到要使用的分区，你就可以通过使用带有 createdisk 参数的 /etc/init.d/oracleasm 命令将该磁盘添加到 ASM。所有 oracleasm 参数都列在下一节中。

![](img/9479df2d00f5e62b87366b125224950f_180_0.png)

> 尽管 ASM 磁盘可以作为磁盘驱动器上的分区创建，但 Oracle 建议为 ASM 使用整个磁盘驱动器。这是通过创建使用整个磁盘的一个分区来实现的。

要将 /dev/sda3 添加到 ASM，请使用以下命令：

```
[root@ptc6 root]# /etc/init.d/oracleasm createdisk VOL1 /dev/sda3
Marking disk "/dev/sda3" as an ASM disk [ OK ]
```

我现在可以查询 ASM，以确保 ASM 卷已为 ASM 库驱动程序使用而添加。

```
[root@ptc6 root]# /etc/init.d/oracleasm listdisks
VOL1
```

一旦你有一个或多个 ASM 磁盘可用，你就可以开始 Oracle 安装过程。当然，只有当你要将 Oracle 数据库创建在 ASM 上时，ASM 卷才是必要的。

## Oracleasm 可选参数

Oracle ASM 库驱动程序支持许多用于管理 ASM 的可选命令。如果你打算使用 ASM，应该熟悉这些命令：

| 命令 | 描述 |
| --- | --- |
| /etc/init.d/oracleasm configure | 用于配置 ASM 模块和 ASM 配置文件以及设置 ASM 挂载点。 |
| /etc/init.d/oracleasm [enable/disable] | 这些命令将更改 ASM 库驱动程序是否在系统启动时启动。此命令修改 /etc/sysconfig/oracleasm 文件。 |
| /etc/init.d/oracleasm [start/stop/restart] | 这些命令将停止、启动或重启 ASM 库驱动程序。 |
| /etc/init.d/oracleasm status | 显示 ASM 库驱动程序的状态。 |
| /etc/init.d/oracleasm createdisk name dev | 此命令接受要创建的卷的名称和设备名称，以便将磁盘驱动器与 ASM 关联：/etc/init.d/oracleasm createdisk VOL1 /dev/sda3。 |
| /etc/init.d/oracleasm deletedisk name | 从与 ASM 的关联中移除磁盘驱动器。 |
| /etc/init.d/oracleasm listdisks | 列出与 ASM 关联的所有磁盘名称。 |
| /etc/init.d/oracleasm querydisk [name/dev] | 用于确定磁盘名称或磁盘设备是否与 ASM 关联。参见下面的示例。 |
| /etc/init.d/oracleasm scandisks | 用于 RAC 集群，以便集群节点能够识别在另一个节点上已与 ASM 关联的磁盘。 |

以下是使用 /etc/init.d/oracleasm 命令的几个示例：
检查 ASM 库驱动程序的状态：

```
[root@ptc6 root]# /etc/init.d/oracleasm status
Checking if ASM is loaded: [ OK ]
Checking if /dev/oracleasm is mounted: [ OK ]
```

重启 ASM 库驱动程序：

```
[root@ptc6 root]# /etc/init.d/oracleasm restart
Unmounting ASMLib driver filesystem [ OK ]
Unloading module "oracleasm" [ OK ]
Loading module "oracleasm" [ OK ]
Mounting ASMLib driver filesystem [ OK ]
Scanning system for ASM disks [ OK ]
```

删除 ASM 磁盘：

```
[root@ptc6 root]# /etc/init.d/oracleasm deletedisk VOL2
Removing ASM disk "VOL2" [ OK ]
```

添加 ASM 磁盘：

```
[root@ptc6 root]# /etc/init.d/oracleasm createdisk VOL2 /dev/sda4
Marking disk "/dev/sda4" as an ASM disk [ OK ]
```

列出 ASM 磁盘：

```
[root@ptc6 root]# /etc/init.d/oracleasm listdisks
VOL1
VOL2
```

查询 ASM 磁盘：

```
[root@ptc6 root]# /etc/init.d/oracleasm querydisk VOL2
Disk "VOL2" is a valid ASM disk
[root@ptc6 root]# /etc/init.d/oracleasm querydisk /dev/sda3
Disk "/dev/sda3" is marked an ASM disk
```

扫描 ASM 磁盘：

```
[root@ptc6 root]# /etc/init.d/oracleasm scandisks
Scanning system for ASM disks [ OK ]
```

> **NOTE**
> 每当在 RAC 集群的节点上添加 ASM 驱动器时，都应在集群中的所有其他节点上运行 scandisk。这将验证所有节点是否已刷新所有 ASM 信息并且保持同步。

一旦 ASM 驱动器创建完成，你就可以开始安装 Oracle。在安装过程中，你将被允许选择将用于数据库的哪种数据类型。

## 使用 ASM 驱动器

ASM 磁盘在 ASM 实例中使用，该实例作为 Oracle 10g 安装的一部分创建，并且仅用于管理 ASM 磁盘的目的。此实例使用 CREATE DISKGROUPS 语句创建在 ASM 中使用的磁盘组。本章后面将更详细地解释使用 ASM 驱动器。

## 安装过程

Oracle 10g 安装过程涉及两个步骤。首先，必须对安装介质进行分级。如果从 Oracle 技术网络网站复制软件，则必须从 .cpio 文件中解压缩并提取软件。第二步是运行 Oracle 安装程序。

有多个文件可供下载，包括：

- **ship.db.cpio.gz** 这是 Oracle 数据库二进制归档，包含创建 Oracle Database 10g 服务器所需的所有程序。
- **ship.ccd.cpio.gz** 伴随 CD 包含两种不同的安装类型。第一种包含与数据库 CD 配套的数据库组件，包括数据库示例、JPublisher、Legato 单服务器版本、Java 库和 Oracle Text 提供的知识库。第二种安装类型由伴随组件组成：HTTP 服务器和 Oracle HTML DB。
- **ship.crs.cpio.gz** 第三个映像是 Oracle 10g Cluster Ready Services。这将在后续章节中详细介绍。

安装的第一步是获取你想要使用的 CD 映像，并将它们分级到 Linux 文件系统中的目录。

### 分级安装

在创建 oracle_stage 目录并将该目录的所有权更改为“oracle”之后，将安装文件复制到此目录。确保 Oracle 用户对此目录具有权限。由于 Oracle 用户将执行安装，以下步骤应作为用户“oracle”运行。

Oracle 安装介质首先使用 gunzip（GNU Unzip）解压缩文件进行分级。只需对你想要解压缩的每个文件运行 gunzip，如下所示：

```
gunzip ship.db.cpio.gz
gunzip ship.ccd.cpio.gz
gunzip ship.crs.cpio.gz
```

文件解压缩后，安装介质需要从 cpio 文件中提取。因为每个归档都有一个解压到的顶级目录，称为 Disk1，所以在开始下一个 cpio 命令之前，你应该将此目录更改为另一个名称。这将避免所有三个 CD 的程序都在同一个子目录中。这是通过使用 cpio 和 mv 命令完成的，如下所示：

```
cpio -idmv ship.db.cpio
mv Disk1 db.Disk1
cpio -idmv ship.ccd.cpio
mv Disk1 ccd.Disk1
cpio -idmv ship.crs.cpio
mv Disk1 crs.Disk1
```

CD 或 CD 解包后，你就可以开始安装过程。

### 运行安装程序

为了调用安装程序，你将运行 shell 程序 runInstaller。请记住，在运行安装程序之前必须完成一些先决条件。以下是这些先决条件的摘要。

- 必须设置内核参数。
- 必须设置 shell 限制。
- 你必须以 Oracle 用户帐户登录。
- 你必须使用 X Windows 登录到图形会话，以便 Java 安装程序能够工作。
- 环境变量 ORACLE_BASE 和 ORACLE_SID 应该被设置。

建议从 /tmp 目录运行此程序，因此请使用以下命令调用安装程序。

```
# cd /tmp
# /oracle_stage/db.Disk1/runInstaller
```

**NOTE**
*为了使 Oracle 安装程序正常工作，X-Windows 必须处于运行状态。如果你通过 ssh shell 运行安装程序，X-Windows 应在你的本地 PC 上运行，并且 .ssh/config 文件中的选项“ForwardX11 no”应被设置。*

