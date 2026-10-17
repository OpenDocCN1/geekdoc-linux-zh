
您可以调整不同的 RAID 级别以使用除镜像以外的功能。其他 RAID 级别使用条带化，并且可以根据性能、数据冗余和成本进行调优。Linux 内核支持软件 RAID，并且几家硬件供应商都有适用于 SATA、IDE 和 SCSI 磁盘配置且在 Linux 中表现良好的 RAID 控制器卡。供应商包括 LSI Logic (www.lsilogic.com)、Promise (www.promise.com) 和 3ware (www.3ware.com)。关于 Linux 中 RAID 的更多信息，请参见 http://tldp.org/HOWTO/Software-RAID-HOWTO.html。

> 不要依赖 RAID 作为备份手段。RAID 仅在其中一个磁盘发生故障时帮助保护您免受数据丢失。它无法防止您意外覆盖或删除数据。

### 网络备份

前面提到的所有备份策略都可以通过网络执行。这是有利的，因为您可以让网络中的多台计算机共享单个备份设备。这与在每个系统上安装磁带机或其他备份设备相比，成本更低且更方便。然而，如果您有很多计算机，您的备份设备将需要大量容量。在这种情况下，您可能需要考虑使用机械式磁带加载器、DVD-RW 驱动器或 CD/DVD 光驱柜（能够无需操作员干预即可存放多张 CD 或 DVD 的设备）。

甚至可以通过网络执行某种形式的磁盘镜像。例如，Web 服务器可以在另一台服务器上存储其数据的副本。如果第一台服务器崩溃，简单的 TCP/IP 主机名更改即可将 Web 流量重定向到第二台服务器。当原始服务器重建完成后，它可以从备份服务器恢复所有数据并重新投入业务。

### 选择备份介质

制定了备份策略后，是时候选择备份介质了。CentOS 可使用多种类型的备份硬件和介质。每种类型都有其优缺点。

您选择的介质类型主要取决于您需要归档的数据量、您将保存备份的时间长度、您预计从备份中恢复数据的频率，以及您愿意花费多少预算。表 12-1 比较了最常见的备份介质。

以下部分描述了如何使用磁带、可写 DVD 和可写 CD 作为备份介质。使用额外的硬盘作为备份介质将在本章后面描述。

### 磁带

多年来，磁带是用于备份大量计算机数据的最常见介质。磁带提供了一种低成本、方便的方式来归档您的文件。当今高容量磁带驱动器可以在惊人小的磁带上备份数吉字节的数据，从而允许安全地存储大量信息。磁带还易于异地传输，以便在火灾、飓风或其他灾难情况下确保数据的安全。

### 常见备份介质比较

| 备份介质 | 优点 | 缺点 |
| :------------ | :--------- | :------------ |
| 磁带 | 高容量，归档大量数据的成本低 | 顺序访问介质，因此恢复单个文件可能很慢 |
| 可写 CD | 随机访问介质，因此恢复单个文件更容易。可以从任何 CD-ROM 驱动器恢复备份。 | 存储空间有限（每张 CD 最高 700 MB）。 |
| 可写 DVD | 随机访问介质（类似于 CD）。大容量（4.7 GB，虽然您实际可达到的容量可能更低）。DVD-R9 和 DVD-9 DVD 可以存储高达 8.5 GB 的数据。 | DVD-RW 驱动器和 DVD-R 光盘相对昂贵（尽管价格正在下降）。随着更多制造商在其 PC 中添加 DVD 写入器，DVD 最终将取代 CD 成为最常见的可移动介质驱动器。 |
| 额外硬盘 | 允许更快和更频繁的备份。从崩溃中快速恢复。无需加载介质。可以更快地定位和恢复数据。您可以将第二个磁盘配置为第一个磁盘的虚拟克隆，这样如果第一个磁盘崩溃，您可以从第二个磁盘启动。 | 数据不能存储在异地；因此，如果整个服务器被摧毁，就有数据丢失的风险。这种方法不适合保存文件的许多修订版本的历史归档。硬盘最终会填满。通过使用可移动硬盘，您可以在备份驱动器满时将其移除并移动到安全位置，从而克服这一限制。 |

磁带的主要缺点是它是一种`顺序访问介质`。这意味着磁带是从头到尾读取或写入的，搜索特定文件可能耗时较长。因此，磁带是备份和恢复整个文件系统的良好选择，但通常不是定期恢复单个文件的理想选择。

CentOS 可以使用各种各样的磁带驱动器。大多数 SCSI 磁带驱动器无需加载特殊模块即可工作。现在许多 IDE 磁带驱动器也可以原生支持，而无需驱动器以“SCSI 仿真”模式运行。然而，某些驱动器可能需要安装额外的软件和内核模块。

### 可写光盘驱动器

另一种逐渐流行的备份介质是可写光盘驱动器。与磁带相比，可写光盘驱动器有几个优势，最主要的是光盘属于`随机访问介质`。这意味着光盘驱动器可以迅速定位光盘上的特定文件，而无需顺序扫描整个磁盘。当您希望保留频繁更改的数据文件（如软件项目的源代码或法律文件的草稿）的修订历史时，这一点非常有用。

尽管人们过去认为光盘的寿命非常长，但这种观念最近受到了质疑。如果备份数据只需保存两年或更短时间，光盘可能仍是一个不错的选择。对于更长的时间周期，磁带备份通常比可写光盘更耐用。如果您的备份用于短期存储，您可能应该考虑使用可重写光盘或 CD-RW 光驱。可重写光盘（与普通可写光盘不同）可以重新格式化并用于存储新的备份。

最大的缺点是光盘最多只能存储约 700 MB 的数据。相比之下，DVD 可以存储 4.7 GB 的数据（双层 DVD 约为 8.5 GB），而许多磁带驱动器可以存储数 GB 的数据。例如，DAF DDS-3 磁带最多可容纳 24 GB 的压缩数据，而 8mm LTO-2 磁带最多可容纳 100 GB 的压缩数据。

### 为可写光盘获取 cdrecord

要在 CentOS 上写入光盘，可以使用默认安装的 `cdrecord`、`cdparanoia` 和 `mkisofs` 软件包。

### 写入光盘

由于写入 CD-R 或 CD-RW 盘的数据一旦写入便成为永久性数据，因此你需要在一个步骤中完成光盘的格式化和文件复制。如果先进行格式化，最终会得到一个无法再写入的 CD 上的空文件系统。

> **注意** 使用名为 `growisofs` 的`命令`（在本章后文中有详细描述），你可以以不关闭会话的方式写入光盘。稍后，你可以在最终关闭光盘之前，通过多个会话添加更多数据。`cdrecord` 命令本身现在也支持 `multi` 选项，它可以保持会话开放以供进一步写入。并非所有光盘驱动器都支持多会话写入（这需要硬件支持 CD-ROM **XA mode 2** 形式 1）。

第一步是创建一个光盘文件系统的映像文件，作为计算机上的一个文件。你使用 `mkisofs` 命令来完成这一步。第二步是使用 `cdrecord` 命令等工具将映像烧录到 CD 或 DVD 上。

例如，假设你要为用户 `connie` 备份其家目录。你需要调用 `mkisofs` 命令，并传入要创建的文件系统映像文件名，随后是基于它进行操作的目录：

```bash
$ mkisofs -R -o /var/tmp/connie.iso /home/connie
```

### 创建备份和恢复数据

![](img/2f265415ceec72538dd3c78ffca75c10_510_0.png)

这会在 `/var/tmp` 目录中创建一个名为 `connie.iso` 的 ISO9660 文件系统映像文件。`-R` 选项启用 Linux 特定的文件所有权和长文件名。如果你的 `/var` 分区没有足够的空间容纳该映像，请选择其他位置。

> **提示** 默认情况下，`mkisofs` 在创建文件系统映像时保留文件和目录的所有权和访问权限。这对于制作备份是合适的，但对于创建软件发行版 CD 则不然。在这种情况下，请将 `mkisofs` 的第一个参数 `-R` 改为 `-r`。这样所有文件将存储为公共可读，并在适当时保持可执行权限。

如果你拥有 ATAPI 光驱，你不再需要该驱动器的 SCSI ID 才能向其记录数据。你可以输入设备名称代替 SCSI ID（例如，`dev=/dev/cdrom`）。但是，如果你拥有 SCSI 光驱，在将映像文件写入光盘之前，你必须首先发现该光盘驱动器的 SCSI 总线号、设备 ID 号和逻辑单元号（LUN）。你可以找出光盘驱动器正在使用的 SCSI 设备 ID。调用带有单一参数 `-scansbus` 的 `cdrecord` 命令：

```bash
# cdrecord -scansbus
```

你应该看到类似以下的响应：

```text
scsibus:
    0,0,0     0) 'IDE-CD ' 'R/RW 4x4x24 ' '1.04' Removable CD-ROM
    0,0,1     1) *-
    0,0,2     2) *-
    0,0,3     3) *-
    0,0,4     4) *-
    0,0,5     5) *-
    0,0,6     6) *-
    0,0,7     7) *-
```

这告诉你光盘驱动器正在使用 SCSI ID 0。在这种情况下，逻辑单元号（LUN）始终应为 0，因此你现在已经拥有了这三个数字。你作为 `dev` 参数的一部分将它们提供给 `cdrecord`。

SCSI 总线号列在第一位；紧随其后的是 ID 号，然后是 LUN。整个命令应该看起来类似于这样：

```bash
# cdrecord -v speed=2 dev=0,0,0 -data /var/tmp/connie.iso
```

对于 ATAPI 光驱，如果光驱设备名为 `/dev/cdrom`，你的命令行可能如下所示：

```bash
# cdrecord -v speed=2 dev=/dev/cdrom -data /var/tmp/connie.iso
```

命令中包含几个额外的参数。`-v` 参数告诉 `cdrecord` 向屏幕提供详细输出。`speed` 参数告诉 `cdrecord` 以什么速度进行记录（在本例中为 2x）。你可以选择省略 `speed=2`，让 `cdrecord` 自动检测你的光驱的记录速度。`-data` 参数告诉 `cdrecord` 将 WAV 或 AU 文件作为数据烧录，而不是作为音轨。如果没有该选项，这些文件类型将作为音轨烧录，而其他所有文件则作为数据烧录。

![](img/2f265415ceec72538dd3c78ffca75c10_510_1.png)

在实际运行 `cdrecord` 之前，你可能考虑添加 `-dummy` 选项，该选项会模拟光盘烧录过程，而不会实际启动激光烧录。你可以在完成后添加 `-eject` 参数来弹出光盘。在工作期间，`cdrecord` 应该显示类似以下内容的状态消息：

```text
cdrecord: No write mode specified.
cdrecord: Assuming -tao mode.
cdrecord: Future versions of cdrecord may have drive dependent
defaults.
cdrecord: Continuing in 5 seconds...
Cdrecord-Clone 2.01-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2004
Jörg Schilling
TOC Type: 1 = CD-ROM
scsibdev: '/dev/cdrom'
devname: '/dev/cdrom'
scsibus: -2 target: -2 lun: -2
Warning: Open by 'devname' is unintentional and not supported.
LINUX sg driver version: 3.5.27
Using libsgio version 'schily-0.6'.
SCSI buffer size: 64512
atapi: 1

Device type    : Removable CD-ROM
Version        : 0
Response Format: 1
Vendor_info    : 'IDE-CD  '
Identification : 'R/RW 4x4x24       '
Revision       : '1.04'
Device seems to be: Generic mmc CD-RW.
Using generic SCSI-3/mmc  CD-R/CD-RW driver (mmc_cdr).
Driver flags   : MMC SWAUDIO10
Supported modes: TAO PACKET RAW/R16
Drive buf size: 1672864 = 1636 KB
FIFO size    : 4194304 = 4096 KB
Track 01: data  0 MB
Total size:  0 MB (00:04.02) = 302 sectors
Last start:  1 MB (00:06.02) = 302 sectors
Current Session: 2048
ATIP info from disk:
Indicated writing power: 5
Is not unrestricted
Is not erasable
Disk sub type: Medium Type B, low Beta category (B-) (4)
```

![](img/2f265415ceec72538dd3c78ffca75c10_512_0.png)

在 `cdrecord` 完成光盘写入且 shell 提示符返回后，删除文件系统映像文件 `/var/tmp/connie.iso`。适当地标记光盘并将其存放在安全的地方。

如果你需要 CD 中复制的任何文件，只需将 CD 放回光驱即可。如果它没有自动打开显示 CD 内容的窗口，请输入 `mount /media/cdrecord`。在文件夹窗口中打开 `/media/cdrecord` 并复制你需要的文件。

请注意，光盘驱动器的挂载点名称可能不是 `/media/cdrecord`。udev 机制的工作方式是使用通用名称，如 `cdrecord`、`disk` 或 `cdrom`，用于不包含卷 ID 的 CD 或 DVD。但是，如果在创建 CD 时卷 ID 被添加到 CD 头部，该名称将用作挂载点。例如，卷 ID 为 GAMEDISK 的游戏 CD 将挂载为 `/media/GAMEDISK`。

> 有关 `cdrecord` 的更多信息，请参阅第 7 章。你也可以从 CD-Writing-HOWTO 中了解有关安装和排查可写光盘驱动器故障的更多信息。如果你使用的是桌面版 CentOS 系统，你可能希望使用图形化 CD 刻录工具代替。第 7 章还描述了用于复制和烧录 CD 和 DVD 的图形工具 K3B。

### 可写 DVD 光驱

`cdrecord` 可用于写入 CD 和 DVD。使用可写 DVD 光驱和 `cdrecord` 命令，你可以将数据备份到 DVD-R、DVD-RW、DVD+R 和 DVD+RW 光盘中。

> **注意：** DVD-R 是一种一次写入的 DVD 格式，容量约为 4.7 GB。DVD-RW 格式的光盘可以多次写入和重写。DVD-RW 是一种读写格式，可提供更快的数据写入速度，而 DVD+R 是类似的一次写入格式。通常，DVD 刻录机支持加号（DVD+RW、DVD+R）或减号（DVD-RW、DVD-R）格式。某些驱动器支持两者。重要的是购买与你硬件兼容的光盘。

在 Linux 中向 DVD 刻录的第一个技巧是确保你拥有一台支持 DVD 写入的驱动器。你可以通过取出 CD/DVD 驱动器中的光盘并输入以下内容来检查：

```
$ cdrecord -prcap -dev=/dev/cdrom | less
Cdrecord-Clone 2.01-xvd (1686-pc-linux-gnu)
    .
    .
    .
Device type      : Removable CD-ROM
Version          : 0
Response Format: 2
Capabilities     :
Vendor_info      : 'PIONEER '
Identification   : 'DVD-RW DVR-105 '
Revision         : '1.30'
Device seems to be: Generic mmc2 DVD-R/DVD-RW.

Drive capabilities, per MMC-3 page 2A:

Does read CD-R media
Does write CD-R media
Does read CD-RW media
Does write CD-RW media
Does read DVD-ROM media
Does read DVD-R media
Does write DVD-R media
Does not read DVD-RAM media
Does not write DVD-RAM media
Does support test writing
    .
    .
    .
```

在上面的输出中，你可以看到该驱动器支持 CD 和 DVD 的读写。使用空格键翻页浏览输出（按 q 退出）。在输出的接近末尾处，你应该能看到驱动器支持的读取和写入速度。请注意，这些是最大可能速度，因此实际最大写入速度取决于你使用的 CD 或 DVD 介质。

向 DVD 写入数据的程序与将数据备份到 CD 光盘几乎相同，除了以下几点例外：

- 每个备份光盘可以容纳更多数据（单层 DVD 为 4.7 GB，双层 DVD 为 8.5 GB，而 CD 为 700 MB）。
- DVD 刻录机和介质都比相应的 CD 产品昂贵，尽管过去几年 DVD 刻录机的价格大幅下降。

> **注意：** 当制造商说 4.7 GB 时，他们指的是每 GB 1,000 MB，而不是 1,024 MB。因此，你实际上只能在 DVD 上存储大约 4.3 GB 的数据（或者更精确地说，4,294,967,296 字节）。

还有一些其他问题，在使用 DVD 介质从 Linux 记录数据时你也应该了解：

- 虽然大多数新的可写 DVD 驱动器今天都支持 DVD-R 和 DVD+R 格式，但一些旧驱动器可能不支持 DVD+R。
