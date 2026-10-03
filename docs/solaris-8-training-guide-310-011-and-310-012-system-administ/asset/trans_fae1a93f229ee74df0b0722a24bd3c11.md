
> 注意
如果未指定 fsname 和 volume，labelit 会打印这些标签的当前值。fsname 和 volume 都限制为六个字符或更少。

## 表 7.2
### labelit 命令

| 参数 | 描述 |
|---|---|
| special | 此名称应为物理磁盘分区（例如，/dev/dsk/c0t0d0s6）。 |
| fsname | 此表示文件系统的挂载点（例如，root (/)、/home 等）。 |
| volume | 可用于表示物理卷名。 |
| -F | 这指定要操作的文... |
| -v | 打印命令行但不执行操作。 |

以下是使用 labelit 命令标记磁盘分区的示例。输入以下内容：

```
labelit -F ufs /dev/rdsk/c0t0d0s6 disk1 vol1
```

系统响应如下：

```
fsname:  disk1
volume:  vol1
```

## volcopy 命令

管理员（root）可以使用 volcopy 命令复制已标记的文件系统。此命令适用于 ufs 文件系统，但必须先使用 labelit 实用程序标记文件系统，然后才能发出 volcopy 命令。要确定文件系统是否为 ufs 文件系统，请发出以下命令：

```
fstyp  /dev/rdsk/c0t0d0s6
```

系统响应如下：

```
ufs
```

volcopy 命令可用于将文件系统从一个磁盘复制到另一个磁盘。

volcopy 的语法如下：

```
volcopy [options] <fsname> <srcdevice> <volname1> <destdevice> <volname2>
```

volcopy 在表 7.3 中有描述。

## 表 7.3
### volcopy 命令

| 选项 | 描述 |
|---|---|
| -F | 这指定要操作的文... |
| -V | 打印命令行，但不执行操作。 |
| -a | 要求操作员响应“yes”或“no”。如果未指定 -a 选项，volcopy 会在复制前暂停 10 秒。 |
| -o <options> | 这是特定于文件系统类型的选项列表。列表必须具有以下格式：-o 后跟一个空格，然后是一系列以逗号分隔的 keyword [=value] 对，中间没有空格。 |
| <fsname> | 这表示被复制的文件系统的挂载点（例如，/、u1 等）。 |
| <srcdevice> / <destdevice> | 这是使用原始设备指定的磁盘分区（例如，/dev/rdsk/c0t0d0s7、/dev/rdsk/c0t0d1s7 等）。 |
| <srcdevice> / <volname1> | 这是从中提取文件系统副本的设备和物理卷。 |
| <destdevice> / <volname2> | 这是目标设备和物理卷。 |

注意 fsname 和 volname 限制为六个字符或更少，并记录在超级块中。volname 可以是连字符（—）以使用现有的卷名。

以下示例将 /home1 (/dev/rdsk/c0t0d0s6) 的内容复制到 /home2 (/dev/rdsk/c0t1d0s6)：

```
volcopy -F ufs disk1 /dev/rdsk/c0t0d0s6 vol1 /dev/rdsk/c0t1d0s6 vol2
```

其他命令也可以用于复制文件系统——ufsdump、cpio、tar 和 dd 等。这些命令在第 11 章“备份和恢复”中讨论。

## 调整文件系统

可能出现需要更改创建文件系统时设置的一些参数的情况。也许你想更改 minfree 值以在大型磁盘驱动器上释放更多磁盘空间。使用 tunefs 命令，可以修改以下文件系统参数：

- maxcontig
- rotdelay
- maxbpg
- minfree
- optimization

> 警告 tunefs 可能在几秒钟内破坏文件系统。使用 tunefs 之前请务必备份整个文件系统。

请参阅表 7.1 以了解这些选项的描述。

tunefs 的语法如下：

```
tunefs [ -a <maxcontig> ] [ -d <rotdelay> ] [ -e <maxbpg> ] [ -m <minfree> ] [ -o [ <value> ] ] \
special/filesystem
```

tunefs 命令在表 7.4 中有描述。

## 表 7.4
### tunefs 命令

| 选项 | 描述 |
|---|---|
| -a <maxcontig> | 指定在强制旋转延迟之前布局的连续块的最大数量（参见 -d 选项）。默认值是 1，因为大多数设备驱动程序每次磁盘传输都需要一次中断。对于可以将多个缓冲区链接到一次传输的设备驱动程序，将其设置为最大链长度。 |
| -d <rotdelay> | 指定为服务传输完成中断并在同一磁盘上启动新的传输而预期的时间（以毫秒为单位）。它用于决定在文件中的连续块之间放置多少旋转间距。 |
| -e <maxbpg> | 设置任何单个文件在被强制开始从另一个柱面组分配块之前可以从一个柱面组分配的最大块数。通常，此值设置为柱面组总块数的约四分之一。其目的是防止任何单个文件使用完单个柱面组中的所有块。此限制的效果是导致大文件比允许它们在寻求其他位置之前分配柱面组中的所有块时更频繁地进行长寻道。对于仅包含大文件的文件系统，应将此参数设置得更高。 |
| -m <minfree> | 指定从普通用户手中保留的空间百分比（最小空闲空间阈值）。默认值是 10%；然而，在大型文件系统上，minfree 值会自动确定。 |
| -o <value> | 更改文件系统的优化策略。值是 space 或 time。使用 space 以节省空间；使用 time 以组织文件布局并最小化访问时间。通常将文件系统优化为时间，除非其已超过 90% 满。 |
| <special>/<filesystem> | 输入特殊设备名称（如 /dev/rdsk/c0t0d0s6）或文件系统名称（如 /home）。 |

使用 tunefs 之前必须卸载文件系统。

要将文件系统的最小空闲空间（minfree）从 10% 更改为 5%，请输入以下内容：

```
tunefs -m5 /dev/rdsk/c0t0d0s6
minimum percentage of free space changes from 10% to 5%
```

tunefs 手册页建议将 minfree 设置为 10%，并且如果将值设置在该值以下，会损失性能。这意味着磁盘的 10% 无法使用。在磁盘大小只有几百兆字节的时代，这可能不是太糟糕，但对于 9GB 的磁盘，你将损失 900MB 的磁盘空间。手册中关于性能损失的提及

> 注意
在大型文件系统上，minfree 会自动确定以免浪费磁盘空间。如果要查看 newfs 使用的实际 minfree 值，请使用下面描述的 mkfs -m 命令。

页是误导性的。对于如此大的磁盘驱动器，你可以承受将 minfree 降低到 1%。这被证明是一个实用且负担得起的限制。此外，性能不会成为问题，因为即使在 90MB 区域内定位空闲块也很有效。一个经验法则是对于最大 1GB 的文件系统使用默认的 10% minfree 值，并调整 minfree 值，使你的 minfree 区域不超过 100MB。至于性能，应用程序不会抱怨较低的 minfree 值。唯一的例外是 root (/) 文件系统，在这种情况下，系统管理员可以使用他的判断来允许更多空闲空间，只是为了保守起见，以防 root (/) 达到 100% 满。

稍后，如果你想查看创建文件系统时使用的参数，请发出 mkfs 命令：

```
mkfs -m /dev/rdsk/c0t0d0s6
```

系统响应如下：

```
mkfs -F ufs -o nsect=117,ntrack=9,bsize=8192,fragsize=1024,cgsize=16,free=5,rps=90,nbpi=2062,opt=t,\
apc=0,gap=0,nrpos=8,maxcontig=15 /dev/rdsk/c0t0d0s6 205334
```

## fstyp 命令

查看文件系统参数的另一个好命令是 fstyp 命令。使用 -v 选项获取文件系统参数的完整列表：

```
fstyp -v /dev/rdsk/c0t0d0s6
```

系统响应如下：

```
ufs
  magic 11954  format dynamic      time  Sat Oct      2 10:11:06 1999
  sblkno 16    cblkno 24    iblkno 32    dblkn o 528
  sbsize 3072  cgsize 2048  cgoffset     64      cgmask 0xffffffff0
  ncg 13       size 102667 blocks 95994
  bsize 8192   shift 13     mask 0xffffe000
  fsize 1024   shift 10     mask 0xfffffc00
  frag 8       shift 3      fsbtodb      1
  minfree 5%   maxbpg 2048  optim time
  maxcontig 15 rot delay 0ms rps 90
  csaddr 528   cssize 1024  shift 9      mask 0xfffffe00
  ntrak 9      nsect 117    spc 1053     ncyl 195
  cpg 16       bpg 1053     fpg 8424      ipg 3968
  nindir 2048  inopb 64     nspf 2
  nbfree 11995 ndir 2       nifree 51577 nffree 1
  cgrotor 0    fmod 0        ronly 0
  fs_reclaim is not set
```
