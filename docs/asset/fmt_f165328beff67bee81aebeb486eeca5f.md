
# 附录 B：磁盘驱动器

`q` 退出不保存更改
`s` 创建空的 Sun 磁盘标签
`t` 更改分区的系统 ID
`v` 更改显示/输入单位
`v` 验证分区表
`w` 将表写入磁盘并退出
`x` 额外功能（仅限专家）

Command (for help: p)

Disk/hda: 40.0 GB 40020664320 bytes
240 头部, 63 扇区, 569 磁道
Units = cylinders of 15120 = 512 = 7741440

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hd1` | | 1 | 566 | 4278982 | b | W95 FATE |
| `/dev/hd2` * | | 567 | 2694 | 1608760 | 7 | HPFS/NTFS |
| `/dev/hd3` | | 2695 | 5169 | 1871100 | 5 | Extended |
| `/dev/hd4` | | 2695 | 2700 | 45328 | 83 | Linux |
| `/dev/hd5` | | 2701 | 2706 | 45328 | 83 | Linux |
| `/dev/hd7` | | 2707 | 2712 | 45328 | 83 | Linux |
| `/dev/hd8` | | 2713 | 2778 | 498928 | 82 | Linux swap / |
| `/dev/hd9` | | 2779 | 3553 | 858968 | 83 | Linux |
| `/dev/hd10` | | 3554 | 4328 | 858968 | 83 | Linux |
| `/dev/hd11` | | 4329 | 5169 | 6357928 | 83 | Linux |

Solaris

Command (for help: q)

`m` 命令向你显示 `fdisk` 接受的所有单字母命令。你可以通过 `p` 命令查看当前分区表。此示例中的 IDE 有三个分区，均用于 Linux。

`fdisk` 分区程序表中的 `Id` 字段显示分区类型（在 `fdisk` 提示符处输入 `p`）；类型是一个十六进制数。如果你想查看所有已知的分区 ID，在 `fdisk` 提示符处输入 `i`（小写的 L），

Command (for help: i)

| Empty | | | W95 FAT1 80 | Old Minix | | Solaris boot |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 FAT12 | | NEC | 81 Minix / Old be | Solaris | | |
| 2 XENIS root | | 39 Plan | 82 Linux / Soc1 | DRDOOS/sec (FAT |
| 3 Centric| | Partition Block | Linux | | c4 | DRDOOS/sec (FAT |
| 4 FAT16<M | | Venice | 80 OS/2 Hidden: | c6 | DRDOOS/sec (FAT |
| 5 Extended | | PPP Prep Boot | 85 Extended | c7 | Syria |
| 6 FAT16 | | SFS | | 85 NTFS volume set da | Non-F da |
| 7 HPFS/NTFS | | | ONX4.x | 87 NTFS volume set db | CTOS / |
| 8 AIX | | | | Utility |
| 9 AIX bootable | | 4 | ONX4.x 3rd part be | Linux |
| a OS/2 Boot | 50 | OnTrack | 93 Amoeba | el | DOS access |
| b W95 FATE3 | | 51 | OnTrack DM 6 Aux Amoeba | e3 | DOS R/O |

# 附录 I：附录

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| c W95 FAT32 (LBA) | 52 | CP/M9f BSD/OS e4 SpeedStor |
| e W95 FAT16 (LBA) | 53 | OnTrack DM6 Aux a0 IBM Thinkhub eb Beds FS |
| f W95 Ext'd (LBA) | 54 | OnTrackDM6 a5 FreeBSD ee EFI GPT |
| 10 OPUS | 55 | EZ-Drive a6 OpenBSD ef EFI (FAT-12/ |
| 11 Hidden FAT32 | 56 | Golden a7 NextSTEP f0 Linux/PARISC |
| 12 Compaq diast 5c | 61 SpeedStor a8 Darwin f1 SpeedStor |
| 14 Hidden FAT16 K3 | 63 Novell Detroit d01 f1 Linux raid |
| 16 Hidden FAT16 K3 | 64 Novell Detroit d02 bswap fe LANet |
| 17 Hidden HPSFS/NTC | 65 Novell d08 Boot hard ff |
| 18 AST SmartLife | 70 Novell bb Boot ff |
| 19 Hidden W95 FAT30 | 70 DiskSecure Mult bb |
| c Hidden W95 FAT37 | 75 PC/IX |

# 从硬盘启动

要从硬硬盘自动启动 Linux，你需要一个引导加载程序。Fedora 使用 GNU 引导加载程序 (`GRUB`)。引导加载程序使用磁盘的主引导记录（MBR）并最先加载。随后，启动程序会提示启动操作系统（这意味着从哪个磁盘分区启动）。启动操作系统基本上涉及将操作系统的主程序加载到内存中。对于 Linux 来说，这一步涉及将 Linux 内核加载到内存并将控制权交给内核。第 2 章描述了如何配置 `GRUB` 以安装新内核。你可以咨询以了解更多关于 `grub` 的信息。在安装过程中，你忘记了（此处原文似乎有缺失，按原意翻译）。

要从硬硬盘自动启动 Linux，你需要一个引导加载程序。Fedora 使用 GNU 引导加载程序 (`GRUB`)。引导加载程序使用磁盘的主引导记录并最先加载。随后，启动程序会提示启动操作系统（这意味着从哪个磁盘分区启动）。启动操作系统基本上涉及将操作系统的主程序加载到内存中。对于 Linux 来说，这一步涉及将 Linux 内核加载到内存并将控制权交给内核。第 2 章描述了如何配置 `GRUB` 以安装新内核。你可以咨询以了解更多关于 `grub` 的信息。在安装过程中，你忘记了（此处原文此处不完整）。

*(注：原文文本中部分句子如 "During installation, you forget..." 似乎不完整，翻译已按原样保留)*

# 调整分区大小

如果你不想费力重新安装 Windows，你必须以某种方式更改现有的分区。FIPS 可以将现有的 FAT 或 FAT32 分区拆分为两个独立的分区，允许你完成此任务。顺便提一下，FAT 和 FAT32 分区用于 MS-DOS 和 Windows 95/98/Me。Windows NT、2000 和 XP 都支持 FAT 和 FAT32，但它们通常使用 NTFS 文件系统（NTFS）。第 2 章描述了如何使用 FIPS。你也可以使用以下实用工具之一对硬硬盘进行分区：

- *PowerQuest:PartitionMagic*: 这一商业工具允许你在不破坏数据的情况下调整大小、拆分、合并、删除和恢复已删除的文件。`PartitionMagic` 可以在 Windows XP 上运行，并可以调整包含 FAT、FAT32 和 Linux ext2 文件系统的分区大小。有关更多信息，请访问 www.powerquest.com。
- *Acronis Disk Suite Director*: 这一商业工具允许你在不丢失数据的情况下调整大小、复制和移动分区。它可以调整包含包含 FAT、FAT32 和 Linux ext2 等在内的分区大小。有关更多信息，请访问 www.acronis.com。
- *GNU parted*: Linux 使用 GNU `parted`，它可以操纵 FAT、FAT32 和 Linux ext2 分区。使用 `parted`，你可以调整 Linux 内部的分区大小。有关更多信息，请访问 www.gnu.org/software/parted/

# 使用 fdisk 进行分区

磁盘分区涉及在单个硬硬盘内创建较小的逻辑设备。在 Linux 中，你可以使用分区工具 `fdisk` 来查看和更改磁盘的分区表。

即使你已经对硬硬盘进行了分区，你也可以随时运行 `fdisk` 来查看硬硬盘当前的分区表。例如，如果你有一个设备名称为 `/dev/hda` 的 IDE 磁盘，你可以通过 `fdisk` 查看其分区表如下：

```
