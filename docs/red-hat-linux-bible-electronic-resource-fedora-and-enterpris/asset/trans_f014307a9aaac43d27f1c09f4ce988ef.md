

图 6-13：GIMP 是一款功能强大的图形处理工具。

![](img/27a85d56d393921ced6412ae6e8336bf_260_0.png)

> **注意：** 如果您的系统中没有 GIMP 或安装不正确，您可以从随书附带的 CD #1 安装它。或者，您可以从 www.gimp.org 获取最新版本的 GIMP。

在许多方面，GIMP 类似于 Adobe Photoshop。一些人认为 GIMP 的脚本功能与 Adobe Photoshop 中的“动作”相比，不相上下，甚至更胜一筹。然而，GIMP 缺少的一项功能是对 CMYK 分色的支持。

### 进行屏幕捕获

如果您想展示在 Red Hat Linux 上工作的示例，可以使用屏幕捕获程序来捕获屏幕图像。（`ksnapshot` 命令包含在 CD #2 上的 `kdegraphics` 软件包中。）

要打开屏幕捕获程序，请从 Red Hat 菜单中点击“图形”→“屏幕捕获程序”（或输入 `ksnapshot`）。图 6-14 显示了屏幕捕获程序的一个示例。

屏幕捕获程序首次打开时，会对整个桌面进行快照。窗口上的按钮可让您：

- **打印快照** — 将快照发送到打印机。
- **保存快照** — 将快照保存为 X 位图、Windows 图标、PNG、可移植像素图、JPEG、X 像素图、封装 PostScript 或 Windows BMP 格式的文件。
- **新建快照** — 进行一次新的快照。选择“仅抓取窗口...”后，您可以点击一个窗口以单独捕获该窗口。

![](img/27a85d56d393921ced6412ae6e8336bf_261_0.png)

### 使用 KPaint 修改图像

使用 KPaint 窗口（一个随 KDE 附带的实用程序，包含在 CD #2 的 `kdegraphics` 软件包中），您可以处理并转换多种格式的图像。图 6-15 显示了 KPaint 的一个示例。

![](img/27a85d56d393921ced6412ae6e8336bf_261_1.png)

从桌面（在 Red Hat 菜单中，点击“图形”→“更多图形应用程序”→“绘图程序”）或从终端窗口（`/usr/bin/kpaint&`）启动 KPaint。从空白画布开始，或通过打开受支持格式之一的图像开始（“文件”→“打开”，浏览文件，然后选择“确认”）。在 `/usr/share/backgrounds` 目录中查找可供尝试的图形。

绘图工具可让您绘制椭圆、矩形、线条和其他形状。您可以将文件保存为多种不同格式，包括 MS Windows 像素图、封装 PostScript 图像、MS Windows 图标、JPEG、PNG、PNM、TIFF、X 位图或 X Window 像素图。

### 使用由 SANE 驱动的扫描仪

在 Linux 下使用扫描仪的软件开发工作，是由一个名为“扫描仪访问现在很简单”（SANE，Scanner Access Now Easy）的项目推动的。该项目旨在标准化扫描仪、数码相机和数码摄像机等设备的驱动程序创建方式，并帮助简化使用这些设备的应用程序接口。

SANE 现在已包含在 Red Hat Linux 发行版中。`sane-backend` 和 `sane-frontend` 软件包在 CD #1 上，而 `xsane` 和 `xsane-gimp` 软件包在 CD #2 上。您可以从 www.mostang.com/sane 获取最新的 SANE 驱动程序包。

想要将 Linux 用作出版平台的人，通常关心关于扫描仪的两个问题：支持哪些扫描仪，以及有哪些应用程序可用于驱动扫描仪。一般来说，支持的 SCSI 扫描仪比并口扫描仪多。

由于持续的开发工作，不断有新的扫描仪获得支持。您可以在 www.mostang.com/sane/sane-backends.html 找到当前支持的扫描仪列表。至于应用程序，目前 Red Hat Linux 中提供了以下这些：

- **xsane** — 这是一个基于 X 的 SANE 扫描仪图形前端；xsane 可以作为 GIMP 插件工作，也可以作为一个独立应用程序工作（从 Red Hat 菜单中，选择“图形”→“扫描”）。它支持 JPG、TIFF、PostScript 和 PNM 格式的 8 位输出。对于 PNM（ASCII）、PNG 和原始格式，有实验性的 16 位支持。
- **scanimage** — 这是一个用于获取扫描图像的命令行界面。它支持与 `xscanimage` 相同的格式。该命令获取扫描图像，然后将数据导向标准输出（因此您可以将其发送到文件或通过管道传递给另一个程序）。

由于 SANE 扫描仪驱动程序的架构，可以将扫描仪驱动程序与扫描仪应用程序分离。这使得跨网络共享扫描仪成为可能。

### 小结

近年来，基于现代 GUI 的出版工具增强了 Red Hat Linux（及其他 UNIX 系统）一直以来提供的基于文本的出版工具。强大的开源出版工具（如 OpenOffice）正变得与商业办公套件具有竞争力。传统的出版工具（如 Groff——实现了传统的 troff/nroff 文本处理，以及 LaTeX——一种特别适合科学和数学出版的 TeX 宏接口）在 Red Hat Linux 中仍然可用。

## 第 7 章：在 Red Hat Linux 中玩游戏

**本章内容**

- 基本 Linux 游戏信息
- X Window 游戏
- 商业 Linux 游戏
- Transgaming 和 WineX 游戏

计算机游戏的进步反映了计算机自身的改进。在 20 世纪 70 年代，UNIX 系统的第一批游戏在视觉上很简单，可以在缓慢的、基于字符的终端连接上运行。如今，结合了图形、动画和声音的游戏，总体上帮助推动了计算机技术的进步。

可用于 Red Hat Linux 的游戏软件的可用性，类似于 Linux 出版软件。许多旧软件仍然存在（且免费），而较新的软件以演示版形式提供，但获取完整版需要花费一些金钱。一些专家预测，游戏将成为将 Linux 带入家庭的软件类别。尽管目前流行的游戏应用程序数量有限，但像 Linux 中的其他事物一样，每天都有更多游戏变得可用。

本章探讨 Linux 游戏的现状，包括启动游戏环境的基础知识，以及游戏的硬件考量。它描述了随 Red Hat Linux 附带或可轻松下载的免费游戏（大多是相当简单的 X Window 游戏）。对于运行为其他平台创建的游戏，本章介绍了 WineX 等游戏模拟器。

本章还讨论了一些提供 Linux 演示版的流行商业游戏。如果您喜欢这些演示版，可以购买这些游戏，它们可在 Linux 中原生运行。

### 基本 Linux 游戏信息

### 在哪里获取 Linux 游戏信息

要查找可用于 Linux 的最新游戏新闻以及下载站点链接，请访问几个可用的网站。以下是一些入门网站：

- **TransGaming Technologies** (www.transgaming.com) — 该公司的使命是将其他平台的游戏移植到 Linux。
- **The Linux Game Tome** (http://happypenguin.org) — 该网站提供了一个数据库，包含大量在 Linux 上运行的游戏的描述和评论。您可以对该网站列出的游戏进行关键字搜索。该网站还包含获取不同游戏的链接，以及其他游戏网站的链接。
- **Linuxgames.com** (http://linuxgames.com) — 该网站能让您深入了解 Linux 游戏的现状。这里有 HOW-TO 文档和常见问题解答（FAQ）的链接，以及讨论 Linux 游戏的论坛。还有您感兴趣的特定游戏信息网站的链接。
- **id Software** (www.idsoftware.com) — 访问 id Software 网站，了解 Quake、Unreal Tournament 和 Return to Castle Wolfenstein 的 Linux 演示版信息。
- **Loki Entertainment Software** (www.lokigames.com) — Loki 将畅销游戏移植到 Linux，但于 2001 年倒闭。其产品包括《文明：召唤神力》、《神话 II：灵魂收割者》、《模拟城市 3000》、《铁路大亨 II》和《雷神之锤 III：竞技场》的 Linux 版本。Loki 演示启动器仍可用于查看这些游戏的演示版，一些盒装套装以极低的价格出售。
- **Tux Games** (www.tuxgames.com) — 如果您准备购买游戏，Tux Games 网站专门销售 Linux 游戏。除了提供 Linux 游戏新闻和产品外，该网站还列出了其最畅销的游戏，并包含即将发布游戏的通知。
- **Linux Gamers' FAQ** (http://iculus.org/lgfaq) — 此 FAQ 包含关于免费和商业 Linux 游戏的大量信息。它列出了将游戏移植到 Linux 的游戏公司，告诉在哪里获取 Linux 游戏，并解答与常见 Linux 游戏问题相关的查询。

如果您对开发自己的游戏感兴趣，请尝试 Linux 游戏开发中心 (http://lgdc.sunsite.dk)。

### Linux 游戏入门

如何开始 Linux 游戏取决于您对它的重视程度。如果您只是想玩几个游戏打发时间，可以找到大量随 Linux 附带的有趣 X Window 游戏。如果您想玩更强大的商业游戏，可以从以下方面选择：

