
Command (m for help): n

Partition type

p primary partition (0 primary, 0 extended, 4 free)

e extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1): 1

First sector (2048-2097151, default 2048):

Using default value 2048

Last sector, +sectors +size(K,M,G) (2048-2097151, default 2097151):500M

Created new partition 1 of type 'Linux' and of size 500 MiB.

```
```

Command (m for help): a

Selected partition 1

```
```

Command (m for help): w

Disk `/dev/sdb`: 1 GiB, 107371824 bytes, 2097152 sectors

```
| Device Boot Start End Sectors Size Id Type |
| `/dev/sdb` * 2048 102607 1024000 500M 83 Linux |
```

Command (m for help): w

```

注意扇区数量如何与 500MiB 的二进制表示相匹配。这是创建你可能需要的任何其他分区的命令。
当添加或更改分区时，通常不需要重启 Linux 即可读取新的分区表，除非另一个分区已经被驱动并挂载。如果是这样，使用 `w` 命令写入分区表的尝试将临时失败并显示以下消息：

> WARNING: Re-reading the partition table failed with error 16:
Device or resource busy.
内核 仍在使用旧表。新表将在下次重启或在你运行 `partition(8)` 或 `kpart(8)` 后使用。

如果你运行 `partprobe /dev/sdb`，内核将读取新的分区表，你就可以使用新创建的分区了。

## 使用 fdisk：多种分区类型

一个特别感兴趣的功能是基于 `t` 命令更改分区系统标识。如果你为逻辑卷或交换空间（swap space）提供空间，`t` 命令是非常重要的。按下 `t` 后，系统会提示编辑分区编号（如果配置了多个）。然后你可以使用 `L` 命令列出分区类型，如下所示。（如果设备上只有一个分区，则会自动检测。）

```
Command (m for help): t

Selected partition 1

Hex code or alias (type L to list all): L
```

可用分区标识符列表（如图 7-4 所示）令人印象深刻。请注意，它不仅限于 Linux 分区。然而，由于本书涵盖了 Linux，表 7-1 列出了相关的分区类型。

除非你要进行更改，否则输入 83。你将返回到 `fdisk` 命令提示符。

## 使用 fdisk：删除分区

该示例删除了唯一配置的分区。屏幕输出示例首先从 `fdisk` 开始。然后你可以打印 (p) 当前分区表，按编号删除 (d) 分区（在本例中为 1），将更改写入 (w) 设备，并从提示符中退出 (q)。无需多说，不要在任何你需要保留数据的分区上执行任何操作。

图 7-4 Linux 分区类型：

| 00 Empty | 24 NEQ DOS | 81 Minix / Old lin | bf Solaris |
| 01 FAT12 | 27 HIDDEN MTFS Win | 82 Linux / swap / So | c1 D0/sec (FAT- |
| 02 XENIS root | 30 Plan 9 | c4 D0/sec (FAT- |
| 03 XENIS user | 33 Partition Magic | 84 05/2 hidden or | c6 D0/sec (FAT- |
| 04 FAT16 <32M | 40 QNX 80286 | 85 Linux extended | c7 Linux |
| 05 Extended | 41 PPC Prep Boot | 86 NTFS volume | de Na-FS Data |
| 06 W95 FAT32 | CP/M | | 87 NTFS volume | db CPY / CTOS / |
| 06 FAT16 | 56 Golden Edim | 88 Linux deinst | df BootIT |
| 07 HPFS/XFS/ext4 | 42 4QNX.4 2rd part | 89 Linux LW | fd BootIT |
| 08 AIX | 44 QNX.4 3rd part | 93 Amoeba | e1 door access |
| 09 AIX boot | 50 05/2 Boot Main | 94 FreeBSD BBA | e3 dos R/O |
| 09 W95 FAT32 (lba) | 51 Ontrack DMG Aux | 95 BSD/OS | e4 Speedor |
| 09 W5 Ext (LBA) | 53 Ontrack DMG Aux | a5 FreeBSD | ea Linux extended |
| 10 OPUS | 55 EZ-Drive | a6 BSB0 | eb Beb FS |
| 11 Hidden Fat12 | 56 Hidden | a7 NEXTSTEP | ee GPT |
| 12 Compaq dialog | 55 Sciam Prim Ed | a8 Darwin UFS | ef EFA (FAT-12) |
| 13 FAT16 <3 | 63 GU HURD of Sys | a9 NeB50 | f1 Speed FS |
| 14 Hidden Master | 64 Novell West | b0 HFS / hfs- | f4 Speed FS |
| 15 Bootsector | 65 Novell West | b7 BSI fs | fb VMware WFS |
| 16 Hidden16 | 71 JAP | b8 BSI swap | fc Linux raid aut |
| 17 Hidden HPFS/XFS/ext4 | 72 Blue | b9 Linux | fe |
| 18 Hidden W95 FAT32 | 73 W95 FAT32 | ac | fe |
| 19 Hidden W95 FAT32 (lba) | 74 FAT16 <32M | ff | | |
| 20 Hidden W5 Ext (LBA) | 75 FAT16 | | |

# 264 第 7 章 存储与文件系统管理

在运行写入 (`w`) 命令之前，`fdisk` 实用程序不会真正将更改写入磁盘。或者，你可以使用退出 (`q`) 命令取消这些更改。如果没有看到任何错误信息，则更改已写入磁盘。正如本章所述，需要额外工作来配置 RHEL 使用该新创建的交换分区。

# gdisk 工具

如上一节所示，MBR 分区方案最多支持 15 个分区（3 个主分区和 12 个逻辑分区），外加一个扩展分区，扩展分区仅仅是逻辑分区的“容器”。相比之下，GPT 分区方案可以容纳达 128 个分区。

MBR 的另一个局限性是磁盘大小。MBR 方案使用 32 位地址，支持高达 2TB 的磁盘驱动器。另一方面，GPT 格式依赖于 64 位地址，支持高达 800 万 TB 的驱动器！

尽管你可以使用 `fdisk` 和 `g` 命令切换到 GPT 分区表，但 `gdisk` 工具是专门为 GPT 分区设计的。如果你熟悉 `fdisk`，那么 `gdisk` 看起来也会熟悉。当你在带有 MBR 分区表的磁盘上启动 `gdisk` 时，你会看到以下内容：

```
[root@server1 ~] gdisk /dev/sdb

****************************************************

找到有效的 GPT 和有效的 MBR；正在内存中将 MBR 转换为 GPT 格式。此操作具有潜在破坏性！如果不想将 MBR 分区转换为 GPT 格式，请输入 'q' 退出！

****************************************************
```

如消息所示，输入 `q` 退出；否则，你可能会丢失驱动器上的任何数据。在这种情况下，`gdisk` 警告我们磁盘正在使用 MBR 分区表，我们应该使用 `fdisk` 修改分区布局。

一旦启动，`gdisk` 的工作方式与 `fdisk` 。输入问号 (?) 获取命令列表：

```
Command (? for help): ?

将 GPT 数据备份到文件

更改分区名称

删除分区

显示分区的详细信息
```
