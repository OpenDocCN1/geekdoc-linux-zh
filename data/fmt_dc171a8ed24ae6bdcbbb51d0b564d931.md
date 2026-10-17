
| `/dev/mapper/vg00-data` | 1188 | 18432 | 20480 | 326 | 900 | 1000 |

8. 上述命令对 `root` 用户可用；但普通用户可以使用 `quota` 命令查看自己的用户配额。`root` 用户也可以使用该命令，还可以查看其他：

## 注意 33
要配置和管理 XFS 文件系统（全部或部分），必须使用 `xfs_quota` 命令。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

### 摘要

- 磁盘设备由位于 `/dev` 目录下的设备文件表示。这些设备文件指定了数据传输类型、Linux 内核中设备的主号以及特定设备的设备号。
- 每个设备都必须包含一个文件系统，并通过 `mount` 命令将其挂载到 Linux 目录以便使用。可以使用 `unmount` 命令卸载文件系统。在挂载和卸载操作期间，用于挂载设备的目录不能被任何已登录的用户使用。
- 存储设备（如硬盘和 SSD）在这些这些分区上创建分区之前必须先进行分区。要对存储设备进行分区，可以使用多种工具，包括 `cfdisk`、`gdisk` 和 `parted`。
- Linux 支持许多文件系统；每个文件系统都针对特定用途，多个文件系统可以挂载到目录树上不同的挂载点。你可以使用 `mkfs` 命令及其变体在设备上创建文件系统。
- LVM（逻辑卷管理）可以从系统中存储设备多个分区内的空闲空间创建逻辑卷。与分区一样，逻辑卷可以包含文件系统并挂载到 Linux 目录。它们允许对存储进行轻松扩展和重新配置。
- 大多数移动媒体设备被 Linux 系统识别为 SCSI，并由桌面环境自动挂载。
- 使用 `df` 和 `du` 命令监控磁盘使用情况非常，以避免存储空间和节点（inodes）耗尽。同样，使用 `fsck` 命令及其变体检查错误也是重要的。
- 你可以使用磁盘配额来限制每个用户在文件系统上的空间。

### 关键术语

`/dev` 目录

`/etc`

`/etc/mtab`

`/proc/devices`

坏块

`blkid` 命令

块

块设备

`cfdisk` 命令

字符设备

磁道

设备文件

`d (df 空闲空间)` 命令

磁盘配额

`d (目录用法)` 命令

`elabel` 命令

`edquota` 命令

`eject` 命令

`extabfile` 命令

`fdisk` 命令

文件系统损坏

格式化

`fsck (文件系统检查)` 命令

`fuser` 命令

`gdisk (GPT 分区)` 命令

逻辑卷 (LV)

`lsblk` 命令

`lsub`

`lvcreate` 命令

`lvdisplay` 命令

`lveend` 命令

主号

从号

`mkmfs (创建文件系统)` 命令

`mkmofs` 命令

`mkswap` 命令

`mount` 命令

挂载点

挂载

`ed (GPT)` 分区

`partprobe` 命令

物理范围 (PE) 大小

物理卷 (PV)

`prcreate` 命令

`pvsize` 命令

`quota` 命令

`quotaoff` 命令

`quotam` 命令

配额

`parted` 命令

`resize2fs` 命令

根文件系统

扇区

软限制

`swapoff` 命令

`swapon` 命令

同步

`tune2fs` 命令

`udev` 守护进程

`udevadm`

`unmount` 命令

通用标识符 (UUID)

`vgreate` 命令

`vdisplay` 命令

`vgend` 命令

虚拟文件系统

卷组 (VG)

`fsadmin` 命令

`sdb` 命令

`fs` 命令

`fgrow` 命令

`fsinfo` 命令

`fs quota` 命令

`fsck repair` 命令

### 复习题

1. 以下哪个命令用于在 GPT 存储设备上创建分区？
a. `gdisk`
b. `cfdisk`
c. `fdisk`
d. `parted`

2. 存储设备上的分区用文件系统格式化后，该设备上的所有分区必须使用相同的文件系统。
a. 正确
b. 错误

3. 你想查看某些正在被系统使用的分区。你可以使用哪个命令？（选择所有适用项）
a. `cat /etc/fstab`
b. `df -hT`
c. `cat /etc/mtab`
d. `ls /sys/block`

4. Jaime 在他的系统中安装了两个新的 SAS SSD。他可以使用它们进行数据存储和检索，但他必须做什么？（选择所有适用项）
a. 挂载这两个 SSD 以便操作系统可以访问。
b. 在每个 SSD 上挂载一个文件系统。
c. 在每个 SSD 上创建一个或多个分区。
d. 使用 `vi` 编辑 `/etc/mtab` 并为 SSD 创建条目。
e. 挂载在两个 SSD 上创建的任何分区，以便操作系统可以访问。
f. 将 SSD 上创建的所有分区用 Linux 识别的有效文件系统进行格式化。

5. 鉴于来自 `/etc/fstab` 的以下输出，哪些文件系统将被 `fsck` 命令自动检查？

```
/dev/sda1   ext4    defaults        1 1

/dev/sda2   swap    defaults        0 1

/dev/sda3   ext4    defaults        0 1

/dev/sda4   ext4    defaults        0 1

/dev/home   ext4    defaults        0 1

/dev/sr0    media/dev iso9660  ro      0 0
```
