
启动 Linux ................................................................................61

玩 Shell .......................................................................................64

关机 ................................................................................68

# 第 1 章：介绍 Linux

本章内容

- 解释什么是 Linux
- 概述 Linux 发行版通常包含什么
- 发现 Linux 帮助你管理什么
- 开始使用 Linux

既然你手里拿着这本书，可以肯定你已经听过关于 Linux 的东西。如果你想知道它是否值得考虑，以及它能帮你做什么，那么这一章就是为你准备的。在这里，我提供了 Linux 的概况，并告诉你如何立即开始使用它。

![](img/49a40dc66bb14561782e2a1125eaccf3_34_0.png)

虽然 Linux 可以运行在许多平台上，但本书聚焦于适用于 Intel 8086 和 Pentium 处理器的 Linux（基本上是任何可以运行各种 Windows 的 PC）。

## 什么是 Linux?

PC 可以被视为硬件的组合——你可以触碰到的东西，机箱、显示器、键盘和鼠标。机箱包含了所有最重要的硬件——中央处理器（CPU），运行软件的微芯片（告诉计算机如何听你差遣的程序），你实际上无法触碰。在典型的基于 Pentium 的 PC 中，Pentium 微处理器就是 CPU。系统的其他重要硬件包括内存（RAM）和硬盘。

操作系统是运行软件（任何告诉计算机如何听你差遣的程序）的程序，它管理所有硬件并让它们运行良好。你作为用户通过点击菜单或输入晦涩的文本来提供这些命令。Linux 是操作系统，UNIX、Windows XP 和 Windows Vista 也是。Linux 操作系统模仿了 UNIX；在最基础的形式下，Linux 操作系统被称为 Linux 内核。

# 10 什么是 Linux?

## Linux 真的可以在任何计算机上运行吗？

Linux 运行在许多不同的计算机系统中——由于发行版非常多，它似乎可以在几乎任何类型的计算机上运行。Lin Torvalds 和程序员为 Intel x86（及兼容）处理器线开发了 Linux。本书涵盖 8086 和 Pentium 处理器。（这些被称为 IA32 处理器或 i386。）现在 Linux 也适用于基于其他处理器的系统——例如

- AMD 的 64 位 AMD64 处理器
- Motorola 68000 系列
- Alpha APs
- Sun SPARCs 和 UltraSPCs
- HP-RISC
- PowerPC 和 PowerPC64 处理器
- MIPS R4x0 和 R5x0。

IBM 为其 S390 和 z 系列大型机发布了自己的 Linux 版本。

# 什么是 Linux？

在技术术语中，Linux 是一个多用户、多任务的操作系统。这仅意味着 Linux 允许多个用户登录，并且每个用户都可以同时运行多个一个程序。在如今，几乎所有的操作系统都是多用户和多任务的，但 Linux 最初诞生于 1994 年时，多用户和多任务是非常重大的卖点。

第一卷

第一章

## Linux 发行版

一个 Linux 发行版由 Linux 内核（操作系统）和一组应用程序，以及一个易于使用的安装程序组成。

大多数人所说的 Linux是指某个特定的 Linux 发行版。

你会发现许多 Linux 发行版，每个版本包含标准的 Linux 操作系统以及以下软件包：

- `X Window 系统`：它是图形用户界面。
- 一个或多个图形化桌面：最流行的是 GNOME 和 KDE。
- 一系列应用程序：Linux 程序以即插可用软件的形式提供，但源代码（人类用来告诉计算机做什么的命令）也作为文档包含在内（或可供获取）。

目前的 Linux 发行版包含了大量的软件选择——因此某些发行版通常需要多张 CD-ROM 或单张 DVD-ROM（已包含在内）。

Linux 内核的开发与维护、Linux 发行版中的软件包以及 Linux 发行版本身是以开源项目的形式组织的。简而言之，开源意味着可以访问源代码并拥有在不受任何限制的情况下自由分发软件的权利。其定义比这段简短说明要丰富得多。要了解开源含义的细节以及可接受的开源许可，您可以访问开源倡议网站 www.opensource.org。

表 1-1 列出了几个 Linux 发行版以及各自的简要描述。除了表 1-1 所示的之外，还有许多 Linux 发行版。

要了解更多关于 Linux 发行版的信息，请访问 http://distrowatch.com 的 DistroWatch.com。在该网站上，你可以阅读特定发行版的介绍，并找到特定发行版 CD 或 DVD 的链接。

介绍 Linux

# 12 什么是 Linux？

| 发行版 | 描述 |
| :--- | :--- |
| Debian GNU/Linux | 这一非商业发行版始于 1992 年，一直是一个受欢迎的发行版，全球有很多志愿者开发者为该项目做出贡献。Debian 是一个巨大的发行版，安装需要花费一些时间。安装完基础系统后，你可以使用名为 `apt-get` 的软件包轻松安装和升级 Debian 软件包，其中 `apt` 代表高级软件包工具。Debian 可以在 where.debian.org 免费获取。Debian 是其他几个近期发行版（包括 Ubuntu 和 CentOS）的基础。 |
| Fedora | 这一发行版曾被称为 Fedora Core，是 Red Linux（来自 Red Hat 的发行版）的继者。Fedora Core 1 于 2003 年 11 月发布，是 Red Hat 9 的继者，Fedora 8 于 2007 年底发布。Fedora 免费提供，其软件包使用 Red Hat 软件包管理器 (`RPM`) 格式。你可以从 http://project.org 下载 Fedora。 |
| Gentoo Linux | 这是一个非商业的、基于源码（所有软件均以源代码形式提供）的发行版，于 2002 年出现。安装程序为 Gentoo Linux 许多二进制文件，但其理念是在用户的计算机上编译所有源码包。构建一个带有最新图形化桌面和开发工具的完整 Gentoo 系统非常耗时，需要下载并编译所有软件包。Gentoo Linux 可以在 www.gentoo.org 免费获取。 |
| Knoppix | 这种基于 Debian 的 Live CD 发行版以其创始人德国人 Klaus Knoppix 命名。Knoppix 可以作为恢复工具来修复已安装的 Linux 系统问题，因为你可以直接从 CD 运行 Knoppix，而无需安装到硬盘上（尽管其他发行版也可以这样做）。Knoppix 可以在 www.gentoo.org 免费获取（注：此处原文逻辑似乎有误，此处按字面翻译）。Knoppix 可以在 CD 免费获取。访问 knopper.net/knoppix/index.html。Knoppix 使用 Debian 格式。 |
| Linspace | 这种 Live CD 发行版基于 Debian，并以德国 Klaus Knoppix 命名。Knoppix 可以作为恢复工具...（此处重复且逻辑混乱）。要了解更多关于 Linspace 的信息，请访问 lin.com。 |
| 发行版 | 描述 | 第一卷 |
| :--- | :--- |
| Debian GNU/Linux | 这一非商业发行版始于 1992 年，一直是一个受欢迎的发行版，全球有很多志愿者开发者为该项目做出贡献。Debian 是一个巨大的发行版，安装需要花费一些时间。安装完基础系统后，你可以使用名为 `apt-get` 的软件包轻松安装和升级 Debian 软件包，其中 `apt` 代表高级软件包工具。Debian 可以在 where.debian.org 免费获取。Debian 是其他几个近期发行版（包括 Ubuntu 和 CentOS）的基础。 |
| Fedora | 这一发行版曾被称为 Fedora Core，是 Red Linux（来自 Red Hat 的发行版）的继者。Fedora Core 1 于 2003 年 11 月发布，是 Red Hat 9 的继者，Fedora 8 于 2007 年底发布。Fedora 免费提供，其软件包使用 Red Hat 软件包管理器 (`RPM`) 格式。你可以从 http://project.org 下载 Fedora。 |
