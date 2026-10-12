
## D.9 Alpha 架构备注

32 位和 64 位的加载和存储操作（即 Digital 术语中的长字和双字）。联合架构师（Dick Sites, Rich Witek）通过引用以下优势来证明这一决策的合理性：

- 缓存和内存子系统对字节的支持往往会减慢对 32 位和 64 位数据的访问速度。
- 字节支持使得在缓存/内存子系统中构建高速纠错电路变得困难。

Alpha 通过提供强大的指令来操纵 64 位寄存器内的字节和字节组进行了补偿。字符串操作的标准基准测试（例如某些 Byte 基准测试）表明，Alpha 在字节操纵方面表现出色。

缺少字节加载和存储指令会影响某些软件信号量的实现，并影响 I/O 子系统的设计。Digital 解决 I/O 问题的方案是使用一些低位地址线在 I/O 传输期间指定数据大小，并将这些线解码为字节使能。这种所谓的稀疏寻址（Sparse Addressing）浪费了地址空间，并导致 I/O 空间不连续（关于稀疏寻址的复杂性，等我找到时间写出来时再详细说明）。请注意，在此上下文中，I/O 空间指的是位于 PCI 上的所有系统资源，因此既包括 PCI 内存空间，也包括 PCI I/O 空间。

随着 21164A 的引入，Alpha 架构经过工程变更（ECo）以包含字节寻址。在早期 CPU 上执行这些新指令将导致 OPCDEC PALCode 异常，从而由 PALCode 来处理该访问。这将带来性能影响。其结果是，使用这些新指令（在我看来）应仅限于设备驱动程序，而非应用程序代码。

这些新的字节加载和存储指令意味着未来的支持芯片组将能够支持连续的 I/O 空间。

### D.9 PALCode 及相关内容

这是解释 PALCode 的章节占位符。如果有足够的兴趣，我会撰写它。

## D.10 移植

任何基于 Alpha 的机器运行 Linux 的能力实际上仅受限于你获取其内部结构细节信息的能力。由于 E66、EB64+ 和 EB164 主板已有 Linux 移植版本，所有基于 21066、21064/APECS 或 21164/ALCOR 的系统只需很少或无需修改即可运行 Linux。这些主板之间的主要区别在于它们路由中断的方式。中断有三个来源：

- 板载设备
- PCI 设备
- ISA 设备

所有系统都使用 Intel 系统 I/O 桥（SIO）作为 PCI 和 ISA 之间的桥接器（主 I/O 总线是 PCI，ISA 总线是用于支持低速和“传统”I/O 设备的次要总线）。SIO 包含传统的级联 8259 中断控制器对。

某些系统（例如 Noname）将其所有中断通过 SIO 路由到 CPU。某些系统具有单独的中断控制器，并将所有 PCI 中断加上 SIO 中断（8259 输出）通过该控制器路由，而所有 ISA 中断则通过 SIO 路由。

系统之间的其他差异包括：

- 它们有多少插槽
- 它们有哪些板载 PCI 设备
- 它们是否有 Flash 或 EPROM

## D.11 更多信息

所有 DS 评估板设计均免费授权，一套设计的完整文档套件价格约为 50 美元。这包括所有原理图、可编程部件源码、CPU 和支持芯片组的数据手册。文档套件可从 Digital Semiconductor 分销商处获得。我并不是建议许多人会想要立刻冲出去购买这套资料，但我确实想指出这些信息是可以获得的。

希望这有帮助。如有评论/更新/扩展建议，请致信 Neal Crook，neal.crook@reo.mts.digital.com

## D.12 参考文献

http://www.research.digital.com/wrl/publications/abstracts/TN-13.html
Bill Hamburgen, Jeff Mogul, Brian Reid, Alan Eustace, Richard Swan, Mary Jo Doherty, and Joel Bartlett. Characterization of Organic Illumination Systems. DEC WRL, Technical Note 13, April 1989.

# 附录 E

# Alpha Miniloader 使用指南

本文档描述了 Miniloader，这是一个用于 Alpha 系统的程序，可用于初始化机器并加载 Linux。Alpha Linux Miniloader（全称）也被称为 Milo。

## E.1 介绍

本文档描述了 Alpha AXP 上 Linux 的 Miniloader（Milo）。此固件用于初始化基于 Alpha AXP 的系统，加载并启动 Linux，并最终为 Linux 提供 PALCode。

### E.1.1 版权

Alpha Miniloader (Milo) HOWTO 的版权 ©1995, 1996 David A Rusing 所有。

> **版权** 与其他所有 Linux HOWTO 文档一样，本文件可以完整或部分地以任何物理或电子介质进行复制和分发，前提是保留所有副本上的此版权声明。允许并鼓励商业再分发；但是作者*希望*在发生此类分发时得到通知。您可以将此 HOWTO 翻译成任何语言，只要*保留此版权声明和*

免责声明原封不动，并添加一份通知说明谁翻译了该文档。

**免责声明** 尽管我已尽力包含我能获得的最准确和最新的信息，但我无法保证使用本文件中的信息不会导致数据或设备丢失。我对 HOWTO 中的信息不提供任何保修，我也不会因使用本 HOWTO 中的信息而产生的任何后果承担责任。

### E.1.2 本文档的新版本

本文档的最新版本可在 `ftp://gatekeeper.dec.com/pub/` 找到，David Mosberger-Tang 也很乐意在他优秀的 Linux Alpha FAQ 网站 `http://www.azstarnet.com/~explinux` 中包含其 html 形式。

## E.2 什么是 Milo？

在基于 Intel 的 PC 系统上，BIOS 固件设置系统，然后从 DOS 文件系统的引导块中加载要运行的映像。这在很大程度上就是 Milo 在基于 Alpha 的系统上做的事情，然而 BIOS 固件和 Milo 之间存在一些有趣的差异，最值得注意的是 Milo 包含并未经修改地使用了标准 Linux 设备驱动程序。Milo 是固件，而 LILo 则依赖于 BIOS 固件来加载自身。Milo 的主要功能部分是：

1. PALCode，
2. 内存设置代码（构建页表并开启虚拟寻址），
3. 视频代码（BIOS 仿真代码和 TGA (21030)），
4. Linux 内核代码。这包括真实的 Linux 内核代码（例如，中断处理）和仿制或模拟的 Linux 内核，
5. Linux 块设备驱动程序（例如，软盘驱动程序），
6. 文件系统支持（ext2、MS-DOS 和 ISO9660），
7. 用户界面代码（MILO），
8. 内核接口代码（为 linux 设置 HWRPB 和内存映射），
9. 用于管理环境变量的 NVRAM 代码。

以下段落更详细地描述了这些功能部分。

PALCode 可以被视为一个微小的软件层，它将芯片定制为特定的操作系统。它在一种特殊模式（PALmode）下运行，该模式有一定限制，但它使用标准的 Alpha 指令集，仅增加五条指令。通过这种方式，Alpha 芯片可以运行诸如 Windows NT、OpenVMS、Digital Unix 以及当然 Linux 这样多样化的操作系统。Milo 使用的 PALCode（因此 Linux 本身也是）与 Milo 的其他部分一样，是自由软件。它源自 Digital 的评估板软件示例 Digital Unix PALCode。不同 PALCode 之间的差异是由于 Alpha 芯片之间存在的地址映射和中断处理的差异（基于 21066 的系统与基于 21064+2107x 的系统具有不同的 I/O 映射），以及不同基于 Alpha 的系统之间的差异。

为了使 Milo 正常工作，它需要知道可用的内存是什么，Linux 最终将从哪里运行，并且必须能够为 Linux 设备驱动程序分配临时内存。该代码维护一个内存映射，其中包含永久分配页和临时分配页的条目。在启动过程中，Milo 将自身解压到物理内存中的正确位置。当它将控制权传递给 Linux 内核时，它会保留压缩版本自身、PALCode（内核所需）和一些数据结构的内存。这使得系统中大部分内存留给了 Linux 本身。

内存代码的最后一步是设置并开启虚拟寻址，以便 Linux 期望看到的数据结构位于虚拟内存中的正确位置。

Milo 包含视频代码，用于初始化和使用系统的视频设备。如果有 VGA 设备，它会检测并使用它，否则它会尝试使用 TGA (21030) 视频设备。如果都失败，它会假设没有图形设备。标准预构建映像中包含的 BIOS 仿真是 Digital 自己的 BIOS 仿真，它支持大多数，如果不是全部，可用的标准图形设备。

