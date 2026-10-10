

![](img/c27875544958897d817484d558c208c8_223_0.png)

# **图 5-1** 挂载前的目录结构

![](img/c27875544958897d817484d558c208c8_223_1.png)

# **图 5-2** 挂载软盘设备后的目录结构

![](img/c27875544958897d817484d558c208c8_223_2.png)

如今大多数系统都配有多种可移动媒体设备——例如光盘、DVD、USB 闪存盘和 USB 硬盘——这些设备可能会长时间连接在您的 PC 上。因此，在 Linux 系统的 `/media` 目录下创建子目录来挂载这些可移动媒体设备，而仅在 `/mnt` 目录中临时挂载设备，被视为一种良好的惯例。例如，您可以将软盘挂载到 `/media/floppy` 目录，将 DVD 挂载到 `/media/DVD` 目录。然后，您可以通过导航到 `/media/floppy` 目录来访问软盘上的文件，也可以通过导航到 `/media/DVD` 目录来访问 DVD 上的文件。

当 Linux 系统首次启动时，硬盘上存在的文件系统会被挂载到 `/` 目录。这被称为**根文件系统**，包含大多数操作系统文件和目录。

系统文件。计算机内部硬盘上存在的其他文件系统也可以在启动时挂载到 `/` 目录下的各个挂载点目录，以及通过以下章节中讨论的文件系统表（`/etc/fstab`）中的条目进行挂载。

`mount` 命令用于将设备挂载到挂载点目录，`umount` 命令用于将设备从挂载点目录卸载；本章剩余部分将讨论这两个命令。

## 处理软盘

传统上，使用软盘可移动媒体来存储小文件（例如需要在计算机之间传输的电子表格）是非常普遍的。如今，并非所有系统都配备软盘，但我们将在此考察软盘，因为它们是练习和学习常用于处理文件系统的命令的一种简便方式，并且可以在虚拟化软件中模拟。

请记住，每个磁盘设备在用于存储文件之前，都必须先格式化一个文件系统。为此，您可以使用 `mkfs`（make filesystem）命令，并使用 -t 开关指定文件系统类型，以及代表软盘设备的设备文件。要在计算机的第一个软盘驱动器中用 ext2 文件系统格式化软盘，请将软盘放入软盘驱动器，并输入以下命令：

```
[root@server1 ~]# mkfs -t ext2 /dev/fd0
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=0 blocks, Stripe width=0 blocks
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=1572864
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group
Allocating group tables: done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
[root@server1 ~]#
```

或者，您可以在 -t 选项后指定不同的文件系统，例如 DOS FAT 文件系统。这会导致 `mkfs` 命令产生不同的输出，如下例所示：

```
[root@server1 ~]# mkfs -t msdos /dev/fd0
mkfs.msdos 3.0.23 (2013-10-15)
[root@server1 ~]#
```

如果您未使用 `mkfs` 命令指定文件系统，默认假设的文件系统是 ext2 文件系统，如下例所示：

```
[root@server1 ~]# mkfs /dev/fd0
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=0 blocks, Stripe width=0 blocks
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=1572864
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group

Allocating group tables: done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done

[root@server1 ~]#
```

虽然创建文件系统最常用的命令是 `mkfs`，但也存在 `mkfs` 命令的其他变体和快捷方式。例如，要创建 ext2 文件系统，您可以在命令行输入 `mke2fs /dev/fd0`。表 5-3 列出了 `mkfs` 命令的其他替代方案。

软盘格式化为文件系统后，在可以使用它之前，必须将其挂载到目录树上。可以使用不带选项或参数的 `mount` 命令来获取当前挂载的文件系统列表，该命令会读取 `/etc/mtab`（mount table）文件中列出的信息，如下面的示例输出所示：

```
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)

[root@server1 ~]# cat /etc/mtab
/dev/sda1 / ext4 rw 0 0
proc /proc proc rw 0 0
sysfs /sys sysfs rw 0 0
devpts /dev/pts devpts rw,gid=5,mode=620 0 0
tmpfs /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
sunrpc /var/lib/nfs/rpc_pipefs rpc_pipefs rw 0 0

[root@server1 ~]#
```

| 命令 | 创建的文件系统 |
| :--- | :--- |
| `mkfs` | 大多数类型的文件系统 |
| `mkdosfs` | FAT |
| `mkfs.msdos` |  |
| `mkfs.vfat` |  |
| `mkfs.ext2` | ext2 |
| `mke2fs` |  |
| `mke2fs -t ext2` |  |
| `mkfs.ext3` | ext3 |
| `mke2fs -t ext3` |  |
| `mkfs.ext4` | ext4 |
| `mke2fs -t ext4` |  |
| `mkisofs` | ISO |
| `mkreiserfs` | REISERFS |
| `mkfs.reiserfs` |  |
| `mkfs.xfs` | XFS |
| `mkntfs` | NTFS |
| `mkfs.ntfs` |  |

**表 5-3** 用于创建文件系统的命令

从上面的示例输出中可以看出，设备 /dev/sda1 已挂载到 / 目录，并包含一个 ext4 文件系统。列出的其他文件系统是系统使用的特殊文件系统，将在本书稍后部分进行讨论。

要将设备挂载到目录树上，您可以使用带有选项和参数的 `mount` 命令，以指定文件系统类型、要挂载的设备以及挂载该设备的目录（挂载点）。确保当前没有用户正在使用该挂载点目录非常重要；否则，系统会给出错误消息，并且磁盘不会被挂载。要检查 /media/floppy 目录是否被任何用户使用，您可以使用带有 -u 选项的 `fuser` 命令，如下面的输出所示：

```
[root@server1 ~]# fuser -u /media/floppy
[root@server1 ~]#
```

上述输出表明 /media/floppy 目录未被任何用户进程使用。要将格式化为 ext2 文件系统的第一个软盘设备挂载到 /media/floppy 目录，只需输入以下命令：

```
[root@server1 ~]# mount -t ext2 /dev/fd0 /media/floppy
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/fd0 on /media/floppy type ext2 (rw)
[root@server1 ~]#
```

![](img/c27875544958897d817484d558c208c8_226_0.png)

![](img/c27875544958897d817484d558c208c8_227_0.png)

如果省略 `mount` 命令的 -t 选项，它将尝试自动检测设备上的文件系统。因此，命令 `mount /dev/fd0 /media/floppy` 将执行与上述输出中所示的 mount 命令相同的操作。

请注意，在 `mount` 命令的上述输出中，/dev/fd0 显示已挂载到 /media/floppy 目录。要访问和存储软盘设备上的文件，现在可以将 /media/floppy 目录视为软盘的根目录。当在磁盘设备上创建 ext2 文件系统时，默认会创建一个名为 `lost+found` 的目录，该目录由本章稍后讨论的 `fsck` 命令使用。要探索最近挂载的软盘文件系统，您可以使用以下命令：

```bash
[root@server1 ~]# cd /media/floppy
[root@server1 floppy]# pwd
/media/floppy
[root@server1 floppy]# ls -F
lost+found/
[root@server1 floppy]#
```

要将文件复制到软盘设备，只需将 /media/floppy 目录指定为 `cp` 命令的目标，如下所示：

```bash
[root@server1 floppy]# cd /etc
[root@server1 etc]# cat issue
Fedora release 20 (Heisenbug)
Kernel 3.11.10-301.fc20.x86_64 on an x86_64 (tty1)
[root@server1 etc]# cp issue /media/floppy
[root@server1 etc]# cd /media/floppy
[root@server1 floppy]# ls -F
issue lost+found/
[root@server1 floppy]# cat issue
Fedora release 20 (Heisenbug)
Kernel 3.11.10-301.fc20.x86_64 on an x86_64 (tty1)
[root@server1 floppy]#
```

同样，您也可以在软盘设备下创建子目录来存储文件；这些子目录在挂载点目录下方被引用。要在上一个示例中挂载的软盘上创建一个名为 `workfiles` 的目录，并将 `/etc/inittab` 文件复制到其中，您可以使用以下命令：

```bash
[root@server1 floppy]# pwd
/media/floppy
[root@server1 floppy]# ls -F
issue lost+found/
```

