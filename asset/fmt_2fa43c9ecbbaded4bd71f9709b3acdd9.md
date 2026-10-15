
上述文件系统某些用于特殊用途（`/sys`、`/proc`，以及其他），我们关注的是磁盘（`/dev/`、`/dev/sd*`，以及其他）。在此情况下，挂载的 Linux 分区是 `/dev/sda2`（为 `/boot` 目录提供启动所需的数据）和 `/dev/sda3`（提供了从根目录开始的 Linux 文件系统的空间）。

该系统还包含一个 Windows 分区（`/dev/sda1`）和一个 Linux 交换分区（`/dev/sda5`）。在 `/dev/sda2` 上还有一个较小的 `/boot` 分区（4MB）。在这种情况下，Linux 的根分区有 3.3GB 的磁盘空间，并位于 `/dev/sda3`。除非显式给出命令行，否则 `fdisk l` 命令会从 `/proc/partitions` 获取分区信息。

# 挂载文件系统

大多数磁盘分区都是自动挂载的。当你安装 Fedora、Ubuntu、SUSE 以及其他 Linux 系统时，会被要求创建分区并为这些分区指定挂载点。（其他安装程序则假设你在开始之前已经知道要分区）。当你启动 Linux 时，硬盘上所有列在 `/etc/fstab` 中的 Linux 分区通常都会被挂载。正因如此，本节重点介绍如何手动挂载其他类型的设备，使其成为你 Linux 系统的一部分。

`mount` 命令不仅用于挂载设备，还用于在你的 Linux 系统上挂载其他类型的文件系统。这意味着你可以存储来自其他操作系统的文件，或者使用适用于某些特定活动的文件系统（例如写入块

# 第 10 章：学习基础管理

（尺寸）。然而，对于普通 Linux 用户而言，该功能最常用的用途是让用户能够从软盘、CD-ROM或其他移动介质获取并处理文件。

### 注意

随着 Linux 2.6 内核增加了自动挂载功能并更改了可移动介质的方式（早期历史中的 Udev 和 HAT），你不再需要为 Linux 系统手动挂载可移动介质。然而，理解如何在 Linux 服务器上手动挂载和卸载文件系统仍然是一项非常有用的技能。

# 支持的文件系统

要查看当前系统上可用的系统类型，请使用 `cat /proc/filesystems`。表 10-5 显示了 Linux 支持的文件系统类型，尽管它们目前可能没有在使用，或者没有构建到你当前的内核中（因此它们可能需要作为模块加载）。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_362_0.png)

| Type | Description |
|---|---|
| adfs | Acorn 磁盘文件系统，RISC 操作系统上使用的标准文件系统 |
| befs | BeOS 操作系统使用的文件系统。 |
| cifs | 通用网络文件系统 (CIFS)，用于访问符合 SNIA CIFS 规范服务器的虚拟文件系统。通过 Samba 和 Windows 共享对 SMB 协议进行改进和标准的尝试。 |
| ext4 | ext3 文件系统的继者。它相比 ext3 有许多改进，例如支持高达 1 EB 的卷和高达 16 TB 的文件大小。（这已取代 ext3 成为 Fedora 的默认文件系统）。 |
| ext3 | ext 文件系统是 Linux 系统中最常见的。ext3 文件系统（也称为第三代扩展文件系统）包含日志功能，与 ext2 相比，提高了了文件系统从崩溃中恢复的能力。 |
| ext2 | 早期 Linux 系统的默认文件类型。功能与 ext3 相同，但 ext2 不包含日志功能。 |
| ext | 这是 ext 的第一个版本。现在已很少使用 |
| iso9660 | 演自 High Sierra 文件系统（CD-ROM 的原始标准）。High Sierra 标准的扩展（称为 Rock Ridge 扩展）允许 iso9660 文件系统支持文件名和 UNIX 风格的信息（如权限、所有权和链接）。数据 CD-ROM 通常使用这种文件类型。 |

# 第三部分：学习系统管理技能

## 表 10-5（续）

| Type | Description |
|---|---|
| kafs | AFS 客户端系统类型。用于分布式计算环境，以便与 Linux、Windows 和 Macintosh 客户端共享文件。 |
| minix | Minix 文件系统类型，最初用于 Minix 版本的 UNIX。它支持最多 30 个字符的文件名。 |
| msdos | MS-DOS 文件系统。你可以用它来挂载来自微软操作系统的软盘。 |
| vfat | 微软扩展 FAT (VFAT) 文件系统。 |
| umsdos | 带有扩展的 MS-DOS 文件系统，允许允许使用类似于 UNIX 的功能（包括长文件名）。 |
| proc | 不是真正的文件系统，而是指向 Linux 内核的文件系统接口。你可能不需要任何特殊设置来建立 proc 文件系统。许多实用工具依赖 `/proc` 获取 Linux 内核信息。 |
| reiserfs | ReiserFS 文件系统。ReiserFS 曾是若干 Linux 发行版的常用默认文件类型。然而，ext3 现在是目前 Linux 最常用的文件类型。 |
| swap | 用于交换分区。当 RAM 当前使用时，这些区域会被临时使用。数据被交换到交换区域，并在需要时返回 RAM。 |
| squashfs | 压缩的只读文件系统类型。Squashfs 在刻录 CD 上很流行，因为空间有限且是只读介质（如 CD 或 DVD）。 |
| nfs | 网络文件系统 (NFS) 类型的文件系统。NFS 用于在其他 Linux 或 UNIX 计算机上挂载文件系统。 |
| hpfs | 该文件系统用于只读挂载 OS/2 HPFS 文件系统。 |
| ncpfs | 与 Novell NetWare 文件系统相关。NetWare 文件系统可以通过网络挂载。 |
| ntfs | Windows NTFS 文件系统。取决于你拥有的发行版，它可能作为只读文件系统被支持（因此你可以从其挂载并复制文件）。 |
| affs | 用于 Amiga 计算机的文件系统。 |
| ufs | Sun Micros 操作系统上的文件系统（即 Solaris 和 SunOS）。 |

如果你想使用当前系统上不可用的文件系统类型（当你输入 `cat /proc/filesystems` 时），请尝试使用 `modprobe` 加载该文件系统的模块。例如，`modprobe ufs` 会将 UFS 文件系统类型添加到运行的内核中。使用 `man fs` 查看 Linux 文件系统的描述。

# 使用 fstab 分区定义挂载文件系统

你本地计算机上的硬盘分区以及你每天使用的远程文件系统可能都已设置为在启动 Linux 时自动挂载。`/etc/fstab` 文件包含了每个分区的定义，其中选项描述了分区的挂载方式。以下是 `/etc/fstab` 文件的示例：

| LABEL=/ | ext3 | defaults | 1 1 |
|---|---|---|---|
| LABEL=/boot | /boot | ext3 | defaults | 1 2 |
| /dev/devpts | /dev/pts | devpts | gid=5,mode=620 | 0 0 |
| /dev/shm | /dev/shm | tmpfs | defaults | 0 0 |
| /dev/proc | /proc | proc | defaults | 0 0 |
| /dev/sys | /sys | sysfs | defaults | 0 0 |
| /dev/sda1 | /sda1 | swap | | 0 0 |
| /dev/cdrom | /media/cdreorder | iso.9660 | exec,noauto,managed | 0 0 |
| /dev/sda2 | /sda2 | vfat | | 0 0 |
| /dev/fd0 | /fd0 | auto | | 0 0 |

所有列出的项目在启动时都会挂载，第四字段中设置为 `noauto` 的项除外。

任何用户都可以输入 `mount`（不带选项）来查看本地 Linux 系统上当前挂载了哪些文件系统。以下是 `mount` 命令的示例。它显示了一个包含根（/）文件系统的单磁盘分区（`/dev/sda1`），以及分别挂载在 `/proc` 和 `/dev` 上的 `proc` 和 `devfs` 类型。最后的一个条目显示了一个软盘，它被格式化为标准的 Linux 文件系统（`ext3`）并挂载在 `/mnt/floppy` 上。

```
$ mount

/dev/sda3 on / type ext3 (rw)

/dev/sda2 on /boot type ext3 (rw)

/dev/sda1 on /mnt/wine vfat (rw)

/dev/proc on /proc type proc (rw)

/dev/sys on /dev/pts type sysfs (rw)

/dev/devpts devpts (rw,gid=5,mode=620)
```
