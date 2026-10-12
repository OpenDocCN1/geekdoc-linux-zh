

## 使用 KPaint 修改图像

使用 KPaint 窗口（这是 KDE 桌面环境自带的一个实用程序，包含在 kpaint 软件包中），你可以处理和转换多种格式的图像。图 6-14 展示了一个 KPaint 的示例。

![](img/1744bde8c889adfab3fc911e1687fecf_271_0.png)

图 6-14：使用 kpaint 编辑位图图像。

你可以从桌面（点击 KDE 菜单 → 图形 → KPaint）或从终端窗口（`/usr/bin/kpaint&`）启动 KPaint。你可以从空白画布开始，或者打开一种受支持格式的图像（文件 → 打开，浏览查找文件，然后选择确定）。可以在 `/usr/share/pixmaps/backgrounds` 目录中查找图形进行尝试。

绘画工具允许你绘制椭圆、方框、线条和其他形状。你可以将文件保存为多种不同的格式，包括 MS Windows 位图、封装的 PostScript 图像、MS Windows 图标、JPEG、PNG、PNM、TIFF、X 位图或 X 窗口像素图。

## 使用 SANE 驱动的扫描仪

用于在 Linux 上使用扫描仪的软件是由一个名为“扫描仪访问现在很容易”（Scanner Access Now Easy, SANE）的项目推动的。该项目希望标准化扫描仪、静态数码相机和数码摄像机等设备驱动程序的开发方式，并有助于简化使用这些设备的应用程序的接口。

SANE 现在已包含在 Red Hat Linux 发行版中。sane-backends 和 sane-frontends 软件包位于随本书附带的第一张 Red Hat Linux 安装光盘（CD-1）上。你可以从 www.mostang.com/sane 获取最新的 SANE 驱动程序软件包。

希望使用 Linux 作为出版平台的人通常对扫描仪的两个问题感兴趣：支持哪些扫描仪以及有哪些可用应用程序来使用扫描仪。一般来说，支持的 SCSI 扫描仪比并口扫描仪更多。

由于持续的开发工作，新扫描仪不断被支持。你可以在 `www.mostang.com/sane/sane-backends.html` 找到当前支持的扫描仪列表。至于应用程序，目前 Red Hat Linux 中可用的是：

-   **xsane** — 这是 SANE 扫描仪的基于 X 的图形前端；*xsane* 可以作为 GIMP 插件运行，也可以作为独立应用程序运行。它支持 8 位输出，格式包括 JPG、TIFF、PNG、PostScript 和 PNM。对于 PNM（ASCII）、PNG 和原始格式，提供实验性的 16 位支持。图 6-15 展示了 *xsane* 窗口。

![](img/1744bde8c889adfab3fc911e1687fecf_272_0.png)

-   **xscanimage** — 另一个基于 X 的窗口，用于预览和扫描来自 Linux 扫描仪或数码摄像头的图像。从命令行启动 *xscanimage* 可以将图像保存为 PBM（黑白）、PGM（灰度）或 PPM（彩色）。当作为 GIMP 插件使用时，由 GIMP 处理图像。
-   **scanimage** — 这是用于获取扫描图像的命令行接口。它支持与 *xscanimage* 相同的格式。该命令获取扫描图像，然后将数据重定向到标准输出（因此你可以将其发送到文件或通过管道传输到另一个程序）。
-   **xcam** — 此图形界面允许你从系统的视频摄像头接口抓取连续图像。

由于 SANE 扫描仪驱动的架构设计，可以将扫描仪驱动与扫描仪应用程序分离。这使得跨网络共享扫描仪和视频摄像头成为可能。

## 摘要

近年来，基于现代 GUI 的出版工具增强了一直与 Red Hat Linux（以及其他 UNIX 系统）提供的基于文本的出版工具。Red Hat Linux 附带的出版工具包括 Groff（实现传统的 troff/nroff 文本处理）和 LaTeX（一种特别适用于科学和数学出版的 TeX 宏接口）。

随着 Red Hat Linux 日益普及，越来越多的面向 Linux 的商业出版应用程序出现。Anyware Office 和 StarOffice 是两套在 Linux 中提供强大出版功能的应用程序套件。Red Hat Linux 包含一些免费的文字处理器，包括 AbiWord 和 KWord。虽然 AbiWord 不及最好的商业文字处理器，但它具有基本功能并具有未来的潜力。

为了创建和修改图形，Red Hat 附带了 GIMP、xv 和 KPaint 等应用程序。

# 第 7 章

## 使用 Red Hat Linux 玩游戏

### 本章内容

-   基本的 Linux 游戏信息
-   X Window 游戏
-   基于字符的游戏
-   xmame 游戏模拟器
-   Transgaming 和 WineX 游戏
-   商业 Linux 游戏

计算机游戏的进步反映了计算机本身的改进。在 20 世纪 70 年代，UNIX 系统上的首批游戏在视觉上很简单，并且可以在缓慢的基于字符的终端连接上运行。如今，结合了图形、动画和声音的游戏推动了计算机技术整体进步的进程。

可用于 Red Hat Linux 的游戏软件的可用性与 Linux 出版软件类似。许多旧软件仍然存在（且免费），而较新的软件则以演示形式提供，但要获取完整版则需付费。一些专家预测，游戏将成为将 Linux 带入家庭的软件类别。尽管目前流行的游戏应用程序数量有限，但就像 Linux 中的其他所有内容一样，每天都有更多游戏变得可用。

本章介绍 Linux 游戏的当前状态，包括启动游戏环境的基础知识，以及多用户游戏的硬件和网络考虑因素。它描述了 Red Hat Linux 附带的或可以轻松下载到的免费游戏（大多是基于字符的以及相当简单的 X Window 游戏）。对于运行其他平台创建的游戏，本章介绍了一些游戏模拟器。

本章还讨论了一些图形游戏，例如 Quake III，其演示版本可用于 Linux，同时全版商业游戏也已打包用于 Linux。

## 基本 Linux 游戏信息

要运行 Red Hat Linux 附带的大多数基于文本或基于 X Window 的游戏应用程序，你需要知道的信息并不多。大多数可能会让你绊倒的游戏问题涉及那些需要特殊硬件和软件来运行 3D 图形和动画的商业游戏。除此之外，有一些游戏信息可能有用。

-   游戏通常放在 `/usr/games` 或 `/usr/X11R6/bin` 中，尽管许多 KDE 游戏只是堆在 `/usr/bin` 中。如果你经常玩的一款游戏位于 `/usr/games` 或其他默认不在你的 `PATH` 中的目录，你可能希望将它们添加到你的 `PATH` 中。这样，你就无需输入完整的目录结构来运行命令了。游戏也可能安装在 `/usr/local/games` 或其他目录（如 `/opt` 的子目录）中。
-   较旧的 Linux 游戏的手册页位于第 6 节（在 `/usr/share/man/man6` 目录中）。

> **提示：** 安装游戏软件包后，我会输入 `rpm -ql package`，其中 `package` 是游戏软件包名称。这会告诉我可执行文件和文档所在的位置（如果有）。

### 在哪里获取 Linux 游戏信息

要查找有关 Linux 上最新游戏的新闻以及下载站点的链接，请访问几个可用的网站。以下是一些入门网站：

-   **The Linux Game Tome** (`http://happypenguin.org`) — 该网站设有一个数据库，包含大量在 Linux 上运行的游戏的描述和评论。你可以对该网站上列出的游戏进行关键词搜索。该网站还包括获取不同游戏的链接以及其他游戏网站的链接。
-   **Linuxgames.com** (`http://linuxgames.com`) — 该网站可以帮助你获取你感兴趣的游戏的最新信息。它包含 HOW-TO 和常见问题解答（FAQs）的链接，以及讨论 Linux 游戏的论坛。还有链接到提供你感兴趣的特定游戏信息的网站。
-   **id Software** (`www.idsoftware.com/archives`) — 访问 id Software 网站获取有关 Quake 和 Doom 游戏 Linux 演示版本的信息和下载链接。
-   **Loki Entertainment Software** (`www.lokigames.com`) — Loki 将畅销游戏移植到 Linux，但于 2001 年倒闭。他们的产品包括 Civilization: Call to Power、Myth II: Soulblighter、SimCity 3000、Railroad Tycoon II 以及 Quake III Arena 的 Linux 版本。Loki 演示启动器仍然可用，可以查看其中一些游戏的演示版本。

