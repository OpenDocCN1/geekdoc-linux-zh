

或开发新的基于 ATCA 的平台。ATCA 平台的主要应用是载波级电信交换和传输设备，以及高端数据中心服务器和存储设备。

ATCA 平台正在引领行业趋势，逐渐远离内部专有的硬件和软件平台。许多电信和网络市场的大型设备制造商已缓慢地从自定义、内部设计的硬件平台转向其他方案。这种趋势在软件平台中也很明显，从操作系统到所谓的中间件（如高可用性和协议栈解决方案）。缩小规模和上市时间压力是推动这一趋势的两个关键因素。

ATCA 由若干 PICMG 规范定义。表 3-11 总结了这些规范。

| 规范 | 摘要 |
|:--- |:--- |
| PICMG 3.0 | 机械规范，包括互连、电源、冷却和基础系统管理 |
| PICMG 3.1 | 以太网和光纤通道交换矩阵接口 |
| PICMG 3.2 | Infiniband 交换矩阵接口 |
| PICMG 3.3 | StarFabric 接口 |
| PICMG 3.4 | PCI Express 接口 |
| PICMG 3.5 | RapidIO 接口 |

本节描述的平台是当今任何关于嵌入式 Linux 平台的讨论中最相关的。特别是对于 ATCA，行业正越来越多地转向商业现货（COTS）技术。ATCA 和 Linux 都在这一行业趋势中扮演着日益重要的角色。

### 3.4 本章摘要

- 许多独立处理器在 Linux 下得到支持。其中最广泛支持的是 IA32/IA64 和 PowerPC 架构。这些独立处理器被用作构建块，以构建高性能计算引擎。我们介绍了来自 Intel、IBM 和 Freescale 的若干示例。
- 集成处理器，即片上系统（SOC），主导了嵌入式 Linux 格局。许多供应商和几种流行架构用于嵌入式 Linux 设计。本章按架构和制造商介绍了其中一些最流行的架构。
- 一种日益流行的趋势是远离专有硬件和软件平台，转向商业现货（COTS）解决方案。两个在嵌入式 Linux 系统中广泛使用的流行平台：cPCI 和 ATCA。

#### 3.4.1 延伸阅读建议

PowerPC 32 位架构参考手册：

*Programming Environments Manual for 32-Bit Implementations of the PowerPC Architecture—Revision 2*

Freescale Semiconductor, Inc.
www.freescale.com/files/product/doc/MPCFPE32B.pdf

PowerPC 64 位架构参考：

The *Programming Environments Manual for 64-Bit Microprocessors—Version 3.0*

International Business Machines, Inc.

PowerPC 架构简要总结：

A *Developer’s Guide to the POWER Architecture*

Brett Olsson, Processor Architect, IBM Corp.
Anthony Marsala, Software Engineer, IBM Corp.
www-128.ibm.com/developerworks/linux/library/l-powarch/

Intel XScale 总结页面
www.intel.com/design/intelxscale/

## 第 4 章
## Linux 内核——另一种视角

本章内容
- 背景 第 66 页
- Linux 内核构建 第 70 页
- 内核构建系统 第 79 页
- 获取 Linux 内核 第 96 页
- 本章摘要 第 97 页

> 如果你想了解内核内部机制，市面上有很多关于内核设计和操作的优质书籍。本章及全书其他章节的 4.5.1 节“延伸阅读建议”中介绍了几本这样的书。然而，关于从项目角度如何看待内核的组织结构和布局，相关著述极少。如果你正在寻找为新的嵌入式项目添加定制支持的正确位置，该怎么做？你如何知道哪些文件对你的架构很重要？

乍一看，理解 Linux 内核以及如何为特定平台或应用配置它似乎是一项几乎不可能的任务。在最近的 Linux 内核快照中，Linux 内核源代码树由超过 20,000 个文件组成，包含超过六百万行代码——而这仅仅是个开始。你仍然需要工具、根文件系统和许多 Linux 应用程序才能构建一个可用的系统。

本章介绍 Linux 内核，涵盖内核的组织方式以及源代码树的结构。然后，我们考察构成内核镜像的组件，并讨论内核源代码树的布局。接着，我们详细介绍内核构建系统以及驱动内核配置和构建系统的文件。本章最后通过考察完整嵌入式 Linux 系统所需的内容来结束。

### 4.1 背景

Linus Torvalds 在芬兰赫尔辛基大学就读时编写了 Linux 的原始版本。他的工作始于 1991 年。同年 8 月，Linus 在 **comp.os.minix** 上发布了这条如今著名的公告：

```
From: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)
Newsgroups: comp.os.minix
Subject: What would you like to see most in minix?
Summary: small poll for my new operating system
Message-ID: <1991Aug25.205708.954@klaava.Helsinki.FI>
Date: 25 Aug 91 20:57:08 GMT
Organization: University of Helsinki
```

大家好，使用 minix 的各位 -

> 我正在做一个（免费的）操作系统（只是一个爱好，不会像 gnu 那样庞大和专业），适用于 386(486) AT 克隆机。自四月以来，它一直在酝酿中，现在开始准备就绪。希望得到任何关于人们喜欢/不喜欢 minix 中哪些方面的反馈，因为我的操作系统在某种程度上与其相似（由于实际原因，文件系统的物理布局相同，以及其他方面）
> 
> 我目前移植了 bash(1.08) 和 gcc(1.40)，一切似乎都能正常工作。这意味着我将在几个月内得到一些实用的东西，我希望知道大多数人希望有什么功能。欢迎提出建议，但我不会承诺实现它们 :-) 
> 
> Linus (torvalds@krucna.helsinki.fi)
>
> P.S. 是的 - 它不含任何 minix 代码，并且具有多线程文件系统。它不具备可移植性（使用 386 任务切换等），并且可能永远不会支持除 AT 硬盘以外的任何东西，因为我只有那些 :-)。

自最初发布以来，Linux 已发展为一个功能齐全的操作系统，具有强健性、可靠性，以及可与最优质的商业操作系统相媲美的高级功能。据一些估计，Web 上超过一半的互联网服务器是由 Linux 服务器驱动的。在线搜索巨头 Google 使用一组运行容错版 Linux 的低成本 PC 来实现其流行搜索引擎，这已不是秘密。

#### 4.1.1 内核版本

你可以在许多地方获取 Linux 内核及互补组件的源代码。你当地的书店可能拥有几个作为 Linux 书籍配套 CD-ROM 的版本。你也可以从互联网上的许多位置下载内核本身，甚至完整的 Linux 发行版。Linux 内核的官方网站位于 www.kernel.org。你经常听到术语 *mainline source* 或 *mainline kernel*，指的是 kernel.org 上找到的源代码树。

本书编写期间，Linux 版本 2.6 是当前版本。在开发周期早期，开发者选择了一种编号系统，旨在区分用于开发和实验的内核源代码树与用于稳定、生产就绪内核的源代码树。编号方案包含主版本号、次版本号和序列号。在 Linux 版本 2.6 之前，如果次版本号是偶数，则表示生产内核；如果是奇数，则表示开发内核。例如：

- Linux 2.4.x---生产内核
- Linux 2.5.x---实验（开发）
- Linux 2.6.x---生产内核

目前，Linux 2.6 内核没有单独的开发分支。所有新功能、增强和修复都通过一系列把关人，他们最终过滤并将更改推送到由 Andrew Morton 和 Linus Torvalds 维护的顶层 Linux 源代码树。

了解你正在使用的内核版本非常容易。内核源代码树中顶层 *makefile*¹ 的前几行详细说明了特定实例所代表的精确内核版本。对于 2.6.14 生产内核，它看起来像这样：

```
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 14
EXTRAVERSION =
NAME=Affluent Albatross
```

在同一个 makefile 的后半部分，这些宏被用来形成一个版本级宏，如下所示：

```
KERNELRELEASE=$ {VERSION} . $ {PATCHLEVEL} . $ {SUBLEVEL} $ {EXTRAVERSION}
```

该宏在内核源代码树的多个地方用于指示内核版本。事实上，版本信息的使用频率之高，以至于内核开发者专门从 makefile 中的版本宏派生出一组宏。这些宏位于 Linux 内核源代码树中的 **.../include/linux/version.h**²。它们在下面的列表 4-1 中重现。

**列表 4-1**

**内核包含文件：.../include/linux/version.h**

```
#define UTS_RELEASE "2.6.14"
#define LINUX_VERSION_CODE 132622
#define KERNEL_VERSION(a,b,c) (((a) << 16) + ((b) << 8) + (c))
```

你可以在运行中的 Linux 系统的命令行提示符下像这样检查内核版本：

```
$ cat /proc/version
Linux version 2.6.13 (chris@pluto) (gcc version 4.0.0 (DENX ELDK 4.0.0.0)) #2 Thu Feb 16 19:30:13 EST 2006
```

关于内核版本的最后一点说明：通过自定义 **EXTRAVERSION** 字段，可以轻松地在你自己的内核项目中跟踪内核版本。

¹ 我们稍后会讨论内核构建系统和 makefile。
² 在本书中，任何路径前的三个点用于指示在你系统中到达顶层 Linux 源代码树所可能采取的任何路径。

