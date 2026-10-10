
本书为初级和中级 GNU/Linux 程序员编写，他们希望学习学习如何在 GNU/Linux 操作系统上开发应用程序，或将其知识扩展到更高级的开发领域。本书涵盖了工具、API 和技术，并有许多示例说明了 GNU/Linux API 的用法。

本章详细介绍了自由软件和开源开发范式，包括一些适用于自由软件的许可证。讨论了被称为“自由软件”和“开源”的两种主要的开放开发类型，以及这些领域存在的一些问题。

# 第 4 章：LINUX 虚拟化与仿真

虚拟化是一种允许多个操作系统在同一台机器上并发执行的技术。操作系统不需要是同一种类型，也不需要相同的架构（x86、PowerPC 等）。本章探索了虚拟化技术的基础，然后介绍了为 Linux 可用的一些虚拟化和仿真选项。

# 第 1 章 GNU/Linux 历史

## 本章内容

- UNIX 历史
- 理查德·斯托曼（Richard Stallman）与 GNU 运动
- 林纳·托瓦尔斯（Linus Torvalds）与 Linux 内核

## 引言

在进入 GNU/Linux 的技术方面之前，让我们花一点时间了解 GNU/Linux 操作系统的历史（以及我们为什么使用 GNU/Linux 这个术语）。我们将通过回顾它的两个主要来源以及实现它的两个关键人物。

## UNIX 操作系统的历史

为了理解 GNU/Linux，让我们先回到 1969 年查看 UNIX 操作系统的历史。尽管 UNIX 已经存在了 30 多多年，但它是有以来创建的最灵活、最强大的操作系统之一。图 1.1 显示了时间线。

UNIX 的目标是提供一个支持应用程序移植性的多任务、多用户操作系统。这一传统在所有 UNIX 变体中一直延续，并且考虑到操作系统可移植性（运行在许多平台上的）的新视角，UNIX 继续演进和增长。

## GNU/Linux 应用编程

![](img/f7bd35eb87a62f74c6f23c07df847dff_24_0.png)

## AT&T UNIX

UNIX 起于 1969 年 AT&T 贝尔实验室针对 DEC PDP-7 的小型研究项目。丹尼斯·里奇（Dennis Ritchie）和肯·汤普（Ken Thompson）设计并构建了 UNIX，旨在取代当时的 Multics 操作系统。

在 Multics 从 AT&T 退出后，Thompson 和 Ritchie 在 PDP-7 上开发了 UNIX，为了玩当时流行的游戏《太空旅行》（UNIX/Linux History04）。

## BSD

BSD（伯克利软件发行版）于 1976 年在加州大学伯克利分校作为 UNIX 的分支被创建。BSD 不仅是 GNU/Linux 的强大竞争对手，在许多方面更为优越。BSD 创建了许多创新，包括 Sockets 网络编程范式和各种 IPC 机制（在本书第三部分“应用开发主题”中讨论）。我们今天在 GNU/Linux 中发现许多实用程序都源自 BSD。例如，vi 编辑器和 termcap（允许以与显示无关的方式显示）是由比·乔（Bill Joy）于 1978 年在伯克利创建的 [Byte94]。

BSD 和 GNU/Linux 主要区别之一是许可。我们将在第三章“自由软件开发”中解决这一差异。

## GNU/Linux 历史

GNU/Linux 的历史实际上两个独立的故事汇合在一起，产生了一个世界级的操作系统。理查德·斯托曼创建了一个组织来构建类 UNIX 操作系统。他拥有工具、编译器和各种应用程序，但他缺少一个内核。林纳·托瓦尔斯拥有内核，但没有可以使其发挥用的工具或应用程序。

关于 GNU/Linux 的一个争议性问题是为什么它被称为 GNU/Linux，而不是常用的名称 Linux。答案很简单。Linux 指的是内核（或操作系统的核心），它最初由林纳·托瓦尔斯开发。其余软件——Shell、编译器工具链、实用工具和大量的应用程序——运行在内核之上。这些软件大部分都是 GNU。事实上，构成 GNU/Linux 操作系统的代码规模远大于内核。因此，将整个操作系统称为 Linux 至少说法是不准确的。

理查德·斯托曼在他的《Linux 与 GNU 项目》（Linux/GNU04）中对这一争议提供了一个有趣的视角。

## GNU 与自由软件基金会

开源之父理查德·斯托曼于 1983 年在 net-unix-users Usenet 组发布了一封帖子，寻求开发一个自由且兼容 UNIX 的操作系统的帮助 [Stallman83]。

## 整合一切

正如俗所说，剩下的就是历史了。GNU/Linux 从 i386 单 CPU 操作系统演变为支持许多处理器架构的多处理器操作系统。如今，GNU/Linux 已经存在于大型超级计算机和小型手持设备中。它运行在 x86 系列、ARM、PowerPC、日立 SuperH、68K 等许多架构上。随着其在嵌入式社区的持续采用，这对 GNU/Linux 来说是一个非常重要的特性。

近年来，GNU/Linux 成为虚拟化等新技术的先驱。在过去（1960 年代 IBM 主机时代），人们创建了称为虚拟机程序的特殊操作系统，作为其他系统的操作系统。今天，通过 Xen 和内核虚拟机（KVM）等项目，Linux 变成了虚拟机管理器。在第 4 章“Linux 虚拟化与仿真”中，我们将学习更多构建在 Linux 之上的虚拟化和仿真技术。

GNU/Linux 从其微的起点演变为目前可用扩展性最强、安全、可靠且性能最高的操作系统之一。与 Windows 相比，GNU/Linux 不容易被黑客利用 [NewsForge04]。当你考虑 Web 服务器时，开源的 Apache HTTP 服务器被破解的可能性远低于微软的 IIS [Wheeler04]。

## Linux 发行版

在早期，运行 GNU/Linux 系统并不简单。用户有时必须修改内核和驱动程序才能启动操作系统。今天，GNU/Linux 提供了一种简单的加载操作系统的方法。由于内核具有可加载模块的特性，动态和自动地配置操作系统并利用可用的外设变得非常简单。像 Debian 这样的项目以及 Red Hat 和 Suse 这样的公司，引入了包含了 GNU/Linux 操作系统和预编译程序的的发行版。大多数发行版包含超过 10,000 个软件包（应用程序），让你能够轻松获取所需的内容。如果你没有需要的内容，可以使用包管理系统（如 apt）轻松地更新你的软件。我们将在第 28 章探讨包管理器和系统管理。

## GNU/Linux 应用程序编程

## 总结

GNU/Linux 的历史在三个层面上都是有趣的，这是一个关于挫折的故事。Thompson 和 Ritchie 设计了原始 UNIX，是为了取代 Multics 操作系统。Richard Stallman 创建了 GNU 和 FSF，是为了创建一个任何人都可以使用的、无专利许可的操作系统。Linus Torvalds 出于挫折感通过 Minix 创建了 Linux。无论他们的动机是什么，他们以及世界上其他的人以当时人们无法想象的方式成功了。如今，GNU/Linux 与商业操作系统竞争并提供了一个真实且实用的选择。即使在嵌入式系统领域，Linux 也开始主导包括手机在内的各种设备。

## 参考文献

- [Byte94] "Unix at 25" http://www.byte.com/art/9410/sec/art3ms.html.
- [Debian04] Debian Linux http://www.debian.org.
- [Linux/GNU04] "Linux and the GNU Project" http://www.gnu.org/linux-and-gnu.html.
- [Minix04] Minix Operating System http://www.minix.3.
- [Montague03] "Why You Should Use a BSD-Style License," Bruce R. Montague, http://63.249.85/132/open_source_license.html.
- [NewsForge04] "Linux and Windows Compared," Stacey Quandt, http://os.newsforge.com/04/05/18/1715247.shtml.
- [RedHat04] Red Hat http://www.redhat.com 和 fedora.redhat.com.
- [RobotWisdom02] "Timeline of GNU/Linux and UNIX" http://www.robotwisdom.com/timeline.html.
- [Stallman83] "Initial GNU Announcement" http://www.gnu.org/gnu/initial-announcement.html.
- [Stallman02] "Free in Freedom," Richard Stallman, O'Reilly & Associates., 2002.
- [Suse04] Suse Linux http://www.suse.com.
