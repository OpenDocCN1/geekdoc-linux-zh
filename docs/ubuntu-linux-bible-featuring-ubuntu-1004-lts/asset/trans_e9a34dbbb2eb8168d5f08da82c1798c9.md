

## 第一部分：Ubuntu 入门

## 笔记本电脑/MID 用户

笔记本电脑无疑是目前最热门的计算平台之一，它们提供了低成本、足够的使用性能和网络就绪性的惊人组合。另一个日益流行且可用性不断提高平台是移动互联网设备（MID）系统，它们是无线手持设备，通常配备触摸屏而非键盘。有几种针对此类系统的 Ubuntu 发行版都已针对其较小的屏幕、网络导向以及音频/视频能力进行了优化：

- * *EasyPeasy*：一种基于 Ubuntu 的发行版，现在支持各种笔记本电脑。更多信息请访问 www.geteasyasy.com，包括下载和安装说明的链接。

- * *Kubuntu 笔记本电脑版*：一种基于 Ubuntu 的发行版，将最新的 KDE 4 桌面强大功能引入笔记本电脑平台。更多信息请访问 https://wiki.ubuntu.org/Kubuntu/Netbook，包括下载和安装说明的链接。

- * *Ubuntu 移动互联网设备 (MID) 版*：一种最初由 Canonical 与 Intel 合作开发的基于 Ubuntu 的发行版。Ubuntu Mobile 在 Intel MID 上的地位已很大程度上淡出，转而支持 Moblin 项目（www.moblin.org），这是一个 Linux 基金项目，目前正与 Intel 直接合作。关于 Ubuntu Mobile 的更多信息请访问 www.ubuntu.com/products/mobile。Canonical 对 MID 的关注已稍微转向针对基于 Intel 的笔记本电脑和 MID 的 Ubuntu Remix，以及针对使用 ARM 处理器（www.arm.com）的笔记本电脑和 MID 的 Ubuntu Desktop 版（www.ubuntu.com/products/whatis/ubuntu）。

- * *Ubuntu 笔记本电脑混合版 (UNR)*：由 Canonical 提供的官方 Ubuntu 版本，提供了针对笔记本电脑和 MID 较小屏幕优化的定制用户界面。UNR 是我最喜欢的面向笔记本电脑的、基于 Ubuntu 的发行版。更多信息请访问 www.canonical.com/projects/ubuntu/unr，包括下载和安装说明的链接。

便携式、网络感知和小型足迹的系统正越来越受欢迎，我确定会有更多针对此类系统的基于 Ubuntu 发行版出现。

## 服务器用户

虽然可以在桌面 Linux 系统上运行如邮件系统、Web 服务器、DNS 服务器、打印服务器和文件服务器等服务器应用程序，但在企业或学术环境中，这通常是错误的做法。许多服务器是精简且高效的命令行导向机器，它们将所有可用周期都分配给运行的服务器进程，而不是通过运行 GUI（至少默认情况下如此）来“浪费”它们。Canonical 提供了 Ubuntu Server，该版本将 Ubuntu Linux 的强大、稳定易于管理的特性引入服务器机房。默认情况下，Ubuntu Server 提供了一个基础且安全的系统，没有开放的网络端口，但你可以在系统中安装其他基础配置，例如 LAMP（Linux、Apache、MySQL 和 Perl），这些关键服务器组件已预配置协同工作，从而最大限度地减少你的安装和管理工作。服务器版还提供对 LTSP（Linux 终端服务器项目）的开箱支持，它支持瘦客户端并使一个服务器系统能够满足许多轻级桌面系统的存储和应用需求。Ubuntu 服务器版默认不安装图形用户界面，但标准的 GNOME 桌面（或你选择的 X 窗口管理器）可以作为软件包手动安装。有关 Ubuntu Server 版的更多信息或若要下载副本，请访问 www.ubuntu.com/products/whatubuntu/serveredition。

Canonical 曾提供过名为 JeOS 的 Ubuntu 服务器版，旨在作为设备运行虚拟机。JeOS 代表“恰合适的操作系统”（Just Enough Operating System），意味着 JeOS 针对小磁盘、最小足迹和最小资源消耗进行了优化，将尽可能多的服务器硬件留给虚拟机使用。JeOS 现在是一个与 Ubuntu 服务器版发行版捆绑的优化内核。有关 JeOS 的更多信息，请访问 www.ubuntu.com/products/whatubuntu/serveredition/jeos。有关 Ubuntu 上的虚拟化更多信息，请参阅第 24 章。

## 安装要求

随着 Linux 发行版迁移到 2.6 内核，且 Linux 变得越来越流行，你的硬件不受 Ubuntu 支持的概率变得越来越小。本节概述了 Ubuntu 支持的系统类型以及运行可用系统的通用硬件要求。

## 注意事项

Linux 的优点之一是它支持广泛的系统类型。大多数 Linux 发行版（包括 Ubuntu）可以在那些本会被丢弃或当作门垫的旧系统上运行。在旧系统上运行时，你可能希望使用命令行界面或更轻量的环境。为了测试，我使用一个具有完全这些特征的系统（一台我不忍舍手的旧 IBM ThinkPad 380XD），GNOME 在上面运行起来非常痛苦。如果你确实需要在此类系统上运行 Ubuntu，请参阅本节前面的关于低速和低内存系统替代图形环境的说明。

## 支持的系统类型

Ubuntu 支持以下任何设备：

- Intel、AMD 的 i386 或兼容处理器
- 基于 ARM 的系统。ARM 是低功耗、高性能 CPU，在嵌入系统中非常流行，包括各种厂商的笔记本电脑。有关 ARM 的详细信息见 www.ubuntu.com/products/whatubuntu/arm。
- 64 位 AMD、Intel 64 处理器（包括 Athlon 64、Opteron 和 Xeon）

## 注意事项

Canonical 曾正式支持 PowerPC (PPC) 处理器（如用于 Macintosh 计算机系统的处理器），涵盖 Ubuntu 6.10 到 7.10 发行版。这意味着 PPC 和 UltraSPARC 版本的 Ubuntu 变成了社区支持的发行版。这意味着 Canonical 可能仍产生某些问题，且所有的 Ubuntu 下载站点可能无法提供某些版本。关于 PPC 的更多信息，请访问 https://wiki.ubuntu.com/PowerPCFAQ。

## 硬件要求

对于任何计算机软件，如果你在你最强大的系统上安装和使用 Ubuntu，将获得更好的体验，但从技术上讲，Ubuntu 仍然可以在你的 25 MHz i386 上（缓慢地）运行。然而，美国的国家格言在这里非常适用：“多比越好”。暂时放下我对比 Linux 的偏好，你不应该真的去尝试在一个运行速度低于 166 MHz 或内存小于 96 MB 的系统上安装和运行 Ubuntu。

安装 Ubuntu 并获得合理用户体验的最低硬件要求如下：

- 700 MHz 或更快的处理器
- 384 MB 内存
- CD-ROM 驱动器
- 以太网接口
- 支持 1024x768 分辨率的 VGA 接口
- 8 GB 可用磁盘空间

## 注意事项

如果你想使用 Ubuntu 的组合和高级视觉效果功能，你应该至少拥有 1.2 GHz 的处理器以及最近的 ATI、Intel 或 NVIDIA 显卡。

> 如果你的系统满足或超过这些要求，就可以开始。针对笔记本电脑和 MID 设备的定制发行版有不同的要求，例如使用 U 盘而非 CD-ROM 驱动器。你确实可以在较慢的系统上安装 Ubuntu

