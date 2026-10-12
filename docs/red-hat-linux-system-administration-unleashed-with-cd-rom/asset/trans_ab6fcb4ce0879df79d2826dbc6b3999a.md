
```
pd: pd version 1.0, major 45, cluster 64, nice 0
pda: Sharing parport1 at 0x378
pda: ep at 1.0, Shuttle EPAT chip c3 at 0x378, mode 5 (EPP-32), delay 1
pda: SyQuest EZ135A, 262144 blocks [128M], (512/16/32), removable media
pda: pda1
```

要访问此设备，您必须在 /dev 目录中创建适当的设备特殊文件。这些设备应该已经存在于您的 Red Hat 系统上；然而，如果不存在，文件 /usr/src/linux/Documentation/paride.txt 中有一个脚本可以为您创建它们。一旦这些设备创建完成，它们就像其他 ATAPI/IDE 设备一样被访问，只是设备名称除外。现在我们已经了解了 Linux 可用的各种类型的可移动媒体设备，让我们继续讨论授予用户访问权限的话题。

## 授予用户访问权限

在不授予 root 访问权限的情况下允许访问系统上的可移动媒体设备有多种方法。本节介绍其中两种选项，一种专门针对 DOS 文件系统，另一种是让用户能够挂载可移动媒体而不损害系统安全的方法。它还介绍了使用自动挂载程序挂载可移动媒体以及这样做的一些优点和缺点。请注意，您可能不希望将可移动媒体设备的访问权限授予服务器系统上的用户。这里描述的方法最适合工作站。

## mtools 软件包

在 Linux 下授予对可移动设备的访问权限的一种方法是使用 mtools 软件包。该软件包包含许多与 DOS 命令相对应的命令，用于访问 DOS 文件系统类型，例如 FAT 和 VFAT。表 10.4 显示了一些最常见的 mtools 命令、其 DOS 对应项（如果存在）以及它们的作用。

表 10.4 mtools 命令

| mtools 命令 | DOS 命令 | 描述 |
|---|---|---|
| mattrib | attrib | 设置文件上的 DOS 文件属性。 |
| mbadblocks |  | 扫描磁盘上的坏块并标记它们。 |
| mcd | cd | 在 DOS 文件系统上更改目录。 |

### 表 10.4 继续

| mtools 命令 | DOS 命令 | 描述 |
|---|---|---|
| mcopy | copy | 将文件复制到 DOS 文件系统或从其中复制。 |
| mdel | del | 从 DOS 文件系统删除文件。 |
| mdeltree | deltree | 删除目录及其下的所有文件。 |
| mdi | rdir | 显示目录列表。 |
| mdu |  | 显示 DOS 文件系统的磁盘空间使用情况。 |
| mformat | format | 对指定设备执行最小的 DOS 格式化。 |
| mlabel | label | 在 DOS 文件系统上设置卷标。 |
| mmd | md | 在 DOS 文件系统上创建目录。 |
| mmove | move | 在 DOS 文件系统上移动或重命名文件或目录。 |
| mrd | rd | 从 DOS 文件系统删除目录。 |
| mren | ren | 在 DOS 文件系统上重命名文件。 |
| mtype | type | 显示 DOS 文件系统上的文本文件。 |
| mzip |  | 发出 Zip 磁盘专用命令。允许您弹出、写保护、移除写保护等。 |

这些命令访问可能包含 DOS 文件系统的各种设备的能力由 /etc/mtools.conf 文件决定。在默认的 Red Hat 安装中，该文件如下所示：

/etc/mtools.conf

```
# Example mtools.conf files. Uncomment the lines which correspond to
# your architecture and comment out the "SAMPLE FILE" line below

# Linux floppy drives
drive a: file="/dev/fd0" exclusive 1.44m
drive b: file="/dev/fd1" exclusive 1.44m

# First SCSI hard disk partition
#drive c: file="/dev/sda1"

# First IDE hard disk partition
#drive c: file="/dev/hda1"

# # dosemu floppy image
# drive m: file="/var/lib/dosemu/diskimage"

# dosemu hdimage
drive n: file="/var/lib/dosemu/hdimage" offset=8832

# Atari ramdisk image
# drive o: file="/tmp/atari_rd" offset=136

# ZIP disk for Solaris:
# Drive X is ZIP-100 at target 5
# drive X: file="/dev/rdsk/c0t5d0s2" partition=4 scsi=1 nodelay

# ZIP disk for SunOS:
# Zip drive is at target 5, which default kernel calls tape st1 !!
# drive Y: file="/dev/rdsk/c0t5d0s2" partition=4 scsi=1 nodelay

# autoselect zip drive/floppy on HP-UX 9/10
# drive a: file="/dev/rdsk/c0t0d5s0" exclusive partition=4
# drive a: file="/dev/rdsk/c0t0d5s0" exclusive partition=4
# drive a: file="/dev/rfloppy/c0t0d5s0" exclusive

#
# A/UX target 5 on 1st scsi bus jaz or zip
# drive X: file="/dev/rdsk/c0t5d0s31" partition=4

# Some examples for BeOS.
# floppy drive. hardcoded in devices.c, so no real need to define it here
#drive a: file="/dev/floppy_disk" exclusive
# ZIP drive on SCSI ID 6
#drive z: file="/dev/scsi_disk_060" offset=16384 fat_bits=16

# SCO Unix 3.2v4
# # Floppy disk drives
#
# drive a: file="/dev/install" exclusive
# drive b: file="/dev/install1" exclusive
#
# SCSI hard disk partitions
#
# drive c: file="/dev/dsk/0sC"
# drive d: file="/dev/dsk/0sD"
# drive e: file="/dev/dsk/0sE"
# drive f: file="/dev/dsk/0sF"
# drive g: file="/dev/dsk/0sG"
# drive h: file="/dev/dsk/0sH"

# # uncomment the following line to display all file names in lower
# # case by default
# mtools_lower_case=1
```

文件中的注释描述了每个条目的用途，而 mtools 的手册页则更详细地描述了如何向此文件添加条目。此外，mtools 套件最详细的文档可以通过在您的 Red Hat 系统上发出命令

`info mtools`

或使用 Emacs 的 info 模式查找 mtools 来访问。

mtools 套件明显的缺点是它仅适用于 DOS 文件系统。除此之外，mtools 套件可能是解决让用户访问可移动设备问题的一个简单解决方案。如果其主要目的是实现“ Sneakernet ”文件传输，这可能就足够了。

## 授予用户挂载权限

系统管理员可用的另一个选项是通过 mount 命令的特殊选项授予用户挂载软盘和 CD-ROM 驱动器等可移动设备的权限。现代 mount 版本都支持此选项，启用它包括两个步骤。第一步是为可移动媒体设备创建挂载点，第二步是修改 `/etc/fstab` 以设置适当的挂载选项以允许用户访问。让用户能够挂载软盘或 CD-ROM 等可移动媒体并不是一个轻率的决定。然而，它可能是有用的，以便用户可以在未联网的系统之间传输文件。

## 创建挂载点

创建挂载点听起来可能是一个微不足道的练习，但以下是一些可能有帮助的建议：

- 为挂载点使用描述性名称，例如 /mnt/dosa 代表 Windows 或 DOS 中的 A 驱动器。
- 为不同文件系统类型创建多个挂载点，以便用户不必学习挂载选项。

举例来说，考虑以下情况。用户工作站都只有一个软盘驱动器和一个可作为 /dev/cdrom 访问的 IDE CD-ROM 驱动器。您希望允许用户挂载用于 Linux（扩展 2 文件系统）或 DOS/Windows 格式的软盘以及数据 CD。在这种情况下，我会创建的挂载点为：

- /mnt/dosA 用于 DOS/Windows 格式的软盘
- /mnt/fd0 用于 Linux 格式的软盘
- /mnt/cdrom 用于数据 CD

如果我后来在系统上添加一个 Zip 驱动器并希望允许用户在其上挂载 DOS 或 Linux 格式的磁盘，我会添加额外的挂载点：

- /mnt/zip 用于 Linux 格式的 Zip 磁盘
- /mnt/zipdos 用于 DOS/Windows 格式的磁盘

## 修改 /etc/fstab

为了支持这些类型的驱动器的用户挂载，您必须修改文件系统表 /etc/fstab。以下是此文件中的一个示例行，演示了您必须指定的两个选项以允许普通用户挂载文件系统：

### /etc/fstab 条目

```
/dev/fd0  /mnt/fd0  ext2  noauto,nosuid,user,rw  1  0
```

在此条目中，我们指定了多个选项。其中第一个是 noauto 选项，表示此文件系统不应自动挂载（即使用 mount -a 选项）。这在启动时尤其重要，因为您很可能没有软盘在磁盘驱动器中，并且您不希望等待软盘设备超时。下一个选项是 nosuid 选项，这是一个重要的安全考虑因素，禁止从软盘执行 setuid 和 setgid 程序。user 选项是允许用户挂载此文件系统的关键。此选项只能在 /etc/fstab 文件中设置，它告诉 mount 程序禁用当前用户是否为 root 的检查。这意味着普通用户现在只需发出命令即可将软盘设备挂载到挂载点 /mnt/fd0

```
mount /mnt/fd0
```
