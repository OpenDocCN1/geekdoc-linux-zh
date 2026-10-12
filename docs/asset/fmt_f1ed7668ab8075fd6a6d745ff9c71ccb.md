
### 3. 从显示内容中识别您想要使用的设备。

如果显示的设备是 FBA 类型的 DASD，则您无需对其进行配置。您可以继续将它们绑定到 Oracle 数据库文件。

如果您使用 ECKD 类型的 DASD，如果该 DASD 尚未格式化，请输入类似下方的命令来格式化 DASD：

```
# /sbin/dasdfint -b 4096 -f /dev/dasdxxxx
```

> 警告：格式化 DASD 会破坏设备上的所有现有数据。请确保：
> 
> * 您指定了正确的 DASD 设备名称
> * DASD 不包含您想要保留的现有数据

此命令使用 4 KB 的块大小和兼容的磁盘布局（默认）格式化 DASD，允许您在 DASD 上创建多多三个分区。

### 4. 如果您打算在 SCSI 设备上创建原始逻辑卷，请执行第 5 步。

如果您打算在 DASD 上创建原始逻辑卷，且您已使用兼容的磁盘布局格式化了 DASD，请确定您如何创建分区。

要在设备上创建单磁盘分区（例如，如果您想为数据库文件在整个原始逻辑卷创建一个分区），请输入类似下方的命令：

```
# /sbin/fdasd -a /dev/dasdxxxx
```

Oracle Grid Infrastructure 安装指南

# 在 IBM: Linux on z 上配置原始逻辑卷

此命令在设备上创建一个分区。现在可以准备将设备标记为物理卷。请继续第 6 步。

### 5. 如果您打算在 SCSI 设备上创建原始逻辑卷，请遵循以下步骤：

a. 如必要，安装或配置您打算用于磁盘组的共享 DASD 并重启系统。

b. 输入以下命令识别您要使用的磁盘名称：

```
# fdisk -l
```

SCSI 设备的设备名称类似于：

`/dev/sdxn`

在此示例中，`x` 是标识磁盘的字母，`n` 是分区号。例如，`/dev/sda` 是第一个磁盘。

c. 如必要，使用 `t` 命令更改分区。

d. 输入类似下方的命令将您要使用的每个设备标记为物理卷：

对于 SCSI 设备：

```
# pvcreate /dev/sda1 /dev/sdb1
```

要在设备上创建以下：

### 7. 使用您标记的设备创建一个名为 `oracle_vg` 的卷组，输入类似下方的命令：

对于 SCSI 设备：

```
# vgcreate oracle_vg /dev/sda1 /dev/sdb1
```

为集群和 Oracle RAC 的 Oracle Grid Infrastructure 配置存储 3-39

# 在 IBM: Linux on z 上配置原始逻辑卷

对于 DASD 设备：

```
# vgcreate oracle_vg /dev/dasdal /dev/dasdb
```

### 8. 在您创建的卷组中创建所需的逻辑卷，输入类似下方的命令：

```
# lvcreate -L size -n lv_name vg_name
```

在此示例中：

- `size` 是逻辑卷的大小，例如 `500M`
- `lv_name` 是逻辑卷的名称，例如 `orcl_system_raw_500m`
- `vg_name` 是卷组的名称，例如 `oracle_vg`

例如，要在 `oracle_vg` 卷组中名为 `rac` 的数据库的 SYSTEM 表空间创建一个 500 MB 的逻辑卷，输入以下命令：

```
# lvcreate -L 500M -n rac_system_raw_500m oracle_vg
```

> 注意：这些命令为每个逻辑卷创建一个类似于下方的设备名称：
> 
> `/dev/vg_name/lv_name`

### 9. 在其他集群节点上，输入以下命令扫描所有卷组并激活它们：

```
# vgscan
# vgchange -a y
```

# 为集群安装 Oracle Grid Infrastructure

本章描述了为集群安装 Oracle Grid Infrastructure 的步骤。Oracle Grid Infrastructure 由 Oracle Clusterware 和 Oracle 自动存储管理 (Oracle ASM)组成。如果您之后计划安装带有实时应用集群 (Oracle RAC) 的 Oracle Database，这就是两阶段安装中的第一阶段。

本章包含以下主题：

- 使用 OUI 准备安装 Oracle Grid Infrastructure
- 安装 Oracle Grid Infrastructure
- 使用仅软件安装方式安装 Oracle Grid Infrastructure
- Oracle Berkeley DB 的限制
- 确认 Oracle Clusterware 功能
- 确认 Oracle Clusterware 文件的 Oracle ASM 功能
- 理解 Oracle Grid Infrastructure 中的离线过程

## 4.1 准备使用 OUI 安装 Oracle Grid Infrastructure

在用安装程序安装 Oracle Grid Infrastructure 之前，请使用以下检查清单，确保您已拥有安装期间所需的所有信息，并确保您已完成开始安装之前必须完成的所有任务。在完成下列表中的每个任务时请进行勾选，并记录所需的信息，以便您在安装期间提供它们。

- 停止正在运行的 Oracle 进程

您可能需要停止正在运行的 Oracle 进程：

**在未使用 Oracle ASM 的独立数据库节点上安装：** 在安装 Oracle Grid Infrastructure 软件时，不需要停止数据库。

**在已经在 Oracle ASM 上运行独立 Oracle Database 11g release 2 (11.2) 的节点上安装：** 停止 Oracle ASM 实例。Oracle ASM 实例将在安装期间重启。

**在 Oracle RAC 节点上安装：** 此安装需要升级 Oracle Clusterware，因为运行 Oracle RAC 需要 Oracle Clusterware。作为升级的一部分，当滚动升级从节点到节点进行时，您必须停止数据库节点。

### 准备使用 OUI 安装 Oracle Grid Infrastructure

> 注意：如果您正在将 Oracle RAC 9i Release 2 (9.2) 节点升级到 Oracle Grid Infrastructure 11g Release 2（版本 11.2.0.1 和 11.2.0.2），且 TNLSNR 正在监听 SCAN 监听的端口（默认 1521），则应关闭 TNLSNR。

如果您正在升级到 Oracle Grid Infrastructure 11g Release 2 (11.2.0) 或更高版本，则可以忽略此问题。

如果正在运行来自 Oracle9i Release 9.2 或更早版本的全局服务守护 (GSD)，则在安装 Oracle Grid Infrastructure 之前运行以下命令：

```
$ Oracle_home/bin/gsdctl stop
```

其中 `Oracle_home` 是运行 GSD 的 Oracle Database home。

> 警告：如果您有 Oracle9i release 2 (9.2) Oracle Cluster Manager (Oracle CM) 安装，请停止 Oracle CM 服务，这将阻止 Oracle Grid Infrastructure 11g Release 2 (11.2) 软件检测 Oracle9i 2 节点列表并导致 Oracle Grid Infrastructure 安装失败。

> 注意：如果您在启动 Oracle 通用安装程序 (OUI) 后收到停止所有 Oracle 服务的警告，请运行命令

```
Oracle_home/bin/localconfig delete
```

其中 `Oracle_home` 是现有的 Clusterware home。

- 如果已有现有安装，为 Oracle 自动存储管理和集群升级做准备

在 Oracle Grid Infrastructure 安装期间，现有的 Oracle Clusterware 和集群 ASM 安装都将进行升级。

当集群成员运行 Oracle Grid Infrastructure 11g Release 2 (11.2) 时，新的集群软件将成为活动集群。

如果您打算安装 Oracle RAC，必须在安装 Oracle Database 11g Release 2 (11.2) 版本 Oracle RAC 之前，首先在所有集群节点上升级到 Oracle Grid Infrastructure 11g Release 2 (11.2)。

> 注意：所有 Oracle Grid Infrastructure 升级（现有 Oracle Clusterware 和 Oracle ASM 安装的升级）均为原地升级。

- 确定 Oracle 目录 (`oralInventory`) 位置
