

## 衡量 DAMN SMALL LINUX 的成功

尽管体积小，Damn Small Linux 一直稳居最受欢迎的 Linux 发行版之列。根据监控 Linux 网站的各大网站排名，DSL 一直位居最活跃之列。据 Google 统计，网络上关于 Damn Small Linux 的引用接近 1,000,000 条。Yahoo 显示，指向 Damn Small Linux 主页的入站链接约为 1,480,000 条。

在 DistroWatch（www.distrowatch.com）过去三年中，DSL 在页面点击量上一直稳居 Linux 发行版前十名，常与 Debian、Slackware、KNOPPIX 和 Gentoo 等知名 Linux 系统并列。根据监控网站流量的 Alexa（www.alexa.com）数据显示，2007 年初，DSL 网站（www.damnsmalllinux.org）在网络上的流行度约为 33,350 名。这一排名使其比 Ubuntu、SuSE、Slackware、KNOPPIX、Mepis、Morphix 等 Linux 发行版的主页更受欢迎。

就媒体报道而言，关于 Damn Small Linux 的文章和评测不计其数。2004 年 5 月，DSL 在 TechTV 的 The Screen Savers 节目中被重点介绍。DSL CD 已随 Linux Format、Linux User & Developer、Sys Admin、Linux Journal、PC Magazine、PC World、Computer Power User（CPU）和 Linux Pro 等杂志附赠。

尽管 Damn Small Linux 并不是第一个 Linux live CD（事实上，它最初基于 KNOPPIX live CD），但它仍有诸多首创之举。DSL 是首个实现以下功能的 Linux live CD 发行版：

- 提供备份和恢复功能。
- 使用下载脚本在运行时（在 ramdisk 中）添加软件。
- 采用可扩展的软件模块，可从 live CD 或磁盘使用。
- 集成 USB 安装脚本。
- 使用包含 QEMU 虚拟化软件的特殊嵌入式 DSL 版本，可在 Windows 桌面上虚拟运行。
- 提供专为 live CD 或 USB 驱动器设计的低内存扩展。

DSL 还包含许多专门与桌面导向 live CD 相关的首创功能。它是首个可放入可启动名片的桌面导向 live CD，提供任何桌面操作系统中最小的占用空间。它也是首个使用 Tiny X KDrive 服务器作为桌面 X 显示服务器的发行版。为了实现许多标准 Linux 工具，DSL 是首个使用 BusyBox 节省空间实用程序的发行版。

## 理解 DAMN SMALL LINUX 最擅长做什么

当你启动 Damn Small Linux 时，首先看到的是启动屏幕。在大多数情况下，你可以按 Enter，片刻之后桌面系统就会出现。只需几次点击，你就可以浏览网页、编辑文档、播放音乐或进行数十种其他活动。图 1-1 显示了繁忙的 DSL 桌面的示例。

![](img/af53325d7f38f1cdafca9f44568e4ab8_31_0.png)

图 1-1 Damn Small Linux 提供了一个简洁高效的桌面界面。

图 1-1 中的 DSL 桌面展示了一些 DSL 桌面的基本功能以及一些应用程序。你可以通过屏幕左上角显示的图标（单击左键）启动应用程序。在右上角，可查看系统资源（CPU、进程、文件系统等）的数据。dock.lua 工具（右下角）可让你调整音频并挂载磁盘分区。底部面板显示当前日期/时间、最小化应用程序以及管理工作区的工具。使用左下角的工具可在工作区之间移动应用程序。

图 1-1 中显示正在运行的应用程序包括 Firefox 网络浏览器、XMMS 音乐播放器、XPaint 图像编辑器和 Beaver 文本编辑器。右上角是出色的 torsmo 系统监视器，可监控所有系统资源（处理器、RAM、交换空间、磁盘和其他资源使用情况）。这些以及 DSL 中原生可用的其他应用程序将在第 3 章“使用 DSL 应用程序”中详细介绍。

图 1-1 中显示的一个管理工具是 MyDSL 扩展工具。你可以使用该工具下载和安装预打包以在 DSL 中运行的应用程序（参见第 5 章“使用 MyDSL 扩展应用程序”）。

尽管图 1-1 中 DSL 桌面上显示的应用程序已打包在基本 50MB 可启动映像中，但 Damn Small Linux 的价值远不止于此。如果 DSL 不能完全满足你的需求（以及你想要使用它的位置），该项目会帮助你以以下方式改进使用 DSL 的体验：

- 可扩展——使用 MyDSL 功能和互联网连接，只需几次鼠标点击即可在运行的 DSL 系统上下载并安装大量额外应用程序。由于 DSL 的根源在于其他流行的 Linux 发行版（尤其是 Debian 和 KNOPPIX），为这些发行版创建的软件通常也可以直接放入 DSL 中运行。参见附录 B，“MyDSL 扩展。”
- 可移植——尽管标准 DSL 可在小至 50MB 可启动名片的介质上运行，但它可以轻松地从硬盘、标准 CD 或 DVD、USB 闪存盘或其他固定和可移动介质运行。它甚至可以从已安装的 Linux 或 Microsoft Windows 系统中嵌入运行。
- 许多人已将 DSL 放在 USB 闪存盘上，并附带其他应用程序和数据（文档、音乐、图像和演示文稿）。因此，你无需随身携带整台笔记本电脑，只需携带一个约指甲大小的 USB 闪存盘或笔式驱动器即可携带所需的一切。

保持基本 DSL 系统小巧、快速和高效，使其既是一个不错的工具本身，也是构建的基础。以下是使用 DSL 的一些最佳理由列表：

- 老机器焕发新生——DSL 可在仅有 16MB RAM 和 486DX 处理器的计算机上运行。DSL 开发人员提供 DSL 的版本

