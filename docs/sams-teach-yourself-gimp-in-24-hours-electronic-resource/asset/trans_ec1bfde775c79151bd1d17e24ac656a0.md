

# 引言

课程中穿插了名为“备注”、“提示”和“注意”的特殊元素，它们将为您提供额外的信息。

![](img/0183f053b347a6407a2381be231d0345_22_0.png)

> 备注提供了提供了关于正在讨论的话题或功能的补充信息。

![](img/0183f053b347a6407a2381be231d0345_22_1.png)

> 提示提供了节省时间的建议，并推荐了帮助你获得更专业结果的方法。

![](img/0183f053b347a6407a2381be231d0345_22_2.png)

> 注意将警告你需要避免的陷阱、圈套和错误。

# 1 小时

# 安装与配置

# 使用 GIMP

这一小时旨在协助你完成一项枯燥的任务：将 GIMP（GNU 图像处理程序）v.1.0 成功安装并在你的系统上顺畅运行——如果你还没有这样做的话。它主要针对那些在 PC 架构（Intel 及其兼容机）上运行 Linux 2.0+ 的用户，尽管这里列出的步骤很容易适用于其他的 UNIX 变体和硬件平台，且通常很少或不需要修改（大多数情况下）。

我假设你已经有了 Linux 或某些 UNIX 变体，并运行了 X Window 系统实现。然而，如果情况如此，这一小时也会简要介绍如何在 PC 上安装 Linux。尝试这些东西真的没有任何理由。

在安装像这这样的新软件时，准备和理解至关重要，特别是如果你对 UNIX 较少经验。这绝非困难，但在过程中涉及许多变量，其中任何一个变量都可能导致问题。因此，为了在困难出现之前防止其发生，你应该仔细检查以下标准：

- 你应该在目标机器上拥有管理员权限。
- 检查所需的软件包，并记录你已经安装了哪些、缺少哪些——以及软件的版本。
- 你应该确切知道你的系统是如何设置的以及安装了什么。这样，你就能意识到你的设置可能存在的任何特性（例如，运行 Red Hat 5.1 的用户应该知道）。现在，让我们开始吧。

# 安装 Linux——入门教程

本书主要针对那些已经安装并运行了 Linux（或其他 UNIX 变体），并拥有一些运行和使用它的实际操作知识的用户。然而，如果你是 GNU/Linux 或广义 UNIX 的新手，但想立即开始使用 GIMP 和其他优秀的开源软件，不要担心；Linux 可以从几个供应商处获得（见下方的网站列表），通过少量研究，你很快就能运行一个非常出色的 Linux 盒子。CD-ROM 包含了 GIMP 以及许多其他精彩的应用程序，帮助你探索自由软件的奇妙世界。以下列表列出了你需要的内容：

- gzipped 格式的 GIMP 源码
- RPM 格式的 GIMP 源码
- 适用于各种平台的 RPM 和 gzipped 格式的 GIMP 二进制文件
- GIMP 顺畅运行所需的所有其他（库、额外的免费程序等）

为了安装 Linux，你需要以下内容：

- 一台运行从 386 到 PII 的 Intel 兼容 PC（Linux 也可以轻松适用于其他平台，如 PowerPC、Alpha 和 Spar Sparc）。
- 至少 8MB 内存（Linux 技术上可以在 4MB 内存的 386 上运行，虽然这对于许多应用程序已经足够，但运行像 X 和 GIMP 这样的应用程序通常需要更多的动力来提高生产力。我建议至少使用 Pentium 100 配合 16MB 内存以获得舒适的体验，无论软件如何。）

# 安装与配置

- 一个 CD-ROM 驱动器（或至少一个软驱驱动器、快速的互联网连接——56K，或者如果你想保持理智——以及大量的耐心，取决于你选择如何方法安装 Linux。）
- 学习和折腾的意愿

成功安装 Linux 的基础说明包含在你从下方列出的任何一家公司选择的发行版中。你将找到执行诸如创建启动盘、划分硬盘分区、安装 Linux、设置 X 等操作的基础说明。在安装和设置过程中，打印这些说明以备参考可能是一个好主意。市面上还有很多 Linux 书籍可以在你开始时帮助你（例如《24 小时快速自学 Linux》）。关于 Linux 的更多信息可以在以下网站上找到：

- Linux 文档项目—http://sunsite.edu/mdw/linux.html
- Red Hat（提供适用于 Intel、Alpha 和 Sparc 机器的版本）—http://www.redhat.com/
- Caldera（Open Linux)—http://www.caldera.com/
- Slackware Linux—http://www.slackware.org/
- Debian Linux—http://www.debian.org/
- S.U.SE. Linux—http://www.suse.de/
- Linux for the PowerPPC—基于 LinuxPPC—http://www.linuxppc.com/
- Yellow Dog Linux（另一个 Macintosh 发行版—基于 LinuxPPC)—http://www.yellowdoglinux.com/
- Mlinux（针对 Macintosh 的 Linux；LinuxPPC 的替代方案)—http://www.mklinux.com/
- Linux-m68k（支持其他 m68k Mac)—http://www.linux-m68k.org/
- Linux 笔记本页面—http://cs.utex.edu/users/kharker/linux-laptop/
- Linux/Sparc 帮助页—http://www.ubc.ca/s_linux.html
- 半官方 Linux 主页—http://www.linux.org/
- Linux Now!—http://www.linuxnow.com/
- 所有关于窗口管理器—http://themes.org/
- 自定义你的 X 环境—http://themes.org/

# 运行 GIMP 的系统要求

为了成功安装和运行 GIMP 1.0，需要以下项目：

- 一个运行良好的 UNIX 变体（Linux, Solaris, HP-UX, FreeBSD, OpenBSD, AIX, IRIX 等）
- 一个运行良好的 X Window 系统实现（X11R5 或更高版本——优选 X11R6）
- GNU 编译器或等物
- GTK 1.0 或更高版本
- 最新的图形库（libjpeg, libpng, libtiff, libxpm, libz 等）
- 充足的硬件（在 PC 上，这可能意味着至少是 486 且带有 16MB 内存）
- 至少 20MB 硬盘空间用于最小化安装（完整编译和调试会需要 100MB），并留有剩余空间

# 关于 GIMP

GTK 是 GIMP ToolKit 的缩写。它是 GIMP 中一个至关且必需的组件——GIMP 构建在其之上的工具包。如果你在好奇的话，工具包多程度上是指任何为图形应用程序绘制“小部件”的库——滚动条、按钮、菜单等。UNIX 传统上有很多工具包可供选择，根据程序员的需求，其简单或稳健程度各不相同。最初，GIMP 使用 Motif 作为工具包，但 GIMP 的创建者创建了 GTK，作为商业许可 Motif 的一种更现代、更具操作性的替代方案。GTK 纯洁、强大、高效且符合美学（至少对我而言）。它现在被用于许多其他应用程序，以及 GNOME 桌面项目。

在写作时，最好只安装稳定系列的 GTK 以供 GIMP 使用。如果你在好奇的话，工具包基本上是任何为图形应用程序绘制“小部件”的库。目前，使用 1.1 版本可能不会在运行 GIMP 时遇到问题，因为 http://gtk.org/ 和 http://www.gimp.org/ 上是最新的版本。

# 安装与配置

# 图形库

你的操作系统（OS）安装如果较新或维护良好，可能已经有了相当图形库可用，但你可能需要从全球许多 FTP 镜像站点获取，例如 ftp://ftp.x.org/contrib/libraries/ 和 ftp://ftp.gimp.org/pub/gimp/。这里是清单：

- aalib 1.2 或更高
- xdelta .20 或更高
- libpng 1.0.1 或更高
- libxpm 4.7 或更高
- libtiff 3.4 或更高
- libmempeg 1.2.1 或更高
- libjpeg 6b 或更高
- zlib 1.1.2 或更高

ImageMagick（并不需要，但它包含了许多格式以及非常实用的工具）可以在 http://www.wizards.dupont.com/cristy/ImageMagick.html 找到。

