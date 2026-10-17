
## 6.6. 解决方案：使用 `parted` 创建 GPT 分区

`Number Start End Size File system Name Flags`

```
(parted)
```

此示例显示了如何创建两个大小相等的主分区。

```
(parted) mkpart primary 0 50%

Warning: The resulting partition is not properly aligned for best performance.

Ignore/Cancel? I

(parted) mkpart primary 50% 100%

(parted)
```

通过 `print` 验证并使用 `quit` 退出。由于 `parted` 直接作用磁盘，因此不需要像 `fdisk` 那样使用 `(w/write)`。

```
(parted) print

Model: ATA VBOX HARDDISK (scsi)

Disk /dev/sdb: 8590MB

Sector size (logical/physical): 512B/512B

Partition Table: gpt

Disk Flags:

Number  Start  End     Size File system Name Flags

1 17.4KB 4295MB 4295MB primary

2 4295MB 8590MB 8590MB primary

(parted) quit

Information: You may need to update /etc/fstab.

[root@rhel7 ~]#
```

## 6.7. 练习：分区

1. 使用 `fdisk -l` 显示现有的分区和大小。
2. 使用 `df -h` 显示现有的分区和大小。
3. 比较 `fdisk` 和 `df` 的输出。
4. 在小磁盘上创建一个 `200MB` 的主分区。
5. 在大磁盘上创建一个 `400MB` 的主分区和两个 `300MB` 的逻辑驱动。
6. 使用 `df -h` 和 `fdisk -l` 验证你的工作。
7. 再次比较 `fdisk` 和 `df` 的输出。这两个命令都显示了新分区吗？
8. 使用 `dd` 命令对包含你 `200MB` 主分区的 `MBR` 进行备份。
9. 备份分区表，并包含你的 `400MB` 主分区和 `300MB` 逻辑驱动在备份中。
10. （可选）使用 `fdisk` 移除你所有的分区。然后恢复备份。

## 6.8. 解决方案：分区

1. 使用 `fdisk -l` 显示现有的分区和大小。

```
as root: # fdisk -l
```

2. 使用 `df -h` 显示现有的分区和大小。

```
df -h
```

3. 比较 `fdisk` 和 `df` 的输出。

某些分区会在两个输出中列出（可能是 `/dev/sda` 或 `/dev/hda`）。

4. 在小磁盘上创建一个 `200MB` 的主分区。

```
选择你添加的磁盘之一（此示例示例使用 /dev/sdc）

root@rhel53 ~# fdisk /dev/sdc
```

```
...
Command (for help): n
Command action

  e extended
  p primary partition (1-4)
Partition number (1-4): 1
First cylinder (1-261, default 1): 1
Last cylinder or size or +sizeK (1-261, default 261): +200m
Command (for help): w

The partition table has been altered!

Calling ioctl() to re-read partition table.

Syncing disks.
```

5. 在大磁盘上创建一个 `400MB` 的主分区和 `300MB` 的逻辑驱动。

选择你添加的磁盘之一（此示例使用 `/dev/sdb`）

```
fdisk /dev/sdb

inside fdisk : n p 1 +400m enter --- n e 2 enter enter --- n 1 +300m (twice)
```

6. 使用 `df -h` 和 `fdisk -l` 验证你的工作。

```
fdisk -l ; df -h
```

7. 再次比较 `fdisk` 和 `df` 的输出。两个命令都显示了新分区吗？

新创建的分区通过 `fdisk` 可见。但它们没有被 `df` 显示。

8. 使用 `dd` 命令对包含你 `200MB` 主分区的 `MBR` 进行备份。

```
dd if=/dev/sdc of=bootsector.sdc count=1 bs=512
```

9. 备份分区表，包含你的 `400MB` 主分区和 `300MB` 逻辑驱动。确保逻辑驱动在备份中。

```
sfdisk -d /dev/sdb > parttable.sdb.fdisk
```

## 第 7 章 文件系统

当你完成硬盘分区后，你可以在每个分区上放置文件系统。

本章基于上一节的分区，并为下一节做准备，在下一节我们将挂载文件系统。

## 7.1. 关于文件系统

文件系统是在你的分区上组织文件的一种。除了基于文件的存储外，文件系统通常还包含目录和访问控制，并包含有关文件的元信息，如访问时间、修改时间和文件所有权。

文件名的属性（长度、字符集等……）取决于你选择的文件系统。目录通常被实现为文件，你将学习它是如何实现的！文件系统中的访问控制通过用户所有权（以及组所有权和成员身份关系）结合一个或多个访问控制列表来跟踪。

### 7.1.1. man fs

通过输入 `man fs` 访问关于文件系统的手册页。

```
[root@rhel65 ~]# man fs
```

### 7.1.2. /proc/filesystems

Linux 内核会在 `/proc/filesystems` 中通知你当前加载的文件系统驱动程序。

```
root@rhel65 ~# cat /proc/filesystems | grep -v nodev

ext2
iso9660
ext3
```

### 7.1.3. /etc/filesystems

`/etc/filesystems` 文件包含自动检测的文件系统列表（以防在使用 `mount` 命令时不使用 `-t` 参数）。

该文件的帮助由 `man mount` 提供。

```
[root@rhel65 ~]# man mount
```
