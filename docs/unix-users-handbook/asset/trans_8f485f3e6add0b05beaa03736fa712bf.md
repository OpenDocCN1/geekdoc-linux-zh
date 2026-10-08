

## 块设备文件（UNIX 示例）

（由 **file** 命令描述为 *块特殊设备*。）

```
# ls -l /dev/dsk/c0t1d0
brw-r--r--    1 bin     sys       31 0x001000 Apr 17  1999 /dev/dsk/c0t1d0
# file /dev/dsk/c0t1d0
/dev/dsk/c0t1d0:        block special (31/4096)
#
```

![](img/75f39fc91296b889c0653851accdfd46_94_0.png)

![](img/75f39fc91296b889c0653851accdfd46_94_1.png)

## 块设备文件（Linux 示例）

（由 **file** 命令描述为 *块特殊设备*。）

```
# ls -l loop*
brw-rw----    1 root    disk      7,    0 Sep 23  1999 loop0
brw-rw----    1 root    disk      7,    1 Sep 23  1999 loop1
brw-rw----    1 root    disk      7,    2 Sep 23  1999 loop2
brw-rw----    1 root    disk      7,    3 Sep 23  1999 loop3
brw-rw----    1 root    disk      7,    4 Sep 23  1999 loop4
brw-rw----    1 root    disk      7,    5 Sep 23  1999 loop5
brw-rw----    1 root    disk      7,    6 Sep 23  1999 loop6
brw-rw----    1 root    disk      7,    7 Sep 23  1999 loop7
# file loop*
loop0: block special (7/0)
loop1: block special (7/1)
loop2: block special (7/2)
loop3: block special (7/3)
loop4: block special (7/4)
loop5: block special (7/5)
loop6: block special (7/6)
loop7: block special (7/7)
#
```

## 字符设备文件（UNIX 示例）

（由 **file** 命令描述为 *字符特殊设备*。）

```
# ls -l /dev/rdsk/c0t1d0
crw-r-----  1 root  sys  188 0x001000 Mar 23  1999 /dev/rdsk/c0t1d0
# file /dev/rdsk/c0t1d0
/dev/rdsk/c0t1d0:
character special (188/4096)
#
```

## 字符设备文件（Linux 示例）

（由 **file** 命令描述为 *字符特殊设备*。）

```
# ls -l mi*
crw-rw-rw- 1 root  sys  14,  2 Sep 23  1999 midi00
crw-rw-rw- 1 root  sys  14, 18 Sep 23  1999 midi01
crw-rw-rw- 1 root  sys  14, 34 Sep 23  1999 midi02
crw-rw-rw- 1 root  sys  14, 50 Sep 23  1999 midi03
crw-rw-rw- 1 root  sys  14,  0 Sep 23  1999 mixer
crw-rw-rw- 1 root  sys  14, 16 Sep 23  1999 mixer1
# file mi*
midi00: character special (14/2)
midi01: character special (14/18)
midi02: character special (14/34)
midi03: character special (14/50)
mixer: character special (14/0)
mixer1: character special (14/16)
#
```

## 文件系统布局

在开始讨论文件系统布局之前，你需要知道你并不一定只有一个文件系统。你的系统管理员可能已经在你的系统上设置了多种文件系统类型。作为一个初学者，你不需要过多关心不同的文件系统类型；然而，在继续深入文件系统布局之前，让我简要介绍一些不同的文件系统类型。系统管理员非常关心不同的文件系统类型，因为他们或她发布的命令允许指定诸如 "-F" 后跟文件系统类型的选项。寻找你的 UNIX 变体支持的不同文件系统类型的一个良好起点是 **mount** 命令的手册页。"-F" 选项，或者在 Linux 中用于类型的 "-t" 等其它选项，通常后面跟着一系列受支持的文件系统类型列表。不同的文件系统类型和针对文件系统类型的命令选项取决于你正在使用的 UNIX 变体。一些通常支持文件系统类型选项的命令包括 **dcopy**、**fsck**、**mksf**、**mount**、**newfs** 以及其他一些，如果你将来要执行系统管理任务，作为高级用户你可能需要了解其中的一些。以下是 UNIX 变体上一些常见受支持的文件系统的说明。

![](img/75f39fc91296b889c0653851accdfd46_96_0.png)

- 个人电脑文件系统 (PCFS) 是一种允许直接访问 PC 格式磁盘的文件系统类型。
- UNIX 文件系统 (UFS) 是某些 UNIX 变体上的标准或基本默认 UNIX 文件系统。
- CD-ROM 文件系统 (CDFS) 在你挂载 CD-ROM 时使用。CD-ROM 是只读的，因此你无法向其写入。在某些 UNIX 变体上，这被称为 High Sierra 文件系统 (HSFS)。
- 网络文件系统 (NFS) 是一种从本地系统访问网络中其他系统上文件的方法。挂载的 NFS 文件系统看起来像是本地系统的一部分，尽管它实际上位于另一个系统上。
- 回环文件系统 (LOFS) 允许你使用不同的路径名称在同一文件系统上拥有多个挂载点。
- VxFS 是一种基于扩展的日志文件系统，支持 HP-UX 上的快速文件系统恢复和在线功能，如备份。
- 高性能文件系统 (HPSF) 是 HP 版本的 UNIX 文件系统。这用于大多数示例中。
- TMPFS 是一种基于内存的文件系统。
- CacheFS 是存在于缓存中的文件系统。

文件系统类型是 UNIX 变体高度自定义的领域。你会发现某些文件系统列在一些 UNIX 变体中，而其他列在其它 UNIX 变体中。尽管 UNIX 及其相关命令在从一个 UNIX 变体过渡到另一个时非常相似，但文件系统类型通常特定于某个特定的 UNIX 变体。确定你的 UNIX 变体包含哪些文件系统类型的一个良好起点是查看 mount 手册页中列出的文件系统类型。

![](img/75f39fc91296b889c0653851accdfd46_97_0.png)

我们在使用的 Caldera Linux 系统上 mount 的手册页列出了许多文件系统类型。在使用 Linux mount 命令时，你会使用 -t vfstype 选项来指定要挂载的文件系统类型之一：

- minix
- ext
- ext2
- xiafs
- hpfs
- fat
- msdos
- umsdos
- vfat
- proc
- nfs
- iso9660
- smb
- ncp
- affs
- ufs
- sysv
- xenix
- coherent

我经常在 Linux 系统上挂载的一种常见文件系统是 DOS 软盘。例如，我们会通过以下一系列事件来挂载 DOS 软盘、将文件复制到它并卸载它：

```
# mount -t msdos /dev/fd0 /mnt/floppy
# cp * /mnt/floppy
# ls /mnt/floppy
file1     file2     file3     file4
# umount /dev/fd0
```

![](img/75f39fc91296b889c0653851accdfd46_98_0.png)

![](img/75f39fc91296b889c0653851accdfd46_99_0.png)

这一系列命令首先将 **/dev/fd0**（它是软盘设备文件）挂载到挂载点 **/mnt/floppy** 下。**/dev/fd0** 被挂载为 *msdos* 类型，如 **-t msdos** 所指定。接下来，我将当前目录中的所有文件复制到软盘。然后使用 *ls* 列出软盘上的所有文件，生成了图中所示的四个文件列表。接着，我使用 **umount** 命令卸载软盘，以便我可以使用软盘到 DOS 系统并读取文件。由于软盘被挂载为 *msdos* 类型，文件是以 DOS 格式写入软盘的。

类似地，要在 Linux 系统上挂载 CD-ROM，你会发出以下挂载命令：

```
# mount /dev/hdd /cdrom
mount: block device /dev/hdd is write-protected, mounting read-only
#
```

![](img/75f39fc91296b889c0653851accdfd46_99_1.png)

你会用你的 CD-ROM 设备文件替换 **/dev/hdd**。CD-ROM 当然是只读设备，如 **mount** 的消息所示。

大多数 UNIX 变体的文件系统布局基于 AT&T SVR4 布局。这意味着从一个 UNIX 变体到下一个，你会看到在文件系统布局中使用的大致相同的名称。

图 2-1 是文件系统的高级描述。

![](img/75f39fc91296b889c0653851accdfd46_100_0.png)

**图 2-1** 通用 UNIX 文件系统布局（在 UNIX 变体间略有不同）

以下是 UNIX 文件系统布局中一些更重要的特征：

- 文件和目录按类别组织。图 2-1 中最明显的两个类别是静态与动态文件。此外，还有其他类别，如可执行文件、配置文件、数据文件等。静态文件也被标记为“共享”，因为网络上的其他主机可能会共享这些。目录 `/usr`、`/sbin` 和 `/opt` 是共享目录。
- 操作系统和应用程序相互独立。应用程序供应商不在乎他们的应用程序加载到哪里；那取决于你。但对一个系统

