

## 表 A–5 以太网驱动程序模块

| 硬件 | 模块 | 参数 |
| --- | --- | --- |
| AMD PCnet32 和 AMD PCnetPCI | pcnet32.o |  |
| RedCreek Communications PCI | rpcpi.o |  |
| 使用 RTL8129 或 RTL8139 快速以太网芯片组的 RealTek 网卡 | rtl8139.o |  |
| Sangoma S502/S508 多协议 FR | sdla.o |  |
| Sangoma S502A, ES502A, S502E, S503, S507, S508, S509 | sldadrv.o |  |
| SysKonnect 令牌环 ISA/PCI 适配器，TR4/16(+) ISA 或 PCI，TR4/16 PCI，以及旧款 SK NET TR4/16 ISA 卡 | sktr.o | sktr=io_port,IRQ,mem sktr io=io_port irq=IRQ mem=mem |
| SMC Ultra 和 SMC EtherEZ ISA 以太网卡 (8K, 83c790) | smc-ultra.o | smc-ultra=io_port,IRQ smc-ultra io=io_port irq=IRQ |
| SMC Ultra32 EISA 以太网卡 (32K) | smc-ultra32.o |  |
| SMC 9000 系列以太网卡 | smc9194.o | smc9194=io_port,IRQ smc9194 io=io_port irq=IRQ ifport=[0,1,2] |
| Compaq Netelligent 10/100 TX PCI UTP <br> Compaq Netelligent 10 T PCI UTP <br> Compaq 集成 NetFlex 3/P <br> Compaq Netelligent 双 10/100 TX PCI UTP <br> Compaq Netelligent 集成 10/100 TX UTP <br> Compaq Netelligent 10/100 TX 嵌入式 UTP <br> Compaq Netelligent 10 T/2 PCI UTP/同轴 <br> Compaq Netelligent 10/100 TX UTP <br> Compaq NetFlex 3/P <br> Olicom OC-2325, OC-2183, OC-2326 | tlan.o | tlan=io_port,IRQ,aui,debug <br> tlan io=io_port irq=IRQ <br> 其他模块选项： <br> speed=10Mbs,100Mbs <br> debug=0x[0,1,2,4,8] <br> aui=1 <br> duplex=[1,2] |
| Digital 21x4x Tulip PCI 以太网卡 <br> SMC EtherPower 10 PCI(8432T/8432BT) <br> SMC EtherPower 10/100 PCI(9332DST) <br> DEC EtherWorks 100/10 PCI(DE500-XA) <br> DEC EtherWorks 10 PCI(DE450) <br> DEC QSILVERs, Znyx 312 etherarray <br> Allied Telesis LA100PCI-T <br> Danpex EN-9400, Cogent EM110 | tulip.o |  |
| 配备 VIA VT86c100A Rhine-II PCI 或 3043 Rhine-I 的 VIA Rhine PCI 快速以太网卡 <br> D-Link DFE-930-TX PCI 10/100 | via-rhine.o |  |
| AT&T GIS (前身为 NCR) WaveLAN ISA 卡 | wavelan.o | wavelan=[IRQ,0],io_port,NWID |
| WD8003 和 WD8013 “兼容”以太网卡 | wd.o | wd=io_port, IRQ, mem,mem_end <br> wd io=io_port irq=IRQ mem=mem mem_end=end |
| Packet Engines Yellowfin | yellowfin.o |  |
| G-NIC PCI 千兆以太网适配器 |  |  |
| 基于 Z8530 的 AX.25 HDLC 卡 | z85230.o |  |

以下是这些模块使用的一些示例：

### 表 A–6 以太网参数配置示例

| 配置 | 示例 |
| :--- | :--- |
| IO 地址为 300 且 IRQ 为 11 的 NE2000 ISA 卡 | `ne=0x300,11` <br> `ether=0x300,11,eth0` |
| IO 为 390，IRQ 自动探测，并使用 NWID 为 0x4321 的 Wavelan 卡 | `wavelan=0,0x390,0x4321` <br> `ether=0,0x390,0x4321,eth0` |

## A.4.1 使用多个以太网卡

你可以在一台计算机中使用多张以太网卡。如果每张卡使用不同的驱动程序（例如，一张 3c509 和一张 DE425），你只需要在 `/etc/conf.modules` 中为每张卡添加 `alias`（以及可能的 `options`）行。更多信息请参见第 3.2.2 节，*加载内核模块*。

如果任意两张以太网卡使用相同的驱动程序（例如，两张 3c509，或者一张 3c595 和一张 3c905），你需要在驱动程序（针对 ISA 卡）的 `options` 行中提供两张卡的地址，或者（针对 PCI 卡）简单地每张卡添加一行 `alias`。

关于使用多张以太网卡的更多信息，请参见 http://metalab.unc.edu/LDP/HOWTO/Ethernet-HOWTO.html 上的 *Linux Ethernet-HOWTO*。如果你在安装 Red Hat Linux 时安装了 `howto` 软件包，你可以在文件 `/usr/doc/HOWTO/Ethernet-HOWTO` 中找到它。

## B 磁盘分区简介

磁盘分区是个人计算机领域的标准组成部分，并且已经存在了相当长一段时间。然而，随着购买预装操作系统计算机的人数众多，相对较少的人理解分区的工作原理。本章试图解释磁盘分区是如何工作的，以便让 Red Hat Linux 的安装尽可能简单。

如果你对磁盘分区有一定的了解，可以跳过本节，直接查看第 B.1.4 节，*为 Red Hat Linux 腾出空间*，以获取更多关于释放磁盘空间以准备 Red Hat Linux 安装的信息。本节还讨论了 Linux 系统使用的分区命名方案，与其他操作系统共享磁盘空间，以及相关主题。

### B.1 硬盘基本概念

硬盘执行一个非常简单的功能——它们存储数据并按命令可靠地检索它。

在讨论诸如磁盘分区等问题时，了解一些底层硬件知识是很重要的；不幸的是，容易陷入细节之中。因此，让我们使用一个简化的磁盘驱动器图来帮助我们解释“内部”发生了什么。图 B–1，*未使用的磁盘驱动器* 显示了一个全新的、未使用的磁盘驱动器。

#### 图 B-1 未使用的磁盘驱动器

![](img/eda1471ab4ce718c791c97a85559a478_295_0.png)

没什么好看的，不是吗？但如果我们在基本层面上谈论磁盘驱动器，这就够了。假设我们想在这个驱动器上存储一些数据。以目前的状态，它是行不通的。我们需要先做点什么……

#### B.1.1 重要的不是写什么，而是怎么写

观众中的老手可能第一次就理解了这个。我们需要**格式化**驱动器。格式化（在 Linux 术语中通常称为“创建**文件系统**”）将信息写入驱动器，在未经格式化的驱动器的空白空间中创建秩序。

#### 图 B-2 带有文件系统的磁盘驱动器

![](img/eda1471ab4ce718c791c97a85559a478_296_0.png)

如图 B-2，带有文件系统的磁盘驱动器所示，文件系统施加的秩序涉及一些权衡：

- 驱动器可用空间的一小部分被用来存储与文件系统相关的数据，可以被视为开销。
- 文件系统将剩余空间分成小的、大小一致的段。在 Linux 世界中，这些段被称为块。¹

鉴于文件系统使目录和文件成为可能，这些权衡通常被视为一个小代价。

值得注意的是，不存在单一、通用的文件系统；如图 B-3，具有不同文件系统的磁盘驱动器所示，磁盘驱动器上可能写入了许多不同文件系统中的某一个。正如你可能猜测的那样，不同的文件系统往往是不兼容的；也就是说，支持一种文件系统（或少数几种相关文件系统类型）的操作系统可能不支持另一种。然而，最后这句话并不是一条绝对的规则。例如，Red Hat Linux 支持多种文件系统（包括许多其他操作系统常用的文件系统），使数据交换变得容易。

![](img/eda1471ab4ce718c791c97a85559a478_297_0.png)

> 块确实是大致一致的，不像我们的插图。请记住，一个普通的磁盘驱动器包含成千上万个块。但为了本次讨论的目的，请忽略这些小的差异。

当然，将文件系统写入磁盘仅仅是个开始。这个过程的目标是实际*存储*和*检索*数据。让我们看看在写入一些文件后的驱动器。

#### 图 B-4 写入了数据的磁盘驱动器

![](img/eda1471ab4ce718c791c97a85559a478_298_0.png)

如图 B-4，写入了数据的磁盘驱动器所示，之前空的 14 个块现在正在保存数据。我们无法确定这个驱动器上有多少个文件；可能少到一个，多到 14 个，因为所有文件至少使用一个块。另一个需要注意的重要点是，已使用的块不一定形成连续的区域；已使用和未使用的块可能是交错的。这就是所谓的碎片化。碎片化在尝试调整现有分区大小时可能会起作用。

与大多数计算机相关技术一样，磁盘驱动器随时间不断变化。特别是，它们以某种特定方式发生了变化——它们变大了。不是在尺寸上变大，而是在容量上变大。正是这种额外的容量推动了磁盘驱动器使用方式的变化。

#### B.1.2 分区 – 将一个驱动器变为多个

随着磁盘驱动器容量的飙升，一些人开始质疑将所有这些空间放在一个大块中是否不是一个好主意。这种想法是由几个

