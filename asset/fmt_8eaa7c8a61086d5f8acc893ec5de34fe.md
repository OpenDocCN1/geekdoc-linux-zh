
```
Command (m for help): l
 0  Empty          1b  Hidden Win95 FAT 64   Novell Netware   bb  Boot Wizard hid
 1  FAT12          1c  Hidden Win95 FAT 65   Novell Netware   c1  DRDOS/sec (FAT-
 2  XENIX root     1e  Hidden Win95 FAT 70   DiskSecure Multi  c4  DRDOS/sec (FAT-
 3  XENIX usr      24  NEC DOS            75  PC/IX            c6  DRDOS/sec (FAT-
 4  FAT16 <32M     39  Plan 9             80  Old Minix        c7  Syrinx
 5  Extended       3c  PartitionMagic     81  Minix / old Linux  da  Non-FS data
 6  FAT16          40  Venix 80286        82  Linux swap       db  CP/M / CTOS / ...
 7  HPFS/NTFS      41  PPC PReP Boot      83  Linux            de  Dell Utility
 8  AIX             42  SFS                84  OS/2 hidden C:   df  BootIt
 9  AIX bootable    4d  QNX.4.x            85  Linux extended   e1  DOS access
 a  OS/2 Boot Manager 4e  QNX.4.x 2nd part   86  NTFS volume set  e8  DOS R/O
 b  Win95 FAT32     4f  QNX.4.x 3rd part   87  NTFS volume set  e4  SpeedStor
 c  Win95 FAT32 (LBA 50) OnTrack DM   8e  Linux LVM        eb  BeOS fs
 e  Win95 FAT16 (LBA 51) OnTrack DM6 Aux 93 Amoeba          ee  EFI GPT
 f  Win95 Ext'd (LBA 52) CP/M         94  Amoeba BBT       ef  EFI (FAT-12/16/32
10  OPUS            53  OnTrack DM6 Aux 9f BSD/OS            f1  SpeedStor
11  Hidden FAT12    54  OnTrackDM6        a0  IBM Thinkpad hid  f4  SpeedStor
12  Compaq diagnostics 55  EZ-Drive          a5  BSD/386          f2  DOS secondary
14  Hidden FAT16 <32M 36 56  Golden Bow       a6  OpenBSD          fd  Linux raid auto
16  Hidden FAT16    5c  Priam Edisk       a7  NetXTSTEP        fe  LANstep
17  Hidden HPFS/NTFS 61 SpeedStor       b7  BSDI fs          ff  BBT
18  AST SmartSleep  63  GNU HURD or SysV b8 BSDI swap
```

4. 快速检查一切是否按预期指定：

```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 507 cylinders
Units = cylinders of 1008 * 512 bytes
```

| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| `/dev/hdb1` |  | 1 | 507 | 255496+ | 83 | Linux |

现在是时候使用 `w` 命令为我们的 Linux 系统写入新的分区信息了：

```
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
WARNING: If you have created or modified any DOS 6.x partitions, please see the fdisk manual page for additional information.
Syncing disks.
```

理论上，我们完成了，现在我们有一个符合适当 Linux 格式的磁盘。这意味着我们应该能够对其进行 `fsck`，对吗？

```
# fsck /dev/hdb
Parallelizing fsck version 1.23 (15-Aug-2001)
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Couldn't find ext2 superblock, trying backup blocks...
fsck.ext2: Bad magic number in super-block while trying to open /dev/hdb
The superblock could not be read or does not describe a correct ext2 filesystem. If the device is valid and it really contains an ext2 filesystem (and not swap or ufs or something else), then the superblock is corrupt, and you might try running e2fsck with an alternate superblock:
e2fsck -b 8193 <device>
```

啊啊……磁盘上还没有实际写入任何 Unix 文件系统信息。那是下一节的主题。

尽管 `fdisk` 的界面相对原始，但使用起来并不太困难，并且使将新硬盘切片成特定分区变得简单直接。这只是让第二个驱动器作为 Linux 系统的一部分出现的旅程中的第一步。

### 使用 mke2fs 添加文件系统

如果我们能把计算机磁盘当作绘画来谈论，那么运行 `fdisk` 就相当于买一块空白画布并把它放在壁橱里。除非你能把它放在画架上并取出颜料和画笔，否则你几乎无法做任何事情。

#### 任务 10.2：使用 mke2fs 创建文件系统

文件系统使用 `mkfs` 在硬盘上创建，并且由于不同文件系统在底层特性上差异很大，大多数现代 Unix 系统为每个受支持的文件系统都有特定的 `mkfs` 版本。

1. Linux 包含许多用于在磁盘上构建新文件系统的应用程序：

```
# man -k mkfs
mkdosfs [mkfs] (8) - create an MS-DOS file system under Linux
mkfs (8) - build a Linux file system
mkfs.bfs [mkfs] (8) - make an SCO bfs filesystem
mkfs.minix [mkfs] (8) - make a Linux MINIX filesystem
# man -k mke2fs
mke2fs (8) - create a Linux second extended file system
```

> 请注意，`mke2fs` 并没有匹配 `man -k mkfs`。这是一个经典例子，说明在 Unix 中搜索特定命令时你必须多挖一点。有一天这会被修复，但现在...

相比之下，Mac OS X Darwin 甚至没有匹配 `mkfs` 的东西，但如果你尝试变体 `newfs` 你会发现：

```
$ man -k newfs
newfs(8), mount_mfs(8) - construct a new file system
newfs_msdos(8) - construct a new MS-DOS (FAT) file system
```

请注意，你可以在 Macintosh 环境中，甚至在命令行中创建 Windows 格式的硬盘映像。
