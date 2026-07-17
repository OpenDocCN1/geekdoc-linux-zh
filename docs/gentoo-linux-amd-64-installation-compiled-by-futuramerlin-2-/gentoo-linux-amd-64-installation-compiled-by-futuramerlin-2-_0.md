# Gentoo Linux AMD 64 安装指南，Futuramerlin 编译于 2016 年 6 月 2 日



![](img/cover.jpg)

![cover](img/cover.jpg)![cover](img/cover_image.jpg)


| 手册：主页 - Gentoo Wiki |
| | |
| Gentoo Wiki |
| | |
| |
* * * *
| |
|  |

# 手册：主页

从 Gentoo Wiki 快速到：导航, 搜索其他语言：[加泰罗尼亚语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/ca "Manual: Pàgina principal (96% 翻译)") • ‎[捷克语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/cs "Příručka:Hlavní stránka (79% 翻译)") • ‎[德语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/de "Handbuch:Hauptseite (100% 翻译)")英语 • ‎[西班牙语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/es "Manual de Gentoo: Página Principal (100% 翻译)") • ‎[法语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/fr "Manuel:Page Principale (67% 翻译)") • ‎[克罗亚亚语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/hr "Priručnik:Početak (100% 翻译)") • ‎[印尼语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/id "Buku Petunjuk:Laman Utama (100% 翻译)") • ‎[意大利语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/it "Manuale: Pagina Principale (100% 翻译)") • ‎[日语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/ja "ハンドブック:メインページ (100% 翻译)") • ‎[韩语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/ko "Handbook:Main Page/ko (100% 翻译)") • ‎[荷兰语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/nl "Handboek:Hoofdpagina (46% 翻译)") • ‎[巴西葡萄语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/pt-br "Manual:Página Principal (100% 翻译)") • ‎[俄语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/ru "Handbook:Главная Страница (100% 翻译)") • ‎[土耳其语](https://wiki.gentoo.org/wiki/Handbook:Main_Page/tr "Rehber:Ana Sayfa (100% 翻译)")[中文（大陆）](https://wiki.gentoo.org/wiki/Handbook:Main_Page/zh-cn "手册")[快速链接：](https://wiki.gentoo.org/wiki/Handbook:Alpha "Alpha") [AMD64](https://wiki.gentoo.org/wiki/Handbook:AMD64 "AMD64") [HPPA](https://wiki.gentoo.org/wiki/Handbook:HPPA "HPPA") [IA64](https://wiki.gentoo.org/wiki/Handbook:IA64 "IA64") [MIPS](https://wiki.gentoo.org/wiki/Handbook:MIPS "MIPS") [PPC](https://wiki.gentoo.org/wiki/Handbook:PPC "PPC") [PPC64](https://wiki.gentoo.org/wiki/Handbook:PPC64 "PPC64") [SPARC](https://wiki.gentoo.org/wiki/Handbook:SPARC "SPARC") [x86](https://wiki.gentoo.org/wiki/Handbook:x86 "x86") [x86_64](https://wiki.gentoo.org/wiki/Handbook:x86_64 "x86_64")


## 1 Gentoo 手册计划

### 简介
Gentoo 手册是将文档集中到一个连贯手册中的一项工作。该手册包含了基于网络的安装说明，以及关于使用 Gentoo 和 Portage 的部分。

### 架构
Gentoo Linux 适用于许多架构。但到底什么是架构？

*架构*是指支持相同指令的 CPU（处理器）家族。在桌面世界最著名的两种架构是 `x86` 和 x86_64（后者使用 `amd64` 命名）。但还有许多其他架构，例如 `sparc`、`ppc`（PowerPC 家族）、`mips`、`arm`...

## 2 查看手册

注意
下表提供了支持架构的高级概览。CPU 或系统示例仅仅是一个示例。如果你仍然不确定选择哪种架构，请阅读 Gentoo 手册第二章的第一节（选择安装介质），该部分将详细说明支持的平台。

ARM 和 ARM64 受 Gentoo 项目支持，但尚还没有完整的手册。更多信息请参阅 [ARM 项目](https://wiki.gentoo.org/wiki/Project:ARM)。

| 每个章节一页（许多短页面） | 每个部分一页（较长页面） |
| | |
| 架构手册 | 架构描述 | 安装 Gentoo Linux | 使用 Gentoo | 使用 Portage | 网络配置 |





## Alpha
| [Alpha](https://wiki.gentoo.org/wiki/Handbook:Alpha "Handbook:Alpha") | Alpha 架构是由数字设备公司 (DEC) 开发的一种 64 位架构。它目前仍被一些中端和高端服务器使用，但该架构正在逐渐淡淘汰。(ES40, AlphaPC, UP1000, Noname) | [安装](https://wiki.gentoo.org/wiki/Handbook:Alpha/Full/Installation "Handbook:Alpha/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:Alpha/Full/Working "Handbook:Alpha/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:Alpha/Full/Portage "Handbook:Alpha/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:Alpha/Full/Networking "Handbook:Alpha/Full/Networking") |

## AMD64
| [AMD64](https://wiki.gentoo.org/wiki/Handbook:AMD64 "Handbook:AMD64") | 一种与 x86 架构兼容的 64 位架构（因此也称为 x86_64）。它首次由 AMD（以 AMD64 名称）和 Intel（以 EM64T 名称）使用，现在是中高端桌面电脑最主流的架构。它也常见于服务器领域。(AMD Athlon 64, AMD Opteron, AMD Sempron 处理器, AMD Phenom, Intel Pentium 4, Intel Core2, Intel Core i3, i5, i7, 某些 Intel Atom 变体) | [安装](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation "Handbook:AMD64/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Working "Handbook:AMD64/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Portage "Handbook:AMD64/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Networking "Handbook:AMD64/Full/Networking") |

## ARM
| ARM | 这种 32 位架构是嵌入式和小型系统非常流行的架构。子架构范围从 ARMv1 到 ARMv7 (Cortex)，通常常见于智能手机、平板电脑、手持游戏机、终端用户 GPS 导航系统等。(StrongARM, Cortex-M) | | | | | |

## ARM64
| ARM64 | 这种 64 位架构是用于嵌入式和服务器系统的 ARM 新变体。唯一的子架构是 ARMv8，包含了 Cortex-A53 和 Cortex-A57 处理器，这些处理器开始出现在开发板、智能手机、平板电脑等各种 SoC 中。(Cortex-A53, Cortex-A57) | | | | | | |

## HPPA
| [HPPA](https://wiki.gentoo.org/wiki/Handbook:HPPA "Handbook:HPPA") | HPPA（称为 PA-RISC 架构）是惠普开发的一种指令集，直到 2008 年左右一直被用于其中高端服务器系列（之后 HP 开始使用 Intel Itanium）。(HP 9000, PA-8600) | [安装](https://wiki.gentoo.org/wiki/Handbook:HPPA/Full/Installation "Handbook:HPPA/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:HPPA/Full/Working "Handbook:HPPA/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:HPPA/Full/Portage "Handbook:HPPA/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:HPPA/Full/Networking "Handbook:HPPA/Full/Networking") |

## IA64
| [IA64](https://wiki.gentoo.org/wiki/Handbook:IA64 "Handbook:IA64") | Intel 设计的 64 位架构，用于其 Intel Itanium 处理器系列。该架构不兼容 x86 或 x86_64（即 amd64），主要用于中高端服务器系列。(Intel Itanium) | [安装](https://wiki.gentoo.org/wiki/Handbook:IA64/Full/Installation "Handbook:IA64/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:IA64/Full/Working "Handbook:IA64/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:IA64/Full/Portage "Handbook:IA64/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:IA64/Full/Networking "Handbook:IA64/Full/Networking") |

## MIPS
| [MIPS](https://wiki.gentoo.org/wiki/Handbook:MIPS "Handbook:MIPS") | 由 MIPS Technologies 开发，MIPS 架构包含多个子家族（称为版本），如 MIPS I、MIPS III、MIPS32、MIPS64 等。MIPS 在嵌入式系统中中最常见。(MIPS32 1074K, R16000) | [安装](https://wiki.gentoo.org/wiki/Handbook:MIPS/Full/Installation "Handbook:MIPS/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:MIPS/Full/Working "Handbook:MIPS/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:MIPS/Full/Portage "Handbook:MIPS/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:MIPS/Full/Networking "Handbook:MIPS/Full/Networking") |

## PPC
| [PPC](https://wiki.gentoo.org/wiki/Handbook:PPC "Handbook:PPC") | 许多 Apple、IBM 和摩托罗拉处理器使用的 32 位架构。它们最常见于嵌入式系统。(Apple OldWorld, Apple NewWorld, generic Pegasos, Efika, 较的 IBM iSeries 和 pSeries) | [安装](https://wiki.gentoo.org/wiki/Handbook:PPC/Full/Installation "Handbook:PPC/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:PPC/Full/Working "Handbook:PPC/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:PPC/Full/Portage "Handbook:PPC/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:PPC/Full/Networking "Handbook:PPC/Full/Networking") |

## PPC64
| [PPC64](https://wiki.gentoo.org/wiki/Handbook:PPC64 "Handbook:PPC64") | PPC 架构的 64 位变体，在嵌入式和高端服务器中流行。(IBM iSeries) | [安装](https://wiki.gentoo.org/wiki/Handbook:PPC64/Full/Installation "Handbook:PPC64/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:PPC64/Full/Working "Handbook:PPC64/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:PPC64/Full/Portage "Handbook:PPC64/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:PPC64/Full/Networking "Handbook:PPC64/Full/Networking") |

## SPARC
| [SPARC](https://wiki.gentoo.org/wiki/Handbook:SPARC "Handbook:SPARC") | SPARC 架构以其最常见的厂商 Sun（现 Oracle）和富士通闻名。它被用于服务器系统，尽管也有工作站。在 Gentoo 中仅支持 SPARC64。(E3000, Blade 1000) | [安装](https://wiki.gentoo.org/wiki/Handbook:SPARC/Full/Installation "Handbook:SPARC/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:SPARC/Full/Working "Handbook:SPARC/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:SPARC/Full/Portage "Handbook:SPARC/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:SPARC/Full/Networking "Handbook:SPARC/Full/Networking") |

## X86
| [X86](https://wiki.gentoo.org/wiki/Handbook:X86 "Handbook:X86") | 一种常被称为“Intel 兼容”的 CPU 的 32 位架构。直到最近，它是桌面电脑最流行的架构。Gentoo 为 i486（支持所有家族）和 i686（支持 Pentium 及以上）提供构建。(i486, i686, AMD Athlon, Intel Core, Intel Atom) | [安装](https://wiki.gentoo.org/wiki/Handbook:X86/Full/Installation "Handbook:X86/Full/Installation") | [工作](https://wiki.gentoo.org/wiki/Handbook:X86/Full/Working "Handbook:X86/Full/Working") | [Portage](https://wiki.gentoo.org/wiki/Handbook:X86/Full/Portage "Handbook:X86/Full/Portage") | [网络](https://wiki.gentoo.org/wiki/Handbook:X86/Full/Networking "Handbook:X86/Full/Networking") |

### 常见问题

### 你们不能为每个选择魔法地创建手册吗？

一切都是可能的，但我们选择仅在架构层面这样做。其他选择（如分区、内核选择、工具安装等）易于在单个文档中解释。

### 在 Gentoo 手册中找不到 stage1 信息

关于使用 stage1 或 stage2 tarball 的说明现在可以在 [Gentoo FAQ](https://wiki.gentoo.org/wiki/FAQ#How_do_I_install_Gentoo_using_a_stage1_or_stage2_tarball.3F "FAQ") 中找到。目前 stage3 安装是唯一支持的安装方式。

### 我不同意 ...





请通过相应手册页的 `Discussion pages`（讨论页）提交您的想法。文档是为社区制作的，因此非常欢迎社区的反馈。

然而，您必须知道，开发文档时做出的多数决策是基于共识模型的。无法以一种让所有人都满意的写法来编写或结构化文档。您必须接受一个“不”，理由是我们认为当前的实现对大多数人有利。

为了妥善地[跟踪开放问题](https://wiki.gentoo.org/index.php?title=Special%3AWhatLinksHere&target=Template%3AInfoBox+talk+open&namespace=561)，我们要求在提问时添加以下标记：

CODE `Example open discussion`

```
 {{InfoBox stack
|{{InfoBox talk open|date=Jul 2 2015}}
}}
```

这允许我们[跟踪] Gentoo 手册中的问题](https://wiki.gentoo.org/index.php?title=Special%3AWhatLinksHere&target=Template%3AInfoBox+talk+open&namespace=561)。

![cover](img/cover_image.jpg)


# 手册:AMD64

# 手册:AMD64

从 Gentoo Wiki 跳转到：导航, 搜索 其他语言：[捷克语](https://wiki.gentoo.org/wiki/Handbook:AMD64/cs "Příručka:AMD64 (100% translated)") • [德语](https://wiki.gentoo.org/wiki/Handbook:AMD64/de "Gentoo Linux AMD64 Handbuch (100% translated)") • 英语 • [西班牙语](https://wiki.gentoo.org/wiki/Handbook:AMD64/es "Manual de Gentoo: AMD64 (100% translated)") • [法语](https://wiki.gentoo.org/wiki/Handbook:AMD64/fr "Le manuel de Gentoo pour l'architecture AMD64 (100% translated)") • [意大利语](https://wiki.gentoo.org/wiki/Handbook:AMD64/it "Manuale: AMD64 (100% translated)") • [日本語](https://wiki.gentoo.org/wiki/Handbook:AMD64/ja "ハンドブック:AMD64 (100% translated)") • [한국어](https://wiki.gentoo.org/wiki/Handbook:AMD64/ko "Handbook:AMD64/ko (100% translated)") • [荷兰语](https://wiki.gentoo.org/wiki/Handbook:AMD64/nl "Handboek:AMD64 (100% translated)") • [巴西葡萄牙语](https://wiki.gentoo.org/wiki/Handbook:AMD64/pt-br "Manual:AMD64 (100% translated)") • [俄语](https://wiki.gentoo.org/wiki/Handbook:AMD64/ru "Handbook:AMD64 (100% translated)") • [土耳其语](https://wiki.gentoo.org/wiki/Handbook:AMD64/tr "Gentoo Linux AMD64 Rehberi (100% translated)") • [中文（中国大陆）‎](https://wiki.gentoo.org/wiki/Handbook:AMD64/zh-cn "手册：AMD64 (100% translated)")

### 安装

* [关于安装](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/About "Handbook:AMD64/Installation/About")
* [选择介质](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Media "Handbook:AMD64/Installation/Media")
* [配置网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Networking "Handbook:AMD64/Installation/Networking")
* [准备磁盘](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Disks "Handbook:AMD64/Installation/Disks")
* [准备阶段](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Stage "Handbook:AMD64/Installation/Stage")
* [基础基础](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Base "Handbook:AMD64/Installation/Base")
* [配置内核](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Kernel "Handbook:AMD64/Installation/Kernel")
* [配置系统](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/System "Handbook:AMD64/Installation/System")
* [安装工具](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Tools "Handbook:AMD64/Installation/Tools")
* [配置引导程序](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Bootloader "Handbook:AMD64/Installation/Bootloader")
* [完成安装](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Finalizing "Handbook:AMD64/Installation/Finalizing")

## 使用 Gentoo

* [Gentoo 简介](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working "Handbook:AMD64/Working")
* [USE 标记](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")
* [Portage 特性](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Features "Handbook:AMD64/Working/Features")
* [初始化脚本](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Initscripts "Handbook:AMD64/Working/Initscripts")
* [环境变量](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/EnvVar "Handbook:AMD64/Working/EnvVar")

## 使用 Portage

* [文件](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Files "Handbook:AMD64/Working/Files")
* [变量](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Variables "Handbook:AMD64/Working/Variables")
* [分支](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Branches "Handbook:AMD64/Working/Branches")
* [工具](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Tools "Handbook:AMD64/Working/Tools")
* [自定义树结构](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/CustomTree "Handbook:AMD64/Working/CustomTree")
* [高级功能](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Advanced "Handbook:AMD64/Working/Advanced")

### 网络配置

* [入门](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Introduction "Handbook:AMD64/Networking/Introduction")
* [高级配置](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Advanced "Handbook:AMD64/Networking/Advanced")
* [模块化网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Modular "Handbook:AMD64/Networking/Modular")
* [无线网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Wireless "Handbook:AMD64/Networking/Wireless")
* [添加功能](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Extending "Handbook:AMD64/Networking/Extending")
* [动态管理](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Dynamic "Handbook:AMD64/Networking/Dynamic")

这是 Gentoo 手册，旨在集中 Gentoo/Linux 的信息。本手册包含了基于互联网的安装说明以及关于如何使用 Gentoo 和 Portage 的部分。


## 安装 Gentoo

在此部分，读者将学习如何在系统上安装 Gentoo。

[关于 Gentoo Linux 安装](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/About "Handbook:AMD64/Installation/About")

本章介绍了本手册中记录的安装方法。





# [选择合适的安装介](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Media "Handbook:AMD64/Installation/Media")

可以通过多种方式安装 Gentoo。本章将解释如何使用最小化安装光盘来安装 Gentoo。

## [配置网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Networking "Handbook:AMD64/Installation/Networking")

为了能够下载最新的源代码，需要配置网络。

## [准备磁盘](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Disks "Handbook:AMD64/Installation/Disks")

为了能够安装 Gentoo，需要创建必要的分区。本章描述了如何对磁盘进行分区供以后使用。

## [安装 Gentoo 文件](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Stage "Handbook:AMD64/Installation/Stage")

Gentoo 的安装通过 `stage3` 归包完成。在本章中，我们将描述如何解压 `stage3` 归包并配置 `Portage`。

## [安装 Gentoo 基础系统](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Base "Handbook:AMD64/Installation/Base")

在安装并配置 `stage3` 之后，将设置基础系统以提供最小环境。

## [配置 Linux 内核](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Kernel "Handbook:AMD64/Installation/Kernel")

Linux `kernel` 是每个发行版的核心。本章解释了如何配置内核。

## [配置系统](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/System "Handbook:AMD64/Installation/System")

需要编辑一些重要的配置文件。本章提供了这些文件的概述，并解释了如何进行后续操作。

## [安装系统工具](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Tools "Handbook:AMD64/Installation/Tools")

在本章中，选择并安装了一些重要的工具。

## [配置引导程序](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Bootloader "Handbook:AMD64/Installation/Bootloader")

在本章中，安装并配置了正确的引导程序。

## [完成安装](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Finalizing "Handbook:AMD64/Installation/Finalizing")

安装现在几乎完成。最后的收尾工作将在本章中记录。

## 使用 Gentoo

### [Portage 简介](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Portage "Handbook:AMD64/Working/Portage")

本章解释了用户为了维护系统软件绝对需要知道的“简单”步骤。

### [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")

`USE` 标志是 Gentoo 一个非常重要的方面。在本章中，读者将学习如何使用 `USE` 标志，并理解 `USE` 标志如何与系统交互。

### [Portage 特性](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Features "Handbook:AMD64/Working/Features")

发现 `Portage` 拥有的特性，例如支持分布式编译、`ccache` 等等。

### [Init 脚本系统](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Initscripts "Handbook:AMD64/Working/Initscripts")

Gentoo 使用一种特殊的 `initscript` 格式，该格式等特性允许依赖驱动决策和虚拟 initscripts。本章解释了所有这些方面，并解释了如何处理这些脚本。

### [环境变量](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/EnvVar "Handbook:AMD64/Working/EnvVar")

在 Gentoo 中可以轻松地管理环境变量。本章解释了如何这样做，并描述了经常使用的变量。

## 使用 Portage

### [文件和目录](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Files "Handbook:AMD64/Portage/Files")

为了深入了解 `Portage`，首先学习它将文件和数据存储在哪里。

### [变量](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Variables "Handbook:AMD64/Portage/Variables")

`Portage` 可以通过各种变量完全配置，这些变量可以在配置文件中设置或作为环境变量。

### [混合软件分支](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Branches "Handbook:AMD64/Portage/Branches")

Gentoo 根据稳定性和架构支持将软件划分为几个分支。“混合软件分支”解释了如何配置这些分支，以及如何单独地覆盖这种分离状态。

### [额外工具](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Tools "Handbook:AMD64/Portage/Tools")

`Portage` 带有了一些额外的工具，它们可能会让 Gentoo 体验更好。继续阅读以发现如何使用 `dispatch-conf` 和工具。

### [自定义 Portage 树](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/CustomTree "Handbook:AMD64/Portage/CustomTree")

本章提供了一些关于如何使用自定义 `Portage` 树、如何仅同步必要的类别、注入包等方面的提示和技巧。

### [高级功能](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Advanced "Handbook:AMD64/Portage/Advanced")

随着时间的推移，`Portage` 不断演进和成熟。额外的功能被不断加入——其中许多对高级用户有用。本章将详细介绍这些特定功能。

## Gentoo 网络配置

### [入门](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Introduction "Handbook:AMD64/Networking/Introduction")

在大多数常见环境中快速启动网络接口运行的指南。

### [高级配置](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Advanced "Handbook:AMD64/Networking/Advanced")

在这里我们学习配置是如何工作的——这是在继续模块化网络之前的先验知识。

### [模块化网络](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Modular "Handbook:AMD64/Networking/Modular")

学习如何选择不同的 `DHCP` 客户端，设置 `bonding`、`bridging`、`VLANs` 等。

### [无线](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Wireless "Handbook:AMD64/Networking/Wireless")

为无线网络配置 Gentoo。

### [添加功能](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Extending "Handbook:AMD64/Networking/Extending")

冒险的用户可以为网络工具添加自己的功能。

### [动态管理](https://wiki.gentoo.org/wiki/Handbook:AMD64/Networking/Dynamic "Handbook:AMD64/Networking/Dynamic")

适用于笔记本电脑用户或在不同网络间移动电脑的人。





# 手册：AMD64/完整

来自 Gentoo Wiki [手册:AMD64](https://wiki.gentoo.org/wiki/Special:MyLanguage/Handbook:AMD64 "Special:MyLanguage/Handbook:AMD64") 跳转到：导航, 搜索 其他语言：[德语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/de "Handbuch:AMD64/Komplett (100% translated)") • 英语 • [西班牙语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/es "Handbook:AMD64/Full/es (100% translated)") • [日语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ja "ハンドブック:AMD64/フル (100% translated)") • [韩语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ko "Handbook:AMD64/Full/ko (100% translated)") • [俄语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ru "Handbook:AMD64/Full (100% translated)") • [中文（中国大陆）‎](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/zh-cn "手册：AMD64/完整 (100% translated)")

根据请求，我们也为 Gentoo 手册的每个部分提供单个页面版本，以便于打印。

然而，这将导致手册中使用的链接无法正常工作 - 它们将不会指向“完整页面”中的后续章节，而是指向独立的页面。

此外，由于 wiki 本身的限制，无法实现整个手册的单页完整视图。

*   [安装 Gentoo Linux](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation "Handbook:AMD64/Full/Installation")
*   [使用 Gentoo](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Working "Handbook:AMD64/Full/Working")
*   [使用 Portage](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Portage "Handbook:AMD64/Full/Portage")
*   [网络配置](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Networking "Handbook:AMD64/Full/Networking")

检索自 "[`wiki.gentoo.org/index.php?title=Handbook:AMD64/Full&oldid=181102`](http://wiki.gentoo.org/index.php?title=Handbook:AMD64/Full&oldid=181102)"![cover](img/cover_image.jpg)

*   1.1 准备工作
*   2 高级安装
*   2.1 软件 RAID
*   2.2 使用 2.4 内核的 ATA RAID
*   2.3 使用安装 CD 内核
*   3 简化安装过程
*   3.1 离开你的终端
*   4 修复错误/问题
*   4.1 对你的磁盘进行广泛测试
*   4.2 从故障的安装中恢复

Gentoo 安装技巧与技巧

来自 Gentoo Wiki [手册:AMD64](https://wiki.gentoo.org/wiki/Special:MyLanguage/Handbook:AMD64 "Special:MyLanguage/Handbook:AMD64") 跳转到：导航, 搜索 其他语言：[德语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/de "Handbuch:AMD64/Komplett (100% translated)") • 英语 • [西班牙语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/es "Handbook:AMD64/Full/es (100% translated)") • [日语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ja "ハンドブック:AMD64/フル (100% translated)") • [韩语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ko "Handbook:AMD64/Full/ko (100% translated)") • [俄语](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/ru "Handbook:AMD64/Full (100% translated)") • [中文（中国大陆）‎](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/zh-cn "手册：AMD64/完整 (100% translated)")

根据请求，我们也为 Gentoo 手册的每个部分提供单个页面版本，以便于打印。

然而，这将导致手册中使用的链接无法正常工作 - 它们将不会指向“完整页面”中的后续章节，而是指向独立的页面。

此外，由于 wiki 本身的限制，无法实现整个手册的单页完整视图。

*   [安装 Gentoo Linux](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation "Handbook:AMD64/Full/Installation")
*   [使用 Gentoo](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Working "Handbook:AMD64/Full/Working")
*   [使用 Portage](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Portage "Handbook:AMD64/Full/Portage")
*   [网络配置](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Networking "Handbook:AMD64/Full/Networking")

检索自 "[`wiki.gentoo.org/index.php?title=Handbook:AMD64/Full&oldid=181102`](http://wiki.gentoo.org/index.php?title=Handbook:AMD64/Full&oldid=181102)"![cover](img/cover_image.jpg)

## 目录

*   Gentoo 安装技巧与技巧
*   gentoo.org 站点
*   导航
*   搜索
*   1 简介
*   1.1 准备工作
*   2 高级安装
*   2.1 软件 RAID
*   2.2 使用 2.4 内核的 ATA RAID
*   2.3 使用安装 CD 内核
*   3 简化安装过程
*   3.1 离开你的终端
*   4 修复错误/问题
*   4.1 对你的磁盘进行广泛测试
*   4.2 从故障的安装中恢复

Gentoo 安装技巧与技巧

Gentoo 安装提供了非常灵活的安装方法。大部分内容以简练的方式讨论 - 它们旨在安装说明的补充，而不是替代。

### 准备工作

软件 RAID

**注意**

如果你不熟悉软件 RAID，请阅读 [Software-RAID-HOWTO](https://raid.wiki.kernel.org/index.php/Linux_Raid)。**注意**

更详细的过程可以参考我们的 [软件 RAID 和 LVM2 x86 快速安装指南](https://gentoo-handbook.lugons.org/doc/en/gentoo-x86+raid+lvm2-quickinstall.xml)。

从安装 CD 启动后，加载相应的 RAID 模块。例如，如果你计划使用 RAID-1：

```
root # modprobe raid1
```





当你划分磁盘时，请确保你的分区使用 `fd`（Linux raid 自动检测）作为分区类型，而不是 `83`（Linux 原生）。你可以使用 `fdisk` 中的 `t` 命令来更改分区类型。

现在，在我们开始创建 RAID 阵列之前，我们需要创建元设备节点：

```bash
root # mknod /dev/md1 b 9 1
root # mknod /dev/md2 b 9 2
root # mknod /dev/md3 b 9 3
```

分区完成后，使用 `mdadm`（一个用于[RAID 管理](http://www.linuxdevcenter.com/pub/a/linux/2002/12/05/RAID.html)的高级工具）在安装光环境中创建 `/etc/mdadm.conf` 文件。例如，为了让启动分区、交换分区和根分区镜像（RAID-1）并覆盖 `/dev/sda` 和 `/dev/sdb`，你可以使用：

```bash
root # mdadm --create --verbose /dev/md1 --level=1 --raid-devices=2 --metadata=0.90 /dev/sda1 /dev/sdb1
root # mdadm --create --verbose /dev/md2 --level=1 --raid-devices=2 --metadata=0.90 /dev/sda2 /dev/sdb2
root # mdadm --create --verbose /dev/md3 --level=1 --raid-devices=2 --metadata=0.90 /dev/sda3 /dev/sdb3
```

### 简化安装过程

### 离开终端

许多人希望在系统编译时离开。在某些情况下，这相当困难，因为安装是在公共环境中进行的，你无法信任每个人。如果是此类情况，你希望能够在后台执行编译并退出所有终端。

有几种可能的解决方案。第一种是使用 `screen`。启动安装光盘后，设置你的 root 密码并启动 screen 会话：**注意**

并不是所有的安装光盘都提供 `screen`。如果是这样，你将使用本节描述的其他方法之一。

```bash
root # screen -S gentoo
```

进入 screen 会话后，你可以完成整个安装过程。当你想要离开终端时，按下 `Ctrl` + `a`, `d`（即同时按下 `Ctrl` 和 `a`，然后按 `d`）来分离（detach）你的 screen 会话。现在你可以安全地退出系统了。

要重新访问终端，再次以 root 身份登录并连接（attach）到运行中的 screen 会话：

```bash
root # screen -x gentoo
```

如果你无法使用 `screen`，仍然有一种离开终端的方法。遵循安装说明，但当你到达开始长时间编译的步骤（例如 `./scripts/bootstrap.sh` 步骤）时，使用 `nohup`，它允许进程在你退出时继续运行。不要忘记末尾的 `&`，否则进程将不会放在后台运行！记住你所在的位置（使用 `pwd` 命令可以显示），因为你之后需要知道它。

```bash
root # pwd
/usr/portage
root # nohup ./scripts/bootstrap.sh &
```

现在退出 chroot 环境（`exit`）和安装光盘会话。你的编译将在后台继续。

当你想要检查编译情况时，以 root 身份登录（在安装光盘上）并 chroot 回你的环境，进入你离开时的目录：

```bash
root # chroot /mnt/gentoo /bin/bash
root # env-update && source /etc/profile
root # cd /usr/portage
```

现在对该目录下的 `nohup.out` 文件使用 `less` 命令。编译会将输出追加到该文件中，因此如果你想跟踪编译进度，运行 `less nohup.out` 并按下 `F` 来跟踪变化。编译完成后，你可以继续执行安装说明的下一步。

如果你厌倦了跟踪变化，按下 `Ctrl` + `C` 紧接着按 `q`。这不会停止编译进程，只会停止 `less` 进程。

## 修复错误/问题

### 对磁盘进行广泛测试

如果你认为你的磁盘需要对一致性进行彻底检查（坏道等），你可以在在该磁盘上放置 ext2 或 ext3 文件系统时（使用 `mke2fs`）使用 `-c`（小写字母 `c`）选项。这将格式化磁盘、执行读取测试并将所有坏块标记为坏块。如果你非常多疑，可以使用 `-c -c` 格式化磁盘并进行广泛的读写测试。

```bash
root # mke2fs -j -c /dev/sda3
```

### 从故障安装中恢复

如果由于某些原因你的 Gentoo 安装失败了，你不需要重新开始安装。相反，你可以安全地“回到”你认为犯错的地方（或者你认为说明有缺陷的地方），并尝试不同的方法。

首先，你需要 chroot 回你的 Gentoo Linux 环境。再次遵循说明，但忽略分区步骤，因为你的分区已经创建并填充了数据。因此，你可以直接将这些分区挂载到 `/mnt/gentoo`。你还应该忽略关于 stage 提取（stage extraction）的步骤。




Gentoo 是 Gentoo Foundation, Inc. 的商标。除非另有明确说明，本文档内容采用 [CC-BY-SA-3.0](https://creativecommons.org/licenses/by-sa/3.0/) 许可协议。适用 [Gentoo 名称和标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html)。![cover](img/cover_image.jpg)

* 帮助
* Gentoo
* Gentoo 项目
* 文档
* Gentoo 手册
* Gentoo 常见问题
* 特色文档
* 核心系统
* 硬件
* 软件
* 桌面
* 服务器与安全
* 项目与社区
* 链入此
* 相关更改
* 特殊页面
* 可打印版本
* 浏览属性
* 手册
* 讨论
* 手册:AMD64
* 完整版
* 导航
* 搜索

* 1 引言
* 1.1 欢迎
* 1.2 安装结构是怎样的
* 1.3 哪些选项
* 1.4 常见问题
* 2 硬件要求
* 3 Gentoo Linux 安装 CD
* 3.1 最小化安装 CD
* 3.2 偶尔使用的 Gentoo LiveDVD
* 3.3 那么什么是 stages（阶段）
* 4 下载并刻录 CD
* 4.1 下载媒体
* 4.2 验证下载的文件
* 4.2.1 基于 Microsoft Windows 的验证
* 4.2.2 基于 Linux 的验证
* 4.3 刻录
* 4.3.1 使用 Microsoft Windows 刻录
* 4.3.2 使用 Linux 刻录
* 5 引导 CD
* 5.1 引导 CD
* 5.2 偶尔使用的 Gentoo LiveDVD
* 5.3 那么什么是 stages（阶段）

## 1 引言

### 1.1 欢迎
### 1.2 安装结构是怎样的
### 1.3 哪些选项
### 1.4 常见问题

## 2 硬件要求

## 3 Gentoo Linux 安装 CD

### 3.1 最小化安装 CD
### 3.2 偶尔使用的 Gentoo LiveDVD
### 3.3 那么什么是 stages（阶段）

## 4 下载并刻录 CD

### 4.1 下载媒体
### 4.2 验证下载的文件
#### 4.2.1 基于 Microsoft Windows 的验证
### 4.2.2 基于 Linux 的验证
### 4.3 刻录
#### 4.3.1 使用 Microsoft Windows 刻录
### 4.3.2 使用 Linux 刻录

## 5 引导 CD

### 5.1 引导 CD
### 5.2 偶尔使用的 Gentoo LiveDVD
### 5.3 那么什么是 stages（阶段）





### 4.2 验证下载的文件
### 4.2.1 基于 Microsoft Windows 的验证
### 4.2.2 基于 Linux 的验证

### 4.3 刻录
### 4.3.1 使用 Microsoft Windows 刻录
### 4.3.2 使用 Linux 刻录

## 5 启动 CD
### 5.1 启动安装 CD
### 5.2 额外的硬件配置
### 5.3 可选：用户账户
### 5.4 可选：在安装时查看文档
### 5.5 可选：启动 SSH 守护进程

## 6 自动网络检测
### 6.1 确定接口名称
### 6.1.1 `ifconfig` 命令
### 6.1.2 `ip` 命令
### 6.2 可选：配置任何代理
### 6.3 测试网络

## 7 自动网络配置
### 7.1 默认：使用 net-setup
### 7.2 替代方案：使用 PPP
### 7.3 替代方案：使用 PPTP

## 8 手动网络配置
### 8.1 加载相应的网络
### 8.2 使用 `DHCP`
### 8.3 准备无线访问
### 8.4 理解术语
### 8.5 使用 `ifconfig` 和 `route`

## 9 块设备简介
### 9.1 块设备
### 9.2 分区表
### 9.4.2 `LVM2`
### 9.5 默认分区方案

## 10 设计分区方案
### 10.1 多少个以及大？
### 10.2 交换空间如何？
### 10.3 什么是 BIOS 启动分区？

## 11 默认：使用 `parted` 对磁盘进行分区
### 11.1 使用 `parted` 查看当前分区布局
### 11.2 设置 `GPT` 标签
### 11.3 使用 `parted` 删除所有分区
### 11.4 创建分区

## 12 替代方案：使用 `fdisk` 对磁盘进行分区
### 12.1 查看当前分区布局





### 12.2 使用 fdisk 删除所有分区
### 12.3 创建 BIOS 启动分区
### 12.4 创建启动分区
### 12.5 创建交换分区
### 12.6 创建根分区
### 12.7 保存分区布局

### 13 创建文件系统
#### 13.1 引言
#### 13.2 文件系统
#### 13.3 在分区上应用文件系统
#### 13.4 激活交换分区

### 14 挂载

### 15 安装 stage tarball
#### 15.1 设置日期时间
#### 15.2 选择 stage tarball
##### 15.2.1 Multilib (32 位和 64 位)
##### 15.2.2 No-multilib (纯 64 位)
#### 15.3 下载 stage tarball
#### 15.4 解压 stage tarball
### 16 配置选项
##### 17.1.1 发行版
##### 17.1.2 Gentoo 仓库
#### 17.2 复制
#### 17.3 挂载
#### 17.4 进入环境
### 18 配置
#### 18.1 安装 stage tarball
#### 18.2 更新树形树
#### 18.3 阅读新闻
#### 18.4 选择正确的配置
##### 18.4.1 No-multilib
##### 18.4.2 systemd
#### 18.5 更新 @world
#### 18.6 配置 USE 变量

### 19 可用：使用 systemd
### 20 时区
### 21 配置本地化
### 22 安装源码
### 23 默认：手动配置





# 24 替代方案：使用 `genkernel`

# 25 内核模块
### 25.1 配置模块
### 25.2 可选：安装固件

# 26 文件系统信息
### 26.1 关于 `fstab`
### 26.2 创建 `fstab` 文件

# 27 网络信息
### 27.1 主机和域名信息
### 27.2 配置网络
### 27.3 启动时自动启动网络
### 27.4 `hosts` 文件
### 27.5 可选：使 PCMCIA 正常

# 28 系统信息
### 28.1 Root 密码
# 31 可选：文件索引

# 32 可选：远程访问

# 33 文件系统工具

# 34 网络工具
### 34.1 安装 `DHCP` 客户端
### 34.2 可选：安装 `PPPoE` 客户端

# 35 选择启动加载程序

# 36 默认：使用 `GRUB2`
### 36.1 安装 `GRUB2`
### 36.2 配置 `GRUB2`

# 37 替代方案：使用 `LILO`
### 37.1 安装 `LILO`
### 37.2 配置 `LILO`

# 38 替代方案：使用 `efibootmgr`

# 39 重启系统

# 40 用户管理
### 40.1 添加日常使用的用户

# 41 磁盘清理
### 41.1 移除 tar 包

# 42 接下来去哪里
### 42.1 文档





| 10 | 新安装的 Gentoo Linux 环境已准备好可以开始探索。 |

每当出现某个选择时，手册都会尝试解释每个选择的优缺点。虽然正文随后会继续给出默认选择（在标题中以“Default: ” 标识），但也会记录其他可能性（在标题中以“Alternative: ” 标记）。不要认为默认选项就是 Gentoo 推荐的。然而，这通常是 Gentoo 认为大多数用户会使用的选项。

有时可以遵循一个可选步骤。这些步骤被标记为“Optional: ”，因此在安装 Gentoo 时并不是必需的。然而，某些可选步骤依赖于之前做出的决定。在发生这种情况时，指令会告知读者，包括在做出决定时以及在描述可选步骤的正文之前。

### 有哪些选项

有关其他安装方法（包括使用非 Gentoo 光盘）的帮助，请阅读我们的替代安装指南。

我们还提供了一份 Gentoo 安装提示与技巧 文档，阅读它可能也会。

### 故障排除

如果在安装过程中（或在安装文档中）发现问题，请访问我们的[错误跟踪系统](https://bugs.gentoo.org) 并检查该错误是否已知。如果不是，请为之创建一个错误报告，以便我们处理。不要害怕负责处理这些错误的开发人员——他们（通常）并不会吃人。

但请注意，尽管本文是针对特定架构的，但它也可能包含对其他架构的引用。这是由于 Gentoo 手册的大部分使用了适用于所有架构的通用源代码（以避免重复劳动和开发资源的枯竭）。我们将尝试将这种情况降到最低，以避免混淆。

如果不确定某个问题是用户问题（尽管已仔细阅读文档但仍犯了某些错误）还是软件问题（尽管我们仔细测试了安装/文档但仍犯了某些错误），欢迎加入 `irc.freenode.net` 上的 #gentoo。当然，我们也欢迎所有人，因为我们的聊天频道涵盖了 Gentoo 的方方面面。

说到这里，如果对 Gentoo 有任何额外问题，请查看常见问题解答 文章。[Gentoo 论坛](https://forums.gentoo.org/viewforum.php?f=40) 上也有 [FAQs]。

## 硬件要求

在开始之前，我们首先列出在 `amd64` 机器上成功安装 Gentoo 所需要的硬件要求。

| | 最小 CD | LiveDVD |
| :--- | :--- | :--- |
| CPU |  AMD64 CPU 或 [EM64T](http://en.wikipedia.org/wiki/EMT64#Intel_64) CPU（Core 2 Duo & Quad 处理器均为 EM64T） | |
| 内存 | 256 MB | 512 MB |
| 磁盘空间 | 2.5 GB（不包括交换空间） | |
| 交换空间 | 至少 256 MB | |

Gentoo AMD64 项目页面 是获取更多关于 Gentoo `amd64` 支持信息的好地方。

## Gentoo Linux 安装光盘

### 最小安装 CD

Gentoo 最小安装 CD 是一个可启动光盘，包含一个自包含的 Gentoo 环境。它允许用户从光盘启动 Linux。在启动过程中，会检测硬件并加载相应的驱动程序。该光盘由 Gentoo 开发人员维护，只要有活跃的互联网连接，任何人都可以安装 Gentoo。

最小安装 CD 名为 `install-amd64-minimal-<release>.iso`。

### 偶尔提供的 Gentoo LiveDVD

偶尔，Gentoo Ten 项目会制作一种特殊的 DVD，用于安装 Gentoo。本章后续的指令针对最小安装 CD，因此可能会略有不同。然而，LiveDVD（或任何其他可启动 Linux 环境）支持通过只需在终端中调用 `sudo su -` 或 `sudo -i` 获取 root 提示符。

### 什么是 stage？

`stage3` tar 包是一个包含最小 Gentoo 环境的归档，适用于使用本手册中的指令继续 Gentoo 安装。此前，Gentoo 手册描述了使用三种 stage tar 包之一进行安装。虽然 Gentoo 仍然提供 `stage1` 和 `stage2` tar 包，但官方安装方法使用的是 `stage3` tar 包。如果您感兴趣使用 `stage1` 或 `stage2` tar 包执行 Gentoo 安装，请阅读 Gentoo FAQ 中关于如何使用 stage1 或 stage2 tar 包安装 Gentoo 的内容。

Gentoo 使用的默认安装介质是最小 CD，托管了一个可启动的、极小的 Gentoo 环境，其中带有从[下载](https://www.gentoo.org/downloads/)（推荐）或通过手动浏览许多[可用镜像](https://www.gentoo.org/mirrors/)安装 Gentoo 的工具。

如果从镜像下载：

1. 进入 `releases/` 目录。
2. 选择相关的架构（如 `amd64`）。
3. 选择 `autobuilds/` 目录。
4. 对于 `amd64` 和 `x86`，选择 `current-install-` 或 `current-iso/`。
5. 对于所有其他架构，导航到 `current-iso/`。

**注意**

某些目标架构如 `arm`、`mips` 和 `s390` 将不会有最小 CD。目前，Gentoo Release 项目 不支持为这些目标构建 .iso 文件。

在此位置内部，安装光盘是带有 `.iso` 后缀的文件。例如，查看以下列表：**releases/amd64/autobuilds/current-iso/ 下的可下载文件列表示例**:

```
 [DIR] hardened/                                          05-Dec-2014 01:42    -
[   ] install-amd64-minimal-20141204.iso                 04-Dec-2014 21:04  208M
[   ] install-amd64-minimal-20141204.iso.CONTENTS        04-Dec-2014 21:04  3.0K
[   ] install-amd64-minimal-20141204.iso.DIGESTS         04-Dec-2014 21:04  740
[TXT] install-amd64-minimal-20141204.iso.DIGESTS.asc     05-Dec-2014 01:42  1.6K
[   ] stage3-amd64-20141204.tar.bz2                      04-Dec-2014 21:04  198M
[   ] stage3-amd64-20141204.tar.bz2.CONTENTS             04-Dec-2014 21:04  4.6M
[   ] stage3-amd64-20141204.tar.bz2.DIGESTS              04-Dec-2014 21:04  720
[TXT] stage3-amd64-20141204.tar.bz2.DIGESTS.asc          05-Dec-2014 01:42  1.5K
```

在上面的示例中，`install-amd64-minimal-20141204.iso` 文件就是最小安装 CD 本身。但正如所示，还存在其他相关文件：

*   `.CONTENTS` 文件，是一个列出安装光盘上所有可用文件的文本文件。在下载之前，该文件可以用于用于验证安装光盘上是否有特定的固件或驱动程序。





-   `.DIGESTS` 文件包含 ISO 文件本身的哈希值，采用多种哈希格式/算法。此文件可用于验证下载的 ISO 文件是否损坏。
-   `.DIGESTS.asc` 文件不仅包含 ISO 文件的哈希值（与 `.DIGESTS` 文件相同），还包含该文件的加密签名。这既可以验证下载的 ISO 文件是否损坏，也可以验证该下载内容确实由 Gentoo 发布工程团队提供，且未被篡改。

目前请忽略此位置提供的其他文件 - 这些文件在安装继续进行后会再次。下载 `.iso` 文件，如果想对下载进行验证，请同时下载与该 `.iso` 文件对应的 `.DIGESTS.asc` 文件。不需要下载 `.CONTENTS` 文件，因为安装说明将不再引用该文件，而且 `.DIGESTS` 文件包含的信息与 `.DIGESTS.asc` 文件相同，区别在于后者在其基础上额外包含了一个签名。

## 验证下载的文件

### 注意事项
2.  如果加密签名验证通过，则验证校验和，以确保下载的文件本身没有被损坏。

### 基于 Microsoft Windows 的验证

在 Microsoft Windows 系统上，已经备好用于验证校验和和加密签名的正确工具集的概率较低。

要首先验证加密签名，可以使用 [GPG4Win](http://www.gpg4win.org/) 等工具。安装后，需要导入 Gentoo 发布工程团队的公钥。密钥列表可以在[签名页面](https://www.gentoo.org/downloads/signatures/)上找到。导入后，用户即可验证 `.DIGESTS.asc` 文件的签名。

#### 重要提示

这并不验证 `.DIGESTS` 文件是否正确，仅验证 `.DIGESTS.asc` 文件是正确的。这意味着应该根据 `.DIGESTS.asc` 文件中的值进行校验和验证，这就是为什么上面的指令只提到了下载 `.DIGESTS.asc` 文件。

校验和本身可以使用 [Hashcalc 应用](http://www.sinf.gr/en/hashcalc.html) 进行验证，尽管还有许多其他工具。大多数情况下，这些工具会向用户显示计算出的校验和，并要求用户将其与 `.DIGESTS.asc` 文件中的值进行对比。

### 基于 Linux 的验证

在 Linux 系统上，验证加密签名常用的方法是使用 [app-crypt/gnupg](https://packages.gentoo.org/packages/app-crypt/gnupg) 软件。安装此包后，可以使用以下命令验证 `.DIGESTS.asc` 文件的加密签名。

首先，从[签名页面](https://www.gentoo.org/downloads/signatures/)下载正确的密钥：

```bash
user $ gpg --keyserver hkps.pool.sks-keyservers.net --recv-keys 0xBB572E0E2D182910
```

```
gpg: requesting key 0xBB572E0E2D182910 from hkp server pool.sks-keyservers.net
gpg: key 0xBB572E0E2D182910: "Gentoo Linux Release Engineering (Automated Weekly Release Key) <releng@gentoo.org>" 1 new signature
gpg: 3 marginal(s) needed, 1 complete(s) needed, classic trust model
gpg: depth: 0  valid:   3  signed:  20  trust: 0-, 0q, 0n, 0m, 0f, 3u
gpg: depth: 1  valid:  20  signed:  12  trust: 9-, 0q, 0n, 9m, 2f, 0u
gpg: next trustdb check due at 2018-09-15
gpg: Total number processed: 1
gpg:         new signatures: 1
```

## 启动 CD

### 启动安装 CD

一旦刻录好安装 CD，就可以启动它了。从光驱器中取出所有 CD，重启系统并进入 BIOS 或 UEFI。这通常通过按下 `DEL`、`F1` 或 `ESC` 实现，具体取决于所使用的系统和主板。在 BIOS 或 UEFI 菜单中，更改启动顺序，使 CD-ROM 优先于硬盘启动。如果不进行此更改，系统将直接从硬盘重启，忽略 CD-ROM。

现在将安装 CD 放入 CD-ROM 驱动器并重启。应该会显示启动提示。在此界面，按 `Enter` 将按照默认启动选项开始启动过程。若要使用自定义启动选项启动安装 CD，请指定内核并在后跟启动选项，然后按 `Enter`。

在启动提示界面，用户可以选择显示可用的内核（`F1`）和启动选项（`F2`）。如果在 15 秒内未做出任何选择（无论是显示信息还是使用内核），则安装 CD 将回退到从磁盘启动。这允许安装程序重启并尝试已安装的环境，而无需从光驱槽中取出 CD（这对于远程安装来说非常实用）。
| :--- | :--- |
| gentoo | 支持 K8 CPU（包括 NUMA 支持）和 EM64T CPU 的默认内核 |
| gentoo-nofb | 与 `gentoo` 相同，但不带帧缓冲区支持 |
| memtest86 | 测试本地内存是否存在错误 |

内核之外，启动选项有助于进一步调优启动过程。

| 硬件选项 | 说明 |
| :--- | :--- |
| `acpi=on` | 加载对 ACPI 的支持，并导致 CD 在启动时启动 `acpid` 守护进程。只有当系统需要 ACPI 才能正常工作时才需要此。超线程支持不需要此。 |
| `acpi=off` | 完全禁用 ACPI。这在某些旧系统上很有用，也是使用 APM 的要求。这将禁用你处理器的任何超线程支持。 |
| `console=X` | 为 CD 设置串口控制访问。第一个选项是设备（x86 上通常为 `ttyS0`），随后是任何连接选项，用逗号分隔。默认选项为 9600,8,n,1。 |
| `dmraid=X` | 允许向设备映射器 RAID 子系统传递选项。选项应封装在引号中。 |
| `doapm` | 加载 APM 驱动支持。这还需要设置 `acpi=off`。 |
| `dopcmcia` | 加载对 PCMCIA 和 Cardbus 硬件的支持，并导致 CD 在启动时启动 `pcmcia cardmgr`。只有当从 PCMCIA/Cardbus 设备启动时才需要。 |
| `doscsi` | 加载对大多数 SCSI 控制器的支持。启动大多数 USB 设备的要求，因为它们使用内核的 SCSI 子系统。 |
| `sda=stroke` | 允许在 BIOS 无法处理大磁盘的情况下分区整个硬盘。此选项仅用于带有旧 BIOS 的机器。将 `sda` 替换为需要此选项的设备。 |
| `ide=nodma` | 强制禁用内核中的 DMA，某些 IDE 芯片组和某些 CDROM 驱动器需要它。如果系统读取 IDE CDROM 遇到困难，请尝试此选项。这也会禁用默认 `hdparm` 设置的执行。 |





| `noapic` | 这将禁用较新主板上存在的高可编程中断控制器（APIC）。已知这在旧版硬件上可能会导致某些问题。 |
| `nodetect` | 禁用 CD 执行的所有自动检测功能，包括设备自动检测和 DHCP 探测。这对于对故障的 CD 或驱动进行调试很有用。 |
| `nodhcp` | 禁用对检测到的网卡进行 DHCP 探测。这对于仅使用静态地址的网络很有用。 |
| `nodmraid` | 禁用对 device-mapper RAID 的支持，例如用于板载 IDE/SATA RAID 控制器的 RAID。 |
| `nofirewire` | 禁用 Firewire 模块的加载。当你的 Firewire 硬件导致 CD 启动出现问题时，才需要此选项。 |
| `nogpm` | 禁用 gpm 控制台鼠标支持。 |
| `nohotplug` | 禁用启动时加载热插拔（hotplug）和冷插拔（coldplug）初始化脚本。这对于对故障的 CD 或驱动进行调试很有用。 |
| `nokeymap` | 禁用用于选择非美式键盘布局的键映射选择。 |
| `nolapic` | 禁用单处理器内核上的本地 APIC。 |
| `nosata` | 禁用 Serial ATA 模块的加载。如果系统在 SATA 子系统出现问题，则使用此项。 |
| `nosmp` | 在支持 SMP 的内核上禁用 SMP（对称多处理）。这对于调试某些驱动程序和主板的 SMP 相关问题很有用。 |
| `nosound` | 禁用音频支持和音量设置。这对于音频支持导致问题的系统很有用。 |
| `nousb` | 禁用 USB 模块的自动加载。这对于调试 USB 问题很有用。 |
| `slowusb` | 为缓慢的 USB CD-ROM（如 IBM BladeCenter 中的）在启动过程中添加一些额外的停顿。 |

### 逻辑卷/设备管理 |
| `dolvm` | 启用对 Linux 逻辑卷管理（LVM）的支持。 |

### 其他选项 |
| `debug` | 启用调试代码。这可能会变得很混乱，因为它会在屏幕上显示大量数据。 |
| `docache` | 将 CD 的整个运行部分缓存到 RAM 中，允许用户卸载 `/mnt/cdrom` 并挂载另一个 CD-ROM。此选项要求可用 RAM 至少是 CD 大的两倍。 |
| `scandelay` | 使 CD 在启动过程的某些阶段暂停 10 秒，以便让初始化缓慢的设备准备就绪。 |
| `scandelay=X` | 允许用户指定在启动过程某些阶段添加的延迟（秒），以便让初始化缓慢的设备准备就绪。将 `X` 替换为暂停的秒数。 |

#### 注意
CD 会在检查 `do*` 选项之前检查 `no*` 选项，这样就可以按照指定的顺序进行覆盖。

现在启动 CD，选择一个内核（如果默认的 `gentoo` 内核不再适用）和启动选项。例如，我们启动 `gentoo` 内核，并带有 `dopcmcia` 内内核参数：

```
boot: gentoo dopcmcia
```

接下来，用户将看到启动屏幕和进度条。如果是在非美式键盘的系统上进行安装，请确保立即按下 `Alt` + `F1` 切换到详细模式并按照提示操作。如果在 10 秒内未进行任何选择，将接受默认设置（美式键盘）并继续启动过程。启动过程完成后，用户将自动以 `root` 用户（超级用户）身份登录到“Live”Gentoo Linux 环境。当前控制台上将显示 root 提示符，可以通过按下 `Alt` + `F2`、`Alt` + `F3` 和 `Alt` + `F4` 切换到其他控制台。按下 `Alt` + `F1` 返回启动的控制台。

### 额外的硬件配置
当安装 CD 启动时，它会尝试检测所有硬件设备并加载相应的内核模块来支持这些硬件。在大多数情况下，工作做得非常好。但在某些情况下，它可能不会自动加载系统所需的内核模块。如果 PCI 自动检测漏过了系统的某些硬件，则必须手动加载相应的内核模块。

在下一个示例中，加载了 `8139too` 模块（它支持某些类型的网络接口）：

```
root # modprobe 8139too
```

### 可选：用户账户
如果其他人需要访问安装环境，或者需要在安装 CD 上以非 root 用户身份运行命令（例如出于安全考虑，使用 `irssi` 聊天而不使用 root 权限），则需要创建一个额外的用户账户并将 root 密码设置为强密码。

要更改 root 密码，请使用 `passwd` 工具：

```
root # passwd
```

```
New password: (输入新密码)
Re-enter password: (重新输入密码)
```

要创建用户账户，首先输入其凭据，然后是账户密码。使用 `useradd` 和 `passwd` 命令来完成这些任务。

在下一个示例中，创建了一个名为 `john` 的用户：

```
root # useradd -m -G users john
root # passwd john

要从（当前的）`root` 用户切换到新创建的用户账户，请使用 `su` 命令：

```
root # su - john
```

### 可选：安装时查看文档
若要在安装期间查看 Gentoo 手册，请先按照上述方法创建一个用户账户。然后按下 `Alt` + `F2` 进入新终端。

在安装过程中，可以使用 `links` 命令浏览 Gentoo 手册——当然，这只有在网络连接正常后才能开始。

```
user $ links https://wiki.gentoo.org/wiki/Handbook:AMD64
```

要返回原始终端，按下 `Alt`+`F1`。

### 可选：启动 SSH 守护进程
为了允许其他用户在安装期间访问系统（可能是为了在安装期间支持，甚至进行远程操作），需要创建一个用户账户（如前所述）并启动 SSH 守护进程。

要启动 SSH 守护进程，请执行以下命令：

```
root # /etc/init.d/sshd start
```

**注意**
如果用户登录系统，他们将收到消息，提示需要确认此系统的主机密钥（通过所谓的“指纹”）。这是预期的，因为这是人们首次登录该系统。然而，稍后当系统完成后，有人登录新创建的系统时，SSH 客户端将警告主机密钥已更改。这是因为用户现在登录的是一个对于 SSH 而言不同的服务器（即新安装的 Gentoo 系统，而不是当前安装正在使用的实时环境）。请按照屏幕上给指令替换客户端系统上的主机密钥。

为了能够使用 `sshd`，网络需要正常运行。请继续阅读配置网络章节。

## 自动网络检测
也许它直接就能用？





如果系统连接到带有 DHCP 服务器的以太网，那么网络配置可能已经自动设置好了。如果是这样，安装光盘包含的许多网络感知命令，如 `ssh`、`scp`、`ping`、`irssi`、`wget` 和 `links` 等都可以立即使用。

## 确定接口名称

### ifconfig 命令
eth0      Link encap:Ethernet  HWaddr 00:50:BA:8F:61:7A
          inet addr:192.168.0.2  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::50:ba8f:617a/10 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1498792 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1284980 errors:0 dropped:0 overruns:0 carrier:0
          collisions:1984 txqueuelen:100
          RX bytes:485691215 (463.1 Mb)  TX bytes:123951388 (118.2 Mb)
          Interrupt:11 Base address:0xe800 
```

由于向[可预测网络接口名称](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/)的转变，系统上的接口名称可能与旧的 `eth0` 命名惯不同。最近的安装媒体可能会显示常规网络接口名称，如 `eno0`、`ens1` 或 `enp5s0`。在 `ifconfig` 输出中寻找与本地网络 IP 地址相关的接口。

**提示**

如果使用标准的 `ifconfig` 命令没有显示任何接口，请尝试使用带有 `-a` 选项的命令。此选项强制实用程序显示系统检测到的所有网络接口，无论其处于启用还是禁用状态。如果 `ifconfig -a` 没有产生结果，说明硬件故障或接口驱动程序未加载到内核。这两种情况都超出了手册的范围。请联系 [#gentoo](http://webchat.freenode.net/?channels=gentoo) 获取支持。

### ip 命令

作为 `ifconfig` 的替代方案，可以使用 `ip` 命令确定接口名称。以下示例显示了 `ip addr` 的输出（来自另一个系统，因此显示的信息与之前的示例不同）：

`root #` `ip addr`

```
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether e8:40:f2:ac:25:7a brd ff:ff:ff:ff:ff:ff
    inet 10.0.20.77/22 brd 10.0.23.255 scope global eno1
       valid_lft forever preferred_lft forever
    inet6 fe80::ea40:f2ff:feac:257a/64 scope link 
       valid_lft forever preferred_lft forever
```

上面的输出可能比替代方案稍微复杂一点。上述示例中的接口名称直接跟在数字后面；它是 `eno1`。

在本文的剩余部分中，手册将假设运行的网络接口称为 `eth0`。

## 可选：配置任何代理

如果通过代理访问互联网，则必须在安装期间设置代理信息。定义代理非常：只需定义一个包含代理服务器信息的变量即可。

在大多数情况下，使用服务器主机名定义变量就足够了。例如，我们假设代理名为 `proxy.gentoo.org`，端口为 `8080`。

设置 HTTP 代理（用于 HTTP 和 HTTPS 流量）：

设置 RSYNC 代理：

`root #` `export RSYNC_PROXY="proxy.gentoo.org:8080"`

如果代理需要用户名和密码，请使用以下语法设置变量：

**向代理变量添加用户名/密码**

```
http://username:password@proxy.gentoo.org:8080
```

## 测试网络

尝试 ping 你的 ISP 的 DNS 服务器（在 `/etc/resolv.conf` 中找到）以及任一个选定的网站。这确保了网络运行正常、网络数据包已到达网络、DNS 域名解析正常等。

`root #` `ping -c 3 www.gentoo.org`

如果这一切运行正常，则可以跳过本章的剩余部分，进入准备磁盘。





现在继续进行准备磁盘。

## 手动网络配置

### 加载适当的网络模块

当安装光盘启动时，它会尝试检测所有硬件设备并加载相应的内核模块（驱动程序）来支持这些硬件。在大多数情况下，它的工作非常好。然而，在某些情况下，它可能不会自动加载所需的内核模块。

如果 `net-setup` 或 `pppoe-setup` 失败，可能是网卡没有被立即找到。这意味着用户可能需要手动加载适当的内核模块。

要查找为网络提供了哪些内核模块，请使用 `ls` 命令：

`root #` `ls /lib/modules/`uname -r`/kernel/drivers/net``

如果找到了网络设备的驱动程序，请使用 `modprobe` 加载内核模块。例如，加载 `pcnet32` 模块：

`root #` `modprobe pcnet32`

要检查网卡现在是否被检测到，请使用 `ifconfig`。检测到的网卡将显示类似如下的内容（再次说明，这里的 `eth0` 只是一个示例）：

          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)
```

但如果显示以下错误，则网卡未被检测到：

`root #` `ifconfig eth0`

```
eth0: error fetching interface information: Device not found
```

可以通过 `/sys` 文件系统列出系统上可用的网络接口名称：

`root #` `ls /sys/class/net`

```
dummy0  eth0  lo  sit0  tap0  wlan0
```

在上面的示例中，找到了 6 个接口。`eth0` 最可能是（有线的）以太网适配器，而 `wlan0` 是无线接口。

假设网卡现在已检测到，请重试 `net-setup` 或 `pppoe-setup`（现在应该可以工作了），但对于硬核用户，我们也解释了如何手动配置网络。

根据您的网络设置选择以下章节之一：

*   使用 DHCP 用于自动获取 IP
*   准备无线访问 如果使用了无线网络
*   理解网络术语 解释网络基础
*   使用 ifconfig 和 route 解释如何手动设置网络

### 使用 DHCP

DHCP（动态主机配置协议）使得自动接收网络信息成为（IP 地址、子网掩码、广播地址、网关、DNS 服务器等）。这只有在网络中有 DHCP 服务器（或 ISP 提供 DHCP 服务）时才有效。要让网络接口自动接收这些信息，请使用 `dhcpcd`：

`root #` `dhcpcd eth0`

某些网络管理员要求系统使用 DHCP 服务器提供的主机名和域名。在这种情况下，请使用：

`root #` `dhcpcd -HD eth0`

如果此有效（尝试 ping 某些互联网服务器，如 Google），则说明一切已就绪并可以继续了。跳过本节的其余部分并继续进行准备磁盘。

在使用无线 (802.11) 网卡时，在继续之前需要配置无线设置。要查看网卡当前的无线设置，可以使用 `iwconfig`。运行 `iwconfig` 可能会显示类似：

`root #` `iwconfig eth0`

```
eth0      IEEE 802.11-DS  ESSID:"GentooNode"                                   
          Mode:Managed  Frequency:2.442GHz  Access Point: 00:09:5B:11:CC:F2    
          Bit Rate:11Mb/s   Tx-Power=20 dBm   Sensitivity=0/65535               
          Retry limit:16   RTS thr:off   Fragment thr:off                       
          Power Management:off                                                  
          Link Quality:25/10  Signal level:-51 dBm  Noise level:-102 dBm        
          Rx invalid nwid:5901 Rx invalid crypt:0 Rx invalid frag:0 Tx          
          excessive retries:237 Invalid misc:350282 Missed beacon:84 
```

**注意**

某些无线网卡的设备名称可能是 `wlan0` 或 `ra0` 而不是 `eth0`。运行不带任何参数的 `iwconfig` 以确定正确的设备名称。

对于大多数用户，只有两个设置可能需要更改：ESSID（即无线网络名称）或 WEP 密钥。如果列出的 ESSID 和访问地址已经是环境中的，说明环境工作正常。

要更改 ESSID 或添加 WEP 密钥，请执行以下命令。

*   将网络名称设置为 `GentooNode`：
    `root #` `iwconfig eth0 essid GentooNode`
*   设置十六进制 WEP 密钥：
    `root #` `iwconfig eth0 key 12341234`
*   设置 ASCII WEP 密钥，在密钥前加缀 `s:`：
    `root #` `iwconfig eth0 key s:password`

**注意**

如果无线网络使用 WPA 或 WPA2 设置，则需要使用 `wpa_supplicant`。有关在 Gentoo 中配置无线的更多信息，请阅读 Gentoo Handbook 中的无线章节。

再次使用 `iwconfig` 确认无线设置。一旦无线正常，请按照下一节所述继续 IP 层选项（理解网络术语）或如所述使用 `net-setup` 工具。

### 理解网络术语

**注意**

如果已知 IP 地址、广播地址、子网掩码和 DNS 服务器，请跳过此小节并继续进行使用 ifconfig 和 route。

如果上述所有操作均失败，则需要手动配置网络。这并不困难。然而，可能需要一些网络术语和基本概念知识。阅读本节后，用户将知道什么是网关、子网掩码的用途、广播地址是如何形成的以及为什么系统需要 DNS 服务器。

IP Address (bits):      11000000 10101000 00000000 00000010
                        -------- -------- -------- --------
                           192      168       0        2
```





IPv4 的继任者 IPv6 使用 128 位（0 和 1）。在本节中，重点是 IPv4 地址。

对于所有可访问的网络而言，此类 IP 地址对于主机来说是唯一的（即你希望能够访问的每个主机都必须有一个唯一的 IP 地址）。为了区分网络内部和外部的主机，IP 地址分为两个部分：网络部分和主机部分。

这种划分通过 `netmask`（子网掩码）表示，它是一系列 1 后面跟着一串 0。IP 中映射到 1 的部分是网络部分，另一部分是主机部分。像常一样，子网掩码可以以 IP 地址的形式写入。

### 网络/主机划分示例

```
 IP address:    192      168      0         2
            11000000 10101000 00000000 00000010
Netmask:    11111111 11111111 11111111 00000000
               255      255     255        0
           +--------------------------+--------+
                    Network              Host
```

换句话说，`192.168.0.14` 是示例网络的一部分，但 `192.168.1.2` 不是。

广播地址是一个与网络具有相同网络部分、但主机部分全为 1 的 IP 地址。网络上的每个主机都会监听这个 IP 地址。它确实是为了广播数据包设计的。

### 广播地址

```
 IP address:    192      168      0         2
            11000000 10101000 00000000 00000010
Broadcast:  11000000 10101000 00000000 11111111
               192      168      0        255
           +--------------------------+--------+
                     Network             Host
```

为了能够浏览互联网，网络中的每台计算机都必须知道哪个主机共享了互联网连接。这个主机被称为网关。由于它是一个普通主机，因此它有一个普通的 IP 地址（例如 `192.168.0.1`）。

之前我们提到每个主机都有自己的 IP 地址。为了能够通过名称（而不是 IP 地址）访问此主机，我们需要一种将名称（如 `dev.gentoo.org`）翻译为 IP 地址（如 `64.5.62.82`）的服务。这种服务被称为 `name service`（域名服务）。使用此类服务，需要在 `/etc/resolv.conf` 中定义必要的域名服务器。
| :--- | :--- |
| 系统 IP 地址 | 192.168.0.2 |
| 子网掩码 | 255.255.255.0 |
| 广播地址 | 192.168.0.255 |
| 网关 | 192.168.0.1 |
| 域名服务器 | 195.130.130.5, 195.130.130.133 |

### 使用 ifconfig 和 route

设置网络包含三个步骤：

1. 使用 `ifconfig` 分配 IP 地址
2. 使用 `route` 设置到网关的路由
3. 通过将 DNS 服务器 IP 存放在 `/etc/resolv.conf` 完成设置

要分配 IP 地址，需要 IP 地址、广播地址和子网掩码。然后执行以下命令，将 `${IP_ADDR}` 替换为正确的 IP 地址，将 `${BROADCAST}` 替换为正确的广播地址，并将 `${NETMASK}` 替换为正确的子网掩码：

```bash
root # ifconfig eth0 ${IP_ADDR} broadcast ${BROADCAST} netmask ${NETMASK} up
```

使用 `route` 设置路由。将 `${GATEWAY}` 替换为正确的网关 IP 地址：

```bash
root # route add default gw ${GATEWAY}
```

现在打开 `/etc/resolv.conf`：

```bash
root # nano -w /etc/resolv.conf
```

使用以下模板填充 DNS 服务器（s）。确保将 `${NAMESERVER1}` 和 `${NAMESERVER2}` 替换为适当的 DNS 服务器地址：

### /etc/resolv.conf 使用的默认模板

```
nameserver ${NAMESERVER1}
nameserver ${NAMESERVER2}
```

就是这样。现在通过 ping 某些互联网服务器（如 Google）来测试网络。如果成功了，恭喜你。继续准备磁盘。

### 分区表

从上面的描述中，人们可能会认为使用 GPT 始终应该是推荐的方法，但有几需要注意。

目前正在使用两种分区技术：`MBR` 和 `GPT`。

#### MBR

`MBR`（主引导记录）设置使用 32 位标识符作为分区的起始扇区和长度，并支持三种分区类型：主分区、扩展分区和逻辑分区。主分区的信息存储在主引导记录本身中。由于这个空间很小，仅支持四个主分区（例如 `/dev/sda1` 到 `/dev/sda4`）。

为了支持更多分区，可以将其中一个主分区标记为扩展分区。该分区随后可以包含逻辑分区（分区中的分区）。由于 32 位标识符限制，每个分区的大小限制为 2 TB。此外，MBR 设置不提供任何备份-MBR，因此如果应用程序或用户覆盖了 MBR，所有分区信息将丢失。

#### GPT

`GPT`（GUID 分区表）设置为分区使用 64 位标识符。它存储分区信息的位置也比 MBR 的 512 字节大得多，并且对分区数量没有限制。此外，分区的大小受限于一个大得限制（几乎是 8 ZB - 是的，泽字节）。

当系统操作系统与固件之间的软件接口为 UEFI（而不是 BIOS）时，GPT 几乎是强制性的，因为与 MBR 会产生兼容性问题。GPT 的另一个优势是在磁盘末尾有一个备份 GPT，可以用于修复磁盘开头的主 GPT 损坏。GPT 还带有 CRC32 校验和，以检测头和分区表中的错误。

### GPT 或 MBR

从上面的描述中，使用 GPT 始终应该是推荐的方法，但有几需要注意。在基于 BIOS 的计算机上使用 GPT 可以运行，但你无法与 Microsoft Windows 操作系统进行双引导。原因是 Microsoft Windows 如果检测到 GPT 分区标签，将在 EFI 模式下引导。某些配置为以 BIOS/CSM/Legacy 模式启动的缺陷 BIOS 或 EFI 也可能在从 GPT 标签磁盘启动时出现问题。如果是这种情况，可能可以通过在保护性 MBR 分区上添加启动/活动标记来解决该问题，这必须通过 `fdisk` 配合 `-t dos` 选项强制其使用 MBR 格式读取分区表。

在这种情况下，启动 `fdisk` 并使用 `a` 键切换标记。按 `1` 选择第一个分区，然后按 `w` 键将更改写入磁盘并退出 fdisk 应用程序。





`user $` `fdisk -t dos /dev/sda`

```
Welcome to fdisk (util-linux 2.24.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): a
Partition number (1-4): 1

Command (m for help): w
```

### 使用 UEFI

在使用 UEFI 启动操作系统的系统（而不是 BIOS）上安装 Gentoo 时，创建一个 EFI 系统分区（EFI system partition）是非常关重要的。下文关于 `parted` 的说明包含了此操作所需的指引。

### 高级存储

#### Btrfs RAID

如上所述，`btrfs` 具有跨多个设备创建文件系统的能力。这种方式生成的 `Btrfs` 文件系统可以以后模式运行：`raid0`、`raid1`、`raid10`、`raid5` 和 `raid6`。RAID 模式 `5` 和 `6` 有了改进，但仍被认为不稳定。创建多设备文件系统后，可以使用少量命令添加新设备并移除旧设备`Btrfs` 比其他文件系统需要更多的参与，因此对新手并不友好。

`ext4` 文件系统可以转换为 `btrfs` 文件系统，这对于那些希望使用稳定、经过测试的文件系统安装 Gentoo，并希望通过实验逐渐增加对 `btrfs` 等新文件系统了解的人来说可能有用。

#### LVM2

`amd64` 安装光盘支持 `LVM2`。`LVM2` 增加了分区设置提供的灵活性。下方的安装指令将侧重于“普通”分区，但如果需要该路径，知道支持 `LVM2` 是很有好的。

### 默认分区方案

在手册的剩余部分中，将使用以下分区方案作为简单的布局示例：

| 分区 | 文件系统 | 大小 | 描述 |
| :--- | :--- | :--- | :--- |
| `/dev/sda1` | (引导程序) | 2M | BIOS 启动分区 |
| `/dev/sda2` | `ext2` (或 `vfat`) | 128M | 启动分区 |
| `/dev/sda3` | (swap) | 512M 或更高 | 交换分区 |
| `/dev/sda4` | `ext4` | 磁盘剩余空间 | 根分区 |

如果这足够且读者采用 GPT 路径，可以立即跳转到 默认：使用 parted 对磁盘进行分区。那些对 MBR 仍然感兴趣（嘿——确实会！）并想使用示例布局的人可以跳转到 替代方案：使用 fdisk 对磁盘进行分区。

`fdisk` 和 `parted` 都是分区工具。`fdisk` 广为人知、稳定，并推荐用于 MBR 分区布局，而 `parted` 是第一批支持 GPT 分区的 Linux 块设备管理工具之一。喜欢 `fdisk` 用户界面的可以使用 `gdisk` (GPT fdisk) 作为 `parted` 的替代方案。

在进入创建指令之前，第一部分将更详细地描述如何创建分区方案并提到一些常见的陷阱。

## 设计分区方案

### 多少以及多大？

分区的数量高度取决于环境。例如，有很多用户，建议将 `/home/` 独立，因为这可以增加安全性并使备份更容易。如果安装 Gentoo 是为了邮件服务器，那么 `/var/` 应该是独立的，因为所有邮件都存储在 `/var/` 中。选择合适的文件系统将能够最大化性能。游戏服务器将有一个独立的 `/opt/`，因为大多数游戏服务器都安装在那里。`/home/` 的原因类似：安全性和备份。在大多数情况下，`/usr/` 应该保持大一些：它不仅包含大部分应用程序，仅 Portage 树就占用大约 500 MB，还不包括存储在其中的各种源码。

可见，这很大程度上取决于管理员想要什么。独立的分区或卷具有以下优势：

*   为每个分区或卷选择性能最好的文件系统。
*   如果某个失效工具持续向某个分区或卷写入文件，整个系统不会耗尽可用空间。
*   如有必要，文件系统检查的时间会减少，因为可以并行进行多次检查（尽管这种优势在多个磁盘上比在多个分区上更明显）。
*   通过将某些分区或卷挂载为只读、`nosuid`，可以增强安全性。

然而，多个分区也有缺点。如果配置不当，系统可能会在一个分区上有很多可用空间，而在另一个分区上没有。此外，挂载点如 `/usr/` 或 `/var/` 往往需要 `initramfs` 在启动脚本之前挂载。这并不总是这样，所以结果可能有所异。对于 SCSI 和 SATA 磁盘，还有一个 15 个分区的限制，除非使用 GPT 标签。

### 什么是 BIOS 启动分区？

BIOS 启动分区是非常小的（1 到 2 MB）分区，引导程序如 GRUB2 可以在其中放入无法放入分配存储（MBR 情况下为几百字节）且无法放在其他地方的数据。

此类分区并非总是，但考虑到低空间消耗以及我们在记录分区差异方面的困难，建议在任何情况下都创建它。

为了完整起见，当使用 GPT 分区布局配合 GRUB2，或者当使用 MBR 分区布局配合 GRUB2 且第一个分区早于磁盘上的 1 MB 位置时，需要 BIOS 启动分区。

## 默认：使用 parted 对磁盘进行分区

在本章中，将使用之前指令提到的示例分区布局：

| 分区 | 描述 |
| :--- | :--- |
| `/dev/sda1` | BIOS 启动分区 |
| `/dev/sda2` | 启动分区 |
| `/dev/sda3` | 交换分区 |
| `/dev/sda4` | 根分区 |

根据个人偏好更改分区布局。

### 使用 parted 查看当前分区布局

`parted` 程序提供了一个简单的磁盘分区界面，并支持非常大的分区（超过 2 TB）。启动 parted 磁盘（在我们的示例中，我们使用 `/dev/sda)。建议要求 parted 使用最佳分区对齐：

`root #` `parted -a optimal /dev/sda`

```
GNU Parted 2.3
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
```




对齐意味着分区从磁盘内已知边界处开始，以确保操作系统层面的磁盘操作（从磁盘检索页面）使用最少的磁盘内部操作次数。未对齐的分区可能导致，即使操作系统只请求单个页面，磁盘也需要读取两个页面而不是一个。

要了解 `parted` 支持的所有选项，请输入 `help` 并按回车。

### 设置 GPT 标签

`x86` 或 `amd64` 架构上的大多数磁盘都是使用 `msdos` 标签准备的。使用 `parted` 命令在磁盘上放置 GPT 标签的命令是 `mklabel gpt`：**警告**

若要使磁盘具有 MBR 布局，请使用 `mklabel msdos`。

### 使用 parted 删除所有分区

如果尚未执行此操作（例如，通过了先前的 `mklabel` 操作，或者因为磁盘是新格式化的），首先从磁盘上删除所有现有分区。输入 `print` 查看当前分区，并输入 `rm <N>`，其中 `<N>` 是要删除的分区编号。

```
(parted) rm 2
```

对所有不需要的其他分区执行相同操作。然而，确保不要在这里犯任何错误——`parted` 会立即执行更改（不像 `fdisk`，它会暂存更改，允许用户在保存或退出 `fdisk` 之前“撤销”更改）。

### 创建分区

现在创建分区。使用 `parted` 创建分区并不困难——我们只需要告知 `parted` 以下设置：

*   使用的分区类型。这通常是 `primary`。如果使用了 `msdos` 分区标签，请记住主分区不能超过 4 个。如果需要超过 4 个分区，请将前四个分区之一设为扩展分区，并在其中创建逻辑分区。
*   分区的起始位置（可以用 MB、GB、... 等表示）
*   分区的结束位置（可以用 MB、GB、... 等表示）

首先，告诉 `parted` 我们使用的尺寸单位是兆字节（实际上是兆兆，缩写为 `MiB`，这是“标准”符号，但我们在整个文中将使用 `MB`，因为它常见得多）：

```
(parted) unit mib
```

现在创建一个 2 MB 分区，稍后将用于 GRUB2 引导程序。使用 `mkpart` 命令为此操作，并告知 `parted` 从 1 MB 开始到 3 MB （创建一个大小为 2 MB 的分区）。

```
(parted) mkpart primary 1 3
(parted) name 1 grub
(parted) set 1 bios_grub on
(parted) print
```

```
Model: Virtio Block Device (virtblk)
Disk /dev/sda: 20480MiB
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number   Start      End      Size     File system  Name   Flags
 1       1.00MiB    3.00MiB  2.00MiB               grub   bios_grub
(parted) name 2 boot
(parted) mkpart primary 131 643
(parted) name 3 swap
(parted) mkpart primary 643 -1
(parted) name 4 rootfs
```

当使用 UEFI 接口启动系统（而不是 BIOS）时，将引导分区标记为 EFI 系统分区。当在分区上设置 `boot` 选项时，`parted` 会自动这样做：

```
(parted) set 2 boot on
```

最终结果所示：

```
(parted) print
```

```
Model: Virtio Block Device (virtblk)
Disk /dev/sda: 20480MiB
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number   Start      End      Size     File system  Name   Flags
 1       1.00MiB    3.00MiB  2.00MiB               grub   bios_grub
 2       3.00MiB    131MiB   128MiB                boot   boot
 3       131MiB     643MiB   512MiB                swap
 4       643MiB     20479MiB 19836MiB              rootfs
```

**注意**

在 UEFI 安装上，引导标记将出现在引导分区上。

使用 `quit` 命令退出 `parted`。

## 替代方案：使用 fdisk 对磁盘分区

**注意**

尽管最近的 `fdisk` 应该支持 GPT，但它在 GPT 上仍存在一些问题。下面提供的说明假设使用的分区布局是 MBR。

| /dev/sda3 | 交换分区 |
| /dev/sda4 | 根分区 |

### 查看当前布局

使用 `fdisk` 显示当前布局：`fdisk -l`。

以下部分解释了如何使用 `fdisk` 创建示例分区布局。示例分区布局之前提到过：

| 分区 | 描述 |
| :--- | :--- |
| /dev/sda1 | BIOS 引导分区 |
| /dev/sda2 | 引导分区 |
| /dev/sda3 | 交换分区 |
| /dev/sda4 | 根分区 |

### 修改分区布局

`fdisk` 是一个划分分区的强大工具。`注意`

若要使用 GPT，添加 `t`。`fdisk` 默认使用 MBR。

```
Disk /dev/sda: 30.0 GB, 30005821440 bytes
240 heads, 63 sectors/track, 3876 cylinders
Units = cylinders of 15120 * 512 = 7741440 bytes

Device Boot    Start       End    Blocks   Id  System
```

### 使用 fdisk 删除所有分区

首先从磁盘上删除所有现有分区。输入 `d` 删除分区。例如，要删除现有的 `sda1`：

```
Command (m for help): d
Partition number (1-4): 1
```

该分区现在已安排删除。在打印分区列表时它将不再显示，但在更改保存之前不会被擦除。这允许用户在出错时撤销操作——在这种情况下，立即输入 `q` 并按回车，分区将不会删除。

重复输入 `p` 打印分区列表，然后输入 `d` 和要删除的分区编号。最终，分区表将为空：

```
```

### 创建 BIOS 引导分区

现在内存中的分区表是空的，我们准备好创建分区。

首先创建一个非常小的 BIOS 引导分区。输入 `n` 创建新分区，然后输入 `p` 选择主分区，紧随输入 `1` 选择第一个主分区。在提示起始扇区时，确保它从 2048 开始（引导程序需要它）并按回车。在提示最后一个扇区时，输入 `+2M` 以创建一个大小为 2 字节的分区：**注意**

从扇区 2048 开始是一种安全措施，以防引导程序无法检测到该分区可用。

```
Command (m for help): n
```





```
Command action
  e   extended
  p   primary partition (1-4)
p
Partition number (1-4): 1
First sector (64-10486533532, default 64): 2048
Last sector, +sectors +size{M,K,G} (4096-10486533532, default 10486533532): +2M
```

为 EFI 目的标记该分区：

`Command (m for help):` `t`

```
Selected partition 1
Hex code (type L to list codes): 4
Changed system type of partition 1 to 4 (BIOS boot)
```

注意 `Note` 

不建议在 MBR 分区布局下使用 EFI。如果使用了支持 EFI 的系统，请使用 GPT 布局。

### 创建启动分区

  e   extended
  p   primary partition (1-4)
p
Partition number (1-4): 2
First sector (5198-10486533532, default 5198): (Hit enter)
Last sector, +sectors +size{M,K,G} (4096-10486533532, default 10486533532): +128M
```

现在，当按下 `p` 时，将显示分区打印信息：

`Command (m for help):` `p`

```
Disk /dev/sda: 30.0 GB, 30005821440 bytes
240 heads, 63 sectors/track, 3876 cylinders
Units = cylinders of 15120 * 512 = 7741440 bytes

   Device Boot    Start       End    Blocks   Id  System
/dev/sda1             1         3      5198+  ef  EFI (FAT-12/16/32)
/dev/sda2             3        14    105808+  83  Linux
```

输入 `a` 切换分区的启动标记并选择 `2`。再次按下 `p` 后，注意到 "Boot" 列中放置了一个 `*`。

### 创建交换分区

要创建交换分区（swap partition），输入 `n` 创建新分区，然后输入 `p`  `fdisk` 创建主分区。然后输入 `3` 创建第三个主分区 `/dev/sda3`。当提示输入起始扇区时，按 `Enter`。当提示输入结束扇区时，输入 `+512M`（或交换空间所需的任何大小）来创建一个大小为 512MB 的分区。

在完成所有这些操作后，输入 `t` 设置分区类型，输入 `3` 选择刚刚创建的分区，然后输入 `82` 将分区类型设置为 "Linux Swap"。

### 创建根分区

最后，创建根分区（root partition），输入 `n` 创建新分区，然后输入 `p` 让 `fdisk` 创建主分区。然后输入 `4` 创建第四个主分区 `/dev/sda4`。当提示输入起始扇区时，按 `Enter`。当提示输入结束扇区时，按 `Enter` 创建一个占据磁盘上剩余空间的分区。完成这些步骤后，输入 `p` 应该显示出类似所示的分区表：

`Command (m for help):` `p`

```
Disk /dev/sda: 30.0 GB, 30005821440 bytes
240 heads, 63 sectors/track, 3876 cylinders
Units = cylinders of 15120 * 512 = 7741440 bytes

   Device Boot    Start       End    Blocks   Id  System
/dev/sda1             1         3      5198+  ef  EFI (FAT-12/16/32)
/dev/sda2   *         3        14    105808+  83  Linux
要保存分区布局并退出 `fdisk`，输入 `w`。

`Command (m for help):` `w`

分区创建完成后，现在是时候在它们上建立文件系统了。

## 创建文件系统

### 简介

现在分区已经创建，是需要在它们上放置文件系统了。在下一节中将介绍 Linux 支持的各种文件系统。已经知道使用哪种文件系统的读者可以继续阅读 将文件系统应用到分区。其他人则应该继续阅读以了解可用的文件系统……

### 文件系统

有多种文件系统可用。其中一些在 amd64 架构上被认为是稳定的——在为重要分区选择更实验性的文件系统之前，建议阅读相关文件系统及其支持状态。

#### btrfs

一种下一代文件系统，提供了许多高级功能，如快照、通过校验和进行自愈、透明压缩、子卷和集成 RAID。一些发行版已开始将其作为开箱可用选项，但它尚未达到生产就绪。文件系统损坏的报告很常见。其开发者促人们运行最新版本的内核以确保安全，因为旧版本已知缺陷。这种情况已经持续多年，现在还太早判断情况是否发生了变化。针对损坏问题的修复很少回溯到旧内核中。使用此文件系统时务必小心！

#### ext2

这是一个经过验证的 Linux 文件系统，但它没有元数据日志，这意味着启动时进行常规的 `ext2` 文件系统检查可能非常耗时。现在有许多新一代日志文件系统，可以非常快速地检查一致性，因此通常优于它们的非日志对应品。日志文件系统可以防止在系统启动且文件系统恰好处于不一致状态时长时间延迟。

#### ext3

`ext2` 文件系统的日志版本，除了提供元数据日志以快速恢复外，还提供了全数据日志和顺序数据日志等其他增强日志模式。它使用 `HTree` 索引，在几乎所有情况下都能实现高性能。简而言之，`ext3` 是一个非常优秀且可靠的文件系统。

#### ext4

`ext4` 最初作为 `ext3` 的分支创建，它通过对磁盘格式进行中等修改，带来了新功能、性能改进并消除了大小限制。它可以跨越高达 1 EB 的卷，最大文件大小为 16TB。`ext4` 没有使用经典的 `ext2/3` 位图块分配方法，而是使用 `extents`，这提高了大文件的性能并减少了碎片。`ext4` 还提供了更复杂的块分配算法（延迟分配和多块分配），为文件系统驱动程序提供了更多优化磁盘数据布局的方法。`ext4` 是推荐的通用全平台文件系统。

#### f2fs

闪存友好文件系统（Flash-Friendly File System）最初由三星创建，用于 NAND 闪存。截至 2016 年第二季度，该文件系统仍被认为不成熟，但在将 Gentoo 安装到 microSD 卡、USB 驱动器或其他闪存存储设备时，是一个不错的选择。

#### JFS

IBM 的高性能日志文件系统。`JFS` 是一种基于 `B+tree` 的轻量、快速且可靠的文件系统，在各种条件下都有良好的性能。

#### ReiserFS

一种基于 `B+tree` 的日志文件系统，具有良好的性能，特别是在处理许多微文件时，代价是消耗更多的 CPU 周期。`ReiserFS` 的维护似乎比其他文件系统少。

也称为 `FAT32`，Linux 支持它但不支持任何权限设置。它主要用于与其他操作系统（主要是微软 Windows）的互操作，但也是某些系统固件（如 UEFI）的必要条件。

#### NTFS

这种“新技术”文件系统是微软 Windows 的旗舰文件系统。与上面的 `vfat` 类似，它不存储 BSD 或 Linux 正常运行所需的权限设置或扩展属性，因此不能作为根文件系统。它*仅*用于与 Windows 系统进行互操作（注意“仅”的强调）。





在小分区（小于 8GB）上使用 `ext2`、`ext3` 或 `ext4` 时，必须使用正确的选项创建文件系统以保留足够的节点（inodes）。`mke2fs` (`mkfs.ext2`) 程序使用 `"bytes-per-inode"` 设置来计算文件系统应该拥有多少个节点。对于较小的分区，建议增加计算出的 inode 数量。

在 `ext2` 上，可以使用以下命令完成：

```bash
root # mkfs.ext2 -T small /dev/<device>
```

在 `ext3` 和 `ext4` 上，添加 `-j` 选项以启用日志功能：

```bash
root # mkfs.ext2 -j -T small /dev/<device>
```

这通常会使给定文件系统的 inode 数量增加四倍，因为其 `"bytes-per-inode"` 从每 16kB 一个减少到每 4kB 一个。通过提供比例，可以进一步调优：

```bash
root # mkfs.ext2 -i <ratio> /dev/<device>
```

## 在分区上应用文件系统

要在分区或卷上创建文件系统，对于每可能的的文件系统都有相应的用户空间工具。点击下表中的文件系统名称获取每个文件系统的更多信息：

| 文件系统 | 创建命令 | 最小 CD 中包含？ | 软件包 |
| :--- | :--- | :--- | :--- |
| btrfs | `mkfs.btrfs` | 是 | [sys-fs/btrfs-progs](https://packages.gentoo.org/packages/sys-fs/btrfs-progs) |
| ext2 | `mkfs.ext2` | 是 | [sys-fs/e2fsprogs](https://packages.gentoo.org/packages/sys-fs/e2fsprogs) |
| ext3 | `mkfs.ext3` | 是 | [sys-fs/e2fsprogs](https://packages.gentoo.org/packages/sys-fs/e2fsprogs) |
| ext4 | `mkfs.ext4` | 是 | [sys-fs/e2fsprogs](https://packages.gentoo.org/packages/sys-fs/e2fsprogs) |
| f2fs") | `mkfs.f2fs` | 是 | [sys-fs/f2fs-tools](https://packages.gentoo.org/packages/sys-fs/f2fs-tools) |
| jfs | `mkfs.jfs` | 是 | [sys-fs/jfsutils](https://packages.gentoo.org/packages/sys-fs/jfsutils) |
| reiserfs") | `mkfs.reiserfs` | 是 | [sys-fs/reiserfsprogs](https://packages.gentoo.org/packages/sys-fs/reiserfsprogs) |
| xfs | `mkfs.xfs` | 是 | [sys-fs/xfsprogs](https://packages.gentoo.org/packages/sys-fs/xfsprogs) |
root # mkfs.ext2 /dev/sda2
root # mkfs.ext4 /dev/sda4
```

现在在新建的分区（或逻辑卷）上创建文件系统。

## 激活交换分区

`mkswap` 是用于初始化交换分区的命令：

```bash
root # mkswap /dev/sda3
```

要激活交换分区，使用 `swapon`：

```bash
root # swapon /dev/sda3
```

使用上述命令创建并激活交换空间。

## 挂载

现在分区已经初始化并包含了文件系统，是时候挂载这些分区了。使用 `mount` 命令，但不要忘记为每个创建的分区创建必要的挂载目录。例如，我们挂载根分区和启动分区：

```bash
root # mount /dev/sda4 /mnt/gentoo
root # mkdir /mnt/gentoo/boot
root # mount /dev/sda2 /mnt/gentoo/boot
```

**注意**

如果 `/tmp/` 需要位于单独的分上，请确保在挂载后更改其权限：

```bash
root # chmod 1777 /mnt/gentoo/tmp
```

这同样适用于 `/var/tmp`。

在后续说明中，将挂载 `proc` 文件系统（内核的虚拟接口）以及其他内核伪文件系统。但在此之前，我们先安装 Gentoo 安装文件。

```bash
root # date
```

如果日期不正确，使用 `date` 命令更新：

```bash
root # date MMDDhhmmYYYY
```

### 选择 stage

选择正确的 stage tar 包至关重要。stage 包含了构建系统所需的基础工具。

#### Multilib (64-位)

选择 stage tar 包至关重要。大多数用户应该选择 AMD64/Stage。这提供了相当大的灵活性。

#### No-multilib (32-位)

不建议选择 `no-multilib` stage，因为不推荐这样做。

**警告**

请注意，从 no-multilib 迁移到 multilib 需要对工具链 有深入了解。这超出了本指南的范围。

### 下载 stage tar 包

进入 root 挂的 Gentoo 挂载点（通常是 `/mnt/gentoo`）：

```bash
root # cd /mnt/gentoo
```

取决于安装媒介，有几种工具可以下载 stage。这些工具之一是 `links`，一个非图形化的、菜单驱动的浏览器。要下载 stage，浏览到 Gentoo 镜像列表，例如：

```bash
root # links https://www.gentoo.org/downloads/mirrors/
```

使用 `links` 使用 HTTP 代理时，通过 `-http-proxy` 选项传递 URL：

```bash
root # links -http-proxy proxy.server.com:8080 https://www.gentoo.org/downloads/mirrors/
```

如果需要定义代理，导出 `http_proxy` 和/或 `ftp_proxy` 变量：

```bash
root # export http_proxy="http://proxy.server.com:port"
root # export ftp_proxy="http://proxy.server.com:port"
```

在镜像列表上，选择一个最近的镜像。通常 HTTP 镜像足够了，但也可用其他协议。进入 `releases/amd64/autobuilds/` 目录。在这里显示所有所有 stage 文件（它们可能存储在以子架构命名的子目录中）。选择一个并按 `D` 下载。





与最小化安装 CD 类似，还有额外的下载内容：

- 一个 `.CONTENTS` 文件，包含 stage tar 压缩包内所有文件的列表
- 一个 `.DIGESTS` 文件，包含不同算法的 stage 文件的校验和
- 一个 `.DIGESTS.asc` 文件，与 `.DIGESTS` 文件一样，包含不同算法的 stage 文件的校验和，但经过了加密学签名，以确保其由 Gentoo 项目提供

完成后，按 `Q` 退出浏览器。

下载 stage 文件后，可以验证已下载的 stage tar 压缩包的完整性。使用 `openssl` 将输出结果与 `.DIGESTS` 或 `.DIGESTS.asc` 文件提供的校验和进行对比。

例如，验证 SHA512 校验和：

```bash
root # openssl dgst -r -sha512 stage3-amd64-<release>.tar.bz2
```

另一种方法是使用 `sha512sum` 命令：

```bash
root # sha512sum stage3-amd64-<release>.tar.bz2
```

验证 Whirlpool 校验和：

```bash
root # openssl dgst -r -whirlpool stage3-amd64-<release>.tar.bz2
```

将这些命令的输出与 `.DIGESTS(.asc)` 文件中记录的值进行对比。值必须匹配，否则下载的文件可能损坏（或者校验和文件损坏了）。

### 解压 stage tar 压缩包

现在将下载的 stage 解压到系统中。我们使用 `tar` 来操作：

```bash
root # tar xvjpf stage3-*.tar.bz2 --xattrs
```

确保使用了相同的选项（`xvjpf` 和 `--xattrs`）。`x` 代表提取（Extract），`v` 代表详细（Verbose）以查看解压过程中的情况（可选），`j` 代表使用 bzip2 解压缩，`p` 代表保留权限（Preserve permissions），`f` 表示我们要提取的是文件（File）而非标准输入。最后，`--xattrs` 用于包含归包中存储的扩展属性。

现在 stage 已经安装完成，继续配置编译选项。

## 配置编译选项

### 介绍

为了优化 Gentoo，可以设置几个变量，这些变量会影响 Portage（Gentoo 官方支持的包管理器）的行为。所有这些变量都可以设置为环境变量（使用 `export`），但那并不是永久的。为了保留设置，Portage 会读取 `/etc/portage/make.conf` 文件，这是 Portage 的配置文件。

**注意**

在 `/mnt/gentoo/usr/share/portage/config/make.conf.example` 中可以找到所有可能变量的注释列表。由于[此处有逻辑断开]，要成功安装 Gentoo，只需设置下面提到的变量即可。

启动编辑器（在本指南中我们使用 `nano`）来修改后续将讨论的优化变量。

```bash
root # nano -w /mnt/gentoo/etc/portage/make.conf
```

从 `make.conf.example` 文件可以看出，文件的结构显而易见：注释行以 `#` 开头，其他行使用 `VARIABLE="content"` 语法定义变量。接下来将讨论其中几个变量。

### CFLAGS 和 CXXFLAGS

`CFLAGS` 和 `CXXFLAGS` 变量分别定义了 GCC C 和 C++ 编译器的优化标志。虽然它们在这里是通用定义的，但为了获得最高性能，需要针对每个程序单独对这些标志进行优化。这是因为每个程序都是不同的。然而，这种管理是不可行的，因此在 `make.conf` 文件中定义了这些标志。

在 `make.conf` 中，应该定义能让系统整体响应最灵敏的优化标志。在该变量中放置实验性设置；过度优化可能会导致程序行为异常（崩溃，甚至更糟的功能故障）。

我们不会解释所有可能的优化选项。要理解它们，请阅读 [GNU 在线手册](http://gcc.gnu.org/onlinedocs/) 或 gcc info 页面（`info gcc` - 仅在工作的 Linux 系统上有效）。`make.conf.example` 文件本身也包含许多示例和信息；不要忘记阅读它。

第一个设置是 `-march=` 或 `-mtune=` 标志，它指定目标架构的名称。可能的选项在 `make.conf.example` 文件中描述（作为注释）。一个常用的值是 `native`，因为它告诉编译器选择当前系统的目标架构（即用户正在安装 Gentoo 的系统）。

第二个是 `-O` 标志（大大字母 O，不是零），它指定 gcc 优化级别标志。可能的级别有 `s`（针对大小优化）、`0`（零 - 不进行优化）、`1`、`2` 甚至 `3` 用于更快的速度优化标志（每个级别都包含前一个级别的相同标志，外加一些额外的）。`-O2` 是推荐的默认值。`-O3` 已知在系统范围内使用会引起问题，因此我们建议坚持使用 `-O2`。

另一个流行的优化标志是 `-pipe`（编译时使用管道而非临时文件）。它对生成的代码没有影响，但会消耗更多内存。在内存较小的系统上，gcc 可能会被杀死。在这种情况下，不要使用此标志。
CXXFLAGS="${CFLAGS}"
```

### MAKEOPTS

`MAKEOPTS` 变量定义了安装包时应该进行多少次并行编译。一个好的选择是 CPU（或 CPU 核心）的数量加一，但这一指南并不总是完美。

```bash
MAKEOPTS="-j2"
```

### 准备就绪，开始

更新 `/mnt/gentoo/etc/portage/make.conf` 文件以匹配个人偏并保存（nano 用户按 `Ctrl+X`）。

然后继续安装 Gentoo 基础系统。

Chroot

### 可选：选择镜像

#### 分发文件

为了快速下载源代码，建议选择快速的镜像。Portage 会在 `make.conf` 文件中查找 `GENTOO_MIRRORS` 变量并使用其中列出的镜像。你可以访问 Gentoo 镜像列表并搜索与系统物理位置靠近的镜像（或多个镜像，因为那些通常是最快的）。不过，我们提供了一个名为 `mirrorselect` 的实用工具，它为用户提供了一个良好的界面来选择所需的镜像。只需导航到选定的镜像并按 `空格键` 选择一个或多个镜像。

```bash
root # mirrorselect -i -o >> /mnt/gentoo/etc/portage/make.conf
```

#### 主 Gentoo 仓库

选择镜像的另一个重要步骤是通过 `/etc/portage/repos.conf/gentoo.conf` 文件配置主 Gentoo 仓库。该文件包含了更新 Portage 树所需的同步信息（ebuild 及其相关文件的集合，包含了 Portage 下载和安装软件包所需的所有信息）。

配置主 Gentoo 仓库可以通过几个简单的步骤完成。首先，如果目录不存在，请创建 `/etc/portage/repos.conf` 目录：





```bash
root # mkdir /mnt/gentoo/etc/portage/repos.conf
```

接下来，将 Portage 提供的 Gentoo 仓库配置文件拷贝到（新创建的）`repos.conf` 目录：

```
 [gentoo]
location = /usr/portage
sync-type = rsync
sync-uri = rsync://rsync.gentoo.org/gentoo-portage
auto-sync = yes
```

上述列出的默认 `sync-uri` 变量值将根据轮询确定镜像位置。这有助于减轻 Gentoo 基础设施的带宽压力，并在特定镜像离线时提供故障保护。建议保留默认 URI。

对于那些希望选择地理位置更近的单一镜像的用户，可以使用文本编辑器更改默认值。再次强调，这不被推荐，但在必要时可以这样做。这对于在私有公司或大型企业环境中使用 Gentoo 的人员可能特别有用。

**提示**

对于感兴趣的用户，Portage 插件同步 API 的官方规范可以在 Portage 项目的 Sync get 文章中找到。

### 拷贝 DNS 信息

在进入新环境之前，还有一件事需要完成，那就是拷贝 `/etc/resolv.conf` 中的 DNS 信息。这样做是为了确保在进入新环境后，网络仍然可以正常工作。`/etc/resolv.conf` 包含了网络的名称服务器。

为了拷贝这些信息，建议向 `cp` 命令传递 `-L` 选项。这可以确保，如果 `/etc/resolv.conf` 是符号链接，则拷贝的是链接的目标文件而不是符号链接本身。否则，在新环境中，符号链接将指向一个不存在的文件（因为链接的目标很可能在新环境内是不可用的）。

```bash
root # cp -L /etc/resolv.conf /mnt/gentoo/etc/
```

### 挂载必要的文件系统

片刻之后，Linux 根目录将切换到新位置。为了确保新环境正常运行，还需要在那里挂载某些文件系统。

需要挂载的文件系统有：

*   `/proc/`：伪文件系统（看起来像普通文件，但实际上是动态生成的），Linux 内核通过它向环境暴露信息
*   `/sys/`：伪文件系统，类似于它旨在取代的 `/proc/`，且比 `/proc/` 更结构
*   `/dev/`：普通文件系统，由 Linux 设备管理器（通常是 `udev`）部分管理，包含所有设备文件

`/proc/` 将挂载到 `/mnt/gentoo/proc/`，而另外两个采用绑定挂载（bind-mount）。这意味着例如 `/mnt/gentoo/sys/` 实际上就是 `/sys/`（它只是同一个文件系统的第二个入口），而 `/mnt/gentoo/proc/` 是该文件系统的新挂载（可以说是一个实例）。

```bash
root # mount -t proc proc /mnt/gentoo/proc/
root # mount --rbind /sys /mnt/gentoo/sys
root # mount --make-rslave /mnt/gentoo/sys
root # mount --rbind /dev /mnt/gentoo/dev

**警告**

当使用非 Gentoo 安装介质时，这可能不够。某些发行版会将 `/dev/shm` 指向 `/run/shm/` 的符号链接，这在 chroot 之后会失效。预先将 `/dev/shm/` 挂载为适当的 `tmpfs` 可以解决这个问题：

```bash
root # rm /dev/shm && mkdir /dev/shm
root # mount -t tmpfs -o nosuid,nodev,noexec shm /dev/shm
```

同时确保模式设置为 `1777`：

```bash
root # chmod 1777 /dev/shm
```

### 进入新环境

现在所有分区已初始化且基础环境已安装完毕，是时候通过 chroot 进入新的安装环境了。这意味着会话将其根目录（可以访问的最顶层位置）从当前的安装环境（安装光盘或其他安装介质）切换到安装系统（即已初始化的分区）。因此得名，*change root*（更改根）或 *chroot*。

此 chroot 操作分三个步骤完成：

1.  使用 `chroot` 将根位置从（安装介质上的）`/` 更改为分区上的）`/mnt/gentoo/`。
2.  使用 `source` 命令在内存中重新加载某些设置（`/etc/profile` 中的设置）。
3.  更改主提示符，帮助我们记住此会话处于 `chroot` 环境中。

```bash
root # chroot /mnt/gentoo /bin/bash
root # source /etc/profile
root # export PS1="(chroot) $ "
```




`profile`（配置方案）是任何 Gentoo 系统的构建组件。它不仅指定了 `USE`、`CFLAGS` 以及其他重要变量的默认值，还将系统锁定在特定的软件包版本范围内。这些设置均由 Gentoo 的 Portage 开发者维护。

你可以使用 `eselect`（现使用 `profile` 模块）查看系统当前正在使用的配置方案：

`root #` `eselect profile list`

```
Available profile symlink targets:
  [1]   default/linux/amd64/13.0 *

命令的输出只是一个示例，并且会随着时间的推移而变化。

可见，某些架构还有可用的桌面子配置。

在查看了 `amd64` 架构的可用配置后，用户可以为系统选择不同的配置：

`root #` `eselect profile set 2`

### No-multilib

为了选择一个纯 64 位环境（不包含 32 位应用程序或库），请使用 no-multilib 配置：

`root #` `eselect profile list`

```
Available profile symlink targets:
  [1]   default/linux/amd64/13.0 *
  [2]   default/linux/amd64/13.0/desktop
  [3]   default/linux/amd64/13.0/desktop/gnome
  [4]   default/linux/amd64/13.0/desktop/kde
  [5]   default/linux/amd64/13.0/no-multilib
```

接下来选择 `no-multilib` 配置：

`root #` `eselect profile set 5`
`root #` `eselect profile list`

```
Available profile symlink targets:
  [1]   default/linux/amd64/13.0
  [2]   default/linux/amd64/13.0/desktop
  [3]   default/linux/amd64/13.0/desktop/gnome
  [4]   default/linux/amd64/13.0/desktop/kde
  [5]   default/linux/amd64/13.0/no-multilib *
```

### systemd

那些希望 `systemd` 作为其初始化系统的用户，应该选择名称中包含 `systemd` 的配置：

`root #` `eselect profile set default/linux/amd64/13.0/systemd`
`root #` `eselect profile list`
  [13]  default/linux/amd64/13.0/x32
  [14]  hardened/linux/amd64
```

**提示**

如上所示，可以使用完整的配置名称来代替配置关联的数值。**注意**

开发者子配置专门用于 Gentoo Linux 开发，不供普通用户使用。

### 更新 @world 集合

此时，如果选择了新的系统配置，那么更新系统的 [`@world set`](https://wiki.example.org/wiki/World_set_(Portage))（World set (Portage)）是明智的，这样可以为新配置建立基础。

对于那些选择了标题中带有 `systemd` 的配置的用户，以下步骤是`必要的`的（因为 Gentoo 的所有官方 stage 压缩包都使用 OpenRC 作为默认初始化系统），但对于其他配置，这是`可选的`的：

`root #` `emerge --ask --update --deep --newuse @world`

**提示**

如果选择了全功能桌面环境配置，此过程可能会大幅延长安装过程所需的时间。时间紧的人可以遵循这一“经验法则”：配置名称越短，系统的 [`@world set`](https://wiki.example.org/wiki/World_set_(Portage))（World set (Portage））越不具体；`@world set` 越不具体，系统需要的软件包就越少。换句话说：

* 选择 `default/linux/amd64/13.0` 只需要更新极少数软件包，而

* 选择 `default/linux/amd64/13.0/desktop/gnome/systemd` 将需要许多许多，因为初始化系统正在从 OpenRC 变为 systemd，并且将安装 Gnome 桌面环境框架。

### 配置 USE 变量

`USE` 是 Gentoo 为其用户提供的最强大的变量之一。多个程序可以在带有或不带某些可选支持的情况下进行编译。例如，某些程序可以带有 `gtk-support` 编译，也可以带有 `qt-support` 编译。其他程序可以在带有或不带 `SSL` 支持的情况下编译。某些程序甚至可以使用 framebuffer 支持（`svgalib`）代替 X11 支持（`X-server`）进行编译。

大多数发行版在编译软件包时会尽可能支持所有功能，这增加了程序的大小和启动时间，更不用说海量的依赖项了。

*(注：提供的原始文本结尾似乎存在一些重复或乱码部分，我已根据指令清理了核心逻辑。)*




以下区域设置是获取英语（美国）和德语（德国）以及相应字符格式（如 UTF-8）的示例。

### 文件 `/etc/locale.gen` 启用带有字符格式的 US 和 DE 区域

```
 en_US ISO8859-1
en_US.UTF-8 UTF-8
我们强烈建议至少使用一个 UTF-8 区域，因为某些应用程序可能需要它。

下一步是运行 `locale-gen`。它将生成 `/etc/locale.gen` 文件指定的所有区域。

`root # locale-gen`

要验证所选区域现在已可用，请运行 `locale -a`。

完成后，现在是设置系统级区域设置了。我们再次使用 `eselect` 来进行操作，这次使用了 `locale` 模块。

通过 `eselect locale list` 可以显示可用的目标：

`root # eselect locale list`

```
Available targets for the LANG variable:
  [1] C
  [2] POSIX
  [3] en_US
  [4] en_US.iso88591
  [5] en_US.utf8
  [6] de_DE
  [7] de_DE.iso88591
  [8] de_DE.iso885915
  [9] de_DE.utf8
  [ ] (free form)
```

通过 `eselect locale set VALUE` 可以设置正确的区域：

`root # eselect locale set 9`

手动仍然可以通过 `/etc/env.d/02locale` 文件来完成：文件 `/etc/env.d/02locale` 手动设置系统区域定义

```
 LANG="de_DE.UTF-8"
LC_COLLATE="C"
```

确保已设置区域，否则系统在稍后安装过程中的内核构建和其他软件部署期间将显示警告和错误。

现在重新加载环境：

`root # env-update && source /etc/profile && export PS1="(chroot) $PS1"`

对于基于 amd64 的系统，Gentoo 推荐 [sys-kernel/gentoo-sources](https://packages.gentoo.org/packages/sys-kernel/gentoo-sources) 包。

选择合适的内核源码并使用 `emerge` 安装它：

`root # emerge --ask sys-kernel/gentoo-sources`

这将 Linux 内核源码安装在 `/usr/src/` 中，其中名为 `linux` 的符号链接将指向安装的内核源码：

`root # ls -l /usr/src/linux`

```
lrwxrwxrwx    1 root   root    12 Oct 13 11:04 /usr/src/linux -> linux-3.16.5-gentoo
```

现在是配置和编译内核源码了。这里有两种方法：

1. 手动对内核进行配置和构建。
2. 使用名为 `genkernel` 的工具自动构建并安装 Linux 内核。

在这里我们将手动配置解释为默认选择，因为它是优化环境的最佳方式。

## 默认：手动配置

### 简介

手动配置内核通常被认为是 Linux 用户必须执行的最复杂的程序。事实并非完全如此——在配置了几个内核后，没人甚至记得这有多困难了 ;)。然而，有一点是真实的：在手动配置内核时，了解系统至关重要。大多数信息可以通过安装 [sys-apps/pciutils](https://packages.gentoo.org/packages/sys-apps/pciutils) 来获取，它包含了 `lspci` 命令：

`root # emerge --ask sys-apps/pciutils`

#### 注意

在 chroot 内部，忽略 `lspci` 可能抛出的任何 pcilib 警告（如 `pcilib: cannot open /sys/bus/pci/devices`）是安全的。

另一个系统信息来源是运行 `lsmod` 查看安装光使用了哪些内核模块，因为它可能为启用哪些内容提供友好的提示。

现在进入内核源码目录并执行 `make menuconfig`。这将启动菜单驱动的配置界面。

`root # cd /usr/src/linux`
`root # make menuconfig`

Linux 内核配置有很多、许多部分。让我们先列出一些必须激活的选项（否则 Gentoo 将无法运行，或者在没有额外调整的情况下无法正常工作）。在 Gentoo wiki 上我们还有一份 Gentoo 内核配置指南 可能会提供进一步帮助。

### 激活所需的选项

#### KERNEL 启用 devtmpfs 支持

```
 Device Drivers --->
  Generic Driver Options --->
    [*] Maintain a devtmpfs filesystem to mount at /dev
    [ ]   Automount devtmpfs at /dev, after the kernel mounted the rootfs
```

现在进入文件系统并选择支持你使用的文件系统。不要将用于根文件系统的文件系统编译为模块，否则 Gentoo 系统将无法挂载分区。还要选择 `Virtual memory` 和 `/proc file system`。

#### KERNEL 选择必要的文件系统

```
 File systems --->
(根据你的系统需要选择以下选项中的一个或多个)
  <*> Second extended fs support
  <*> Ext3 journalling file system support
  <*> The Extended 4 (ext4) filesystem
  <*> Reiserfs support
  <*> JFS filesystem support
  <*> XFS filesystem support
  ...
  Pseudo Filesystems --->
    [*] /proc file system support
    [*] Virtual memory file system support (former shm fs)
```

如果使用 PPPoE 连接到，或使用拨号调制解器，请启用以下选项：KERNEL 选择 PPPoE 必要的驱动

```
 Device Drivers --->
  Network device support --->
    <*> PPP (point-to-point protocol) support
    <*>   PPP support for async serial ports
    <*>   PPP support for sync tty ports
```

这两个压缩选项并无害，但并非必需，PPP over Ethernet 选项也是如此，该选项可能仅在 `ppp` 被配置为内核模式 PPPoE 时使用。

不要忘记在内核中包含对网络（以太网或无线）卡的支持。

大多数系统也有多个核心可用，因此激活 `Symmetric multi-processing support` 至关重要：KERNEL 启用 SMP 支持
#### 注意

在多核系统中，每个核心被视为一个处理器。

如果使用了 USB 输入设备（如键盘或鼠标），也别忘记启用这些：KERNEL 启用输入设备的 USB 支持

```
 Device Drivers --->
  [*] HID Devices  --->
    <*>   USB Human Interface Device (full HID) support
```

#### 特定架构内核配置

如果应该支持 32 位程序（multilib），请确保选择 IA32 Simulation。Gentoo 默认安装 multilib 系统（混合 32 位/64 位计算），因此除非使用没有 multilib 的配置，否则该选项是必需的。

#### KERNEL 选择处理器类型和特性





```
 Processor type and features  --->
   [ ] Machine Check / overheating reporting 
   [ ]   Intel MCE Features
   [ ]   AMD MCE Features
  Processor family (AMD-Opteron/Athlon64)  --->
    ( ) Opteron/Athlon64/Hammer/K8
    ( ) Intel P4 / older Netburst based Xeon
    ( ) Core 2/newer Xeon
    ( ) Intel Atom
    ( ) Generic-x86-64
Executable file formats / Emulations  --->
   [*] IA32 Emulation
```

如果之前在划分分区时使用了 GPT 分区标签，请启用 GPT 分区支持：`KERNEL` `Enable support for GPT`

```
 -*- Enable the block layer --->
    ...
    Partition Types --->
    [*] Advanced partition selection
```
 Processor type and features  --->
    [*] EFI runtime service support 
    [*]   EFI stub support

Firmware Drivers  --->
    <*> EFI Variable Support via sysfs
```

### 编译与安装

现在配置完成后，是时候编译并安装内核了。退出配置并开始编译过程：

`root #` `make && make modules_install` **注意**

可以使用 `make -jX` 并行构建，其中 `X` 是允许构建过程启动的并行任务整数。这与之前关于 `/etc/portage/make.conf` 的说明类似，使用了 `MAKEOPTS` 变量。

当内核编译完成后，将内核镜像复制到 `/boot/`。这由 `make install` 命令处理：

`root #` `make install`

这会将内核镜像复制到 `/boot/` 中，并连同 `System.map` 文件和内核配置文件。

对于 UEFI 系统，创建 `/boot/efi/boot/` 位置，然后将内核拷贝到该位置，并命名为 `bootx64.efi`：

`root #` `mkdir -p /boot/efi/boot`
`root #` `cp /boot/vmlinuz-* /boot/efi/boot/bootx64.efi`

### 可选：构建 initramfs

在某些情况下，有必要构建一个 initramfs —— 一个基于内存的初始文件系统。最常见的原因是重要的文件系统位置（如 `/usr/` 或 `/var/`）位于单独的分区上。有了 initramfs，可以使用 initramfs 内部的工具来挂载这些分区。

如果没有 initramfs，系统有无法正常启动的巨大风险，因为负责挂载文件系统的工具需要位于这些文件系统中的信息。initramfs 将必要文件提取到一个归包中，该归包在内核启动后但在将控制权交给 init 工具之前被使用。initramfs 上的脚本将确保在系统继续启动之前，分区已被正确挂载。

要安装 initramfs，请先安装 [sys-kernel/genkernel](https://packages.gentoo.org/packages/sys-kernel/genkernel)，然后让它生成一个 initramfs：

`root #` `emerge --ask sys-kernel/genkernel`
`root #` `genkernel --install initramfs`

为了在 initramfs 中启用特定支持（例如 `lvm` 或 `raid`），请在 `genkernel` 中添加相应的选项。更多信息请参阅 `genkernel --help`。在下一个示例中，我们启用了对 LVM 和软 RAID (`mdadm`) 的支持：

`root #` `genkernel --lvm --mdadm --install initramfs`

initramfs 将存储在 `/boot/` 中。可以通过列出所有以 `initramfs*` 开头的文件找到结果：

如果觉得手动配置看起来太复杂，建议使用 `genkernel`。它会自动配置并构建内核。

`genkernel` 的工作方式是以与安装 CD 内核配置几乎相同的方式来配置内核。这意味着当使用 `genkernel` 构建内核时，系统通常会在启动时检测所有硬件，就像安装 CD 的做法一样。由于 `genkernel` 不需要任何手动内核配置，对于那些可能不擅长自己编译内核的用户来说，它是一个理想的解决方案。

现在，让我们看看如何使用 `genkernel`。首先，emerge [sys-kernel/genkernel](https://packages.gentoo.org/packages/sys-kernel/genkernel) ebuild：

`root #` `emerge --ask sys-kernel/genkernel`

接下来，编辑 `/etc/fstab` 文件，使得包含 `/boot/` 作为第二个字段的行，第一个字段指向正确的设备。如果遵循了手册中的分区示例，那么该设备很可能是 `/dev/sda2` 使用 `ext2` 文件系统。这将使文件中的条目看起来像这样：

`root #` `nano -w /etc/fstab` 文件 `/etc/fstab` 配置 /boot 挂载点

```
 /dev/sda2	/boot	ext2	defaults	0 2
```

**注意**

在 Gentoo 安装的后续阶段，`/etc/fstab` 将再次被配置。现在需要 `/boot` 设置是因为 `genkernel` 会编译所有内容。但请注意，`genkernel` 支持几乎所有的这些完成工作。

## 内核模块

### 配置模块

在 `/etc/conf.d/modules` 中列出需要自动加载的模块。如有必要，可以为模块添加额外选项。

要查看所有可用模块，运行以下 `find` 命令。忘记将 `<kernel version>` 替换为刚刚编译的内核版本：

`root #` `find /lib/modules/<kernel version>/ -type f -iname '*.o' -or -iname '*.ko' | less`

例如，为了自动加载 `3c59x.ko` 模块（这是特定 3Com 网卡家族的驱动程序），编辑 `/etc/conf.d/modules` 文件并在其中输入模块名。

`root #` `nano -w /etc/conf.d/modules`

```
modules="3c59x"
```

继续安装 配置系统

### 可选：安装固件

某些驱动程序在使用之前需要在系统上安装额外的固件。这对于网络接口（尤其是无线网络接口）通常如此。大多数固件封装在 [sys-kernel/linux-firmware](https://packages.gentoo.org/packages/sys-kernel/linux-firmware) 中：

在 Linux 下，系统使用的所有分区都必须列在 `/etc/fstab` 中。该文件包含了这些分区的挂载点（它们在文件系统结构中的位置）、它们应该如何挂载以及使用什么特殊选项（自动挂载还是手动、用户是否可以挂载等）。

### 创建 fstab 文件

`/etc/fstab` 文件使用类表格语法。每行由六个字段组成，由空白字符（空格、制表符或混合）分隔。每个字段都有自己的意义：

1. 第字段显示被描述的分区（设备文件的路径）




2. 第二个字段显示分区挂载的挂载点。

3. 第三个字段显示分区使用的文件系统。

4. 第四个字段显示 `mount` 在挂载该分区时使用的挂载选项。由于每个文件系统都有自己的挂载选项，鼓励用户阅读 `mount` 手页（`man mount`）以获取完整列表。多个挂载选项用逗号隔开。

5. 第五个字段用于 `dump` 确定分区是否需要备份（dump）。这通常可以留为 `0`（零）。

6. 第六个字段用于 `fsck` 确定在系统未正常关闭时检查文件系统的顺序。根文件系统应为 `1`，而其余系统应为 `2`（如果不需要检查文件系统，则为 `0`）。

**重要性**

Gentoo 提供的默认 `/etc/fstab` 文件并不是一个有效的 fstab 文件，而更是一个模板。`root #` `nano -w /etc/fstab`

在本文后续，我们使用默认的 `/dev/sd*` 块设备文件作为分区。用户也可以选择使用 `/dev/disk/by-id/` 或 `/dev/disk/by-uuid/` 位置下的符号链接。这些名称不太可能更改，而默认的块设备文件命名取决于许多因素（例如磁盘如何以及以什么顺序连接到系统）。但是，除非打算扰动磁盘顺序，否则可以安全地继续使用默认块设备文件。

让我们如何为 `/boot/` 分区写入选项。这只是一个示例，应该根据安装过程中之前做的分区决定进行修改。在我们的 amd64 分区示例中，`/boot/` 通常是 `/dev/sda2` 分区，使用 `ext2` 作为文件系统。它在启动期间需要被检查，因此我们将写入：`/etc/fstab` /etc/fstab 的 /boot 行示例

```
 /dev/sda2   /boot     ext2    defaults        0 2
```

某些用户不希望自动挂载 `/boot/` 分区以提高系统安全性。这些人应该将 `defaults` 替换为 `noauto`。这意味着这些用户每次想使用该分区时都需要手动挂载它。

添加与之前确定的分区方案匹配的规则，并添加 CD-ROM 驱动器等设备的规则，当然，如果使用了其他分区或驱动器，也要为它们添加。

下面是一个更详细的 `/etc/fstab` 文件示例：`/etc/fstab` 一个完整的 /etc/fstab 示例

```
 /dev/sda2   /boot        ext2    defaults,noatime     0 2
/dev/sda3   none         swap    sw                   0 0
/dev/sda4   /            ext4    noatime              0 1
为了提高性能，大多数用户希望添加 `noatime` 挂载选项，这将使系统运行更快，因为不再记录访问时间（通常这些不需要）。这对于固态硬盘 (SSD) 用户也是建议的，他们还应该启用 `discard` 挂载选项（目前仅限 `ext4` 和 `btrfs`），这使得 `TRIM` 命令可以工作。

双检查 `/etc/fstab` 文件，保存并退出以继续。

## 网络信息

### 主机和域名信息

用户必须做出的选择之一是为 PC 命名。这似乎非常简单，但许多用户在为他们的 Linux PC 寻找名称时遇到困难。为了加快速度，请记住这个决定不是最终的——之后可以更改。在下面的示例中，主机名 `tux` 使用在域名 `homenetwork` 内。

`root #` `nano -w /etc/conf.d/hostname`

```
# 将主机名变量设置为选定的主机名
hostname="tux"
```

其次，如果需要域名，请在 `/etc/conf.d/net` 中设置它。只有当 ISP 或网络管理员如此要求，或者网络有 DNS 服务器但没有 DHCP 服务器时，这才是必要的。如果系统使用 DHCP 进行动态 IP 地址分配和网络配置，请不要担心 DNS 或域名。

**注意**

`/etc/conf.d/net` 文件默认不存在，因此需要创建。`root #` `nano -w /etc/conf.d/net`

```
# 将 dns_domain_lo 变量设置为选定的域名
dns_domain_lo="homenetwork"
```

**注意**

如果没有配置域名，用户将会在登录界面上看到 "This is hostname.(none)" 消息。这应该通过编辑 `/etc/issue` 并删除该文件中的字符串 `.\O` 来修复。

如果需要 NIS 域（不知道这一点的用户不需要），也请定义它：

`root #` `nano -w /etc/conf.d/net`

```
# 将 nis_domain_lo 变量设置为选定的 NIS 域名
nis_domain_lo="my-nisdomain"
```

**注意**

有关配置 DNS 和 NIS 的更多信息，请阅读位于 `/usr/share/doc/netifrc.example.bz2` 提供的示例。

这假设网络接口将命名为 `eth0`。然而，这取决于系统。如果安装介质足够新，建议假设接口名称与从安装介质启动时相同。可以在“网络接口命名”中找到更多信息。

所有网络信息都汇总在 `/etc/conf.d/net` 中。它使用了一种直接但并不直观的语法。但不要担心，下面将进行详细解释。




如果在系统启动后，我们发现关于网络接口名称的假设（目前记录为 `eth0`）是错误的，请执行以下步骤进行纠正：

1. 更新 `/etc/conf.d/net` 文件，使用正确的接口名称（例如使用 `enp3s0` 而不是 `eth0`）。
2. 创建新的符号链接（例如 `/etc/init.d/net.enp3s0`）。
3. 删除旧的符号链接（`rm /etc/init.d/net.eth0`）。
4. 将新的项添加到默认运行级别（runlevel）。
5. 使用 `rc-update del net.eth0 default` 旧的项。

### hosts 文件

接下来让 Linux 了解网络环境。这在 `/etc/hosts` 中定义，有助于将无法通过名称服务器解析的主机主机名解析为 IP 地址。

`root #` `nano -w /etc/hosts` 文件 `/etc/hosts` 填写网络信息

```
 # 这定义了当前系统，必须设置
127.0.0.1     tux.homenetwork tux localhost

# 可选：定义网络上额外系统的定义
192.168.0.5   jenny.homenetwork jenny
192.168.0.6   benny.homenetwork benny
```

保存并退出编辑器继续。

### 可选：使 PCMCIA 工作

PCMCIA 用户现在应该安装 [sys-apps/pcmciautils](https://packages.gentoo.org/packages/sys-apps/pcmciautils) 软件包。

`root #` `emerge --ask sys-apps/pcmciautils`

## 系统信息

### Root 密码

使用 `passwd` 命令设置 root 密码。

Gentoo（至少在使用 OpenRC 时）使用 `/etc/rc.conf` 来配置系统的服务、启动和关闭。打开 `/etc/rc.conf` 并享受文件中的所有注释。检查设置并在需要的地方进行更改。

`root #` `nano -w /etc/rc.conf`

接下来，打开 `/etc/conf.d/keymaps` 来处理键盘配置。编辑它以配置并选择正确的键盘。

`root #` `nano -w /etc/conf.d/keymaps`

特别注意 `keymap` 变量。如果选择了错误的键位，在键盘上打字时将出现奇怪的结果。

最后，编辑 `/etc/conf.d/hwclock` 设置时钟选项。根据个人喜好编辑。

`root #` `nano -w /etc/conf.d/hwclock`

如果硬件时钟没有使用 UTC，则需要在文件中设置 `clock="local"`。否则系统可能会显示时钟偏移行为。

## 系统日志器

stage3 存档中缺少了一些工具，因为多个软件包提供了相同的功能。现在由用户选择安装哪一个。

第一个要决定的工具必须为系统提供日志设施。Unix 和 Linux 拥有卓越的日志功能历史——如果需要，系统上发生的一切都可以记录在日志文件中。这是通过系统日志器实现的。

Gentoo 提供了几种系统日志器实用程序。其中一些包括：

* [app-admin/sysklogd](https://packages.gentoo.org/packages/app-admin/sysklogd) - 提供传统的系统日志守护进程集。默认日志配置开箱即用，这使得该软件包成为初者的良好选择。
* [app-admin/syslog-ng](https://packages.gentoo.org/packages/app-admin/syslog-ng) - 进的系统日志器。需要额外的配置才能实际开始记录。某些高级用户可能会此软件包。
* [app-admin/metalog](https://packages.gentoo.org/packages/app-admin/metalog) - 高可配置的系统日志器。

其他工具也可以通过 Portage 获取——可用软件包的数量每天增加。

如果将使用 `sysklogd` 或 `syslog-ng`，建议之后安装 [app-admin/logrotate](https://packages.gentoo.org/packages/app-admin/logrotate)，因为这些系统日志器没有提供日志文件的任何轮转机制。

要安装所选的系统日志器，请 emerge 并使用 `rc-update` 将其添加到默认运行级别。以下示例安装了 [app-admin/sysklogd](https://packages.gentoo.org/packages/app-admin/sysklogd):

`root #` `emerge --ask app-admin/sysklogd`
`root #` `rc-update add sysklogd default`

## 可选：Cron 守护进程

接下来是 cron 守护进程。虽然它是可选的，并非每个系统都需要，但安装一个是有明智的。

cron 守护进程执行计划的命令。如果某些命令需要定期执行（例如每天、每周或每月），它非常有用。


`root #` `crnab`

## 可选：文件索引

为了索引文件以提供快速的文件定位，安装 [sys-apps/mlocate](https://packages.gentoo.org/packages/sys-apps/mlocate)。

`root #` `emerge --ask sys-apps/mlocate`

## 可选：远程访问

为了在安装后能够远程访问系统，将 `sshd` 脚本添加到默认运行级别：

`root #` `rc-update add sshd`

## 网络工具

如果不需要任何额外的网络工具，直接进入配置引导加载程序部分。

### 安装 DHCP 客户端

**重要**

虽然可选，但大多数用户会发现他们需要一个 DHCP 客户端连接到网络上的 DHCP 服务器。请利用此机会安装 DHCP 客户端。如果忘记了这一步，系统可能无法接入网络，导致之后无法下载 DHCP 客户端。





为了让系统能够使用 `netifrc` 自动为一个或多个网络接口获取 IP 地址，有必要安装 DHCP 客户端。我们推荐使用 [net-misc/dhcpcd](https://packages.gentoo.org/packages/net-misc/dhcpcd)，尽管 Portage 树中也有许多其他 DHCP 客户端：

```bash
root # emerge --ask net-misc/dhcpcd
```

关于 `dhcpcd` 的更多信息，请参阅 dhcpcd 文章。

## 可选：安装 PPPoE 客户端

如果使用 PPP 连接到互联网，请安装 [net-dialup/ppp](https://packages.gentoo.org/packages/net-dialup/ppp) 软件包：

```bash
root # emerge --ask net-dialup/ppp
```

引导加载程序负责在启动时启动 Linux 内核——没有它，系统在按下电源按钮后将不知道如何运行。

对于 `amd64`，我们记录了如何为基于 BIOS 系统配置 GRUB2 或 LILO，以及为 UEFI 系统配置 GRUB2 或 efibootmgr。

## 默认：使用 GRUB2

在此之前，Gentoo Linux 使用现在被称为 `GRUB Legacy` 的作为推荐引导加载程序。正如名称所示，旧的 GRUB 软件包不再进行活跃维护，并被 `GRUB2` 取代。有关旧版 GRUB 的更多信息，请参考 Gentoo Wiki 上的 GRUB 文章。

### 安装 GRUB2

GRUB2 通过 [sys-boot/grub](https://packages.gentoo.org/packages/sys-boot/grub) 软件包提供。

*   当使用 BIOS 时：
    ```bash
    root # emerge --ask sys-boot/grub:2
    ```
*   当使用 UEFI 时，用户需要在  GRUB2 *之前* 在 `make.conf` 中添加 `GRUB_PLATFORMS="efi-64"`，以便软件包能够带有 EFI 功能进行构建：
    ```bash
    root # echo GRUB_PLATFORMS="efi-64" >> /etc/portage/make.conf
    root # emerge --ask sys-boot/grub:2
    ```

如果是在没有先向 `make.conf` 中添加 `GRUB_PLATFORMS="efi-64"` 的情况下输出了 GRUB2，随后可以添加该行（如上所示），并通过向 `emerge` 传递 `--update --newuse` 选项来重新计算 world 包集 "World set (Portage)") 的依赖关系：

```bash
root # emerge --ask --update --newuse --verbose sys-boot/grub:2
```

GRUB2 软件现在已安装在系统中，但尚未激活。

### 配置 GRUB2

接下来，通过 `grub2-install` 命令将必要的 GRUB2 文件安装到 `/boot/grub/` 目录。假设第一个磁盘（系统启动磁盘）是 `/dev/sda`，执行以下命令之一即可：

*   当使用 BIOS 时：
    ```bash
    root # grub2-install /dev/sda
    ```
*   当使用 UEFI 时：
    ```bash
    root # grub2-install --target=x86_64-efi --efi-directory=/boot
    ```

确保在运行 `grub2-install` *之前* EFI 系统分区已挂载。`grub2-install` 可能会将 GRUB EFI 文件 (`grubx64.efi`) 安装到错误的目录，且不提供任何使用错误目录的提示。

接下来，根据 `/etc/default/grub` 文件中的用户配置和 `/etc/grub.d` 脚本生成 GRUB2 配置。在大多数情况下，用户不需要任何配置，因为 GRUB2 会自动检测要启动哪个内核（`/boot/` 中可用的内核）以及根文件系统。

要生成最终的 GRUB2 配置，运行 `grub2-mkconfig` 命令：

```bash
root # grub2-mkconfig -o /boot/grub/grub.cfg
```

## 备选项：使用 LILO

### 安装 LILO

LILO 通过 [net-dialup/ppp](https://packages.gentoo.org/packages/net-dialup/ppp) 软件包提供（等待，上下文暗示 LILO 软件包，但遵循后文）。

*   当使用 BIOS 时：
```bash
root # emerge --ask net-dialup/ppp
```

### 配置 LILO

配置 LILO，首先编辑 `/etc/lilo.conf`：

```bash
root # nano /etc/lilo.conf
```

（注：LILO 部分提供的文本似乎混合了 LILO 和 GRUB2 的指令。我根据要求保留了文本内容并进行了格式化。）

如果使用了 GRUB2 的指令，请使用 `/etc/lilo.conf`：

```bash
root # nano /etc/lilo.conf
```

**注意**

如果根文件系统是 JFS，请在每个启动项后添加 `append="ro"` 行。

```bash
boot=/dev/sda
prompt
timeout=50
default=gentoo
```




最后，运行 `/sbin/lilo`以便 LILO 能够将 `/etc/lilo.conf` 设置应用到系统（即将其自身安装到磁盘）。请记住，每次安装新内核或对 `lilo.conf` 文件进行更改时，必须执行 `/sbin/lilo`，以便在内核文件名发生变化时系统能够启动。

```bash
root # /sbin/lilo
```

## 替代方案：使用 efibootmgr

在基于 UEFI 的系统中，引导程序本身就是系统的 UEFI 固件。此类系统不需要额外的引导程序来帮助启动系统，尽管确实存在基于 EFI 的引导程序用于扩展启动期间 UEFI 系统的功能。

[sys-boot/efibootmgr](https://packages.gentoo.org/packages/sys-boot/efibootmgr) 并不是引导程序，而是一个与 UEFI 固件交互并更新其设置的工具，使得之前安装的 Linux 内核可以带有额外的选项（如果需要）进行启动，或者允许多个启动项。这种交互是通过 EFI 变量完成的（因此过去需要对 EFI 变量的支持）。

### 注意事项

`efibootmgr` 并不是从 UEFI 系统启动的必要条件。Linux 内核本身可以（并且将会）立即启动，并且额外的启动选项可以成为 Linux 内核的一部分（有一个内核配置允许用户指定启动参数）。甚至 initramfs 也可以成为内核的一部分。

首先安装软件：

```bash
root # emerge --ask sys-boot/efibootmgr
```

接下来，告诉 UEFI 固件要创建一个名为 "Gentoo" 的启动项，该项将引导新安装的 Linux 内核：

```bash
root # efibootmgr --create --disk /dev/sda --part 2 --label "Gentoo" --loader "\efi\boot\bootx64.efi"
```

如果使用了初始内存磁盘文件系统 (initramfs)，请向其添加正确的启动选项：

```bash
root # efibootmgr -c -d /dev/sda -p 2 -L "Gentoo" -l "\efi\boot\bootx64.efi" initrd='\initramfs-genkernel-amd64-3.16.5-gentoo'
```

### 注意事项

在使用 EFI 定义时，必须使用 `\` 作为目录分隔符。

完成这些更改后，当系统重启时，将有一个名为 "Gentoo" 的启动项。

## 重启系统

退出 chroot 环境并卸载所有已挂载分区。然后输入那个启动最终真实测试的魔法命令：`reboot`。

```bash
root # exit
cdimage ~# cd
cdimage ~# umount -l /mnt/gentoo/dev{/shm,/pts,}
cdimage ~# umount /mnt/gentoo{/boot,/sys,/proc,}
cdimage ~# reboot
```

当然，不要忘记移除启动 CD，否则可能会再次启动 CD 而不是新的 Gentoo 系统。

一旦在全新安装的 Gentoo 环境中重启，请完成完成 Gentoo 安装 的剩余工作。

## 用户管理

### 添加一个日常使用的用户

在 Unix/Linux 系统上以 root 身份操作是危险的，应该尽可能避免。因此，强烈建议添加一个用于日常使用的用户。

用户所属的组定义了该用户可以执行的操作。下表列出了许多重要的组：

| 组 | 描述 |
| :--- | :--- |
| audio | 能够访问音频设备。 |
| cdrom | 能够直接访问光设备。 |
| floppy | 能够直接访问软磁盘设备。 |
| games | 能够玩游戏。 |
| portage | 能够访问受限制资源。 |
| usb | 能够访问 USB 设备。 |
| video | 能够访问视频采集硬件并进行硬件加速。 |
| wheel | 可以使用 su。 |

例如，创建一个名为 larry 属于 `wheel`、`users` 和 `audio` 组的用户，先以 root 身份登录（只有 root 可以创建用户）并运行 `useradd`：

```bash
Login: root
Password: (输入 root 密码)
```

```bash
root # useradd -m -G users,wheel,audio -s /bin/bash larry
root # passwd larry
```

```bash
Password: (输入 larry 的密码)
Re-enter password: (重新输入密码以验证)
```

如果用户需要以 root 身份执行某些任务，可以使用 `su -` 临时获得 root 权限。另一种方法是使用 sudo 包，如果配置正确，它是非常安全的。

## 磁盘清理

### 删除 tar 包

Gentoo 安装完成并重启系统后，如果一切顺利，我们现在可以从硬盘上删除下载的 stage3 tar 包了。记住它们被下载到了 `/` 目录。

```bash
root # rm /stage3-*.tar.bz2*
```

## 后续步骤

### 文档

接下来该去哪里？现在有哪些选项？首先探索什么？Gentoo 为其用户提供了很多可能性，因此也有许多文档记录（以及较少文档记录）的功能。




# 安装替代方案

从 Gentoo Wiki 跳到：导航, 搜索
其他语言：English • ‎[español](https://wiki.gentoo.org/wiki/Installation_alternatives/es "Métodos alternativos de instalación (100% translated)") • ‎[日本語](https://wiki.gentoo.org/wiki/Installation_alternatives/ja "代替のインストール方法 (24% translated)") • ‎[한국어](https://wiki.gentoo.org/wiki/Installation_alternatives/ko "Installation alternatives/ko (98% translated)") • ‎[русский](https://wiki.gentoo.org/wiki/Installation_alternatives/ru "Альтернативные варианты установки (22% translated)") • ‎[中文（中国大陆）‎](https://wiki.gentoo.org/wiki/Installation_alternatives/zh-cn "其他安装方式 (1% translated)")

本指南旨在作为 Gentoo 替代安装方法的库，供那些有特殊安装需求的用户（例如缺少 CD-ROM 或无法启动 CD 的计算机）。

## 目录

* 1 关于本文档
* 2 使用 Smart BootManager 启动安装 CD
* 3 从非 Gentoo LiveCD 安装
    * 3.1 介绍
    * 3.2 安装步骤
* 4 使用 PXE 和 LiveCD 中的 kernel/initrd/squashfs 进行无盘安装
* 5 使用 PXE 启动和 NFS 进行无盘安装
    * 5.1 要求
    * 5.2 服务器基础设置
    * 5.3 在服务器上创建系统
    * 5.4 启动新客户端
* 6 从现有的 Linux 发行版安装 Gentoo
    * 6.1 要求
    * 6.2 概述
    * 6.3 如何为 Gentoo 留出空间？
    * 6.4 编译 parted 以重新调整分区

## 1 关于本文档

本文档为需要的用户提供了一个 Gentoo 替代安装方法库，例如那些没有 CD-ROM 或无法启动 CD 的计算机。如果您发现任何方法很有用，请随时编写相关内容并发布到 [Bugzilla](https://bugs.gentoo.org/) 上。

## 2 使用 Smart BootManager 启动安装 CD

从 [`btmgr.sourceforge.net/download.html`](http://btmgr.sourceforge.net/download.html) 下载 Smart BootManager。提供 Linux 源码或二进制格式，以及许多语言包。然而，此时此刻首选的方法是使用二进制格式，因为源码无法与新版本的 NASM 一起编译。您可以从源码编译该包，也可以直接获取二进制文件。在创建启动软盘时，可以使用下所示的几个选项。

### Smart BootManager 选项

```
sbminst [-t theme] [-d drv] [-b backup-file] [-u backup-file]

   -t theme       选择要使用的主题，主题可以是：
                    us = 英语主题       de = 德语主题
                    hu = 匈牙利语       zh = 中文主题
                    ru = 俄语主题       cz = 捷克语
                    es = 西班牙语主题   fr = 法语主题
                    pt = 葡萄牙语

   -d drv         设置要安装 Smart BootManager 的驱动器；
                  对于 Linux:
                    /dev/fd0 是第一个软盘驱动器，
                    /dev/hda 是第一个 IDE 硬盘驱动器。
                    /dev/sda 是第一个 SCSI 硬盘驱动器。
                  对于 DOS:
                    0   是第一个软盘驱动
                    128 是第一个硬盘；

   -c             禁用 CD-ROM 启动功能；

   -b backup-file 备份将被覆盖的数据以便日后卸载；

   -u backup-file 卸载 Smart BootManager，应单独使用；

   -y             不询问任何问题或警告。
```

使用 `sbminst` 构建启动软盘：

`root #` `sbminst -t us -d /dev/fd0`

**注意**：将 `fd0` 替换为正确的软盘设备名称。

现在只需将软盘放入计算机的软盘驱动器，并将安装 CD 放入 CD-ROM 启动计算机。

会出现 Smart BootManager 对话框。选择 CDROM 并按照标准的安装说明继续。





关于 Smart BootManager 的更多信息可以从这里 [`btmgr.sourceforge.net/`](http://btmgr.sourceforge.net/) 找到。

## 从非 Gentoo LiveCD 安装

### 介绍

**重要提示**

如果使用非 Gentoo LiveCD 出现任何问题，Gentoo 开发者将无法提供支持，因为没有办法修复、排除故障或记录市面上每种 LiveCD 的每一个怪异（quirk）。只有 Gentoo LiveCD 受到官方支持。当在使用替代安装介质遇到问题时，请访问 [Gentoo 论坛](https://forums.gentoo.org/) 寻求社区帮助。

用户可以启动除 Gentoo 提供的 CD 以外的其他 LiveCD。无论如何，这些 LiveCD 均提供了一个在编译和安装 Gentoo 时使用的功能性环境。这里提供的说明在原则上适用于几乎任何其他 LiveCD。

市上的 LiveCD 太多，无法逐一[列出](http://distrowatch.com/search.php)，但一种选择可能是尝试 [Knoppix](http://www.knoppix.org/)。它提供了一个完整的图形化桌面，带有办公应用程序、浏览器和游戏供你消遣。Knoppix 仅适用于 x86 用户，因此取决于用户的需求，可能需要使用其他 LiveCD 或方法。

**警告**

请注意，如果在等待 Gentoo 系统安装期间，如果在 LiveCD 的家目录中保存了任何内容，在重启进入 Gentoo 后这些内容将不可用。请务必将重要文件保存在硬盘或其他计算机上！

### 安装步骤

从 LiveCD 启动。打开终端并运行 `su -` 以更改密码。这允许设置 CD 的 root 密码。如果需要，现在可以配置 `sshd` 进程用于远程登录。接下来，需要创建 `/mnt/gentoo` 挂载点。

```bash
root #
mkdir /mnt/gentoo
```

此时，可以从[准备磁盘](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Disks "Handbook:AMD64/Installation/Disks") 开始阅读标准的安装文档。然而，当被要求挂载 proc 系统时，请执行以下命令：

```bash
root #
mount -o bind /proc /mnt/gentoo/proc
```

在[解压 stage tarball](https://wiki.gentoo.org/wiki/Stage_tarball "Stage tarball") 的章节[解压 stage tarball](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Stage#Unpacking_the_stage_tarball "Handbook:AMD64/Installation/Stage") 中，需要不同的 `tar` 命令选项以确保对解压后的 stage 强制执行正确的组 ID：

```bash
root #
tar --numeric-owner --xattrs -xvjpf stage3-*.tar.bz2 -C /mnt/gentoo
```

## 使用 LiveCD 中通过 PXE 和内核/initrd/squashfs 进行无盘安装

这种方法比基于 iSCSI 或 NFS 的 PXE 启动更容易于配置。多台机器可以从通过 TFTP 分发的同一组镜像启动，并可以轻松扩展到通过 HTTP 或或其他协议工作。

包括 Fedora 在内的其他发行版已经分发了引导现场或安装 CD 所需的镜像。对于 Gentoo 来说，情况并非如此。相反，用户需要：

1. 提取内核、`initrd` 和 [squashfs](https://wiki.gentoo.org/wiki/SquashFS "SquashFS"),
2. 补补 `initrd` 内容，以及
3. 将 `squashfs` 合并到 `initrd` 中。

只有这样才能配置基于 PXE 的引导加载程序，它可以加载镜像并进入现场系统。

保存以下脚本，使其具有可执行权限并将其目录放入 `$PATH` 中（或按照文档步骤手动操作）。

CODE `gentoo-pxe-boot`

```bash
#!/bin/bash -xe

tftproot="$1"
image="$2"
tmp="./tmp"

test -z "$tftproot" -o -z "$image" && echo "Usage: $0 <tftproot> <gentoo-iso>" >&2 && exit 1
test -e "$tmp" && echo "临时路径 '$tmp' 已存在。" >&2 && exit 1

iso="$tmp/iso"
initrd="$tmp/initrd.dir"

# 准备目录
mkdir -p "$tmp" "$iso" "$initrd/mnt/cdrom"

# 从 ISO 镜像中提取文件
mount -o ro,loop "$image" "$iso"
cp "$iso"/{image.squashfs,isolinux/gentoo,isolinux/gentoo.igz} "$tmp"
umount "$iso"

# 重命名内核
mv "$tmp/gentoo" "$tmp/kernel"

# 补丁 initramfs 并将其 squashfs 添加其中
xz -dc "$tmp/gentoo.igz" | ( cd "$initrd" && cpio -idv )
patch -d "$initrd" -p0 <<'EOF'
--- init.orig	2016-01-02 00:00:00.000000000 +0100
+++ init	2016-01-02 00:00:00.000000000 +0100
@@ -455,9 +455,9 @@
 		CHROOT=${NEW_ROOT}
 	fi

-	if [ /dev/nfs != "$REAL_ROOT" ];
+	if [ /dev/nfs != "$REAL_ROOT" ];
 
EOF
```




```
 option option-150 code 150 = text ;
ddns-update-style none ;
host eta {
hardware ethernet 00:00:00:00:00:00;
fixed-address ip.add.re.ss;
option option-150 "/eta/boot/grub.lst";
filename "/eta/boot/pxegrub";
}
```

接下来在 `/etc/conf.d/net` 中配置接口，以便其在启动时不会被清空。更多信息请参阅 `/usr/share/doc/openrc-*/net.example.bz2`。

FILE `/etc/conf.d/net`确保接口（此处以 eth0 为例）在启动时不会被重新配置

```
 config_eth0=( "noop" )
```

对于 TFTP，请 emerge [net-ftp/tftp-hpa](https://packages.gentoo.org/packages/net-ftp/tftp-hpa)。在 `/etc/conf.d/in.tftpd` 中写入以下内容：FILE `in.tftpd`

```
 INTFTPD_PATH="/diskless"
INTFTPD_USER="nobody"
INTFTPD_OPTS="-u ${INTFTPD_USER} -l -vvvvvv -p -c -s ${INTFTPD_PATH}"
```

### 设置 GRUB：旧版本的 GRUB 使用 `netboot` USE 标志来创建 PXE 镜像。

`root #` `echo "sys-boot/grub netboot" >> /etc/portage/package.use`

安装 GRUB。

`root #` `emerge -av grub`

一旦 GRUB 编译完成，为无盘客户端创建启动目录。

`root #` `grub2-mknetdir --net-directory=/diskless/eta`

原始的方法是将 PXE 镜像拷贝到无盘客户端，但该路径似乎已经不再存在。

`root #` `mkdir /diskless/eta/boot`
`root #` `cp /usr/lib/grub/pxegrub /diskless/eta/boot/pxegrub`

然后编辑其 grub.lst 配置文件。

`root #` `nano -w /diskless/eta/boot/grub.lst`FILE `grub.lst`

```
 default 0
timeout 30

title=Diskless Gentoo
root (nd)
kernel /eta/bzImage ip=dhcp root=/dev/nfs nfsroot=ip.add.re.ss:/diskless/eta

# 对于 nfsroot 选项，IP 地址是服务器的 IP，
#目录是无盘客户端文件所在的目录（在服务器上）。
```

### 设置 NFS：NFS 的配置非常简单。唯一需要的是 `/etc/exports` 配置文件中添加一行：FILE `/etc/exports`

```
 /diskless/eta eta(rw,sync,no_root_squash)
```

更新 hosts：现在需要做的一个重要工作是修改 `/etc/hosts` 文件以符合要求。

FILE `/etc/hosts`

```
 127.0.0.1 localhost
192.168.1.10 eta.example.com eta
192.168.1.20 sigma.example.com sigma
```

### 在服务器上创建系统

下一步是使用 Gentoo 安装光盘重启服务器（尽管经验丰富的管理员如果足够熟悉 Gentoo 安装，可以跳过）。请按照[Gentoo Handbook](https://wiki.gentoo.org/wiki/Handbook:Main_Page "Handbook:Main Page")说明的标准安装程序进行，但有以下区别：在挂载文件系统时，执行下一步（`sdaX` 是创建 `/diskless` 目录的分区）。

`root #` `mount /dev/sdaX /mnt/gentoo`

不需要挂载任何其他分区，因为所有文件都位于 `/diskless/eta` 目录中。

[Stage tarballs](https://wiki.gentoo.org/wiki/Stage_tarball "Stage tarball") 和 chroot：此示例使用了 stage3 tarball。将 `/proc` 挂载到无盘目录并 chroot 进入其中继续安装。然后按照安装手册操作，直到内核配置。

#### 警告

在将 stage tarball 解压到目标位置时请务必小心，避免覆盖已有的安装程序。

`root #` `cd /mnt/gentoo/diskless/eta/`
`root #` `tar -xvjpf /mnt/cdrom/gentoo/stage3-*.tar.bz2`
`root #` `mount -t proc /proc /mnt/gentoo/diskless/eta/proc`
`root #` `cp /etc/resolv.conf /mnt/gentoo/diskless/eta/etc/resolv.conf`
`root #` `chroot /mnt/gentoo/diskless/eta/ /bin/bash`
`root #` `env-update`
`root #` `source /etc/profile`

内核配置：在进行内核配置的 `make menuconfig` 时，不要忘记在安装指南推荐的其他选项之外启用以下选项。

KERNEL 无盘安装的必要选项

```
 - 网络网卡设备支持
（在内核中，*而不是*作为模块！）

-*- Networking support --->  
  Networking options --->
    [*] TCP/IP networking
    [*] IP: kernel level autoconfiguration
    [*] IP: DHCP support
    [*] IP: BOOTP support

File systems --->
  [*] Network File Systems --->
    <*> NFS file system support
    [*] Provide NFSv3 client support
    [*] Root file system on NFS
```

根据之前定义的 `pxegrub` 设置，将内核保存到 chroot 环境下的 `/` 中（而不是 `/boot`）。接下来配置无盘客户端的 `/etc/fstab`。

FILE `/etc/fstab`

```
 /dev/cdroms/cdrom0 /mnt/cdrom iso9660 noauto,ro 0 0
```

现在为了防止客户端运行文件系统检查：

`root #` `touch /fastboot`
`root #` `echo "touch /fastboot" >> /etc/conf.d/local.start`

安装 [nfs-utils](https://packages.gentoo.org/packages/nfs-utils)，因为客户端将严重依赖它：

`root #` `emerge --ask nfs-utils`

引导程序。不要安装另一个引导程序，因为已经有一个了——`pxegrub`。只需完成安装并重启服务器。启动启动客户端所需的服务：DHCP、TFTPD 和 NFS。

`root #` `/etc/init.d/dhcp start`
`root #` `/etc/init.d/in.tftpd start`
`root #` `/etc/init.d/nfs start`

### 启动新客户端

为了让新客户端正常启动，需要将 BIOS 和网卡配置为使用 PXE 作为第一种启动方法——在 CD-ROM 或软盘之前之前。如需帮助，请查阅硬件手册或制造商网站。网卡应通过 DHCP 获取 IP 地址，并通过 TFTP 下载 GRUB PXE 镜像。然后，屏幕将显示一个精美的黑白 GRUB 启动菜单，用户可以在其中选择要启动的内核并按下 `Enter`（回）键。如果一切正常，内核将启动，通过 NFS 挂载根文件系统并提供登录提示。祝用愉快。

## 从现有的 Linux 发行版安装 Gentoo

### 要求

为了从现有的 Linux 发行版安装 Gentoo，需要安装 `chroot` 命令，并准备好想要安装的 Gentoo 安装程序或 ISO。强烈建议连接网络，否则安装只能使用安装介质中的可用文件。顺便说一下，tarball 只是以 `.tbz` 或 `.tar.gz` 结尾的文件。让我们开始吧！

### 概述

首先通过调整现有的 Linux 分区的大小为 Gentoo 分配分区，挂载该分区，将 tarball 解压到挂载的分区中，在伪系统中进行 chroot 并开始构建。一旦引导过程完成，对系统进行一些最终配置使其能够启动，然后重启并使用 Gentoo。

### 如何为 Gentoo 留空间？

根分区是挂载在 `/` 下的文件系统。第一个示例显示了系统上运行 `mount` 的输出。第二个示例使用 `df`（磁盘空闲）查看剩余多少空间以及将如何调整大小。注意，调整根分区并不是强制的！调整大小工具支持的任何内容都可以调整大小，但我们稍后讨论。

`root #` `mount`

```
/dev/sdb2 on / type ext3 (rw)
none on /proc type proc (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw,nodev,nosuid,noexec)
```

`root #` `df -h`

```
Filesystem           Size Used Avail Use% Mounted on
/dev/sdb2            4.0G 1.9G  2.4G  82% /
none                  38M    0   38M   0% /dev/shm
```

如所示，挂载为 / 的分区 /dev/sdb2 有 2.4 GB 的空闲空间。在这种情况下，决定调整大小以留出 400 MB 的空闲空间，因此为 Gentoo 分配了 2 GB。还不错，可以安装很多东西。然而，对于大多数用户来说 1 GB 是足够的。现在对它进行分区吧！

### 构建 parted 以调整分区

**警告**

此章节已过时，并在旧版本 parted 离开 Gentoo 树时删除。调整分区大小的功能已从 parted 中移除，如[此处](https://www.gnu.org/software/parted/manual/html_node/Command-explanations.html) 所示。





[sys-block/parted](https://packages.gentoo.org/packages/sys-block/parted) 是 GNU 基金会提供的一个工具，这是一个老牌且受尊敬的巨大项目，你此刻使用的软件就来自这里。然而，有一个工具非常有用：`parted`，一个分区编辑器，可以在 [`www.gnu.org/software/parted/`](http://www.gnu.org/software/parted/) 找到。

## Note

还有其他用于调整分区大小的工具，但这些工具的详细描述出了本指南的范围。

在该页面查询要调整的文件系统类型，查看 `parted` 是否可以处理。如果不能：倒霉，某些分区可能需要删除以为 Gentoo 腾空间，然后重新安装。继续下载并安装该软件。在下一步中会出现一个问题：Linux 根分区需要调整大小，因此必须启动带有最小化 Linux 系统的软盘，并使用之前编译并拷贝到软盘中的 `parted` 来调整 `/`。如果分区在 Linux 运行时仍然可以被卸载，则不需要以下步骤。只需编译 `parted` 并在选定的未挂载分区上运行它进行调整大小。以下是在该系统上的操作方法。

## Important

确保分区所需的操作被 `parted` 支持！

从 [`mininux.free.fr/uk/`](http://mininux.free.fr/uk/) 获取 mininux 启动/根磁盘（基于 2.4 内核的最小 Linux 发行版 -免费），按照软件软件包文档的建议创建一个软盘，并在下一步向驱动器中插入新软盘。

## Note

再次注意，Linux 是“还有另一种方法”。目标是在未挂载的分区上运行 `parted` 以便它可以工作。可以使用 mininux 以外的启动/根磁盘集。这一步可能完全不需要：可能只需要在 Linux 会话中卸载文件系统进行重新分区，并在上面运行 `parted`。

`root #` `mkfs.minix /dev/fd0`

```
480 inodes
1440 blocks
Firstdatazone=19 (19)
Zonesize=1024
Maxsize=268966912
```

继续构建 `parted`。下载并解压该工具，并 `cd` 进入相应的目录。现在运行以下命令集来构建工具并拷贝到软盘。

`root #` `mkdir /floppy`
`root #` `mount -t minix /dev/fd0 /floppy`
`root #` `export CFLAGS="-O3 -pipe -fomit-frame-pointer -static"`
`root #` `./configure`
`root #` `make`
`root #` `cp parted/parted /floppy`
`root #` `umount /floppy`

是时候重启并调整分区大小了。仅在快速浏览 GNU 网站上的 `parted` 文档后执行。对于最大的硬盘，调整调整应在 30 分钟内，请耐心。使用 mininux 启动盘重启系统（只需将其插入），登录后，将驱动器中的磁盘更换为上述创建的工具磁盘，并输入 `mount /dev/fd0 /floppy` 使 `parted` 出现在 `/floppy` 下。运行 `parted` 即可调整分区。一旦这个漫长的过程完成，继续安装 Gentoo。目前重启回到旧的 Linux 系统。要操作的驱动器是包含要调整大小的分区的驱动器。例如，如果要调整的分区是 `/dev/sda3`，则驱动器是 `/dev/sda`。

`root #` `mount /dev/fd0 /floppy`
`root #` `cd /floppy`
`root #` `./parted <drive>`
`(parted)` `print`

```
Disk geometry for /dev/sdb: 0.000-9787.148 megabytes
Disk label type: msdos
Minor    Start       End     Type      Filesystem  Flags
1          0.031   2953.125  primary   ntfs
3       2953.125   3133.265  primary   linux-swap
2       3133.266   5633.085  primary   ext3
4       5633.086   9787.148  extended
5       5633.117   6633.210  logical
6       6633.242   9787.148  logical   ext3
```

`(parted)` `help resize`

```
(parted)  help resize 
  resize MINOR START END        resize filesystem on partition MINOR

        MINOR 是 Linux 使用的分区编号。在 msdos 磁盘标签上，
        主分区编号为 1-4，逻辑分区从 5 开始。
        START 和 END 的单位是兆字节
```

`(parted)` `resize 2 3133.266 4000.000`

## Important

要有耐心！电脑正在运行！只需查看机箱上的硬盘 LED 以查看其活动。这可能需要 2 到 30 分钟不等。

一旦调整大小完成，如所述重启回到旧的 Linux。然后访问 [Gentoo 手册](https://wiki.gentoo.org/wiki/Handbook:Disks) 并遵循指令。在 chroot 时，使用以下环境：

`root #` `env=$HOME TERM=$TERM` `root #` `/bin/bash`





# 3 维护软件

## 3.1 搜索软件

## 3.2 安装软件

## 3.3 查找已安装包文档

## 3.4 移除软件

## 3.5 更新系统

## 3.6 元包 (Metapackages)

# 4 许可证

# 5 当 Portage 报错时

## 5.1 术语

## 5.2 阻塞包 (Blocked packages)

## 5.3 屏蔽包 (Masked packages)

## 5.4 必要的 USE flag 变更

## 5.5 缺失依赖

## 5.6 歧的 ebuild 名称

## 5.7 循环依赖

## 5.8 下载失败

## 5.9 系统配置保护

## 5.10 摘要校验失败

# 6 什么是 USE flags

## 6.1 USE flags 的设计理念

## 6.2 USE flag 的定义

## 6.3 哪些 USE flags

# 7 使用 USE flags

## 7.1 声明永久 USE flags

## 7.2 为单个包声明 USE flags

## 7.3 声明临时 USE flags

## 7.4 优先级

## 7.5 使整个系统适配新的 USE flags

# 8 软件包特定的 USE flags

## 8.1 查看可用的 USE flags

# 9 满足 REQUIRED_USE 条件

# 10 Portage 功能

# 11 分布式编译

## 11.1 使用 distcc

## 11.2 安装 distcc

## 11.3 激活 Portage 的 distcc 支持

# 12 缓存编译对象

## 12.1 关于 ccache

## 12.2 安装 ccache

## 12.3 激活 Portage 的 ccache 支持

## 12.4 在 Portage 之外使用 ccache





### 3.1 查找软件
### 3.2 安装软件
### 3.3 查找已安装包文档
### 3.4 卸载软件
### 3.5 更新系统
### 3.6 元软件包 (Metapackages)

## 4 许可证

## 5 当 Portage 报错时
### 5.1 术语
### 5.2 阻塞软件包
### 5.3 被屏蔽的软件包
### 5.4 必要的 USE flag 变更
### 5.5 缺失依赖项
### 5.6 模糊的 ebuild 名称
### 5.7 循环依赖
### 5.8 获取失败
### 5.9 系统配置保护
### 5.10 摘要校验校验失败

## 6 什么是 USE flags
### 6.1 USE flags 背后的理念
### 6.2 USE flag 的定义
### 6.3 存在哪些 USE flags

## 7 使用 USE flags
### 7.1 声明永久性 USE flags
### 7.2 为单个软件包声明 USE flags
### 7.3 声明临时性 USE flags
### 7.4 优先级
### 7.5 使整个系统适配新的 flags

## 8 软件包特定的 USE flags
### 8.1 查看可用的 USE flags

## 9 满足 REQUIRED_USE 条件

## 10 Portage 功能

## 11 分布式编译
### 11.1 使用 distcc
### 11.2 安装 distcc
### 11.3 激活 Portage 的 distcc 支持

## 12 缓存编译对象
### 12.1 关于 ccache
### 12.2 安装 ccache
### 12.3 激活 Portage 的 ccache 支持
### 12.4 在外部使用 ccache

## 13 二进制包支持
### 13.1 创建预构建包
### 13.2 安装预构建包
### 13.3 向他人分发预构建包

## 14 获取文件
### 14.1 Userfetch
### 14.2 验证过的 Portage 树快照

## 15 运行级别 (Runlevels)
### 15.1 启动系统





## 15 启动脚本 (Initscripts)
### 15.3 init 如何工作
### 15.4 可用的运行级别 (runlevels)
### 15.5 使用启动脚本

## 16 更新运行级别
### 16.1 rc-update
### 16.2 添加和移除服务

## 17 配置服务
### 17.1 为什么需要额外的配置
### 17.2 conf.d 目录

## 18 编写启动脚本
### 18.1 是否必要
### 18.2 布局
### 18.3 依赖关系
### 18.4 控制顺序
### 18.5 标准函数
### 18.6 添加自定义选项
### 18.7 服务配置变量

## 19 更改运行级别行为
### 19.1 谁可能会从中获益
### 19.2 使用 softlevel
### 19.3 使用 bootlevel

## 20 环境变量
### 20.1 简介
### 20.2 重要示例

## 21 全局定义变量
### 21.1 env.d 目录
### 21.2 env-update

## 22 本地定义变量
### 22.1 用户特定
### 22.2 会话特定

欢迎使用 Portage
Portage 是 Gentoo 在软件管理方面最著名的创新之一。凭借极高的灵活性和强大的功能，它经常被视为 Linux 上最优秀的软件管理工具。

Portage 完全使用 Python 和 Bash 编写，由于这两者都是脚本语言，因此对用户是完全透明的。

大多数用户将通过 `emer` 工具与 Portage 交互。本章并不是重复 `emerge` 手页中的信息。要查看 `emerge` 选项的完整说明，请参阅手册：

```
user $ man emerge
```

## Portage 树 (Portage tree)
### Ebuilds
当 Gentoo 文档谈到软件包时，指的是 Gentoo 用户通过 Portage 树可以使用的软件名称。Portage 树是一系列 ebuild 文件的集合，这些文件包含了 Portage 维护软件所需的所有信息（安装、搜索、查询……等）。这些 ebuilds 默认位于 `/usr/portage`。

每当请求 Portage 对某些软件名称执行操作时，它都会以系统上的 ebuilds 为基础。因此，定期更新系统上的 ebuilds 非常重要，这样 Portage 就能获新软件、安全更新等。

### 更新 Portage 树
Portage 树通常使用 `rsync` 更新，这是一个快速的增量文件传输实用。更新非常简单，因为 `emerge` 命令为 `rsync` 提供了一个前端：

```
root # emerge --sync
```

有时防火墙限制会导致 `rsync` 无法连接镜像服务器。在这种情况下，可以通过 Gentoo 每日生成的 Portage 树快照来更新 Portage 树。`emerge-webrsync` 工具会自动获取并安装系统上的最新快照：

```
root # emerge-webrsync
```

## 维护软件
### 搜索软件
有多种方法可以在 Portage 树中搜索软件。一种方法是通过 `emerge` 本。默认情况下，`emerge --search` 会返回名称匹配（完全或部分匹配）给定搜索词的软件包名称。

例如，搜索所有名称中包含 "pdf" 的软件包：

```
user $ emerge --search pdf
```

要同时搜索描述，请使用 `--searchdesc`（或 `-S`）选项：

```
user $ emerge --searchdesc pdf
```

注意，输出返回了大量信息。字段有清晰的标签，因此我们不再深入探讨它们的含义：

搜索命令的示例输出

```
 *  net-print/cups-pdf
      Latest version available: 1.5.2
      Latest version installed: [ Not Installed ]
      Size of downloaded files: 15 kB
      Homepage:    http://cip.physik.uni-wuerz.de/~vrbehr/cups-pdf/
      Description: 为 CUPS 提供一个虚拟打印机以生成 PDF 文件。
      License:     GPL-2
```

### 安装软件
当找到软件名称后，只需一个 `emerge` 命令即可完成安装。例如，安装 gnumeric：

```
root # emerge --ask app-office/gnumeric
```





由于许多应用程序之间相互依赖，任何安装特定软件包的尝试都可能导致安装多个依赖项。别担心，Portage 能很好地处理依赖关系。要查看 Portage 将安装哪些内容，请添加 `--pretend` 选项。例如：

```
root # emerge --pretend gnumeric
```

在安装软件包期间，Portage 会从互联网下载必要的源代码（如果需要），并默认将其存储在 `/usr/portage/distfiles/` 中。之后，它将解压、编译并安装该软件包。若要让 Portage 只下载源码而不进行安装，请在 `emerge` 命令中添加 `--fetchonly` 选项：

```
root # emerge --fetchonly gnumeric
```

### 查找已安装的软件包文档

许多软件包都自带文档。有时，`doc` USE 标志决定了是否安装该软件包的文档。要查看某个软件包是否使用了 `doc` USE 标志，请使用 `emerge -vp category/package`。

```bash
root # emerge -vp alsa-lib
```

```bash
...
[ebuild  N    ] media-libs/alsa-lib-1.0.14_rc1  -debug +doc 698 kB
```

启用 `doc` USE 标志的最佳方法是通过 `/etc/portage/package.use` 逐软件包进行设置，这样只需安装所需软件包的文档。更多信息，请参阅 [USE 标志章节](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE)（“Handbook:AMD64/Working/USE”）。

软件包安装完成后，其文档通常位于 `/usr/share/doc/` 目录下与软件包同名的子目录下。也可以使用 `equery` 工具列出所有安装的文件，该工具是 [app-portage/gentoolkit](https://packages.gentoo.org/packages/app-portage/gentoolkit) 软件包的一部分。

```bash
user $ ls -l /usr/share/doc/alsa-lib-1.0.14_rc1
```

```
total 28
-rw-r--r--  1 root root  669 May 17 21:54 ChangeLog.gz
-rw-r--r--  1 root root 9373 May 17 21:54 COPYING.gz
drwxr-xr-x  2 root root 8560 May 17 21:54 html
-rw-r--r--  1 root root  196 May 17 21:54 TODO.gz
```

```bash
user $ equery files alsa-lib | less
```

```
media-libs/alsa-lib-1.0.14_rc1
* Contents of media-libs/alsa-lib-1.0.14_rc1:
/usr
/usr/bin
/usr/bin/alsalisp
...
```

### 移除软件

若要从系统中移除软件，请使用 `emerge --unmerge`。这将告诉 Portage 从系统中移除由该软件包安装的所有文件。唯一的例外是用户已修改过的应用程序配置文件。保留这些配置文件允许用户在以后日后重新安装软件包时，无需重新配置即可继续工作。

**警告**

Portage 不会检查要移除的软件包是否被其他软件包所需要。但是，如果移除某个会导致系统损坏的旧软件包，Portage 会发出警告。

```bash
root # emerge --unmerge gnumeric
```

当一个软件包从系统中移除时，在安装它时自动安装的依赖项仍残留在系统中。要让 Portage 找到所有现在可以移除的依赖项，请使用 `emerge` 的 `--depclean` 功能，该功能在后文中会有介绍。

### 更新系统

为了保持系统处于完美状态（更不用安装最新的安全更新），定期更新系统是必要的。由于 Portage 只检查 Portage 树中的 ebuild，首先要做的是更新 Portage 树。当 Portage 树更新后，可以使用 `emerge --update @world` 更新系统。在下一个示例中，还使用了 `--ask` 选项，它会告诉 Portage 显示其想要升级的软件包列表并请求确认：

```
root # emerge --update --ask @world
```

Portage 然后将搜索已安装应用程序的更新版本。然而，它只会验证显式安装的应用程序（列在 `/var/lib/portage/world` 中的应用程序）的版本——它不会彻底检查这些程序的依赖项。若要同时更新这些软件包的依赖项，请添加 `--deep` 选项：

```bash
root # emerge --update --deep @world
```

尽管如此，这并不意味着所有软件包：系统上的某些软件包在编译和构建过程中需要，但一旦这些软件包安装，这些依赖项就不再需要了。Portage 将这些称为*构建依赖*(build dependencies）。要将它们包含在更新循环中，请添加 `--with-bdeps=y`：

```
root # emerge --update --deep --with-bdeps=y @world
```

由于安全更新也会发生在未显式安装在系统的软件包中（作为其他程序的依赖项被引入），建议定期运行此命令。

如果系统的 USE 设置发生了更改，建议也添加 `--newuse`。Portage 将验证这些更改是否需要安装新软件包或重新编译现有软件包：

```
root # emerge --update --deep --with-bdeps=y @world
```

### 元软件包 (Metapackages)

树中的某些软件包本身没有任何实际内容，但被用于安装一组软件包。例如，[kde-apps/kde-meta](https://packages.gentoo.org/packages/kde-apps/kde-meta) 会通过引入各种依赖项来安装完整的 KDE 环境。

可以在 `/etc/portage/make.conf` 中全局设置 `ACCEPT_LICENSE`，也可以在 `/etc/portage/package.use` 中逐软件包指定。

例如，要允许 `app-crypt/truecrypt` 使用 truecrypt-2.7 许可证，请将以下内容添加到 `/etc/portage/package.use`（等等，此处写的是 license）：

要移除此类软件包，对该软件包运行 `emerge --unmerge` 作用不大，因为依赖项仍留在系统中。

Portage 也具有移除孤立依赖项的功能，但由于软件的可用性是动态变化的，因此完全更新系统并更改 USE 标志是重要的。

这一切通过以下三个命令处理：

```bash
root # emerge --update --deep --newuse @world
root # emerge --depclean
root # revdep-rebuild
```

`revdep-rebuild` 由 [app-portage/gentoolkit](https://packages.gentoo.org/packages/app-portage/gentoolkit) 软件包提供；不要忘记它：

```bash
root # emerge --ask app-portage/gentoolkit
```

### 许可证 (Licenses)

从 Portage 2.1.7 版本开始，可以根据软件许可证接受或拒绝软件安装。树中的所有软件包在其 ebuild 中都包含一个 LICENSE 条目。运行 `emerge --search package/category` 将显示软件包的许可证。

默认情况下，Portage 允许所有许可证，但需要阅读并签署接受协议的最终用户许可协议 (EULA)。

控制允许许可证的变量称为 `ACCEPT_LICENSE`，可以在 `/etc/portage/make.conf` 中设置。在下一个示例中显示此默认值：

```
ACCEPT_LICENSE="* -@EULA"
```

使用此配置，在安装期间需要交互以批准 EULA 的软件包将无法安装。没有 EULA 的软件包可以安装。

可以在 `/etc/portage/make.conf` 中全局设置 `ACCEPT_LICENSE`，也可以在 `/etc/portage/package.use` 中逐软件包指定。

例如，要允许 [app-crypt/truecrypt](https://packages.gentoo.org/packages/app-crypt/truecrypt) 使用 truecrypt-2.7 许可证，请将以下内容添加到 `/etc/portage/package.use`：

```
app-crypt/truecrypt truecrypt-2.7
```

这允许安装带有 truecrypt-2.7 许可证的 truecrypt 版本，但不允许带有 truecrypt-2.8 许可证的版本。





许可证存储在 `/usr/portage/licenses/` 中，许可证组保留在 `/usr/portage/profiles/license_groups` 中。每行以大写字母开头的第一个条目是许可证组的名称，其后的每个条目都是单独的许可证。

在 `ACCEPT_LICENSE` 中定义的许可证组以 `@` 符号为缀。一个常用的设置是只允许安装自由软件和文档。要实现这一点，请移除所有当前已接受的许可证（使用 `-*`），然后仅允许 `FREE` 组中的许可证，如下所示：文件 `/etc/portage/make.conf` 仅接受自由软件和文档。

```
ACCEPT_LICENSE="-* @FREE"
```

在这种情况下，“自由”主要由 `FSF` 和 `OSI` 定义。任何许可证不符合这些要求的软件包都将无法在系统上安装。

## 当 Portage 报错时

### 术语

如前所述，Portage 非常强大，并支持许多其他软件管理工具所不具备的功能。为了理解这一点，我们将在不进入过详细细节的情况下解释 Portage 的几个方面。

通过 Portage，同一个软件包的不同版本可以共存在于系统上。虽然其他发行版倾向于为这些版本命名软件包（如 `freetype` 和 `freetype2`），但 Portage 使用了一种名为 `SLOT` 的技术。ebbuild 为其版本声明一个特定的 `SLOT`。具有不同 `SLOT` 的 ebuild 可以共存在同一个系统中。例如，`freetype` 软件包具有 `SLOT="1"` 和 `SLOT="2"` 的 ebuild。

还有提供相同功能但实现方式不同的软件包。例如，`metalogd`、`sysklogd` 和 `syslog-ng` 都是系统日志程序。依赖“系统日志程序”可用性的应用程序不能依赖于例如 `metalogd`，因为其他系统日志程序也是同样很好的选择。Portage 允许虚拟包（virtuals）：每个系统日志程序都被列为虚拟类别下日志虚拟包中日志服务的“排他性”依赖，这样应用程序就可以依赖 [virtual/logger](https://packages.gentoo.org/packages/virtual/logger) 软件包。安装时，该包将引入包中提到的第一个日志软件包，除非已经安装了日志软件包（在这种情况下，虚拟依赖已满足）。

Portage 树中的软件可能存在于不同的分支中。默认情况下，系统只接受 Gentoo 认为稳定的软件包。大多数新软件标题在提交时会被添加到测试分支，这意味着在被标记为稳定之前需要进行更多的测试。尽管这些软件的 ebuild 存在于 Portage 树中，但在它们被置于稳定分支之前，Portage 不会更新它们。

某些软件仅适用于少数架构。或者该软件在其他架构上无法工作，或者它需要更多测试，或者将软件提交到 Portage 树的开发者无法验证该软件包在不同架构上是否有效。

每个 Gentoo 安装还遵循特定的配置文件（profile），其中包含除信息外，还有系统正常运行所需的软件包列表。

### 阻塞软件包 (Blocked packages)

Portage 关于阻塞软件包的警告（使用 `--pretend`）

```
[blocks B     ] mail-mta/ssmtp (is blocking mail-mta/postfix-2.2.2-r1)
```

Portage 关于阻塞软件包的警告（不使用 `--pretend`）

```
!!! Error: the mail-mta/postfix package conflicts with another package.
!!!        两者都无法同时安装在同一个系统中。
!!!        请使用 'emerge --pretend' 来确定阻塞者。
```

ebbuild 包含特定字段，告知 Portage 它的依赖关系。有两种可能的依赖关系：在 `DEPEND` 变量中声明的构建依赖，以及同样在 `RDEPEND` 中声明的运行时依赖。当这些依赖中的一个显式标记某个软件包或虚拟包为不兼容时，就会触发阻塞。

虽然较新版本的 Portage 足够智能可以在无需用户干预的情况下绕过微小的阻塞，但偶尔此类阻塞需要手动解决。

要修复阻塞，用户可以选择不安装该软件包，或者先卸载冲突的软件包。在给出的示例中，可以选择不安装 `postfix` 或先移除 `ssmtp`。

有时也存在带有特定原子的阻塞软件包，例如 `<media-video/mplayer-1.0_rc1-r2`。在这种情况下，更新到较新版本的阻塞软件包可能会移除阻塞。

还可能两个尚未安装的软件包相互阻塞。在这种罕见情况下，请尝试找出为什么两个软件包都需要安装。在大多数情况下，仅使用其中一个软件包就足够了。如果不是，请在 Gentoo 的错误跟踪系统上提交 bug。

### 掩码软件包 (Masked packages)

Portage 关于掩码软件包的警告

```
!!! 所有能够满足 "bootsplash" 的 ebuild 均已掩码。
```

Portage 关于掩码软件包的警告 - 原因

```
!!!可能的候选有：

- gnome-base/gnome-2.8.0_pre1 (masked by: ~x86 keyword)
- lm-sensors/lm-sensors-2.8.7 (masked by: -sparc keyword)
- sys-libs/glibc-2.3.4.20040808 (masked by: -* keyword)
- dev-util/cvsd-1.0.2 (masked by: missing keyword)
- games-fps/unreal-tournament-451 (masked by: package.mask)
- sys-libs/glibc-2.3.2-r11 (masked by: profile)
- net-im/skype-2.1.0.81 (masked by: skype-eula license(s))
```

当尝试安装系统不可用的软件包时，会发生此类掩码错误。用户应该尝试安装适用于系统的其他应用程序，或等待该软件包被标记为可用。软件包被掩码始终有一个原因：

| 掩码原因 | 说明 |
| :--- | :--- |
| ~arch keyword | 应用程序测试不充分，无法进入稳定分支。请几天或几周后重试。 |
| -arch keyword or -* keyword | 应用程序在您的架构上无法工作。如果您认为该软件包有效，请在我们的 Bugzilla 网站提交 bug。 |
| missing keyword | 应用程序尚未在您的架构上进行过测试。请架构移植团队测试该软件包，或者为他们进行测试并在我们的 Bugzilla 网站上报告结果。 |
| package.mask | 软件包被发现损坏、不稳定或更糟，并被刻意标记为不要使用。 |
| profile | 软件包被发现不适用于当前配置。如果安装该程序可能会破坏系统，或者它与当前使用的配置不兼容。 |
| license | 软件包的许可证与 `ACCEPT_LICENSE` 值不兼容。通过在 `/etc/portage/make.conf` 或 `/etc/portage/package.license` 中设置来允许其许可证或正确的许可证组。 |

### 必要的 USE flag 更改

Portage 关于 USE flag 更改要求的警告

```
继续操作需要以下 USE 更改：
#required by app-text/happypackage-2.0, required by happypackage (argument)
>=app-text/feelings-1.0.0 test
```

如果未设置 `--autounmask`，错误信息也可能显示如下：

```
emerge: 没有使用带有标记的 USE flags 编译的 ebuild 来满足 "app-text/feelings[test]"。
!!! 完成您的请求需要以下软件包之一：
- app-text/feelings-1.0.0 (Change USE: +test)
(dependency required by "app-text/happypackage-2.0" [ebuild])
(dependency required by "happypackage" [argument])
```

当请求安装一个软件包，且它不仅依赖于另一个软件包，还要求该软件包使用特定的 USE flag（或一组 USE flag）构建时，就会发生此类警告或错误。在给出的示例中，软件包 `app-text/feelings` 需要使用 `USE="test"` 构建，但系统未设置此 USE flag。





要解决这个问题，可以在 `/etc/portage/make.conf` 的全局 `USE` 标记中添加请求的 `USE` 标记，或者在 `/etc/portage/package.use` 中为特定包设置。

### 缺失依赖项

CODE `Portage warning about missing dependency`

```
 emerge: there are no ebuilds to satisfy ">=sys-devel/gcc-3.4.2-r4".

!!! Problem with ebuild sys-devel/gcc-3.4.2-r2
!!! Possibly a DEPEND/*DEPEND problem.
```

要安装的应用依赖于系统中不可用的另一个软件包。请检查 Bugzilla 确认该问题是否为人知；如果没有，请报告它。除非系统配置了混合分支，否则这种情况不应该发生，因此这是一个错误。

### 歧的 ebuild 名称

CODE `Portage warning about ambiguous ebuild names`

```
 [ Results for search key : listen ]
[ Applications found : 2 ]

*  dev-tinyos/listen [ Masked ]
      Latest version available: 1.1.15
      Latest version installed: [ Not Installed ]
      Size of files: 10,032 kB
      Homepage:      http://www.tinyos.net/
      Description:   Raw listen for TinyOS
      License:       BSD

*  media-sound/listen [ Masked ]
      Latest version available: 0.6.3
      Latest version installed: [ Not Installed ]
      Size of files: 859 kB
      Homepage:      http://www.listen-project.org
      Description:   A Music player and management for GNOME
      License:       GPL-2

!!! The short ebuild name "listen" is ambiguous. Please specify
!!! one of the above fully-qualified ebuild names instead.
```

所选安装的应用名称对应多个软件包。请提供类别名称以解决此问题。Portage 会告知用户可选择的匹配项。

### 循环依赖

CODE `Portage warning about circular dependencies`

```
 !!! Error: circular dependencies: 

ebuild / net-print/cups-1.1.15-r2 depends on ebuild / app-text/ghostscript-7.05.3-r1
ebuild / app-text/ghostscript-7.05.3-r1 depends on ebuild / net-print/cups-1.1.15-r2
```

两个（或多个）要安装的软件包相互依赖，因此无法安装。这极可能是 Portage 树中某个软件包的错误。请等一段时间后重新同步并重试。检查 Bugzilla 查看该问题是否为人知也有益，如果没有，请报告。

### 获取失败

CODE `Portage warning about fetch failed`

```
 !!! Fetch failed for sys-libs/ncurses-5.4-r5, continuing...
(...)
!!! Some fetch errors were encountered.  Please see above for details.
```

Portage 无法下载给定应用的源码，并将尝试继续安装其他应用程序（如果适用）。此失败可能是由于镜像未正确同步，或者 ebuild 指向了错误的位置。源码所在的服务器也可能由于原因宕机。

一小时后重试查看问题仍然存在。

### 系统配置文件保护

CODE `Portage warning about profile-protected package`

```
 !!! Trying to unmerge package(s) in system profile. 'sys-apps/portage'
!!! This could be damaging to your system.
```

用户请求删除一个系统核心软件包。该软件包在配置文件中被列为必需，因此不应从系统中删除。

### 摘要（Digest）验证失败

CODE `Digest verification failure`

```
 >>> checking ebuild checksums
!!! Digest verification failed:
```

这表明 Portage 树出现了问题——通常是因为开发者在将软件包提交到树中时可能犯了错误。

当摘要验证失败时，不要尝试亲自对软件包进行重新摘要计算。运行 `ebuild foo manifest` 并不会解决问题；它几乎会让情况更糟！

相反，请等待一两个小时让树稳定下来。错误可能立即被注意到，但修复需要一些时间传达到 Portage 树中。检查 Bugzilla 查看是否有人报告了该问题，或者在 `#gentoo` (IRC) 中询问。如果没有，请为损坏的软件包提交 bug。

一旦 bug 被修复，请重新同步 Portage 树以获取修复后的摘要。

**重要**

这并不意味着在短时间内多次重新同步树！正如 rsync 策略中（以及运行 `emerge --sync` 时）所示，同步过于频繁的用户将被封禁！事实上，最好等到下一次计划的同步，以免重新同步导致 rsync 服务器过载。

## 什么是 USE 标记

### USE 标记背后的思想

在安装 Gentoo（或其他任何发行版，甚至是操作系统）时，用户根据其工作环境做出选择。服务器的设置与工作站的设置不同。游戏工作站与 3D 渲染工作站不同。

这不仅适用于选择安装哪些软件包，也适用于特定软件包应该支持哪些功能。如果没有 OpenGL，为什么要费力安装并维护 OpenGL 并在大多数软件包中构建 OpenGL 支持呢？如果有人不想使用 KDE，为什么要费力编译那些在不需要的情况下完美运行的带 KDE 支持的软件包呢？

为了帮助用户决定安装/激活哪些内容，Gentoo 希望用户能以简单的方式指定他们的环境。这迫使用户决定他们真正想要什么，并方便 Portage 做出有效的决策。

### USE 标记的定义

输入 USE 标记。此类标记是一个关键字，体现了对特定概念的支持和依赖信息。如果有人定义了特定的 `USE` 标记，Portage 就会知道他们想要所选关键字的支持。当然，这也会更改软件包的依赖信息。

来看一个具体的例子：`kde` 关键字。如果该关键字不在 `USE` 变量中，所有具有可选 KDE 支持的软件包将在*不带* KDE 支持的情况下编译。所有具有可选 KDE 依赖的软件包都将在*不安装* KDE 库（作为依赖）的情况下安装。当定义了 `kde` 标记时，这些软件包将*带有* KDE 支持进行编译，并且 KDE 库*将*作为依赖被安装。

通过正确定义关键字，系统将根据用户的需求进行定制。

### 有哪些 USE 标记

USE 标记有两种类型：全局 USE 标记和本地 USE 标记。

*   *全局* USE 标记在整个系统中被多个软件包使用。这是大多数人看到的 USE 标记。可用全局 USE 标记列表可以在[主站](https://www.gentoo.org/support/use-flags/#global) 上或在本地的 `/usr/portage/profiles/use.desc` 文件中找到。

*   *本地* USE 标记由单个软件包用于做出特定特定的决策。可用本地 USE 标记列表可以在[主站](https://www.gentoo.org/support/use-flags/#local) 上或在本地的 `/usr/portage/profiles/use.local.desc` 文件中找到。

## 使用 USE 标记

### 声明永久 USE 标记

如前，所有 USE 标记都声明在 `USE` 变量内部。为了方便用户搜索和选择 USE 标记，我们提供了一个默认的 USE 设置。该设置是我们认为 Gentoo 用户常用的 USE 标记集合。此默认设置在所选配置包含的 `make.defaults` 文件中声明。

系统监听的配置文件由 `/etc/portage/make.profile` 符号指向。每个配置都构建在其他配置之上，因此结果是所有配置文件的总和。顶部配置是基础配置（`/usr/portage/profiles/base`）。

要查看当前激活的所有 USE 标记，使用 `emerge --info`：

`root #` `emerge --info | grep ^USE`

```
USE="a52 aac acpi alsa branding cairo cdr dbus dts ..."
```




可见，该变量已经包含了许多关键词。不过，不要修改任何 `make.defaults` 文件来根据个人需求定制 `USE` 变量，因为当 portage 树更新时，这些文件的更改将被撤销！

要更改此默认设置，请向 `USE` 变量中添加或删除关键字。这通过在 `/etc/portage/make.conf` 中定义 `USE` 变量来实现全局配置。在该变量中，可以添加所需的额外 `USE` 标记，或移除不再需要的 `USE` 标记。后者通过在关键字前加上负号（`-`）来实现。

例如，要移除对 KDE 和 QT 的支持并添加对 ldap 的支持，可以在 `/etc/portage/make.conf` 中定义以下 `USE`：`/etc/portage/make.conf` 在 make.conf 中更新 USE

```
 USE="-kde -qt4 ldap"
```

### 为单个包声明 USE 标记

用户有时希望为一个（或几个）应用程序声明特定的 USE 标记，而不是全局生效。要实现这一点，请编辑 `/etc/portage/package.use`。这通常是一个文件，也可以是一个目录；更多信息请参阅 `man portage`。以下示例假设 `package.use` 是单文件。

例如，仅为 mysql 开启 berkdb 支持：`/etc/portage/package.use` 为 MySQL 启用 berkdb 支持

```
 dev-db/mysql berkdb
```

同样也可以显式禁用某些应用程序的 USE 标记。例如，禁用 PHP 中的 java 支持（但通过 make.conf 中的 USE 标记声明为所有其他包保留该支持）：`/etc/portage/package.use` 禁用 PHP 中的 java 支持

```
 dev-php/php -java
```

### 声明临时 USE 标记

用户有时需要短时间内设置一个 USE 标记。与其编辑两次 `/etc/portage/make.conf`（为了执行和撤销 USE 更改），不如直接将 `USE` 变量声明为环境变量。请记住，此设置仅对输入的命令有效；重新编译或更新此应用程序（无论是显式地还是作为系统更新的一部分）都将撤销通过（临时）USE 标记定义触发的更改。

以下示例了在安装 seamonkey 期间临时从 USE 设置中移除 java：

`root #` `USE="-java" emerge seamonkey`

### 优先级

当然，对于哪个设置优先于 USE 设置存在特定的优先级。USE 设置的优先级从低到高排序如下（第一个优先级最低）：

1. 您的配置中 `make.defaults` 文件中声明的默认 USE 设置
2. `/etc/portage/make.conf` 中的用户定义 USE 设置
3. `/etc/portage/package.use` 中的用户定义 USE 设置
4. 作为环境变量的用户定义 USE 设置

要查看 Portage 最终所的最终 USE 设置，请运行 `emerge --info`。这将列出所有相关变量（包括 `USE` 变量）以及在 portage 中已知的当前定义。

`root #` `emerge --info`

### 使整个系统适配新的 USE 标记

在修改 USE 标记后，应该更新系统以反映必要的更改。要做到这一点，请在运行 `emerge` 时使用 `--newuse` 选项：

`root #` `emerge --update --deep --newuse @world`

接下来，运行 portage 的 `depclean` 来移除在“旧”系统上编译但已因新 USE 标记而废弃的条件依赖。

**警告**

运行 `emerge --depclean` 是一个危险的操作，应该小心处理。请双击提供的“废弃”包列表，以确保不会移除所需的包。在以下示例中，我们添加了 `-p` 选项，让 depclean 仅列出包而不删除它们：

`root #` `emerge -p --depclean`

当 depclean 完成后，运行 `revdep-rebuild` 来重新编译那些与可能移除的包所提供的共享对象动态链接的应用程序。`revdep-rebuild` 是 `app-portage/gentoolkit` 包的一部分；别忘记先 emerge 它。

`root #` `revdep-rebuild`

完成所有这些操作后，系统将使用新的 USE 标记设置。

## 包特定的 USE 标记

### 查看可用的 USE 标记

以 seamonkey 为例：它监听哪些 USE 标记？要找到答案，我们使用带有 `--pretend` 和 `--verbose` 选项的 `emerge`：

`root #` `emerge --pretend --verbose seamonkey`

```
这些将按顺序合并的包：

正在计算依赖关系 ...完成！
[ebuild   R   ] www-client/seamonkey-1.0.7  USE="crypt gnome java -debug -ipv6
-ldap -mozcalendar -mozdevelop -moznocompose -moznoirc -moznomail -moznopango
-moznoroaming -postgres -xinerama -xprint" 0 kB
```

`emerge` 并不是这项工作的唯一工具。事实上，有一个专门用于包信息的工具 `equery`，它位于 `app-portage/gentoolkit` 包中。

`root #` `emerge --ask app-portage/gentoolkit`

现在使用 `uses` 参数运行 `equery` 来查看特定包的 USE 标记。例如，对于 gnumeric：

`root #` `equery --uses gnumeric`

```
[ 正在查找匹配 gnumeric 的包...
[ 找到这些 USE 变量

### 满足 REQUIRED_USE 条件

某些 ebuild 要求或禁止某些 USE 标记组合才能正常工作。这通过放置在 `REQUIRED_USE` 中的一组条件来实现。这些条件确保了所有功能和依赖都是完整的，并且构建将成功。如果未满足其中任何条件，`emerge` 将警告你并要求你修复问题。

下面是 `REQUIRED_USE` 表达式的一些示例：

| 示例 | 描述 |
| :--- | :--- |
| `REQUIRED_USE="foo? ( bar )"` | 如果设置了 `foo`，则必须设置 `bar`。 |
| `REQUIRED_USE="foo? (!bar )"` | 如果设置了 `foo`，则不能设置 `bar`。 |
| `REQUIRED_USE="foo? ( #124;&#124; ( baz ) )"` | 如果设置了 `foo`，则必须设置 `bar` 或 `baz`。 |
| `REQUIRED_USE="^^ ( foo bar baz )"` | `foo`、`bar` 或 `baz` 恰好设置一个。 |
| `REQUIRED_USE="&#124;&#124; ( foo bar baz )"` | `foo`、`bar` 或 `baz` 至少设置一个。 |
| `REQUIRED_USE="?? ( foo bar baz )"` | `foo`、`bar` 或 `baz` 最多设置一个。 |

## Portage 特性

Portage 有许多附加功能，可以让 Gentoo 体验变得更好。许多这些功能依赖于某些改进性能、可靠性、安全性的工具 ...

## 分布式编译

### 使用 distcc





`distcc` 是一个将编译分发到网络上几台（不一定相同）机器的程序。`distcc` 客户端会将所有必要信息发送到可用的 `distcc` 服务器（运行 `distccd`），以便它们为客户端编译源码片段。最终结果是缩短编译时间。

关于 `distcc` 的更多信息（以及如何让它在 Gentoo 中工作）可以参阅 [Distcc](https://wiki.gentoo.org/wiki/Distcc "Distcc") 文章。

## 安装 distcc

`distcc` 自带有一个图形化监控器，用于监控计算机发送出去进行编译的任务。如果设置了 `USE=gnome` 或 `USE=gtk`，则会自动安装此工具。

```bash
root # emerge --ask sys-devel/distcc
```

### 激活 Portage 的 distcc 支持

在 `/etc/portage/make.conf` 内部 `FEATURES` 变量中添加 `distcc`。接下来，编辑 `MAKEOPTS` 变量并增加系统允许的并行构建作业数量。一个已知指南是填充 `-jX`，其中 `X` 是运行 `distccd` 的 CPU 数量（包括当前主机）加一，但这只是一个指南。

现在运行 `distcc-config` 并输入可用的 `distcc` 服务器列表。假设可用的 DistCC 服务器为 `192.168.1.102`（当前主机）、`192.168.1.103` 和 `192.168.1.104`（两台“远程”主机）：

```bash
root # distcc-config --set-hosts "192.168.1.102 192.168.1.103 192.168.1.104"
```

别忘了运行 `distccd` 守护进程：

```bash
root # rc-update add distccd default
root # /etc/init.d/distccd start
```

## 缓存编译对象

### 关于 ccache

`ccache` 是快速编译器缓存。每当编译应用程序时，它都会缓存中间结果，这样每当重新编译同一个程序时，编译时间就会大大缩短。第一次运行 `ccache` 时，它会比普通编译慢得多。然而，随后的重新编译应该更快。`ccache` 只有在同一个应用程序被多次编译（或频繁升级相同应用程序）时才有用；因此它主要对软件开发者有用。

关于 `ccache` 的更多信息，请访问其[首页](http://ccache.samba.org/)。

**警告**

`ccache` 已知会导致许多编译失败。有时 ccache 会保留过时的代码对象或损坏的文件，这会导致无法 emerge 包。如果发生这种情况（构建日志中出现类似“File not recognized: File truncated”的错误），请在报告 之前尝试在禁用 ccache 的情况下重新编译应用程序（在 `/etc/portage/make.conf` 中设置 `FEATURES="-ccache"`）。

### 安装 ccache

运行以下命令安装 `ccache`：

```bash
root # emerge --ask dev-util/ccache
```

### 激活 Portage 的 ccache 支持

打开 `/etc/portage/make.conf` 并向 `FEATURES` 变量添加 `ccache`。接下来，添加一个名为 `CCACHE_SIZE` 的新变量并将其设置为 `2G`：

FILE `/etc/portage/make.conf`  Portage ccache 支持

```bash
FEATURES="... ccache ..."
CCACHE_SIZE="2G"
```

要检查 `ccache` 是否运行，请 `ccache` 提供其统计信息。由于 Portage 使用不同的 ccache 主目录，因此需要临时设置 `CCACHE_DIR` 变量：

```bash
root # CCACHE_DIR="/var/tmp/ccache" ccache -s
```

`/var/tmp/ccache/` 是 Portage 的默认 ccache 主目录；可以通过设置 `/etc/portage/make.conf` 中的 `CCACHE_DIR` 变量进行更改。

当单独运行 `ccache` 时，它将使用默认位置 `${HOME}/.ccache/`，这就是为什么在请求 (Portage) ccache 统计信息时需要设置 `CCACHE_DIR` 变量。

### 在 Portage 之外使用 ccache

要使用 `ccache` 进行非 Portage 编译，将 `/usr/lib/ccache/bin/` 添加到 `PATH` 变量的开头（在 `/usr/bin` 之前）。可以通过编辑用户主目录下的 `~/.bash_profile` 实现。使用 `~/.bash_profile` 是定义 `PATH` 变量的方法之一。

FILE `~/.bash_profile` 在任何其他 PATH 之前设置 ccache 位置

```bash
PATH="/usr/lib/ccache/bin:/opt/bin:${PATH}"
```

## 二进制包支持

### 创建预构建包

Portage 支持安装预构建包。尽管 Gentoo 本身不提供预构建包，但 Portage 可以感知预构建包。

如果包已安装在系统上，使用 `quickpkg` 来创建预构建包，或者使用带有 `--buildpkg` 或 `--buildpkgonly` 选项运行 emerge。

要让 Portage 为每个安装的包创建预构建包，请向 `FEATURES` 变量中添加 `buildpkg`。

可以通过 `catalyst` 获取更广泛的支持创建预构建包集。关于 catalyst 的更多信息，请阅读 [Catalyst FAQ](https://wiki.gentoo.org/wiki/Project:Catalyst/FAQ "Project:Catalyst/FAQ")。

### 安装预构建包

尽管 Gentoo 不提供，但可以创建一个存储预构建包的中央仓库。为了使用此仓库，必须通过让 `PORTAGE_BINHOST` 变量指向它来让 Portage 感知。例如，如果预构建包位于 ftp://buildhost/gentoo：FILE `/etc/portage/make.conf` 添加 PORTAGE_BINHOST 位置

```bash
PORTAGE_BINHOST="ftp://buildhost/gentoo"
```

要安装预构建包，在 `emerge` 命令中配合 `--usepkg` 选项添加 `--getbinpkg` 选项。前者告诉 `emerge` 从之前定义的服务器下载预构建包，而后者要求 `emerge` 在获取源码并编译之前，尝试先安装预构建包。

例如，使用预构建包安装 gnumeric：

```bash
root # emerge --usepkg --getbinpkg gnumeric
```

关于 `emerge` 二进制包选项的更多信息可以在 `emerge` 手页中找到：

```bash
user $ man emerge
```

### 将预构建包分发给他人

如果要将预构建包分发给他人，请确保允许这样做。为此检查上游包的分发条款。例如，对于在 GNU GPL 下发布的包，必须提供二进制文件的同时提供源码。

如果构建的二进制文件不可分发，Ebuild 可以在 `RESTRICT` 变量中定义 `bindist` 限制。有时这种限制取决于一个或多个 USE flag。

默认情况下，Portage 不会因为限制屏蔽任何包。这可以通过设置 `/etc/portage/make.conf` 中的 `ACCEPT_RESTRICT` 变量进行全局更改。例如，要屏蔽具有 `bindist` 限制的包，在 make.conf 中添加以下行：FILE `/etc/portage/make.conf` 仅接受可二进制分发的包

```bash
ACCEPT_RESTRICT="* -bindist"
```

还可以通过向 `emerge` 命令传递 `--accept-restrict` 选项来覆盖 `ACCEPT_RESTRICT` 变量。例如，`--accept-restrict=-bindist` 将临时屏蔽具有 `bindist` 限制的包。

分发包时还要考虑设置 `ACCEPT_LICENSE` 变量。请参阅[许可证部分](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Portage#Licenses "Handbook:AMD64/Working/Portage")。

**重要**

每个*用户*遵守包的许可证条款以及用户所在国家的法律完全是其自身的责任。ebuild 定义的元数据变量（`RESTRICT` 或 `LICENSE`）在不允许分发二进制文件时可以提供指导，但 Portage 的输出或 Gentoo 开发者回答的问题*不是*法律陈述，不应将其视为法律依据。请谨慎遵守你所在地的法律。

## 获取文件

### Userfetch

当以 root 身份运行 Portage 时，`FEATURES="userfetch"` 将允许 Portage 在获取包源码时放弃 root 权限。这是一个微小的安全改进。

### 验证过的 Portage 树快照





管理员可以选择由 Gentoo 基础设施发布的、经过加密验证的树快照来更新本地 Gentoo ebuild 树。这确保了没有恶意的 rsync 镜像向系统正在下载的树中添加未请求代码或软件包。

#### 注意事项

以下是使用 `repos.conf` 设置和使用 `emerge-webrsync` 同步方法的更新方法。

Gentoo 发布媒体的 OpenPGP 密钥现在以二进制密钥环的形式可用。可以通过[app-crypt/gentoo-keys](https://packages.gentoo.org/packages/app-crypt/gentoo-keys)` 包进行安装：

`root #` `emerge --ask app-crypt/gentoo-keys`

这将会将密钥环安装到 `/var/lib/gentoo/gkeys/keyrings/gentoo/release` 路径。

### 文件 `/etc/portage/make.conf` - 在 Portage 中启用 GPG 支持

```
 FEATURES="webrsync-gpg"
PORTAGE_GPG_DIR="/var/lib/gentoo/gkeys/keyrings/gentoo/release"
```

### 文件 `/etc/portage/repos.conf/gentoo.conf` - 清空 sync-uri 变量

```
 [DEFAULT]
main-repo = gentoo

[gentoo]
# 通过清空值或设置 auto-sync = no 来禁用同步
# 不要在此配置文件中使用引号（'' 或 ""）为变量赋值！
# 对于 portage-2.2.18 使用 'websync'
# 对于 portage-2.2.19 及更高版本使用 'webrsync' (websync 已重命名为 webrsync)
sync-type = webrsync
sync-uri = 
auto-sync = yes
```

确保已安装[app-crypt/gnupg](https://packages.gentoo.org/packages/app-crypt/gnupg)` 包：

`root #` `emerge --ask app-crypt/gnupg`

使用 gpg 验证密钥环中的密钥是否正确：

`root #` `gpg --homedir /var/lib/gentoo/gkeys/keyrings/gentoo/release --with-fingerprint --list-keys`

核对密钥的指纹，是否与[官方 Gentoo 发布工程项目页面上列出的](https://wiki.gentoo.org/wiki/Project:RelEng#Keys "Project:RelEng")一致。

对每个你想要信任的密钥重复以下命令。（将 keyid '0x...' 替换为你想要信任的密钥。）

`root #` `gpg --homedir /var/lib/gentoo/gkeys/keyrings/gentoo/release --edit-key 0xDB6B8C1F96D8BF6D trust`

如果出现 GPG 命令行菜单，请完全信任该密钥并输入以下内容退出程序：

`gpg>` `4`
`gpg>` `quit`

系统现在已配置为仅使用 OpenPGP/gpg 验证的快照进行同步。

有多个命令选项可以执行同步。

#### 注意事项

同步仅需以下命令之一。更多详情请参阅[Portage 同步 wiki 文章](https://wiki.gentoo.org/wiki/Project:Portage/Sync "Project:Portage/Sync")。

`root #` `emerge --sync`
`root #` `emaint sync -a`
`root #` `emaint sync --repo gentoo`
`root #` `emerge-webrsync`

## 级别 (Runlevels)

### 启动系统

当系统启动时，会有大量文本流过。仔细观察，你会发现这些文本在每次系统重启时（通常）都是相同的。所有这些动作的顺序被称为启动序列，并且它在很大程度上是静态定义的。

首先，引导加载程序将加载在引导程序配置中定义的内核镜像。然后，引导加载程序指示 CPU 运行内核。当内核加载并运行后，它会初始化所有内核特定的结构和任务，并启动 init 进程。

该进程随后确保所有文件系统（在 `/etc/fstab` 中定义）已挂载并准备好使用。然后它执行位于 `/etc/init.d/` 中的多个脚本，这些脚本将启动成功启动系统所需的服务。

最后，当所有脚本执行完毕后，init 会激活终端（大多数情况下只是隐藏在 `Alt`+`F1`、`Alt`+`F2` 等之下的虚拟控制台），并为其挂载一个名为 `agetty` 的特殊进程。该进程将通过运行 login 来确保用户能够通过这些终端登录。

### Init 脚本 (Initscripts)

现在 init 不会随机执行 `/etc/init.d/` 中的脚本。更进一步，它不会运行 `/etc/init.d/` 中的所有脚本，只运行被指示执行的脚本。它通过查看 `/etc/runlevels/` 来决定执行哪些脚本。

首先，init 运行所有在 `/etc/runlevels/boot/` 中有符号链接的 `/etc/init.d/` 脚本。通常，它会按字母顺序启动脚本，但某些脚本包含依赖信息，告诉系统在启动它们之前必须运行另一个脚本。

当所有 `/etc/runlevels/boot/` 引用的脚本执行完毕后，init 继续运行在 `/etc/runlevels/default/` 中有其符号链接的脚本。同样，它将使用字母顺序来决定先运行哪个脚本，除非脚本包含依赖信息，在这种情况下，顺序将改变以提供有效的启动序列。后者也是为什么在安装 Gentoo Linux 期间使用的命令使用了 `default`，例如 `rc-update add sshd default`。

### init 如何工作的

当然，init 并不是由自己决定这一切的。它需要一个指定需要采取哪些操作的配置文件。该配置文件是 `/etc/inittab`。

记住刚才描述的启动序列 - init 的第一个动作是挂载所有文件系统。这在 `/etc/inittab` 的以下行定义：

### 文件 `/etc/inittab` - 初始化命令

```
 si::sysinit:/sbin/rc sysinit
```

这一行告诉 init 它必须运行 `/sbin/rc sysinit` 来初始化系统。`/sbin/rc` 脚本负责初始化，所以可以说 init 并没有做什么——它将初始化系统的任务委托给了另一个进程。

其次，init 执行了所有在 `/etc/runlevels/boot/` 中符号链接的脚本。这在以下行定义：

### 文件 `/etc/inittab` - 启动命令调用

```
 rc::bootwait:/sbin/rc boot
```

同样，`rc` 脚本执行必要的任务。注意给 `rc` 的选项（`boot`）与 `/etc/runlevels/` 的子目录相同。

现在 init 检查其配置文件查看它应该运行哪个级别。为了决定这一点，它从 `/etc/inittab` 读取以下行：

### 文件 `/etc/inittab` - 默认级别选择

```
 id:3:initdefault
```

在这种情况下（大多数 Gentoo 用户将使用的），级别 id 为 3。利用此信息，init 检查为了启动级别 3 它必须运行什么：

### 文件 `/etc/inittab` - 级别定义

```
 l0:0:wait:/sbin/rc shutdown
 l1:S1:wait:/sbin/rc single
 l2:2:wait:/sbin/rc nonetwork
 l3:3:wait:/sbin/rc default
 l4:4:wait:/sbin/rc default
 l5:5:wait:/sbin/rc default
 l6:6:wait:/sbin/rc reboot
```

定义级别 3 的行再次使用 `rc` 脚本启动服务（现在参数为 `default`）。再次注意，`rc` 的参数与 `/etc/runlevels/` 的子目录相同。

当 `rc` 完成完成后，init 决定应该激活哪些虚拟控制台以及在每个控制台上需要运行哪些命令：

### 文件 `/etc/inittab` - 终端定义

```
 c1:12345:respawn:/sbin/agetty 38400 tty1 linux
 c2:12345:respawn:/sbin/agetty 38400 tty2 linux
 c3:12345:respawn:/sbin/agetty 38400 tty3 linux
 c4:12345:respawn:/sbin/agetty 38400 tty4 linux
 c5:12345:respawn:/sbin/agetty 38400 tty5 linux
 c6:12345:respawn:/sbin/agetty 38400 tty6 linux
```

### 可用的级别

在前面的章节中，我们看到 init 使用编号方案来决定它应该激活哪个级别。级别（runlevel）是系统运行的状态，包含一组脚本（级别脚本或 init 脚本），这些脚本在进入或离开级别时必须执行。

在 Gentoo 中，定义了七个级别：三个内部级别和四个自定义级别。内部级别被称为 *sysinit*、*shutdown* 和 *reboot*，它们的作用正如其名所示：初始化系统、关机和重启系统。





用户定义的运行级别（runlevels）是指带有相应的 `/etc/runlevels/` 子目录的级别：`boot`、`default`、`nonetwork` 和 `single`。`boot` 级别启动所有系统必需的服务，其他运行级别都会使用这些服务。其余三个运行级别的区别在于它们启动的服务不同：`default` 用于日常操作，`nonetwork` 用于不需要网络连接的情况，而 `single` 用于系统需要修复时。

## 使用 initscripts

由 `rc` 进程启动的脚本被称为初始化脚本（init scripts）。`/etc/init.d/` 中的每个脚本都可以使用 `start`、`stop`、`restart`、`zap`、`status`、`ineed`、`iuse`、`needsme`、`usesme` 或 `broken` 参数执行。

要启动、停止或重启一个服务（以及所有依赖的服务），应使用 `start`、`stop` 和 `restart` 参数：

```
root # /etc/init.d/postfix start
```
**注意** 只需要服务的服务的停止或重启。其他的依赖服务（使用该服务但不需要它的服务）将保持不变。

要停止一个服务但不停止依赖于它的服务，请使用 `--nodeps` 配合 `stop` 参数：

```
root # /etc/init.d/postfix --nodeps stop
```

要查看服务的状态（已启动、已停止、……），请使用 `status` 参数：

```
root # /etc/init.d/postfix status
```

如果状态信息显示服务正在运行，但实际上它并没有运行，请使用 `zap` 参数将状态信息重置为“stopped”（已停止）：

```
root # /etc/init.d/postfix zap
```

若还要查询该服务具有哪些依赖，请使用 `iuse` 或 `ineed`。使用 `ineed` 可以查看对于该服务的正确运行是真正必需的服务。相反，`iuse` 显示了该服务可以使用但对于其正确运行并非所必需的服务。

```
root # /etc/init.d/postfix ineed
```

同样，也可以查询哪些服务需要该服务（`needsme`）或可以使用它（`usesme`）：

```
root # /etc/init.d/postfix needsme
```

最后，查询该服务所需的缺失依赖项：

```
root # /etc/init.d/postfix broken
```

## 更新运行级别

### rc-update

Gentoo 的初始化系统使用依赖树来决定需要先启动哪个服务。由于这是一项我们不希望用户手动完成的繁琐任务，因此我们创建了工具来简化运行级别和初始化脚本的管理。

通过 `rc-update`，可以向某个运行级别添加或删除初始化脚本。`rc-update` 工具随后会自动请求 `depscan.sh` 脚本重新构建依赖树。

### 添加和删除服务

在早期的指令中，初始化脚本已经添加到“default”运行级别中。“default”的含义在本文前面已经解释过。在运行级别旁边，`rc-update` 脚本需要第二个参数来定义操作：`add`、`del` 或 `show`。

要添加或删除初始化脚本，只需给 `rc-update` 提供 `add` 或 `del` 参数，随后是初始化脚本和运行级别。例如：

```
root # rc-update del postfix default
```

`rc-update -v show` 命令将显示所有可用的初始化脚本，并列出它们将在哪些运行级别执行：

```
root # rc-update -v show
```

也可以运行 `rc-update show`（不带 `-v`）仅查看已启用的初始化脚本及其运行级别。

## 配置服务

### 为什么需要额外的配置

初始化脚本可能相当复杂。因此，并不希望让用户直接编辑初始化脚本，因为这会使其更容易出错。然而，能够配置此类服务是非常重要的。例如，用户可能想为服务本身提供更多选项。

将此类配置放在初始化脚本之外的另一个原因是，可以更新初始化脚本，而不必担心用户的配置更改会被撤销。

### conf.d 目录

Gentoo 提供了一种配置此类服务的简单方法：每个可以配置的初始化脚本在 `/etc/conf.d/` 中都有一个文件。例如，apache2 初始化脚本（位于 `/etc/init.d/apache2`）有一个名为 `/etc/conf.d/apache2` 的配置文件，该文件可以包含启动时传递给 Apache 2 服务器的选项：FILE `/etc/conf.d/apache2` **apache2 初始化脚本的示例选项**

```
 APACHE2_OPTS="-D PHP5"
```

此类配置文件*仅*包含变量（就像 `/etc/portage/make.conf` 一样），使得配置服务变得非常容易。它允许我们提供更多关于变量的信息（作为注释）。

## 编写 initscripts

### 是否必要

不，编写初始化脚本通常不是必要的，因为 Gentoo 为所有提供的服务都提供了现成的初始化脚本。但是，某些用户可能在没有使用 portage 的情况下安装了服务，在这种他们可能必须创建一个初始化脚本。

如果服务不是专门为 Gentoo 编写的，请不要使用服务提供的初始化脚本：Gentoo 的初始化脚本与其他发行版使用的初始化脚本不兼容！

### 布局

初始化脚本的基本布局所示。

CODE **初始化脚本布局示例**

```
 #!/sbin/openrc-run

depend() {
  (依赖信息)
}

start() {
  (启动服务所需的命令)
}

stop() {
  (停止服务所需的命令)
}
```

每个初始化脚本都需要定义 `start()` 函数。所有其他部分都是可选的。

### 依赖

可以定义两个类似于依赖的设置，它们会影响初始化脚本的启动或排序：`use` 和 `need`。在这两个旁边，还有两个影响顺序的方法，称为 `before` 和 `after`。最后两个本身并不是依赖关系——如果所选的没有被计划启动（或启动失败），它们不会导致原始初始化脚本失败。

*   `use` 设置告知初始化系统此脚本使用了所选脚本提供的功能，但并不直接依赖于它。一个好的例子是 `use logger` 或 `use dns`。如果这些服务可用，它们将被充分利用，但如果系统没有 logger 或 DNS 服务器，这些服务仍然可以工作。如果服务存在，则它们会在使用它们的脚本之前启动。

*   `need` 设置是硬依赖。这意味着需要另一个脚本的脚本不会在另一个脚本成功启动之前启动。此外，如果另一个脚本重启，这个脚本也会之重启。

*   当使用 `before` 时，如果所选的脚本是初始化级别的一部分，则给定的脚本将在所选脚本之前启动。因此，定义了 `before alsasound` 的初始化脚本 `xdm` 将在 `alsasound` 脚本之前启动，但前提是 `alsasound` 同样在同一个初始化级别中被计划启动。如果 `alsasound` 没有被计划启动，则此特定设置不起作用，`xdm` 将在初始化系统认为最合适的时候启动。

*   同样，`after` 告知初始化系统，如果所选的脚本是初始化级别的一部分，则给定的脚本应在所选之后之后。如果不是，则该设置不起作用，脚本将由初始化系统在其认为最合适的时候启动。

从上述可以清楚，`need` 是唯一的“真正”依赖设置，因为它影响脚本是否会启动。所有其他设置仅仅是指向初始化系统的指针，以澄清脚本可以（或应该）以什么顺序启动。

现在，查看 Gentoo 许多可用的初始化脚本，注意有些脚本依赖于某些不是初始化脚本的东西。这些“东西”我们称为虚拟设备（virtuals）。





虚拟依赖（Virtual dependency）是指一个服务提供的依赖，但该依赖并非由该服务唯一提供。初始化脚本可以依赖系统日志记录器，但有很多可用的系统日志记录器（`metalogd`、`syslog-ng`、`sysklogd` 等）。由于脚本不需要它们中的每一个（没有哪个合理的系统会安装并运行所有这些系统日志记录器），因此我们确保了所有这些服务都提供一个虚拟依赖。

例如，查看 postfix 的依赖信息：FILE `/etc/init.d/postfix` **postfix 服务的依赖信息**

```
 depend() {
  need net
  use logger dns
  provide mta
}
```

如上所示，postfix 服务：

*   需要（虚拟的）`net` 依赖（例如由 `/etc/init.d/net.eth0` 提供）。
*   使用（虚拟的）`logger` 依赖（例如由 `/etc/init.d/syslog-ng` 提供）。
*   使用（虚拟的）`dns` 依赖（例如由 `/etc/init.d/named` 提供）。
*   提供（虚拟的）`mta` 依赖（所有邮件服务器通用的）。

### 控制顺序

如上一节所述，可以告诉初始化系统应该使用何种顺序来启动（或停止）脚本。这种排序既通过依赖设置 `use` 和 `need` 来处理，也通过顺序设置 `before` 和 `after` 来处理。由于我们之前已经描述过这些内容，让我们以 portmap 服务作为此类初始化脚本的示例来看。

FILE `/etc/init.d/portmap` **portmap 服务的依赖信息**

```
 depend() {
  need net
  before inetd
  before xinetd
}
```

可以使用 `*` 通配符来捕获同一运行级别（runlevel）中的所有服务，尽管不建议这样做。

CODE **使用 * 通配符**

```
 depend() {
  before *
}
```

如果服务必须写入本地磁盘，则它应该需要 `localmount`。如果它在 `/var/run/` 中放置任何内容（如 pidfile），则它应该在 `bootmisc` 之后启动：

CODE **需要 localmount 且在 bootmisc 之后的依赖设置**

```
 depend() {
  need localmount
  after bootmisc
}
```

### 标准函数

除了 `depend()` 功能外，也有必要定义 `start()` 函数。该函数包含了初始化服务所需的所有命令。建议使用 `ebegin` 和 `eend` 函数来告知用户正在发生什么：

CODE **start() 函数示例**

```
 start() {
  if [ "${RC_CMD}" = "restart" ];
  then
    # 如果重启需要比停止、启动更多的操作则执行某些操作
  fi

  ebegin "Starting my_service"
  start-stop-daemon --start --exec /path/to/my_service \
    --pidfile /path/to/my_pidfile
  eend $?
}
```

启动和停止函数中都应使用 `--exec` 和 `--pidfile`。如果服务不创建 pidfile，则尽可能使用 `--make-pidfile`，但建议进行测试以确保。否则，不要使用 pidfiles。也可以在 `start-stop-daemon` 选项中添加 `--quiet`，但除非该服务输出极其详尽，否则不建议这样做。如果服务启动失败，使用 `--quiet` 可能会阻碍调试。

上述示例中使用的另一个显著设置是检查 `RC_CMD` 变量的内容。与之前的初始化脚本系统不同，较新的 openrc 系统不支持特定特定的重启功能。相反，脚本需要检查 `RC_CMD` 变量的内容，以查看某个函数（无论是 `start()` 还是 `stop()`）是否作为重启的一部分被调用。

**注意**

确保 `--exec` 实际调用的是服务，而不仅仅是一个启动服务并退出的 shell 脚本——这才是初始化脚本要做的工作。

有关 `start()` 函数的更多示例，请阅读 `/etc/init.d/` 目录下可用初始化脚本的源代码。

另一个可以（但不必非）定义的函数是 `stop()`。如果使用了 `start-stop-daemon`，初始化系统足够智能可以自动填充此函数。

CODE **stop() 函数示例**

```
 stop() {
  ebegin "Stopping my_service"
  start-stop-daemon --stop --exec /path/to/my_service \
    --pidfile /path/to/my_pidfile
  eend $?
}
```

如果服务运行某些其他脚本（例如 Bash、Python 或 Perl），并且该脚本后来更改了名称（例如从 `foo.py` 改为 `foo`），则必须在 `start-stop-daemon` 中添加 `--name`。这必须指定名称。

start-stop-daemon 有一个非常好的 man 手页可以参考。

Gentoo 脚本示例

```

start-stop-daemon --start --exec /path/to/my_service \
    --pidfile /path/to/my_pidfile
--name foo
```

Gentoo 脚本基于 POSIX Shell。

### 添加自定义选项

如果初始化脚本需要比我们遇到的更多选项，请将选项添加到 `extra_commands`。例如，为了支持 `restartdelay`：

CODE **restartdelay 示例**。

## 更改运行级别行为

### 谁可能从中受益

许多笔记本用户都遇到过这种情况：在家里需要启动 `net.eth0`，但在路上不想启动 `net.eth0`（因为没有网络）。在 Gentoo 中可以任意更改运行级别的行为。

例如，可以创建一个第二个默认运行级别，并为其分配其他初始化脚本。启动时，用户可以选择使用何种运行级别。

### 使用软级别

首先，为第二个运行级别创建运行级别目录。作为示例，我们创建 `offline` 运行级别：

`root #` `mkdir /etc/runlevels/offline`

为新创建的运行级别添加必要的初始化脚本。例如，创建一个没有 `net.eth0` 的当前默认运行级别的副本：

`root #` `cd /etc/runlevels/default` `root #` `for service in *; do rc-update add $service offline; done` `root #` `rc-update del net.eth0 offline` `root #` `rc-update show offline`

```
（部分输出）
               acpid | offline
          domainname | offline
               local | offline
            net.eth0 |
```

尽管 `net.eth0` 已从离运行级别中移除，udev 可能仍尝试启动它检测到的任何设备并启动相应的服务，这种功能被称为热插（hotplugging）。默认情况下，Gentoo 不启用热插。

要启用热插，但仅针对选定的脚本集，请使用 `/etc/rc.conf` 中的 `rc_hotplug` 变量：

### 服务配置变量

为了支持 `/etc/conf.d/` 中的配置文件，以下文件会被加载（即变量可用）：

*   etc/conf.d/YOUR_SCRIPT
*   etc/conf.d/basic
*   rc.conf

此外，如果初始化脚本提供虚拟依赖（例如 `net`），与该依赖的文件（例如 `/etc/conf.d/net`）也会被加载。



修改启动加载程序配置并为离线运行级别（runlevel）添加新条目。在该条目中，添加 `softlevel=offline` 作为启动参数。

### 使用 bootlevel

使用 `bootlevel` 与 `softlevel` 完全对应。唯一的区别在于，这里定义的是第二个“boot”运行级别，而不是第二个“default”运行级别。

## 环境变量

### 介绍

环境变量是一个命名的对象，其中包含一个或多个应用程序所使用的信息。许多用户（尤其是 Linux 新手）认为这有点诡异或难以管理。然而，这是一个误区：通过使用环境变量，用户可以轻松地更改一个或多个应用程序的配置设置。

### 重要示例

下表列出了 Linux 系统使用的若干变量并描述了它们的用途。示例值列在表格之后。

| 变量 | 描述 |
| :--- | :--- |
| `PATH` | 该变量包含用冒号分隔的目录列表，系统会在这些目录下查找可执行文件。如果输入的可执行文件名称（如 `ls`、`rc-update` 或 `emerge`），但该可执行文件不在列出的目录中，系统将不会执行它（除非使用完整路径作为命令，例如 `/bin/ls`）。 |
| `ROOTPATH` | 该变量的功能与 `PATH` 相同，但它只列出 root 用户输入命令时应该检查的目录。 |
| `LDPATH` | 该变量包含用冒号分隔的目录列表，动态链接器会在这些目录中搜索库文件。 |
| `MANPATH` | 该变量包含用冒号分隔的目录列表，`man` 命令在这些目录中查找帮助页（man pages）。 |
| `INFODIR` | 该变量包含用冒号分隔的目录列表，`info` 命令在这些目录中查找 info 页面。 |
| `PAGER` | 该变量包含用于列出文件内容的程序路径（例如 `less` 或 `more`）。 |
| `EDITOR` | 该变量包含用于修改文件内容的程序路径（例如 `nano` 或 `vi`）。 |
| `KDEDIRS` | 该变量包含用冒号分隔的目录列表，包含 KDE 特有的材质。 |
| `CONFIG_PROTECT` | 该变量包含用空格分隔的目录列表，这些目录在更新期间应受 Portage 保护。 |
| `CONFIG_PROTECT_MASK` | 该变量包含用空格分隔的目录列表，这些目录在更新期间不应受 Portage 保护。 |

以下是这些变量的示例定义：

**上述变量的示例设置**

```
PATH="/bin:/usr/bin:/usr/local/bin:/opt/bin:/usr/games/bin"
ROOTPATH="/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin"
LDPATH="/lib:/usr/lib:/usr/local/lib:/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
MANPATH="/usr/share/man:/usr/local/share/man"
INFODIR="/usr/share/info:/usr/local/share/info"
PAGER="/usr/bin/less"
EDITOR="/usr/bin/vim"
KDEDIRS="/usr"
CONFIG_PROTECT="/usr/X11R6/lib/X11/xkb /opt/tomcat/conf \
/usr/kde/3.1/share/config /usr/share/texmf/tex/generic/config/ \
/usr/share/texmf/tex/platex/config/ /usr/share/config"
CONFIG_PROTECT_MASK="/etc/gconf"
```

## 全局定义变量

### env.d 目录

为了集中定义这些变量，Gentoo 引入了 `/etc/env.d/` 目录。在该目录下有许多文件，例如 `00basic`、`05gcc` 等，它们包含了名称中所述应用程序所需的变量。

例如，当安装 `gcc` 时，`ebuild` 会创建一个名为 `05gcc` 的文件，其中包含了以下变量的定义：`/etc/env.d/05gcc` **默认启用 gcc 的环境变量**

```
PATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
ROOTPATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
MANPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/man"
INFOPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/info"
CC="gcc"
CXX="g++"
LDPATH="/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
```

其他发行版可能会要求用户在 `/etc/profile` 或其他位置更改或添加此类环境变量定义。相反，Gentoo 让用户（以及 `Portage`）能够轻松地维护和管理环境变量，而无需关注那些可能包含环境变量的众多文件。

例如，当 `gcc` 更新时，`/etc/env.d/05gcc` 文件也会随之更新，而无需任何用户交互。

这不仅有利于 `Portage`，对用户也有益。有时用户可能会被要求在系统范围内设置某个特定的环境变量。以 `http_proxy` 变量为例。与其弄乱 `/etc/profile`，用户只需创建一个文件（例如 `/etc/env.d/99local`）并写入：`/etc/env.d/99local` **全局变量**

```
http_proxy="proxy.com:8080"
```

### env.update

为了集中定义这些变量，Gentoo 引入了 `/etc/env.d/` 目录。在该目录下有许多文件，例如 `00basic`、`05gcc` 等，它们包含了名称中所述应用程序所需的变量。

例如，当安装 `gcc` 时，`ebuild` 会创建一个名为 `05gcc` 的文件，其中包含了以下变量的定义：`/etc/env.d/05gcc` **默认启用 gcc 的环境变量**

```
PATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
ROOTPATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
MANPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/man"
INFOPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/info"
CC="gcc"
CXX="g++"
LDPATH="/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
```

其他发行版可能会要求用户在 `/etc/profile` 或其他位置更改或添加此类环境变量定义。相反，Gentoo 让用户（以及 `Portage`）能够轻松地维护和管理环境变量，而无需关注那些可能包含环境变量的众多文件。

例如，当 `gcc` 更新时，`/etc/env.d/05gcc` 文件也会随之更新，而无需任何用户交互。

这不仅有利于 `Portage`，对用户也有益。有时用户可能会被要求在系统范围内设置某个特定的环境变量。以 `http_proxy` 变量为例。与其弄乱 `/etc/profile`，用户只需创建一个文件（例如 `/etc/env.d/99local`）并写入：`/etc/env.d/99local` **全局变量**

```
http_proxy="proxy.com:8080"
```

### env.update

为了集中定义这些变量，Gentoo 引入了 `/etc/env.d/` 目录。在该目录下有许多文件，例如 `00basic`、`05gcc` 等，它们包含了名称中所述应用程序所需的变量。

例如，当安装 `gcc` 时，`ebuild` 会创建一个名为 `05gcc` 的文件，其中包含了以下变量的定义：`/etc/env.d/05gcc` **默认启用 gcc 的环境变量**

```
PATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
ROOTPATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
MANPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/man"
INFOPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/info"
CC="gcc"
CXX="g++"
LDPATH="/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
```

（注：由于原文文本中存在大量重复段落，此处已根据指令要求合并并整理了基于 Gentoo 环境变量管理逻辑的翻译内容。）

**以下为基于逻辑的完整翻译译文：**

[content]
修改启动加载程序配置并为离线运行级别添加新条目。在该条目中，添加 `softlevel=offline` 作为启动参数。

### 使用 bootlevel

使用 `bootlevel` 与 `softlevel` 完全对应。唯一的区别在于，这里定义的是第二个“boot”运行级别，而不是第二个“default”运行级别。

## 环境变量

### 介绍

环境变量是一个命名的对象，其中包含一个或多个应用程序所使用的信息。许多用户（尤其是 Linux 新手）认为这有点诡异或难以管理。然而，这是一个误区：通过使用环境变量，用户可以轻松地更改一个或多个应用程序的配置设置。

### 重要示例

下表列出了 Linux 系统使用的若干变量并描述了它们的用途。

| 变量 | 描述 |
| :--- | :--- |
| `PATH` | 该变量包含用冒号分隔的目录列表，系统会在这些目录下查找可执行文件。如果输入的可执行文件名称（如 `ls`、`rc-update` 或 `emerge`），但该可执行文件不在列出的目录中，系统将不会执行它（除非使用完整路径作为命令，例如 `/bin/ls`）。 |
| `ROOTPATH` | 该变量的功能与 `PATH` 相同，但它只列出 root 用户输入命令时应该检查的目录。 |
| `LDPATH` | 该变量包含用冒号分隔的目录列表，动态链接器会在这些目录中搜索库文件。 |
| `MANPATH` | 该变量包含用冒号分隔的目录列表，`man` 命令在这些目录中查找帮助页。 |
| `INFODIR` | 该变量包含用冒号分隔的目录列表，`info` 命令在这些目录中查找 info 页面。 |
| `PAGER` | 该变量包含用于列出文件内容的程序路径（例如 `less` 或 `more`）。 |
| `EDITOR` | 该变量包含用于修改文件内容的程序路径（例如 `nano` 或 `vi`）。 |
| `KDEDIRS` | 该变量包含用冒号分隔的目录列表，包含 KDE 特有的材质。 |
| `CONFIG_PROTECT` | 该变量包含用空格分隔的目录列表，这些目录在更新期间应受 Portage 保护。 |
| `CONFIG_PROTECT_MASK` | 该变量包含用空格分隔的目录列表，这些目录在更新期间不应受 Portage 保护。 |

以下是这些变量的示例定义：

**上述变量的示例设置**

```
PATH="/bin:/usr/bin:/usr/local/bin:/opt/bin:/usr/games/bin"
ROOTPATH="/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin"
LDPATH="/lib:/usr/lib:/usr/local/lib:/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
MANPATH="/usr/share/man:/usr/local/share/man"
INFODIR="/usr/share/info:/usr/local/share/info"
PAGER="/usr/bin/less"
EDITOR="/usr/bin/vim"
KDEDIRS="/usr"
CONFIG_PROTECT="/usr/X11R6/lib/X11/xkb /opt/tomcat/conf \
/usr/kde/3.1/share/config /usr/share/texmf/tex/generic/config/ \
/usr/share/texmf/tex/platex/config/ /usr/share/config"
CONFIG_PROTECT_MASK="/etc/gconf"
```

## 全局定义变量

### env.d 目录

为了集中定义这些变量，Gentoo 引入了 `/etc/env.d/` 目录。在该目录下有许多文件，例如 `00basic`、`05gcc` 等，它们包含了名称中所述应用程序所需的变量。

例如，当安装 `gcc` 时，`ebuild` 会创建一个名为 `05gcc` 的文件，其中包含了以下变量的定义：`/etc/env.d/05gcc` **默认启用 gcc 的环境变量**

```
PATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
ROOTPATH="/usr/i686-pc-linux-gnu/gcc-bin/3.2"
MANPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/man"
INFOPATH="/usr/share/gcc-data/i686-pc-linux-gnu/3.2/info"
CC="gcc"
CXX="g++"
LDPATH="/usr/lib/gcc-lib/i686-pc-linux-gnu/3.2.3"
```

其他发行版可能会要求用户在 `/etc/profile` 或其他位置更改或添加此类环境变量定义。相反，Gentoo 让用户（以及 `Portage`）能够轻松地维护和管理环境变量，而无需关注那些可能包含环境变量的众多文件。

例如，当 `gcc` 更新时，`/etc/env.d/05gcc` 文件也会随之更新，而无需任何用户交互。

这不仅有利于 `Portage`，对用户也有益。有时用户可能会被要求在系统范围内设置某个特定的环境变量。以 `http_proxy` 变量为例。与其弄乱 `/etc/profile`，用户只需创建一个文件（例如 `/etc/env.d/99local`）并写入：`/etc/env.d/99local` **全局变量**

```
http_proxy="proxy.com:8080"
```




可能没有必要全局定义环境变量。例如，用户可能想将 `/home/my_user/bin` 和当前工作目录（用户所在的目录）添加到 `PATH` 变量中，但并不希望系统上的其他用户在他们的 `PATH` 中也包含这些路径。若要在本地定义环境变量，请使用 `~/.bashrc` 或 `~/.bash_profile`：

### 为本地使用扩展 PATH

```bash
# 冒号后若无目录，将被视为当前工作目录
PATH="${PATH}:/home/my_user/bin:"
```

注销并重新登录后，`PATH` 变量将会被更新。

### 会话特定

有时可能需要更严格的定义。例如，用户可能希望能够使用临时目录创建的二进制文件，但又不想直接使用二进制文件自身的路径，或不想在短暂需要时编辑 `~/.bashrc`。

在这种情况下，只需通过 `export` 命令在当前会话中定义 `PATH` 变量即可。只要用户不注销，`PATH` 变量将一直使用临时设置。

```bash
root # export PATH="${PATH}:/home/my_user/tmp/usr/bin"
```

引用自 "[`wiki.gentoo.org/index.php?title=Handbook:AMD64/Full/Working&oldid=181110`](http://wiki.gentoo.org/index.php?title=Handbook:AMD64/Full/Working&oldid=181110)"

*   此页面最后修改于 2014 年 12 月 13 日 18:45。
*   [隐私政策](https://wiki.gentoo.org/wiki/Gentoo_Wiki:Privacy_policy "Gentoo Wiki:Privacy policy")
*   [关于 Gentoo Wiki](https://wiki.gentoo.org/wiki/Gentoo_Wiki:About "Gentoo Wiki:About")
*   [免责声明](https://wiki.gentoo.org/wiki/Gentoo_Wiki:General_disclaimer "Gentoo Wiki:General disclaimer")
*   [https://twitter.com/gentoo @Gentoo on Twitter]
*   [https://plus.google.com/+Gentoo +Gentoo on Google+]
*   [https://www.facebook.com/gentoo.org Gentoo on Facebook]

**© 2001–2016 Gentoo Foundation, Inc.**

Gentoo 是 Gentoo Foundation, Inc. 的商标。除非另有明确说明，本文档的内容均根据 [CC-BY-SA-3.0](https://creativecommons.org/licenses/by-sa/3.0/) 许可发布。[Gentoo 名称和徽标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html) 适用。

![cover](img/cover_image.jpg)





# Gentoo Linux amd64 手册：使用 Portage

## 11 使用单一分支
### 11.1 稳定版 (Stable)
### 11.2 测试版 (Testing)

## 12 混合稳定版与测试版
### 12.1 `package.accept_keywords`
### 12.2 测试特定版本

## 13 屏蔽包 (Masked packages)
### 13.1 `package.unmask`
### 13.2 `package.mask`

## 14 `dispatch-conf`

## 15 `etc-update`

## 16 `quickpkg`

##目录
## 1 Portage 文件
### 1.1 配置指令
### 1.2 特定配置信息
### 1.3 用户特定配置
### 1.4 修改 Portage 文件和目录位置

## 2 存储文件
### 2.1 Portage 树 (Portage tree)
### 2.2 预编译二进制文件
### 2.3 源代码
### 2.4 Portage 数据库
### 2.5 Portage 缓存

## 3 编译软件
### 3.1 临时 Portage 文件
### 3.2 编译目录
### 3.3 Live 文件系统位置

## 4 特性
### 4.1 `ebuild`

## 5 配置

## 6 编译特定
### 6.1 配置 (Configure)
### 6.2 合并 (Merge)

## 7 配置
### 7.1 Portage
### 7.2 排除 (Excluding)

## 8 下载
### 8.1 服务器
### 8.2 获取 (Fetch)
### 8.3 Rsync

## 9 Gentoo 配置
### 9.1 分支选择
### 9.2 Portage

## 10 Portage 行为
### 10.1 资源管理
### 10.2 输出行为





# 12 稳定版（stable）与测试版的混合

## 12.1 `package.accept_keywords`

## 12.2 测试特定版本

# 13 屏蔽软件包（Masked packages）

## 13.1 `package.unmask`

## 13.2 `package.mask`

# 14 dispatch-conf

# 15 etc-update

# 16 quickpkg

# 17 使用 Portage 树子集

## 17.1 排除软件包和类别

# 18 添加非官方 ebuild

## 18.1 定义 Portage overlay 目录

## 18.2 使用多个 overlays 工作

# 19 非 Portage 维护的软件

## 19.1 使用 Portage 管理自维护软件

# 20 简介

# 21 软件包级别的环境变量

## 21.1 使用 `/etc/portage/env`

## 21.2 示例：为特定包使用调试

# 22 挂钩 emerge 过程

## 22.1 使用 `/etc/portage/bashrc` 及关联文件

## 22.2 示例：更新文件数据库

# 23 在 `--sync` 之后执行任务

## 23.1 使用 `/etc/portage/postsync.d` 位置

## 23.2 示例：运行 `eix-update`

# 24 覆盖配置（profile）设置

## 24.1 使用 `/etc/portage/profile`

## 24.2 示例：向系统添加 `nfs-utils`

# 25 应用非标准补丁

## 25.1 使用 `ebuild_user`

## 25.2 示例：为 Firefox 应用补丁

# Portage 文件

### 配置指令

Portage 附带了一个存储在 `/usr/portage/config/make.globals` 的默认配置。所有的 Portage 配置都通过变量处理。Portage 监听哪些变量以及这些变量的含义将在后文中描述。

由于许多配置指令在不同架构之间存在差异，Portage 还包含了系统的一部分的默认配置文件。该配置由 `/etc/portage/make.profile` 符号链接指向；Portage 的配置设置在配置配置及其所有父配置的 `make.defaults` 文件中。我们稍后会详细介绍关于配置（profiles）和 `/etc/portage/make.profile` 目录。

可以将 Portage 配置变量定义为环境变量，但我们不建议这样做。

### 配置特定信息

我们已经遇到过 `/etc/portage/make.profile` 目录了。实际上，它并不是一个目录，而是一个指向配置的符号链接，默认位于 `/usr/portage/profiles/` 内部的一个，尽管用户可以在其他地方创建自己的配置并指向它们。该符号链接指向的配置是系统所遵循的配置。

### 用户特定配置

当需要更改 Portage 安装软件的行为时，则需要修改 `/etc/portage/` 内部的一组文件。强烈建议使用 `/etc/portage/` 内的文件，并强烈不建议通过环境变量来覆盖行为！





*   `package.use` 列出了某些特定包使用的 `USE` 标记，而无需让整个系统都使用这些 `USE` 标记。

这些并不非要是文件；它们也可以是目录，每个包包含一个文件。关于 `/etc/portage/` 目录以及可以创建的所有文件的完整列表，可以查看 Portage 的 man 页面：

```
user $ man portage
```

### 更改 Portage 文件和目录位置

之前提到的配置文件无法存储在其他地方——Portage 始终会在这些确切的位置查找这些配置文件。然而，Portage 将许多其他位置用于各种用途：构建目录、源代码存储、Portage 树位置等……

所有这些用途都有著名的默认位置，但可以通过 `/etc/portage/make.conf` 根据个人喜好进行。本章的其余部分解释了 Portage 使用的特殊位置以及如何更改它们在文件系统中的位置。

不过，本文并非作为参考手册。为了获得 100% 的覆盖，请咨询 Portage 和 `make.conf` 的 man 页面：

```
user $ man portage
user $ man make.conf
```

### 存储文件

### Portage 树

Portage 树的默认位置是 `/usr/portage`。这由 `PORTDIR` 变量定义。当将 Portage 树存储在其他地方（通过更改此变量），不要忘记相应地更改 `/etc/portage/make.profile` 链接。

更改 `PORTDIR` 变量后，建议也更改以下变量，因为它们不会注意到 `PORTDIR` 的变化。这是由于 Portage 处理变量的方式：`PKGDIR`、`DISTDIR`、`RPMDIR`。

### 预编译二进制文件

尽管 Portage 默认使用预编译二进制文件，但它对它们有广泛的支持。当要求 Portage 使用预编译包时，它将在 `/usr/portage/packages` 中查找它们。该位置由 `PKGDIR` 变量定义。

### 源代码

应用程序源代码默认存储在 `/usr/portage/distfiles` 中。该位置由 `DISTDIR` 变量定义。

### Portage 数据库

Portage 将系统状态（安装了哪些包、哪些文件属于哪个包等）存储在 `/var/db/pkg` 中。

警告

不要手动修改这些文件！这可能会破坏 Portage 对系统的认知。

### Portage 缓存

Portage 缓存（包含修改时间、虚拟包、依赖树信息等）存储在 `/var/cache/edb` 中。该位置确实是一个缓存：如果用户在此时没有运行任何 Portage 相关应用程序，可以清理它。

### 编译软件

### 临时 Portage 文件

Portage 的临时文件默认存储在 `/var/tmp/` 中。这由 `PORTAGE_TMPDIR` 变量定义。

更改 `PORTAGE_TMPDIR` 变量时，建议也更改以下变量，因为它们不会注意到 `PORTAGE_TMPDIR` 的变化。这是由于 Portage 处理变量的方式：`BUILD_PREFIX`。

### 构建目录

Portage 为其  的每个包在 `/var/tmp/portage/` 内部创建特定的构建目录。该位置由 `BUILD_PREFIX` 变量定义。

### 实时文件系统位置

默认情况下，Portage 所有文件安装在当前文件系统（`/`）上，但可以通过设置 `ROOT` 环境变量更改。这在创建新的构建镜像时非常有用。

### 日志功能

### Ebuild 日志

Portage 可以为每个 ebuild 创建日志文件，但只有当 `PORT_LOGDIR` 变量被设置为 Portage（通过 Portage 用户）可写的位置时才可以实现。默认情况下，此变量未设置。如果未设置 `PORT_LOGDIR`，则当前的日志系统将不会有任何构建日志，尽管用户可能会从新的 elog 支持接收某些日志。

如果未定义 `PORT_LOGDIR` 使用了 elog，则构建日志和由 elog 保存的任何其他日志将可用，如下文所示。

Portage 通过使用 `elog` 对日志提供精粒度的控制：

*   `PORTAGE_ELOG_CLASSES`：用户可以在此处定义要记录什么类型的消息。可以是 info、warn、error、log 和 qa 的任何以空格分隔的组合。

    *   info: 记录 ebuild 打印的 "einfo" 消息
    *   warn: 记录 ebuild 打印的 "ewarn" 消息
    *   error: 记录 ebuild 打印的 "eerror" 消息
    *   log: 记录某些 ebuild 中找到的 "elog" 消息
    *   qa: 记录 ebuild 打印的 "QA Notice" 消息

*   `PORTAGE_ELOG_SYSTEM`：这选择处理日志消息的模块。如果留空，则禁用日志。可以使用 save、custom、syslog、mail、save_summary 和 mail_summary 的任何以空格分隔的组合。为了使用 elog，必须使用一个模块。

    *   save: 在 `$PORT_LOGDIR/elog` 中为每个包保存一个日志，如果未定义 `$PORT_LOGDIR` 则存储在 `/var/log/portage/elog`。
    *   custom: 将所有消息传递给 `$PORTAGE_ELOG_COMMAND` 中用户定义的命令；稍后将讨论。
    *   syslog: 将所有消息发送到已安装的系统记录器。
    *   mail: 将所有消息传递给 `$PORTAGE_ELOG_MAILURI` 中用户定义的邮件服务器；稍后将讨论。elog 的邮件功能需要 `>=portage-2.1.1`。
    *   save_summary: 类似于 save，但它会合并 `$PORT_LOGDIR/summary.log` 中的所有消息，如果未定义 `$PORT_LOGDIR` 则存储在 `/var/log/portage/summary.log`。
    *   mail_summary: 类似于 mail，但会在 emerge 退出时发送所有消息。

*   `PORTAGE_ELOG_COMMAND`：仅在启用 custom 模块时使用。用户可以指定一个命令来处理日志消息。注意，该可以使用两个变量：`${PACKAGE}` 是包名和版本，而 `${LOGFILE}` 是日志文件的绝对路径。例如：

示例 PORTAGE_ELOG_COMMAND

```
PORTAGE_ELOG_COMMAND="/path/to/logger -p '${PACKAGE}' -f '${LOGFILE}'
```

### Portage 配置

如之前所述，可以通过许多变量对 Portage 配置，这些变量应该定义在 `/etc/portage/make.conf` 或 `/etc/portage/` 的一个子目录下。请参考 `make.conf` 和 portage man 页面以获取更多完整的信息：

```
user $ man make.conf
user $ man portage
```

### 构建特有选项

### 配置和编译器选项

当 Portage 构建应用程序时，会将以下变量的内容传递给编译器和配置脚本：

*   `CFLAGS` 和 `CXXFLAGS` 定义了 C 和 C++ 编译所需的编译器标志。
*   `CHOST` 定义了应用程序配置脚本的构建主机信息。
*   `MAKEOPTS` 传递给 make 命令，通常用于定义编译期间使用的并行度。关于 make 选项的更多信息可以在 make man 页面中找到。

`USE` 变量在配置和编译期间也会使用，但在之前的章节中已详细解释过。

### 合并选项

当 Portage 合并了某个软件标题的新版本时，它将从系统中删除旧版本的过时文件。Portage 在卸载旧版本之前会给用户 5 秒延迟。这 5 秒由 `CLEAN_DELAY` 变量定义。

可以通过设置 `EMERGE_DEFAULT_OPTS` 告诉 emerge 每次运行时使用某些选项。一些实用的选项包括 `--ask`、`--verbose`、`--tree` 等。

### 配置文件保护

### Portage 保护的位置

如果文件没有存储在受保护的位置，Portage 将覆盖软件新版本提供的文件。这些受保护的位置由 `CONFIG_PROTECT` 变量定义，通常是配置文件的位置。目录列表由空格分隔。

将写入此类受保护位置的文件将将被重命名，并警告用户存在（推测的）配置文件的新版本。




要查询当前的 `CONFIG_PROTECT` 设置，请使用 `emerge --info` 输出：

```
user $ emerge --info | grep 'CONFIG_PROTECT='
```

关于 Portage 配置文件保护的更多信息，请参阅 `emerge` 手页中的 `CONFIGURATION FILES` 章节：

```
user $ man emerge
```

### 排除目录

用户可以使用 `CONFIG_PROTECT_MASK` 变量来“取消保护”受保护位置的某些子目录。

## 下载选项### 服务器位置

当系统无法提供所需的信息或数据时，Portage 将从互联网检索。。各种信息和数据通道的服务器位置由以下变量定义：

- `GENTOO_MIRRORS` 定义了包含源码（distfiles）的服务器位置列表。
- `PORTAGE_BINHOST` 定义了包含系统预编译包的特定服务器位置。

第三个设置涉及 rsync 服务器的地址，用户使用它来更新 Portage 树。这定义在 `/etc/portage/repos.conf` 文件中（如果该路径被定义为一个目录，则定义在该目录内部的文件中）：

- `sync-type` 定义服务器类型，默认为 `rsync`。
- `sync-uri` 定义 Portage 用来获取 Portage 树的特定服务器。

`GENTOO_MIRRORS`、`sync-type` 和 `sync-uri` 变量可以通过 `mirrorselect` 自动设置。当然，在使用之前需要先安装 [app-portage/mirrorselect](https://packages.gentoo.org/packages/app-portage/mirrorselect)。欲需更多信息，请查看 mirrorselect 的在线帮助：

```
user $ mirrorselect --help
```

如果环境需要使用代理服务器，可以声明 `http_proxy`、`ftp_proxy` 和 `RSYNC_PROXY` 变量。

### 获取命令

当 Portage 需要获取源码时，它默认使用 `wget`。可以通过 `FETCHCOMMAND` 变量进行更改。

Portage 能够恢复部分下载的源码。它它默认使用 `wget`，但可以通过 `RESUMECOMMAND` 变量进行修改。

确保 `FETCHCOMMAND` 和 `RESUMECOMMAND` 将源码存储在正确的位置。在变量内部，可以使用 `${URI}` 和 `${DISTDIR}` 变量分别指向源码位置和 distfiles 位置。

还可以定义特定协议的句处理器，如 `FETCHCOMMAND_HTTP`、`FETCHCOMMAND_FTP`、`RESUMECOMMAND_HTTP`、`RESUMECOMMAND_FTP` 等。

### Rsync 设置

无法更改 Portage 更新 Portage 树时使用的 `rsync` 命令，但可以设置与 `rsync` 命令相关的变量：

- `PORTAGE_RSYNC_OPTS` 设置同步期间使用的若干默认变量，变量之间用空格分隔。除非你完全清楚自己在做什么，否则不应更改。请注意，即使 `PORTAGE_RSYNC_OPTS` 为空，某些绝对必要的选项始终会被。
- `PORTAGE_RSYNC_EXTRA_OPTS` 可用于同步时设置额外选项。每个选项应用空格分隔。
    - `--timeout=<number>`：定义了 `rsync` 连接在被视为超时之前可以空闲的秒数。该变量默认为 `180`，但拨号用户或电脑慢的用户可能希望将其设置为 `300` 或更高。
    - `--exclude-from=/etc/portage/rsync_excludes`：指向一个文件，该文件列出了 `rsync` 在更新过程中应该忽略的包和/或分类。在这种情况下，指向 `/etc/portage/rsync_excludes`。
    - `--quiet`：减少屏幕输出。
    - `--verbose`：打印完整的文件列表。
    - `--progress`：为每个文件显示进度条。
- `PORTAGE_RSYNC_RETRIES` 定义了 `rsync` 在放弃之前尝试连接到 `SYNC` 变量指向的镜像的次数。该变量默认为 `3`。

关于这些或其他选项的更多信息，请阅读 `man rsync`。

## Gentoo 配置### 分支选择

可以使用 `ACCEPT_KEYWORDS` 变量更改默认分支。它默认架构的稳定分支。关于 Gentoo 分支的更多信息可以在下一章找到。

### Portage 特性

可以通过 `FEATURES` 变量激活某些 Portage 特性。Portage 特性在之前的章节中讨论过。

## Portage 行为### 资源管理

通过 `PORTAGE_NICENESS` 变量，用户可以增加或减少  时的 nice 值。`PORTAGE_NICENESS` 的值会加到当前的 nice 值上。

关于 nice 值的更多信息，请参阅 `nice` 手页：

```
user $ man nice
```

### 输出行为

`NOCOLOR` 变量默认为 `false`，定义 Portage 是否应该禁用彩色输出。

## 使用单一分支### 稳定

`ACCEPT_KEYWORDS` 变量定义了系统使用的软件分支。它默认为系统架构（例如 amd64）的稳定软件分支。

建议坚持稳定分支。然而，如果稳定性不是那么重要，或者管理员想通过向 [`bugs.gentoo.org`](https://bugs.gentoo.org/) 提交错误报告来帮助 Gentoo，可以使用测试分支。

### 测试

为了使用更新的软件，用户可以考虑使用测试分支。要让 Portage 使用测试分支，请在架构前添加一个 `~`。

测试分支正如其名——测试中（Testing）。如果一个包处于测试阶段，意味着开发者认为它是功能正常的，但尚未经过彻底测试。使用测试分支的用户很可能是第一个发现包中漏洞的人，在这种情况下他们应该提交错误报告让开发者知道。

但请注意；使用测试分支可能会导致稳定性问题、不完美的包处理（例如错误/缺失依赖项）、过于频繁的更新（导致大量编译）或损坏的包。对于不知道 Gentoo 工作原理以及如何解决问题的用户，我们建议坚持稳定和测试分支。

例如，要为 amd64 架构选择测试分支，编辑 `/etc/portage/make.conf` 并设置：FILE `/etc/portage/make.conf` 使用测试分支

```
 ACCEPT_KEYWORDS="~amd64"
```

从稳定切换到测试时，用户会发现有很多包将得到更新。请记住，移动到测试分支后，返回稳定分支可能具有挑战性。

## 混合稳定与测试### package.accept_keywords

可以要求 Portage 为特定包允许测试分支，对系统的其余部分使用稳定分支。要实现这一点，请在 `/etc/portage/package.accept_keywords` 中添加包类别和名称。也可以创建一个（同名的）目录，并在目录下的文件中列出包。

例如，为 gnumeric 使用测试分支：FILE `/etc/portage/package.accept_keywords` 仅为 gnumeric 应用使用测试分支

```
 app-office/gnumeric
```

### 测试特定版本

要使用测试分支中的特定软件版本，但不想让 Portage 对后续版本使用测试分支，请在 `package.accept_keywords` 位置添加版本。在这种情况下使用 `=` 操作符。也可以使用 `<=`、`<`、>` 或 `>=` 运算符输入版本范围。

任何情况下，如果添加了版本信息，*必须*使用运算符。如果没有版本信息，则不能使用运算符。

在以下示例中，我们要求 Portage 即使在 gnumeric-1.2.13 处于测试分支也允许安装它：FILE `/etc/portage/package.accept_keywords` 允许选择特定版本

```
 =app-office/gnumeric-1.2.13
```

## 屏蔽包### package.unmask

**重要**




Gentoo 开发者不支持使用取消屏蔽（unmasking）包。在进行此类操作时请务必谨慎。与 `package.unmask` 和/或 `package.mask` 相关的支持请求可能无法得到回复。

当包被 Gentoo 开发者屏蔽后，尽管在 `package.mask` 文件（默认位于 `/usr/portage/profiles/`）中提到了原因，用户仍想使用该包，则将所需的版本（通常是与配置中 `package.mask` 文件中完全相同的行）添加到 `/etc/portage/package.unmask` 文件中（或如果该位置是一个目录，则添加到该目录下的某个文件中）。

例如，如果 `=net-mail/hotwayd-0.8` 被屏蔽，则可以通过在 `package.unmask` 位置添加完全相同的行来取消屏蔽：文件 `/etc/portage/package.unmask`取消屏蔽特定的包/版本

```
 =net-mail/hotwayd-0.8
```

**注意**

如果 `/usr/portage/profiles/package.mask` 中的条目包含包版本范围，则有必要仅取消屏蔽实际需要的版本。请阅读上一节以了解如何指定版本。

### package.mask

也可以要求 Portage 不考虑某个包或包的特定版本。要要操作，请通过向 `/etc/portage/package.mask` 位置添加适当的行（在该文件中或该目录下的某个文件中）来屏蔽该包。

例如，为了防止 Portage 安装新于 `gentoo-sources-2.6.8.1` 的内核源码，请在 `package.mask` 位置添加以下行：文件 `/etc/portage/package.mask` 屏蔽版本大于 2.6.8.1 的 gentoo-sources

```
 >sys-kernel/gentoo-sources-2.6.8.1
```

## dispatch-conf

`dispatch-conf` 是一个辅助合并 `._cfg0000_<name>` 文件的工具。当 Portage 想要覆盖受 `CONFIG_PROTECT` 变量保护的目录中的文件时，会生成 `._cfg0000_<name>` 文件。

通过 `dispatch-conf`，用户可以在合并配置文件的更新的同时跟踪所有更改。`dispatch-conf` 将配置文件之间的差异存储为补丁或使用 RCS 版本控制系统。这意味着如果某人在更新配置文件时犯错，管理员可以随时将文件回滚到之前的版本。

使用 `dispatch-conf` 时，用户可以请求保持配置文件不变、使用新的配置文件、编辑当前文件或交互式地合并更改。`dispatch-conf` 还有一些实用的额外功能：

* 自动合并仅包含注释更新的配置文件更新
* 自动合并仅在空格数量上不同的配置文件

先编辑 `/etc/dispatch-conf.conf` 并创建 `archive-dir` 变量引用的目录。然后执行 `dispatch-conf`：

```
root # dispatch-conf
```

运行 `dispatch-conf` 时，每个更改的配置文件将一个接一个通过审查。按 `u` 更新（替换）当前配置文件为新文件并继续处理下一个文件。按 `w` 消除（删除）新配置文件并继续处理下一个文件。一旦处理完所有配置文件，`dispatch-conf` 将退出。在任何时候都可以使用 `q` 退出应用程序。

欲更多信息，请查看 `dispatch-conf` 帮助页。它描述了如何交互式地合并当前和新的配置文件、编辑新配置文件、检查文件之间的差异等。

```
user $ man dispatch-conf
```

## etc-update

另一个合并配置文件的工具是 `etc-update`。它不像 `dispatch-conf` 那么简单，功能也没有那么全，但它确实提供了交互式合并设置，并可以自动合并微小更改。

然而，与 `dispatch_conf` 不同，`etc-update` 不保留配置文件的旧版本。一旦文件更新，旧版本将永远消失。非常小心，因为在希望保留旧配置文件时使用 `etc-update` 的安全性远低于使用 `dispatch-conf`。

```
root # etc-update
```

在合并简单的更改后，将提供一个等待更新的保护文件列表。底部显示了可能的选项：

etc-update 提供的选项

```
 输入相应的数字选择要编辑的文件。
              (-1 退出) (-3 自动合并所有剩余文件)
                           (-5 自动合并但不使用 'mv -i'):
```

输入 `-1` 时，`etc-update` 将退出并停止任何其他更改。使用 `-3` 或 `-5`，所有列出的配置文件将被用新版本覆盖。因此，首先选择不应自动更新的配置文件非常重要。只需输入该配置文件左侧列出的数字即可。

例如，我们选择了配置文件 `/etc/pear.conf`：

更新特定的配置文件

```
 /etc/pear.conf 和 /etc/._cfg0000_pear.conf 之间的差异开始
[...]
 /etc/pear.conf 和 /etc/._cfg0000_pear.conf 之间的差异结束
1) 用更新替换原始文件
2) 删除更新，保持原始不变
3) 交互式合并原始文件与更新
4) 再次显示差异
```

显示两个文件之间的差异。如果更新后的配置文件可以无问题使用，输入 `1`。如果不需要更新后的配置文件，或者它没有提供任何新的有用信息，输入 `2`。如果必须交互式更新当前配置文件，输入 `3`。

这里没有必要进一步阐述交互式合并。为了完整起见，我们将列出在交互式合并两个文件时可以使用的命令。用户将看到两行（原始文件和建议的新文件）以及一个提示，用户可以输入以下命令之一：

交互式合并可用的命令

```
 ed:     编辑并使用两个版本，每个版本都带有头信息。
eb:     编辑并使用两个版本。
el:     编辑并使用左侧版本。
er:     编辑并使用右侧版本。
e:      编辑一个新版本。
l:      使用左侧版本。
r:      使用右侧版本。
s:      静默包含公共行。
v:      详细包含公共行。
q:      退出。
```

在完成重要配置文件的更新后，用户可以自动更新所有其他配置文件。如果 `etc-update` 找不到更多可更新的配置文件，它将退出。

## quickpkg

通过 `quickpkg`，用户可以创建系统中已合并包的存档。这些存档可以作为预构建包使用。运行 `quickpkg` 非常简单：只需将要归档的包名添加。

例如，归档 `curl`、`orage` 和 `procps`：

```
root # quickpkg curl orage procps
```

预构建包将存储在 `$PKGDIR` 中（默认 `/usr/portage/packages/`）。这些包被放在 `$PKGDIR/CATEGORY`。

## 使用 Portage 树的子集

### 排除包和类别

可以选择性更新某些类别/包并忽略其他类别/包。这可以通过在 `emer --sync` 步骤中让 rsync 排除类别/包来实现。

在 `/etc/portage/make.conf` 的 `PORTAGE_RSYNC_EXTRA_OPTS` 变量中定义包含排除模式的文件：文件 `/etc/portage/make.conf`定义排除文件

```
 PORTAGE_RSYNC_EXTRA_OPTS="--exclude-from=/etc/portage/rsync_excludes"
```

文件 `/etc/portage/rsync_excludes`排除所有游戏

```
 games-*/*
```

但请注意，这可能会导致依赖问题，因为新的允许包可能依赖于新的但排除的包。

## 添加非官方 ebuild

### 定义 Portage 覆盖层（overlay）目录




你可以要求 Portage 使用并非通过 Portage 树中官方提供的 ebuilds。创建一个新目录（例如 `/usr/local/portage`）来存储这些第三方 ebuilds。请确保使用与官方 Portage 树相同的目录结构！

然后，在 `/etc/portage/make.conf` 中定义 `PORTDIR_OVERLAY` 并让其指向之前定义的目录。现在使用 Portage 时，它也会考虑这些 ebuilds，且在下次运行 `emerge --sync` 时不会删除或覆盖这些 ebuilds。

### 与多个覆盖层（Overlays）一起工作

对于那些在多个覆盖层上进行开发、想在包进入 Portage 树之前对其进行测试，或仅仅想从各种来源使用非官方 ebuilds 的高级用户，[app-portage/layman](https://packages.gentoo.org/packages/app-portage/layman) 软件包提供了 layman，这是一个帮助用户保持覆盖层仓库更新的工具。

首先，按照[覆盖层用户指南](https://wiki.gentoo.org/wiki/Project:Overlays/User_Guide "Project:Overlays/User Guide") 所示安装并配置 layman，然后使用 `layman -a` 添加所需的仓库。

例如，启用 hardened-development 覆盖层：

```
root # layman -a hardened-development
```

无论通过 `layman` 使用多少个仓库，都可以通过以下命令更新所有仓库：

```
root # layman -S
```

关于与覆盖层一起工作的更多信息，请参阅 `man layman` 以及之前链接的 layman/overlay 用户指南。

## 非 Portage 维护的软件

### 使用 Portage 管理自维护的软件

有时，用户希望单独配置、安装和维护软件，而不让 Portage 自动化该过程，尽管 Portage 可以提供这些软件版本。已知案例包括内核源码和 nvidia 驱动程序。可以配置 Portage，使其知道某个包是在系统上手动安装的（从而在计算依赖关系时考虑此信息）。这一过程被称为*注入*（*injecting*），Portage 通过 `/etc/portage/profile/package.provided` 文件支持此操作。

例如，要让 Portage 知道手动安装的 `gentoo-sources-2.6.11.6`，请向 `/etc/portage/profile/package.provided` 添加以下行：FILE `/etc/portage/package.provided` 将 `gentoo-sources-2.6.11.6` 标记为手动安装

```
sys-kernel/gentoo-sources-2.6.11.6
```

**注意**

这是一个使用*不带*操作符版本的文件。

### 简介

对于大多数用户来说，目前获得的信息已足够完成所有的 Linux 操作。但 Portage 的功能远不止于此；许多功能是针对高级用户的，或仅适用于特定的边缘情况。尽管如此，这不应成为不记录它们的借口。

当然，极大的灵活性意味着大量的潜在用例。在这里是不可能记录所有内容的。相反，我们希望关注一些通用问题，然后这些问题可以根据个人需求进行弯曲。更多的调整和技巧可以在 Gentoo Wiki 各处找到。

这些额外功能（如果不是全部的话）都可以通过翻阅 Portage 提供的手册页轻松找到：

```
user $ man portage
user $ man make.conf
```

最后请记住，这些都是高级功能，如果操作不当，可能会调试和故障排除变得非常困难。在遇到 bug 并提交 bug 报告时，请务必提到这些内容。

## 包级环境变量

### 使用 /etc/portage/env

默认情况下，包编译将使用在 `/etc/portage/make.conf` 中定义的环境变量，如 `CFLAGS`、`MAKEOPTS` 等。但在某些情况下，为特定包提供不同的变量可能会是有益的。为此，Portage 支持使用 `/etc/portage/env` 和 `/etc/portage/package.env`。

`/etc/portage/package.env` 文件包含了需要差异化环境变量的包列表，以及一个告诉 Portage 执行哪些更改的特定标识符。标识符的名称格式任意，Portage 将在 `/etc/portage/env/IDENTIFIER` 文件中查找变量。

### 示例：为特定包启用调试

作为一个示例，我们为 [media-video/mplayer](https://packages.gentoo.org/packages/media-video/mplayer) 包启用调试功能。

首先，在名为 `/etc/portage/env/debug-cflags` 的文件中设置调试变量。该名称是任意选择的，但当然反映了差异的原因，以便以后更清楚地说明为什么要设置差异。

FILE `/etc/portage/env/debug-cflags` 调试专用变量

```
CFLAGS="-O2 -ggdb -pipe"
FEATURES="${FEATURES} nostrip"
```

接下来，我们标记 [media-video/mplayer](https://packages.gentoo.org/packages/media-video/mplayer) 包以使用这些内容：FILE `/etc/portage/package.env` 为 mplayer 包使用 `debug-cflags`

```
media-video/mplayer debug-cflags
```

## 挂钩 emerge 过程

### 使用 /etc/portage/bashrc 和关联文件

当 Portage 处理 ebuilds 时，它使用一个 bash 环境，在其中它调用各种构建函数（如 `src_prepare`、`src_configure`、`pkg_postinst` 等）。但 Portage 也允许用户设置特定的 bash 环境。

使用特定 bash 环境的优势是它允许用户挂钩（hook）emer 过程。

使用特定 bash 环境的好处是它允许用户在执行每个步骤时挂钩。这可以通过 `/etc/portage/bashrc` 实现，也可以通过使用包级环境（通过 `/etc/portage/env`，如前所述）来实现。

为了挂钩该过程，bash 环境可以监听 `EBUILD_PHASE`、`CATEGORY` 等变量。根据这些变量的值，可以执行额外的步骤/函数。

### 示例：更新文件数据库

在示例中，我们将使用 `/etc/portage/bashrc` 调用某些文件数据库程序，以确保它们的数据库是最新的。示例中使用的应用程序 `aide`（一种入侵检测工具）和 `updatedb`（配合 mlocate 使用），但这些仅作为示例。为了这种情况使用 `/etc/portage/bashrc`，我们需要挂钩 `postrm`（删除文件）和 `postinst`（安装文件）函数，因为此时文件系统发生了变化。

FILE `/etc/portage/bashrc` 挂钩 postinst 和 postrm 阶段

```
if [ "${EBUILD_PHASE}" == "postinst" ] || [ "${EBUILD_PHASE}" == "postrm" ];
then
  echo ":: Calling aide --update to update its database";
  aide --update;
  echo ":: Calling updatedb to update its database";
  updatedb;
fi
```




默认情况下，Gentoo 使用由 `/etc/portage/make.profile` 指向的配置（指向正确配置目录的符号链接）包含的设置。这些配置定义了特定的设置，并通过其父文件从其他配置中继承设置。

通过使用 `/etc/portage/profile`，用户可以覆盖配置设置，例如 `packages`（哪些包被视为系统集的一部分）、强制使用的标志（flags）等。

### 示例：将 nfs-utils 添加到系统集

当对于关键的文件系统使用基于 NFS 的文件系统时，可能需要将 [net-fs/nfs-utils](https://packages.gentoo.org/packages/net-fs/nfs-utils) 标记为系统包，这样如果管理员尝试卸载（unmerge）它，Portage 将向其发出强烈警告。

要实现这一点，我们将包添加到 `/etc/portage/profile/packages` 中，并在前面加上一个 `*`：FILE `/etc/portage/profile/packages` 将 nfs-utils 标记为系统包

```
 *net-fs/nfs-utils
```

### 应用非标准补丁

#### 使用 epatch_user

为了以类似的方式管理多个 ebuild，ebuild 开发人员使用 eclasses（类似于 shell 库）来定义常用的函数。这些 eclasses 中的之一是 `eutils.eclass`，它提供了一个名为 `epatch_user` 的有趣函数。

`epatch_user` 函数应用位于 `/etc/portage/patches/<category>/<package>[-<version>[-<revision>]` 的源码补丁，取决于先找到哪个目录遗憾的是，并不是所有的 ebuild 都会自动调用此函数，因此仅将补丁放在此位置并不总是有效。

幸运的是，根据本章前面提供的信息，用户可以通过挂钩（例如挂钩 prepare 阶段）来调用此函数。函数可以根据需要多次调用——它只会应用一次补丁。

#### 示例：对 Firefox 应用补丁

[www-client/firefox](https://packages.gentoo.org/packages/www-client/firefox) 包是许多已经在 ebuild 内部调用 `epatch_user` 的包之一，因此不需要覆盖任何特定内容。

如果出于某种原因（例如开发者提供了一个补丁并要求检查是否修复了报告的错误），想要对 Firefox 进行补丁，则只需要将补丁放在 `/etc/portage/patches/www-client/firefox` 中（最好使用完整名称和版本，以确保补丁不会干扰后续版本）并重新编译 Firefox。

取自 "[`wiki.gentoo.org/index.php?title=Handbook:AMD64/Full/Portage&oldid=181108`](http://wiki.gentoo.org/index.php?title=Handbook:AMD64/Full/Portage&oldid=181108)"

*   此页面最后修改于 2014 年 12 月 13 日 18:44。
*   [隐私政策](https://wiki.gentoo.org/wiki/Gentoo_Wiki:Privacy_policy "Gentoo Wiki:Privacy policy")
*   [关于 Gentoo Wiki](https://wiki.gentoo.org/wiki/Gentoo_Wiki:About "Gentoo Wiki:About")
*   [免责声明](https://wiki.gentoo.org/wiki/Gentoo_Wiki:General_disclaimer "Gentoo Wiki:General disclaimer")
*   [](https://twitter.com/gentoo "@Gentoo on Twitter")
*   [](https://plus.google.com/+Gentoo "+Gentoo on Google+")
*   [](https://www.facebook.com/gentoo.org "Gentoo on Facebook")

**© 2001–2016 Gentoo Foundation, Inc.**

Gentoo 是 Gentoo Foundation, Inc. 的商标。除非另有明确说明，本文档的内容均根据 [CC-BY-SA-3.0](https://creativecommons.org/licenses/by-sa/3.0/) 许可协议发布。[Gentoo 名称和标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html) 适用。![cover](img/cover_image.jpg)

## 目录

*   Gentoo Linux amd64 手册 - 网络配置 - Gentoo Wiki
*   gentoo.org 站点
*   导航
*   搜索
*   1 入门
*   2 高级配置
*   3 网络依赖
*   4 变量名与值
*   5 网络命名
*   5.1 工作原理
*   5.2 使用旧式命名
*   5.3 使用自定义名称
*   6 网络模块
*   7 接口处理器
*   8 DHCP
*   9 PPPoE
*   10 IP（自动分配）
*   11 绑定
*   12 桥接 (802.1d)
*   13 接口地址
*   14 隧道
*   15 VLAN (802.1q)
*   16 介绍
*   17 WPA supplicant
*   18 无线工具





# Gentoo Linux amd64 手册：网络配置

来自 Gentoo Wiki [AMD64 手册](https://wiki.gentoo.org/wiki/Special:MyLanguage/Handbook:AMD64 "Special:MyLanguage/Handbook:AMD64") | [完整版](https://wiki.gentoo.org/wiki/Special:MyLanguage/Handbook:AMD64/Full "Special:MyLanguage/Handbook:AMD64/Full")
跳转到：导航, 搜索

## 目录

* 1 开始上手
* 2 高级配置
* 3 网络依赖项
* 4 变量名与值
* 5 网络接口命名
    * 5.1 工作原理
    * 5.2 使用旧式内核命名
    * 5.3 使用自定义名称
* 6 网络模块
* 7 接口处理器
* 8 DHCP
* 9 带有 PPPoE/PPPoA 的 ADSL
* 10 APIPA (自动私有 IP 地址)
* 11 绑定 (Bonding)
* 12 桥接 (支持 802.1d)
* 13 MAC 地址
* 14 隧道化 (Tunneling
* 15 VLAN (支持 802.1q)
* 16 导言
* 17 WPA supplicant
* 18 无线工具
    * 18.1 初始设置与托管模式
    * 18.2 使用旧式内核命名
    * 18.3 使用自定义名称
]

## 1 开始上手

**注意**

本文档假设用户已经正确配置了系统，并知道接口名称。它也将假设要配置的接口是 `eth0`，这只是一个例子。

为了开始配置网络，首先让 Gentoo RC 系统知道该接口。这是通过在 `/etc/init.d` 中创建 `net.lo` 到 `eth0`（或者您的实际接口名称）的符号链接来实现。

```bash
root # cd /etc/init.d
root # ln -s net.lo net.eth0
```

Gentoo RC 系统现在知道该接口了。它还需要知道如何配置它。所有的网络接口都在 `/etc/conf.d` 中配置。以下是 DHCP 和静态地址的配置示例。

文件 `/etc/conf.d` 示例

```bash
# 用于 DHCP
config_eth0="dhcp"

# 使用 CIDR 格式的静态 IP
config_eth0="192.168.0.7/24"
routes_eth0="default via 192.168.0.1"
dns_servers_eth0="192.168.0.1 8.8.8.8"

# 使用掩掩码格式的静态 IP
config_eth0="192.168.0.7 netmask 255.255.255.0"
routes_eth0="default via 192.168.0.1"
dns_servers_eth0="192.168.0.1 8.8.8.8"
```

**注意**

如果某个接口没有提到配置，则假设使用 DHCP。

**注意**

CIDR 代表无类域间路由。最初，IPv4 地址被分为 A、B、C 类。早期的分类系统没有预见到互联网的巨大普及，现在面临着新的唯一地址耗尽的风险。CIDR 允许一个 IP 地址指定多个 IP 地址。CIDR IP 地址看起来和普通的 IP 地址一样，只是在结尾多了一个斜杠和一个数字，例如 `192.168.0.0/16`。CIDR 在 [RFC 1519](https://tools.ietf.org/html/rfc1519) 中有描述。

现在接口已经配置好了，我们可以使用以下命令来启动和停止它：





`root # /etc/init.d/net.eth0 start`
`root # /etc/init.d/net.eth0 stop` 这里的

在排排除网络故障时，请查看 `/var/log/rc.log`。除非在 `/etc/rc.conf` 中将 `rc_logger` 变量设置为 `NO`，否则启动活动的信息将存储在在该日志文件中。

现在网络接口已经成功停止并启动，下一步是让它在 Gentoo 启动时自动启动。以下是实现方法：

`root # rc-update add net.eth0 default`
`root # rc`

## 进级配置

`config_eth0` 变量是接口配置的核心。它是一个用于配置接口（在本例中为 `eth0`）的高级指令列表。指令列表中的每个命令都按顺序执行。如果至少有一个命令执行成功，则认为接口是正常的（OK）。

以下是内置指令列表：

| Value | 描述 |
| :--- | :--- |
| `null` | 什么都不做。 |
| `noop` | 如果接口已启动且存在地址，则成功终止配置。 |
| 一个 IPv4 或 IPv6 地址 | 将地址添加到接口。 |
| `dhcp`, `adsl`, 或 `apipa`（或来自第三方模块的自定义值） | 运行提供该命令的模块。例如，`dhcp` 将运行提供 DHCP 的模块，该模块可以通过 `dhcpcd`、`dhclient` 或 `pump` 服务。 |

如果某个命令失败，请指定一个回退值。回退值必须与配置结构完全匹配。

可以将这些值链联起来。这里是一些真实世界的示例：文件 `/etc/conf.d/net` 配置示例

## 网络依赖

`/etc/init.d/` 中的初始化脚本可以依赖于特定的网络接口，也可以仅依赖于 "net"。Gentoo 初始化系统中的所有网络接口都提供所谓的 "net"。

如果在 `/etc/rc.conf` 中，将 `rc_depend_strict` 变量设置为 `YES`，则在假设满足对 "net" 的依赖关系之前，所有提供 "net" 的网络接口都必须处于激活状态。换句话说，如果一个系统有 `net.eth0` 和 `net.eth1`，并且一个初始化脚本依赖于 "net"，那么两者都必须启用。

相反，如果设置了 `rc_depend_strict="NO"`，那么只要至少有一个网络接口启动，"net" 依赖就会被标记为已解决。

但是 `net.br0` 依赖于 `net.eth0` 和 `net.eth1` 呢？`net.eth1` 可能是一个无线或 PPP 设备，在被添加到网接器之前需要进行配置。这不能在 `/etc/init.d/net.br0` 中完成，因为它是 `net.lo` 的符号链接。

答案是在 `/etc/conf.d/net` 中定义一个 `rc_need_` 设置：文件 `/etc/conf.d/net` 添加对 net.br0 的依赖

```
rc_need_br0="net.eth0 net.eth1"
```

然而，仅靠这一点是不够的。Gentoo 的网络初始化脚本使用一个名为 "net" 的虚拟依赖来通知系统网络何时可用。显然，在上述情况下，网络只有在 `net.br0` 启动时才应该被标记为可用，而不是当其他接口启动时。因此，我们同样需要在 `/etc/conf.d/net` 中说明这一点：文件 `/etc/conf.d/net` 更新虚拟依赖和网络准备

```
rc_net_lo_provide="!net"
rc_net_eth0_provide="!net"
rc_net_eth1_provide="!net"
```

关于依赖关系的更详细讨论，请参阅 Gentoo Handbook 中关于编写初始化脚本的章节。关于 `/etc/rc.conf` 的更多信息可以在该文件的注释中。

## 变量名和值

变量名是动态的。它们通常遵循 `variable_${interface|mac|essid|apmac}` 的结构。例如，变量 `dhcpcd_eth0` 保存 `eth0` 的 dhcpcd 选项值，而 `dhcpcd_essid` 存储当任何接口连接到 ESSID "essid" 时的 dhcpcd 选项值。

然而，并没有硬性规定接口名称必须是 `ethx`。事实上，许多无线接口的名称如 `wlanx`、`rax` 以及 `ethx`。此外，某些用户定义的接口（如网接器）可以命名为任何名称。为了让生活更有趣，无线接入点的名称可以包含非字母数字字符——这很重要，因为用户可以按每个 ESSID 配置网络参数。

这一切的缺点是 Gentoo 使用 bash 变量处理网络——而 bash 无法使用英语字母数字以外的任何字符。为了绕过此限制，我们将每个非英语字母数字字符更改为 `_`（下划线）字符。

bash 的另一个缺点是变量的内容——某些字符需要转义。这可以通过在需要转义的字符前面放置 `\`（反斜杠）来实现。以下字符需要通过这种方式进行转义：`"`、`''` 和 `\`。

在这个示例中，我们使用无线 ESSID，因为它们可以包含最广泛的字符。我们将使用 ESSID `My "\ NET`：文件 `/etc/conf.d/net` 变量名

```
# 这可以工作，但域名是无效的
dns_domain_My____NET="My \"\\ NET"
```

上述设置在存在 `My "\ NET` 时将域名设置为 `My "\ NET`。

## 网络接口命名

### 工作原理

网络接口名称并不是随机选择：Linux 内核和设备管理器（尽管也有 `udev` 可用）会选择接口名称。当检测到接口时，Linux 内核会收集有关该设备的数据。这包括：

*   网络卡的板载（onboard）名称，通过 `ID_NET_ONBOARD` 查看。
*   网络卡插入的插槽（slot），通过 `ID_NET_SLOT` 查看。
*   访问网络卡的路径（path），通过 `ID_NET_PATH` 查看。
*   （厂商提供的）卡的 MAC 地址，通过 `ID_NET_MAC` 查看。

根据这些信息，设备管理器决定如何命名接口。默认情况下，它使用上述三个变量中的命中（`ID_NET_ONBOARD`、`ID_NET_SLOT` 或 `ID_NET_PATH`）。例如，如果 `ID_NET_ONBOARD` 被发现并设置为 `eno1`，那么接口将被命名为 `eno1`。

给定一个活跃的接口名称，可以使用 `udevadm` 显示提供的值：

`root # udevadm test-builtin net_id /sys/class/net/enp3s0 2>/dev/null`

```
ID_NET_MAC=enxc80aa94296
ID_OUI_FROM_DATABASE=Quanta Computer Inc.
ID_NET_PATH=enp3s0
```

由于顶部变量中的第一个也是唯一的命中是 `ID_NET_PATH`，其值被用作接口名称。如果没有任何变量包含值，系统将回退到内核命名（eth0、eth1 等）。

### 使用旧式的内核命名

在此更改之前，网络接口由 Linux 内核本身命名，取决于驱动程序加载的顺序（以及其他可能的晦涩原因）。通过在引导加载程序中设置启动参数 `net.ifnames=0` 启用这种行为。

### 使用自定义名称

更改命名的整个想法并不是为了困扰人们，而是为了让重命名变得简单。假设系统有两个原本被称为 `eth0` 和 `eth1` 的接口。一个用于通过电缆访问网络，另一个用于无线接入。有了接口命名的支持，用户可以将它们命名为 `lan0`（有线）和 `wifi0`（无线——最好避免使用以前旧的名称如 `eth*` 和 `wlan*`，因为这些可能仍与建议的名称冲突）。

找到这些卡的参数，然后使用这些信息设置我们自定义的命名规则：

`root # udevadm test-builtin net_id /sys/class/net/eth0 2>/dev/null`

```
ID_NET_MAC=enxc80aa94296
ID_OUI_FROM_DATABASE=Quanta Computer Inc.
```

`root # vim /etc/udev/rules.d/70-net-name-use-custom.rules`





```bash
# 第一个使用 MAC 信息，并使用 70 号使其位于其他网络规则之前
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="c8:0a:a9:42:9d:76", NAME="lan0"
```

`root #` `vim /etc/udev/rules.d/76-net-name-use-custom.rules`

```bash
# 第二一个使用 ID_NET_NAME_PATH 信息，并使用 76 号使其位于
# 75-net-*.rules 和 80-net-*.rules 之间
SUBSYSTEM=="net", ACTION=="add", ENV{ID_NET_NAME_PATH}=="enp3s0", NAME="wifi0"
```

由于这些规则是在默认规则之前触发的（规则按照字母数字顺序触发，因此 `70` 于 `80` 之前），规则文件中提供的名称将被使用，而不是默认名称。分配给文件的数字应在 `76` 到 `79` 之间（环境变量由以 `75` 开头的规则定义，而回退命名在编号为 `80` 的规则中完成）。

## 网络模块

我们现在支持模块化网络脚本，这意味着我们可以轻松添加对新接口类型和配置模块的支持，同时保持与现有模块的兼容性。

如果模块所需的包已安装，则默认加载模块。如果用户在此处指定了一个未安装对应包的模块，他们将收到一个错误提示，说明需要安装哪个包。理想情况下，模块设置仅在安装了两个或多个提供相同服务的包，且需要其中一个优于另一个时使用。

### 注意

除非另有说明，这里讨论的所有设置都存储在 `/etc/conf.d/net`。

### `/etc/conf.d/net` 模块定义

```bash
# 优先使用 ifconfig 使用 iproute2
modules="ifconfig"

# 你也可以为接口指定其他模块
# 在这种情况下，我们优先使用 pump 而不是 dhcpcd
modules_eth0="pump"

# 你还可以指定不使用的模块 - 例如你可能正在
# 使用 supplicant 或 linux-wlan-ng 来控制无线配置，
# 但你仍然想根据关联的 ESSID 配置网络设置。
modules="!iwconfig"
```

## 接口处理器

我们目前提供两个接口处理器：`ifconfig` 和 `iproute2`。执行任何类型的网络配置只需要其中一个。

`ifconfig` 是默认安装的（`net-tools` 包是系统配置的一部分）。`iproute2` 是一个更强大灵活的包，但默认并不包含。

`root #` `emerge --ask sys-apps/iproute2`

### `/etc/conf.d/net` 已安装 iproute2 但仍偏好 ifconfig

```bash
# 如果两者都已安装，由于 openrc 倾向于使用 iproute2，
# 则通过此设置优先使用 ifconfig
modules="ifconfig"
```

由于 `ifconfig` 和 `iproute2` 的功能非常相似，我们允许它们的基本配置相互工作。例如，以下两个代码段无论用户使用哪种模块都能正常工作。

### `/etc/conf.d/net` 配置的不同方法示例

```bash
config_eth0="192.168.0.2/24"
config_eth0="192.168.0.2 netmask 255.255.255.0"

# 我们也可以指定广播地址
config_eth0="192.168.0.2/24 brd 192.168.0.255"
config_eth0="192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
```

## DHCP

DHCP 是从 DHCP 服务器获取网络信息（IP 地址、DNS 服务器、网关等）的手段。这意味着如果网络上运行着 DHCP 服务器，用户只需告诉每个客户端使用 DHCP，它就会自动设置好网络。当然，用户在使用 DHCP 之前，可能需要对无线、PPP 或其他其他内容进行配置。

DHCP 可以由 `dhclient`、`dhcpcd` 或 `pump` 提供。每个 DHCP 模块都有其优缺点——这里是快速的概述。

| DHCP 模块 | 包 | 优点 | 缺点 |
| :--- | :--- | :--- | :--- |
| dhclient | [net-misc/dhcp](https://packages.gentoo.org/packages/net-misc/dhcp) | 由 ISC 开发，他们也是制作 BIND DNS 软件的开发者。可配置性强 | 配置过于复杂，软件相当臃肿，无法从 DHCP 获取 NTP 服务器，默认不发送主机名 |
| dhcpcd | [net-misc/dhcpcd](https://packages.gentoo.org/packages/net-misc/dhcpcd) | 长期以来 Gentoo 的默认，不依赖外部工具，由 Gentoo 活跃开发 | 有时可能缓慢，当租期为无限时尚未进入守护进程 |
| pump | [net-misc/pump](https://packages.gentoo.org/packages/net-misc/pump) | 轻量级，不依赖外部工具 | 上游不再维护，不可靠，特别是在调制解调器上，无法从 DHCP 获取 NIS 服务器 |

如果安装了多个 DHCP 客户端，请指定使用哪一个——否则如果可用，我们默认为使用 `dhcpcd`。

要向 DHCP 模块发送特定选项，请使用 `module_eth0="..."`（将模块更改为正在使用的 DHCP 模块 - 例如 `dhcpcd_eth0`）。

我们尝试让 DHCP 尽可能保持无关性——因此我们通过 `dhcp_eth0` 变量支持以下命令：

*   `release` - 释放 IP 地址供重用
*   `nodns` - 不覆盖 `/etc/resolv.conf`
*   `nontp` - 不覆盖 `/etc/ntp.conf`
*   `nonis` - 不覆盖 `/etc/yp.conf`

### `/etc/conf.d/net` 示例 DHCP 配置

```bash
# 只有在安装了多个一个 DHCP 模块时才需要
modules="dhcpcd"

config_eth0="dhcp"
dhcpcd_eth0="-t 10" # 10 秒后超时
dhcp_eth0="release nodns nontp nonis" # 只获取地址
```

### 注意

`dhcpcd` 和 `pump` 默认会将当前主机名发送到 DHCP 服务器，因此不再需要指定。

## 带有 PPPoE/PPPoA 的 ADSL

首先我们需要安装 ADSL 软件。

`root #` `emerge --ask net-dialup/ppp`

其次，创建 PPP 网络脚本以及供 PPP 使用的以太网接口脚本：

`root #` `ln -s /etc/init.d/net.lo /etc/init.d/net.ppp0`
`root #` `ln -s /etc/init.d/net.lo /etc/init.d/net.eth0`

确保在 `/etc/rc.conf` 中将 `rc_depend_strict` 设置为 `YES`。

现在我们需要配置 `/etc/conf.d/net`。

### `/etc/conf.d/net` 基本 PPPoE 设置

```bash
config_eth0=null (指定以太网接口)
config_ppp0="ppp"
link_ppp0="eth0" (指定以太网接口)
plugins_ppp0="pppoe"
username_ppp0='user'
password_ppp0='password'
pppd_ppp0="
noauth
defaultroute
usepeerdns
holdoff 3
child-timeout 60
lcp-echo-interval 15
lcp-echo-failure 3
noaccomp noccp"

rc_need_ppp0="net.eth0"
```

你也可以在 `/etc/ppp/pap-secrets` 中设置密码。

### `/etc/ppp/pap-secrets` 示例 pap-secrets

```bash
# * 非常重要
"username"  *  "password"
```

如果在 调制解调器上使用 PPPoE，请确保安装 `br684ctl`。请阅读 `/usr/portage/net-dialup/speedtouch/files/README` 获取有关如何正确配置的信息。

### 重要

请仔细阅读 `/usr/share/doc/netif-*/net.example.bz2` 中关于 ADSL 和 PPP 的部分。它包含了对任何 PPP 设置可能需要的更多详细的解释。

## APIPA（自动私有 IP 地址）

APIPA 通过在接口上 `arping` 169.254.0.0-169.254.255 范围内的随机地址来寻找可用地址。如果没有，我们将该地址分配给接口。

这对于没有 DHCP 服务器且系统不直接连接互联网且所有其他计算机都使用 APIPA 的局域网有用。

为了支持 APIPA，请安装 [net-misc/iputils](https://packages.gentoo.org/packages/net-misc/iputils) 或 [net-analyzer/arping](https://packages.gentoo.org/packages/net-analyzer/arping)。

### `/etc/conf.d/net` APIPA 配置

```bash
# 先尝试 DHCP - 如果失败则回退到 APIPA
config_eth0="dhcp"
fallback_eth0="apipa"

# 仅使用 APIPA
config_eth0="apipa"
```

## 绑定 (Bonding)

对于链路绑定/聚合安装 [net-misc/ifenslave](https://packages.gentoo.org/packages/net-misc/ifenslave)。

绑定用于增加网络带宽或在面对硬件故障时提高韧性。如果系统有两个连接到同一个网络的网卡，管理员可以将它们绑定在一起，使得应用程序只看到一个接口，但它们实际上在使用两个网卡。




配置绑定（bonding）有多种方法。其中某些模式，例如 `802.3ad` `LACP` 模式，需要网络交换机的支持和额外配置。关于各个选项的参考，请参阅本地的 `/usr/src/linux/Documentation/networking/bonding.txt`。

首先，清除参与接口的配置：FILE `/etc/conf.d/net` 清除接口配置。

```
 config_eth0="null"
config_eth1="null"
config_eth2="null"
```

接下来，定义接口之间的绑定：FILE `/etc/conf.d/net` 定义绑定。

```
 slaves_bond0="eth0 eth1 eth2"
config_bond0="192.168.100.4/24"
# 选择适合你需求的正确模式和额外配置选项
mode_bond0="balance-alb"
```

从运行级别（runlevels）中移除 `net.eth*` 服务，创建一个 `net.bond0` 服务并将其添加到正确的运行级别。

## 桥接 (Bridging - 支持 802.1d)

如需桥接支持，请使用 [net-misc/bridge-utils](https://packages.gentoo.org/packages/net-misc/bridge-utils)。

桥接用于将网络连接在一起。例如，系统可能有一台通过 ADSL 调制解调器连接互联网的服务器，并通过无线网卡允许其他计算机通过该解调器上网。可以创建一个桥接将这两个接口连接起来。

FILE `/etc/conf.d/net` 桥接配置。

```
 # 配置桥接 - "man brctl" 查看更多详情
brctl_br0="setfd 0
sethello 2
stp on"

# 将端口添加到桥接 br0
bridge_br0="eth0 eth1"

# 你需要将端口配置为 null 值，以免启动 dhcp
config_eth0="null"
config_eth1="null"

# 最后为桥接分配一个地址 - 你也可以使用 DHCP
config_br0="192.168.0.1/24"

# 依赖 eth0 和 eth1，因为它们可能需要额外配置
rc_need_br0="net.eth0 net.eth1"
```

### 重要提示

使用某些桥接设置时，请咨询变量名文档。

在使用 `IPv6` 进行桥接时，如上例所示，`SLAAC` 要求 `STP` 设置为 `on`。

## MAC 地址可以通过网络配置文件更改接口的 MAC 地址。

FILE `/etc/conf.d/net` MAC 地址更改示例。

```
 # 设置接口的 MAC 地址
mac_eth0="00:11:22:33:44:55"

# 仅随机化最后 3 个字节
mac_eth0="random-ending"

# 在相同物理类型的连接之间随机化（例如光纤、
# 铜线、无线），所有厂商
mac_eth0="random-samekind"

# 在任何物理类型的连接之间随机化（例如光纤、铜线、
# 无线），所有厂商
mac_eth0="random-anykind"

# 完全随机 - 警告：由此生成的某些 MAC 地址
# 可能无法符合预期
mac_eth0="random-full"
```

## 隧道 (Tunneling)

隧道不需要安装任何额外的软件，因为接口处理器可以完成工作。

FILE `/etc/conf.d/net` 隧道配置。

```
 # 用于 GRE 隧道
iptunnel_vpn0="mode gre remote 207.170.82.1 key 0xffffffff ttl 255"

 # 用于 IPIP 隧道
iptunnel_vpn0="mode ipip remote 207.170.82.2 ttl 255"

 # 配置接口
config_vpn0="192.168.0.2 peer 192.168.1.1"
```

## VLAN (支持 802.1q)

如需 VLAN 支持，请确保已安装 [sys-apps/iproute2](https://packages.gentoo.org/packages/sys-apps/iproute2)并确保使用 `iproute2` 作为配置模块而非 `ifconfig`。

虚拟局域网（VLAN）是一组网络设备，其行为就像连接到同一个网段一样——尽管它们并非如此。VLAN 成员只能看到同一 VLAN 的成员，即使它们可能共享相同的物理网络。

要配置 VLAN，首先在 `/etc/conf.d/net` 中指定 VLAN ，如下所示：FILE `/etc/conf.d/net` 指定 VLAN 。

```
 vlans_eth0="1 2"
```

接下来，为每个 VLAN 配置接口：FILE `/etc/conf.d/net` 每个 VLAN 的接口配置。

```
 config_eth0_1="172.16.3.1 netmask 255.255.254.0"
routes_eth0_1="default via 172.16.3.254"

config_eth0_2="172.16.2.1 netmask 255.255.254.0"
routes_eth0_2="default via 172.16.2.254"
```

VLAN 特定的配置通过 `vconfig` 处理，如下：FILE `/etc/conf.d/net` 配置 VLAN。

```
 vlan1_name="vlan1"
vlan1_ingress="2:6 3:5"
eth0_vlan1_egress="1:2"
```

### 重要提示

使用某些 VLAN 设置时，请咨询变量名文档。

## 介绍

Linux 上的无线网络通常非常简单。配置 wifi 有两种方法：图形化客户端或命令行。

最简单的方法是在安装桌面环境后使用图形客户端。大多数图形客户端（如 `wicd` 和 `NetworkManager`）都是直目易懂的。它们提供了一个方便的点击界面，让用户可以在几秒钟内连接到网络。

### 注意

`wicd` 除了主图形界面外还提供了一个命令行工具。通过设置 `ncurses` USE 标志安装 [net-misc/wicd](https://packages.gentoo.org/packages/net-misc/wicd) 软件包。这个 `wicd-curses` 工具对于那些不使用 `gtk` 桌面环境但仍想要一个无需手动编辑配置文件的简单命令行工具的人来说特别有用。

也可以通过编辑几个配置文件从命令行配置无线网络。这需要多花一点时间设置，但下载和安装的包最少。由于图形客户端大多数都是直目易懂的（主页上有帮助的截图），我们将关注命令行替代方案。

有两个支持命令行驱动无线配置的工具：[net-wireless/wireless-tools](https://packages.gentoo.org/packages/net-wireless/wireless-tools) 和 [net-wireless/wpa_supplicant](https://packages.gentoo.org/packages/net-wireless/wpa_supplicant)。在这两个工具中，[net-wireless/wpa_supplicant](https://packages.gentoo.org/packages/net-wireless/wpa_supplicant) 是首选。需要记住的一点是无线网络是全局配置的，而不是基于接口的。

[net-wireless/wireless-tools](https://packages.gentoo.org/packages/net-wireless/wireless-tools) 软件支持几乎所有的卡和驱动，但无法连接到仅支持 WPA 的访问点。如果网络仅提供 WEP 加密或完全开放，那么 [net-wireless/wireless-tools](https://packages.gentoo.org/packages/net-wireless/wireless-tools) 在简单性上胜于另一个软件包。

### 警告

`baselayout` 目前暂不支持 `linux-wlan-ng` 驱动。这是因为 `linux-wlan-ng` 有其自己的设置和配置，与每个人的设置完全不同。据传 `linux-wlan-ng` 的开发者正在改变相对于 `wireless-tools` 的设置，所以当这发生时，`linux-wlan-ng` 就可以配合 `baselayout` 使用。

某些无线卡默认是禁用的。要激活它们，请参阅硬件文档。某些卡可以使用 `rfkill` 应用程序解锁。如果是这种情况，使用 `rfkill list` 查看可用的卡，并使用 `rfkill unblock INDEX` 激活无线功能。如果不是，无线卡可能需要通过笔记本电脑上的按钮、开关或特殊组合组合来解锁。

## WPA supplicant

[WPA supplicant 项目](http://hostap.epitest.fi/wpa_supplicant) 提供了一个允许用户连接到启用 WPA 的访问点的软件包。

```
root # emerge --ask net-wireless/wpa_supplicant
```

### 重要提示

必须在内核中启用 `CONFIG_PACKET`，`wpa_supplicant` 才能工作。要查看当前内核是否已启用，请尝试：

```bash
root # zgrep CONFIG_PACKET /proc/config.gz
root # grep CONFIG_PACKET /usr/src/linux/.config
```





取决于 `USE` 标记，`wpa_supplicant` 可以安装一个使用 Qt4 编写的图形界面，它能与 KDE 良好集成。要获取它，请为 [net-wireless/wpa_supplicant](https://packages.gentoo.org/packages/net-wireless/wpa_supplicant) 包启用 `USE="qt4"`。

接下来，配置 `/etc/conf.d/net`，使得 `wpa_supplicant` 模块优于 `wireless-tools`（如果两者都安装了，默认使用 `wireless-tools`）。

FILE `/etc/conf.d/net` **强制使用 wpa_supplicant**

```bash
 # 优先使用 wpa_supplicant 而非 wireless-tools
modules="wpa_supplicant"

# 告诉 wpa_supplicant 它应该使用哪个驱动程序很重要，
#因为它目前并不擅长猜测
wpa_supplicant_eth0="-Dnl80211"
```

**Note**

在使用 `host-ap` 驱动时，必须先将网卡设置为 `Managed mode` 才能正确配合 `wpa_supplicant` 使用。这可以通过在 `/etc/conf.d/net` 中设置 `iwconfig_eth0="mode managed"` 实现。

接下来配置 `wpa_supplicant` 本身（取决于接入点的安全性，这会有点复杂）。下面的示例取自 `wpa_supplicant` 自带的 `/usr/share/doc/wpa_supplicant-<version>/wpa_supplicant.conf.gz` 并进行了简化。

FILE `/etc/wpa_supplicant/wpa_supplicant.conf` **部分简化示例**

```bash
 # 不要修改此行，否则 wpa_supplicant 将拒绝工作
ctrl_interface=/var/run/wpa_supplicant

# 确保只有 root 用户可以读取 WPA 配置
ctrl_interface_group=0

# 让 wpa_supplicant 处理扫描和 AP 选择
ap_scan=1

# 简单情况：WPA-PSK，PSK 为 ASCII 密码，允许所有有效的加密算法
network={
  ssid="simple"
  psk="very secret passphrase"
  # 优先级越高，匹配速度越快
  priority=5
}

# 与之前相同，但请求针对特定 SSID 的扫描（针对拒绝广播
# SSID 的 AP）
network={
  ssid="second ssid"
  scan_ssid=1
  psk="very secret passphrase"
  priority=2
}

# 只使用 WPA-PSK。接受任何有效的加密组合
network={
  ssid="example"
  proto=WPA
  key_mgmt=WPA-PSK
  pairwise=CCMP TKIP
  group=CCMP TKIP WEP104 WEP40
  psk=06b4be19da289f475aa46a33cb793029d4ab3db7a23ee92382eb0106c72ac7bb
  priority=2
}

# 明文连接（无 WPA，无 IEEE 802.1X）
network={
  ssid="plaintext-test"
  key_mgmt=NONE
}

# 共享 WEP 密钥连接（无 WPA，无 IEEE 802.1X）
network={
  ssid="static-wep-test"
  key_mgmt=NONE
  # 引号内的密钥是 ASCII 密钥
  wep_key0="abcde"
  # 未加引号的密钥是十六进制密钥
  wep_key1=0102030405
  wep_key2="1234567890123"
  wep_tx_keyidx=0
  priority=5
}

# 共享 WEP 密钥连接（无 WPA，无 IEEE 802.1X）使用共享密钥
# IEEE 802.11 认证
network={
  ssid="static-wep-test2"
  key_mgmt=NONE
  wep_key0="abcde"
  wep_key1=0102030405
  wep_key2="1234567890123"
  wep_tx_keyidx=0
  priority=5
  auth_alg=SHARED
}

# IBSS/ad-hoc 网络使用 WPA-None/TKIP
network={
  ssid="test adhoc"
  mode=1
  proto=WPA
  key_mgmt=WPA-NONE
  pairwise=NONE
  group=TKIP
  psk="secret passphrase"
}
```

## Wireless tools

### 设置和托管模式

[wireless tools 项目](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) 提供了一种配置基础无线接口的方法，最高支持 WEP 安全级别。虽然 WEP 是一种较弱的安全方法，但它在世界上仍然流行。

Wireless tools 的配置由几个主要变量控制。下面的示例配置文件描述了所有需要的内容。需要注意的是，没有进行配置意味着“连接到最强的未加密接入点”——wireless tools 总是尝试将系统连接到某些设备。

`root #` `emerge --ask net-wireless/wireless-tools`

**Note**

虽然用户可以将无线设置存储在 `/etc/conf.d/wireless`，但本指南建议将其存储在 `/etc/conf.d/net` 中。

**Important**

你需要咨询变量名文档。FILE `/etc/conf.d/net` **iwconfig 设置示例**

```bash
 # 优先使用 iwconfig 而非 wpa_supplicant
modules="iwconfig"

 # 为名为 ESSID1 和 ESSID2 的接入点配置 WEP 密钥
 # 你可以配置最多 4 个 WEP 密钥，但任何时候只能激活一个
# 所以我们提供了一个默认索引 [1] 来设置密钥 [1]，然后
# 再次将活动密钥更改为 [1]
 # 这样做是为了防你定义其他使用非 1 号 WEP 密钥的 ESSID
#
# 在密钥前加上 s: 表示它是 ASCII 密钥，否则为 HEX 密钥
#
# enc open 指定开放式安全（安全性最高）
# enc restricted 指定受限安全（安全性最低）
key_ESSID1="[1] s:yourkeyhere key [1] enc open"
key_ESSID2="[1] aaaa-bbbb-cccc-dd key [1] enc restricted"

 # 以下内容仅在扫描可用接入点时起作用

 # 有时会看到多个接入点，因此我们需要定义
 # 优先连接的顺序
preferred_aps="'ESSID1' 'ESSID2'"
```

### 细调 AP 选择

可以添加一些额外的选项来精调 AP 选择，但这些并非强制。

一种方法是配置系统使其仅连接到优的 AP。默认情况下，如果所有配置都失败且 wireless tools 可以连接到未加密的接入点，它就会尝试连接。这可以通过 `associate_order` 变量控制。这里是这些值及其控制方式。

| Value | 描述 |
| :--- | :--- |
| any | 默认行为。 |
| preferredonly | 连接到优先列表中的可见 AP。 |
| forcepreferred | 如果在扫描中未找到，则强制按优先顺序连接到 AP。 |
| forcepreferredonly | 不扫描 AP —— 而是按顺序尝试连接每一个。 |
| forceany | 等同于 forcepreferred + 连接到任何其他可用 AP。 |

还有 `blacklist_aps` 和 `unique_ap`。`blacklist_aps` 的工作方式与 `preferred_aps` 类似。`unique_ap` 是一个是或否的值，表示第二个接口是否可以连接同一个接入点。

FILE `/etc/conf.d/net` **blacklist_aps 和 unique_ap 示例**

```bash
 # 有时你永远不想连接到某些接入点
blacklist_aps="'ESSID3' 'ESSID4'"

 # 如果你有多个无线网卡，可以指定是否想
 # 与同一个接入点关联
 值为 "yes" 和 "no"
 # 默认是 "yes"
unique_ap="yes"
```

### Ad-hoc 和 master 模式

当无法连接到任何接入点时，将系统设置为 ad-hoc，请使用此作为回退：FILE `/etc/conf.d/net` **回退到 ad-hoc**

```bash
 adhoc_essid_eth0="This Adhoc Node"
```

也可以连接到 ad-hoc 网络，或者以 `master` 模式运行系统使其自身成为接入点。

FILE `/etc/conf.d/net` **ad-hoc/master 配置示例**

```bash
 # 设置模式 —— 可以 managed（默认）、ad-hoc 或 master
 # 并非所有驱动程序都支持所有模式
mode_eth0="ad-hoc"

 # 设置接口的 ESSID
 # 在 managed 模式下，这将强制接口连接到
 # 指定的 SSID 而不是其他
essid_eth0="This Adhoc Node"

 # 如果未指定，我们使用 3 号通道
channel_eth0="9"
```

**Important**

关于通道选择的一个重要资源是 NetBSD 文档中的 [BSD wavel 文档](http://www.netbsd.org/Documentation/network/wavelan.html)。共有 14 个通道可用；我们被告知北美地区 1-11 号合法，欧洲大部分地区为 1-13 号，法国为 10-13 号，而日本仅限 14 号合法。如有疑问，请参考网卡或接入点的附带文档。请确保选定的通道与接入点（或 ad-hoc 网络中的另一个网卡）所在的通道一致。





由于驱动程序或环境问题，还有一些变量可以帮助无线网络运行。以下是可以尝试的其他内容的表格。

| 变量名 | 默认值 | 描述 |
| :--- | :--- | :--- |
| `iwconfig_eth0` | | 详情参阅 `iwconfig` 手页了解发送给 `iwconfig` 的内容。 |
| `iwpriv_eth0` | | 详情参阅 `iwpriv` 手页了解发送给 `iwpriv` 的内容。 |
| `sleep_scan_eth0` | 0 | 扫描之前睡眠的秒数。当驱动/固件需要更多时间激活才能在使用时，需要此设置。 |
| `sleep_associate_eth0` | 5 | 在移动到下一个接口之前，等待接口与接入点（AP）关联的秒数。 |
| `associate_test_eth0` | MAC | 驱动在丢失或尝试关联时，不会将关联的 MAC 地址重置为无效地址。某些驱动在丢失或尝试关联时不会重置质量级别。有效的设置为 MAC、quality 和 all。 |
| `scan_mode_eth0` | | 某些驱动必须在 ad-hoc 模式下扫描，因此如果扫描失败，请在此设置 ad-hoc。 |
| `iwpriv_scan_pre_eth0` | | 在扫描前向接口发送一些 `iwpriv` 命令。详情参阅 `iwpriv` 手页。 |
| `iwpriv_scan_post_eth0` | | 在扫描后向接口发送一些 `iwpriv` 命令。详情参阅 `iwpriv` 手页。 |

## 按 ESSID 定义网络配置

在本节中，我们展示了如何根据 ESSID 配置网络设置。例如，对于 ESSID 为 `ESSID1` 的无线网络配置静态 IP 地址，而 ESSID 为 `ESSID2` 的使用 DHCP。

**注意**

此方法同时适用于 `wpa_supplicant` 和 `wireless-tools`。**重要**

请查阅变量名文档。文件 `/etc/conf.d/net` 可按 ESSID 覆盖网络设置。

```
config_ESSID1="192.168.0.3/24 brd 192.168.0.255"
routes_ESSID1="default via 192.168.0.1"

config_ESSID2="dhcp"
fallback_ESSID2="192.168.3.4/24"
fallback_route_ESSID2="default via 192.168.3.1"

# 我们也可以定义 DNS 服务器和其他内容
# 注意：除非告诉它，否则 DHCP 将覆盖这些设置
dns_servers_ESSID1="192.168.0.1 192.168.0.2"
dns_domain_ESSID1="some.domain"
dns_search_domains_ESSID1="search.this.domain search.that.domain"

# 你可以通过接入点的 MAC 地址进行覆盖
# 如果你去具有相同 ESSID 的不同地点，这非常有用
config_001122334455="dhcp"
dhcpcd_001122334455="-t 10"
dns_servers_001122334455="192.168.0.1 192.168.0.2"
```

## 标准函数钩子

可以在 `/etc/conf.d/net` 中定义四个函数，这些函数将在启动/停止操作前后被调用。调用这些函数时会先传递名称，以便一个函数可以控制多个适配器。

`preup()` 和 `predown()` 函数的返回值应为 0（成功），表示接口的配置或取消配置可以继续。如果 `preup()` 返回非零，则接口配置将中止。如果 `predown()` 返回非零，则不允许接口继续取消配置。

`postup()` 和 `postdown()` 函数的返回值会被忽略，因为如果它们指示失败，也没有事可做。

`${IFACE}` 被设置为正在启动/停止的接口。`${IFVAR}` 是 `${IFACE}` 转换为 bash 允许的变量名。

文件 `/etc/conf.d/net` pre/post up/down 函数示例

```
if grep -q 'Link detected: no'; then
    ewarn "No link on ${IFACE}, aborting configuration"
    return 1
  fi

  # 记住在成功时返回 0
  return 0
}

predown() {
  # 脚本中的默认值是测试 NFS 根目录并禁止
  #在这种情况下关闭接口。注意，如果你指定了
  # predown() 函数，你将覆盖该逻辑。这里有它，以防你还需要...
  if is_net_fs /; then
    eerror "root filesystem is network mounted -- can't stop ${IFACE}"
    return 1
  fi

  # 记住在成功时返回 0
  return 0
}

postup() {
  # 此函数可以用于，例如注册到
  # 动态 DNS 服务。另一种可能性是在接口
  # 后发送/接收邮件。
       return 0
}

postdown() {
  # 此函数主要在这里是为了完整性……我还没有
  # 想出可以用它做的什么酷的事情 ;-)
  return 0
}
```

**注意**

关于编写函数的更多信息，请阅读 `/usr/share/doc/netifrc-*/net.example.bz2`。

## 无线工具函数钩子

**注意**

这在 WPA Supplicant 中不起作用——但 `${ESSID}` 和 `${ESSIDVAR}` 变量在 `postup()` 函数可用。

可以在 `/etc/conf.d/net` 中定义两个函数，这些函数将在关联函数前后被调用。调用这些函数时会先传递名称，以便一个函数可以控制多个适配器。

`preassociate()` 函数的返回值应为 0（成功），表示接口的配置或取消配置可以继续。如果 `preassociate()` 返回非零，则接口配置将中止。

`postassociate()` 函数的返回值会被忽略，因为如果它指示失败，也没有事可做。

`${ESSID}` 设置为系统连接的 AP 的精确 ESSID。`${ESSIDVAR}` 是 `${ESSID}` 转换为 bash 允许的变量名。

文件 `/etc/conf.d/net` pre/post 关联函数

```
if grep -q 'Login incorrect'; then
      ewarn "Login Failed for ${user}"
      return 1
    fi
  fi

  return 0
}

postassociate() {
  # 此函数主要在这里是为了完整性……我还没有
  # 想出可以用它做的什么酷的事情 ;-)

  return 0
}
```

**注意**

`${ESSID}` 和 `${ESSIDVAR}` 在 `predown()` 和 `postdown()` 函数中无效。**注意**

关于编写自定义函数的更多信息，请阅读 `/usr/share/doc/netifrc-*/net.example.bz2`。

## 网络管理

对于笔记本电脑，系统可能处于移动中。因此，系统可能并不总是插有以太网线或有可用接入点。此外，用户可能希望在插入以太网线或发现接入点时网络自动工作。

在本章中，我们将介绍如何实现这一点。

**注意**

本文仅讨论 `ifplugd`，但也有 `netplug` 等替代方案。`netplug` 是 `ifplugd` 的轻量级替代方案，但它依赖于内核驱动程序的正常工作，而许多驱动程序并非如此。

### ifplugd

[ifplugd](http://0pointer.de/lennart/projects/ifplugd/) 是一个守护进程，在以太网线插入或移除时启动和停止接口。它还可以管理检测接入点的关联或新接入点的进入范围。

`root #` `emerge --ask sys-apps/ifplugd`

`ifplugd` 的配置也相当直观。配置位于 `/etc/conf.d/net` 中。运行 `man ifplugd` 获取可用变量的详情。此外，查看 `/usr/share/doc/netifrc-*/net.example.bz2` 获取示例。

文件 `/etc/conf.d/net` 示例 ifplug 配置

```
# 将 eth0 替换为要监控的接口
ifplugd_eth0="..."

# 监控无线接口
ifplugd_eth0="--api-mode=wlan"
```

除了管理多个网络连接外，用户可能希望添加一个工具，以便于处理多个 DNS 服务器和配置。这在系统通过 DHCP 获取 IP 地址时非常有用。

`root #` `emerge --ask net-dns/openresolv`

通过 `man resolvconf` 了解更多其功能。





*   [在模板调用中使用重复参数的页面](https://wiki.gentoo.org/index.php?title=Category:Pages_using_duplicate_arguments_in_template_calls&action=edit&redlink=1 "Category:在模板调用中使用重复参数的页面（页面不存在）")
*   此页面最后修改于 2014 年 12 月 13 日 18:44。
*   [隐私政策](https://wiki.gentoo.org/wiki/Gentoo_Wiki:Privacy_policy "Gentoo Wiki: 隐私政策")
*   [关于 Gentoo Wiki](https://wiki.gentoo.org/wiki/Gentoo_Wiki:About "Gentoo Wiki: 关于")
*   [免责声明](https://wiki.gentoo.org/wiki/Gentoo_Wiki:General_disclaimer "Gentoo Wiki: 一般免责声明")
*   [](https://twitter.com/gentoo "@Twitter 上的 Gentoo")
*   [](https://plus.google.com/+Gentoo "+Google+ 上的 Gentoo")
*   [](https://www.facebook.com/gentoo.org "Facebook 上的 Gentoo")

© 2001–2016 Gentoo Foundation, Inc.

Gentoo 是 Gentoo Foundation, Inc. 的商标。除非另有说明，本文档的内容均受 [CC-BY-SA-3.0](https://creativecommons.org/licenses/by-sa/3.0/) 许可协议保护。[Gentoo 名称和标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html)适用。![cover](img/cover_image.jpg)

# 项目:Overlays/Overlays 指南

来自 Gentoo Wiki< [项目:Overlays](https://wiki.gentoo.org/wiki/Project:Overlays "项目:Overlays") 跳转到：导航, 搜索

## 目录

*   1 请求添加新存储库 (overlays)
    *   1.1 基础规则
    *   1.2 请求添加托管在其他处的存储库（新方法）
    *   1.3 请求添加托管在其他处的存储库（旧方法）
    *   1.4 请求为存储库托管
    *   1.5 请求将 git.g.o 存储库自动镜像到 GitHub / 任何外部托管
*   2 调试常见问题
    *   2.1 测试对 git.gentoo.org 存储库的访问
    *   2.2 调试 SSH 密钥问题
*   3 报告存储库的 Bug

## 1 请求添加新存储库 (overlays)

### 基础规则

Gentoo Overlays 项目成员维护着一个为 [layman](https://wiki.gentoo.org/wiki/Layman "Layman")、[overlays.gentoo.org](http://overlays.gentoo.org/) 以及许多面向 Gentoo 服务的全局列表。如果您希望将您的存储库列入，我们将为您提供帮助。

列表中的所有存储库都必须满足一些规则。这些规则：

1. 存储库必须通过 layman 支持的任一协议/版本控制系统 (VCS) 可访问。为了获得最佳移植性，推荐使用 `git+https://`。
2. 存储库必须符合最低 QA 标准：具有有效且唯一的存储库名称（在 `profiles/repo_name` 中，`layout.conf` 不通用），并且在 `metadata/layout.conf` 中有有效的 `masters=` 条目。
3. 存储库所有者必须拥有 [Gentoo Bugzilla](https://bugs.gentoo.org/) 账户。Bugzilla 将用于所有关于存储库的官方通信。
4. 存储库应尽力维护，不要给用户带来问题。我们保留移除被报告会对我们的用户构成严重威胁的存储库的权利。

存储库可以托管您自己的基础设施上、任何公共托管服务上，或者我们可以在 [git.gentoo.org](https://gitweb.gentoo.org/) 为您托管（仅限 git）。后者，我们还支持自动填充存储库的外部镜像（例如在 GitHub 上）。

### 请求添加托管在其他处的存储库（新方法）

添加存储库的新推荐方法是在 api.gentoo.org 存储库上提交[拉取请求](https://github.com/gentoo/api-gentoo-org/pulls)或对其提交补丁。

（分叉并）克隆存储库：

```bash
user$ git clone git@github.com:myuser/api-gentoo-org.git
```

然后，通过复制并修改适当的模板，将您的存储库添加到 `files/overlays/repositories.xml` 中。切记更新所有 URL，并将所有者设置为您的 Gentoo Bugzilla 电子邮件地址（我们将进行验证的！）。之后，验证 XML 是否正确，并提交更改，提交信息以 `repositories:` 关键字开头。

```bash
user$ xmllint --noout --schema $(portageq get_repo_path / gentoo)/metadata/xml-schema/repositories.xsd repositories.xml
user$ git commit repositories.xml -m 'repositories: Add foo-overlay'
user$ git push
```

### 请求添加托管在其他处的存储库（旧方法）

*（注：原文中未提供此章节的内容）*

### 请求为存储库托管

*注：原文中未提供此章节的内容）*

### 请求将 git.g.o 存储库自动镜像到 GitHub / 任何外部托管

（注：原文中未提供此章节的内容）*

## 2 调试常见问题

### 2.1 测试对 git.gentoo.org 存储库的访问

*（注：原文中未提供此章节的内容）*

### 2.2 调试 SSH 密钥问题

*（注：原文中未提供此章节的内容）*

## 3 报告存储库的 Bug

*（注：原文中未提供此章节的内容）*





如果你有一个开启的 bug，请在 commit 消息中包含 `#nnnnnn`。建议保持 bug 开启状态，因为这可以让我们清晰地验证你提供了正确的电子邮箱地址。

之后，你可以提交拉取请求（pull request）、生成 git patch 并将其附加到 bug 上，或者发送邮件至 `overlays@g.o` 联系我们。

## 请求添加托管在其他处的仓库（旧方法）

如果你的仓库已经托管在某处，请在 [Gentoo Infra 产品、Gentoo Overlays 组件中创建一个 bug](https://bugs.gentoo.org/enter_bug.cgi?product=Gentoo+Infrastructure&component=Gentoo+Overlays&short_desc=Add+repository:+NAME&comment=description:+%0ahomepage:+%0aowner:+%0asources:+%0afeeds:+%0a) 并提供以下信息：

1. 请求的仓库名称（必须与 `profiles/repo_name` 中的某一个相同，填写此处仅作为确认），
2. 简短描述，
3. 主页 URL，
4. 仓库所有者，
5. 仓库类型及 URL，
6. 仓库提交源 URL（如果有的话）。

或者，你可以为你的仓库提供一个 `repositories.xml-format` 文件，我们将从中复制信息。

请注意，如果你不是仓库所有者，你必须获得其显式许可才能添加该仓库。他也必须符合 Bugzilla 账号的要求。

## 请求托管仓库

如果你希望我们为你托管仓库，请在 [Gentoo Infra 产品、Gentoo Overlays 组件中创建一个 bug](https://bugs.gentoo.org/enter_bug.cgi?product=Gentoo+Infrastructure&component=Gentoo+Overlays&short_desc=New+repository+hosting:+repo/user/NAME&comment=description:+%0ahomepage+%28optional%29:+%0aadmin+access+to:+%0awrite+access+to:+%0a%0apublic+SSH+key:%0a) 并提供以下信息：

1. `repo/user/...` 命名空间下请求的仓库名称（URL 将为 git.gentoo.org/repo/user/），
2. 简短描述，
3. 如果计划使用外部主页，请提供 URL，
4. 如果之前没有为 `git.gentoo.org` 提供过公钥，请提供你的公钥，
5. 应该拥有写入或管理权限的其他人员列表（如果适用，提供他们的公钥），
6. 如果需要，请求添加外部镜像。

此 bug 将同时用于创建 git 仓库和将其添加到列表的目的。

请注意，你需要接受以下服务条款：

```
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
 Use of this service is  limited to overlays containing ebuilds
 and  supporting  files  (e.g.  init.d  scripts,  configuration
files, patches,  but not distfiles)  and must follow  the same
guidelines as apply to the gentoo-x86 tree of Gentoo.

 Any or all uses of this  service and all files on this service
may  be  intercepted, monitored, recorded, copied,  audited,
inspected, and disclosed to authorized site personnel, as well
as authorized  officials of federal law
enforcement agencies,
both domestic  and foreign.  By using this service, the user
consents to such interception, monitoring, recording, copying,
auditing,  inspection, and  disclosure  at the discretion of
authorized site  personnel.  Use  of this service constitutes
consent to  security monitoring and testing.   All activity is
logged with  your host name  and IP address.   Unauthorized or
improper use of this service  may result in civil and criminal
penalties.   By continuing  to use  this service you indicate
your awareness of and consent to these terms and conditions of
use.   -- Gentoo Linux Infrastructure Admins

                     CEASE USE IMMEDIATELY,
  if you do not agree to the conditions stated in this warning.
                      *******************
 -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
```

## 请求在 GitHub / 任何外部托管平台自动镜像 git.g.o 仓库

我们支持将你的 git.g.o 仓库自动镜像到任意外部 git 托管平台，包括 GitHub 以及你的私有 git 服务器（通过 SSH）。镜像通过服务器端 git hooks 完成，因此所有更改都会立即传播到所有外部镜像。

**警告**

自动镜像是单向的且具有破坏性。git.g.o 中的所有分支和标签将强制推送到镜像端，所有剩余的分支和标签将被修剪。所有推送到 GitHub/外部托管但未进入 git.g.o 的提交在下次推送到 git.g.o 时会被自动丢弃。

要使镜像工作，你需要允许我们的 SSH 部署密钥拥有仓库推送权限。取决于所使用的托管平台：

* 如果是 GitHub，你需要将 [gentoo-bot](https://github.com/gentoo-bot) 用户添加到仓库的贡献者中，
* 否则，你需要添加以下部署密钥：

FILE `id_rsa.pub`Gentoo 仓库镜像公钥

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCoJNoPdn0LtNjscz50rlJms7RSZF95wfwhz+3pgKQ3z9hr8u3wXcVngl0G17D1VYZJonrMQGDBbpAQyYVI6bu7HqUg7DmLvoTqnh9nfH5vrXcVmYKTWDWV2fANF8U2NX0VpD4VIS/aB/5uNscUtZ1ApkpxgW+j+qO/kthQZn97ILAsQ4KsoGF25+cXMkpwDxsemOKjE+mKeA0hzHiyERxViClwxvKNx4s65CWFqUBlEKTG1QaCAoNpnowYHcqWFzaH3wlEzwfDM1orvpZ3fFma4U9F32x+HuyfkbqY7YchvKQj8boqapbqy7fJn4FUtXa/XNC6JX43xrxHMaxqF+tV gentoo mirroring
```

之后，开启一个请求镜像的 bug。完成后，推送到 git.g.o 以测试镜像更新。

## 调试常见问题

### 测试访问 git.gentoo.org 仓库

如果你在访问 git.gentoo.org 托管的仓库时遇到问题，请先输入：

`user $ ssh git@git.gentoo.org info`

```
hello foo@example.com, this is git@oystercatcher running gitolite3 gitolite-gentoo-9999-gentoo on git 2.8.2

 R W	data/api
 R W	data/dtd
 R W	data/gentoo-changelogs
 R W 	data/gentoo-news
 R  	data/glsa
 ...

Please see http://wiki.gentoo.org/wiki/Gitolite for more help
```

这应该返回一个 gitolite 状态消息，显示你的电子邮箱地址以及所有仓库的 ACL。如果你得到的是“permission denied”错误，则意味着你当前的 SSH 密钥未注册在 gitolite 中。请同时查看调试 SSH 密钥问题。

如果你看到错误的电子邮箱地址，且你过去使用过不同的邮箱地址，可能两个地址都注册了不同的 SSH 密钥。请联系 Overlays 团队将你的密钥合并到单一地址。

如果你的邮箱地址是正确的，但你本应拥有的仓库没有写入权限（'W'），请联系仓库所有者或 Overlays 团队（如果是所有者）。

如果状态显示你拥有写入权限，请验证你是否使用了正确的 git URI。如需写入权限，你需要通过 SSH 使用 git：

`user $ git clone git@git.gentoo.org:repo/path.git`

### 调试 SSH 密钥问题

**注意**

OpenSSH 7.0 不再默认允许使用 DSA 密钥。如果你正在使用 DSA 密钥，请查看 [OpenSSH 7.0 新](https://www.gentoo.org/support/news-items/2015-08-13-openssh-weak-keys.html)。

`permission denied` 问题的常见原因是 SSH 没有使用正确的 SSH 密钥。

如果你没有 ssh-agent（或带有 SSH 的 gpg-agent、带有 SSH 的 gnome-keyring），请先加载你的密钥：

`user $ ssh-add`

要获取当前的 SSH 密钥，请输入：

`user $ ssh-add -L`

```
ssh-rsa AAAA...
```

为了确认公钥与私钥匹配，请对比：

`user $ ssh-add -l`

```
4096 SHA256:RNizcaEs7yUE3nMio4W/OOZ3fE68foNv5nUA9ubz32M (none) (RSA)
```

以及：

`user $ ssh-keygen -l -f /path/to/id_*`

```
4096 SHA256:RNizcaEs7yUE3nMio4W/OOZ3fE68foNv5nUA9ubz32M (none) (RSA)
```





`ssh-add` 会打印活动 SSH 密钥的指纹，而 `ssh-keygen` 会打印指定文件的指纹（可以是私钥文件或公钥文件）。不同的指纹意味着使用了不同的密钥。

如果你有 `~/.ssh/id_*.pub` 文件，检查它们是否与私钥匹配是一个好主意。如果其中任何一个文件的指纹与私钥文件不同，请将其删除，因为这会混淆 SSH 并阻止其使用正确的私钥。之后，你可以使用上述 `ssh-add -L` 语法重新生成公钥。

## 在仓库中报告 bug

如果你想就第三方仓库或其中的包报告 bug，可以使用该仓库特定的 bug 跟踪器（如果有的话）或 Gentoo Bugzilla。如果请求需要 Gentoo Overlays 项目成员执行特定的显式操作（例如，移除仓库），则必须通过 Gentoo Bugzilla 提交。

在 Gentoo Bugzilla 上报告第三方仓库中包的 bug 时，请记住明确说明该包来自哪个仓库。这通常使用 `::repository-name` 符号（类似于 Portage）。这将确保该 bug 能够被正确分配给仓库所有者，而不是 Gentoo 中相应包的维护者。

![cover](img/cover_image.jpg)

| 通用概念 – Gentoo 开发指南 |
| :--- | :--- |
| 未知 | |
| * * * |

[**获取 Gentoo！**](https://get.gentoo.org/)gentoo.org 站点

* [gentoo.org](https://www.gentoo.org/ "Gentoo 主站")
* [Wiki](https://wiki.gentoo.org/ "查找并贡献文档")
* [Bugs](https://bugs.gentoo.org/ "报告问题并发现常见问题")
* [Forums](https://forums.gentoo.org/ "与社区讨论")
* [Packages](https://packages.gentoo.org/ "为你的 Gentoo 寻找软件")
* [Planet](https://planet.gentoo.org/ "了解开发者社区的动态")
* [Archives](https://archives.gentoo.org/ "阅读过去的讨论")
* [Sources](https://sources.gentoo.org/ "浏览我们的源代码")
* [Infra Status](https://infra-status.gentoo.org/ "获取 Gentoo 提供的服务的更新")

![Gentoo Linux Logo](img/site-logo.png) 开发指南

* [首页](https://devmanual.gentoo.org//index.html)
* 通用概念
    * [Autotools 基础](https://devmanual.gentoo.org/general-concepts/autotools/index.html)
    * [配置文件保护](https://devmanual.gentoo.org/general-concepts/config-protect/index.html)
    * [Git 到 RSYNC](https://devmanual.gentoo.org/general-concepts/git-to-rsync/index.html)
    * [依赖](https://devmanual.gentoo.org/general-concepts/dependencies/index.html)
    * [Manifest](https://devmanual.gentoo.org/general-concepts/manifest/index.html)
    * [分布式与并行编译](https://devmanual.gentoo.org/general-concepts/distributed-building/index.html)
    * [Ebuild 版本号](https://devmanual.gentoo.org/general-concepts/ebuild-revisions/index.html)
    * [Emerge 与 Ebuild 关系](https://devmanual.gentoo.org/general-concepts/emerge-and-ebuild/index.html)
    * [FEATURES](https://devmanual.gentoo.org/general-concepts/features/index.html)
    * [文件系统](https://devmanual.gentoo.org/general-concepts/filesystem/index.html)
    * [项目与群组](https://devmanual.gentoo.org/general-concepts/herds-and-projects/index.html)
    * [安装目标](https://devmanual.gentoo.org/general-concepts/install-destinations/index.html)
    * [许可证](https://devmanual.gentoo.org/general-concepts/licenses/index.html)
    * [语言 (Linguas)](https://devmanual.gentoo.org/general-concepts/linguas/index.html)
    * [镜像站](https://devmanual.gentoo.org/general-concepts/mirrors/index.html)
    * [新闻动态](https://devmanual.gentoo.org/general-concepts/news/index.html)
    * [覆盖层 (Overlay)](https://devmanual.gentoo.org/general-concepts/overlay/index.html)
    * [位置无关代码 (PIC)](https://devmanual.gentoo.org/general-concepts/pic/index.html)
    * [Portage 缓存](https://devmanual.gentoo.org/general-concepts/portage-cache/index.html)
    * [权限](https://devmanual.gentoo.org/general-concepts/privileges/index.html)
    * [沙箱](https://devmanual.gentoo.org/general-concepts/sandbox/index.html)
    * [槽位管理 (Slotting)](https://devmanual.gentoo.org/general-concepts/slotting/index.html)
    * [Portage 树](https://devmanual.gentoo.org/general-concepts/tree/index.html)
    * [USE 标志](https://devmanual.gentoo.org/general-concepts/use-flags/index.html)
    * [用户环境](https://devmanual.gentoo.org/general-concepts/user-environment/index.html)
    * [虚拟包 (Virtuals)](https://devmanual.gentoo.org/general-concepts/virtuals/index.html)
* [快速上手 Ebuild 指南](https://devmanual.gentoo.org/quickstart/index.html)
* [Autotools 基础](https://devmanual.gentoo.org/general-concepts/autotools/index.html)

1. [主索引](https://devmanual.gentoo.org/index.html)

# 通用概念

本节涵盖了在编写 ebuild 或操作 Portage 树时应当熟悉的通用概念。

## 目录

* [Autotools 基础](https://devmanual.gentoo.org/general-concepts/autotools/index.html)
* [配置文件保护](https://devmanual.gentoo.org/general-concepts/config-protect/index.html)
* [Git 到 RSYNC](https://devmanual.gentoo.org/general-concepts/git-to-rsync/index.html)
* [依赖](https://devmanual.gentoo.org/general-concepts/dependencies/index.html)
* [Manifest](https://devmanual.gentoo.org/general-concepts/manifest/index.html)
* [分布式与并行编译](https://devmanual.gentoo.org/general-concepts/distributed-building/index.html)
* [Ebuild 版本号](https://devmanual.gentoo.org/general-concepts/ebuild-revisions/index.html)
* [Emerge 与 Ebuild 关系](https://devmanual.gentoo.org/general-concepts/emerge-and-ebuild/index.html)
* [FEATURES](https://devmanual.gentoo.org/general-concepts/features/index.html)
* [文件系统](https://devmanual.gentoo.org/general-concepts/filesystem/index.html)
* [项目与群组](https://devmanual.gentoo.org/general-concepts/herds-and-projects/index.html)
* [安装目标](https://devmanual.gentoo.org/general-concepts/install-destinations/index.html)
* [许可证](https://devmanual.gentoo.org/general-concepts/licenses/index.html)
* [语言 (Linguas)](https://devmanual.gentoo.org/general-concepts/linguas/index.html)
* [镜像站](https://devmanual.gentoo.org/general-concepts/mirrors/index.html)
* [新闻动态](https://devmanual.gentoo.org/general-concepts/news/index.html)
* [覆盖层 (Overlay)](https://devmanual.gentoo.org/general-concepts/overlay/index.html)
* [位置无关代码 (PIC)](https://devmanual.gentoo.org/general-concepts/pic/index.html)
* [Portage 缓存](https://devmanual.gentoo.org/general-concepts/portage-cache/index.html)
* [权限](https://devmanual.gentoo.org/general-concepts/privileges/index.html)
* [沙箱](https://devmanual.gentoo.org/general-concepts/sandbox/index.html)
* [槽位管理 (Slotting)](https://devmanual.gentoo.org/general-concepts/slotting/index.html)
* [Portage 树](https://devmanual.gentoo.org/general-concepts/tree/index.html)
* [USE 标志](https://devmanual.gentoo.org/general-concepts/use-flags/index.html)
* [用户环境](https://devmanual.gentoo.org/general-concepts/user-environment/index.html)
* [虚拟包 (Virtuals)](https://devmanual.gentoo.org/general-concepts/virtuals/index.html)

### 有问题或建议？

请随时[联系我们](https://www.gentoo.org/inside-gentoo/contact/)。





*   [](http://twitter.com/gentoo "@Gentoo on Twitter")
*   [](https://plus.google.com/+Gentoo "+Gentoo on Google+")
*   [](https://www.facebook.com/gentoo.org "Gentoo on Facebook")

Copyright (C) 2001-2016 Gentoo Foundation, Inc.

Gentoo 是 Gentoo Foundation, Inc. 的商标。本文档的文本根据 [知识产权 署名-相同共享 3.0 国际许可许可证](http://creativecommons.org/licenses/by-sa/3.0/) 分发。[Gentoo 名称和标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html) 适用。![cover](img/cover_image.jpg)

| 快速上手 Ebuild 指南 – Gentoo 开发指南 |
| | |
| 未知 | |
| | |
| |
| * * * | |
| | |

## [获取 Gentoo!](https://get.gentoo.org/) gentoo.org 站点

*   [gentoo.org](https://www.gentoo.org/ "Gentoo 主网站")
*   [Wiki](https://wiki.gentoo.org/ "查找并贡献文档")
*   [Bugs](https://bugs.gentoo.org/ "报告问题并查找常见问题")
*   [Forums](https://forums.gentoo.org/ "与社区讨论")
*   [Packages](https://packages.gentoo.org/ "为你的 Gentoo 寻找软件")
*   [Planet](https://planet.gentoo.org/ "了解开发者社区的动态")
*   [Archives](https://archives.gentoo.org/ "阅读过去的讨论")
*   [Sources](https://sources.gentoo.org/ "浏览我们的源代码")
*   [Infra Status](https://infra-status.gentoo.org/ "获取 Gentoo 提供服务的更新")

[](https://1b9a50f4f9de4348cd9f-e703bc50ba0aa66772a874f8c7698be7.ssl.cf5.rackcdn.com/site-logo.svg "<OBJECT>, image/svg+xml@https://1b9a50f4f9de4348cd9f​-e703bc50ba0aa66772a8​74f8c7698be7.ssl.cf5.rackcdn.com/site-logo.svg")![Gentoo Linux 标志](img/site-logo.png) 开发指南

*   [首页](https://devmanual.gentoo.org//index.html)
*   快速上手 Ebuild 指南
*   [主索引](https://devmanual.gentoo.org/index.html)
*   [通用概念](https://devmanual.gentoo.org/general-concepts/index.html)

### 1. [主索引](https://devmanual.gentoo.org/index.html)

# 快速上手 Ebuild 指南

本页提供了关于 ebuild 编写的简要介绍。它并不试图涵盖开发者遇到的许多细节或问题——而是提供了一些示例，这些示例在尝试理解 ebuild 如何工作的基本原理时可能有所帮助。

若要全面了解所有细节，请参阅 [Ebuild 编写](https://devmanual.gentoo.org/ebuild-writing/index.html)。[通用概念](https://devmanual.gentoo.org/general-concepts/index.html)章节也将很有帮助。请注意，这里使用的示例虽然基于真实的 ebuild，但对部分内容进行了删除、修改和简化。

## 第一个 Ebuild

我们将从为活力的 ctags 工具编写的 ebuild 开始，它是一个源代码索引工具。这是一个简化的 `dev-util/ctags/5.5.4.ebuild`（你可以在主页查看真实的 ebuild）。

```bash
# Copyright 1999-2016 Gentoo Foundation
# 根据 GNU 通用许可证许可证 v2 分发
# $Id$

EAPI=5

DESCRIPTION="Exuberant ctags 生成 tags 文件用于快速导航"
HOMEPAGE="http://ctags.sourceforge.net"
SRC_URI="mirror://sourceforge/${P}.tar.gz"

LICENSE="GPL-2"
SLOT="0"
KEYWORDS="~mips ~sparc ~x86"

src_configure() {
    econf --with-posix
}

src_install() {
    emake DESTDIR="${D}" install
    dodoc FAQ README
    dohtml EXTENDING.html
}
```

### 基础格式

如你所见，ebuild 只是在特殊环境中执行的 bash 脚本。ebuild 的顶部是一个头部块。该块存在于所有的 ebuild 中。ebuild 使用制表符（tabs）缩进，每个制表符代表四个空格。参阅 [Ebuild 文件格式](https://devmanual.gentoo.org/ebuild-writing/file-format/index.html)。

### 信息变量

接下来是一系列变量。这些变量告诉 Portage 关于该 ebuild 和软件包的各种信息。ebuild 的 `EAPI`，请参见 [EAPI 使用和描述](https://devmanual.gentoo.org/ebuild-writing/eapi/index.html)。

`DESCRIPTION` 变量被设置为软件包及其目的的简短描述。`HOMEPAGE` 是指向软件包主页的链接（记得包含 `http://` 部分）。

`SRC_URI` 告诉 Portage 用于下载源码 tar 包的地址。在这里，`mirror://sourceforge/` 是一个特殊的表示法，意味着“Sourceforge 的任何一个镜像”。`${P}` 是由 Portage 设置的只读变量，代表软件包的名称和版本——在这种情况下，它将是 `ctags-5.5.4`。

`LICENSE` 是 `GPL-2`（通用公共许可证第 2 版）。`SLOT` 变量告诉 Portage 该软件包安装到哪个槽（slot）。如果你以前见过槽位，可以直接使用 `"0"` 或阅读 [槽位机制](https://devmanual.gentoo.org/general-concepts/slotting/index.html)。

`KEYWORDS` 变量设置为测试过该 ebuild 的架构。我们使用 `~` 关键字表示新写的 ebuild——即使它们看起来可以工作也不会直接提交到稳定版。详情请参阅 [关键字](https://devmanual.gentoo.org/keywording/index.html)。

### 构建函数

接下来是一个名为 `src_configure` 的函数。Portage 在想要配置软件包时调用此函数。`econf` 函数是调用 `./configure` 的封装器。如果由于某些原因在 `econf` 中发生错误，Portage 将停止而不是继续安装。

`src_install` 函数由 Portage 在想要安装软件包时调用。这里有一个微妙之处——我们不是直接安装到文件系统，而是必须安装到由 `${D}` 变量指定的特殊位置（Portage 设置它——参阅 [安装目标](https://devmanual.gentoo.org/general-concepts/install-destinations/index.html) 和 [沙箱](https://devmanual.gentoo.org/general-concepts/sandbox/index.html)).）。注意：标准的安装方法是 `emake DESTDIR="${D}" install`。这适用于任何编写良好的标准 Makefile。如果产生沙箱错误，请尝试 `einstall`。如果仍然失败，请参阅 [src_install](https://devmanual.gentoo.org/ebuild-writing/functions/src_install/index.html) 获取如何进行手动安装。

`dodoc` 和 `dohtml` 是将文件安装到 `/usr/share/doc` 相关部分的辅助函数。

ebuild 可以定义其他函数（参阅 [Ebuild 函数](https://devmanual.gentoo.org/ebuild-writing/functions/index.html)）。在所有情况下，Portage 都提供一个合理的默认实现，这种实现通常能“正确处理”。例如，这里没有定义 `src_unpack` 和 `src_compile` 函数——`src_unpack` 函数用于解压任何 tar 包或对源码进行补丁，但默认实现在这种情况下完成了我们需要的一切。同样，默认的 `src_compile` 函数将调用 `emake`，它是 `make` 的封装器。




这里是 `app-misc/detox/detox-1.1.1.ebuild`:

```bash
# Copyright 1999-2016 Gentoo Foundation
# Distributed under the terms of the GNU General Public License v2
# $Id$
EAPI=5
DESCRIPTION="detox safely removes spaces and strange characters from filenames"
HOMEPAGE="http://detox.sourceforge.net/"
SRC_URI="mirror://sourceforge/${PN}/${P}.tar.bz2"
LICENSE="BSD"
SLOT="0"
KEYWORDS="~hppa ~mips sparc x86"
RDEPEND="dev-libs/popt"
DEPEND="${RDEPEND} sys-devel/flex sys-devel/bison"
src_configure() { econf --with-popt }
src_install() { emake DESTDIR="${D}" install dodoc README CHANGES }
```

再次，你可以看到 ebuild 头部以及各种信息变量。在 `SRC_URI` 中，`${PN}` 被用于获取不带版本后缀的包名（还有更多此类变量——请参见[预定义只读变量](https://devmanual.gentoo.org/ebuild-writing/variables/index.html#predefined-read-only-variables)）。

再次，我们定义了 `src_configure` 和 `src_install` 函数。

`DEPEND` 和 `RDEPEND` 变量是 Portage 确定构建和运行该包所需的包的方式`DEPEND` 变量列出了编译依赖，而 `RDEPEND` 列出了运行时依赖。更多复杂的示例请参见[依赖关系](https://devmanual.gentoo.org/general-concepts/dependencies/index.html)。

## 带有补丁的 Ebuild

通常我们需要应用补丁。这是在 `src_prepare` 函数中使用 `epatch` 辅助函数完成的。要使用 `epatch`，必须先告诉 Portage 需要 `eutils` eclass（eclass 类似于库）——这是通过在 ebuild 顶部的 `inherit eutils` 实现的。这里是 `app-misc/detox/detox-1.1.0.ebuild`:

```bash
# Copyright 1999-2016 Gentoo Foundation
# Distributed under the terms of the GNU General Public License v2
# $Id$
EAPI=5
inherit eutils
DESCRIPTION="detox safely removes spaces and strange characters from filenames"
HOMEPAGE="http://detox.sourceforge.net/"
SRC_URI="mirror://sourceforge/${PN}/${P}.tar.bz2"
LICENSE="BSD"
SLOT="0"
KEYWORDS="~hppa ~mips ~sparc ~x86"
RDEPEND="dev-libs/popt"
DEPEND="${RDEPEND} sys-devel/flex sys-devel/bison"
src_prepare() { epatch "${FILESDIR}"/${P}-destdir.patch \ "${FILESDIR}"/${P}-parallel_build.patch }
src_configure() { econf --with-popt }
src_install() { emake DESTDIR="${D}" install dodoc README CHANGES }
```

注意 `${FILESDIR}/${P}-destdir.patch` —— 它指向 `detox-1.1.0-destdir.patch`，该文件位于 Portage 树的 `files/` 子目录中。较大的补丁文件必须放在你的开发者空间 `dev.gentoo.org` 上，而不是 `files/` 或镜像站 —— 请参见[Gentoo 镜像](https://devmanual.gentoo.org/general-concepts-mirrors/index.html#gentoo-mirrors) 和[使用 epatch 补丁](https://devmanual.gentoo.org/ebuild-writing/functions/src_prepare/epatch/index.html)。

## 带有 USE Flags 的 Ebuild

现在来看一些 `USE` 标记。这里是 `dev-libs/libiconv/libiconv-1.9.2.ebuild`，它是为没有实现该功能的 `libc` 提供的替代 iconv。

```bash
# Copyright 1999-2016 Gentoo Foundation
# Distributed under the terms of the GNU General Public License v2
# $Id$

EAPI=5

DESCRIPTION="GNU charset conversion library for libc which doesn't implement it"
HOMEPAGE="http://www.gnu.org/software/libiconv/"
SRC_URI="ftp://ftp.gnu.org/pub/gnu/libiconv/${P}.tar.gz"

LICENSE="LGPL-2.1"
SLOT="0"
KEYWORDS="~amd64 ~ppc ~sparc ~x86"
IUSE="nls"

DEPEND="!sys-libs/glibc"

src_configure() {
    econf $(use_enable nls)
}

src_install() {
    emake DESTDIR="${D}" install
}
```

注意 `IUSE` 变量。它列出了 ebuild 中用的所有（非特殊）use 标记。这被用于 `emerge -pv` 的输出等之处。

包的 `./configure` 脚本接受通常 `--enable-nls` 或 `--disable-nls` 参数。我们使用 `use_enable` 工具函数根据用户的 `USE` 标记来自动生成这些参数（参见[查询函数参考](https://devmanual.gentoo.org/function-reference/query-functions/index.html)）。

另一个更复杂的示例，这次是基于 `mail-client/sylpheed/sylpheed-1.0.4.ebuild`:

```bash
# Copyright 1999-2016 Gentoo Foundation
# Distributed under the terms of the GNU General Public License v2
# $Id$
EAPI=5
inherit eutils
DESCRIPTION="A lightweight email client and newsreader"
HOMEPAGE="http://sylpheed.good-day.net/"
SRC_URI="mirror://sourceforge/${PN}/${P}.tar.bz2"
LICENSE="GPL-2"
SLOT="0"
KEYWORDS="alpha amd64 hppa ia64 ppc ppc64 sparc x86"
IUSE="crypt imlib ipv6 ldap nls pda ssl xface"
RDEPEND="=x11-libs/gtk+-2* crypt? ( >=app-crypt/gpgme-0.4.5 ) imlib? ( media-libs/imlib2 ) ldap? ( >=net-nds/openldap-2.0.11 ) pda? ( app-pda/jpilot ) ssl? ( dev-libs/openssl ) xface? ( >=media-libs/compface-1.4 ) app-misc/mime-types x11-misc/shared-mime-info"
DEPEND="${RDEPEND} dev-util/pkgconfig nls? ( >=sys-devel/gettext-0.12.1 )"
src_prepare() { epatch "${FILESDIR}"/${PN}-namespace.diff \ "${FILESDIR}"/${PN}-procmime.diff }
src_configure() {
 econf \
 $(use_enable nls) \
 $(use_enable ssl) \
 $(use_enable crypt gpgme) \
 $(use_enable pda jpilot) \
 $(use_enable ldap) \
 $(use_enable ipv6) \
 $(use_enable imlib) \
 $(use_enable xface compface)
}
src_install() { emake DESTDIR="${D}" install doicon sylpheed.png domenu sylpheed.desktop dodoc [A-Z][A-Z]* ChangeLog* }
```

注意可选依赖。某些 `use_enable` 行使用了两个参数的版本 —— 这在 `USE` 标记名称不完全匹配 `./configure` 参数时非常有帮助。





*   [Pacho Ramos](https://wiki.gentoo.org/wiki/User:Pacho "User:Pacho") (Pacho) - *开发者*
*   [Richard Freeman](https://wiki.gentoo.org/wiki/User:Rich0 "User:Rich0") (rich0) - *开发者*
*   [Mikle Kolyada](https://wiki.gentoo.org/wiki/User:Zlogene "User:Zlogene") (Zlogene) - *开发者*

### 子项目（及继承成员）

| 类别 | 详情 |
| :--- | :--- |
| [Gentoo/AMD64 架构测试员](https://wiki.gentoo.org/wiki/Project:AMD64_Arch_Testers "Project:AMD64 Arch Testers") | 父项目 |
| [Gentoo Base 系统](https://wiki.gentoo.org/wiki/Project:Base "Project:Base") | [项目列表](https://wiki.gentoo.org/wiki/Project:Gentoo "Project:Gentoo") |

## 文档

AMD64 项目提供以下文档：

*   [AMD64 常见问题](https://wiki.gentoo.org/wiki/AMD64/FAQ "AMD64/FAQ")
*   [AMD64 手册](https://wiki.gentoo.org/wiki/Handbook:AMD64 "Handbook:AMD64")
*   [32 位 Chroot 指南](https://wiki.gentoo.org/wiki/Project:AMD64/32-bit_Chroot_Guide "Project:AMD64/32-bit Chroot Guide")
*   此外，与开发相关的文档列在下方的资源部分。

## 资源

AMD64 项目提供的资源包括：

*   AMD64 邮件列表
*   #gentoo-amd64 IRC 频道
*   [AMD64 论坛](https://forums.gentoo.org/viewforum-f-46.html)
*   [Bugzilla](https://bugs.gentoo.org/)
*   [app-emulation/emul-linux-x86-* 包的包列表](http://dev.gentoo.org/%7Epacho/emul.html)
*   [修复 -fPIC 错误指南](https://wiki.gentoo.org/wiki/Project:AMD64/Fixing_-fPIC_Errors_Guide "Project:AMD64/Fixing -fPIC Errors Guide")

## 群组 (Herds)

AMD64 项目维护以下群组：

| 群组 | 成员 | 描述 |
| :--- | :--- | :--- |
| `amd64` | Chainsaw, ago, angelos, hparker, nimiux, pacho, rich0, zlogene | 特定于 x86_64 的包

## 参与

有多种方法可以帮助该发行版及其社区：

*   在邮件列表、[论坛](https://forums.gentoo.org/)或 Freenode 上的 #gentoo-amd64 IRC 频道上回答问题。
*   在 [Bugzilla](https://bugs.gentoo.org/) 上为每个发现的 bug 提交报告。
*   申请[架构测试员](https://wiki.gentoo.org/wiki/Project:AMD64_Arch_Testers "Project:AMD64 Arch Testers") 职位。

检索自 "[http://wiki.gentoo.org/index.php?title=Project:AMD64&oldid=384980]"[分类](https://wiki.gentoo.org/wiki/Special:Categories "Special:Categories"):

*   [Gentoo 项目](https://wiki.gentoo.org/wiki/Category:Gentoo_Projects "Category:Gentoo Projects")

![cover](img/cover_image.jpg)

## 目录

*   内容
*   gentoo.org 
*   导航
*   搜索
*   1 简介
*   2 安装
*   2.1 AMD64 和 EM64T 有什么区别？
*   2.2 我应该使用什么 CFLAGS？
*   2.3 我应该使用什么内核？
*   2.4 使用 64 位系统代替 32 位会有性能提升吗？
*   2.5 什么是 multilib？我如何使用它？
*   2.6 我如何创建一个 32 位 chroot？
*   2.7 我可以通过 emerge -e @world 将我的 x86 系统升级到 AMD64 吗？
*   2.8 我可以使用 Reiser4 吗？
*   3 硬件
*   3.1 我的二进制 NVIDIA/ATI 驱动能用吗？





# 介绍

本文档包含了关于在 `amd64` 系统上使用 Gentoo Linux 的常见问题。这些问题中的许多一个来自[论坛](http://forums.gentoo.org/)、IRC 以及各种[邮件列表](https://www.gentoo.org/get-involved/mailing-lists/all-lists.html)。[AMD64 项目](https://wiki.gentoo.org/wiki/Project:AMD64 "Project:AMD64") 为该架构上的 Gentoo Linux 提供支持。如果你对此常见问题解答（FAQ）有建议或疑问，请在相关的[讨论页](https://wiki.gentoo.org/wiki/Talk:AMD64/FAQ "Talk:AMD64/FAQ") 上留言。

### 安装

### AMD64 和 EM64T 之间有什么区别？

两者都指的是 64 位处理器，分别来自 AMD (`AMD64`) 和 Intel (`EM64T`)。AMD 的 64 位处理器包括 Athlon 64、Turion、Neo、Phenom 和 Opteron 家族。Intel 的 64 位处理器包括 Core 2、Core i *X*、Celeron、Xeon 和 Pentium（均基于 Core 2 架构）。旧版 Pentium 4 和 Xeon 芯片的[最后几个](https://en.wikipedia.org/wiki/x86-64#Intel_64) 也支持 `EM64T`。

AMD 的 64 位处理器系列发布早于 Intel 的产品。因此，出于历史原因，Gentoo 中所有兼容 x86-64 架构的架构关键字均为 `amd64`。因此，`AMD64` 是 64 位芯片的泛指，无论 AMD 还是 Intel。

### 我应该使用什么 CFLAGS？

你应该使用简单的 `CFLAGS` 以避免以后出现系统问题。对于 AMD 和 Intel (`EM64T`) 系统，支持的 `CFLAGS` 值为 `-O2 -march=native -pipe`。

###应该使用什么内核？

你可以使用 Portage 中提供的几乎所有的内核源。我们推荐使用 [sys-kernel/gentoo-sources](https://packages.gentoo.org/packages/sys-kernel/gentoo-sources)，因为它是一个为 Gentoo Linux 设计的特殊内核。它包含了许多 AMD64 特有的补丁，因此是 Gentoo/AMD64 官方支持的内核。

确保你在内核中激活了 `IA32_EMULATION` 选项。

```bash
root # cd /usr/src/linux
root # make menuconfig
```
`KERNEL Enabling IA32 emulation`

```
 Executable file formats / Emulations  --->
  [*] IA32 Emulation
```

**警告**

如果你禁用了此选项，在[multilib](https://wiki.gentoo.org/wiki/Multilib "Multilib") 系统上可能会遇到编译失败。

### 使用 64 位系统代替 32 位系统会有性能提升吗？

这是一个很难回答的问题。在某些情况下，你会获得性能提升，而在另一些情况下则不会。对于日常使用，64 位和 32 位之间几乎没有区别。在浮点计算方面，64 位通常更快，这通常是多媒体应用和 3D 渲染中的情况。Linux.com 的文章 ["Gentoo Linux 中的 64 位性能"](http://www.linux.com/articles/114024?tid=121) 和 ["64 位 Linux 和 BSD 正在稳定增长"](http://www.linux.com/feature/43873) 可能会让你感兴趣。还有一个非常不错的帖子，["文章：Gentoo Linux 中的 64 位性能"](https://forums.gentoo.org/viewtopic-t-349691.html)。

### 什么是 multilib，我该如何使用它？

每个 AMD64 处理器都能运行 32 位代码和 64 位代码。然而，当你有 32 位应用程序时，无法将其与 64 位库混合。你可以通过选择相应的配置（profile）来决定是否支持 [multilib](https://wiki.gentoo.org/wiki/Multilib "Multilib")。默认是启用 multilib 的配置。

**警告**

目前不支持从无 multilib 切换到 multilib（[转换提示](http://jkroon.blogs.co.za/it/gentoo/converting-no-multilib-to-multilib)），因此在使用无 multilib 的配置之前请考虑你的决定。

###我如何创建一个 32 位的 chroot？

请阅读 [32bit chroot 指南](https://wiki.gentoo.org/wiki/Project:AMD64/32-bit_Chroot_Guide "Project:AMD64/32-bit Chroot Guide)。

###我可以通过执行 emerge -e @world 从 x86 系统升级到 AMD64 吗？

由于 **x86** (32 位) 和 **amd64** (64 位) 安装之间的若干差异，通过这种方式是不可能的。请使用 [AMD64 Handbook](https://wiki.gentoo.org/wiki/Handbook:AMD64 "Handbook:AMD64) 进行全新安装。

###我可以使用 Reiser4 吗？

Gentoo Kernel 项目提供的任何内核均未提供 Reiser4，因此 AMD64 团队不支持它。答案是不。

# 硬件

### 我的二进制 NVIDIA/ATI 驱动可以工作吗？

是的，NVIDIA 和 ATI 提供了适用于 AMD64 的驱动。你可以通过执行 `emerge x11-drivers/nvidia-drivers` 或 `emerge x11-drivers/ati-drivers` 来安装它们。如果你对这些驱动有更多问题，应该阅读 [nvidia-drivers 指南](https://wiki.gentoo.org/wiki/NVidia/nvidia-drivers "NVidia/nvidia-drivers") 或 [ATI FAQ](https://wiki.gentoo.org/wiki/ATI_FAQ "ATI FAQ")。

###我如何使用 Cool'n'Quiet/PowerNow/SpeedStep 功能？

# 

###我可以让 Adobe Flash 运行吗？

###我想安装包 foo，但 emerge 说：(masked by: ~amd64 keyword)

###我想安装包 foo，但 emerge 提示：(masked by: missing keyword)

#我如何能帮助 Gentoo/AMD64 项目？

###我如何提供帮助？

# 其他资源

###我可以在哪里获得更多关于 Gentoo/AMD64 的帮助或信息？





你必须编译一个支持这些特性的内核。你只需要启用下面的功能即可：`KERNEL` `Kernel options for Cool'n'Quiet/PowerNow/SpeedStep`

```
 Power management and ACPI options --->
  [*] Device power management core functionality
  [*] ACPI (Advanced Configuration and Power Interface) Support --->
    <*>   Processor
    <*>     Thermal Zone
  CPU Frequency scaling --->
  [*] CPU Frequency scaling
         Default CPUFreq governor (ondemand) --->
  -*-   'performance' governor
  <*>   'userspace' governor for userspace frequency scaling
  -*-   'ondemand' cpufreq policy governor
  <*>   ACPI Processor P-States driver
  CPU Idle  --->
    -*- CPU idle PM support
```

然后执行 `emerge sys-power/cpupower` 并使用首选文本编辑器编辑 `/etc/conf.d/cpupower`。

### 文件 `/etc/conf.d/cpupower` 配置示例

```
 # 启动 cpufreq 时的选项（传递给 `cpufower` 程序）
START_OPTS="--governor ondemand"

# 停止 cpufreq 时的选项（传递给 `cpufower` 程序）
STOP_OPTS="--governor performance"
```

## 应用

### 我可以让 Adobe Flash 运行吗？

可以。执行 `emerge [www-plugins/adobe-flash](https://packages.gentoo.org/packages/www-plugins/adobe-flash)`。在 ebuild 安装完成后，务必阅读显示的任何信息。

**警告**

[www-plugins/adobe-flash](https://packages.gentoo.org/packages/www-plugins/adobe-flash) 包已经陈旧且过时，Adobe 将很快对其停止维护。请参阅 [Adobe Flash](https://wiki.gentoo.org/wiki/Adobe_Flash "Adobe Flash") 文章获取更更新的信息。

### 我想安装包 foo，但 emerge 提示：（masked by: ~amd64 keyword)

这意味着该包仍处于“测试”树中。请阅读 Portage 的手册页（`man portage`）或 [AMD64 手册](https://wiki.gentoo.org/wiki/Handbook:AMD64 "Handbook:AMD64") 中的 [混合软件分支](https://wiki.gentoo.org/wiki/Handbook:AMD64/Portage/Branches "Handbook:AMD64/Portage/Branches") 章节获取更多信息。

### 我想安装包 foo，但 emerge 提示：（masked by: missing keyword)

这意味着该包尚未经过测试。这*并不一定*意味着该包无法正常工作。你可以通过接受该包的另一种架构（或一组架构）来取消屏蔽。以下示例显示了如何告诉 Portage 接受在任何关键字下安装指定的包。

```bash
root # echo "category/packagename" >> /etc/portage/package.accept_keywords
root # emerge packagename
```

如果它对你运行良好，请告诉我们并在 [Gentoo's Bugzilla](https://bugs.gentoo.org/) 上提交 bug，这样 AMD64 团队就可以为该包标记关键字，其他用户也能从你的测试中受益。

**警告**

不要尝试调用类似 `ACCEPT_KEYWORDS="~x86" emerge packagename` 的命令。这极有会破坏 Portage 树并导致系统失效。

 我可以如何帮助 Gentoo/AMD64 项目？

### 我可以如何帮助？

随着 `amd64` 架构日益流行，我们越来越需要更多的帮助。提高 Gentoo/AMD64 的质量仍有很多工作要做。普通用户可以通过以下方式帮助我们：

*   提交常规 bug 报告。
*   测试还没有 `~amd64` 关键字的软件。
*   参与 [Arch testers 项目](https://wiki.gentoo.org/wiki/Project:Arch_Testers "Project: Arch Testers")。
*   帮助邮件列表、论坛和 IRC 频道回答问题。
*   发送补丁。

## 其他资源

### 我可以在哪里获得关于 Gentoo/AMD64 的更多帮助或信息？

如果你的任何问题在这里没有得到解答，你可以尝试[项目主页](https://wiki.gentoo.org/wiki/Handbook:AMD64 "Handbook:AMD64") 列出的其他资源。你也可以在 chat.freenode.net 的 #gentoo-amd64、[Gentoo/AMD64 论坛](https://forums.gentoo.org/viewforum-f-46.html) 或通过 gentoo-amd64@lists.gentoo.org 邮件列表向我们提。

***

本文基于以前位于我们主网站 [gentoo.org](http://www.gentoo.org/) 的文档。

以下人员对原始文档有贡献：**Simon Stelling, Luis Medinas, Gerald J. Normandin Jr., Xavier Neys, nightmorph+**

他们被列在此是因为 Wiki 历史不允许进行任何外部归属。如果你编辑了 Wiki 文章，请**不要**将自己添加到此处；你的贡献将记录在历史页面上。取自 "[`wiki.gentoo.org/index.php?title=AMD64/FAQ&oldid=488184`](http://wiki.gentoo.org/index.php?title=AMD64/FAQ&oldid=488184)"[分类](https://wiki.gentoo.org/wiki/Special:Categories "Special:Categories")：

*   [包含元数据的文档](https://wiki.gentoo.org/wiki/Category:Documents_containing_Metadata "Category:Documents containing Metadata")
*   [核心系统](https://wiki.gentoo.org/wiki/Category:Core_system "Category: Core system")

![cover](img/cover_image.jpg)





# 常见问题解答 (FAQ)

本文汇总了来自 gentoo-dev 邮件列表和 IRC Gentoo 频道的常见。

## 1 简介

## 2 入门指南
### 2.1 什么是 Gentoo？它意味着什么？
### 2.2 Gentoo 有何不同之处？

## 3 安装
### 3.1 使用 `-O` 和 `-fomit-pointer` 后系统非常不稳定。这是怎么回事？
### 3.2 如何更改 root（或其他用户）的密码？
### 3.3 如何添加普通用户？
### 3.4 为什么我的用户无法切换 到 root 用户？
### 3.5 我可以将 Gentoo 从一个版本直接升级到另一个版本吗？
### 3.6 我的内核无法启动，我该怎么办？
### 3.7 我的代理需要身份验证，我该怎么办？
### 3.8 如何刻录 ISO 镜像？
### 3.9 我应该使用哪个 CD/stage？
### 3.10 重启后无法连接网络。哪里出问题了？
### 3.11 尝试从 GRUB 或 LILO 启动时只显示黑屏。我该怎么办？
### 3.12 如何使用 stage1 或 stage2 tar 包安装 Gentoo？

## 4 软件包管理
### 4.1 软件包以什么形式存储？
### 4.2 我想手动执行 `./configure` 步骤。可以吗？
### 4.3 如果 `rsync` 对我不起作用怎么办？
### 4.4 我家里的网络连接很慢（或没有）。我可以在其他地方下载源码并将其添加到我的系统中吗？
### 4.5 源码 tar 包收集在 `/usr/portage/distfiles/` 中。删除这些文件安全吗？





# 4.6 /var/tmp/portage 里面有什么？删除 /var/tmp/portage 中的文件和目录安全吗？（FAQ%20-%20Gentoo%20Wiki_split_005.html_What_is_in_.2Fvar.2Ftmp.2Fportage.3F_Is_it_safe_to_delete_the_files_and_directories_in_.2Fvar.2Ftmp.2Fportage.3F）

# 5 使用（FAQ%20-%20Gentoo%20Wiki_split_006.html_Usage）

## 5.1 我该如何设置国际键盘布局？（FAQ%20-%20Gentoo%20Wiki_split_006.html_How_do_I_set_up_an_International_Keyboard_Layout.3F）

## 5.2 DNS 域名解析仅对 root 有效（FAQ%20-%20Gentoo%20Wiki_split_006.html_DNS_name_resolution_works_for_root_only）

## 5.3 为什么我的用户不能使用自己的 crontab？（FAQ%20-%20Gentoo%20Wiki_split_006.html_Why_can.27t_my_user_use_their_own_crontab.3F）

## 5.4 我如何让 numlock 在开机时启动？（FAQ%20-%20Gentoo%20Wiki_split_006.html_How_do_I_get_numlock_to_start_on_boot.3F）

## 5.5 我该如何在注销时清空终端？（FAQ%20-%20Gentoo%20Wiki_split_006.html_How_do_I_have_my_terminal_cleared_when_I_log_out.3F）

# 6 维护（FAQ%20-%20Gentoo%20Wiki_split_007.html_Maintenance）

## 6.1 ReiserFS 和文件系统损坏问题 - 如何修复它们等（FAQ%20-%20Gentoo%20Wiki_split_007.html_ReiserFS_and_filesystem_corruption_issues_-_how_to_fix_them.2C_etc）

# 7 开发（FAQ%20-%20Gentoo%20Wiki_split_008.html_Development）

## 7.1 我可以在哪里报告 bug？（FAQ%20-%20Gentoo%20Wiki_split_008.html_Where_can_I_report_bugs.3F）

## 7.2 新版本多久发布一次？（FAQ%20-%20Gentoo%20Wiki_split_008.html_How_often_are_new_releases_made.3F）

## 7.3 我的扬声器疯狂地响响。我该如何禁用控制台蜂鸣？（FAQ%20-%20Gentoo%20Wiki_split_008.html_My_speaker_beeps_like_crazy._How_do_I_disable_console_beeps.3F）

# 8 资源（FAQ%20-%20Gentoo%20Wiki_split_009.html_Resources）

## 8.1 哪里可以找到关于 Gentoo Linux 的更多信息？（FAQ%20-%20Gentoo%20Wiki_split_009.html_Where_can_I_find_more_information_about_Gentoo_Linux.3F）

## 8.2 我可以买 Gentoo Linux 的 CD 吗？（FAQ%20-%20Gentoo%20Wiki_split_009.html_Can_I_buy_a_CD_of_Gentoo_Linux.3F）

## 8.3 这个 FAQ 没有回答我的问题。我现在该怎么办？（FAQ%20-%20Gentoo%20Wiki_split_009.html_This_FAQ_has_not_answered_my_question._What_do_I_do_now.3F）

### 简介

请注意，这些问题中的许多已经在官方 Gentoo 文档和指南中得到了解答。这仅仅是一个常见问题列表。请阅读 Gentoo 文档和 man 页面，以更深入地了解 Gentoo 和 GNU/Linux 的工作原理，并获取此处未涵盖问题的答案。

# 入门

### Gentoo 如何读音？它是什么意思？

*Gentoo* 的读音为 "gen-too"（"Gentoo" 中的 "g" 是软音，就像 "gentle" 中一样）。[Gentoo 企鹅](https://en.wikipedia.org/wiki/Gentoo_penguin) 的学名为 `Pygoscelis papua`。`Gentoo` 这个名字是由[福尔克兰群岛](https://en.wikipedia.org/wiki/Falkland_Islands) 的居民给企鹅起的。

### 什么让 Gentoo 与众不同？

Gentoo 使用了一个类似于 BSD ports 的系统称为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage")。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。GentooGentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。GentooGentoo 使用了一个了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。GentooGentoo 使用了一个了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。Gentoo 使用了一个名为 [Portage](https://wiki.gentoo.org/wiki/Project:Portage "Project:Portage") 的类 BSD ports 系统。Portage 是一个包管理系统，在 Gentoo 系统上安装和维护软件时提供了极大的灵活性。它提供了编译选项支持（通过 [USE flags](https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/USE "Handbook:AMD64/Working/USE")），允许用户控制编译的特性。GentooGentoo 1.4 及后续版本是基于 `glibc-2.3.x`（更高）的。因此，运行 `emerge --sync && merge -uDN @world` 将整个系统更新到“最新”。不同版本之间的差异在于安装介质和预编译包。请查看 [Gentoo 升级指南](https://wiki.gentoo.org/wiki/Upgrading_Gentoo) 以了解更多关于配置及其在升级中作用。

此外注意，`emerge -uDN world` 更新已安装的包及其依赖，但不会更新构建依赖（构建时需要但安装时不需要的包）。要同时更新这些包，请添加 `--with-bdeps=y` 选项。

### 安装

### 使用 -O2 时某些项是不稳定的

Gentoo 使用源码编译。使用 `-O2 -omit-pointer` 编译内核。

### 我如何更改 root（或任何用户）的密码？

使用 `passwd` 命令更改密码。参见 `man passwd`。

### 我如何添加普通用户？

`useradd larry` 会添加一个名为 `larry` 的用户。然而，这种方法没有赋予用户足够的权限，因此推荐以下命令：

```bash
useradd -m -G users,wheel larry
```

这将添加用户 `larry`。`-G` 选项将用户添加到多个组：

* `users`: 交互用户的标准组
* `audio`: 访问音频设备
* `wheel`: 可以执行 su

### 为什么用户不能 su root？

出于安全考虑，只有属于 `wheel` 组的用户才能 su root。要将用户名添加到 `wheel` 组，请以 root 身份执行以下命令：

```bash
gpasswd -a <username> wheel
```

# 包管理

### 包以什么形式存储？




软件包本身并不是被“存储”的。相反，Gentoo 提供了一组脚本，可以解析依赖关系、获取源代码并编译出一个根据用户需求定制的软件包版本。通常，Gentoo 仅为发布版（releases）和快照构建二进制文件。[Gentoo 开发者手册](http://devmanual.gentoo.org/ebuild-writing/index.html) 详细介绍了 ebuild 脚本的内容。

对于完整的 ISO 发布版，将使用增强型的 `.tbz2` 格式创建全套二进制包，该格式与 `.tar.bz2` 兼容，并在文件末尾附加了元数据。可以使用这些包快速、高效地安装一个运行良好的（尽管未完全优化的）软件包版本。

可以使用 Gentoo 的 Portage 创建 RPM（红帽软件包管理器文件），但目前还无法使用已有的 RPM 来安装软件包。

### 我想自己执行 `./configure` 步骤。可以吗？

可以，但这并不易事，也不推荐这样做。由于执行此方法需要对 Portage 内部和命令有良好的理解，因此建议对 ebuild 进行补丁以实现用户所需的任何操作，并将其放在 Portage overlay 中（这就是为什么存在 overlay 的原因）。这对于维护性来说`要好得多`，而且通常更简单。更多信息请参见 [Gentoo 开发者手册](http://devmanual.gentoo.org/ebuild-writing/index.html)。

### 如果 rsync 对我不起用怎么办？

当处于不允许 rsync 流量通过端口 `873` 的防火墙后，可以使用 `emerge-webrsync` 命令通过常规 HTTP 获取并安装 Portage 快照。有关如何通过代理下载源文件和 Portage 快照，请参阅此章节。

### 我家的网络连接很慢（或没有）。我可以在其他地方下载源码并将它们添加到我的系统中吗？

绝对可以。运行 `emerge --pretend package/atom` 查看将要安装哪些程序。要找到这些软件包的源码以及从哪里下载，运行 `emerge -fp package/atom`。下载源码并用任何介质带回家。将源码放在 `/usr/portage/distfiles/` 文件夹中，然后直接运行 `emerge package/atom`。注意：这是一个`非常`繁琐的过程。

### 源码 tarball 堆积在 /usr/portage/distfiles/。删除这些文件安全吗？

删除这些文件对日常性能没有负面影响。然而，保留最新版本的文件可能是明智的；通常对于特定软件的同一会发布多个 ebuild。如果删除了存档且软件被升级或重新构建，则需要重新从互联网下载它们。

使用来自 [app-portage/gentoolkit](https://packages.gentoo.org/packages/app-portage/gentoolkit) 的 [eclean](https://wiki.gentoo.org/wiki/Eclean "Eclean") 脚本来管理 `/usr/portage/distfiles/` 以及其他位置的内容。请阅读 `man eclean` 了解更多关于它的用法，以及 [Gentoolkit 文章](https://wiki.gentoo.org/wiki/Gentoolkit "Gentoolkit")。

### /var/tmp/portage 里有什么？删除 /var/tmp/portage 中的文件和目录安全吗？

在编译期间，Gentoo 将软件包源码保存在 `/var/tmp/portage` 中。这些文件和文件夹通常在合并成功后删除，但有时会失败。如果 `emerge` 命令没有运行，则清理此目录的所有内容是安全的。在清理此目录之前，务必始终运行 `pgrep emerge`。

## 使用

### 我如何设置国际键盘布局？

编辑 `/etc/conf.d/keymaps` 中的 `keymap` 变量。为了让控制台正确处理 keymap 中的扩展字符，可能需要在 `/etc/conf.d/consolefont` 文件中设置 `consolefont` 和 `consoletransation` 变量（有关环境本地化的更多信息，请参考[本地化指南](https://wiki.gentoo.org/wiki/Localization/Guide "Localization/Guide")）。然后，执行重启，或重启 keymaps 和 consolefont 脚本：

```
`root #` `/etc/init.d/keymaps restart`
`root #` `/etc/init.d/consolefont restart`
```

### DNS 名称解析仅对 root 有效

`/etc/resolv.conf` 权限错误；按如下方式对其进行 `chmod`：

```
`root #` `chmod 0644 /etc/resolv.conf`
```

### 为什么我的用户不能使用自己的 crontab？

将该用户加入 cron 组：

```
`root #` `gpasswd -a <username> cron`
```

### 我如何让 numlock 在启动时启动？

以下命令将把 numlock 服务添加到默认运行级别，在启动时启用 numlock：

```
`root #` `rc-update add numlock default`
`root #` `/etc/init.d/numlock start`
```

每个 GUI 都为此类工作提供不同的工具；请检查你所选 GUI 的帮助部分或在线手册以获取进一步帮助。

### 我如何在注销时清除终端？

要清除终端，请在用户的 `~/.bash_logout` 脚本中添加 `clear` 命令：

```
`user $` `echo clear >> ~/.bash_logout`
```

为了在添加新用户时自动执行此操作，对 `/etc/skel/.bash_logout` 文件执行相同的操作：

```
`root #` `echo clear >> /etc/skel/.bash_logout`
```

## 维护

### ReiserFS 和文件系统损坏问题 - 如何修复它们等

如果 ReiserFS 分区损坏，尝试启动 Gentoo 安装 CD 并在损坏的文件系统上运行 `reiserfsck --rebuild-tree`。这应该让文件系统恢复一致性，尽管由于损坏可能会丢失一些文件或目录。

## 开发

### 我可以在哪里报告 bug？

使用 [Bugzilla](https://bugs.gentoo.org/) 站点报告 bug。在 Freenode IRC 网络上访问 #gentoo，如果不确定某个问题是否真的是 bug，可以问问大家。

### 多久发布一次新版本？

Gentoo 的软件包通常在在上游作者发布新代码后不久更新。至于 Gentoo 本身何时发布新的 stage/profile/ISO 发布版，请查看[发布工程项目](https://wiki.gentoo.org/wiki/Project:RelEng "Project:RelEng") 页面。新版本会在 [gentoo-announce](https://www.gentoo.org/get-involved/mailing-lists/) 邮件列表上公布。更多信息请参阅此章节。

### 我的扬声器疯狂鸣响。我如何禁用控制台鸣声？

可以使用 `setterm` 关闭控制台鸣声，如下：

```
`root #` `setterm -blength 0`
```

要在启动时关闭控制台鸣声，将以下命令放在 `/etc/conf.d/local.start` 文件中。然而，这将禁用当前终端的鸣声。要禁用其他终端的鸣声，将命令输出重定向到目标终端，如下：

```
`root #` `setterm -blength 0 > /dev/vc/1`
```

将 `/dev/vc/1` 替换为需要禁用控制台鸣声的终端。

## 资源

### 关于 Gentoo Linux 的更多信息可以在哪里找到？

大部分官方文档可以在 Wiki 上找到。

### 我可以买 Gentoo 的 CD 吗？

无法自行下载和刻录安装 CD 的用户可以通过我们的授权商店找到。然而，大多数商店已经不再提供 CD 和 DVD，因为这些安装介质很快就会过时。

授权商店列在[页面](https://www.gentoo.org/inside-gentoo/stores/)上。

### 这个 FAQ 没有回答我的问题。我现在该怎么办？

第一步是浏览相关的[文档](https://www.gentoo.org/support/documentation/)，如果失败，可以查看[此处]列出的各种 Gentoo Linux 邮件列表](https://www.gentoo.org/get-involved/mailing-lists/)。如果一切都失败了，或者只想与 Gentoo 朋友聊天，请在 Freenode IRC 频道 #gentoo 访问我们。



本文基于此前发布在我们主网站 [gentoo.org](http://www.gentoo.org/) 的文档。

以下人员对原始文档做出了贡献：`Daniel Robbins, Colin Morey, John P. Davis, Eric Stockbridge, Stoyan Zhekov, Carl Anderson, Jorge Paulo, Benny Chuang, Jonathan Smith, nightmorph`

他们在此列出是因为 Wiki 历史记录不允许任何外部归属。如果您编辑了此 Wiki 文章，请`不要`在此处添加您的姓名；您的贡献将记录在历史页面上。

取自 "[`wiki.gentoo.org/index.php?title=FAQ&oldid=477968`](http://wiki.gentoo.org/index.php?title=FAQ&oldid=477968)"[分类](https://wiki.gentoo.org/wiki/Special:Categories "Special:Categories")：

* [包含元数据的文档](https://wiki.gentoo.org/wiki/Category:Documents_containing_Metadata "Category:包含元数据的文档")
* [核心系统](https://wiki.gentoo.org/wiki/Category:Core_system "Category:核心系统")
* 此页面最后修改于 2016 年 3 月 27 日 16:24。
* [隐私政策](https://wiki.gentoo.org/wiki/Gentoo_Wiki:Privacy_policy "Gentoo Wiki:隐私政策")
* [关于 Gentoo Wiki](https://wiki.gentoo.org/wiki/Gentoo_Wiki:About "Gentoo Wiki:关于 Gentoo Wiki")
* [免责声明](https://wiki.gentoo.org/wiki/Gentoo_Wiki:General_disclaimer "Gentoo Wiki:通用免责声明")
* [](https://twitter.com/gentoo "@Twitter 上的 Gentoo")
* [](https://plus.google.com/+Gentoo "+Google+上的 Gentoo")
* [](https://www.facebook.com/gentoo.org "Facebook 上的 Gentoo")

**© 2001–2016 Gentoo Foundation, Inc.**

Gentoo 是 Gentoo Foundation, Inc. 的注册。除非另有明确说明，本文档的内容受 [CC-BY-SA-3.0](https://creativecommons.org/licenses/by-sa/3.0/) 许可保护。[Gentoo 名称和标志使用指南](https://www.gentoo.org/inside-gentoo/foundation/name-logo-guidelines.html) 适用。
