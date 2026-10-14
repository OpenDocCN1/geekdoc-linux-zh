
```bash
# mkdir /mnt/ul                              创建挂载点
# mount -t ext3 /dev/mapper/vgsub-lvm_ul /mnt/ul  挂载卷
$ df -m /mnt/ul                               检查磁盘空间
文件系统             1M-块 已用 可用 用% 挂载在
/dev/mapper/vgsub-lvm_ul      12        2       10 11% /mnt/ul
```

此时，文件系统只包含一个 `lost+found` 目录：

```bash
$ ls /mnt/ul
lost+found
```

将一个大文件拷贝到新系统。例如，从 `/boot` 目录选择一个内核文件并将其拷贝到 `/mnt/ul`：

```bash
$ cp /boot/vmlinuz-* /mnt/ul  拷贝大文件到 /mnt/ul
$ df -m /mnt/ul 看到 /mnt/ul 上已使用 4MB 
文件系统             1M-块 已用 可用 用% 挂载在
/dev/mapper/vgsub-lvm_ul      12        4       10 27% /mnt/ul
```

在拷贝的文件上运行 `md5` 以备日后检查，例如：

```bash
$ md5 /mnt/ul/vmlinuz-2.6.25-default  检查 md5
8d0dc0347d6eb3d6f2b04e71ef25 /mnt/ul/2.6.25-default
```

## 扩展 LVM 卷

假设空间不足，你想为 LVM 卷添加空间。要做到这一点，请卸载卷并使用 `resize` 命令。之后，你必须用 `fsck` 和 `resize2fs` 检查文件系统：

```bash
$ umount /mnt/ul  卸载卷
$ lvresize --size 16G /dev/vgsub/lvm_ul  扩展逻辑卷 lvm_ul 到 16 GB
逻辑卷 lvm_ul 已调整大小
$ fsck -f /dev/vgsub/lvm_ul 第 1通过：检查节点、块和大小
e2fsck 14.0.2 (12-Jul-2007)通过 1
第 2通过：检查目录结构
第 3通过：检查连接性
第 4通过：检查计数
第 5通过：检查摘要
/dev/vgsub/lvm_ul:12/3072 文件 (25.0% 非连续)，3379/12288 块
$ resize2fs /dev/vgsub/lvm_ul  调整文件系统
resize2fs 14.0.2 (12-Jul-2007)正在调整 /dev/vgsub/lvm_ul 的文件系统大小为 16384 (k) 块。
/dev/vgsub/lvm_ul 文件系统为 16384 块。
```

在示例中，卷和文件系统都调整到了 16。接下来，再次卸载卷并检查磁盘空间以及你创建的 `md5sum`：

```bash
$ mount -t ext3 /dev/mapper/vgsub-lvm_ul /mnt/ul  重新挂载卷
$ df -m /mnt/ul 看到 16MB 中使用了 4MB
文件系统             1M-块 可用 用% 挂载在
/dev/mapper/vgsub-lvm_ul 16 4 20% /mnt/ul
$ md5 /mnt/ul/vmlinuz-2.6.25-default  重新检查 md5
8d0dc0347d6eb3d6f2b04e71ef25 /mnt/ul/2.6.25-default
```

新挂载的卷现在大小为 16MB，而不是 10MB。

## 缩小 LVM 卷

如果你想从现有的 LVM 卷中获取未使用空间，也可以使用 `lvresize` 命令。之前，在调整大小之前卸载卷并运行 `e2fsck`（检查文件系统）和 `resize2fs`（调整到较小大小）：

```bash
# umount /mnt/ul
$ e2fsck -f /dev/vgsub/lvm
e2fsck 14.0.2 (12-Jul-2007)文件系统大小（根据超级块）为 16384 块
设备物理大小为 8192 块
第 1通过：检查节点、块和大小
...
/dev/vgsub/lvm:12/3072 文件 (8.3% 非连续，3531/16384 块)
# resize2fs /dev/vgsub/lvm 12M  调整文件系统
resize2fs 14.0.2 (12-Jul-2007)正在调整 /dev/vgsub/lvm 的文件系统大小为 12288 (lk) 块。
/dev/vgsub/lvm 文件系统现在是 12288 块。
# lvresize --size 12M /dev/vgsub/lvm_ul
警告：正在将活动卷缩小到 12.00 MB
这可能会破坏你的数据（文件系统等）。
你确定要缩小 lvm_ul 吗？[y/n]: y
缩小逻辑卷 lvm_ul 到 8.00 MB
逻辑卷 lvm_ul 已调整大小
# mount -t ext3 /dev/mapper/vgsub-lvm_ul /mnt/ul  重新挂载卷
$ df -m /mnt/ul 看到 12MB 中使用了 4MB
文件系统      1M-块 可用 用% 挂载在
/dev/mapper/vgsub-lvm_ul  12        4        20% /mnt/ul
```

新挂载的卷现在显示为 12MB而不是 16MB。

## 删除 LVM 卷和卷组

要从卷组中删除 LVM 逻辑卷，使用如下命令 `lvremove` 命令：

```bash
# lvremove /dev/vgsub/lvm_ul
确定要删除活动逻辑卷 "lvm_ul" 吗？[y/n]: y
逻辑卷 "lvm_ul" 已删除
```

要删除现有的 LVM 卷组，使用 `vgremove` 命令：

```bash
# vgremove vgsub
卷组 "vgsub" 已删除
```

还有更多操作 LVM 的方法。请参考 LVM HOWTO 获取更多信息（http://tldp.org/HOWTO/HOWTO）。

## 总结

在 Linux 中创建和管理文件系统是 Linux 系统管理的关键部分。Linux 包含多种标准 Linux 文件系统支持（`ext2`, `ext3`, `reiserfs` 等）。它还可以创建和管理 Windows 文件系统类型（`VFAT`, `NTFS` 等）以及旧版和特殊的 Linux 和 Unix 文件系统类型（如 `minix`, `jfs` 和 `xfs`）。

可以使用 `fdisk` 和 `parted` 命令对硬盘进行分区。用于处理文件系统的工具包括创建文件系统的（`mkfs`）、查看和修改文件系统属性的（`tune2fs` 和 `dumpe2fs`）、挂载/卸载文件系统的（`mount` 和 `umount`）以及检查问题的（`badblocks` 和 `fsck`）。要查看文件系统使用了多少空间，请使用 `df` 和 `du` 命令。

# 8

备份与可移动介质

Linux 中的数据备份传统上通过运行命令对要备份的文件进行归档和压缩，然后将该备份存档写入磁带。近年来，归档工具、压缩技术和备份介质的选择大幅增加。对于许多人来说，磁带归档已被通过网络、其他硬盘、或到 CD、DVD 以及其他低成本可移动介质进行数据备份的技术所取代。

### 本章内容

- 使用 `tar` 创建备份归档
- 使用 `gzip`、`bzip2` 和 `lzop` 压缩备份
- 通过 SSH 进行网络备份
- 使用 `rsync` 进行网络同步备份
- 使用 `mkisofs` 创建备份 ISO 镜像
- 使用 `dcdrecord` 将备份镜像刻录到 CD 或 DVD

本章详细介绍了一些用于备份和恢复您的关键数据的有用工具。本章的第一部分详细说明了如何使用 `tar`、`gzip` 和 `rsync` 等基础工具进行备份。

# 将数据备份到压缩归档

如果你来自 Windows 背景，你可能习惯使用 WinZip 和 PKZIP 等工具，它们在一个应用程序中同时对组文件进行归档和压缩。Linux 提供了独立的工具来将组文件收集到单个存档中（如 `tar`），并对该归档进行压缩以实现高效存储（`gzip`、`bzip2` 和 `lzop`）。不过，你也可以通过 `tar` 命令的额外选项完成这两个步骤。

# 使用 tar 创建备份归档

`tar` 命令代表 tape archiver（磁带归档器），起源于早期的 Unix 系统。虽然磁带是 `tar` 最初写入的常用介质，但今天 `tar` 通常用于创建一个可以分发到各种介质的存档文件。

# 第8章：备份与可移动介质

`tar` 命令功能丰富的特点体现在 `tar` 提供的几十个选项上。然而，`tar` 的基本操作用于创建备份归档 (`-c`)、从归档中提取文件 (`-x`)、比较归档之间的差异 (`-d`) 以及更新归档中的文件 (`-u`)。你还可以向现有归档中添加 (`-r` 或 `-a`) 文件，或从现有归档中删除 (`-d`) 文件，或者列出归档的内容 (`-t`)。
