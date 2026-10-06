
[@server1 root]# `ls -1 /dev/fd0`

`br-rw---- root floppy 2, 0 Feb 23 16:02 /dev/fd0`

[@server1 root]#

从上述输出的最左字符可以看出，`/dev/fd0` 是块设备。表 6-1 提供了一些常见设备文件及其类型的列表。

### 表 6-1 常见设备文件

| 设备文件 | 说明 | 块或字符 |
| :--- | :--- | :--- |
| `/dev/fd0` | 系统上的第一块软磁盘 | 块 |
| `/dev/fd1` | 系统上的第二块软磁盘 | 块 |
| `/dev/hda1` | 第一块 IDE 硬盘上的第一个分区（主设备） | 块 |
| `/dev/hdb1` | 第二块 IDE 硬盘上的第一个分区（主从设备） | 块 |
| `/dev/hdc1` | 第三块 IDE 硬盘上的第一个分区（次主设备） | 块 |

### 表 6-1 常见设备文件（续）

| 设备文件 | 说明 | 块或字符 |
| :--- | :--- | :--- |
| `/dev/hdd1` | 第四块 IDE 硬盘上的第一个主分区（次从设备） | 块 |
| `/dev/sda` | 第一块 SCSI 硬盘上的第一个主分区 | 块 |
| `/dev/sdb1` | 第二块 SCSI 硬盘上的第一个主分区 | 字符 |
| `/dev/tty1` | 系统上的第一个本地终端 (Ctrl+Alt+F1) | 字符 |
| `/dev/tty2` | 系统上的第二个本地终端 (Ctrl+Alt+F2) | 字符 |
| `/dev/tty0` | 系统上的第一个本地终端 (COM1) | 字符 |
| `/dev/tty1` | 系统上的第二个本地终端 (COM2) | 字符 |
| `/dev/lp0` | 第一个本地并行端口 (LPT1) | 字符 |
| `/dev/null` | 特殊空设备 | 字符 |
| `/dev/st0` | 第一台磁带机 | 字符 |
| `/dev/usb0` | 第一个 USB 设备 | 字符 |

# 文件系统 237

```
128 ptm

136 pts

162 raw

180 usb

216 rfcomm
```

```
块设备:

  1 ramdisk

  2 fd

  3 ide0

  9 md

  22 idel

  253 device-mapper

  254 mdp
```
```
[root@server1]#_
```

## 6

## 文件系统

回想第 2 章“准备安装 Linux”，文件必须存储在硬盘上一种名为“文件系统”的定义格式中，以便操作系统能够对其进行操作。文件系统的类型决定了在物理磁盘上管理文件的方式。每个文件系统可以有不同的文件存储方法，以及使文件系统具有错误健性的特性。尽管有许多不同类型的文件系统，但正如第 5 章讨论的，文件系统共享三个共同组件：超级块（superblock）、索引节点表（inode table）和数据块（data blocks）。在结构层面，这三个组件协同工作以组织文件，并允许快速访问和检索数据。存储介质（如软磁盘、硬盘和 CD-ROM）在在使用之前需要用文件系统进行格式化。

在设备上创建文件系统通常被称为格式化。

# 文件系统类型

如所述，Linux 操作系统中有许多可用的文件系统。每个文件系统都有其自身的优缺点，因此某些文件系统更适合某些任务，而不适合其他任务。Linux 的优势之一是，你不需要在系统中仅使用一种类型的文件系统；你可以在同一个目录树下使用多个格式化为不同文件系统的不同设备。此外，无论 Linux 系统使用一个文件系统还是二十个文件系统，文件和目录在整个目录树中的显示形式都是相同的。表 6–2 列出了 Linux 中可用的某些文件系统。要获取文件系统类型及其性的完整列表，可以参考互联网上的 Filesystem HOWTO：`http://www.tld.org/HOWTO/Filesystems-HOWTO.html`。

# 第 6 章 Linux 文件系统管理

表 6-2 Linux Linux 文件系统

| 文件系统 | 说明 |
| :--- | :--- |
| bfs | 启动文件系统——一种小型、可启动的文件系统，用于存放启动所需的运行；通常用于 UNIX。 |
| cdfs | 紧凑磁盘文件系统——用于将 CD-ROM 上的所有轨道视为普通文件查看的文件系统。 |
| ext2 | 第二扩展文件系统——Linux 上使用的传统文件系统，它支持访问控制列表（个人用户权限）。此外，它保留了作为基于 Minix 文件系统的原始扩展文件系统新版本的名称。 |
| ext3 | 第三个扩展文件系统——ext2 的变体，允许日志记录，并具有更快的启动和恢复速度。 |
| hfs | 分级文件系统——Apple Macintosh 的原生文件系统。 |
| hpfs | 高性能文件系统——一种 IBM OS/2 文件系统，提供长文件名支持，并针对磁盘数据操作进行了优化。 |
| iso9660 | CD-ROM 文件系统，源自国际标准组织 9660，用于访问存储在 CD-ROM 上的数据。 |
| minix | Torvalds 在 Linux 开发早期使用的 MINIX 文件系统。 |
| mdos | DOS 文件系统。 |
| ntfs | 新技术文件系统——微软为 NT 和 2000 操作系统开发的专有文件系统；目前在 Linux 下作为只读文件系统可用。 |
| reiserfs | 一种类似于 ext3 的日志文件系统，更适合与数据库配合。 |
| udf | 通用磁盘格式文件系统——用于写入 CD-R、CD-RW 或 DVD 的程序的文件系统。 |
| vfat | 支持长文件名的 DOS 文件系统。 |
| vxfs | Veritas 文件系统——一种提供访问控制列表（个人用户权限）的日志文件系统，通常由 UNIX 主要版本使用。 |

# 挂载

*挂载*（mounting）一词源于 20 世纪 60 年代，当时信息存储在磁带上，必须将其挂载到计算机上使数据可用。今天，挂载仍是指使数据可用。具体来说，它指的是通过目录树使用户可以使用设备的过程。该设备被连接到一个称为*挂载点*（mount point）的目录。用户随后可以在此挂载点创建文件和子目录，这些文件随后存储在挂载到该特定目录的文件系统中。

记住，目录仅仅是不包含数据的文件；相反，它们包含内部文件和子目录的列表。因此，Linux 系统很容易覆盖目录以防止用户访问这些数据。这本质上就是设备挂载到某个目录时发生的情况；当设备保持挂载状态时，挂载点目录会被该设备覆盖。挂载之前存在挂载点目录中的任何文件内容都不会丢失；当卸载设备时，挂载点目录会被恢复，之前的文件内容将显示。例如，假设你将包含文件系统的软磁盘设备挂载到 `/mnt` 目录。`mnt` 是包含两个子目录的目录，通常用作挂载可移动介质设备的方便挂载点。在挂载之前，目录结构类似于图 6-1 所示。软磁盘挂载到 `/mnt` 目录后，`/mnt` 目录的内容将被软磁盘文件系统覆盖，如图 6-2 所示。

**图 6-1** 挂载前的目录结构

如果用户在 `/mnt` 目录中存储文件（如图 6–2 所示），该文件将存储在软磁盘设备上。同样，如果用户在图 6-2 所示的 `/mnt` 目录下创建子目录，该子目录将在软磁盘上创建。

重要的是，任何现有目录都可以作为挂载点。如果用户将软磁盘设备挂载到 `/bin` 目录，在软磁盘挂载期间，`bin` 目录中的所有文件都将被覆盖；因此创建用于挂载设备的空目录是安全的做法，以避免影响文件。

当 Linux 系统首次启动时，硬盘上的文件系统会被挂载到 `/` 目录。这被称为**根文件系统**，包含了大多数操作系统文件。计算机硬盘上的其他文件系统也可以在启动时挂载到 `/` 目录下的各种挂载点，如后续章节讨论的 `/etc/fstab`（文件系统表）文件。

`mount` 命令用于将设备挂载到挂载点，`umount` 命令用于从挂载点卸载设备；这两个命令在本章的剩余部分中都将讨论。

# 使用软磁盘

在计算机之间传输少量信息时，通常使用可移动磁盘介质来存储文件。然而，软磁盘在 Linux 中使用之前必须经过准备。

回想每个磁盘设备在使用存储文件之前必须用文件系统进行格式化。为了实现这一点，你可以使用 `mkfs`（创建文件系统）命令并使用 `-t` 切换指定文件系统类型以及代表软磁盘设备的文件。要格式化软磁盘，使用带有 ext2 设备的软磁盘驱动器，将软磁盘放入软磁盘驱动器并输入以下命令：

```
[server@root]# mkfs -t ext2 /dev/fd0

mkfs2fs 1.35 (28-Feb-2004)

Filesystem label=
 type: Linux

Block size=1024 (log=0)

Fragment size=1024 (log=0)

184 inodes, 1440 blocks

72 blocks (5.00%) 留给超级用户

First data block=1

1 block group

8192 blocks per group, 8192 fragments per group

184 inodes per group
```

写入 inode 表：完成
写入超级块和文件系统计数：完成

该文件系统将每隔 28 次挂载或 180 天自动检查一次，以较者为准。使用 `tune2fs -c` 或 `-i` 可以覆盖。

```
[root@server1]# _
```

或者，你可以在 `-t` 选项后指定不同的文件系统，例如 DOS FAT 文件系统。这将导致 `mkfs` 命令产生不同的输出，如下例：

```
[root@server1]# mkfs -t msdos /dev/fd0

mkfs.msdos 2.8 (28 Feb 2001)

[root@server1]# _
```

如果你没有使用 `mkfs` 命令指定文件系统，则假设默认的文件系统是 ext2 文件系统，如下例所示：

```
[root@server1]# mkfs /dev/fd0

mke2fs 1.35 (28-Feb-2004)

Filesystem label=
OS type: Linux

Block size=1024 (log=0)

Fragment size=1024 (log=0)

184 inodes, 1440 blocks

72 blocks (5.00%) reserved for the super user

First data block=1

1 block group

8192 blocks per group, 8192 fragments per group

184 inodes per group
```

写入 inode 表：完成
写入超级块和文件系统计数：完成

该文件系统将每隔 26 次挂载或 180 天自动检查一次，以较者为准。使用 `tune2fs -c` 或 `-i` 可以覆盖。

```
[root@server1]# _
```

虽然创建文件系统最常用的命令是 `mkfs` 命令，但存在 `mkfs` 命令的其他变体和快捷方式。例如，要创建一个 ext2 文件系统，你可以在命令行输入 `mke2fs /dev/fd0`。`mkfs` 命令的其他替代方案列在表 6-3 中。

## 第 6 章 Linux 文件系统管理

### 表 6-3 用于创建文件系统的命令
| 命令 | 描述 |
|--- |--- |
| mkfs | 用于创建大多数类型的文件系统 |
| mkfs.msdos | 用于创建 DOS FAT 文件系统 |
| mkdosfs | | |
| mkfs.vfat | | |
| mkfs.ext2 | 用于创建 ext2 文件系统 |
| mk2fs | | |
| mkfs.ext3 | 用于创建 ext3 文件系统 (j = 日志记录) |
| mk2fs -j | | |
| mkisofs | 用于创建 CD-ROM 文件系统 |
| mkfs.reiserfs | 用于创建 REISERFS 文件系统 |
| mkreiserfs | | |

软磁盘格式化为文件系统后，必须将其挂载到目录树上才能使用。通过使用不带任何选项或参数的 `mount` 命令可以获取当前挂载的文件系统列表，它会读取 `/etc/mtab` 表中列出的信息，输出所示：

```
[root@server1 root]# mount

/dev/hda1 / ext3 (rw)

none on /proc type proc (rw)

none on /sys type sysfs (rw)

none on /dev/pts type devpts (rw,gid=5,mode=620)

usbdevfs on /proc/bus/usb usbdevfs (rw)

none on /dev/shm type tmpfs (rw)

[root@server1 root]# cat /etc/mtab

/dev/hda1 / ext3 rw 0 0

none /proc proc rw 0 0

none /sys sysfs rw 0 0

none /dev/pts devpts rw,gid=5,mode=620 0 0

usbdevfs /proc/bus/usb usbdevfs rw 0 0

none /dev/shm tmpfs rw 0 0

[root@server1 root]#
```

从上述输出中，你可以看到 `/dev/hda1` 挂载在 `/` 目录上，列出的其他文件系统是系统使用的特殊文件系统，将在本书后后部分进行讨论。

要在目录树上挂载设备，你可以使用带有选项和参数的 `mount` 命令来指定文件系统类型、要挂载的设备以及挂载该设备的目录（挂载点）。确保当前没有用户正在使用该挂载点目录非常重要；否则系统会给你错误消息且磁盘不会被挂载。你可以使用带有 `-u` 选项的 `fuser` 命令，输出所示：

```
[root@server1 root]# fuser -u /mnt/floppy

[root@server1 root]#
```

## 软磁盘操作 243

上述输出表明 `/mnt/floppy` 目录没有被任何用户进程占用。要将格式化为 ext2 文件系统的第一个软磁盘设备挂载到 `/mnt/floppy`，只需输入以下命令：

```
[root@server1 root]# mount -t ext2 /dev/fd0 /mnt/floppy

[root@server1 root]# mount

/dev/hda1 on /pts ext3 (rw)

none on /proc type proc (rw)

none on /sys type sysfs (rw)

none on /dev/pts type devpts (rw,gid=5,mode=620)

usbdevfs on /proc/bus/usb usbdevfs (rw)

none on /dev/shm type tmpfs (rw)

/dev/fd0 on /mnt/floppy type ext2 (rw)

[root@server1 root]#
```

注意，上述输出显示 `/fd0` 挂载到了 `/mnt/floppy` 目录。要访问和在软磁盘上存储文件，可以将 `/mnt/floppy` 目录视为根。当设备上创建 ext2 文件系统时，会创建一个名为 `lost+found` 的目录。该目录由 `fsck` 命令使用。要探索挂载的软磁盘文件系统，可以使用以下命令：

```
[root@server1 root]# cd /mnt/floppy

[root@server1 root]# pwd

/mnt/floppy

[root@server1 root]# ls -F

lost+found/
```

要将文件拷贝到软磁盘，只需将 `/mnt/floppy` 目录指定为 `cp` 命令的目标，如下（为了节省命令行输入时间，也可以指定一个参数并允许系统在 `/etc/fstab` 文件中查找剩余信息）：

```
[server1]# cd /etc

[server1]# cat hosts

# 不要删除以下行，否则网络功能将失效。

server1.class.com

127.0.1

[server1]# cp hosts /mnt/floppy

[server1]# ls -F

lost+found/

[server1]# cat hosts

# 不要删除以下行，否则网络功能将失效。

127.0.1

server1.class.com

[server1]#
```

同样，你可以在软磁盘下创建子目录来存储文件；子目录引用挂载点。要在示例中挂载的软磁盘上创建一个 `workfiles` 目录并将 `/etc/fstab` 文件拷贝到其中，可以使用以下命令：

```
[server1 floppy]# pwd

/mnt/floppy

[server1 floppy]# ls -F

lost-found/

[server1 floppy]# mkdir workfiles

[server1 floppy]# ls -F

lost-found/ workfiles/

[server1 floppy]# cd workfiles

[server1 floppy]# pwd

/mnt/floppy/workfiles

[server1 floppy]# cp /etc/fstab .

[server1 floppy]# ls -F

fstab

[server1 floppy]# _
```

尽管你可以从系统直接弹出软磁盘，但这样做可能会导致终端产生错误。在弹出软磁盘之前，必须使用 `umount` 命令正确卸载。`umount` 命令可以接受设备名称或挂载点目录作为参数。与挂载软磁盘类似，卸载软磁盘要求挂载点没有用户。如果在软磁盘正在使用时尝试将其挂载到 `/mnt/floppy` 目录，你会收到类似示例中的错误消息：

```
[root@server1 floppy]# pwd

/mnt/floppy
