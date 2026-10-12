
# 第 13 章：备份和恢复文件

第一步是创建 CD 文件系统的镜像，将其保存为计算机上的一个文件。你使用 `mkisofs` 命令来完成此操作。例如，假设你想为用户 `mary` 的 home 目录创建备份。你需要调用 `mkisofs` 命令，传入要创建的文件系统镜像文件名，随后传入要作为基准的目录：

```bash
$ mkisofs -R -o /var/tmp/mary.iso /home/mary
```

这会在 `/var/tmp` 目录下创建一个名为 `mary.iso` 的 ISO9660 文件系统镜像文件。`-R` 选项会启用 Linux 特定的文件所有权和长文件名支持。如果你的 `/var` 分区没有足够的空间来存放镜像文件，请选择其他位置。

> **提示：** 默认情况下，`mkisofs` 在创建文件系统镜像时会保留文件和目录的所有权及访问权限。这在制作备份时是合适的，但在制作软件发行版 CD 时则不然。在这种情况下，请在 `mkisofs` 的第一个参数中使用 `-r` 选项来替代 `-R`。这样所有文件都将存储为公开可读，并在适当的情况下可执行。

如果你使用的是 ATAPI CD 光驱，不再需要该光驱的 SCSI ID 即可进行刻录。你可以输入设备名称来替代 SCSI ID（例如 `dev=/dev/cdrom`）。然而，如果你使用的是 SCSI CD 光驱，在将镜像文件写入 CD 之前，你必须首先查找 CD 光驱的 SCSI 总线号、设备 ID 号和逻辑单元号（LUN）。你可以查看 CD 光驱当前使用的 SCSI 设备 ID。调用 `cdrecord` 命令并传入单个参数 `-scanbus`：

```bash
$ cdrecord -scanbus
```

你应该会看到类似以下的响应：

```text
cdrecord 2.0 (i686-pc-linux-gnu)  Copyright (C) 1995-2002 Jörg Schilling
Linux sg driver version: 3.1.25
Using libscg version 'schily-0.7'
scsibus0:
      0,0,0   0) 'IDE-CD ' 'R/W 4x4x24 ' '1.04' Removable CD-ROM
      0,0,1   1) * 
      0,0,2   2) * 
      0,0,3   3) * 
      0,0,4   4) * 
      0,0,5   5) * 
      0,0,6   6) * 
      0,0,7   7) * 
```

这表明 CD 光驱使用的是 SCSI ID 0。在这种情况下，逻辑单元号（LUN）始终应为 0，因此你现在拥有了这三个数值。你需要将它们作为 dev 参数的一部分提供给 `cdrecord`。

SCSI 总线号列在最前面；随后是 ID 号，然后是 LUN。整个命令应该类似于以下内容：

```bash
# cdrecord -v speed=2 dev=0,0,0 -data /var/tmp/mary.iso
```

对于 ATAPI CD 光驱，如果 CD 光驱为 `/dev/cdrom`，你的命令行可能如下所示：

```bash
# cdrecord -v speed=2 dev=/media/cdrecorder -data /var/tmp/mary.iso
```

该命令中包含几个额外的参数。`-v` 参数告知 `cdrecord` 向屏幕输出详细信息。`speed` 参数告知 `cdrecord` 刻录的速度（在此例中为 2 倍速）。（你可能会选择省略 `speed=2`，让 `cdrecord` 自动检测你 CD 刻录机的刻录速度。）`-data` 参数告知 `cdrecord` 下一个参数是要写入 CD 的文件系统镜像文件的名称。（你可以在完成后添加 `-eject` 参数来弹出 CD。）随着操作进行，`cdrecord` 应该会显示类似以下内容的状态消息：

```text
cdrecord: No write mode specified.
cdrecord: Assuring -tao mode.
cdrecord: Future versions of cdrecord may have drive dependent defaults.
cdrecord: Continuing in 5 seconds...
Cdrecord-Clone 2.01a27-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2004
Jörg Schilling

TOC Type: 1 = CD-ROM
scsibev: '/dev/cdrom'
devname: '/dev/cdrom'
scsib:-2 2 target: -2 lun: -2
Warning: Open by 'devname' is intentional and not supported.
Running sg driver version: 3.5.27
Using libaacs version 'achy-0.8'.
cdrecord: Warning: using unofficial libaacs transport code version
(achy - Red Hat: scsi-linux-sg.c-1.80-RH '@(#)' scsi-linux-sg.c
1.80 04/03/08 Copyright 1997 J. Schilling)'.
SCSI buffer size: 64512
atapi: 1
Device type : Removable CD-ROM
Version : 0
Response Format: 1
Vendor_info : 'IDE-CD',
Identification: 'RW 4x4x24',
Revision: '1.04'
Device seems to be: Generic mmc CD-RW.
Using generic SCSI-3/mmc CD-R/CD-RW driver (mmc_cdr).
Driver flags : MMC SWABAUDIO
Supported modes: TAO PACKET RAW R16
Drive buf size: 1572864 = 1536 KB
FIFO size: 4194304 = 4096 KB
Track 01: data 0 MB
Total size: 0 MB (00:04.02) = 302 sectors
Lout start: 1 MB (00:06/02) = 302 sectors
Current Sectors: 2048

ATIP info from disk:
Indicated writing power: 5
Is not unrestricted
Is not erasable
Disk sub type: Medium Type B, low Beta category (B-) (4)
ATIP id of lead in:  -12369 (97:17/06)
ATIP start of lead out: 359849 (79:59/74)
Disk type:  Short strategy type (Phthalocyanine or similar)
Menu. index: 69
Manufacturer: Moser Baer India Limited
Manufacturer is guessed because of the orange forum embargo.
The orange forum likes to get money for recent information.
The information for this media may not be correct.
Blocks total: 359849 Blocks current: 359849 Blocks remaining: 359547
Starting to write CD/DVD at speed 4 in real TAO mode for single session.
Last chance to quit, starting real write 0 seconds. Operation starts.
Waiting for reader process to fill input buffer ... input buffer ready.
trackno=0
Performing OPC...
Starting new track at sector: 0
Track 01: 322 of 322 MB written (fifo 100%) [buf 99%] 2.0x.
Track 01: Total bytes read/written: 338395136/338395136 (165232
sectors).
Writing time: 1110.710s
Average write speed 2.0x.
Fixing...
Fixating time: 126.108s
cdrecord: fifo had 5331 puts and 5331 gets.
cdrecord: fifo was 0 times empty and 5262 times full, min fill was 96%.
```

当 `cdrecord` 完成 CD 写入且 shell 提示符返回后，删除文件系统镜像文件 `/var/tmp/mary.iso`。给 CD 贴上适当的标签，并将其存放在安全的地方。

如果你需要 CD 上复制的任何文件，只需将 CD 插回光驱即可。如果它没有自动打开显示 CD 内容的窗口，请输入：`mount /media/cdrecorder`。在文件夹窗口中打开 `/media/cdrecorder` 并复制你想要的文件。

> **交叉引用：** 有关 `cdrecord` 的更多信息，请参阅第 8 章。你还可以从 CD-Writing-HOWTO 中了解有关安装和故障排除可写 CD 光驱的更多知识。如果你使用的是桌面版 Fedora 系统，你可能希望使用图形化 CD 刻录工具。第 8 章还介绍了用于复制和刻录 CD 和 DVD 的图形化工具 K3B。

## 可写 DVD 光驱

使用可写 DVD 光驱和 `dvdrw` 或 `growisofs` 命令，你可以将数据备份到 DVD-R 磁盘。其过程与将数据备份到 CD 磁盘几乎相同，但有以下几点不同：

- 你使用 `dvdrw` 命令替代 `cdrecord`（尽管两者的接口几乎相同）
- 每张备份盘可以容纳更多的数据（4.7GB，相比之下 CD 为 700MB）。
- 与 CD 对应的设备相比，DVD 刻录机和介质都更昂贵。

> **注意：** 当制造商提到 4.7GB 时，他们指的是每 GB 1000MB，而不是 1024MB。因此，在 DVD 上实际只能存储大约 4.4GB 的数据。

`dvdrw` 命令应允许你在任何符合多媒体命令（MMC）标准的 DVD 刻录机上刻录 DVD。`dvdrw` 命令的开发是在 Pioneer DVR-A03 DVD 刻录机上进行的。

遵循“可写 CD 光驱”章节中的步骤创建文件系统镜像文件（使用 `mkisofs`），并确定你的 DVD-R 驱动器位置。然后使用 `dvdrw` 命令实际刻录 DVD。以下是一个 `dvdrw` 命令行的示例，它刻录了一个名为 `bigimage.cd` 的文件系统镜像：

```bash
# dvdrw -v speed=2 dev=/dev/cdrom -data bigimage.cd
```

> **注意：** `growisofs` 命令是一个在母版 DVD 制作过程中可能很有用的工具。该命令结合了 `mkisofs`（用于创建文件系统镜像）和 CD 刻录软件（用于将该镜像写入 CD）的功能。

## 备份到硬盘

正如本章开头的简单备份步骤中所述，磁带、DVD 和 CD 等可移动介质并不是备份数据的唯一选择。你可能会发现安装第二块硬盘并利用它进行备份很有用。与其他备份介质相比，这有几个优点：

- 数据可以快速备份，并且可以在一天中的任何时间进行；因此，在发生崩溃时，备份的数据将更新。
- 没有介质需要加载。数据可以更快地定位和恢复。
- 你可以配置第二块磁盘成为第一块磁盘的虚拟克隆。如果第一块磁盘崩溃，你可以简单地从第二块磁盘启动，而无需安装新硬件。使用磁盘镜像软件，甚至还可以将此过程自动化。
- 借助新型、高性价比的可移动硬盘（包括通过 USB 和 FireWire 连接的硬盘），你可以享受可移动介质的便利性，同时也拥有通常被视为非可移动介质的优势。

然而，备份到硬盘也有一些缺点。例如，硬盘备份方法不适合保存文件许多个修订版本的历史存档，因为硬盘最终会填满。这个问题可以减少

