
还有其他基于 Ubuntu 的发行版可用，但这里没有在这里列出，是因为我实际上没有机会尝试过它们，或者它们似乎没有得到任何机构的支持。我没有列出包含 Friespee（Linuxspin 的社区版本，`www.freespee.org/`）、Linuxspin（`www.linuxspin.org/`）、MEP（`www.mepis.org/`）、Sabayon（`www.sabayon.org/`）等其他 Ubuntu 软件包的独立发行版。我也没有列出那些仅为现有 Ubuntu 安装添加特定软件包集的脚本类“发行版”。如果我漏掉了某个你喜欢的可安装、即插即用的基于 Ubuntu 的发行版，请告诉我。我也总是乐意学习。

### 服务器用户

虽然可以在桌面 Linux 系统上运行邮件服务器、Web 服务器、DNS 服务器、打印机和文件服务器等服务器应用程序，但在企业或学术环境中，这通常不是正确做法。许多服务器系统是精简且高效的命令行机器，将所有可用周期都分配给正在运行的服务器进程，而不是通过运行 GUI（至少默认如此）来“浪费”它们。Ubuntu 提供了针对两个发行版：

- Ubuntu Server 版：Ubuntu 的版本，将 Ubuntu Linux 的强大、稳定易于管理引入服务器机。默认情况下，Ubuntu Server 版提供了一个基础、安全的系统，没有任何开放端口，但你可以安装其他基础配置，例如 `LAMP`（Linux、Apache、MySQL 和 Perl）系统，这些关键组件已预配置好工作，从而最大限度地减少你的安装和管理工作。服务器版还提供对 `LTSP`（Linux 服务器项目）的开箱即用支持，它支持瘦客户端，并允许一个服务器系统满足许多轻量级桌面的存储和分配需求。Ubuntu Server 版默认不安装图形界面，但标准的 `GNOME` 桌面（或你选择的 X 窗口管理器）可以作为软件包手动安装。更多关于 Ubuntu Server 版的信息或下载副本，请访问 `www.ubuntu.com/products/ubuntu-server`

- * Ubuntu Server Edition, JeOS：一种旨在运行虚拟机的服务器的 Ubuntu 版本。`JeOS` 代表“恰够的操作系统”（Just Enough Operating System），意味着它针对小设备、低内存占用和极少资源消耗进行了优化，将尽可能多的服务器硬件留给虚拟机。遗憾的是（除非你是 VMware 主机），`JeOS` 是针对 VMware 虚拟化解决方案（`www.vmware.com`）进行优化的，在我看来这并不是最好的虚拟化解决方案。我怀疑 `JeOS` 将证明 Xen、KVM 等更复杂的虚拟化解决方案非常有用。更多关于 `JeOS` 的信息或下载副本，请访问 `www.ubuntu.com/products/ubuntu-server/jeos`。虚拟机与模拟器。

### 特殊平台

Canonical 宣布了一个名为 Ubuntu 移动互联网设备 (MID) 的发行版，旨在为移动互联网设备（MID）的开发者带来 Ubuntu 的强大功能、可管理性和灵活性，MID 是具有全网络支持的类平板触摸屏。开源软件和 Ubuntu 社区的数百万开发者是嵌入式系统开发的巨大资源，且硬件供应商正在积极开发 MID 硬件。

最初计划于 2007 年 10 月发布，该发行版的第一个版本基于 2008 年 4 月的 Ubuntu 8.04 Hardy Release。更多关于基于 Ubuntu 的发行版的信息，请访问 `www.ubuntu.com/products/mobile`。要安装此发行版的实例，请访问 `http://image.ubuntu.com/releases/hardy`。该站点提供了 MID 的 `KVM`（内核虚拟机）镜像，可以在运行 `KVM` 的 Ubuntu 或 Ubuntu 系统上作为虚拟机运行。（有关 `KVM` 的更多信息请参见附录 7。）该站点还提供适用于 Maclin 和 Melton MID 平台的 MID 安装镜像（分别是 Intel 2007 年和 2008 年代的原型 MID 硬件）。

### 安装要求

随着 Linux 发行版迁移到 2.6 内核，并且 Linux 的日益增长，出现 Ubuntu 不支持硬件的概率越来越小。本节概述了 Ubuntu 支持的系统类型，以及可用系统的通用硬件要求。

# Ubuntu Linux 项目

Linux 的优点之一是它支持极其广泛的系统。大多数 Linux 发行版（包括 Ubuntu）都能运行在那些本会被丢弃或用作桌面的旧系统上。然而（你可以随意引用这一句），软件在旧硬件上的运行速度会较慢。在旧系统上运行时，你可能希望使用命令行界面或比默认 `GNOME`（或 Ubuntu 的 `KDE`）更轻量级的图形环境。如 `Xf` 等桌面或如 `Fluxbox` 和 `iCeWM` 等窗口管理器是 `GNOME` 和 `KDE` 流行且强大的替代方案。更多关于这些信息，请参阅第 5 章中“什么是桌面！Linux 图形环境”部分。

### 支持的系统类型

Ubuntu 和 Kubuntu 支持以下任何类型的系统：

- `i386` 或兼容处理器（Intel、AMD 等）

- 64 位 `AMD` 或 `EM64` 处理器（包括 Ath64、Opteron 和 Xeon）

Ubuntu 官方支持 PowerPC (`PPC`) 处理器（如用于 Mac 系统），直到 Ubuntu 6.10 版本。Ubuntu 曾官方支持 UltraSPARC 平台，这意味着 Canonical 可能仍会制作这些版本，但 PPC 或 SPARC 特有的问题不会阻碍官方 Ubuntu 发布，且这些平台的 Ubuntu 版本可能在 Ubuntu 下载网站上不可用。访问 `https://wiki.ubuntu.com/PowerPCFAQ` 获取 PPC Ubuntu 发行版的信息。

### 硬件要求

对于任何计算机软件，如果你在最强大的系统上使用和安装 Ubuntu，将获得更好的体验，但 Ubuntu 和 Kubuntu 技术上确实可以在你的 25 MHz `i386` 上运行（尽管很慢）。然而，美国那句谚语在这里完全适用：“越多越好”。对于你的 liveusb 来说，你最好在一个处理器运行速度低于 166 MHz 或内存小于 90 MB 的系统上尝试安装和运行 Ubuntu（一台我实在舍不得的旧 IBM ThinkPad SR38XD），如果你真的需要在这样的系统上运行 Ubuntu，可以使用 Xubuntu。

安装 Ubuntu 或 Kubuntu 并获得合理用户体验的最小硬件要求如下：

- 700 MHz 或更好的处理器

- 384MB 内存

- CD 驱动器

- 以太网接口

- 能够支持 1024 × 768 分辨率的 VGA 图形接口

- 3GB 可用磁盘空间

# 第一部分：从 Ubuntu 和 Kubuntu 开始

如果你想使用 Ubuntu 或 Kubuntu 的合成效果和高级视觉效果，你至少需要一个 1.2 GHz 的处理器以及一张较新的 ATI、Intel 或 NVIDIA 显卡。

如果你的系统配置满足或超过了这些要求，你就可以开始了。你完全可以在速度较慢或内存较小的系统上安装 Ubuntu 或 Kubuntu，但这就像在现代汽车上装上赛车光光胎——你将无法获得最佳的体验。

### 时间要求

安装 Ubuntu 或 Kubuntu 所需的时间取决于你的系统速度、你如何配置它，以及你正在安装的发行版类型。如果你要在运行 Microsoft Windows、Solaris 或 Mac OS X 的笔记本电脑上安装 Ubuntu 或 Kubuntu，并将其设置为双启动系统，这可能需要一到两个小时。在新机器上安装任何版本的 Ubuntu 或 Kubuntu 都可能少于一小时。通常情况下，你应该花费一到两个小时来安装 Ubuntu 或 Kubuntu —— 如果时间比这更短，你也不会抱怨的：

### Ubuntu 光盘

随书附的 DVD 是 Ubuntu Desktop DVD，它允许你在不改变现有计算机系统任何内容的情况下测试 Ubuntu，并提供了一个简单、易用的安装程序，让你能够将 Ubuntu 永久安装到你的系统中。Ubuntu 有三种不同的光盘可用，它们提供的功能如下：

- **Desktop DVD：** 本书附带的 DVD 提供可启动的 Ubuntu，允许你可以在不改变现有计算机系统任何内容的情况下运行和尝试 Ubuntu。此 DVD 被称为“Live DVD”，还包含一个易用的图形化安装程序，可以让你轻松地在计算机系统上永久安装 Ubuntu。最后，DVD 还包含一个特殊的安装程序，你可以用它在不重新划分磁盘的系统中安装并使用 Ubuntu。有关使用此 DVD 的信息，请参阅第 2 章“安装”。

- **Server CD：** 网站提供了与 Ubuntu Desktop DVD 等效的镜像，它支持相同的功能（Live CD 或 DVD，Ubuntu 和 Kubuntu），但使用的是 KDE 桌面环境和基于 KDE 的应用程序。
