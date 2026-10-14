
通常，大多数 Linux 系统会自动识别系统中的磁盘，并在安装过程中建议一个合理的方案。同样，当你向系统内部连接一个新磁盘时，Ubuntu 会显示一个对话框，询问你是否要配置该磁盘。安装过程中的分区将在第 2 章“安装 Ubuntu”中进行介绍；当系统已运行时使用图形化分区将在第 23 章“添加硬件和外设”中进行详细说明。

如果你对磁盘进行分区并挂载，或者连接了一个已经分好区的现有磁盘，在将其挂载到某处之前，你的系统无法访问它。本节将讨论如何使用 Linux `mount` 命令挂载磁盘、可用的常用选项，以及如何通过将磁盘添加到系统文件系统配置文件 `/etc/fstab` 中，从而将特定磁盘挂载为系统启动过程的一部分。

## 挂载文件系统

连接磁盘后，你始终可以使用 Linux `fdisk -l` (list) 选项查询其包含的文件系统，例如所示：

```
sudo fdisk -l
/dev/sda: 250.0 GB, 250059350016 bytes
heads, 63 sectors/track, 30401 cylinders
cylinders = cylinders of 16065 * 512 = 8225280 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|--------|------|-------|-----|--------|----|--------|
| /dev/sda1 | | 1 | 1306 | 10490413 | 83 | Linux |
| /dev/sda2 | | 1307 | 2090 | 6297480 | 82 | Linux swap |
| /dev/sda3 | * | 2091 | 2122 | 257040 | 83 | Linux |
| /dev/sda4 | | 2123 | 30399 | 227135002 | 7 | W95 Ext’d (LBA) |
| /dev/sda5 | | 2123 | 2645 | 4200966 | 83 | Linux |
| /dev/sda6 | | 2646 | 6562 | 31463271 | 83 | Linux |
| /dev/sda7 | | 6563 | 10478 | 31455238 | 83 | Linux |
| /dev/sda8 | | 10479 | 30399 | 160015401 | 83 | Linux |

```
/dev/hde: 250.0 GB, 250059350016 bytes
heads, 63 sectors/track, 30401 cylinders
cylinders = cylinders of 16065 * 512 = 8225280 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|--------|------|-------|-----|--------|----|--------|
| /dev/hde1 | | 1 | 30401 | 24419601 | 83 | Linux |

`fdisk` 命令列出系统中检测到的所有磁盘上的分区。你可以使用 `fdisk` 命令列出特定设备的分区，如下所示：

```
sudo fdisk -l /dev/sda
/dev/sda: 250.0 GB, 250059350016 bytes
heads, 63 sectors/track, 30401 cylinders
cylinders = cylinders of 16065 * 512 = 8225280 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|--------|------|-------|-----|--------|----|--------|
| /dev/sda1 | | 1 | 1306 | 10490413 | 83 | Linux |
| /dev/sda2 | | 1307 | 2090 | 6297480 | 82 | Linux swap |
| /dev/sda3 | * | 2091 | 2122 | 257040 | 83 | Linux |
| /dev/sda4 | | 2123 | 30399 | 227135002 | 7 | W95 Ext’d (LBA) |
| /dev/sda5 | | 2123 | 2645 | 4200966 | 83 | Linux |
| /dev/sda6 | | 2646 | 6562 | 31463271 | 83 | Linux |
| /dev/sda7 | | 6563 | 10478 | 31455238 | 83 | Linux |
| /dev/sda8 | | 10479 | 30399 | 160015401 | 83 | Linux |

该命令的首要参数是你想要查询的磁盘基名称，而不是特定分区。你可以通过 `/proc/partitions` 文件获取类似信息（尽管格式较不可用），运行系统使用它来跟踪所有使用的磁盘和分区。上一个示例该文件内容如下：

```
cat /proc/partitions
```

| name | blocks |
|------|--------|
| sda | 244198584 |
| sda1 | 10490413 |
| sda2 | 6297480 |
| sda3 | 257040 |
| sda4 | 1 |
| sda5 | 4200966 |
| sda6 | 31463271 |
| sda7 | 31455238 |
| sda8 | 160015401 |
| hde | 244198584 |
| hde1 | 4416001 |
| hdf | 244198584 |
| hdf1 | 4416001 |

一旦识别了新磁盘上的分区（并可能知道你想挂载哪些），使用 `mount` 命令挂载它们就很简单。你始终需要显式挂载未列在 `/etc/fstab` 文件中的文件系统（下一节将详细说明）。例如，以下命令将分区 `/dev/sda5` 挂载到挂点 `/mnt/tmp`：

```
sudo mount /dev/sda5 /mnt/tmp
```

挂载包含 ext2 文件系统或系统支持的文件系统分区时，不需要指定分区/设备使用的文件系统类型。如果是其他类型，你必须使用 `mount` 命令的 `-t` 选项识别文件系统类型，后跟该文件系统的名称，如下例所示，将 XFS 文件系统 `sda6` 挂载到挂点 `/mnt/xfs`：

```
sudo mount -t xfs /dev/sda6 /mnt/xfs
```

`-t` 选项实际上会导致 `mount` 命令首先查找特殊的、特定文件系统的挂载文件 `/sbin/mount.type`，其中 `type` 是该类型文件系统的名称。这些文件系统命令通常在使用 Synaptic 包管理器或 `apt-get` 与其他类型文件系统的管理工具一起安装，如第 20 章“添加和更新软件”所述。

你可以使用 `-t` 选项指定的文件系统类型有 dfs, affs, autofs, coda, cramfs, devpts, efs, ext, ext2, ext3, hfs, hpfs, iso9660, jfs, minix, msdos, ntfs, proc, qnx4, ramfs, reiserfs, romfs, smbfs, sysv, tmpfs, udf, ufs, umsdos, atm, xenix, xfs 和 xiafs。

网络文件系统需要额外的选项，例如 NFS 文件系统、SMB/CIFS 文件系统等。这些选项是高度特定文件系统的，因此我在这里不列出。相反，我将关注你可能想要挂载的 SMB/CIFS 文件系统。其他常用的挂载选项将在节讨论。

## 启动时挂载文件系统

当 Ubuntu 启动时，主磁盘上的引导块识别文件系统，它使用一个配置文件确定系统上有哪些内核和相关的模块。根文件系统最初以只读模式挂载，以便验证其完整性。完成后，它会被重新挂载为读写模式，系统会验证任何其他文件系统的一致性。文件系统列表包含 `/etc/fstab`（文件系统表）文件中。若要在系统启动时挂载新文件系统或更改系统与特定类型设备的交互方式，你需要在 `/etc/fstab` 文件中添加或自定义条目。我一个系统中 `/etc/fstab` 文件的一个部分如下（你的文件将有所不同）：

| Device | Boot | Start | End | Blocks | Id | System |
|--------|------|-------|-----|--------|----|--------|
| /dev/sda1 | | 1 | 1306 | 10490413 | 83 | Linux |
