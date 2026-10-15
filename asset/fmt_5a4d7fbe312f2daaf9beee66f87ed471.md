
- PCI 设备

- ISA 设备

所有系统都使用 Intel 系统 I/O 桥接器（SIO）作为 PCI 和 ISA（主 I/O 总线是 PCI，ISA 总线是用于支持低速和“传统”I/O 设备的次要总线）之间的桥接器。SIO 包含传统的级联 8259 对。

一些系统（例如 Noname）将其所有中断通过 SIO 然后路由到 CPU。一些系统具有单独的中断控制器，并将所有 PCI 中断加上 SIO 中断（8259 输出）通过该控制器路由，而所有 ISA 中断则通过 SIO 路由。系统之间的其他差异包括：

- 它们拥有多少个插槽

- 它们拥有哪些板载 PCI 设备

- 它们使用的是 Flash 还是 EPROM

### C.11 更多信息

所有 DS 评估板和主板设计都是免许可的，整个设计的文档套件成本约为 50 美元。其中包括所有原理图、可编程部件源代码、CPU 和支持芯片组的数据表。文档套件可从 Digital 半导体分销商处获得。我并不是建议很多人会急于去买这个，但我确实想指出这些信息是可获取的。

希望这有帮助。对 Neal Crook 提出评论/更新/扩展建议，邮箱：`neal.crook@reo.mts.digital.com`

### C.12 参考文献

`http://www.research.digital.com/wrl/publications/abstracts/TN-13.html`

Bill Hamburgen, Jeff Mogul, Brian Reid, Alan Eustace, Richard Swain, Mary Jo Doher ty, and Joel Bartlett. Characterization of Organic Illumination Systems. DEC WRL, Technical Note 13, April 1989.

# 附录 D

## Alpha 迷你加载器指南（HOWTO）

### D.1 简介

本文档描述了用于 Alpha AXP 上的 Linux 的迷你加载器（MILO）。该固件用于初始化基于 Alpha AXP 的系统、加载并启动 Linux，最后为 Linux 提供 PALcode。

#### D.1.1 版权

Alpha 迷你加载器（MILO）HOWTO 的版权属于 (C) 1995, 1996, 1997 年 David A Rusling。

版权。像所有 Linux HOWTO 文档一样，它可以整体或部分复制和分发，在任何介质上（无论是物理还是电子），只要在所有副本上保留此版权声明。允许并鼓励商业再分发；但作者希望能够收到此类分发的通知。您可以将此 HOWTO 翻译成任何语言，前提是保留此版权声明和免责声明不变，并附加一份通知，说明谁翻译了该文档。

免责声明。虽然我尽力包含了我能获取的最准确和最新的信息，但我无法保证使用本文档中的信息不会导致数据或设备丢失。我对 HOWTO 中的信息不提供任何保证，也不能因使用本文档中的信息而产生的任何后果承担责任。

#### D.1.2 本文档的新版本

本文档的最新版本可以在

`ftp://gatekeeper.dec.com/pub/Digital/Linux-Alpha/MiniLoader/docs`

找到，David Mosberger-Tang 好心地在他的优秀的 Linux Alpha FAQ 网站中包含了它的 HTML 格式

`http://www.azstarnet.com/~expilinux`。

### D.2 什么是 MILO？

在基于 Intel 的 PC 系统中，BIOS 固件设置系统，然后从 DOS 文件系统的引导块加载要运行的映像。MILO 在基于 Alpha 的系统上所做的或多或少就是这样，不过 BIOS 固件和 MILO 之间有几个有趣的差异，最不明显的是 MILO 包含并使用未经修改的标准 Linux 设备驱动程序。MILO 是固件，不同于依赖 BIOS 固件来加载自身的 LILO。MILO 的主要功能部分包括：

1. PALcode，

2. 内存设置代码（构建页表并开启虚拟寻址），

3. 视频代码（BIOS 模拟代码和 TGA (21030)），

4. Linux 内核代码。这包括真实的 Linux 内核代码（例如，中断处理）和替代或模拟的 Linux 内核，

5. Linux 块设备驱动程序（例如，软盘驱动程序），

6. 文件系统支持（ext2, MS-DOS 和 ISO9660），

7. 用户界面代码（MILO），

8. 内核接口代码（为 Linux 设置 HWRPB 和内存映射）。

9. 管理环境变量的 NVRAM 代码。

接下来的段落将更详细地描述这些功能部分。

可以将 PALCode 视为一个微小的软件层，用于将芯片定制为适应特定的操作系统。它运行在一种特殊模式（PALmode）下，该模式具有限制条件，但它使用标准的 Alpha 指令集，并额外增加了指令。通过这种方式，Alpha 芯片可以运行 Windows NT、OpenVMS、Digital Unix 以及当然还有 Linux 等多样化的操作系统。MILO 使用的（因此也是 Linux 本身使用的）PALCode 与 MILO 的其他部分一样，是自由软件。它源自 Digital 的评估板软件示例 Digital Unix PALCode。不同 PALCode 之间的差异源于不同 Alpha 芯片之间在地址映射和中断处理方面存在的差异（基于 21066 的系统与 21064+2107x 系统具有不同的 I/O 映射），以及不同 Alpha 架构系统之间的差异。

为了让 MILO 正常工作，它需要知道可用的内存、Linux 最终将从何处运行，并且必须能够为 Linux 设备驱动程序分配临时内存。该代码维护一个内存映射，其中包含永久分配页和临时分配页的条目。在启动过程中，MILO 会将自身解压到物理内存中的正确位置。当它将控制权交给 Linux 内核时，它会为自身的压缩版本、PALCode（内核需要此部分）以及一些数据结构预留内存。这为 Linux 本身留出了系统中大部分内存。

内存代码的最后一步是设置并开启虚拟寻址，以便 Linux 期望看到的数据结构位于虚拟内存的正确位置。

MILO 包含视频代码，用于初始化并使用系统的视频设备。如果存在 VGA 设备，它将检测并使用该设备；否则，它将尝试使用 TGa (21030) 视频设备。如果上述尝试均失败，它将假设没有图形设备。标准预构建映像中包含的 BIOS 模拟是 Digital 自己的 BIOS 模拟，它支持几乎所有（如果不是全部）可用的标准图形设备。

Linux 设备驱动程序驻留在内核中，并期望内核提供某些服务。其中一些服务由 Linux 内核代码直接提供，例如中断处理；另一些服务则由内核类似例程提供。

MILO 最强大的功能是可以将未经修改的 Linux 设备驱动程序嵌入其中。这使其具备支持所有 Linux 支持的设备的能力。MILO 包含了构建时所针对的 Linux 内核中配置的所有块设备，以及大量的块设备代码（例如，`ll_rw_blk()`）。

MILO 从真实的文件系统加载 Linux 内核，而不是从引导块或其他奇怪的地方加载。它支持 MSDOS、EXT2 和 ISO9660 文件系统。支持 Gzip 压缩的文件系统，并推荐使用这些系统，特别是当你从速度较慢的软盘加载时。MILO 通过 `.gz` 后缀识别这些文件。

MILO 内置了一个简单的键盘驱动程序，配合同样简单的视频驱动程序，使其拥有简单的用户界面。该界面允许你列出配置设备上的文件系统、启动 Linux、运行闪存更新工具以及设置控制系统引导的环境变量。像 LILO 一样，你可以向内核传递参数。

MILO 必须告知 Linux 内核系统类型、内存容量以及哪部分内存是空闲的。它使用 HWRPB（硬件重启参数块）数据结构及相关内存簇描述信息来实现这一点。这些数据结构在控制权传递给 Linux 内核之前，被放置在虚拟内存的适当位置。

### D.3 预构建的标准 MILO 映像

如果你计划在标准的基于 Alpha 的系统上运行 Linux，那么可以使用预构建的“标准” MILO 映像。这些文件（连同源代码和其他有趣的内容）可以在 `ftp://gatekeeper.dec.com/pub/Digital/Linux-Alpha/MiniLoader` 中找到。

`images` 子目录包含每个标准系统（例如 AlphaPC64）的目录，MILO 映像的命名约定如下：

- MILO - Miniloader 可执行映像，此映像可以通过多种方式加载，

- fmu.gz - 闪存管理工具，

- `MILO.dd` - 引导块软盘映像。这些应使用 `rawrite.exe` 或 Linux 上的 `dd` 进行写入。

**test-images** 与 **images** 子目录类似，包含每个标准系统的目录。这些映像具有一定的实验性质，但往往包含所有最新功能。

### D.4 如何构建 MILO
