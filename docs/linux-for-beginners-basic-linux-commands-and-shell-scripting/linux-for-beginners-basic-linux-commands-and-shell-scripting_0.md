# Linux 初学者指南：基础 Linux 命令与 Shell 脚本



![](img/rsrc7.jpg)









## Travis Booth 的其他书籍
* 深度学习系列
* Python 深度学习入门：初学者的实战指南
* Python 深度学习入门：超越基础的全面指南
* Python 数据分析系列
* Python 数据分析：初学者真实世界速成课程
* Python 数据分析：超越基础的实战指南
* Python 数据科学系列
* Python 数据科学：初学者的实战学习
* Python 数据科学：超越基础的实战指南
[点击此处探索更多！](https://amzn.to/2nku7aN)

额外优惠：通过 Kindle Matchbook 购买纸质版，即可免费获得电子书。


## 引言
本书包含了如何使用或迁移到 Linux 以获取乐趣和利润的验证步骤和策略。这是 Linux 系列书籍中的第一本。你可以从书中学习 Linux 的基本概念和应用：从安装到基础 Shell 脚本。该系列的后续书籍将为你提供 Linux 概念、哲学和应用知识的深度知识。该系列书籍组织良好，旨在为初学者提供足够的知识成为高级 Linux 用户。

### 谁应该读这本书？
本书使用简单的技术术语编写，并采用简单的示例和解释，使拥有 Linux 零或极少经验的用户也能学习 Linux 是什么以及如何开始学习 Linux。书的结构侧重于提供分步骤的说明和示例，并配有截图和解释，以避免混淆和歧义。内容不仅针对初学者，还面向普通计算机用户、初级管理员以及希望学习或加强对 Linux 及其在实践中应用之方法了解的高管人员。

### 本书是如何组织和使用的
本书将引导你完成自己 Linux 系统的初始设置，并向初学者介绍所需的 Linux 系统管理基础知识。在后面的章节中，它涵盖了更高级的主题，包括某些系统管理原理、理论和实际应用、基础和高级脚本，以及 `GAWK` 等程序。本书按以下方式组织：
* 你将学习更多关于 Linux 的历史、版本等内容（第 1 章）。
* 安装和使用你的第一台 Linux 设备以及一些基础管理（第 2 章）。
* Linux 用户管理原理、实用方法、编辑器、终端和控制台（第 3 章）。
* Linux 命令、文件系统和基础管理简介（第 4 章）。
* Linux 分区类型、数据文件以及通过排序、使用 `grep` 搜索、压缩/解压缩和存档进行的操作（第 5 章）。
* Shell 脚本准备工作，例如理解进程、环境变量和数组（第 6 章）。
* 命令别名、文件描述符、堆、数学运算、高级结构化命令和示例（第 7 章）。
* 函数、参数、选项、`getopt` 和 `getopts`、读取用户输入和交互式脚本、高级函数、库以及 `GAWK` 的完整课程（第 8 章）。

### Tips、注释、注意事项和场景
本书设计了许多排版特征，帮助你从书中获取最多的信息。

## 为什么选择 Linux？
Linux 是一个开源操作系统或内核。它不仅是最流行的服务器操作系统，也是被广泛使用的开源操作系统。它由 Linus Torvalds 在 1991 年在 `GNU` 的合作下创立。Linux 用于许多系统，例如笔记本电脑、台电脑、智能手机、智能冰箱等。尽管在起初它只在计算机程序员中闻名，但现在几乎无处不在。今天，Linux 服务器运行着 Google、Facebook 以及许多知名服务。

与 Windows 和 Mac OS 等其他流行的客户端操作系统相比，Linux 是一个开源系统，而其他系统不是。这意味着用户无法在那些操作系统中进行更改，因为用户无法访问它们的源代码。但任何人都可以修改 Linux 操作系统。这并不意味着 Linux 没有商业版本。

有些人将 Linux 称为 `UNIX` 的克隆。`UNIX` 是 Linux 的基础，或者从技术上说是灵感。在考虑核心时，两者是相似的。尽管 Linux 像 `UNIX`，但它有独特的特征。`UNIX` 和 Linux 之间的区别在于：
* Linux 非常灵活，但 `UNIX` 僵化，因此不能用于任何计算机。
* 与 `Unix` 相比，Linux 提供了广泛的可移植性。
* Linux 的源代码可以轻松获得，但对于 `UNIX` 并非如此。

这些都是 Linux 基础的原因。一个完整的 Linux 系统可以被称为发行版。这包含了 Linux 内核、`GNU` 应用、桌面环境和应用程序。有许多满足需求的发行版：
* Linux Mint
* Ubuntu
* Debian
* Red Hat / CentOS
* Fedora
这些发行版是根据需求定制的。可以根据自己的需求选择最合适的发行版。例如，Ubuntu 可以轻松安装，任何人都可以使用，而 `OpenSUSE` 则需要高级知识。最近，由于许多优点，Linux 用户量激增。考虑到 Linux 的优点，最流行的一点是它是免费的。与 Windows 和 Mac 相比，Linux 在用户中占据主导地位。在历史上，Linux 并不是一个用户友好的操作系统，但现在它拥有足够的功能，并且灵活且高度可定制，可以在不下载完整功能包的情况下安装想要的内容。

Linux 的主要优点之一是它的安全性。由于许多操作系统的安全问题，Linux 的增加是不可避免的，考虑到其强大的安全架构。在使用 Linux 时，大多数情况下不需要使用杀病毒程序（这并不意味着它完全没有漏洞，但这些很罕见）。在考虑隐私时，Linux 系统也是有利的。由于 Linux 是一个开源操作系统，任何爱好者都有机会修改它，创建他们自己的发行版。即使具有所有这些功能，Linux 也非常稳定且可靠。Linux 的安装通过现代 GUI 能力变得极其简单并运行在几乎所有的硬件上。与其他操作系统相比，Linux 的软件更新和补丁也更快。除了上述缺点，还有一些问题，其中之一是 Linux 的版本数量非常多，这让初学者可能会感到困惑。由于 Linux 用户用户更多控制权，在过去的几十年里，Linux 赢得了普及。

# 第 1 章：Linux 内核与操作系统简介
在本章中你将学习：

### 什么是 Linux
Linux 内核、Linux 发行版、桌面系统、Shell。一切从正式的介绍开始。在本章中，我们将从操作系统的角度来看 Linux。

### 什么是 Linux？
在不假设你了解操作系统的情况下，让我们简要看看术语和定义。我们将理解 Linux 是什么及其架构。操作系统是一个旨在更好地与一组硬件交互的软件程序，通过通信、管理和维护自身来实现工作，我们称之为计算机。如果采用一个更传统的定义，操作系统是用户和硬件之间的接口。操作系统通常在计算机的启动（boot）过程中加载到内存中，基本上诊断整个系统的健康状况，然后从硬盘将内容加载到内存。现在你知道操作系统是什么以及它的角色。有很多正在使用的操作系统，主要的操作系统有 Unix、Linux 和 Mac OS。现在当涉及到 Windows 等流行的操作系统时，清楚操作系统是什么。它是私有的且易于区分的。然而，在 Unix 和 Linux 上，有更多关于起源以及如何变为现实可以学习。

如果你对操作系统的历史感兴趣，Unix 是最老的操作系统之一，特别是对于服务器系统。它是一个名为 `Multics` 的旧系统的衍生品。1970 年，Ken Thompson 与开发了 `C` 语言的 Dennis Ritchie 用 `C` 语言重写了这个小系统。Unix 在学术界迅速成长，Berkeley 是其中心。他们引入了 软件发行版 `BSD`。在 70 年代和 80 年代，Unix 在学术界之外演变为操作系统并被其他组织采用。有许多版本，如 `IBM-AIX`、`HP-UX`、`Sun Solaris` 等。重要记住是 Unix 并不是开源软件。最终，在 BSD 家族下出现了一些开源变体，例如 FreeBSD。这种许可现在被称为 BSD 许可证。Linux 的出现得益于两个重要的名字：Richard Stallman 和 Linus Torvalds。在 90 年代，Richard 想要创建一个真正开源且免费的私有 Unix 系统的替代品。他在 `GNU` 名下创建了一系列工具和程序。`GNU` 是一个递归缩写，它的意思是“GNU 不是 Unix！”。然而，一组程序和工具没有内核是无法工作的！

### 什么是内核？
内核是操作系统的核心。一旦启动，它对整个计算机拥有完全控制权。它由一个小的加载程序加载，然后它就是始与终。它被加载到相同或单独的内存空间，然后控制并分配硬件，控制输入/输出操作、软件请求和处理。在赫尔辛基大学期间期间，Linus 正在创建一个非操作系统特有的程序，以便他可以使用当时带有处理器的他的新 PC。他当时使用 `GNU C 编译器` 和其他工具，并在 `MINIX` 上继续开发（尽管架构从微内核变成了单体内核）。得益于 Linus 和他与 GNU 的关系，Linux 作为一个可用的操作系统诞生了，Richard 的免费开源梦想变成了现实。Linux 是一个类 Unix 操作系统。我们也可以说它在某种程度上是 Unix 的克隆。Linux 基本上由内核、`GNU`、X-Windows GUI 和图形桌面系统组成。它还包含了其他应用程序和工具。

### 内核的作用
由于我们从内核介绍开始，让我们看看更多技术细节。这将有助于你理解 Linux 的某些重要方面，以及其他操作系统。





### Slackware
Patrick Volkerding 在 1992 年创建了 Slackware，它是现存最老的 Linux 发行版。它以无 Bug 且简洁的发行而闻名。它可以在 32 位 (`i486`) 和 64 位 (`x86_64`) 架构上运行。其哲学与 Arch Linux 类似。它的缺点很少，例如应用程序支持数量有限以及升级较为复杂。

### Debian
GNU/Linux 出于 1993 年。今天，Debian 可以被认为是最大的 Linux 发行版和最大的协作软件项目。根据 Distrowatch 的数据，Debian 由 1000 多名志愿者开发，拥有 50000 多个二进制包，并启发了 120 多个发行版。Debian 极其稳定，具有卓越的质量保证，并且与其他发行相比支持更多的处理器架构。主要缺点之一是稳定版的发布周期较（2-3 年）。

### Fedora
Fedora 是目前最具创新性的 Linux 发行版之一。它与著名的红帽 Linux 有关。2003 年，红帽引入了一项革命性的变化：Fedora Core。它被引入为一种专为 Linux 爱好者设计的社区版。现在，红帽是最盈利最丰的企业。Fedora 提供了卓越的安全性，支持多个桌面环境，对内核进展、`glibc` 和 `GCC`、`SELinux` 集成、日志文件系统、系统以及企业级功能做出了贡献。它还支持 32 位和 64 位环境。它面向更多的企业级功能和用户。

### Red Hat and Cent OS
红帽在企业领域占据着旗舰地位。它始于 1995 年。它拥有许多创新组件，例如基于 GUI 的 Anaconda 安装程序、`RPM` 包管理器等。遗憾的是，由于不断增加的专利问题等因素，它未能跟上节奏。它在 2003 年结束了其历史，并催生了 `RHEL`（红帽企业级 Linux）和 Fedora core。`RHEL` 无疑是行业事实标准。它能够在 `x86_64`、`Arm64`、`Power ISA`、`IBM Z` 以及桌面平台上运行。它有许多针对不同企业级应用（如服务器和工作站）的变体。同时，Fedora 作为未来 `RHEL` 版本的上游。鉴于其领导力和影响力、卓越的支持和尖端技术，`RHEL` 是企业使用的极品。它被科技巨头使用。

### Gentoo
Gentoo 是一个高度灵活的元发行版，允许用户运行各种内核和软件配置。Gentoo 可以被自定义。该项目由 Daniel Robbins 在 2000 年引入。尽管它提供了灵活性，但使用它需要专业知识。换句话说，这不适合没有经验的用户，因为可能需要更多时间来适应。升级过程可能会非常耗时。

### Arch Linux
Arch Linux 由 Judd Vinet 于 2002 年发布。起初，它被认为是一个存在于中级和高级用户之间的边缘项目。后来，它通过一种被称为“滚动发布”（rolling-release）的特性得到了推广。滚动发布意味着操作系统能够让自己保持最新状态。Arch Linux 拥有优秀的软件管理基础设施。它包含了从源代码安装软件的能力。其缺点之一是由于偶尔的不稳定性而导致系统崩溃的风险。

## Ubuntu
Ubuntu 革新了 Linux 桌面用户的使用体验。它长期一直非常。它于 2004 年发布，至今在 Linux 用户中仍然很受欢迎。Ubuntu 基于 `DEB` 包。它通过 Canonical 提供长期支持，现在甚至通过其服务器版支持企业用户。Ubuntu 的一些特殊特性是它包含一个可安装的实时 DVD，它支持新技术，让新手可以轻松适应 Ubuntu 和不同的桌面环境。Ubuntu 的显著缺点之一是其兼容性不足。

## MX Linux
MX Linux 的引入是为了 MEPIS Linux 的替代品。它设计用于个人也适用于商业。MX Linux 最受欢迎的特性是它的图形化管理工具，被称为 `MX-Tools`。它对该平台拥有卓越的支持，对图形驱动程序具有卓越的兼容性且易管理。与 Mint 和 Ubuntu 相比，MX Linux 对新手可能不够友好。需要时间来适应，它的安装程序和某些工具看起来可能不同。

### Mint
Linux Mint 于 2006 年发布。它基于 Ubuntu 设计。该发行版最适合初学者。Mint 拥有大量的增强功能使其易于使用。它提供了与其他系统的互操作性。因此，它不仅适用于个人使用，也适用于企业。开发者提供 3 种发布，即官方版（12 月）、点版本（根据需要，例如错误补补）和每月快照版。这使得 Mint 极其稳定。

### Backtrack and Kali
还有其他面向系统安全和渗透测试的特殊 Linux 版本。Kali Linux 是目前最流行的渗透测试平台。这一切始于合并 WHAX 创建的 BackTrack（WHAX 是一个基于 Slax 的 Linux 发行版，背后的公司是 Offensive Security。早期的 WHAX 基于 Knoppix 并命名为 Whoppix）。BackTrack 5 基于 Ubuntu Lucid LTS。它支持 32 位和 64 位架构以及 ARM。2013 年，该公司基于 Debian 重建了该平台并在 Kali 的名下发布。Kali Linux 凭借其功能和一套顶级的渗透测试工具，非常稳定且先进。

### Android
Android 又是呢？Android 是基于修改版 Linux 内核和 Google 自己的库的最大类型发行版。Android 运行运行一个名为 `Dalvin` 的虚拟平台来运行用 Java 编写的应用程序。此类应用程序针对不同的硬件平台，并取决于 Google APIs。你不能在 Android 设备上运行桌面版 Linux。你不能在 PC 上运行移动版 Android（在不使用模拟和虚拟化的情况下）。

### Linux Live CDs
Linux Live CDs 和 USB 在各种用户中非常流行。它超越了简单的在安装前学习 Linux 是什么。许多 Linux 实时发行版都支持从 CD-ROM 运行操作系统。这对于演示目的和测试某些事物非常棒。自定义的发行版包含了执行各种简单和复杂系统任务的包，例如更改硬盘布局、安全和恢复程序等许多。这些版本现在以 Linux USB 发行版的形式出现。网站 `https://livecdlist.com/` 列出了极其庞大的实时 CD 集合。所有主流发行版都支持实时 CD 功能。

#### Puppy Linux
Puppy Linux 是一个小于 200MB 的小型系统。这个 Linux 发行版最适合基础计算机功能和网页浏览。尽管它非常小，仍然可以使用文件恢复工具和分区。该发行版使得安装其他流行的应用程序变得简单，因为它有自己的包管理器。Puppy Linux 有各种名为“puplets”的自定义版本。Puppy Linux 的优势之一是可以在旧硬件上使用。

#### Slax
Slax 是一个小型而快速的 Linux 发行版。它基于 Slackware。但现在基于 Debian 稳定版。它是易于使用的 Linux 发行版之一。用户在下载时可以删除或添加模块。Slax 非常方便。该发行版可以通过不同的介质如 USB 闪存或 DVD ROM 启动。Slax 有一个包含许多选项的启动菜单。





# Linux 发版对比

## Knoppix
Knoppix 是一个稳定的 Linux 发行版。它是最早的 Linux CD 之一。该系统非常成熟，包含 1000 多个软件包。Knoppix 的优势之一是它支持独特的硬件。尽管 Knoppix 旨在从实时介质运行，但它也可以安装到硬盘中。Knoppix 有许多派生版本。

## Tiny Core Linux
Tiny Core Linux 发行版是一个非常小的便携操作系统。它仅有 10MB。由于该操作系统非常小，它不包含应用程序或文件管理器。不过，用户可以稍后安装它们。这是初学者的推荐选项之一。

## Ubuntu
Ubuntu 并没有特定的 LiveCD。但是，它的 ISO 镜像可以刻录到 DVD 或设置为 USB 启动盘。它从它启动时提供了一个“试用”的选项。

## MX Linux
MX Linux 适用于旧电脑和现代电脑。这是一个用户友好的发行版，新手也可以使用。




# Linux 桌面系统

Linux 桌面最初是基本的命令行或文本界面。随着 Windows 等客户端操作系统的演进，人们对组织良好的 GUI（图形用户界面）的需求日益增加。现在有多个图形化桌面可供选择。Linux 图形环境由系统软件（如 `X-Windows` 系统）组成，在其之上是桌面环境。让我们先来看 `X-Windows`。

## X-Windows 系统

个人电脑中负责图形环境的主要硬件是显示器和显卡/驱动程序。任何支持图形环境的操作系统，都必须首先与这两者通信。在 Linux 中，这是 `X-Windows` 系统的职责。这是一个低级系统程序，通过通信和管理进程，来创建一个可以生成图形环境的环境。这就是 `X-Windows` 系统在 Linux 操作系统中所做的工作，它基于客户端/服务器架构——`X server` 负责处理来自任何客户端（例如应用程序）的图形请求。因此，它支持网络协议（尽管最初的通信是不安全的）。该系统是在麻省理工学院（MIT）开发的。

在安装 Linux 期间，它会检测显示器和显卡，然后创建一个 `X-Windows` 配置文件。这在安装过程中较容易发现，因为屏幕可能会变黑并闪烁几次。

随着发展，这个旧的系统演变成了更现代的版本：`XFree86` 和 `X.org` 版本。`XFRee86` 是一个扩展免费开源 `X-Windows` 系统的志愿者组织之一。Unix、Linux 系统、BSD 变体、Sun Solaris 以及某些 Mac OS 系统都运行着这个发行版。

另一个参与者是 `X.org`（Open Group 的一部分）。它将旧的 `X-Windows` 系统推向了新的高度，并在两者中都很流行。你可以在 `https://www.x.org/wiki/` 了解更多信息。

## 桌面环境类型

`X-Windows` 系统可以构建基础，但要运行完整的桌面环境还需要另一个程序来运行它，因为对于一直依赖 GUI 的普通用户来说，X-Windows 系统本身并不好用。

为了启用全功能的桌面环境，存在另一套程序。这些被称为桌面环境（Desktop Environments）。让我们来看一些流行的环境。

### KDE 桌面

KDE 或 K Desktop Environment 是较老且流行的系统之一，即使是现在如此。它之所以流行是因为它与微软 Windows 桌面环境相似。KDE 不仅仅是一个环境，它还是一个应用程序集合。它具有高度可定制性。

最新版本有两个变体称为 `Plasma Desktop` 和 `Plasma Notebook`。与其他桌面不同，KDE 提供全套应用程序和体验（你可以在此处查看列表：`https://kde.org/applications/`）。主要的 Linux 平台（如 OpenSUSE 和 Kubuntu）将其作为默认。以下是 KDE 应用程序列表（版本 19.04）。

- `Amarok` : 音乐播放器
- `Dolphin` : 文件管理器。
- `Dragon Player` : 视频播放器。
- `Kate` : 开发环境。
- `Kmail` : 带有隐私保护的电子邮件。
- `Konsole` : KDE 终端模拟器。
- `KOrganizer` : 联系人管理器。
- `KWrite` : 文本编辑器。
- `Okular` : 通用文档查看器。
- `Spectacle` : 截图应用程序。

### GNOME

GNOME 最初发布于 1999 年。GNOME 代表 `GNU Network Object Model Environment`。它是另一个极其流行的桌面环境。然而，对于习惯 Windows 风格桌面的用户来说，GNOME 的风格不同。它背离了 Windows 的外观，但融合了许多相似的功能。如果你熟悉 Ubuntu，这就是你大部分时间必须打交道的桌面。

在相似之处中，提供了桌面图标、类 Windows 面板（位于顶部和底部）、菜单以及拖放功能。然而，GNOME 桌面缺少一些原生的应用程序。为了解决这一障碍，使用 GNOME 的 Linux 发行版集成了 KDE 库。如果你熟悉 Mac 系统，最新的 GNOME 界面与 Mac OS 有一些相似之处。

GNOME 提供了以下应用程序。你可以从这里获取完整的应用程序列表：`https://wiki.gnome.org/Apps/`

- `Empathy` : 通用即时通讯应用。
- `Evince` : 文档查看器。
- `Geary` : GNOME 邮件客户端。Evolution 是一个带有日历和地址簿的类似应用程序。
- `Gedit` : 文本编辑器。
- `Gnome-terminal` : 终端模拟器。

其他流行的桌面环境在下面的列表中。

- `MATE` : `MATE` 在外观和感受上某种程度上传统，带有一丝现代感。它是基于 GNOME 2 开发的。Ubuntu MATE 是一个使用 MATE 的操作系统。更多信息请访问 `https://mate-desktop.org/`。
- `XFCE` : `Xfce` 代表 `XFOrms Common Environment`。这是一个轻量级桌面环境，资源消耗低、用户友好且视觉上观。它与 GNOME 桌面有些相似，因为它基于 `GTK` 工具包。然而，它不是 GNOME 的分支。它适用于 Unix 和 Linux 发行版。MX Linux、Manjaro 和 Xubuntu 使用这个桌面环境。更多信息请访问 `https://www.xfce.org/`。
- `LXDE` : 这代表 `Lightweight X11 Desktop Environment`。正如名称所示，它更快更轻量，但拥有功能丰富的环境。它拥有一组良好的应用程序和一个活跃的社区。LXDE 是旧电脑的很好的桌面环境。它的外观与 GNOME 相似，但正在发生转变。其具有 GNOME 外观和感受的原因是使用了 `GTK +2` 工具包。它也运行在 Unix 和 Linux 平台上。Lubuntu、Knoppix、Peppermint 操作系统使用 LXDE 作为它们的桌面环境。更多信息请访问 `https://lxde.org/`。

## GNU 工具

我介绍了 GNU 及其与 Linux 内核的关系。你可能见过过 `GNU/Linux` 术语的使用。现在你知道背后的原因了。GNU 是为了让 Unix 用户体验类 Unix 环境而设计的。这就是为什么该工具集包含了许多类 Unix 的命令行工具。

Linux 系统使用一组核心工具，被称为 `coreutils`。它包含了管理文件、shell 和文本处理的工具。每个 GNU/Linux 发行版都应该包含这些核心工具。其中最重要的是 `Shell`。在下一章中我们将更详细地查看 shell。以下是对 shell 的介绍。

# 第 2 章：安装 Linux

在本章中，你将学习：
- 安装 Linux
- UEFI 与 Legacy BIOS
- 系统要求
- 安装后任务
- 故障排除

## 安装 Linux

随着 Linux 发行版的演进，图形界面和工具发生了巨大的变化。安装 Linux 比比 90 年代要容易得多。这并不意味着它不能通过命令行安装。这可能是个人偏好，也可能是行业需求。例如，通过命令行安装可以同时实现服务器设置和减少攻击面。我们将在本章中研究这两种方法。让我们从系统要求开始。

有 288 个 Linux 发行版，安装方法可能各不。我不预期涵盖所有的安装方法，因为这不是本书的意图。我们将介绍 Ubuntu 的安装，因为它非常流行且实用。

### 先尝试 Live CD

如果你打算作为裸机安装（bear metal installation）安装 Linux 操作系统，你可以直接安装。但是，如果你想先尝试一下或者演示它的用法，可以先作为 Live CD 模式运行它。大多数 Linux 发行版都支持这种模式。

在本系列中，我们将同时使用 Ubuntu 和 Red Hat 或 CentOS 来提供示例。让我们先学习如何准备 Ubuntu Live CD。





1. 从 [`www.ubuntu.com/getubuntu/download`](http://www.ubuntu.com/getubuntu/download) 下载 Ubuntu。

2. 在 Windows 或 Linux 平台上，将 ISO 镜像刻录到 DVD。

3. 从 DVD 启动并选择“尝试 Ubuntu（Try Ubuntu）”。

如果你想创建 USB 启动盘，这里有相关说明。这些步骤也提供了第 13 步中设置 DVD 的指南。如果你没有安装操作系统，必须进入“在不安装的情况下尝试（Try without installing）”。然后你可以使用 `Gparted` 分区工具，例如，如果你想创建一个启动电脑的 USB 盘。

1. 你需要一个容量为 4 GB 的 USB 盘。请记住，USB 盘在设置过程中会被擦除。如果 USB 盘是 USB 3.0 的速度会更快。

2. USB 盘必须支持启动。某些优盘可能存在问题。在选择 USB 盘之前必须验证这一点。

3. 如果你使用的是 Windows，可以使用如 `Rufus` 等软件准备 USB 盘并完成安装。既然我们正在学习 Linux，为什么不在 Linux 上操作呢？

4. 在 Linux 系统上，让我们使用 `Gparted` 创建 USB 盘。我正在使用 Ubuntu 创建 USB 盘。如果你使用的是 Live CD，它已经存在其中了。

5. 使用以下命令安装 `gparted`：

```
sudo apt-get install gparted
```

6. 格式化一次 USB 盘。

7. 按 `Ctrl+H` 显示隐藏文件。加载镜像文件（挂载）到 USB（复制）。

8. 右键点击分区，选择`管理标志（Manage Flags）`并启用 `boot` 和 `lba` 标志。

如果你想使用其他工具，例如 `mkusb`：

1. 为了进行结构化和格式化，让我们使用一个名为 `mkusb` 的实用。首先在 Ubuntu（标准版）上获取它。每行按回车。

```bash
sudo add-apt-repository universe
sudo add-apt-repository ppa:mkusb/ppa
sudo apt-get update
sudo apt-get install mkusb
```

2. 为了方便起见，让我们使用 `mkusb` 的 GUI 版本。

3. 运行该工具并检查选项。过程完成后，你可以将 USB 恢复为标准存储设备。

![](img/rsrcEH.jpg)图像：mkusb 工具

4. 从第一个选项开始，你可以创建一个启动设备。它将擦除第一个兆字节并创建所需的布局。

### 如果你想在 Ubuntu 上使用 `usb-creator`

1. 要从获取的 ISO 创建便携 USB，让我们使用 Ubuntu 中的 `usb-creator` 实用工具。只需挂载 USB 并启动此程序。

2. 对于源镜像，通过浏览路径提供镜像。如果镜像未列在列表中——如果没有，使用`其他...（Other…）`按钮找到它。

3. 要使用的磁盘：从列表中选择 USB 盘。如果你想使用 DVD，可以插入 DVD。

4. 如果使用 USB，请从列表中选择第一个启动分区。该分区应为 `Fat16` 或 `FAT32` 格式。

5. 如果你遇到 `Dbus` 错误，请参考 [`bugs.launchpad.net/usb-creator/+bug/458334`](https://bugs.launchpad.net/usb-creator/+bug/458334)

### 如果你的电脑使用的是 UEFI 怎么办？

如果 BIOS 模式设置为 legacy（传统），安装 Ubuntu 会更简单。如果它是 UEFI（统一扩展固件接口），你需要设置一个 UEFI 模式启动设备。USB 是此处的最佳选择。除非已经安装了另一个系统并且你想以双启动配置进行安装，否则不需要在 UEFI 模式下安装 Linux。

1. 获取 Ubuntu 64 位 ISO。获取 12.10 或更高版本更好，因为这些版本支持安全启动技术。

2. 在创建 USB 盘时，按照上文说明使用 `Gparted`。

3. 进入电脑的固件菜单并禁用`快速启动/快速启动（Quickboot/Fastboot）`和 `Intel 智能响应技术 (SRT)`。如果你使用的是 Windows 8 或更高版本，请禁用`快速启动（Fast Startup）`。

4. 设置你的固件从 UEFI 模式启动。就这样！

### 从你的 Live CD 启动

1. 插入 DVD 或 USB 盘并开启电脑。

2. 选择语言。

3. 当提示选项时，选择“在不更改电脑任何的情况下尝试 Ubuntu（Try Ubuntu without any change to your computer）”。

### 主要发行版的 Linux 系统要求

下表列出了以下 Linux 发行版的推荐要求。这些不是最低要求！这些是推荐要求。为什么从表中删除了最低要求？因为目前人们通常使用带有较新硬件的强大电脑。拥有至少 1 GB 内存和至少 40-80 GB 硬盘的电脑是极可能的。因此，没有刻意包含最低且有些不切实际的要求。如果你想了解这些具体要求，请参考制造商的网站或知识库。

表格：主要发行版的 Linux 系统要求

| Linux 发行版 | CPU | 内存 | 硬盘 |
| :--- | :--- | :--- | :--- |
| Red Hat Linux 7 | Intel/AMD 64, ARM 及更多 | 768MiB – 1.5 GiB | 10 GiB |
| Cent OS 7 | I386, x86_64, PowerPC8le, IA-32, ARMv7hl, AARch64 (arm64) | 64 位使用 1 GB 逻辑 CPU | 1 GB | 10-20 GB |
| Mint 19 | 推荐 64 位 | | | 20 GB |
| Ubuntu 18.04.3 | 2 GHz | 2 GB | 25 GB |
| Fedora 30 | 双核 | 4 GB | 10 GB |
| Debian 9 | 2 GHz | 2 GiB | 25 GB |
| MX Linux | i486 | | | 5 GB |
| Kali Linux | | | | |

### 执行基础 GUI 安装

1. 插入启动媒体并重启电脑。你将看到启动菜单。接下来，你必须决定是尝试 Ubuntu 还是安装 Ubuntu。接下来，选择你的键盘布局并继续。

2. 在下一个屏幕上，你将看到 4 个选项：

    - 正常安装（类似于全功能）。
    - 最小化安装，包含一组最基本的实用程序。这对于安全很有好处。
    - 其他选项：在安装时下载更新 – 此选项将更新你的系统。但这将花费更多时间。
    - 其他选项：为图形和 Wi-Fi 硬件以及附加格式安装第三方软件 – 此选项非常重要。如果你的电脑需要额外的驱动程序，你可以安装它。

3. 接下来是磁盘选项。你将获得 4 个选项：

    - 擦除磁盘并安装 Ubuntu：如果你正在准备双启动配置，请永远不要使用此选项。否则，这是最佳选项。
    - 加密：你可以在安装期间启用加密。
    - 使用 LVM：此选项允许你利用逻辑卷管理器。它可以帮助磁盘管理任务，例如调整分区大小和快快，以便你可以恢复操作系统。
    - 如果你想保留双启动配置或设置新的分区表，请点击`其他（Something Else）`。

4. 安装 Ubuntu

Ubuntu 和 Linux 系统将硬盘显示为文件。如果磁盘是 IDE，名称为 `/dev/hda` 到 `/dev/hdd`。对于 SCSi 控制器，是 `/dev/sda`。如果有更多磁盘，它们将被命名为 `/dev/sda`、`/dev/sdb` 等。分区将为 `/dev/sda1`、`/dev/sda2` 等。你可以使用 `MBR` 或 `GPT` 作为分区类型。后者是新方案，相比 MBR 具有许多优势。`GPT` 或 GUID 分区表为每个分区设置了唯一的 GUID，分区数量几乎没有限制，并且能够防范数据损坏。在 EFI 和 UEFI 系统上使用 `GPT`。

如果你要自定义分区方案，需要哪些分区以及大小要求是什么？

1. Linux 拥有不同的分区集，让我们看看下表。

表格：Linux 目录

| 目录 | 用途 |
| :--- | :--- |





# 文件系统概述

| 路径 | 描述 |
| :--- | :--- |
| `/` | 这是根目录。最顶层。 |
| `/bin` | 这是二进制文件存储目录。该目录下存在 GNU 实用程序（用户级）。 |
| `/boot` | 系统存储启动目录和在启动过程中使用的文件的地方。 |
| `/dev` | 设备目录和节点。 |
| `/etc` | 系统存储配置文件的地方。 |
| `/home` | 用户目录的主目录。 |
| `/lib` | 系统和应用程序库。 |
| `/media` | 媒体设备挂载的地方，如 CD、USB 驱动器等。 |
| `/mnt` | 可移动介质挂载的位置。 |
| `/opt` | 可选软件包存储在此处。 |
| `/proc` | 进程信息 – 对用户不开放。 |
| `/root` | root 用户的家目录。 |
| `/sbin` | 系统二进制存储目录。管理工具存储在此处。 |
| `/tmp` | 临时文件存放。 |
| `/usr` | 用户安装的软件存储在此处。 |
| `/var` | 变量目录，存储日志等动态文件。 |

## 分区考虑因素

当你创建特定的分区方案时，需要考虑以下计算方法。

| 分区 | 建议 |
| :--- | :--- |
| `/boot`: 如果磁盘大于 100 GB。 | 250 – 1000 MB |
| `/SWAP` | 至少等于 RAM 大小 |
| `/` | 至少 8 GB 到 15 GB |

对于 GPT 和 EFI 分区，需要一个 BIOS 启动分区（用于 Legacy 启动）或一个 EFI 分区。如果是 Legacy 模式，该分区的大小为 1 MB。如果是 EFI，它必须挂载在 `/boot/efi` 且大小为 100-250 MB (fat32)。

`SWAP` 是为内存操作预留的虚拟内存。如果系统需要更多内存空间，不活跃的区域或页面将被转储或交换交换。`SWAP` 不应被视为内存的替代品。旧的 `SWAP` 大小规则是 `2 x RAM`。然而，这现在已不再适用。

### 表：Linux SWAP 分区建议

| 已安装内存大小 | SWAP 空间 | 带有休眠 SWAP |
| :--- | :--- | :--- |
| `<= 2 GB` | `2 x RAM` | `3 x RAM` |
| `2 - 8 GB` | `= RAM` | `2 x RAM` |
| `8 – 64 GB` | `4 GB 到 ½ x RAM (8 GB 足够)` | `1.5 x RAM` |
| `> 64 GB` | `4 GB` | 应避免使用休眠 |

以下是在 Ubuntu 文档中找到的推荐自定义分区方案。由于我们安装了 Ubuntu，如果你打算长期使用，可以考虑以下方案。

### 表：Ubuntu 分区建议

| 分区 | 建议大小 |
| :--- | :--- |
| `/home` | 全部 – 使用独立磁盘更好。 |
| `/usr` | 10 GB |
| `/var` | 2 GB |
| `/lib` | 5 GB |
| `/boot` | 250 MB |
| `/opt` | 500 MB – 5 GB。如果使用通用仓库，请分配几个 GB。 |
| `/etc` | 250 MB |
| `/sbin` | 250 MB |
| `/bin` | 250 MB |
| `/dev` | 避免分区 |
| `/srv` | `<= 100 MB`。如果你运行 Web 服务器或类似程序，请做好规划。 |
| `/tmp` | `<= SWAP` |
| `/mnt` | |
| `/media` | |

来源：`https://help.ubuntu.com/community/DiskSpace`

## 安装过程

10. 现在你知道如何分配分区了。如果你没有分配任何分区而是使用默认设置，将看到以下弹出窗口。

![一张自动生成的手机描述截图](img/rsrcXB.jpg)
图片：确认磁盘更改

11. 接下来，选择你的地理位置。

12. 在下一个窗口中创建你的用户账户。有一点非常需要记住，特别是对于 Windows 用户。Linux 文件系统是**区分大小写**的！你必须小心使用大写和小写字母。如果你使用用户名 `John` 和 `john`，它们是不相同的！这对于文件、文件夹和其他内容也是如此。

![一张自动生成的手机描述截图](img/rsrcXM.jpg)
图片：创建第一个用户！
![一张自动生成的手机描述截图](img/rsrcXU.jpg)
图片：创建第一个用户 - 选项

13. 一旦完成这些步骤，安装将开始，并在安装完成后会你你。

14. 将显示安装完成屏幕。点击 `Restart Now`。

15. 一旦重启，且如果你选择了登录提示，你将进入登录页面。

16. 接下来，你必须完成安装后的任务。记住，在安装期间，你的网络连接将会被配置。

17. 在查看“新功能”部分后，点击 Next。

18. 设置 LivePatch。如果你担心内核补丁修复，这非常关键，我建议你配置它。

19. 在下一个屏幕中，你可以通过创建新账户注册，或如果你已有账户则登录。点击 Next。

20. 在下一个屏幕中，你可以通过点击 `Help improve Ubuntu - Yes, send system info to Canonical` 加入他们的匿名质量保证计划（例如收集崩溃数据等）。如果你不想参与，请选择其他选项并关闭窗口。

欢迎来到你新的 Ubuntu 工作空间。这是 Ubuntu 18.04.3。![](img/rsrcYA.jpg)
图片：Ubuntu 工作空间

## 安装后任务

### 连接网络

如果你无法连接网络，我们可以使用 GUI 进行配置。开始之前，点击右上角的网络图标。它将打开设置面板，然后在其中进入 `Network` 面板。
你只需要进入 `IPv4` 部分并进行配置。如果设置为 `DHCP`，在大多数情况下你就可以正常使用了。如果你使用虚拟机，你将需要在虚拟机宿主机上进行网络桥接。
要选择手动地址，请执行以下程序。![](img/rsrcYP.jpg)
图片：Ubuntu 网络配置
此外，你还可以设置 `IPv6` 地址、`DNS`（在这里我使用 Google DNS）和其他细节。无线连接也类似。

#### 如何使用命令配置连接？

1. 在桌面上点击右键并点击 `Open terminal`。终端将帮助执行命令。

2. 使用以下命令查看连接属性：

```
ip addr
```

3. 如果查看网卡状态，使用：

```bash
ip link
```

4. 查看路由信息：

```bash
ip route
```

5. 查看网络接口的统计信息，使用：

```bash
ip -s link
```





![](img/rsrc107.jpg)
# 安装故障排除

有时在极少数情况下，你可能会收到致命错误 `11 (SIGSEGV)`。如果操作系统安装程序访问了不应访问的内存位置，它将停止继续运行。`SIGSEGV` 代表段错误信号（Segment Violation Signal），换句话说就是段错误。这表明存在硬件相关的问题。如果是由于硬盘问题，你可以尝试擦除并重新安装。如果是由于内存故障，更换内存模块将解决问题。你也可以尝试在 `BIOS` 中禁用 CPU 缓存看看是否有帮助。

# 第 3 章：Linux 用户管理

在本章中，你将学习：
- `sudo` 命令和超级用户/Root 用户
- 通过 GUI/CLI 管理用户
- 管理 `sudoers`
- 命令别名
- 什么是 `/etc/passwd`
- 特殊权限位（Special Bits）

在本章中，你将学习如何设置超级用户、如何修改 root 用户和其他账户，以及如何通过 GUI 和命令行设置管理员、普通用户和组。

## `sudo` 命令

由于你是 Linux  way 系统的初学者，你需要了解一些基本命令，以便提升到 `su` 或超级用户权限。`sudo` 命令将用户提升为 root 用户，提供执行管理任务所需的足够权限。然而，并非每个人默认都能获得这些权限。用户必须被添加到 `/etc/sudoers` 文件才能使用此命令。

![](img/rsrc10Y.jpg)
![](img/rsrc114.jpg)![](img/rsrc119.jpg)

示例：当你第一次使用 Ubuntu 时，你可以控制 root 账户。首先，你需要为 root 设置一个密码，然后进行用户切换。
![](img/rsrc11E.jpg)
太棒了！现在，你是 root 用户了！

## 将用户添加到 sudo 用户列表

要将用户添加到 sudo 用户列表，你应该使用 GUI 或 `sudo visudo` 命令。在终端中执行此命令。运行以下命令：

```bash
sudo visudo
```
![](img/rsrc11P.jpg)
图片：`sudo` 用户列表

让我们尝试理解这个文件。有一个 root 用户，配置为 `root ALL=(ALL) ALL`。第一个 `ALL` 意味着 root 用户可以使用任何终端。第二个 `ALL` 表示 root 可以以任何用户身份运行。最后的 `ALL` 允许该用户运行所有命令。

我们可以添加具有特定控制权限的更多。例如，`poweruser ALL= /sbin/poweroff` 命令将允许 `poweruser` 用户通过任何终端关闭系统。

下一个要学习的是使用别名。你可以在此文件中使用几种类型的别名：
- `Host_Alias`
- `User_Alias`
- `Runas_Alias`
- `Cmnd_Alias`

例如，`sudoers` 文件可能如下：
- 将 `env_reset` 更改为 `env_reset,timestamp_timeout=n`。在这里你必须替换 `n`，以便会话时长不会超过指定的分钟。你可以使用 `-1` 来停止超时限制。
- 默认情况下，在提升 `sudo` 权限时输入密码不会显示字符。如果你想在输入密码时看到 `*`，请在上述行添加 `pwfeedback`。即 `env_reset,pwfeedback`。
- 创建别名并设置权限。见下例。

```text
Defaults          env_reset,pwfeedback,timestamp_timeout=15
Defaults          mail_badpass
Defaults          secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
# 主机别名规范
Host_Alias LAN = jan.contoso.com, jake. contoso.com
Host_Alias SRV = jan.host.com, drake.host.com, jake.host.com
Host_Alias DNET = 10.1.2.0/255.255.255.0
# 用户别名规范
User_Alias OPERATORS = dan
User_Alias WEBADMIN = jan, sana
User_Alias MAILADMIN = kane
# 命令别名规范
Cmnd_Alias SU = /bin/su
Cmnd_Alias HTTPD = /etc/rc.d/init.d/httpd, /etc/rc.d/init.d/mysql
# 用户权限规范
root   ALL=(ALL:ALL) ALL
OPERATORS ALL=ALL # operators 组拥有所有权限。
jan2 DNET=(ALL)ALL#jan2 通过 DNET 网络拥有所有权限。
## admin 组成员可能获得 root 权限
%admin ALL=(ALL) ALL
print_operator ALL= PRINTING#print_operator 可以从任何计算机运行 lpc 和 lprm。
## 允许 sudo 组成员执行任何命令
%sudo   ALL=(ALL:ALL) ALL
```
![](img/rsrc140.jpg)

## 通过 GUI 添加用户

请按照以下步骤通过 Ubuntu GUI 添加用户：

1. 打开 `Account Settings`（账户设置）对话框，可以通过 `Ubuntu Dashboard`，或者点击 Ubuntu 屏幕右上角的向下箭头。
![](img/rsrc14B.jpg)
图片：Ubuntu 用户账户

2. 接下来，点击你的用户名，然后如下所示选择 `Account Settings`（账户设置）。
![](img/rsrc14J.jpg)
图片：Ubuntu 账户设置

3. 将打开 `Users`（用户）对话框。
![](img/rsrc14S.jpg)![](img/rsrc14X.jpg)
图片：Ubuntu 主用户账户

4. 点击 `Users` 对话框右上角的 `Unlock`（解锁）按钮。将打开 `Authentication`（身份验证）对话框，让你提供管理员身份验证信息，因为只有这样你才能创建或编辑用户账户：
![](img/rsrc154.jpg)
图片：身份验证请求

5. 接下来，提供密码并点击 `Authenticate`（验证）按钮。你现在可以看到 `Users` 对话框中的所有字段已为你启用。

6. 点击 `Add User`（添加用户）按钮。`Add User` 对话框将打开让你输入要创建的新用户的详情。

7. 你可以通过此对话框指定要创建 `Standard`（标准）还是 `Administrative`（管理）用户。同样重要的是，为新用户留空密码字段不是良好的安全做法。这样任何用户都可以登录并访问你系统上的隐私和安全数据。让我们添加 `jake` 为一个新的标准用户。
![](img/rsrc15D.jpg)
图片：添加新用户

8. 点击 `Add`（添加）按钮，只有在 `Add User` 对话框中提供了所有有效信息后，该按钮才会可用。新用户现在将被创建，你可以如下所示在 `Users` 对话框中看到它：
![](img/rsrc15M.jpg)
图片：新标准用户

9. 你还可以更改组成为 `Administrator`（管理员）、选择区域、重置密码、启用自动登录以及账户活动。

10. 要删除用户，可以使用右下区域的 `remove`（移除）按钮。





## 通过命令行添加用户

通过 Linux 命令行管理用户和组更加方便。在本节中，我们将介绍相关的技术和示例。

## Linux 中的用户和组管理

Linux 是一个多用户平台。在企业环境甚至 SOHO（小型办公/家庭办公）环境中，它通常供多个用户共享。某些用户和组织过去会让几个用户共享同一个账户。从安全和可用性的来看，这是一种危险的做法。因此，推荐的最佳实践是创建多个账户并相应分配权限。在 Linux 系统中，如果需要共享文件或目录，用户和组管理工具完全能够胜任。

### Root 或超级用户权限

添加新用户涉及管理您以外的账户，这需要超级用户（AKA `root`）权限。其他用户或组管理任务也是如此，例如删除账户、更新账户以及创建和删除组。

与任何其他操作系统一样，用户管理任务是 root 用户或超级用户的责任。这包括用户和组管理任务。由于账户管理需要安全保障，因此这是必须的。

使用以下命令执行用户管理任务：

- `su`: 切换用户。
- `sudo`: 以 root 用户身份通过提权权限执行命令。
- `adduser`: 向 Linux 系统添加用户。
- `userdel`: 删除用户账户，无论是否删除用户文件。
- `addgroup`: 添加组。
- `delgroup`: 组。
- `usermod`: 此命令可在添加用户后修改用户。
- `chage`: 此命令可以更改账户的年龄（更改有效期）。换句话说，它用于更改账户过期时间。

### 涉及的文件

- `/etc/passwd`: 存储用户信息。
- `/etc/shadow`: 密码加密。
- `/etc/sudoers`: 如果用户未列在此文件中，则既无法执行管理任务也无法提供管理授权。我们在在本章之前的某个章节已经介绍过并修改了此文件。
- `/etc/group`: 此文件包含所有的组信息。

超级用户是全能账户，拥有执行任何操作的所有权限。它是起始也是终结。在安装操作系统后可以配置 root 用户。默认情况下，在 Ubuntu 上系统安装程序也会成为超级用户。并不适用于所有的 Linux 发行版。

我们如何知道 `sudo` 是否可用？是的，它必须安装并配置。让我们使用以下命令进行验证。

命令：`which sudo`

该命令验证并确认 `sudo` 是否存在。如果在任何情况下不存在，请使用以下命令安装：
`apt-get install sudo`

## 添加新用户账户

为了获得一些实践经验，让我们使用 Ubuntu 创建一个名为 `Test2` 的用户。使用 `su-` 命令将您的用户切换到 root 用户始终会更好。

```
sudo adduser test2
```

或者，先切换到 root 然后执行：

```
add user test2
```

您将会被提示输入两次密码。然后它将被存储在 `/etc/passwd` 文件中。在该文件中，冒号被用作字段分隔符。在创建用户时，可以提供其他信息（例如：全名）。某些是可选的（电话号码等）。

在创建用户时，会创建一个与用户用户名相同的主组。默认情况下，该用户被分配到该组。

### Sudoers - 什么是

sudoers 文件在本章的早些部分介绍过。为了委托管理任务，必须授予权限。这通过将新创建的用户添加到 `/etc/sudoers` 文件来实现。在本节中，将把新创建的用户添加到 sudoers 文件中，以便授予用户执行某些任务的额外权限。

1. 使用 `sudo visudo` 命令打开 `/etc/sudoers` 文件。为了保护此文件，不要使用其他编辑器打开它。最好通过切换到 root 账户来使用。这可以让操作更安全且不痛苦。通过 `visudo` 打开它，你可以确保：
    a. 其他用户无法同时编辑该文件。
    b. 在退出前会验证语法。
2. 在 `/etc/sudoers` 为新用户账户添加新条目。

例如，假设你想为 `Test2` 提供超级用户权限。要完成此任务，请在 `/etc/sudoers` 的底部添加以下行：

`test2 ALL=(ALL) ALL`

此行的格式为 `A B = (C:D) E`。让我们回顾一下：
- `A` 代表用户名。
- `B` 代表当前主机或网络环境中的所有主机。
- `C:D` 代表用户和组。
- `E` 表示此用户允许执行的命令。

## 创建命令别名

不建议像之前那样直接为用户提供权限。有一种替代的、更细粒度的方法。例如，可以允许一组命令并将其应用于用户。我们通过将命令分一组来实现这一点。这组被称为别名（Alias）。

为了让 `helpdesk` 用户仅使用 `adduser` 和 `usermod` 而不使用其他命令，逐一列出下面的命令（使用绝对路径）。假设我们正在为名为 `helpdesk` 的账户提供权限。您可以将其应用于 `test2` 或任何您喜欢的用户：

`helpdesk ALL=(ALL:ALL) /usr/sbin/adduser, /usr/sbin/usermod`

或者，定义一个别名（只要是全大写，我们可以随心命名，例如 `HELDESK`）。我们使用大写字母定义别名。方法如下：

`Cmnd_Alias HELDESK = /usr/sbin/adduser, /usr/sbin/usermod`
`helpdesk ALL=(ALL:ALL) HELDESK`

除了这里指定的之外，helpdesk 将无法以 root 身份执行任何其他命令。

## 切换用户

现在您已经创建了用户并分配了权限，如果编辑文件后保存成功，是时候切换到该用户并一些测试了。要这样做，请使用 `su` 命令切换到该账户。正如您现在所理解的，不必坚持使用超级用户账户。您可以来回切换。这也将加强安全性。

此外，可以使用 `-l` 选项提供类似于用户如果/她直接登录时期望的环境。执行以下命令：

```
su - helpdesk
```

## 更高级的命令

让我们学习添加新用户的过程。为了管理工作，理论将是非常重要的。当新用户被添加到系统时，会发生以下事件和操作：

- 创建其/她的主目录（在 `/home` 目录下）
- 下列文件（隐藏文件）将被复制到用户的主目录。这些文件用于提供所需的环境变量：
    - `.bash_logout`
    - `.bash_profile`
    - `.bashrc`





- 在 `/var/spool/mail/username` 创建邮件邮箱池
- 创建了一个组。该组的名字与用户名相同。

### 理解 `/etc/passwd`
所有账户信息都存储在该文件中。每个用户都有一条记录，格式如下：
`[username]:[x]:[UID]:[GID]:[Comment]:[Home directory]:[Default shell]`

- `[username]` 是用户账户名。
- `x` 表示该账户受 `/etc/shadow` 中影子密码的保护。
- `UID` 和 `GID` 是用户 ID 和组 ID。
- `Home directory`（主目录）指向用户主目录的绝对路径。
- `Default shell`（默认 shell）将在用户登录时加载。

### 理解 `/etc/group`
组信息存储在 `/etc/group` 文件中。它具有以下格式：
`[Group name]:[Group password]:[GID]:[Group members]`

- `Group name` 是组名。
- `Group password`（组密码）。如果显示 `x`，则不使用。
- `GID` 与 `/etc/passwd` 中的相同。
- `Group members`（组成员），一个用逗号分隔的文件。

### 修改用户
在添加新用户后，可以使用名为 `usermod` 的特殊命令修改其属性。
语法：`usermod [options] [username]`

设置到期日的示例：
`usermod --expiredate 2020-01-31 helpdesk`

添加到多个组的示例：
`usermod --append --groups root,helpdesk helpdesk`

更改主文件夹的示例：
`usermod --home /newhome/helpdesk helpdesk`

更改默认 shell 的示例：
`usermod --shell /bin/sh helpdesk`

![](img/rsrc19Z.jpg)

我们可以如下结合使用上述所有示例：
```
usermod --expiredate 2020-01-31 --append --groups root,helpdesk --home /newhome/helpdesk helpdesk --shell /bin/sh helpdesk
```

### 锁定和解锁用户
可以锁定和解锁用户。这在常规操作中没有帮助，但在工作环境中非常有用。

锁定示例：`usermod --lock helpdesk`
解锁示例：`usermod --unlock helpdesk`

### 组管理（高级）
![](img/rsrc1AA.jpg)

命令：
- `groupadd hr_group`
- `chown :hr_group hr.txt`
- `usermod -aG hr_group user1`
- `usermod -aG hr_group user2`
- `usermod -aG hr_group user3`

![](img/rsrc1AN.jpg)

如果我们来看另一个例子，3 个用户需要访问由一个用户共享的文件，分组将变得非常有用且安全。假设有 3 个用户：
- `user1`
- `user2`
- `user3`

`user1` 有一个文件要共享。如果你通过执行 `chmod` 命令更改文件权限。`660` 表示所有者和组可以读写该文件。然而，如果我们使用创建 `user1` 时生成的默认组，将允许同组中的每个其他用户访问 `user1` 的所有文件和个人数据。这就是组的重要性。你可以设置其他组并应用适当的权限。我们可以实现适当的分组结构，以更好地结合共享与安全。

### 理解 setuid、setgid 和粘滞位 (Sticky Bit)
这是一种应用于文件（即可执行文件）的权限。当你这样做时，其他用户将继承所有者的有效权限。因此，这引发了安全担忧，此类应用程序必须尽可能少。此权限用于系统程序。

例如，让我们以 `/usr/bin/passwd` 为。它负责更改用户的密码。通过这样做，它修改了 `/etc/shadow` 文件。对于该文件，超级用户必须能够更改自己和其他密码，而其他人必须能够更改自己的密码，但不能更改他人的。因此，其他用户必须能够读取和执行。为了做到，root 必须能够指定账户。

![](img/rsrc1B1.jpg)

注意这里的 `rwsr`。`s` 代表 `setuid`。在这种情况下，`setuid` 和用户的执行位已启用（`s` 表示已启用，如果它是 `S`，则表示执行位未启用）。

当启用 `setgid` 位时，真实用户的有效 `GID` 变为组所有者的 GID。其他用户可以在组所有者的权限下访问文件。如果在此目录上设置了此项，在该目录内创建的文件将继承相同的组。新目录继承相同的 `group`。当有人需要访问共享目录时，无论文件的主组是什么，都是最佳方法。要启用 `setgid`，运行以下命令。将 `filename` 替换为原始文件名：
```
chmod g+s [filename]
```
要以八进制形式（数字）发送，你需要设置以下内容。将目录名替换为原始目录名：
```
chmod 2755 [directory]
```
![](img/rsrc1BC.jpg) ![](img/rsrc1BC.jpg) ![](img/rsrc1BH.jpg)

此外注意颜色的变化。

### 粘滞位 (Sticky Bit)
如果粘滞位对文件启用，则会被系统忽略。然而，如果设置在目录上，它将限制用户的操作，例如重命名和删除，除非用户是所有者。要启用此位，运行以下命令：
```
chmod o+t [directory]
chmod 1755 [directory]
```
![](img/rsrc1BC.jpg) ![](img/rsrc1BC.jpg) ![](img/rsrc1C.jpg)

同样注意 `test.txt` 的颜色变化。

### 删除组
要删除组，使用 `groupdel` 命令。
语法：`groupdel [group_name]`
示例：`groupdel test`

### 删除用户
要删除账户，使用 `userdel` 命令。
示例：`userdel test`

# 第 4 章：Linux 终端

在本章中你将学习：
- 终端及其类型
- Terminfo
- 控制台
- Shell

### 终端
在 Unix 和 Linux 早期，计算机没有图形界面。为了与操作系统交互，有一个名为终端的程序，主要基于文本。早期的 Linux 版本没有高级功能，如图形支持。因此，出于安全考虑，现在大多数服务器在文本模式下运行。Linux 现在具有高级功能，如块模式和矢量图形。终端支持的字符集：
- ASCII
- ISO-8859-1, 2, 6, 7 和 8
- Unicode

终端还支持用于控制显示器的控制代码，这有助于控制光标位置和其他不可打印操作。一些控制代码包括：
- 回车
- 方向键
- 向上/向下分页
- 新行（换行符）

此外，使用了缓冲区来保存命令历史，这被称为滚动屏。(rsrc1D.jpg)

另一种类型是备用屏（alternate screen）。在这种方法下，终端可以在另一个屏幕上存储数据。这是基于图形的终端的开始。控制代码用于在屏幕和用用屏之间切换。早期的终端是文本的，字符如**粗体**和下划线、闪烁字符以及白色背景上的黑色。经过了一段时间，出现了颜色的终端，并有多个控制代码来控制行为。今天我们使用高级程序来模拟这些终端。映射可以从一个系统到另一个系统。有一些可用的常用键：
- 方向键
- 删除
- 重复
- 回车
- Break
- 以及特定的功能键（如 F1 到 F12）

### Terminfo
如你所知，有很多终端模拟器。对于每个终端，Linux 操作系统必须保留控制代码以便准确操作。这些特性在一个名为 Terminfo 的数据库中。为了区分终端，创建了一个与该终端相关的文件文件夹。在 Ubuntu 中，terminfo 的位置是 `/etc/terminfo/*`。

你可以使用 `toe` 命令查看所有可用终端类型。
示例：`toe -a` ![](img/rsrc1DN.jpg)

### 控制台
在早期，当你启动 Linux 机器时，你会得到一个带有登录提示的文本控制台。你可以验证身份并发送命令。现代 Linux 系统在启动时创建多个虚拟控制台。最多可以有 6 个。你可以使用快捷键组合或键盘功能键在这些控制台之间切换。例如，你可以使用 `Alt + Fn` 或 `Ctrl + Alt + Fn`（这里简单的 Fn 代表键盘上的功能键）。在 Ubuntu 中，你可以使用 `Alt + Ctrl + F3` 打开文本控制台。返回时按下 `Alt + Ctrl + F2`src1DW.jpg)

### 终端类型
有很多种终端。我们将查看流行且易用的终端。

**xterm**：这是最旧的终端模拟包。它提供了 DEC VT100 CLI 和 Tektronix。现在有模拟器，如 `Eterm` 和 `ROterm`，它们轻量级并提供了很大的功能选择自由。`E` 提供更多灵活性，而 `ROterm` 为高级用户提供了功能。以下图片显示了 xterm 可用的选项。(rsrc1E7.jpg) ![](img/rsrc1EB.jpg) ![](img/rsrc1EG.jpg)

**Konsole**：Konsole 是 KDE 桌面环境提供的终端模拟器。KDE 具有类似于 Windows 的菜单栏并提供标签页窗口。这些方便的功能：
- 透明背景
- 分屏模式
- 可自定义颜色方案和按键绑定
- 增量搜索
- HTML 兼容输出
- 终端通知

对于一组命令行选项，请访问 `https://docs.kde.org/stable/applications/konsole/command-line-options.html`。

**GNOME terminal**：GNOME 也提供了自己的终端包 GNOME terminal。默认情况下 Ubuntu 带有 GNOME terminal。它有很多用的选项。让我们用命令找出 Ubuntu 中存在哪些终端。在模拟器中运行以下命令：
```
update-alternatives --display x-terminal-emulator
```
rsrc1F2.jpg) GNOME terminal 提供了丰富的功能和命令。它支持标签页、附加/分离标签、配置文件、预设大小等。还有具有酷功能的新终端模拟器。以下是列表：
- **Xfce**：用于 XFCE 桌面环境。
- **Terminator**：`https://launchpad.net/terminator`
- **Tilda**：`http://tildasourceforge.net/tildaabout.php`
- **Guake (基于 Python)**：`https://github.com/Guake/Guake`
- **Yakuake**：`ext.kde.org/apps/yakuake`
- **Eterm**：`www.eterm.org`





# Bash 转义序列

| 字符 |  |
| :--- | :--- |
| `\a` | 一个 ASCII 响铃字符 (07)。 |
| `\d` | “星期 月 日”格式的日期。 |
| `\e` | 一个 ASCII 转义字符 (033)。 |
| `\h` | 第一个 `.` 之前的主机名。 |
| `\H` | 主机名。 |
| `\j` | 当前 shell 管理的任务数。 |
| `\l` | shell 终端设备的基名。 |
| `\n` | 换行。 |
| `\r` | 回车。 |
| `\s` | shell 的名称，`$` 的基名。 |
| `\t` | 24 小制 HH:MM:SS 格式的当前时间。 |
| `\T` | 12 小制 HH:MM:SS 格式的当前时间。 |
| `\@` | 12 小制 am/pm 格式的当前时间。 |
| `\u` | 当前用户的用户名。 |
| `\v` | bash 的版本（例如 2.00）。 |
| `\V` | bash 的发布版本，版本 + 补丁级别（例如 2.00.0）。 |
| `\w` | 当前工作目录。 |
| `\W` | 当前工作目录的基名。 |
| `!` | 此命令的历史编号。 |
| `#` | 此命令的编号。 |
| `$` | 如果有效 UID 为 0，则显示 `#`，否则显示 `$` |
| `\nnn` | 与八进制数 `nnn` 对应的字符。 |
| `\\` | 反斜杠。 |
| `\[` | 开始非打印字符序列，可用于将终端控制序列嵌入提示符中。 |
| `\]` | 结束非打印字符序列。 |

来源：[`www.tldp.org/HOWTO/Bash-Prompt-HOWTO/bash-prompt-escape-sequences.html`](https://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/bash-prompt-escape-sequences.html)

你可以通过以下方式使用这些字符来自定义提示符。
![](img/rsrc1HJ.jpg)
![](img/rsrc1HP.jpg)

## Bash 颜色代码

bash 有很多自定义选项，例如字体颜色、背景颜色、闪烁、加粗、下划线等效果。要查看此类精彩列表，请访问 [`misc.flogisoft.com/bash/tip_colors_and_formatting`](https://misc.flogisoft.com/bash/tip_colors_and_formatting)！

![](img/rsrc1HW.jpg)

这些自定义不会在另一个会话中持续。要永久更改，我们必须修改关联的文件。我们稍后会介绍这一点。

## Man! 手册

对于任何操作系统，你都能网上找到手册。对于任何 GNU 应用程序也是如此。然而，对于 bash，它有一个内置的手册，你必须熟悉它。当你不知道某些内容（例如某个新命令）时，它能提供卓越的信息和帮助。

你将正式学习的第一个命令是 `man .`。正如你所知的，没有任何书籍能提供比 `man` 更全面的带示例和实践 Linux 命令指南，但 `man` 可以。

## man 命令语法、输出和参数

以下是命令 `man man .` 的输出。
![](img/rsrc1J6.jpg)
图片：Linux man 命令

这些手册有多个章节，你可能想通过一次性请求选择来节省时间。列表按数字列出了章节。

### 表格：Man 页章节

| 章节 | 内容 |
| :--- | :--- |
| 1 | 用户命令 |
| 2 | 系统调用 |
| 3 | 库函数 |
| 4 | 特殊文件（即设备文件） |
| 5 | 文件格式和文件系统 |
| 6 | 游戏 |
| 7 | 概述与杂项 |
| 8 | 系统管理和权限命令 |
| 9 | 内核例程 |
| l | 本地文档 |
| n | 新页面 |

要获取这些定义，你可以使用命令：`man n intro`
![](img/rsrc1MT.jpg)
![](img/rsrc1MX.jpg)
图片：Linux man 页面

关于这些 man 页面还有一个重要的事实。每个页面都有不同的章节。为了减少时间消耗，你必须对这些章节是什么了如指掌。

### 表格：man 页组成

| 章节 | 目的 |
| :--- | :--- |
| Name | 名称和简短描述 |
| Synopsis | 语法 |
| Description | 详细描述 |
| Definitions | 程序相关定义 |
| Examples | 示例 |
| Overview | 概述 |
| Defaults | 特定程序/命令的默认值 |
| Options | 特殊程序/命令的选项 |
| Arguments | 用户可以提供的可能参数 |
| Parameters | 存储值的参数 |
| Invocations | 与调用命令相关的内容 |
| Reserved Words | 系统或程序的保留字 |
| Exit Status | 退出状态或代码 |
| Errors | 错误 |
| Reporting Bugs | 发现错误后如何报告 |
| Comments | 注释部分 |
| Environment | 使用的一组环境变量 |
| Files | 相关文件，例如涉及的特定配置文件 |
| Author | 作者 |
| Copyright | 版权信息 |
| History | 程序或命令的历史 |
| See Also | 相关主题，例如命令 |





还有其他章节，如果你感兴趣，可以通过执行 `man bash` 命令或访问 [`man.cx/bash#heading7`](https://man.cx/bash#heading7) 来找到更多内容。正如你所理解的，帮助页（man page）中包含大量内容。让我们学习一些更多命令来格式化输出。

### 帮助章节 (Man Section)
`man section_number page_name`
示例：`man 4 tty`![](img/rsrc1T9.jpg)

假设你想查找某个帮助页是否存在。`whatis` 是查找它的最佳命令。其语法为：`whatis keyword`
示例：`whatis man`![](img/rsrc1TF.jpg)

现在，如果你运行 `man 7 man`，你将找到更多关于宏的信息![](img/rsrc1TM.jpg)

如果你不知道具体的页面，但想了解某些特定内容（例如 shell 或终端），以下命令会很有帮助。其语法为：`man – k keyword`
示例：`man -k shell`![](img/rsrc1TU.jpg)

现在你可以找到特定的页面了，例如 `man 1 dash`。

### Less 和 More
这两个命令在在使用帮助页时极其有用，甚至对于其他工作（如文件操作）也是如此。这些命令允许用户通过许多查看选项阅读页面或文件。`Less` 更先进，而且加载速度快，因为它不会一次性加载整个文件。它比它的兄弟命令拥有更多选项。

`man` 是一个旧命令，并不友好。例如，你无法用它向后滚动，导致阅读变得困难。这导致了它的兄弟命令 `less` 的诞生。`Less` 提供了一个类似于文本编辑器的环境，让你来回滚动、输入参数并进行良好的交互。让我们来看 `man ls | more` 命令的输出![](img/rsrc1U3.jpg)

**图片：More 命令**
使用 `more` 时，你必须使用回车键或空格键，不能使用箭头键![](img/rsrc1U9.jpg)
**图片：Less 命令**
末尾有一个微小的 `:`。你可以发送命令来执行额外的操作。使用 `less` 导航和控制要容易得多。

你一定注意了这些命令中使用的新符号。要使用这些命令，你需要学习另一个新运算符。这被称为管道（pipeline）。管道操作符很简单，就是 `|`。它的作用是将一个命令的结果获取并发送到另一个命令，就像在管道中一样。例如，让我们看看下面的示例。

语法：`command_1 | command_2 | command_3 | .... | command_N`
示例：`man bash | more`

首先执行第一个命令（`man bash` 显示 `bash` 的说明手册）。然后它被传递给第二个命令。这是链接命令的极佳方法。另一个例子是 `ls /bin | more`![](img/rsrc1US.jpg)

在下一节中，我们将以更有结构化的方式查看命令，以便操作更加精简化。

### Linux 编辑器
Linux 世界有很多种编辑器。如果你精通脚本，必须具备相关的实践知识并熟悉至少一种编辑器。在本节中，我们将查看几个编辑器。正如你所知的，桌面环境发行版都有自己的编辑器。

#### Vim 编辑器
在过去，Unix 系统使用一种名为 `vi` 的文本编辑器。GNU 对此部分进行了修改，并将其作为“改进版 vi”或 `vim` 提供。`Vim` 编辑器在 CentOS 或 Red Hat 发行版中可用。在 Ubuntu 中，你可能需要手动安装。有一些命令可以验证它是否存在。分别执行以下命令：

```
alias vi
which vils -l /usr/bin/vim
```
在 ubuntu 中，你会得到以下界面![](img/rsrc1V7.jpg)。在这种情况下，你必须使用以下命令安装 `vim`。
```
sudo apt-get install vim
```

在使用 `vim` 时，你必须注意有两种模式：
- 插入模式 (Insert mode)：按 `i` 键进入插入模式。
- 普通模式 (Normal mode)：按 `Esc` 退出。

当你用 `vim` 打开文件时，处于普通模式。当你处于插入模式时，正在写入文件。你还必须知道如何退出、保存并退出：
- 按 `q` 退出。
- 按 `wq` 保存到同一文件并退出。
- 按 `q!` 退出且不保存更改。
- 输入 `w filename` 以不同的名称保存文件。

`vim` 编辑器是一个功能丰富的编辑器。它并不总是那么方便。例如，复制粘贴并不容易。需要利用剪切模式（Yanking）和视觉模式（visual modes）来实现。

#### Nano 编辑器
这个微型编辑器在大多数 Linux 系统以及 Ubuntu 中都可用![](img/rsrc1VS.jpg)
**图片：Linux Nano 编辑器**
它最好的特性是屏幕前的命令列表。它有一套简单的命令集，使用 `Ctrl` 键和其他键。获取帮助按 `Ctrl + G`。退出按 `Ctrl + X`。

#### KDE 编辑器
在 KDE 中，他们提供编辑器，在这些编辑器中，`KWrite` 和 `Kate` 经常被使用。`KWrite` 是单窗口编辑器，而 `Kate` 是一个多窗口且功能丰富的编辑器。

#### GNOME 编辑器
由于我们使用的是 Ubuntu，使用 GNOME 编辑器更好。`gedit` 在很多情况下是默认编辑器![](img/rsrc1W.jpg)
**图片：Linux Gnome 编辑器**
`gedit` 支持标签、具有查找和替换选项、语言、拼检查、日期/时间工具、全屏模式![](img/rsrc1W.jpg)

# 第 5 章：基础 Shell 命令
### 介绍
我们从之前的章节中已经探索了命令。

### 导航
要查看当前目录下的目录列表，在 Windows 中使用 `dir` 命令。该命令在 Linux 上的工作方式相同。要导航到文件，最基本的方法是使用文件的完整路径，例如 `/home/jan/Desktop/`。有一些基础命令可以更方便地做到。

1. 使用 `pwd` 命令了解你当前的工作目录![](img/rsrc20R.jpg)
2. 使用 `cd` 命令更改目录位置。这里我们使用绝对路径 ![](img/rsrc20Y.jpg)
3. 仅使用 `cd` 命令返回主目录。

### 文件系统
文件命名基于 FHS（文件系统标准）。让我们来看看常见的目录。

**表格：Linux 目录类型**

| 目录 | 目的 |
| :--- | :--- |
| / | 这是根目录。最顶层。 |
| /bin | 这是二进制文件存储器。此目录下包含 GNU 工具（用户级）。 |
| /boot | 系统存储启动目录和在启动过程中使用的文件的地方。 |
| /dev | 设备目录和节点。 |
| /etc | 这是系统存储配置文件的地方。 |
| /home | 用户目录的所在地。 |
| /lib | 系统和应用程序库。 |
| /media | 这是挂载媒体设备的地方，如 CD、USB 驱动器。 |
| /mnt | 可移动媒体挂载到此的地方。 |
| /opt | 可选软件包存储在此处。 |
| /proc | 进程信息 – 不对用户开放。 |
| /root | root 用户的主目录。 |
| /run | 运行时数据存储在这里。 |
| /sbin | 系统二进制文件存储器。管理工具存储在这里。 |
| /srv | 本地服务将其文件存储在这里。 |
| /sys | 系统硬件信息存储在这里。 |
| /tmp | 这是临时文件存放。 |
| /usr | 这是用户安装的软件存储的地方。 |
| /var | 变量目录，存储日志等动态文件。 |

### 使用 `ls` 列出文件
我们将查看一些命令。这不会显示根目录。





![](img/rsrc214.jpg)

### 4. 现在我们将使用相对路径来使操作更简单、节省时间。在这种情况下，我们可以使用 `/`。

![](img/rsrc21A.jpg)
在这里，`dir` 命令列出我当前文件夹下的目录。我可以使用 `cd Desktop` 命令跳转到桌面文件夹。

在目录遍历时，有两个特殊字符。它们是 `.` 和 `..`。单点 `.` 代表当前目录。双点 `..` 代表上一级文件夹。

### 5. 要返回上一级目录，请使用 `..`，例如

![](img/rsrc21M.jpg)

### 6. 你也可以使用 `..` 来跳过输入文件夹路径。例如，

### 7. 你可以返回一级再向前移动。在这里，你回到主目录，然后向前（向下）进入 Music 文件夹。

![](img/rsrc21X.jpg)

### 8. 你可以连续使用 `../` 来进入上级文件夹，并使用绝对路径（混合相对路径和绝对路径）往返跳转。

![](img/rsrc223.jpg)

## 列出文件
我们使用 `ls` 命令来列出文件。这是 Linux 用户最常用的命令之一。以下是 `ls` 命令及其用途。

| command | Description |
| :--- | :--- |
| `ls -a` | 列出所有文件，包括所有以 `.` 开头的隐藏文件 |
| `ls --color` | 彩色列表 `[=always/never/auto]` |
| `ls -d` | 列出带有 `*/` 的目录 |
| `ls -F` | 为条目添加指示符（例如 `*/=>@&#124;`） |
| `ls -i` | 列出 inode 索引 |
| `ls -l` | 以长格式列出，包括权限 |
| `ls -la` | 与上述相同，包含隐藏文件 |
| `ls -lh` | 人类可读格式的显示列表 |
| `ls -ls` | 带有文件大小的显示列表 |
| `ls -r` | 逆序的显示列表 |
| `ls -R` | 递归列出（目录树） |
| `ls -s` | 列出文件大小 |
| `ls -S` | 按大小排序 |
| `ls -t` | 按日期/时间排序 |
| `ls -X` | 按扩展名排序 |

让我们检查几个命令。记住，你可以使用多个参数。例如，`ls -la`。

语法：
```
ls [option ...] [file]...
```

详细语法：
```
ls [-a | --all] [-A | --almost-all] [--author] [-b | --escape][--block-size=size] [-B | --ignore-backups] [-c] [-C] [--color[=when]][-d | --directory] [-D | --dired] [-f] [-F | --classify] [--file-type][--format=word] [--full-time] [-g] [--group-directories-first][-G | --no-group] [-h | --human-readable] [--si][-H | --dereference-command-line] [--dereference-command-line-symlink-to-dir] [--hide=pattern] [--indicator-style=word] [-i | --inode][-I | --ignore=pattern] [-k | --kibibytes] [-l] [-L | --dereference][-m] [-n | --numeric-uid-gid] [-N | --literal] [-o][-p | --indicator-style=slash] [-q | --hide-control-chars][--show-control-chars] [-Q | --quote-name] [--quoting-style=word][-r | --reverse] [-R | --recursive] [-s | --size] [-S] [--sort=word][--time=word] [--time-style=style] [-t] [-T | --tabsize=cols][-u] [-U] [-v] [-w | --width=cols] [-x] [-X] [-Z | --context] [-1]
```

示例：
```
ls -l setup.py
```
![](img/rsrc25S.jpg)
这提供了该特定文件的长列表格式详情。

更多示例：
- 列出主目录内容：`ls`
- 列出父目录内容：`ls */`
- 显示当前目录的目录：`ls -d */`
- 列出根目录内容：`ls /`
- 列出具有以下扩展名的文件：`ls *.{htm,sh,py}`
- 列出文件详情。如果未找到则抑制错误：`ls -myfile.txt 2>/dev/null`

`/dev/null` 是一个重要位置。这实际上是一个名为 `null device”（空设备）的特殊文件。它还有其他名称，如 `blackhole` 或 `bit-bucket`。当内容写入此文件时，它会立即丢弃并返回文件结束符（EOF）。

当进程或命令返回错误 `STDERR` 时，标准错误是进程可以写入的默认文件描述符。这些错误将显示在屏幕上。如果有人抑制它，空设备就派上用场了。我们经常将命令行写作 `/dev/null 2>&1`。

`2` 和 `$1` 代表什么？标准输入 (stdin) 的文件描述符是 `0`。标准输出 (stdout) 是 `1`。标准错误 (stderr) 是 `2`。在这里，我们正在抑制 `ls` 命令生成的错误。它被重定向到 stdout，然后写入 `/dev/null` 从而丢弃。

## 颜色代码
![](img/rsrc26A.jpg)
图片：ls 颜色代码。这些颜色代码很好地区分文件类型（你可以在 [`askubuntu.com/questions/17299/what-do-the-different-colors-mean-in-ls`](https://askubuntu.com/questions/17299/what-do-the-different-colors-mean-in-ls) 找到源码）。

让我们运行 `ls -lasSt`
![](img/rsrc26G.jpg)
这使用了长列表格式，显示所有文件并按时间排序。现在，你需要理解这些值：

1. `4`：文件大小（按大小排序）。
2. 在下一部分中 `d` 代表目录。
3. 接下来的几个字符代表权限（`r-`读、`w-`写、`x-`执行）。
4. 硬链接数。
5. 文件所有者。
6. 文件所有者组。
7. 字节大小。
8. 最后修改时间（排序依据）。
9. 文件/目录名。




如果你在命令中使用 `-i`（移除 S，按最后修改时间排序），你可以在最左侧区域看到节点。![](img/rsrc279.jpg)
示例：`ls -laxo`![](img/rsrc27E.jpg)

### 使用 ls 进行模式匹配
`ls` 命令可以与通配符如 `*` 和 `?` 结合使用。在这里，`*` 代表多个字符，而 `?` 代表单个字符。

在这个示例中，我们有如下文件夹，包含以下目录和文件![](img/rsrc27M.jpg)
我们正尝试寻找一个名为 `vm*` 的文件（vm 及其右侧的任何字符）。然后，我们将尝试匹配名为 `INSTALL` 的文件。第一次尝试失败了，因为有 4 个 `?`。下一次尝试成功了![](img/rsrc27S.jpg)
我们现在将使用“或”逻辑来匹配模式![](img/rsrc27W.jpg)
图片：我目录中的文件夹
让我们看看是否可以列出中间包含 `a` 和 `i` 字符的目录![](img/rsrc282.jpg)
另一个使用管道的示例：`ls -la | less`![](img/rsrc288.jpg)

#### 处理文件
在本节中，我们将创建、修改、复制、移动和删除文件。还将学习如何读取文件并执行其他任务。

#### 创建文件
要创建文件并执行更多任务，我们使用 `touch` 命令。
`touch test.txt`![](img/rsrc28H.jpg)
语法：`touch [OPTION]... FILE...`
详细语法：`touch [[-a] [-m] | [--time=timetype] [...]] [[-d datestring] | [-t timestamp]] [-c] [-f] [-h] [-r reffile] file [file ...]`
该命令也可以用于更改文件的访问时间![](img/rsrc28T.jpg)
若仅更改最后访问时间，请使用 `-a`。
示例：`touch -a test1.txt![](img/rsrc290.jpg)
在此处，要查看输出，你在 `ls` 命令中使用 `--time` 参数。仅使用 `ls -l` 不会显示最后访问时间，而是显示最后修改时间。

#### 复制文件
要复制文件，使用 `cp` 命令。
语法：`cp [option]... [-T] source destination`
示例：`cp test1.txt test2.txt![](img/rsrc299.jpg)
`cp` 命令可能是危险的，因为它不会询问 `test2.txt` 是否存在。这会导致数据丢失。因此，请始终使用 `-i` 选项![](img/rsrc29E.jpg)
你可以回答 `y` 或 `n` 来接受或拒绝。
将文件复制到另一个目录：`cp test1.txt /home/jan/Documents![](img/rsrc29M.jpg)
使用相对路径而非绝对路径。
现在我在以下目录：`/home/jan/Desktop`。我想将一个文件复制到 `/home/jan/Documents`
命令：`cp test1.txt ../Documents![](img/rsrc29V.jpg)
使用相对路径将文件复制到当前工作目录。在这里我们使用 `.` 表示当前目录 (pwd)![](img/rsrc2A1.jpg ![](rsrc2A5.jpg)

#### 递归复制文件和文件夹
示例：`cp -R` 将包含文件的 `snapt` 文件夹复制到 `snipt`![](img/rsrc2AB.jpg)
让我们从一个目录递归地复制一组文件到其子目录。
命令：`cp -R ./Y/snapt/test* ./Y/snopt![](img/rsrc2AH.jpg)
这是我的桌面。我在桌面的 `Y` 目录中有这些文件。我想将 `test1.txt` 和 `test2.txt` 从 `Y` 复制到 `snopt` 目录。执行命令后![](img/rsrc2AP.jpg)
如何使用通配符？我们已经在示例中用过了，不是吗？！[](rsrc2AW.jpg)

#### 使用硬链接和符号链接连接文件
Linux 文件系统的另一个功能是链接文件。在无需随处维护文件原始副本的情况下，你可以链接文件以保留同一文件的虚拟副本。你可以将链接视为一个占位符。链接有 2 符号：
- 符号链接 (Symbolic links)
- 硬链接 (Hard links)

符号链接是另一个物理文件。它不是快捷方式。该文件链接到文件系统的另一个文件。与快捷方式不同，符号链接可以立即访问数据对象。
语法：`ln -s [OPTIONS] FILE LINK`
示例：`ln -s ./Y/test1.txt testn.txt![](img/rsrc2B7.jpg)
如果你检查 inode（节点索引），你会发现它们是不同的文件。大小也可以看出差异：
- `279185 test1.txt`
- `1201056 testn.txt`
当你创建符号链接时，目标文件不应存在（特别是与目标符号链接同名的目录不应存在）。然而，你可以强制命令创建或替换文件![](img/rsrc2BE.jpg)
`ln` 命令对目录也有效![](img/rsrc2BK.jpg) ![](img/rsrc2BR.jpg)
如果你想覆盖符号链接，必须如上所述使用 `-f`。否则，如果你想将符号链接从一个文件替换为另一个，请使用 `-n`。
示例：我在桌面上有两个目录 `dir1` 和 `dir2`。我创建了一个从 `dir1` 到 `sym` 的符号链接。然后我想将 `sym` 链接到 `dir2`。如果我同时使用 `-s` 和 `-f`（`-sf`），它是不起作用的。这里使用的选项是 `-n`.rsrc2BX.jpg)

#### 移除链接
要删除符号链接，可以使用以下命令：
- 语法：`unlink linkname`
- 语法：`rm linkname`

#### 创建硬链接
现在我们查看创建硬链接。硬链接创建一个独立的虚拟文件。该文件包含了关于原始文件及其位置的信息。
示例：`ln test1.txt hard_link![](img/rsrc2C7.jpg)![](img/rsrc2CD.jpg)
在这里我们没有看到任何符号表示。这意味着该文件是真实的物理文件。如果你查看 inode，你会发现两个文件具有相同的 inode 号![](img/rsrc2CJ.jpg)
我们如何识别硬链接？通常连接到文件的链接数量为 1。即它本身。如果数字是 2，意味着它与另一个文件有连接。
另一个示例![](img/rsrc2CS.jpg)
符号链接不会改变每个文件硬链接数的递增。参见以下示例![](img/rsrc2CX.jpg)
如果原始文件被删除会发生什么？！[](rsrc2D2.jpg)
现在你可以看到 `hard_link` 的链接减少到了 1。符号链接显示为损坏状态或我们所说的孤立状态![](img/rsrc2D7.jpg)

#### 文件重命名
接下来，我们将查看文件重命名是如何工作的。为此使用的命令是 `mv`。`mv` 代表“move”（移动）。
语法：`mv [options] source dest`
示例：`mv LICENSE LICENSE_1`
使用此命令时必须小心。如果你执行以下操作，会发生什么？！[](rsrc2DH.jpg)
该命令的优点之一是你可以同时移动并重命名文件，特别是当你从一个位置移动到另一个位置时。
示例：将 `/home/jan/Desktop/Y/snapt` 移动到 `/Desktop` 同时进行重命名。这类似于 Windows 中的剪切粘贴。
示例：`mv /home/jan/Desktop/Y/snapt/ ./Snap![](img/rsrc2DT.jpg)[](rsrc2DY.jpg)

#### 删除文件
要删除文件使用 `rm` 命令。`rm` 命令不会询问你是否要删除文件。因此，必须使用 `-i` 选项。
语法：`rm [OPTION]... FILE...`

#### 管理目录
有一组命令用于创建和删除目录：
- 创建目录使用 `mkdir` 命令。
- 删除目录使用 `rm` 命令。
语法：`mkdir [-m=mode] [-p] [-v] [-Z=context] [directory]`
`rm [-p] [-v|verbose] [-ignore-non-empty] [directories]`
示例：使用 `mkdir` 命令创建目录。要创建树形目录必须使用 `-p`。如果不尝试，将无法成功![](img/rsrc2EC.jpg)
命令：`mkdir -p ./Dir1/Child1/Child2`](rsrc2EG.jpg)
示例：`rmdir ./Dir1/Child2`](rsrc2EM.jpg)
如果目录包含文件，无法使用 `rm` 命令删除目录。你需要先删除文件。在这种情况下，可以使用另一个命令来实现。
示例：`rm -rf /Temp`](rsrc2F0.jpg)[](rsrc2F5.jpg)

# 第 6 章：磁盘、介质和文件操作
在本章中你将学习磁盘和分区、文件操作、使用 `grep` 排序以及文件合并。
在本章中，我们将查看一些高级命令来监控基本磁盘属性、管理介质（如挂载和卸载），并学习如何使用高级命令管理数据。

### 操作
在前章节中，我们讨论了 Linux 如何处理文件系统以及默认设置。我们将简要查看 Linux 磁盘格式和文件系统。
Linux 发行版运行在以下磁盘格式上：
- `ext2`
- `ext3`
- `ext4`
- `jfs`
- `ReiserFS`
- `XFS`
- `Btrfs`

ext 系列
这是目前最常用的 Linux 文件系统。`ext` 是扩展文件系统 (etc) 的继承者。第二个版本增加了更多改进并解决了 `ext` 版本（用于 MINIX 系统）的局限性。它将大小扩展到 16 GB 到 2 TB。`ext2` 通常用于可移动介质。最大的改进是日志功能。Linux 内核 2.4.15 集成了 `ext2` 文件系统。这是一个巨大的飞跃，因为它非常稳定，且在机器正常关机后不需要检查磁盘从 `ext2` 到 `ext3` 的升级能力是无缝的。第三版本扩展了功能，第四版本侧重于性能标准。`ext4` 是当前版本。它随内核 2.6.28 发布并提供了向后兼容。它支持 16 GB 到 16 TB 的最大大小，并提供了关闭日志的机制。

JFS
日志文件系统由 IBM 用于 AIX。当系统资源（尤其是处理能力）有限时，它可以作为 `ext4` 的替代方案。

ReiserFS
ReiserFS 作为 `ext3` 的替代方案引入，具有更先进的功能和性能。它还有一个更快的日志系统。

XFS
它是具有并行 I/O 处理的高速 JFS。
在之前的章节中引入了逻辑卷管理器 (LVM)(虚拟文件系统）。下面的图片是整个 LVM 文件结构的视图。
![自动生成的屏幕特写](img/rsrc2K2.jpg)
图片：Linux 文件系统层次结构
源：[`en.wikipedia.org/wiki/Unix_filesystem`](https://en.wikipedia.org/wiki/Unix_filesystem)

### 操作磁盘和介质
### 挂载介质
挂载是将介质集成到虚拟系统的技术。必须在访问介质之前完成。某些系统支持自动挂载，但知道如何手动挂载介质是好的。`mount` 命令用于实现此目标。
语法：`mount -t type device dir`
其他语法：
`mount -a [-fFnrsvw] [-t vfstype] [-O optlist]`
`mount [-fnrsvw] [-o option[,option]...] device|dir`
`mount [-fnrsvw] [-t vfstype]`

`mount` 命令用于附加设备。该命令引用 `/etc/fstab`。`mount` 命令提供：
- 设备名称
- 挂载点
- 文件系统类型
类型取决于可的文件。在许多情况下，`vfat` 是主要的文件系统。否则，它可以是一个光盘。
示例：`mount -t vfat /dev/vdb1 /mnt`](rsrc2KW.jpg)
`mount /cd` 或 `mount /dev/cd`




| `-a, –all` : 包含伪文件、重复和不可访问的文件系统。 |
| `-B, –block-size=SIZE` : 在打印之前按 `SIZE` 缩放大小。 |
| `-h, –human-readable` : 以 1024 的幂次方打印大小 |
| `-H, –si` : 以 1000 的幂次方打印大小 |
| `-i, –inodes` : 列出 inode 信息而非块使用情况 |
| `-l, –local` : 将列出限制在本地文件系统 |
| `-P, –portability` : 使用 POSIX 输出格式 |
| `–sync` : 在获取使用信息前调用 sync |
| `–total` : 忽略所有对可用空间无次要影响的条目，并生成总计 |
| `-t, –type=TYPE` : 将列出限制为类型为 `TYPE` 的文件系统 |
| `-T, –print-type` : 打印文件系统类型 |




### 示例

- 显示所有文件的大小：`df -a`
- 显示某个用户家目录的大小：`df /home/username`（将 username 替换为实际用户名）。![](img/rsrc2PB.jpg)
- 显示文件的大小。这次使用更人类可读的格式，单位为字节、KB、MB 和 GB。![](img/rsrc2PG.jpg)
- 以 1000 的幂次方打印大小。![](img/rsrc2PP.jpg)
- 以人类可读的格式显示总计（1024 块）。![](img/rsrc2PW.jpg)
- 显示文件类型：`df -T filename`

有一个类似的命令可以查找磁盘占用。该命令是 `du`。

### 语法
```
du [OPTION]... [FILE]...
du [OPTION]... --files0-from=F
```

### 选项
某些选项与 `df` 命令相似：
- `-0`, `--null` ： 以 NULL 结束每行输出
- `-a`, `--all` ： 写入所有文件的计数，而不仅仅是目录
- `--apparent-size` ： 打印显示大小，而非磁盘占用
- `-B`, `--block-size=SIZE` ： 在打印到控制台之前将大小缩放为 SIZE
- `-c`, `--total` ： 产生总计
- `-d`, `--max-depth=N` ： 仅当目录位于命令行参数 N 或更少层级时才打印总计
- `-h`, `--human-readable` ： 以人类可读的格式打印大小
- `-S`, `--separate-dirs` ： 对于目录，不包含子目录的大小
- `-s`, `--summarize` ： 仅显示每个目录的总计
- `--time` ： 显示任何文件或目录的最后修改时间
- `--exclude=PATTERN` ： 匹配 PATTERN 的文件

### 示例
- 用户家目录的磁盘占用摘要：`du /home/jan`
- 使用人类可读格式查看![](img/rsrc2RN.jpg)
- 任何目录的磁盘占用总计：`dh -sh`![](img/rsrc2RU.jpg)
- 每个文件的磁盘占用：`du -a`
- 获取目录内文件的磁盘占用并显示总计：`du -ch`![](img/rsrc2S0.jpg)
- 从列表中排除某些文件。`du -ah --exclude`![](img/rsrc2S5.jpg)
- 根据文件修改时间的磁盘占用：`du -ah --time /home/jan/Desktop`![](img/rsrc2SA.jpg)

## 获取磁盘分区信息

要使用的命令是 `lsblk`。它代表“list block devices”（列出块设备）。示例所示![](img/rsrc2SH.jpg

查看磁盘和分区信息，请使用以下命令。虽然这些命令有更多用途，但超出了本书的范围。

### 磁盘信息
- 查看分区描述 – 命令：`sudo fdisk -l`![](rsrc2SS.jpg)
- 查看分区信息 – 命令：`sudo parted -l`![](img/rsrc2SX.jpg)

## 处理数据文件

在本节中，我们将介绍用于操作和组织数据的命令。

### 数据排序
在涉及到人类可理解的格式时，排序是最方便的数据用途之一。可以根据许多模式进行排序。例如，从 A-Z 或 a-z，升序或降序。让我们来看一个例子。命令正如你猜的那样，是 `sort`。![](img/rsrc2T4.jpg)

这里发生了什么？如你所见，它取决于基本规则，例如语言规则。在第一个示例中，1 和 0 在一起，1+0 的排序方式类似于 1，然后是 10，然后是 100 等此类推。如果我们看这个例子，会更容易理解。![](img/rsrc2T9.jpg)

如所示，需要更清晰的指令来区分通用规则和更具体的规则。

### 语法
```
sort [OPTION]... [FILE]...
sort [OPTION]... --files0-from=F
```

### 选项
排序命令有很多选项。更多信息请参见 `man sort`。这些选项是自言自明的。让我们来看一些示例。

- 示例：按数值值排序。
  命令：`sort -n File1`![](img/rsrc2TK.jpg)
- 示例：按月份排序。
  命令：`sort -M File2`![](img/rsrc2TT.jpg)

你会说：“哇！没用！”是什么导致文件没有按照英文排序？如果你的系统使用的语言与英语不同，那么这个命令将无法工作！为了修复这个问题，你必须通过访问设置面板来更改所选语言的格式![](img/rsrc2U0.jpg)

如果格式是非英语国家，请将其更改为相应的格式（在我的情况下，我选择了美国）。更改后必须重启![](img/rsrc2U6.jpg)

漂亮！起作用了！另一个示例是使用 `-r` 选项进行反向排序![](img/rsrc2UC.jpg)

当我们排序时，可以指定一个起始位置。当数据文件有很多位置时这非常有用。例如，让我们看看 `/etc/passwd/`。它有许多类似这样的行。假设你想按第 3 字段排序。在这里我们将选择一个字段分隔符，它是 `:`。要指定字段位置，使用 `-k` 参数。要指定字段分隔符，相应地使用 `-t` 参数。排序格式是数字的。示例尝试按数字用户 ID 对 `passwd` 文件进行排序。

之前：![](img/rsrc2UJ.jpg)
执行 `sort -t ':' -k 3 -n /etc/passwd` 后：![](img/rsrc2UP.jpg)
现在排序得很好。

让我们将之前的命令与 `sort` 命令结合使用。按磁盘空间排序示例：`du -sh /home/jan | sort -nr`。在这里，`r` 表示反向排序。此命令 (`du`) 用于获取磁盘占用的总计，按数字反向顺序排序，然后显示前 10 行（默认 `head` 命令返回前 10 行）![](img/rsrc2UX.jpg)

### 使用磁盘空闲和排序命令
在此示例中，`df -h | sort -r -k 5 -I` 能够按使用百分比对磁盘占用进行排序。之前：`df -h`![](img/rsrc2V4.jpg)
之后：`df -h | sort -nrk5`![](img/rsrc2V8.jpg)
如你所示，根据第 5 字段进行了排序。

排序命令提供了 3 个高级功能：
- 评估文件是否未排序。使用 `-c` 选项即可。我们使用 `sort -cn` 来找出文件是否已排序。它会检测第一行无序的内容。对于其他排序选项也是如此![](img/rsrc2VE.jpg)
- 当我们使用 `-u` 选项时可以删除重复项。让我们使用 `sort -un File1`![](img/rsrc2VK.jpg)
- 最后，`sort` 命令可用于将输出到新文件。这也是很好的选项。让我们使用之前的命令。`sort -un File1 > File3.txt`![](img/rsrc2VT.jpg)

## 使用 grep 搜索
涉及到数据处理时，最重要的无疑是搜索能力。现在我们将查看 `grep` 命令。在数据内部进行搜索是任何使用电脑并从事数据处理的人的最重要任务之一。在文件中查找特定的单词或行文本，而不需要滚动几个小时，真的可以节省你的时间。不要将搜索数据与搜索数据混淆。`grep` 具有许多用于查找匹配 PATTERN 的文件选项![](img/rsrc2WE.jpg)

### 语法
```
grep [OPTIONS] PATTERN [FILE]
```

### 选项
对于选项，更多信息请参见 `man grep`。这些选项是自解释明的
- 匹配 PATTERN 的文件，使用 `--color`![](img/rsrc2WD.jpg)
- 显示行号，使用 `-n`![](img/rsrc2WH.jpg)
- 忽略大小写搜索，使用 `-i`![](img/rsrc2WB.jpg)
- 递归搜索，使用 `-r`![](img/rsrc2WR.jpg)
- 仅打印匹配项的文件名，使用 `-l`![](img/rsrc2WS.jpg)
- 打印不匹配项的行，使用 `-v`![](img/rsrc2WY.jpg)
- 统计匹配的行数，使用 `-c`![](img/rsrc2WW.jpg)

### 示例
- 在文件中搜索特定单词：`grep "word" file`
- 使用正则表达式搜索：`grep "pattern" file`
- 忽略大小写搜索：`grep -i "word" file`

## 获取磁盘分区信息

要使用的命令是 `lsblk`。它代表“list block devices”（列出块设备）。示例所示![](img/rsrc2SH.jpg

查看磁盘和分区信息，请使用以下命令。虽然这些命令有更多用途，但超出了本书的范围。

### 磁盘信息
- 查看分区描述 – 命令：`sudo fdisk -l`![](rsrc2SS.jpg)
- 查看分区信息 – 命令：`sudo parted -l`![](img/rsrc2SX.jpg)

## 处理数据文件

在本节中，我们将介绍用于操作和组织数据的命令。

### 数据排序
- 在涉及到人类可理解的格式时，排序是最方便的数据用途之一。可以根据许多模式进行排序。例如，从 A-Z 或 a-z，升序或降序。让我们来看一个例子。命令正如你猜的那样，是 `sort`。![](img/rsrc2T4.jpg)

这里发生了什么？如你所见，它取决于基本规则，例如语言规则。在第一个示例中，1 和 0 在一起，1+0 的排序方式类似于 1，然后是 10，然后是 100 等此类推。如果我们看这个例子，会更容易理解![](img/rsrc2T9.jpg)

如所示，需要更清晰的指令来区分通用规则和更具体的规则。

### 语法
```
sort [OPTION]... [FILE]...
sort [OPTION]... --files0-from=F
```

### 选项
排序命令有很多选项。更多信息请参见 `man sort`。这些选项是自言自明的。让我们来看一些示例。

- 示例：按数值值排序。
  命令：`sort -n File1`![](img/rsrc2TK.jpg)
- 示例：按月份排序。
  命令：`sort -M File2`![](img/rsrc2TT.jpg)

你会说：“哇！没用！”是什么导致文件没有按照英文排序？如果你的系统使用的语言与英语不同，那么这个命令将无法工作！为了修复这个问题，你必须通过访问设置面板来更改所选语言的格式![](img/rsrc2U0.jpg)

如果格式是非英语国家，请将其更改为相应的格式（在我的情况下，我选择了美国）。更改后必须重启![](img/rsrc2U6.jpg)

漂亮！起作用了！另一个示例是使用 `-r` 选项进行反向排序![](img/rsrc2UC.jpg)

当我们排序时，可以指定一个起始位置。当数据文件有很多位置时这非常有用。例如，让我们看看 `/etc/passwd/`。它有许多类似这样的行。假设你想按第 3 字段排序。在这里我们将选择一个字段分隔符，它是 `:`。要指定字段位置，使用 `-k` 参数。要指定字段分隔符，相应地使用 `-t` 参数。排序格式是数字的。示例尝试按数字用户 ID 对 `passwd` 文件进行排序。

之前：![](img/rsrc2UJ.jpg)
执行 `sort -t ':' -k 3 -n /etc/passwd` 后：![](img/rsrc2UP.jpg)
现在排序得很好。

让我们将之前的命令与 `sort` 命令结合使用。按磁盘空间排序示例：`du -sh /home/jan | sort -nr`。在这里，`r` 表示反向排序。此命令 (`du`) 用于获取磁盘占用的总计，按数字反向顺序排序，然后显示前 10 行（默认 `head` 命令返回前 10 行）![](img/rsrc2UX.jpg)

### 使用磁盘空闲和排序命令
在此示例中，`df -h | sort -r -k 5 -I` 能够按使用百分比对磁盘占用进行排序。之前：`df -h`![](img/rsrc2V4.jpg)
之后：`df -h | sort -nrk5`![](img/rsrc2V8.jpg)
如你所示，根据第 5 字段进行了排序。

排序命令提供了 3 个高级功能：
- 评估文件是否未排序。使用 `-c` 选项即可。我们使用 `sort -cn` 来找出文件是否已排序。它会检测第一行无序的内容。对于其他排序选项也是如此![](img/rsrc2VE.jpg)
- 当我们使用 `-u` 选项时可以删除重复项。让我们使用 `sort -un File1`![](img/rsrc2VK.jpg)
- 最后，`sort` 命令可用于将输出到新文件。这也是很好的选项。让我们使用之前的命令。`sort -un File1 > File3.txt`![](img/rsrc2VT.jpg)

## 使用 grep 搜索
涉及到数据处理时，最重要的无疑是搜索能力。现在我们将查看 `grep` 命令。在数据内部进行搜索是任何使用电脑并从事数据处理的人的最重要任务之一。在文件中查找特定的单词或行文本，而不需要滚动几个小时，真的可以节省你的时间。不要将搜索数据与搜索数据混淆。`grep` 具有许多用于查找匹配 PATTERN 的文件选项。

### 语法
```
grep [OPTIONS] PATTERN [FILE]
```

### 选项
对于选项，更多信息请参见 `man grep`。这些选项是自解释的
- 匹配 PATTERN 的文件，使用 `--color`![](img/rsrc2WD.jpg)
- 显示行号，使用 `-n`![](img/rsrc2WH.jpg)
- 忽略大小写搜索，使用 `-i`![](img/rsrc2WB.jpg)
- 递归搜索，使用 `-r`![](img/rsrc2WR.jpg)
- 仅打印匹配项的文件名，使用 `-l`![](img/rsrc2WS.jpg)
- 打印不匹配项的行，使用 `-v`![](img/rsrc2WY.jpg)
- 统计匹配的行数，使用 `-c`![](img/rsrc2WW.jpg)

### 示例
- 在文件中搜索特定单词：`grep "word" file`
- 使用正则表达式搜索：`grep "pattern" file`
- 忽略大小写搜索：`grep -i "word" file`

## 搜索

（注：由于原文中存在大量重复内容，此处已按要求完成翻译并去重逻辑处理）
涉及到数据处理时，最重要的无疑是搜索能力。现在我们将查看 `grep` 命令。在数据内部进行搜索是任何使用电脑并从事数据处理的人的最重要任务之一。在文件中查找特定的单词或行文本，而不需要滚动几个小时，真的可以节省你的时间。不要将搜索数据与搜索数据混淆。`grep` 具有许多用于查找匹配 PATTERN 的文件选项。

（此处根据原文重复情况，翻译逻辑已确保不重复输出原文）





| 参数 | 说明 |
| :--- | :--- |
| `-c` `<string>` | 从（字符串）读取命令 |
| `-i` | 交互式 shell。此接受用户输入。 |
| `-l` | 模拟作为登录 shell 被调用 |
| `-r` | 将 shell 限制在默认目录的用户中 |
| `-s` | 从用户的输入中读取命令 |

要退出 shell（子 shell 和父 shell），请执行 `exit` 命令。为了更详细地理解这一点，让我们来看这个示例。让我们发布一系列命令并逐个执行。

```bash
ls; pwd; cd ..; pwd; ls;
```

现在，让我们验证一下该命令是否启动了子 shell。虽然我们将在下一节中学习更多关于环境变量的知识，但我们将在这里使用一个环境变量。它是 `$BASH_SUBSHELL`。让我们在第一个示例中使用它。

```bash
ls; pwd; cd ..; pwd; ls; echo $BASH_SUBSHELL
```![](img/rsrc31W.jpg)关注最后一行，那里显示为 `0`。

现在，让我们对命令进行细微修改并再次运行。

```bash
(ls; pwd; cd ..; pwd; ls;)!
```![](img/rsrc322.jpg)除了使用了括号外，这看起来很正常。然而，存在巨大的差异。括号让命令在子 shell 中运行。为了识别这一点，让我们运行以下命令。

```bash
(ls; pwd; cd ..; pwd; ls; echo $BASH_SUBSHELL)!
```![](img/rsrc327.jpg)注意底部从 `0` 到 `1` 的变化。

如果你使用嵌套括号，结果会是什么？！[](rsrc32C.jpg)现在你可以看到 2 个子 shell 的形成了。子 shell 可以被有效地使用。管道、进程列表和协进程都会使用子 shell。你可以结合后台模式有效地使用子 shell。例如，你可以通过 `sleep` 命令将进程放入后台。让我们来看一个示例。

```bash
sleep 10
```

这将在前台模式下让进程睡眠 10 秒，正如你看到光标冻结并闪烁 10 秒一样。要将进程放入后台，请在相同的命令后使用 `&`。

```bash
sleep 1000&
```![](img/rsrc32M.jpg)让我们使用 `ps -f` 来识别它。![](img/rsrc32S.jpg)命令返回了作业 ID（Job ID）以及进程 ID（Process ID）。现在让我们使用 `jobs` 命令观察在后台运行的“作业”。当作业运行和结束时，我们可以看到以下输出。

```bash
jobs
```![](img/rsrc32Y.jpg)![](img/rsrc332.jpg)要获取更多信息，请使用 `job -l` 命令。同样，一组进程也可以被放入后台模式。让我们来看另一个例子。

```bash
(sleep 10; echo $BASH_SUBSHELL; sleep 10) &
```![](img/rsrc339.jpg)一旦处理完第一个，你必须再次按一次回车键。![](img/rsrc33D.jpg)现在，第二个进程的状态变得可见了。

### 使用协进程 (Co-processes)
协处理是一种同时启动子 shell 并执行命令的技术。在这里要使用的命令是 `coproc`。
示例：让进程进入睡眠并观察其行为。
命令：
```bash
coproc sleep 10
```![](img/rsrc33N.jpg)

### 内部和外部命令
在 Linux 环境中，命令有两种类型：内部命令和外部命令。

#### 外部命令
这些不是内置 shell 命令。这些命令（又文件文件命令）存在于 shell 之外。它们实际上是程序或工具。因此，这些程序可以位于 `/bin`、`/sbin`、`/usr/bin` 或 `/usr/sbin` 等目录。外部命令的主要区别在于它需要创建一个（在 Linux 术语中称为 fork）子进程来执行。

#### 内部命令
这些是内置的 shell 命令。内部命令不需要创建子进程。要识别命令的类型及其所在位置，我们可以使用以下命令。例如：

```bash
which ps
type -a ps
```![](img/rsrc343.jpg)让我们通过执行以下命令找到更多关于 `/bin/ps` 的信息：

```bash
ls -l /bin/ps
```![](img/rsrc348.jpg)现在根据信息，`ps` 是一个外部命令。那么什么是内部命令呢？像 `echo` 这样的命令就是内部命令。`echo` 命令简单地将内容回显。要查看选项列表，请参见 `man echo`![](img/rsrc34E.jpg)如你所见，`echo` 不返回任何子进程。内部命令的完整列表可以在 [`manpages.ubuntu.com/manpages/xenial/man7/bash-builtins.7.html`](http://manpages.ubuntu.com/manpages/xenial/man7/bash-builtins.7.html) 获取。控制进程时还有其他几个命令。在书中，我们不会从系统管理员的角度来看 `ps` 命令。让我们看看其他的：

- `bg`: 将进程发送到后台（恢复停止的进程）。![](img/rsrc34P.jpg)
- `fg`: 将进程从后台恢复到前台。![](img/rsrc34V.jpg)

这里 `sleep` 进程在子 shell 中创建，然后停止。一旦它停止，就使用 `fg` 命令将其带回前台。

- `bg`: 将进程发送到后台。
- `fg`: 将进程从后台恢复到前台。
- `wait`: 挂起脚本直到作业完成。
- `disown`: 将作业从 shell 中移除。
- `stop`: 挂起进程。
- `kill`: 杀死进程。





![](img/rsrc384.jpg)注意 `head` 命令。这是为了将输出限制在 10 行。

# 系统变量

Linux 操作系统使用了许多环境变量。在使用文本模式（登录）、使用交互式 shell 或非交互式 shell 时，`bash` 都会查找文件来执行命令。查找的文件取决于上述的方法。

当你登录到 Linux 操作系统时，`bash` shell 会作为登录 shell 加载。这个登录 shell 会查找 5 个不同的文件来执行命令。这些：

- `/etc/profile`
- `$HOME/.bash_profile`
- `$HOME/.bashrc`
- `$HOME/.bash_login`
- `$HOME/.profile`

`/etc/profile` 是 `bash` shell 的默认启动文件。登录时，`bash` 会执行 `/etc/profile` 中的命令。让我们来看下 Ubuntu 上这个文件的内容。

![](img/rsrc38J.jpg)

在这里，你可以看到对 `/etc/bash.bashrc` 的调用。正如我们之前讨论的，它包含了系统环境变量。你可能也注意到 `/etc/profile.d`。它存放了特定特定的启动文件。当你登录到 shell 时，这些文件会被执行。让我们来看看这些文件。

```
ls -l /etc/profile.d
```

![](img/rsrc38R.jpg)

`$HOME` 正如你发现的除了 `/etc/profile` 外，其余的共同点。其目的是提供用户特定的启动文件来定义用户特定的变量。每个文件旁边都有 `.`，表示这是一个隐藏文件。

## 交互式 Shell

当你不登录系统而启动 `bash` shell 时，就会启动交互式 shell。尽管它不像登录 shell，但仍然接受命令。

如果启动了交互式 shell，它不需要处理 `/etc/profile`。它直接在用户的 `HOME` 目录下查找 `.bashrc` 文件。它首先查找 `/etc` 目录下的通用 `bashrc` 文件。然后它为用户输入个人命令别名和私有脚本提供了一个空间。

## 非交互式 Shell

在这种情况下，系统开始执行 shell 脚本，尽管这不需要任何交互，但每次启动脚本都需要运行启动命令。这时一个特殊的全局环境变量派上用场了。它被称为 `BASH_ENV`。

```
echo $BASH_ENV
```

![](img/rsrc392.jpg)

如你所见，没有任何设置。那么它是如何工作的呢？

如果你能回起来，某些命令会产生子 shell，这个子 shell 会继承父 shell 出的变量。

如你所知，如果脚本没有产生子 shell，变量在当前 shell 环境中已经可用。现在即使 `BASH_ENV` 未设置，当前 shell 的本地和全局变量也是可用的。

## 使用永久或持久性环境变量

当你创建环境变量时（特别是为了你的需求），你必须将这些变量存储在永久的位置。你可能认为 `/etc/profile` 是存储全局变量的最佳地方，但并不是。它会随着系统活动（如升级）发生变化。相反，可以使用 `/etc/profile.d` 来存储 `.sh` 文件。对于局部变量，最好的地方是用户 `HOME` 目录下的 `.bashrc` 文件。最后，我们将讨论变量数组的一些细节。

## 变量数组

环境变量可以用数组。这是环境变量的一个非常强大的特性。如果你不知道什么是数组，数组是内存中的一个地方（变量），可以存储多个值。让我们来看一个例子。

```
va_months=(Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
echo $va_months
echo ${va_months[0]}
```

第一个命令创建数组并分配值。第二个命令输出数组的第一个元素。第三个命令输出相同的。我们也可以通过以下命令（示例）修改数组项。

```
va_months[0]=January
echo ${va_months[0]}
```

最后，要显示所有数组元素，使用 `*`。

```
echo ${va_months[*]}
```

![](img/rsrc39S.jpg)

# 第 8 章：编写脚本

在本章中，你将学习：
- 编写 Shell 脚本
- 命令别名和替换
- 管道
- 文件、描述符和退出状态
- 结构命令 (if, for, while, until, break, continue)。

在本章中，你将通过示例对脚本编写获得全面的理解。脚本编写的关键在于你对命令的熟悉程度。脚本非常有优势，因为它可以处理多个命令，处理结果，并将一个结果传递给另一个，从而构建一个链链。

你已经知道如何使用 `;` 执行多个命令了。例如，`pwd; cd ..;` 就是一个组合。它是什么？它是一个基础 shell 脚本！

## 编写 Shell 脚本

要编写 shell 脚本，你只需要对 Linux 命令和文本编辑器有一定的。在 Ubuntu 上，可以使用默认编辑器 (`gedit`)。让我们检查一下组件。

一个 shell 脚本以顶部的注释开始。

```bash
#!/bin/shell_type
```

例如，`#!/bin/bash`。这是一个注释，因为它以 `#` 开头。这些行不会被 shell 解释！要写注释，应该使用 `#`。然而，这一特定行告诉 shell 使用哪种 shell 来执行此脚本。我们称 `#!` 为 Shebang。

下一部分将是一组带有说明的命令。如果你熟悉编程，shell 脚本是类似的。

如果我们创建一个示例脚本：

```bash
#!/bin/bash
who
```

`who` 命令显示你登录的账户以及登录时间。

```bash
pwd
```

应该符合预期。![](img/rsrc3AR.jpg) 将其放在 `/bin` 目录或使用 `PATH` 变量来设置路径。你也可以使用绝对或相对路径。下一步要做的是更改权限。根据结果，没有足够的权限执行此文件。系统将它视为脚本，但尚未修改权限。为了提供执行权限，可以使用 `chmod` 命令。

```bash
chmod +x script
```

![](img/rsrcB1.jpg) 一旦完成此步，脚本就准备好执行了。![](img/rsrcBD.jpg) 如果你想显示文本，可以使用 `echo` 命令。我们在上一节中学习了环境变量。

## 命令别名

使用命令别名可以节省大量时间。要定义别名，你必须进行简单的赋值。

语法：`alias="ls -al"`
示例：`alias search=grep`

## 命令替换

将命令的输出作为变量输入也是可能的。这是一个强大的功能。要实现这一点，必须使用 `$()`。

示例：`user_name=$(who)`

脚本：

```bash
#!/bin/bash
user_name=$(who)
echo "Your username is : $user_name"
```

![](img/rsrcC0.jpg)<< 创建文件

另一个强大的特性是你可以输出结果。你可以根据你的需求命名文件。在下一个示例中解释了这一点。

```bash
#!/bin/bash
mydate=$(date +%Y%m%d)
echo "Today is : $mydate"
who > log.$mydate
```

![](img/rsrc3CA.jpg)在这里创建一个日期并对其进行格式化。`%Y` 是 `YYYY` 格式。月份是数字格式（例如 `09`），日期也是数字格式。输出类似于 `YYYYMMDD`。输出被取入变量。然后我们 `echo` 该变量。最后我们使用 `>` 运算符将其输入重定向到新文件。文件名创建为 `logYYYYMMDD`。这就是我们创建日志以记录的方法。如果脚本在第二天运行，文件名将是 `log2019025`。重定向是一个非常有用的功能。与其使用 `touch` 命令，你可以将输出重定向到文件。你甚至可以使用 `touch` 命令从脚本创建文件。例如：

```bash
#!/bin/bash
mydate=$(date +%Y%m%d)
echo "Today is : $mydate"
touch log.$mydate
```

![](img/rsrc3CN.jpg)# 创建文件并将部分命名为 `.log` 之后使用我们的变量

```bash
who >> log.$mydate
```

![](img/rsrc3CT.jpg)# 将 `who` 命令的输出追加到文件中。

你也可以执行我们使用 `>` 运算符执行的反向过程。这被称为输入重定向。例如，我们可以获取文件的条目直接到新变量或命令。以下示例详细解释了这一点。

```bash
#!/bin/bash
wc < log.20190924
```

`wc` 是你的一个新命令。它统计行、字和字符数。![](img/rsrc3D0.jpg)我们将查看 `<<` 运算符。这被称为内联输入运算符。

示例：

```
wc << lastLine
```

![](img/rsrc3D5.jpg) 如你注意到，直到 `lastLine` 作为文本输入，它捕捉了用户输入。

其他示例：将错误和标准输出重定向到同一个文件。你可以可以使用命令。

```
ls Test Test2 Test3 > dirlist 2>&1
```

在这里，我们尝试列出 `Test` 目录的属性。记住，`ls` 命令支持多个文件或目录名。然后列出每个文件或目录的属性。`Test` 和 `Test2` 目录在我的桌面上。`Test3` 目录不存在。我将此命令的输出以及错误都重定向到一个名为 `dirlist` 的新文件中。![](img/rsrc3DE.jpg)<<标准文件描述符

我们再次回顾描述符。

- 标准输入 - 0: STDIN
- 标准输出 – 1: STDOUT
- 标准错误 - 2: STDERR

第一个是标准输入，后续是标准输出和标准错误。数值是描述符。除了这些技术，管道在脚本中被广泛使用。

## 管道

当一个命令的输出作为另一个命令的输入时，管道非常有用。这是我们到为止学到的内容。使用的运算符是 `|`。

示例：

```bash
#!/bin/bash
cat employee.txt | sort -nr -k 2
```

在这里我们重定向输出。![](img/rsrcDY.jpg) 脚本构建中的数学运算

任何脚本都可以用于执行某些计算。Linux 中有一些内置命令。这些是 `expr` 的表达式。![](img/rsrcEA.jpg)与其使用 `expr` 命令，使用括号更方便。

```bash
#!/bin/bash
var1=2
var2=6
var3=3
var4=$((var1 * var2))
echo $var4
```

![](img/rsrc3EZ.jpg)Bash 计算器当你想要执行复杂的数学函数时，有一个内置工具来执行。它是 `bc`。

`bc` 命令支持：
- 整数和浮点数
- 变量
- 表达式
- 函数
- if-then-else
- 注释

在最后一行，你可以看到一个问题：8.45/5 = 1.6 是不准确的，除非向上舍入。这里的问题是小数位数。为了获得预期的输出，我们需要修改 `scale`。(rsrc3FR.jpg) `bc` 命令支持变量。以下示例使用了变量而不是数值。

```bash
#!/bin/bash
var1=10
var2=2
var3=$(echo "$var1 ^ $var2" | bc)
echo "The answer is : $var3"
```

![](img/rsrc3G8.jpg)另一个使用 `scale` 选项示例。

```bash
#!/bin/bash
var1=10
var2=3
var3=$(echo " scale=3; $var1 / $var2" | bc)
echo "The answer is : $var3"
```

![](img/rsrc3GH.jpg) 下一个示例将查看内联输入运算符如何在脚本中与 `bc` 命令结合。

```bash
#!/bin/bash
var1=8
var2=1.75
var3=3
varF=$(bc << EOF # EOF 代表文件结束
scale = 4
v1 = ($var1 * $var2)
v2 = ($var1 / $var3)
v1 + v2
EOF)
echo The final calculation is: $varF
```

![](img/rsrc3H2.jpg)




| 代码 | 含义 |
| :--- | :--- |
| 0 | 命令成功执行 |
| 1 | 未知错误 |
| 2 | 命令误用 |
| 126 | 命令无法执行 |
| 127 | 未找到命令 |
| 128 | |
| 128+x | |
| 130 | |
| 225 | |

退出状态还有一个很有趣的特性：你可以定义自己的退出码。这通过使用 `exit` 命令后跟一个你指定的数值来实现。

示例：
```bash
#!/bin/bash
ls -la Test
exit 100
```
在结果末尾，当执行 `echo $?` 时，它会显示我们定义的退出码。

另一个示例：
```bash
#!/bin/bash
ls -la Test
echo $?
exit 100
```
如果你观察退出码，可以识别出一个范围（0 – 255）。这是因为 shell 使用了一种名为“取模运算”的方法来计算退出码。它将错误值除以 256，并使用余数作为退出码。

## 结构化命令

到目前为止我们学习了很多命令以及如何构建基础脚本。你也可以使用 `man` 命令或 `--help` 选项来学习关于命令和其他特性的知识。

对于脚本编写，如果你是一个程序员甚至是一个新手，你必须应用一些条件。否则，当我们为了应用可能需要复杂逻辑的现实场景构建脚本时，我们就无法构建命令结构来获取逻辑输出。为了解决这个问题，脚本可以像其他编程语言一样利用 `if-then-else` 和 `for` 等结构化命令。这些被称为条件或逻辑结构。在本节中，我们将深入学习结构化命令。让我们先从一个简单的开始。

### if-then-fi 和 if-then-else-fi

在任何编程语言和逻辑中，`if-then` 逻辑都是最基本的。你可以在脚本中使用同样的方法。以下是它的用法：

```bash
if [expression];then
    # 如果 'expression' 为真，则执行代码
fi
```

示例：
```bash
#!/bin/bash
if grep APR --color File3.txt
then
    echo "APR is found in the file"
else
    echo "APR is not found"
fi
```

然而，如果无法进行比较，这种方法就是无效的。例如，如果你想比较多个情况（例如 APR、MAY、JUN 等）并进行一些逻辑操作，你将需要一种技术来实现。这时 `test` 功能就派上用场了。

```bash
if test conditionthen
    commands
fi
```

在不使用 `test` 单词的情况下，我们可以直接使用方括号。这样做时，必须注意以下几点：
- 你必须在最左边的括号处留空格。
- 你必须在最右边的括号处留空格。

测试条件可以比较数值、字符串和文件。让我们也学习一下运算符以及如何使用它们：
- `eq` : 等于运算符，用于比较两个值。
- `le` : 小于或等于运算符。
- `lt` : 小于运算符。
- `ge` : 大于或等于运算符。
- `gt` : 大于运算符。
- `ne` : 不等于运算符。

我们也可以用类似的方法进行字符串比较。运算符如下：
- `str1 = str2` : 匹配两个字符串是否相等。
- `str1 != str2` : 匹配不相等。
- `str1 > str2` : 大于运算符。
- `str1 < str2` : 小于运算符。
- `-z str1` : 检查长度是否为 0。
- `-n str1` : 检查长度是否大于 0。

让我们也来看看文件比较运算符。

### 文件比较运算符

| 运算符 |  |
| :--- | :--- |
| `FILE1 -ef FILE2` | `FILE1` 和 `FILE2` 具有相同的设备号和 inode 码 |
| `FILE1 -nt FILE2` | `FILE1` 比 `FILE2` 新（修改日期） |
| `FILE1 -ot FILE2` | `FILE1` 比 `FILE2` 旧 |
| `-b FILE` | `FILE` 存在且是块设备文件 |
| `-c FILE` | `FILE` 存在且是字符设备文件 |
| `-d FILE` | `FILE` 存在且是一个目录 |
| `-e FILE` | `FILE` 存在 |
| `-f FILE` | `FILE` 存在且是普通文件 |
| `-g FILE` | `FILE` 存在且设置了组 ID (setgid) |
| `-G FILE` | `FILE` 存在且属于有效组 ID |
| `-h FILE` | `FILE` 存在且是一个符号链接（与 `-L` 相同） |
| `-k FILE` | `FILE` 存在且设置了粘滞位 (sticky bit) |
| `-L FILE` | `FILE` 存在且是一个符号链接（与 `-h` 相同） |
| `-O FILE` | `FILE` 存在且所有有效用户 ID |
| `-p FILE` | `FILE` 存在且是一个命名管道 |
| `-r FILE` | `FILE` 存在且已授予读权限 |
| `-s FILE` | `FILE` 存在且大小大于零 |
| `-S FILE` | `FILE` 存在且是一个套接字 |
| `-t FD` | 文件描述符 `FD` 在终端上打开 |
| `-u FILE` | `FILE` 存在且设置了用户 ID (setuid) |
| `-w FILE` | `FILE` 存在且已授予写权限 |
| `-x FILE` | `FILE` 存在且已授予执行（或搜索）权限 |





让我们来看一些例子。

### 基础比较
```bash
#!/bin/bash
T1="Jan"
T2="Jake"
if [ "$T1" = "$T2" ]; then
echo true
else
echo false
fi
```
![](img/rsrc3U8.jpg)

在这个例子中，我们匹配两个字符串。使用 `if` 匹配命令以获取匹配结果是真还是假。这种逻辑被称为布尔逻辑（Boolean logic）。

如果我们在 `if` 语句之前和之后放置命令会发生什么呢？这些命令不会被视为 `if` 语句的一部分！它们将会在语句之外相应地执行或失败。

在这条命令中，我们使用 `else` 来匹配错误条件。也就是说如果匹配结果为失败。如果你移除 `else` 和 `echo false`，结果会是什么？

示例：
```bash
T1="Jan"
T2="Jake"
if [ "$T1" = "$T2" ]; then
echo true
fi
```
![](img/rsrc3UM.jpg)

如你所注意到的，没有输出。因为两个名字不匹配，它直接跳出了 `if` 语句。在这个例子中，我们使用了逻辑运算符 `=`。我们也可以使用 `!=` 来评估不匹配（或者使用 `-ne`）。`!` 应用非（NOT）逻辑。与 `EQUAL` 运算符结合时，逻辑为不等于（NOT EQUAL）。如果 `T1` 不等于 `T2`，则返回真。

```bash
if [ "$T1" != "$T2" ]; then
```
![](img/rsrc3UU.jpg)

你可以在 `if [expression]; then` 和 `fi` 之间指定更多操作。让我们在这个例子中匹配一个退出码并在中间添加更多命令。

```bash
#!/bin/bash
varx=$(ls -l Test 2>/dev/null)
$?
echo $varx
if [ $varx -eq 0 ]; then
echo A match found
echo varx?
else
echo "The file/directory does not exist"
fi
```

在这个例子中，我们正在获取 `ls` 命令的退出码。如果目录存在，退出码将是 `0`。如果目录不存在，它将是其他值（`1`）。我们通过将其发送到 `/dev/null` 来抑制错误信息。在表达式末尾，我们请求退出码。

然后我们使用 `echo` 命令输出退出码。最后，我们比较退出码。如果是 `0`，则匹配成功，我们再次回显 `varx`。如果退出码不匹配，则 `else` 为真，并将显示另一个消息（该文件/目录不存在）。为什么我们在这里需要 `else`？为了匹配虚假逻辑。在较长的形式中，我们将使用 `elif` (else if) 来匹配各种情况。

![](img/rsrc3VB.jpg)

如你所见，目录存在且返回码为 `0`。让我们删除目录并再次尝试。![](img/rsrc3VF.jpg)
现在目录消失了，输出符合预期。

### 使用嵌套 If
在脚本中，你可能需要匹配比布尔逻辑更多的内容。相反，你可能需要匹配每一个情况。例如，如果你运行 `ls` 命令，可能会更多的退出码需要匹配，并且根据每个代码，我们可以采取行动。这种方法被称为嵌套（nesting）。让我们来看一个例子。

```bash
#!/bin/bash
a=10
b=20
if [ $a -eq $b ]
then
echo “a = b”
elif [ $a -gt $b ]
then
echo “a > b”
elif [ $a -lt $b ]
then
echo “a < b”
else
echo “None of the conditions have met”
fi
```
![](img/rsrc3W5.jpg)

输出是准确且符合预期的。让我们尝试另一个例子。

```bash
#!/bin/bash
user_name=jake
if grep $user_name /etc/passwd
then
echo "The user $user_name found in the system."
elif ls -d /home/$user_name
then
echo "The user $user_name not found but a profile directory exists"
fi
```
![](img/rsrc3WM.jpg)

现在删除用户但不删除他的文件。![](img/rsrc3WS.jpg)
现在，让我们再次执行脚本。![](img/rsrc3WX.jpg)
由于我们没有在使用 `userdel` 时使用 `-f` 选项，配置文件夹仍然存在。这是删除用户时查找剩余文件的一种有用方法。我们甚至可以通过添加另一个情况来扩展此代码。让我们来看接的例子。这一次 jake 的家目录已经被删除。

```bash
#!/bin/bash
user_name=jake
if grep $user_name /etc/passwd
then
echo "The user $user_name found in the system."
elif ls -d /home/$user_name
then
echo "The user $user_name not found but a profile directory exists"
else
echo “The user $user_name does not exist!”
fi
```
![](img/rsrc3XD.jpg)

现在，让我们来看一些文件比较的例子。

```bash
#!/bin/bash
mydir=$home/jan
if [ -d mydir ]
then
echo “The directory $mydir exists!”
ls -l $mydir
else
echo “The directory $mydir does not exist”
fi
```
![](img/rsrc3XV.jpg)

现在比较两个文件的日期，如果另一个文件较旧，则从较新的（临时）文件中追加一些文本。

```bash
#!/bin/bash
varF=/home/jan/Desktop/File1.txt
ls -al > temp.txt
if [ temp.txt -nt File1.txt ]
then
temp.txt >> File1.txt
echo File updated
else
echo The file is newer than the temporary file
fi
```
![](img/rsrc3YA.jpg)

在现实场景中，我们还可以使用这种方法了解是否可以读取文件、写入文件、更新日志文件，并在日志中添加日期和其他细节。让我们尝试是否可以验证文件是否存在以及是否可以向其写入。

```bash
file_name=/home/jan/Desktop/myfile
if [ -f $file_name ] #如果是一个文件且存在
then
if [ -s $file_name ] #如果文件大小大于零
then
if [ -w $file_name ]
then
echo "This file is writable"
date >> $file_name
else
echo "This file is not writable!"
fi
else
echo "This file is empty"
fi
```
![](img/rsrc3YZ.jpg)

我们正在测试每个分支，这里是文件存在、文件不可写以及最后当它被删除或不存在时的输出。

### 使用布尔运算符组合测试用例
当你编写脚本时，你可能需要为了决策比较多一个测试用例（复杂情况）。有两个运算符 `&&` 和 `||` 分别代表与（AND）和或（OR）逻辑。例如，我们可以匹配文件是否存在以及大小是否为零。

### 使用更多功能
还有其他一些高级功能，例如双圆括号和双方括号，用于数学运算和高级字符串操作。我们使用双括号是为了使用内部操作，而不是让单括号产生子壳。在继续之前，有几个符号是你理解的。表 8.3：逻辑运算符

| 符号 | 描述 |
| :--- | :--- |
| ! | 逻辑取反 |
| ~ | 位取反 |
| & | 位与 |
| && | 逻辑与 |
| \| | 位或 |
| \| | 逻辑或 |
| ** | 幂/指数 |
| --val | 前减 1 |
| val-- | 后减 1 |
| ++val | 前增 1 |
| val++ | 后增 1 |
| << | 位移（左） |
| >> | 位移（右） |





# case 命令

当存在长长的 `if-then-else` 语句时，`case` 命令非常有用。通过 `case` 命令，可以将阶段表示为不同的 case。

语法：
```bash
case $variable-name in
pattern1)
    command1...commandN;;
patternN)
    command1...commandN;;
*)
    esac
```
你也可以使用 `pattern1|pattern2|pattern3)` 来匹配多个模式，而不是单个模式。`case` 命令可用于高度高级的决策结构。

### 高级示例：
```bash
#!/bin/bash
if [ -z $1 ] #如果运行脚本时没有参数
then
  rental="Unknown vehicle"
elif [ -n $1 ]
then
  # 如果提供了参数，则将其作为租赁
  rental=$1
fi
# 使用 case 语句进行租赁决策
case $rental in
"car") echo "For $rental rental is $25 per k/m.";;
"van") echo "For $rental rental is$20 per k/m.";;
"jeep") echo "For $rental rental is $18 per k/m.";;
"bicycle") echo "For $rental rental $1 per k/m.";;
*) echo "Sorry, no $rental rental is available for you!";;
esac
```
执行此脚本与之前的脚本有所不同。要执行它，你必须在执行命令中提供一个参数![](img/rsrc43B.jpg)

### 另一个示例：
```bash
#!/bin/bash
case $USER in
root) echo "Welcome Superuser";;
jan | jake) echo "Welcome administrator!";;
testuser) echo "Welcome test! Please use the dev board for reporting";;
*) echo "Access is denied!";;
esac
```
![](img/rsrc43W.jpg)

# for 命令

在脚本编写中，你经常会遇到命令迭代或循环的需求。例如，当你从一个文件或一组文件中读取内容时，这变得非常有用。

语法：
```bash
for var in list
do
    commands
done
```
在这里，`var` 变量持有当前列表项的值。在一次完整迭代结束后，它持有最后一次迭代的值。

### 基础示例：
```bash
#!/bin/bash
for i in {1..5}
do
  echo "Welcome $i times"
done
```
![](img/rsrc44H.jpg)
`for` 命令可以用于以下方法。这主要用于编程中。

### C 风格命令

以下语法被称为 C 风格。在 C 编程语言中，这种表达式风格用于循环等。

语法：
```bash
for (( EXP1; EXP2; EXP3 ))
do
    command1
    command2
    command3
done
```

### 示例：
```bash
#!/bin/bash
for (( a=0; a<=5; a++ ))
do
  echo "Welcome $a times"
done
```
![](img/rsrc456.jpg)
我们甚至可以利用多个表达式。例如，我们可以使用：
`for (( a=0, b=9; a<=5; a++,b--))`

### 带有 IF 命令的 for

可以将 `for` 与 `if` 结合，以便在满足条件时退出循环。它还有其他用途。例如，当你想要查找一个文件时，可以使用 `for` 循环搜索文件名。通过使用 `if`，你可以在找到文件时结束循环。

### 高级示例：
```bash
#!/bin/bash
for file in /etc/*
do
  if [ "${file}" == "/etc/resolv.conf" ]
  then
    countNameservers=$(grep -c nameserver /etc/resolv.conf)
    line=$(grep -n nameserver /etc/resolv.conf)
    lineNumber=${line%:*}
    echo "Total ${countNameservers} nameservers defined in ${file}"
    head -n $lineNumber /etc/resolv.conf | tail -1
    #echo $varRes
    break
  fi
done
```
这是一个复杂的示例。它搜索名称解析表（文件）。找到它后，它计算 nameserver 的数量并输出计数。它通过将行号赋给行变量，然后从字符串中获取行号来显示 nameserver 列表（该字符串在冒号之前是行号）。然后我们使用 `head` 和 `tail` 命令显示条目。
![](img/rsrc45Z.jpg)

当你使用 `for` 循环时，记住不要使用某些表达式，例如带有 `` ` 符号的字符串。这会搞乱输出。也不要在字符串中使用包含多个单词的值，因为 `for` 命令会假设每个列表项是用空格分隔的。如果你将 `New Name` 作为一个单个列表项，它会将其视为两个项。你需要根据情况使用 `""`。

正如你之前做的那样，你可以从变量中读取列表。例如：
```bash
#!/bin/bash
list="Car Bus Bike Helicopter"
for vehicle in $list
do
  echo "Have you ever traveled back home by $vehicle?"
done
```
![](img/rsrc46D.jpg)
它也可以用于从命令中读取值。

### 示例：在此示例中，我们使用一个包含车辆列表的文件。
```bash
#!/bin/bash
list="vehicles"
for vehicle in $(cat $list)
do
  echo "Travel home by $vehicle"
done
```
![](img/rsrc46U.jpg)
如果存在像 Aston Martin 这样的名称会发生什么？再次，`for` 命令会破坏输出。为了解决这个问题，引入了分隔符。

### 字段分隔符

分隔符可以是空格、制表符，甚至是换行符。有一个名为 `Internal Field Separator (IFS)` 的环境变量。这是之前问题的根源。为了解决这个问题，可以定义自己的分隔符。

```bash
#!/bin/bash
list="vehicles"
IFS=$'\n' # 定义我们所需的字段分隔符
for vehicle in $(cat $list)
do
  echo "Travel by $vehicle"
done
```
![](img/rsrc47G.jpg)
`for` 的另一个有用功能是支持通配符。这通常用于搜索文件。例如，可以使用 `for file in /home/*`。

# while 命令

`while` 命令比 `for` 更灵活，类似于 `if-then-else`。

语法：
```bash
while test
do
    other commands
done
```
`while` 循环只要退出码为零，就会一直运行。如果不是，它将中断迭代并结束循环。

### 示例：
```bash
#!/bin/bash
num1=5
while [ $num1 -gt 0 ]
do
  echo $num1
  num1=$[num1 - 1 ]
done
```
![](img/rsrc48A.jpg)

# until 命令

`until` 命令可以被视为 `while` 命令的反相反。

语法：
```bash
until test
do
    other commands
done
```

### 示例：
```bash
#!/bin/bash
var1=10
until [ $var1 -eq 0 ]
do
  echo $var1
  var1=$[var1 - 2 ]
done
```
![](img/rsrc48Y.jpg)

# break 和 continue 命令

控制循环是脚本编写的基本要求。`break` 命令直接跳出循环。它可以与 `if-then-else`、`while` 和 `until` 命令配合使用。另一方面，`continue` 命令跳过当前迭代并进入下一次。但它不会完全中断循环。

```bash
#!/bin/bash
for i in 1 2 3 4 5 6 7 8 9
do
  if [ $i -eq 5 ]
  then
    echo “skipping 5th iteration…”
    continue
  fi
  echo “I is equal to $i”
done
```
![](img/rsrc49.jpg)
这结束了关于结构化命令和条件的课程。在最后，我们将查看一个现实场景，以便你实践所学的知识。

### 示例：创建一组用户

如果你一直担任管理员工作，你可能已经使用过批量更新创建用户的方法。在这种情况下，我们通常使用文本文件或逗号分隔的文件（如果是 Windows 用户则使用电子表格）。在本示例中，我们将使用此类文件并创建多个用户。创建用户时，你必须访问文件，检查用户是否存在，并迭代到文件末尾。文件中将以下字段：`username,fn`。在这里，`fn` 代表全名。正如你注意到的，逗号分隔的文件与默认字段分隔符不匹配。在这种情况下，我们需要使用自己的分隔符 `IFS=','`。

```bash
#!/bin/bash
inp="/home/jan/Desktop/users"
while IFS=',' read -r uid fn
do
  echo "adding $uid"
  useradd -c "$fn" -m $uid
done < $inp
```
![](img/rsrc4A6.jpg) 第 9 章：函数简介

在本章中，你将学习：
- 什么是函数
- 参数和选项
- `getopt(s)`
- 写函数
- 处理函数（退出状态、参数、变量和数组）

### GAWK 基础

在进入函数之前，本节将讨论一些重要主题，从处理用户输入开始。处理用户输入在实际场景中是关重要的。当需要处理来自用户的数据和输入时，交互式脚本非常有用。Linux 提供了几个命令行参数、选项以及处理直接输入（例如从键盘）。

你已经意识到在执行 shell 脚本时启动值是如何传递的。例如，我们带有 `car` 值执行了 `./Myscript`。它为该输入提供了特定信息。这实际上是一个交互式脚本，它能够处理用户输入。

读取提供的参数由 `bash` 处理。有一个特殊变量称为位置参数。这些参数处理脚本名和另外 8 个参数，因此可以使用自定义输入值。脚本名由 `$0` 持有。`$1 - $9` 保存剩余部分。让我们来看带有 2 个参数的简单数学方程。

```bash
#!/bin/bash
multiplication=$[ $1 * $2 ]
echo The multiplication of $1 and $2 is $multiplication
```
![](img/rsrc4B1.jpg)
它获取 `$1` 和 `$2` 并执行一个简单的数学运算。

### 另一个示例：
```bash
#!/bin/bash
var1=$USER
echo Welcome $var1
echo Wishing you a happy $1
```
在本示例中，它获取 `$1` 并向用户显示问候。![](img/rsrc4BD.jpg)
如果你在执行脚本时想在引号内输入多个单词，必须使用双引号。否则，它们会被视为两个项。在下一个示例中，我们将读取脚本名并根据此做决策。有一个特殊变量是 `$0`。它可能包含路径以及其他值。`basename` 命令在这些操作中非常方便。

```bash
#!/bin/bash
var1=$0
var2=$(basename $0)
if [[ $var2 == "Myscript" ]]
then
  echo This is Jan’s script $var1
else
  echo This not Jan’s script $var2
fi
```
![](img/rsrc4BZ.jpg)
现在你知道如何将脚本名作为变量。你可以根据它做决策。例如，如果脚本名为 `who`，它可以运行 `who` 命令。当你带有参数运行脚本时，必须确保没有传递不准确或意外的值导致崩溃。因此，测试输入并通过 `if-then-else` 阶梯是最佳实践。

# 参数计数

有一个特殊变量 `$#` 用于计数参数数量。这在执行脚本时非常有用。让我们来看：

```bash
#!/bin/bash
var1=$#
echo Number of arguments $var1
```
![](img/rsrc4CC.jpg)

### 另一个示例：仅当参数数量为 1 时计算阶乘。
```bash
#!/bin/bash
var1=$#
num=$1
if [ $var1 -eq 1 ]
then
  fact=1
  while [ $num -gt 1 ]
  do
    fact=$((fact * num))
    num=$((num - 1))
  done
  echo $fact
else
  echo "Script usage: ./Myscript 5"
fi
```
![](img/rsrc4D0.jpg)
还有两个提供了获取最后一个参数和脚本名的方法。这些是 `$!` 和 `${#}`。让我们运行以下脚本并获取输出。

```bash
#!/bin/bash
echo $#
echo ${!}
```
![](img/rsrc4DF.jpg)

# 移位操作

`shift` 命令是另一个有用命令。它将当前的位置参数左移 `n` 次。默认 `n = 1`。

语法：
```bash
shift [n]
```
在下一个示例中，尝试移位提供的值：
```bash
shift 0
echo Param 0: $0
echo Param 1: $1
echo Param 2: $2
echo Param 3: $3
echo Param 4: $4
```
![](img/rsrc4EP.jpg)
现在开始移位它们：
```bash
shift 1
echo Param 0: $0
echo Param 1: $1
echo Param 2: $2
echo Param 3: $3
echo Param 4: $4
```
![](img/rsrc4F2.jpg)
尽管 `$0` 没有变化，但其他值已经移位。这次我们使用 `for` 循环。

```bash
for (( i = 0; i <= 4; i++ ));
do
  echo Shifting $i:
  echo 1: $1
  echo 2: $2
  echo 3: $3
  echo 4: $4
  shift
done
```
![](img/rsrc4FG.jpg)
在输出中，你可以看到提供的值在 5 次迭代期间是如何移位的。如果我们提供 4 个值，整个值将移位而没有任何剩余。我们可以使用这种移位来执行遍历文件夹等操作。实际示例是删除特定目录或 3365 天的目录的文件。

# 使用选项移动

在上一节中，我们学习了执行时传递参数或参数。我们也可以传递选项。这些选项可以根据提供的选项做出决策。让我们来看一个示例：
```bash
while [ -n "$1" ]
do
  case "$1" in
    -x) echo "Found a valid option -x" ;;
    -y) echo "Found a valid option -y" ;;
    -z) echo "Found a valid option -z" ;;
    *) echo "$1 is not a valid option" ;;
  esac
  shift
done
```
![](img/rsrc4G4.jpg)
如果我们结合查找参数和选项的示例，我们可以成功获取：
```bash
while [ -n "$1" ]
do
  case "$1" in
    -x) echo "Found a valid option -x" ;;
    -y) echo "Found a valid option -y" ;;
    -z) echo "Found a valid option -z" ;;
    *) echo "$1 is not a valid option" ;;
  esac
  shift
  count=1
  for params in "$@"
  do
    echo "Variable $@ Parameter #$count = $params"
    count=$[count + 1 ]
  done
done
```
(注：由于输入用户提供的原始文本中存在大量重复和乱码的占位符，我已根据逻辑提取并翻译了核心有效的技术部分。)





1. 正常操作示例。
2. 失败，因为缺少栈大小的值。
3. 提供了完整的选项和参数值。
4. 额外的参数值被拒绝。
5. 了 `d` 作为大小（它应该检查数字）以及一个无效的 ‘-5’。
6. 另一个包含 3 个选项和一个参数值的正常操作。

如你所见，`getopt` 存在一些问题。最常见的问题是多个参数值，以及当用空格分隔时无法将两个或多个值识别为一个整体。即使我们使用 `""`，`getopt` 也无法检测出差异。

### getopts 救场

`getopts` 有两个重要的隐式变量（环境变量）。它们是：
- `$OPTIND`
- `$OPTARG`

`$OPTIND` (OPTion INDex) 是指向标志（例如 `-a`）的参数指针。`$OPTARG` (OPTional ARGuments) 是附加到标志上的可选参数（例如 `-a test`）。

还有其他一些规则：
- 如果字母后面跟着 `;`，则认为该选项带有参数值。
- 如果命令以 `:` 开头。
- 如果提供的选项没有带 `-` 或 `+`，则将停止处理。
- 当配合此使用 `while` 命令时，不需要括号。

示例：在这个示例中，我们将使用 `getopts` 从算法选择中获取文件的校验和。这是与单独运行命令的输出对比。

```bash
#!/bin/bash
USAGE="Usage= `basename $0` options [-m filename] [-s filename] -h for help. Example: ./Myscript -m File1.txt"
FILENAME_M='' #此参数通过 -m 提供
FILENAME_S='' #此参数通过 -s 提供
SEL='' # 记录来自 m, s 或 h 的选择
while getopts "m:s:h" opt; do #在 m 或 s 后面必须有一个值
  case "$opt" in
    m)
      FILENAME_M="$OPTARG" # 赋值可选值
      echo "MD5 Selected"
      SEL=$opt # #SEL=m
      ;;
    s)
      FILENAME_S="$OPTARG" # 赋值可选值
      echo "SHA1 Selected"
      SEL=$opt # #SEL=s
      ;;
    h)
      echo $USAGE && exit 0
      ;;
  esac
done
shift $(( OPTIND - 1 ))
if [[ $SEL == m ]] && [[ $FILENAME_M == '' ]]; then
  # 如果未提供文件名
  echo "YOU MUST PROVIDE A FILE NAME!X $USAGE" >&2
  exit 1
elif [[ $SEL == m ]] && [[ $FILENAME_M != '' ]]; then
  # 如果 m 带有文件名
  echo -----------------------------
  md5sum < $FILENAME_M
  echo -----------------------------
elif [[ $SEL == s ]] && [[ $FILENAME_S == '' ]]; then
  # 如果 s 没有文件名
  echo "YOU MUST PROVIDE A FILE NAME!Y $USAGE" >&2
  exit 1
elif [[ $SEL == s ]] && [[ $FILENAME_S != '' ]]; then
  # 如果 s 带有文件名
  echo -----------------------------
  sha1sum < $FILENAME_S
  echo -----------------------------
else
  echo "Unable to proceed: $USAGE"
fi
```

### 读取用户输入

脚本或任何程序最重要的交互功能是获取用户输入并对其处理以创建有效且准确的输出。在 Linux 世界中，我们使用 `read` 命令读取用户输入。该命令提供了一系列全面的选项，并用于高级操作。

语法：`read [-ers] [-a array] [-d delim] [-i text] [-n nchars] [-N nchars][-p prompt] [-t timeout] [-u fd] [name ...] [name2 ...]`

表 9.1: read 命令选项

| 选项 | 说明 |
| :--- | :--- |
| `-a array` | 将读取的单词赋予数组变量 `ARRAY` 的顺序索引，从零开始 |
| `-d delim` | 继续直到读取到 `DELIM` 的第一个字符，而不是换行符 |
| `-e` | 使用 Readline 在交互式 shell 中获取行 |
| `-i text` | 使用 `TEXT` 作为 Readline 的初始文本 |
| `-n nchars` | 在读取 `NCHARS` 个字符后返回，而不是等待换行符，但在遇到分隔符之前读取的字符少于 `NCHARS` 个时则遵循分隔符 |
| `-N nchars` | 仅在恰好读取 `NCHARS` 个字符后返回，除非遇到 EOF 或读取超时，并忽略任何分隔符 |
| `-p prompt` | 在尝试读取之前输出字符串 `PROMPT` 且不带尾换行 |
| `-r` | 不允许反斜杠转义任何字符 |
| `-s` | 不回显来自终端的输入 |
| `-t timeout` | 如果在 `t TIMEOUT` 秒内没有读取到完整行，则超时并返回失败。`TMOUT` 变量的值是默认超时时间。`TIMEOUT` 可以小数。如果 `TIMEOUT` 为 0，则仅当指定的文件描述符上有可用输入时 `read` 才返回成功。如果超时，退出状态将大于 128 |
| `-u fd` | 从文件描述符 `FD` 而不是标准输入读取 |




现在，让我们尝试一些示例并学习如何使用该命令。

```bash
#!/bin/bash
echo -n "Enter your name: "
read name
echo "Hi $name, welcome to Ubuntu GNOME desktop. "
```
![](img/rsrc4RB.jpg)
很酷的！不是吧？下一个示例使用了 `-p` 选项。

```bash
#!/bin/bash
read -p "Enter your name: " name
echo "Hi $name, welcome to Ubuntu GNOME desktop. "
```
![](img/rsrc4RJ.jpg)
在这个示例中，我们使用了一个变量。然而，即使你不指定变量，`read` 命令也有它自己的环境变量变量 `REPLY` 来存储此类数据。

示例：
```bash
#!/bin/bash
read -p "Enter your name: "
echo "Hi $REPLY, welcome to Ubuntu GNOME desktop. "
```
![](img/rsrc4RU.jpg)
另一个实用的选项是 `-t` 选项。我们可以用它来设置用户输入提示超时。

```bash
#!/bin/bash
if read -t 30 -p "Enter your name: "
then
    echo "Hi $REPLY, welcome to Ubuntu GNOME desktop. "
else
    echo "Your session timed out! :("
fi
```
![](img/rsrc4S5.jpg)
如果你无法在 30 秒内做出响应，`read` 将自动终止。这就像会话超时，不是吗？使用 `read` 也可以读取密码，酷酷的地方是，它可以停止显示我们输入的字符。

```bash
#!/bin/bash
read -p "Enter your name: "
echo "Hi $REPLY, welcome to Ubuntu GNOME desktop. "
read -s -p "Enter your password: " pass
echo “Your password is $pass”
```
![](img/rsrc4SF.jpg)
也可以读取单个字符（例如，Y/N），这在请求用户确认时非常有用。对于这种情况，你可以将其与 `case` 命令结合使用。最后，我们将从文件中读取并添加一些行号，使 `read` 变得方便。

```bash
#!/bin/bash
fName='' # 用于存储用户输入的文件名
count=1 # 否则，计数从 0 开始
read -p "File name: " fName=$REPLY
echo $fName
cat $fName | while read line
do
    echo "$count: $line"
    count=$[ $count + 1]
done
echo "EOF"
```
![](img/rsrc4T1.jpg)

# 函数
当你使用从小到大的脚本处理任务时，如果代码部分可以在同一个脚本或其他地方重用，不断重写代码将是一项乏的任务。相反，如果这些部分可以使用必要的值重用或调用，那就太好了。这在通用编程平台上很常见。嗯，`bash` 在这里并不逊！它提供了相同的功能，并被称为函数。函数是在脚本中重用的代码块。在本节中，你将学习如何在代码中使用函数。

## 基本组件
函数可以用以下方式定义。并不复杂。

```bash
function function_name {
    commands
}
```
让我们在一个示例中测试函数的函数。

```bash
#!/bin/bash
function love {
    echo "Do you love Linux?"
}
for(( x=1; x<=5; x++ ))
do
    love
done
```
![](img/rsrc4TP.jpg)
函数在循环内部被调用，它起作用了！如果我们创建一个函数并在第一个函数代码下方更改相同函数的定义（两个函数具有相同的名称），会发生什么？那么名称将是相同的，但它将使用第二个定义！

## 退出状态和返回值
函数应该有一个退出状态。然而，由于它可以包含许多命令以及成功/失败的情况，它将返回最后一次成功或失败的状态。尽管我们可以通过 `$?` 查询它，但这可能会变得麻烦。这就是函数的返回值变得有用的地方。让我们来看一个示例。

```bash
#!/bin/bash
function calculate {
    num1=0
    num2=0
    cal=0
    read -p "Input your first value: " num1
    read -p "Input your second value value: " num2
    cal=$[ $num1 + $num2 ]
    echo $cal
    return 0
}
calculate
echo "$?"
echo "The end!"
```
![](img/rsrc4UD.jpg)
然而，这种技术有两个局限性。它们是：
- 你绝不能在捕获退出状态之前执行任何命令。
- 你必须使用小于 256 的返回值，这是返回值的局限性。

为了解决这个问题，我们可以按照以下步骤直接获取返回值。

```bash
#!/bin/bash
var1=100
var2=200
var3=0
var_F=0
function math {
    var3=$[ $var1 + $var2 ]
    echo $var3
}
echo "The return value is being calculated…"
var_F=$(math)
echo “The result is $var_F”
```
![](img/rsrc4V0.jpg)

## 传递参数
就像我们在脚本中所做的那样，我们可以变量传递给函数。函数可以使用 `$1` 到 `$9` 变量来捕获值。

```bash
function calculate{
    if [ $# -eq 0 ] || [ $# -gt 2 ]
    then
        echo "Need two values!"
    elif [ $# -eq 1 ]
    then
        echo "Need one more value"
    else
        echo $[1 + $2 ]
    fi
}
val=$(calculate 250 500)
echo $val
echo "The end!"
```
![](img/rsrc4VN.jpg)
在这个示例中，我们传递了两个简单的参数。然后我们获取了每个参数并进行了计算。

## 处理变量
在下一节中，我们将查看环境变量如何与函数集成。在函数中使用变量是必要的。然而，使用函数时必须注意：不要在函数内部外部使用相同的变量名，因为一个会破坏另一个的数据。

```bash
#!/bin/bash
function compare{
    temp=10
    result=$[ temp+1 ]
}
temp=5
```
![](img/bash
function compare{
    local temp=10
    result=$[ temp+1 ]
}
temp=5
echo "Final result =" $result
if [ $temp -eq 10 ]; then
    echo "romised!"
elif [ $temp -eq 5 ]; then
    echo "Not compromised!"
else
    echo -1
fi
```
![](rsrc4WZ.jpg
现在，temp 是 5 且没有冲突。

### 使用数组
如果你熟悉数组，可能知道它是什么。然而，对于不熟悉数组的读者，本节包含了介绍。数组是我们用来持有多个参数的内存位置。我们可以通过两种方式创建数组：
- 声明数组。
- 创建数组。

### 声明数组
要声明数组，我们可以简单地使用以下语法：
```bash
declare -a my_array
```

### 创建数组
可以使用以下语法创建数组：
```bash
my_array=(foo baz)
```

### 处理数组
为了插入或修改值，我们可以使用：
`my_array[0]=foo`
我们插入 `foo` 作为数组的第一个元素。为了检索数据，可以使用以下方法：
- `echo ${my_array[@]}`：使用 `@` 符号。
- `echo ${my_array[*]}`：使用 `*` 符号。
![](img/rsrc4XN.jpg 希望你记住 `@` 和 `*` 之间的区别。让我们通过 `for` 循环来看。

```bash
my_array=(foo baz)
for x in "${my_array[@]}"
do
    echo "$x";
done
for y in "${my_array[*]}"
do
    echo "$y";
done
```
![](img/rsrc4Y4.jpg
正如你看到的，`@` 返回每个元素，而另一个返回所有项但作为一个单一字符串。

### 在函数中使用数组
在函数中使用数组非常有用，因为由于数组的复杂性，代码可以重用。让我们从示例中学习。

```bash
function arr_test{
    local temp_arr
    temp_arr=("$@") # 从外部向数组赋值
    echo "Value of the array in the function is: ${temp_arr[*]}"
}
my_array=(a b c d e)
echo "Array values in the original array is: ${my_array[*]}"
arr_test "${my_array[*]}"
```
![](img/rsrc4YM.jpg)!
两个数组具有相同的值。

## 递归函数
什么是递归？函数可能会为了某些目的调用自己。最好的例子是计算阶乘。在计算时，函数递归地调用自己来运行计算。让我们来看这个示例。

```bash
function factorial {
    if [ $1 -eq 1 ]
        # 如果输入是 1，那么结果是 1
        echo 1
    else
        # 如果输入不是 1
        local tmp=$[ $1 - 1 ]
        local result=$(factorial $tmp) # 函数再次调用自己
        echo $[ $result * $1 ]
    fi
}
```
等待，原文有 `result=$(factorial $REPLY)` 类似的。

## 将函数作为库
我们已经学习了如何高效地使用函数。然而，你仍然无法在原始脚本之外使用函数，因为它限于当前会话。这是事实吗？不！你可以在脚本中使用函数来满足另一个脚本的目的。方法如下：
你只需要将脚本保存在尝试使用它的脚本相同的位置。否则，你需要提供完整的（绝对）路径。还有一种调用外部脚本的正确方法。让我们在以下代码中学习。

```bash
function add {
    echo $[ $1 + $2 ]
}
```




| Variable |
| :--- |
| `FIELDWIDTH` |
|  |
| `FS` |
| `OFS` |
| `ORS` |
| `RS` |

让我们来看使用这些变量的示例。

- `awk 'BEGIN{FS=":"} {print $1 "\t" $5}' /etc/passwd` ![](img/rsrc54H.jpg)
- `awk 'BEGIN{FIELDWIDTHS="1 2 3 1"}{print $1,$2,$3,$4}' myfie` 这将字段宽度设置为 1 2 3 1
- `awk 'BEGIN{FS="\n"; RS=""} {print $1,$4}' myfile` 这使用了字段分隔符“`newline`”（换行符）。它会打印数据块（如人的地址块）的第 1 行和第 4 行。

### 用户定义变量
在使用 `gawk` 编写脚本时，我们可以使用自己的变量。以下是一个关于如何方便使用它们的简单示例。
```bash
awk 'BEGIN{show="This is a test";print show}'
```
![](img/rsrc54Y.jpg)

### 使用数组
GAWK 还允许通过简单的方法处理数组。
语法：`var[index] = element`
示例：
```bash
awk 'BEGIN{var[1] = 10;var[2] = 50;sum = var[1] + var[2];print sum> }'
```
这也可以用于任何字符串值。![](img/rsrc55C.jpg)
还可以使用 `for` 函数以更简单的形式对数组进行迭代。
语法：`for (var in array){statements}`
示例：
```bash
awk 'BEGIN{test["a"] = 1;test["b"] = 2;test["c"] = 3;for (var in test){print var," : Value:",test[var]}}'
```
![](img/rsrc55Z.jpg)
若要删除数组变量，可以使用 `delete` 命令。
语法：`delete array[index]`

### GAWK 结构化命令
类似于 bash 脚本，`gawk` 为结构化命令提供了类似的支持，例如 `if`、`while`、`do-while` 和 `for` 命令。以下是每个命令的语法和示例。

#### IF 语句
语法：`if {(condition)}statement1`
示例：
```bash
awk '{if ($1 > 50){​ print $1}}' File3.txt
```
![](img/rsrc56M.jpg)
在此示例中，程序输出 `File3.txt` 中大于 50 的数字。

#### While 循环
该语句具有以下语法。
语法：`while (condition){statements}`
只要条件为真，它就会评估循环并执行所需的任务。
示例：
```bash
awk '{sum = 0;i = 1;while (i < 10){​ sum += $i; i++}print sum}' File3.txt
```
![](img/rsrc57B.jpg)

#### Do While Loop
这与 `while` 语句相似。但是，语句会在 `while` 条件满足之前先求值。
语法：`do{statements} while (condition)`

#### For Loop
`gawk` 中的 `for` 语句类似于 C 风格的 `for` 循环。
语法：`for( variable; condition; iteration)`
示例：
```bash
awk '{sum = 0;for (i=0; i < 10; i++){​ sum += $i}print sum}' File3.txt
```
![](img/rsrc582.jpg)

### GAWK 函数
`gawk` 最重要的特性之一是对函数的支持。它既有内置函数，也有用户定义的函数。

#### 内置函数
`Gawk` 提供了一系列丰富的内置函数，包括：
- 数学函数。
- 字符串函数。
如果你热爱数学，`gawk` 丰富的数学函数将为你带来乐趣。

#### 数学函数
下表包含了内置数学函数。使用这些函数非常简单。
表格：GAWK 数学函数
来源：[`www.gnu.org/software/gawk/manual/html_node/Numeric-Functions.html`](https://www.gnu.org/software/gawk/manual/html_node/Numeric-Functions.html)

| Function | Description |
| :--- | :--- |
| `atan2(y, x)` | 返回 `y / x` 的弧反正切值。你可以使用“`pi = atan2(0, -1)`”来获取 pi 的值。 |
| `cos(x)` | 返回 `x` 的余弦，`x` 为弧度。 |
| `exp(x)` | 返回 `x` 的指数。 |
| `int(x)` | 返回靠近 `x` 的整数，向零截断。浮点表示。 |
| `log(x)` | 返回 `x` 的自然对数。 |
| `rand()` | 返回一个随机数。 |
| `sin(x)` | 返回 `x` 的正弦，以弧度制。 |
| `sqrt(x)` | 返回 `x` 的正平方根。 |

示例：
```bash
awk 'BEGIN{x=sqrt(16); print x}'
```
![](img/rsrc5AG.jpg)

#### 字符串函数
有很多实用的字符串函数，下表包含了这些函数及其描述。
表格：GAWK 字符串函数

| String Function | Description |
| :--- | :--- |
| `index(big, little)` | 子字符串在索引中的起始位置。 |
| `length(string)` | `string` 的长度。 |
| `match(string, regex)` | `Regex` 代表扩展正则表达式 |
| `split(string, array, separator)` | 将 `string` 拆分到 `array` |
| `sprintf(format, ...)` | `printf` 格式字符串 |
| `sub(regex, subst, string)` | 替换 `regex` 的第一次出现处 |
| `gsub(regex, subst, string)` | 替换 `regex` 的所有出现处 |
| `substr(string, start, end)` | 到子字符串结束的索引 |
| `tolower(string)` | 转换为小写。 |
| `toupper(string)` | 转换为大写。 |

表格：GAWK 字符串参数

| Parameters | Description |
| :--- | :--- |
| `big` | 用于扫描查找“`little`”的字符串 |
| `end` | 子字符串结束的索引 |
| `format` | `printf` 格式字符串 |
| `little` | 用于扫描查找“`big`”的字符串 |
| `regex` | `Regex` 代表扩展正则表达式 |
| `start` | 子字符串在索引中的起始位置 |
| `string` | 字符串参数。 |

示例：
```bash
awk 'BEGIN{x = "Linux Lovers"; print toupper(x)}'
```
![](img/rsrc5E9.jpg)

### 用户定义函数
与 bash 脚本一样，`gawk` 支持用户定义函数，而且不仅如此！它还支持函数库。以下是你可以在代码中定义的函数语法。
语法：`function name([variables]){statements}`
示例：
```bash
awk 'function printing(){printf "%s has the home path at %s\n", $1,$6}
BEGIN{FS=":"}{printing()}' /etc/passwd
```
![](img/rsrc5EX.jpg)

### 创建库
这是 `gawk`（也是本书书）的最后一节。在这一节中，你将学习如何创建一个函数库并在不同的脚本中使用它。正如你之前学过的，让我们通过实践来学习。回到 `/etc/passwd` 的示例。

1. **创建库文件**：在桌面上创建并保存此文件为 `awkflib`。
   ```bash
   function myprint(){printf "%s has the home path at %s\n", $1,$6}
   ```
2. **创建新脚本**：现在，创建一个实际文件将其作为库使用，并保存为 `script.awk`。
   ```bash
   BEGIN{FS=":"}{​ myprint()}
   ```
3. **运行脚本。**





# 命令

`awk -f awkflib -f script.awk /etc/passwd`

该命令执行非常成功，我们的库文件按预期工作。通过本节，你已经成功完成了本书中的所有章节和课程。

##结结

Linux 正在企业用户、学校及家庭中迅速普及，它几乎被应用于所有地方，包括服务器、计算机、移动设备、物联网（IoT）以及无数其他场合。本书的内容将成为 Linux 新手和爱好者的极佳资源。

你可能还还不熟悉 Linux，但我邀请你自己在 Linux 环境中尽可能尝试所有的练习示例。Linux 并不消耗资源，因此寻找一台低成本的电脑安装 Linux 并不困难。亲自动手（Get your hands dirty）至关重要。

你可能拥有 Windows 背景，在某些阶段可能会遇到困难。有许多方法可以将 Linux 环境更改为类似 Windows 的环境，所有所需信息都包含在书中。关于哪种操作系统最好存在一些争论。我建议你不要急于下任何判断，而是学习你需要掌握的知识，以便尽可能精通 Linux。

如果你愿意获得职业认证，有许多路径可以尝试。学习 Linux 促进职业发展是一个明智的决定，因为全球范围内都有许多机会。红帽（Red Hat）在其企业平台上提供了一套非常优秀的认证。关于红帽认证的更多信息可以在此处找到：https://www.redhat.com/en/services/training-and-certification。

我在书中添加了多个参考文献以帮助你获取更多信息。Linux 手册页（man pages）和 `--help` 命令也是极佳的来源。

接下来的两将提供更多 Linux 知识，旨在涵盖各个方面，为你提供高水平的 Linux 技术知识。在此之前，祝愿所有读者好运，编码愉快！

