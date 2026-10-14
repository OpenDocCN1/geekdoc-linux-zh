
- **DistroWatch (http://distrowatch.com/table.php?distribution=ubuntu):** 该网站提供有关大多数 Linux 发行版（包括 Ubuntu）内容的摘要信息。他们的 Ubuntu 页面提供了有关各种 Ubuntu 版本内容的高层信息，但更重要的是提供了指向许多 Ubuntu 相关网站的链接、对各种 Ubuntu 版本的评论以及更多内容。如果你不熟悉 DistroWatch，它是查找几乎任何 Linux 相关信息的必备 Linux 网站。

- **Ubuntu Blog (http://ubuntu.com/):** 这是一个关于 Ubuntu 的博客，提供了大量关于通用 Ubuntu 任务的条目，这些条目被分为管理、办公室、服务器等类别。它还包含指向其他网站的链接以及很棒的特定任务文章，例如在 Ubuntu 系统上运行 MythTV 软件包的最佳说明。

- **UbuntuGuide (http://ubuntuguide.org):** 该网站是一个 Ubuntu“入门”指南，是一份极佳的信息资源，尽管它可能并不总是反映最新的 Ubuntu 版本。该网站提供了大量关于如何在 Ubuntu Linux 上执行特定任务的详细信息，非常值得一看。

- **Ubuntu Women (www.ubuntu-women.org):** 该网站提供常见问题解答、wiki、博客和导师计划，专注于让更多女性参与 Ubuntu 以及通用的 FLOSS（自由/许可/开源软件）。这是一个具有伟大信息和宗旨的优秀网站，通过它我们都能受益。

- **Ubuntu (www.ubuntu.org):** 该网站是一个 Ubuntu 用户社区，提供了各种论坛、博客、关于 Debian 和 Ubuntu 的最新文章链接，以及旨在帮助用户使用 Ubuntu 的各种资源。论坛特别出色，涵盖了从开始使用 Ubuntu 到特定定制和优化任务的各个主题。Ubuntu 还针对针对基于 Ubuntu 的发行版，如 Kubuntu、Edubuntu 和 Ubuntu Lite，以及一个针对 Ubuntu Server 发行版的论坛。Ubuntu 网站还提供 RSS 馈，帮助你跟踪最新动态。

网络上还有许多其他 Ubuntu 相关网站，每天都有新的网站出现。DistroWatch 网站提供了指向 Ubuntu 相关网站和评论的良好集合，但与互联网上的任何事物一样，你最喜欢的搜索引擎是你的朋友，它能迅速为你找到数百个其他网站来搜索特定问题的答案，或仅仅查看其他人对 Ubuntu 的看法和评价。

## 总结

Ubuntu 是近期记忆中增长最快的 Linux 发行版，我见过的开源和社区力量的最典范之一。在提供了有关 Linux 的通用信息后，本章概述了 Ubuntu Linux 背后的哲学以及该发行版的目标。正如本章所述，Ubuntu 到今的成功，除了技术卓越和易用性之外，很大程度上植根于丰富且快速增长的用户社区以及一个组织良好的、便于访问各种 Ubuntu 相关资源的网站。

# 安装 Ubuntu

本章将讨论如何在新的或现有的 32 位或 64 位 PC 系统上安装或简单地尝试 Ubuntu Linux。本书附带了一张 Ubuntu 10.04 桌面 CD，你可以通过它将 Ubuntu 永久安装到你的系统中，也可以在不对当前系统进行任何更改的情况下，简单地试用 Ubuntu 10.04。试用（Test-driving）Ubuntu 是尝试预配置的 Ubuntu 安装的极佳方法，而无需实际修改你的硬盘或经历整个安装过程。你还可以将 Live CD 当作便携式电脑随身携带，将其他计算机临时转换为 Ubuntu Linux 系统，无论该机器目前运行的是否 Windows。Live CD 还提供了令人印象深刻的“活动 CD 持久化（Live CD Persistence）”功能，它允许你在使用桌面 CD 时将工作和配置保存到可移动介质中，以便下次下次从 CD 启动时可以重复使用。在大多数情况下，在从 Ubuntu CD 启动后，你可以访问现有的磁盘存储，因此你甚至可以在使用 Live CD 时进行工作，并保存到 USB 闪盘或操作系统使用的磁盘中。

Ubuntu 桌面 CD 将传统的 Live 概念向前推进了一步，它让你能够使用简单易用的安装程序快速安装 Ubuntu Linux，你只需点击从 Live CD 启动时看到的桌面上的图标即可开始。Ubuntu 安装程序可以自动缩小现有的 Microsoft Windows 或 Linux 分区的大小，为安装 Ubuntu 腾出空间（当然，前提是你的现有分区没有满）。

但等一下，还有更多！在运行 Microsoft Windows 的系统上插入 Live CD，可以让你使用一个名为 `Wubi`（基于 Windows 的 Ubuntu 安装程序）的软件包，在你的 Windows 系统上安装 Ubuntu，而无需对该系统进行任何修改，除非在开机时添加一个启动 Ubuntu 的选项（当然，还需要使用你现有的部分磁盘空间来存储 Ubuntu 启动镜像）。关于这点的更多信息稍后介绍！

## 本章内容

- 启动桌面 CD
- 安装 Ubuntu
- 试用 Ubuntu
- 从桌面 CD 访问现有分区
- 创建可启动的 USB 驱动器
- 在不分区的情况下安装 Ubuntu

# 第一部分：上手 Ubuntu

如果你正在使用 32 位 x86 系统并想要运行或尝试 Ubuntu Linux，那么本书附的 Ubuntu 桌面 CD 正适合你。如果不是，本章将解释如何获取适用于你正在使用的系统的 Ubuntu Live CD。

## 注意

在 2009 年底，Canonical 宣布对 ARM 平台的支持，将 Ubuntu 的可用性扩展到使用 ARM 处理器的少数网络。要获取 ARM 版本的 Ubuntu，请参阅 www.ubuntu.com/products/whatis/arm。Ubuntu 版本也适用于 PPC（Power）和 SPARC 平台，但这些不再受 Canonical 的官方支持。Ubuntu for PPC 是一个社区支持的项目，目前仍然活跃，而用于 SPARC 系统的 Ubuntu 已逐渐没落。你可以看到许多社区支持的 Ubuntu 版本，并从原始 URL http://cdimage.ubuntu.com/ports/releases/VERSION/release 下载 镜像，其中 `VERSION` 是标准 Ubuntu 发布版本的名称，例如 Karmic、Lucid 等。

## 获取 64 位桌面 CD

本书附的 Ubuntu 桌面 CD 可以在任何 x86 PC 系统上启动。如果你想在 64 位计算机系统上安装或尝试 Ubuntu，你需要获取另一个不同的等效桌面 CD。如果你有较快的互联网连接（或有充足的时间）以及一个刻光刻录机，获取不同桌面 CD 最简单的方法是下载 ISO 镜像。ISO 镜像是一个包含 CD-ROM 或 DVD 副本的文件，格式符合国际标准组织 9660 规范的要求。如需获取 64 位 Ubuntu 桌面 CD，请访问 Ubuntu 网页 www.ubuntu.com/download，选择你想要 CD 的 Ubuntu 版本，选择你所在的国家或离你最近的国家，然后选择 64 位 Ubuntu 桌面 CD。下载 ISO 镜像到文件后将其刻录到 CD。如果你的互联网连接慢或没有刻录机，正如介绍中所述，这可能会让你抓狂！但对于想要立即体验的人来说，这可能可行。访问 Ubuntu 网页 ship.ubuntu.com，创建账户并设置密码，获取当前版本的 Ubuntu 集。

## 启动桌面 CD

从桌面 CD 启动 Ubuntu 非常简单，只需将相应的桌面 CD 插入系统，然后重启系统。

# 第 2 章：安装 Ubuntu

## 警告

即使插入了正确的桌面 CD，如果 PC 仍然从硬盘启动，那么你需要修改 BIOS 设置中的启动顺序。启动顺序是系统开机时搜索可用设备的顺序。要执行此操作，请打开电脑并按下键盘上访问 BIOS 的键。根据你电脑 BIOS 的类型，这通常是 `Delete` 或 `F2` 键。进入 BIOS 设置后，使用方向键将 CD 驱动器移动到顶部。保存设置并退出（通常按 `F10`）。

当你从 Ubuntu CD 启动时，最初会看到如图 1 所示的屏幕。

图 1

桌面 CD 上的初始屏幕

如果在看到此屏幕时什么都不做，系统将继续从桌面 CD 启动，并最终显示图 2 所示的屏幕。

图 2

默认桌面 CD 尝试/安装界面

看到界面后，你可以选择左侧的滚动列表更改 Ubuntu CD 或 Ubuntu 安装程序使用的语言。然后你可以：

- **尝试 Ubuntu 10.04**：在不对你的计算机系统进行任何更改的情况下进入 Ubuntu Linux。这允许你在不更改系统的情况下尝试 Ubuntu（通常称为试用）。Linux CD 见本节的图 5。从桌面 CD 启动后尝试 Linux 详见本章的“试用 Ubuntu”节。跳转到该节获取更多信息。
