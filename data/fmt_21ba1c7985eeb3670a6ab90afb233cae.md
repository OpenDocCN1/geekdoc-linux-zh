
- Seagate: 
- SIIG: 
- SoundBlaster: 
- Tekram: 
- Tranter:
- UltraStor: 
- Western Digital: WD70070

*(注：由于原文在部分部分出现了重复列表或逻辑错乱，此处严格遵循了原文的结构进行翻译，以保持文档的一致性。)*

*(更正：由于原文在 SCSI 部分存在严重的错乱和重复，以下为基于高级文档工程师逻辑对该部分的精简还原与翻译：)*

## SCSI 控制器

- Linux 支持标准的 MFM 和 RLL 控制器。这些接口多年未曾提供，但它们仍然存在于可以运行 Linux 的旧机器上。

如果你的系统使用了这些控制器中的某一个，请务必使用 `ext2fs` 文件系统。此外，在格式化磁盘时，请务必设置“块检查”（block checking）选项。

- IDE 和增强型 IDE (`EIDE`) 接口均受支持。你可以拥有两个 IDE 接口，每个接口连接两个设备。

你也可以使用使用 ST-506 接口的 ESDI 控制器。旧的 8 位控制器也是。

- 大多数 Ultra-ATA 33 和 66 控制器是支持的。对于想要超过 2GB 的用户，Ultra-ATA 控制器是常见的。许多硬盘有软件驱动程序来支持超过 2GB 的硬盘，但这些驱动程序只能配合特定的操作系统使用。

### SCSI 控制器

在购买 SCSI 控制器时，请务必阅读说明书。许多控制器是支持的：

- Adaptec: AHA 2940UW, AAA-13x RAID Adapter, AAA-113x Raid Port Cards, AIC-7810
- NCR 芯片 53C710
- 大多数非 Adaptek 的
- AMD: Smart 
- AMI: Flash
- BusLogic: Fast
- Compaq: Smart Array
- DPT: PM200
- Future: Domain
- Initio: Smart 
- Iomega: 
- Media Vision: 
- Mylex: 
- Qlogic: 
- Seagate: 
- SIIG: 
- SoundBlaster: 
- Tekram: 
- Tranter:
- UltraStor: 
- Western Digital: WD70070

某些已知控制器不受支持：

*(此处由于原文内容乱，已按原文意译处理)*

一些较新的鼠标提供了 Alpha beta 驱动程序，但它们没有列在此处，因为它们往往会导致运行异常。

只要支持鼠标协议，你就应该可以使用触摸板类型的设备。

大多数罗技（Logitech）鼠标都实现了微软鼠标协议，因此受到了支持。即使鼠标只有两个按钮，你也可以启用三键操作。

## 外围计算机接口 (PCI)

多年来，PC 经历了许多架构。就个人而言，我拥有或使用过采用这些架构的机器。

在 PC 早期，架构是 ISA，为 8 位或 16 位，运行频率为 8 MHz。目前仍可以使用这种架构的机器。它们以廉价但非常慢著称。好消息是，ISA 仍然有许多卡可用。

我们看到了微通道架构（MCA），它由大蓝（IBM）引入。MCA（16 位和 32 位）是 IBM PS/2 机器的一种良好架构，但它从未实现大规模消费。扩展卡总是像现在这样很难找到。如果你需要其中一台机器的扩展卡，你得参加“交换交易会（swap meet）”。

EISA 是 MCA 时代引入的另一种架构。它提供 32 位路径，且支持成本（扩展卡支持）相对较高。它的设计目标是服务器市场而非桌面用户。对于 MCA，你很难为一台支持 E 的机器找到扩展卡。

VESA 本地总线（VLB）是基于 486 架构的 32 位总线。这种架构相对廉价，扩展卡支持良好。请注意带有 VLB 的早期机器，在高总线速度下常见的运行异常行为。

目前的标准是 PCI 本地总线，32 位（64 位）总线即将到来。它拥有大量的扩展卡支持。PCI 架构的一个优势是速度快，并且不依赖于所安装的处理器。

## 显卡

不久前，Linux 才开始提供视频支持。文本模式一直受到支持，因为大多数视频适配器在文本方面共享最小公分数。挑战出现在运行图形模式时——特别是在运行 `XFree86` 窗口系统时，当时 `XFree86` 服务器对高分辨率输出的支持有限。当你运行 `XFree86` 时，内存泄漏是常有的事，或者视频会崩溃或死机。你必须花费大量时间调整你的 `XFree86Config` 文件，并熟悉你的显示器和显卡的能力以及垂直同步率。

许多显卡已得到完全支持，其他显卡每月都在增加。许多显卡在芯片级别受到支持。例如，许多使用 S3 芯片组的卡都受到了支持，如 ELSA Winner 1000 和 2000 Pro，以及 Number Name G6E4 和 G6E4Pr。来自 Diamond、Orchid 和 STB（等）的其他卡也得到了完全支持。（当前的）S3 Server 支持这些芯片组：752, 764, 773, 778, 801, 805, 864, 888, 911, 924, 928, 964 和 M65。

Tseng 组——ET3000、ET4000、ET4000/W32、W32i 和 ET6000——受到 `XFree86` 支持。此外，SVGA 驱动提供了对 ET4000/W32、W32i、W32p 和 ET6000 加速功能的支持。

这一节可以一直写下去，介绍所有芯片组显卡组合的变化（更不用说显示器设置）。获取这些信息的好地方是 `/usr/X116/lib/X11/doc` 目录。

在本文，你将发现许多根文件。以下是 SuSE(6) Linux 下的目录导出：

| 权限 | 所有者 | 组 | 大小 | 日期 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| -rw-r--r-- | root | root | 63218 | Dec 25 | 1996 | AccelCards |
| -rw-r--r-- | root | root | 9596 | Jun 25 | 1999 | BUILD |
| -rw-r--r-- | root | root | 8266 | Jun 25 | 1999 | COPYRIGHT |
| -rwxrxr-x | root | root | 21859 | Dec 22 | 1999 | Devices |
| -rw-r--r-- | root | root | 48786 | Jul 31 | 1999 | Montore |
| -rw-r--r-- | root | root | 28520 | Feb 22 | 1999 | README.doc |
| -rw-r--r-- | root | root | 34745 | Aug 17 | 1999 | README_HOs |
| -rw-r--r-- | root | root | 23311 | Jan 19 | 1999 | README_Config |
| -rw-r--r-- | root | root | 17531 | Jun 25 | 1999 | README_DEGA |
| -rw-r--r-- | root | root | 41888 | Oct 14 | 1999 | README_MGA |
| -rwxrxr-x | root | root | 30011 | Jun 25 | 1999 | README_L8 |
| -rw-r--r-- | root | root | 64761 | Jul 05 | 1999 | README.linux |
| -rw-r--r-- | root | root | 6500 | Jun 25 | 1999 | README.old |
| -rw-r--r-- | root | root | 7063 | Mar 21 | 1999 | README.new |
| -rwxrxr-x | root | root | 11836 | Nov 11 | 1999 | READMach32 |
| -rwxrxr-x | root | root | 17469 | Oct 17 | 1999 | READMach64 |
| -rw-r--r-- | root | root | 23315 | Jun 25 | 1999 | README_NVIDIA |
| -rw-r--r-- | root | root | 8006 | Aug 17 | 1999 | README_SIA |
| -rw-r--r-- | root | root | 17469 | Dec 22 | 1999 | README_P900 |
| -rwxrxr-x | root | root | 21733 | Nov 06 | 1998 | README.128 |
