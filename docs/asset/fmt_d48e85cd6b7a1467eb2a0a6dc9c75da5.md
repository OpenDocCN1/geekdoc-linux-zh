
# 第一部分：Ubuntu 入门

## 第一章：Ubuntu Linux项目

- EasyPeasy：一个基于 Ubuntu 的发行版，最初专注于华硕 EeePC 笔记本电脑，现在支持广泛的笔记本电脑。请访问 www.gteasypeasy.com 获取更多信息，包括下载链接和安装说明。

- Kubuntu Netbook：一个基于 Ubuntu 的发行版，为笔记本电脑平台带来了最新的 KDE 4 桌面。请访问 https://wiki.kubuntu.org/Kubuntu/Netbook 获取更多信息，包括下载和安装链接。

- Ubuntu 移动互联网设备 (MID)：一个最初由 Canonical 与同 Intel MIDs 合作，为了支持 Moblin 项目（www.moblin.org）而开发的基于 Ubuntu 的发行版。该 Moblin 项目是 Linux 基金会的一个项目，目前正与 Intel 合作。请访问 www.ubuntu.com/products/mobile 获取有关 Ubuntu Mobile 的信息。Canonical 的 MID 已很大程度上转向了针对 Intel 架构笔记本电脑的 Ubuntu Remix，以及针对 ARM 架构的 Ubuntu Desktop。对于使用 ARM 处理器的笔记本电脑，请访问 www.ubuntu.com/whatisubuntu/ubuntu-arm。

- Ubuntu Netbook Remix (UNR)：由 Canonical 提供的官方 Ubuntu 版本，提供了一个针对笔记本电脑小屏幕优化的定制用户界面。UNR 是我最喜欢的面向笔记本的基于 Ubuntu 的发行版。请访问 www.canonical.com/ubuntu/unr 获取更多信息，包括下载链接和安装说明。

便携式、网络感知和小型足迹系统仍在日益流行，还将许多其他针对此类系统的基于 Ubuntu 的发行版出现。

### 服务器用户

虽然可以在桌面版 Linux 上运行邮件系统、Web 服务器、DNS 服务器、打印服务器和文件服务器等服务器级应用，但在企业或学术环境中，这通常是错误的做法。许多服务器系统都是精简且高效的，是以命令行为主的机器，它们将所有可用周期都分配给正在运行的服务器进程，而不是通过使用 GUI（至少默认情况下如此）来“浪费”它们。对于服务器系统，Canonical 提供了 Ubuntu Server 版，这是一个将 Ubuntu 的强大、稳定易于管理引入服务器的 Ubuntu 版本。

默认情况下，Ubuntu Server 版开箱即支持 LTSP（Linux 终端服务器项目），支持终端客户端并允许一台服务器满足应用程序需求。Ubuntu Server 版默认不安装图形界面，但可以作为包手动安装标准的 GNOME 桌面（或 KDE for Ubuntu）。欲需更多关于 Ubuntu Server 版的信息或下载副本，请参阅 www.ubuntu.com/products/whatubuntu/serveredition。

Canonical 曾提供过名为 Jeos 的 Ubuntu Server 版，旨在运行虚拟。Jeos 的意思是“足够操作系统”，意味着 Jeos 针对小型磁盘和内存占用以及最小资源消耗进行了优化，为虚拟机留出尽可能多的硬件。Jeos 是与 Ubuntu 服务器发行版捆绑的优化内核。有关 Jeos 的更多信息请访问 www.ubuntu.com/products/whatubuntu/serveredition。关于 Ubuntu 虚拟化的更多信息请见第 24 章。

### 安装要求

随着 Linux 发行版迁移到 2.6 内核且 Linux 变得越来越流行，Ubuntu 不支持的硬件越来越少。本节概述了 Ubuntu 系统类型以及通用硬件要求。

#### 注意

Linux 的优点之一是支持的系统类型广泛。大多数 Linux 发行版（包括 Ubuntu）都能运行在那些会被放弃作为桌面系统的设备上。然而（你可以尽管重复这句话），软件在较慢的硬件上运行也较慢。在其他系统上运行时，你可能希望使用命令行界面或轻量级图形环境，而不是默认的 GNOME（或 KDE for Ubuntu）桌面。如 Xfce 等桌面或 Fluxbox、IceWM 等窗口管理器是 GNOME 和 KDE 流行且强大的替代方案。请参阅第 5 章的“什么是桌面？Linux 图形环境”章节获取更多信息。

#### 支持的系统类型

Ubuntu 支持以下一类系统：

- Intel、AMD 等 i386 或兼容处理器

- ARM 架构系统。ARM 处理器是低功耗、高性能 CPU，在嵌入式系统（包括各种厂商的笔记本电脑）中非常流行。欲获取特定平台的详细信息请访问 www.ubuntu.com/products/whatubuntu/arm。

- 64 位 AMD、Intel 64 和 EM64T 处理器（包括 Athlon 64、Opteron 和 Xeon 64MTT）

##### 注意

Canonical 直到 Ubuntu 6.10 版本才开始正式支持 PowerPC (PPC) 处理器（例如用于许多 Macintosh 电脑系统中的处理器）。同样，Canonical 此从 Ubuntu 6.10 到 7.10 发行版中也正式支持了 UltraSPARC 处理器。此后，Ubuntu 的 PPC 和 SPARC 版本变为了社区支持的发行版。Canonical 可能仍会制作这些版本，但针对 PPC-SPARC 的特定问题将不会阻塞官方 Ubuntu 版本的发布，而且针对这些平台的 Ubuntu 版本可能无法在所有 Ubuntu 下载站上获得。有关 PC 版本的 Ubuntu 发行版的更多信息，请参阅 https://wiki.ubuntu.com/PowerPCFAQ 中的 Ubuntu 常见问题。

#### 硬件要求

对于任何计算机软件，如果你在最强大的系统上安装和运行 Ubuntu，将获得更好的体验；但从技术上讲，Ubuntu 在你那台落满灰尘的 25 MHz Pentium 上也能运行良好（尽管速度很慢）。然而，美国的国家格言说得非常有道理：“越多越好”。就我个人而言，你可能真的应该尝试在处理器运行速度低于 166 MHz 或内存小于 96 MB 的系统上安装并运行 Ubuntu。我曾用一个具有这些特征的系统进行测试（一台我不忍心丢的旧 IBM ThinkPad 38XD），当时 GNOME 的运行简直极其痛苦。如果你确实需要在此类系统上运行 Ubuntu，请查看本节早些关于低速和低内存系统的替代图形环境的说明。

安装 Ubuntu 并获得合理用户体验的最低硬件要求如下：

- 700 MHz 或更快的处理器

- 384 MB 内存

- CD-ROM 光驱

- 以太网接口

- 支持 1024x768 分辨的 VGA 图形接口

- 8 GB 可用磁盘空间

##### 注意

如果你想使用 Ubuntu 的合成和高级视觉效果功能，你应该至少拥有 1.2 GHz 的处理器以及最近的 ATI、Intel 或 Nvidia 显卡。

如果你的系统满足或超过这些要求，你就可以运行了。针对网络级电脑和 MID 设备等特定平台的定制发行版有不同的要求，例如需要 USB 闪盘而非 CD-ROM 光驱。你可以在较慢或内存较小的系统上安装 Ubuntu，但那就像在现代上装上赛光胎——你并无法真正获得最佳体验。

### 时间要求

安装 Ubuntu 所需取决于系统类型、你如何配置该系统以及你正在安装的发行类型。在运行 Microsoft Windows、Solaris 或 Mac X 的笔记本电脑上安装 Ubuntu 并设置双启动系统，可能需要一到两个小时。在新机器上安装任何版本的 Ubuntu 可能不到一小时。通常情况下，你应该计划花费一两个小时来安装 Ubuntu —— 我假设如果时间更短，你不会抱怨的。

### Ubuntu CD

随书附的光盘是 Ubuntu 桌面 CD，它可以让你在不更改任何内容的情况下在现有电脑系统上测试 Ubuntu，并提供了一个简单易用的安装程序，让你可以将 Ubuntu 永久安装到该系统上。Ubuntu 有三种不同的 CD。这些 CD 及其提供的功能如下：

- 桌面 CD：随书附的 CD 提供了一个可启动的 Ubuntu Linux 版本，让你可以在不更改现有系统任何内容的情况下运行和尝试 Ubuntu。此 CD 被称为 Live DVD，还包含一个易于使用的图形化安装程序，让你轻松地在电脑系统上永久安装 Ubuntu。最后，它还包含一个特殊的安装程序，你可以用它在运行 Microsoft Windows 的系统上安装并使用 Ubuntu，无需重新分区。有关使用此 CD 的信息，请参阅第 2 章。

##### 注意

当你从任何 CD 运行程序时，你所做的工作、创建的文件等会在重启电脑系统时丢失，除非你将其保存到网络或其他系统或可移动存储设备（如 USB 闪盘、移动硬盘等）。请参阅第 2 章中的“使用 CD 持久化”部分，了解使用 USB 闪盘或自动保存并恢复从 Ubuntu Desktop DVD 运行时的更改；或者参阅第 2 章中的“从桌面 CD 访问文件”和“通过网络向其他机器复制文件”章节，了解如何在运行 Ubuntu CD 时手动保存你的工作。
