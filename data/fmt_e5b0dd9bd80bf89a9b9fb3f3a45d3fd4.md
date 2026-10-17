
花费大约五个工程师周将 Linux 转换为 Linux 服务器，并花费了两个工程师周将 Linux 服务器移植到 Power Mac。

承认，该移植可以复用一些机器相关的代码，但 Linux 服务器尚未使用这些组件。还需要移植的是：

- 描述页面大小和掩码的一些头文件
- 从 Mach 线程结构填充寄存器的系统调用例程
- 在 fork 系统调用期间初始化 Mach
- 信号传递例程，它将信号处理帧推到用户栈上。

# 第 10 章：MkLinux 概述

## 状态：Intel 平台

目前两个主要的缺失功能是虚拟控制（对于 X11 支持是必要的）以及动态缓冲区支持（缩小部分）。性能是合理的，尽管有很大的改进空间。

我们将尽快解决功能和性能问题。

## 状态：Power Mac 平台

在我们编写此论文时，Power Mac 刚刚通过最小文件系统启动了 Linux。它达到了“login”提示符并能够运行我们的大部分命令。我们有一组最小的驱动程序；使用串口作为控制台并可以访问 SCSI 磁盘。目前没有软盘、光驱、图形或网络驱动程序，但相关工作正在进行。

## Linux 代码库

目前的 Linux 基于 1.2.13 内核版本。它可以被视为 Linux 内核向新架构的移植：`osfmach3_i86` 和 `osfmach3_ppc`。

由于我们一直注意减少 Linux内核版本的更改，我们将尽快提供基于最新 1.3 内核（或可能是 1.4）的 Linux 服务器，但我们目前的优先任务是完成到 Power Mac 的移植。

## Linux 设备驱动程序

哥伦大学的一个团队开发了一个框架，可以在几乎不需要更改的情况下将 Linux 设备包含 Mach 中。这项工作是在 Mach 4 上完成的，但应该很容易适应 OSF MK。这将大大扩展微内核在 Intel x86 平台上的支持硬件列表。

## 168 MkLinux: 针对 Power Macintosh 的微内核 Linux

这是最近构建 OSF MK 所需要的。尽管这仍然需要更多工作，但 OSF MK 应该能够在运行 Linux（服务器版或单内核版）的 Intel x86 系统上，使用 GCC 编译器，为 x86 和 Power Mac 平台进行编译。

Linux 服务器是使用与普通 Linux 内核相同的方法和工具构建的。

由于被微内核与硬件隔离开，Linux 服务器可以与其他操作系统服务器共享同一台机器。事实上，它被作为一个普通的 OSF/1 进程开发的，从 shell 启动，并使用感知 Mach 版本的 GDB（该 GDB 可以处理多线程应用程序）进行调试。在每次测试之前，无需重新启动机器，并且它提供了完全的用户模式调试可能；从初次交互开始，就可以使用 GDB 对 Linux 服务器进行调试。

尽管 Linux 不支持多线程任务（至少不是我们希望的那种方式），但我们能够从另一个 Linux 服务器启动 Linux 服务器。而且，更广泛地说，人们可以在单台机器上并行运行任何所需的系统个性化（system personalities）。

可以使用 Intel x86 平台上强大的（尽管语法很奇怪）内核调试器对微内核进行调试，或者使用 Power Mac 的远程 GDB 进行调试。

## 可用性

OSF MK 微内核和 ODE 开发环境受 OSF 免费版权保护，允许在某些条件下免费使用源码和二进制文件、进行复制和分发，并对商业用途有某些限制。Linux 服务器受 GNU 通用开源许可证保护。

它们都可以从 OSF 开放软件商城 (`www.osf.org/mall/`) 免费获取。

## 相关工作

### BSD-Lite 服务器

Johannes Helander、Jukka Virtanen 以及芬兰的其他人员基于 4.4BSD 源代码开发了一个 BSD-Lite 服务器。该服务器具有一种架构

我们现在能够提供一个基于微内核的完全免费且无负担的环境。我们希望研究社区会发现这个环境对他们的微内核相关项目具有吸引力。

### 致谢

我们要感谢苹果公司（Apple Computer, Inc.）的 Brett Halle、Michael Burg 等人在微内核移植过程中提供的宝贵 Power Mac 专业知识。

感谢 Philippe Bernadat 帮助我们测量和分析系统性能。Philippe Bernadat 还帮助了 Intel x86 上 Linux 服务器支持的微内核增强。

我们还感谢一直将原生 Linux 移植到 PowerPC 的团队工作，特别是 Joseph Brothers、Daniel Puertas 和 Gary Thomas。

## 参考文献

- [Ace86a]

> Mike Accetta, Robert Baron, William Bolosky, David Golub, Richard Rashid, Avadis Tevanian, and Michael Young, Mack: A New Kernel Foundation For UNIX Development., USENIX Proceedings, pp. 93-112. Atlanta, Summer 1986.

- [Ber93a]

> Philippe Bernadat, Microkernel benchmarking techniques, OSF RI Symposium '93, 1993. 幻片

- [Bla95a]

> Philippe Bernadat, Christian Bruel, James Loveluck Eamann McManus, and Jose Rogado, A Performant Microkernel based OS for the HP PARISC, OSF RI Collected Papers, vol. 4, 1995.

- [Bry94a]

> David Black and Philippe Bernadat, Configurable Kernel Project Overview, OSF RI Collected Papers, vol. 4, 1995.

> Bill Bryant, Steve Sears, David Black, and Alan Langerman, Introduction to Mach 3.0's XMM system, OSF RI Collected Papers, vol. 2, 1994.

- [Bur94a]

> Peter Watkins, and Bill Wilcox, Ed Burke, Michael Condict, David Mitchell, Franklin Reynolds, RPC Design for Real-Time MACH, OSF RI Collected Papers, vol. 3, 1994.

- [Car95a]

> Joseph Carbononna, The Event Trace Analysis Package Design Specifications, OSF RI Collected Papers, vol. 4, 1995.

- [Fora]

> Bryan Ford and Jay Lepreau, Evolving Mach 3.0 to use Migrating Threads, UUCS-93-022.

- [Gol90a]

> David Golub, Randall Dean, Alessandro Forin, and Richard Rashid, UNIX as an Application Program, Usenix Conference Proceedings, Summer 1990.

- [Hay94a]

> Robert Haydt, Joseph Carbononna, and Franklin Reynolds, Mach Scheduling Framework, OSF RI Collected Papers, vol. 3, 1994.

- [Hut91a]

> N. C. Hutchinson and L. L. Peterson, The x-kernel: an Architecture for Implementing Network Protocols, IEEE Trans. on Software Eng., no. 1, pp. 64-76, Jan 1991.

- [Loe95a]

> Keith Loepere et al., MK++ Kernel High Level Design, 1995.

- [Pat93a]

# 172 MkLinux: 针对 Power Macintosh 的微内核

Simon Patience, Redirecting System Calls in Mach 3.0: An alternative to the emulator, OSF RI Collected Papers, vol. 1, 1993.

- [Roy93a]

> Paul Roy, David Black, Paulo Guedes, John Lo Verso, Durriya Netterwala, Faramarz Rabi from OSF RI, and Michael Barnett, Bradford Kemp, Michael Leibensberger, Chris Peak, and Roman Zajce from Locus Computing Corporation, An OSF/I UNIX for Massively Multi-computers, OSF RI Collected Papers, vol. 2, 1993.

- [Roz288a]

> M. Rozier et al., CHORUS Distributed Operating Systems, Computing Systems, vol. 1, no. 4, December, 1988.

- [Swa94a]

> Dan Swartzendruber, A preemptible MACH kernel, OSF RI Collected Papers, vol. 3, 1994.

- [Tra93a]

> Philippe Bernadat, Redirecting System Calls in Mach 3.0: An alternative to the emulator, OSF RI Collected Papers, vol. 1, 1993.

- [Tra94a]

> Joseph Carbononna and Franklin Reynolds, Mach Scheduling Framework, OSF RI Collected Papers, vol. 3, 1994.

- [Car95a]

> Joseph Carbononna, The Event Trace Analysis Package Design Specifications, OSF RI Collected Papers, vol. 4, 1995.

- [Vaha]

> Vahalia, UNIX Internals: The New Frontiers, Prentice-Hall.

The 论文传集

## 致谢

我们要感谢苹果公司（Apple Computer, Inc.）的 Brett Halle、Michael Burg 等人在微内核移植过程中提供的宝贵 Power Mac 专业知识。

感谢 Philippe Bernadat 帮助我们测量和分析系统性能。Philippe Bernadat 还帮助了 Intel x86 上 Linux 服务器支持的微内核增强。

我们还感谢一直将原生 Linux 移植到 PowerPC 的团队工作，特别是 Joseph Brothers、Daniel Puertas 和 Gary Thomas。

# 生平

François Barbou des Places 于 1987 年在巴黎十一大学获得计算机科学硕士学位，并在 1989 年从格勒诺的国立 Ecole Supieure d'Informatique et de Mathématiques Appliques 毕业。他目前在 OSF 任工程师。

Nick Stephen 于 1990 年在英国南安普敦大学获得计算机科学一等荣誉学士学位。他目前在 OSF 任工程师。

Franklin Reynolds 从业行业多年。在过去的六年里，他一直在位于马诸塞的开放基金会工作。

... 可用系统

本文描述的工作（Linux 服务器和微内核的移植）部分得到了苹果公司的支持，他们还提供了关于 Power Mac 的有用技术信息。

## 第11 章：

- 兼容性问题
- 帮助！
- 硬件信息

## 硬件概览

许多 Mac OS 用户对操作系统和应用程序下方的硬件毫无兴趣。如果你希望以相同的方式对待 MkLinux，我们没有任何异议。事实上，我们非常高兴 MkLinux 允许这种用法！

某些 MkLinux 用户可能查看内部。如果你属于这一类，你会发现接几章非常有用且有趣。我们涵盖了从设备、控制到接口、处理器描述和芯片使用的各种硬件问题。

此外，PTF 参考盘包含了许多苹果提供的有用硬件文档。如果你愿意跳过 Mac OS 特有的部分，可能会找到你需要的全部。

### 兼容性问题

苹果的工程师努力（并成功地！）隐藏了不同 处理器之间的差异。然而，不同型号之间存在相当大的差异。Mac OS 和 MkLinux 的编程人员都需要非常仔细地处理这些问题，以免导致用户（以及第三方程序员）陷入困境。

由于 Power Macintosh 已上市多年，Apple MkLinux 团队有大量的追赶工作要做。尽管如此，我们预计他们将支持 Power Macintosh 系列。为了理解涉及的工作量，回顾一下个人电脑历史可能会帮助。最初的“IBM PC”电脑实际上是由国际机器公司（IBM）制造的。而且，在 PC 的大部分历史中，IBM 是

事实上的定义权威。当时并不存在官方的标准机构；事实上，IBM 并不热衷于发布其规范。

因此，当各种厂商试图营销“PC 兼容”机器时，用户们采用了一个简单但又有些粗暴的测试方法：“我的所有软件在这台机器上的运行方式，与在‘真实’IBM PC 上的运行完全一样。”如果一台电脑通过了这个测试，它就是兼容的；否则，它就会被作为缺陷品退回给供应商。

这一测试过程产生了两个结果。首先，PC 硬件工程师学会了设计“缺陷级兼容”（bug-for-bug compatible）的主板和接口卡，这并不是一个完全理想的结果，但它满足了 PC 用户对廉价、实用且可靠机器的即时需求。

另一个至今仍困扰着操作系统的编写者，那就是硬件供应商只认为没在流行的软件（MS-DOS 和一小部分应用程序）上测试他们的硬件。如果任何其他操作系统无法处理特定 PROM 组的变幻，那也太遗憾了！

与此同时，Apple 和 Sun 等公司的工程师面临着完全不同的限制：在最少（读作：最便宜的）芯片和设备中装入最大的功能。如果在此过程中软件接口发生了变化，没问题。操作系统的代码可以随时修改以处理硬件变化（这只是简单的软件问题！）。

鉴于这些厂商产生的各种机器架构，系统软件能够处理所有的硬件组合，更不用说处理新的硬件特征以及（噢，没错！）添加新的软件（例如，用户界面）点缀功能了，这相当令人惊讶。

现在，我们必须展示了。来自 Apple 公司和开放小组研究学会（Open Group Research Institute）的一小部分程序员被赋予了让基于 Mach 的 Linux 变体在所有基于 PowerPC 的 Macintosh 系统上运行。这些系统总共使用了三十多个专用芯片，此外还有几种 CPU 实现方式以及各种不一的现成支持芯片。

显然，MkLinux 移植团队有大量工作要做。同样明显的是，如果 MkLinux 用户社区的成员不想等待一段时间的解决方案，他们必须帮助解决一些更晦涩的问题（例如特定 Performa 型号音频支持）。

Apple MkLinux 团队规模极小；只有几位工程师。因此，预计 MkLinux 社区将测试版本、报告错误并（在可能的情况下）建议解决方案。通过积极利用数千名测试人员的服务，我们可以帮助团队找出错误、硬件设计特殊性等。一旦完成，我们就可以继续移植应用程序，甚至（天哪！）使用该系统了……

# 来帮忙吧！

如果你对参与移植工作感兴趣，请访问 MkLinux 网站。那里有一个专门介绍正在进行的项目的区域，以及尚未着手的项目。

如果你觉得某个项目对你来说很有趣，请联系相关人员，告诉他们你的背景、兴趣等。如果似乎很匹配，你将获得一个要执行的任务。做得好，你的名字将名扬四起；如果失败了，你将在名得其实的寂寥中度日。

说真的，对于感兴趣的程序员（包括内核和应用层）有巨大的空间来帮助 MkLinux 成为一个更好的系统。我们需要许多类型的驱动程序，数百个应用程序包需要移植，还有数以亿计的有用 HOWTO 待编写。来帮忙吧！

## 硬件信息

接下来的章节包含计算机硬件信息，特别强调了 Power Macintosh 系统。这些材料大部分改编自 Apple 的文档，包括《Inside Macintosh》和参考库（开发者 CD 系列）光盘版。

关于这些文档的原始版本，请参阅 PTF 参考光盘和 Apple 出版物本身。然而，请注意，原始版本包含大量 Mac OS 特有的信息，你将需要仔细寻找（正如我们做的那样）以找到特定的硬件信息。

# 第 12 章：

- CD-ROM 驱动器
- 软磁盘驱动器
- 硬盘驱动
- 中断按钮
- 键盘
- 显示器
- 鼠标
- 电源开关
- 开机灯
- 重置按钮

# 控制与设备

Power Macintosh 系统与传统的 PC 不同，默认配备了大量的控制和设备。在编写时，Linux 不支持所有这些项目。然而，我们预计它们在不久的将来将获得支持。

无论如何，本章是对这些项目的高级总结，并强调了它们的某些特性。Power Macintosh 系统上控制和设备的具体配置可能会有所。尽管如此，任何 Power Macintosh 系统将拥有本章涵盖的大部分控制和设备：

> 注意：有关你系统中控制和设备的具体配置和位置，请审阅随系统附带的用户指南（或相应文档）中的描述和图表。

# CD-ROM 驱动器
