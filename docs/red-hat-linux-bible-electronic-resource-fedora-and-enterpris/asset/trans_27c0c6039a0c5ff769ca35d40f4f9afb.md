
对于桌面用户来说，从 Windows 过渡到 Linux 正变得越来越容易，WINE 项目等项目取得了长足进步。WINE（本章后面将介绍）让你能直接在 Linux 中运行许多 Windows 程序。WINE 还为应用程序开发者提供了一条途径，使他们能更简单地将 Windows 代码移植到 Linux 上运行。

归根结底，大多数人要完全抛弃 Windows 操作系统仍需付出一些努力。然而，如果你致力于将 Red Hat Linux 作为唯一的应用平台，有几种方法可以缓解这种过渡。仿真程序让你能运行许多为其他操作系统创建的程序。转换程序可以帮助你将图形和文字处理数据文件从其他格式转换为 Linux 应用程序支持的格式。

> 交叉引用：有关导入和导出文字处理及图形文件的信息，请参见第 6 章。

如果你在 PC 上运行 Linux，很有可能你已经为 Windows 95、98、ME、XP、NT 或 2000 操作系统付过费了。你可以在不同的 PC 上运行不同的操作系统，或者将 Windows 和 Linux 安装在硬盘的不同分区上。后者要求你每次想切换操作系统时都必须重新启动。

下一节将介绍在 Red Hat Linux 中运行的应用程序，你可以用它们来替代你习惯使用的 Windows 应用程序。

## 在 Linux 中寻找 Windows 同类应用程序

如果你打算将 Red Hat Linux 用作桌面计算机系统，你必须能够编写文档、处理图形和计算数字。你可能还有其他喜爱的应用程序，如音乐播放器、Web 浏览器和电子邮件阅读器。

> 注意：Codeweavers 公司利用 WINE 技术提供了 CrossOver Office 产品，让你能在 Linux 中安装并运行 Microsoft Office。请参阅本章后面的“使用 WINE 运行 Windows 应用程序”部分。

为了让你大致了解有哪些桌面应用程序可用，表 5-1 列出了流行的 Windows 应用程序、对应的 Linux 应用程序以及在哪里可以找到这些 Linux 应用程序。尽管这些应用程序中有许多尚未达到其 Windows 对应产品的复杂程度，但它们可以作为具有成本效益的替代品。

### 表 5-1：Windows 同类 Linux 应用程序

| Windows 应用程序 | Linux 应用程序 | 在哪里获取 Linux 应用程序 | 成本 |
|---|---|---|---|
| Microsoft Office（办公套件） | OpenOffice (openoffice.org) | 包含在 Red Hat 光盘中 | 免费 |
|  | Koffice | 包含在 Red Hat 光盘中 | 免费 |
|  | StarOffice | www.sun.com/staroffice | $75.95 |
| Microsoft Word（文字处理器） | OpenOffice Writer | 包含在 Red Hat 光盘中 | 免费 |
|  | abiWord | 包含在 Red Hat 光盘中 | 免费 |
|  | kword | 包含在 Red Hat 光盘中 | 免费 |
| Microsoft Excel（电子表格） | OpenOffice Calc | 包含在 Red Hat 光盘中 | 免费 |
|  | gnumeric | 包含在 Red Hat 光盘中 | 免费 |
|  | kspread | 包含在 Red Hat 光盘中 | 免费 |
| Microsoft PowerPoint（演示文稿） | OpenOffice Impress | 包含在 Red Hat 光盘中 | 免费 |
|  | kpresenter | 包含在 Red Hat 光盘中 | 免费 |
| Microsoft Internet Explorer（Web 浏览器） | mozilla | 包含在 Red Hat Linux 光盘中 | 免费 |
|  | epiphany | 包含在 Red Hat Linux 光盘中 | 免费 |
|  | konqueror | 包含在 Red Hat Linux 光盘中 | 免费 |
|  | opera | www.opera.com | 免费下载 |
| Microsoft Outlook（电子邮件阅读器） | evolution | 包含在 Red Hat 光盘中 | 免费 |
|  | kmail | 包含在 Red Hat 光盘中 | 免费 |
|  | Mozilla Mail | 包含在 Red Hat 光盘中 | 免费 |
| Adobe Photoshop（图像编辑器） | The Gimp (gimp) | 包含在 Red Hat 光盘中 | 免费 |
| Quicken 或 Microsoft Money | gnucash | 包含在 Red Hat 光盘中 | 免费 |
| AutoCAD（计算机辅助设计） | LinuxCad | www.linuxcad.com | $89 |

### 获取 Red Hat Linux 应用程序

不幸的是，你无法走进普通的电脑商店找到大量的 Linux 应用程序。获取 Linux 应用程序（随 Red Hat Linux 系统附带的除外）的最佳途径是从互联网下载。也可以从一些 Linux 网站订购 CD-ROM。

专门为 Red Hat Linux 发行版编译和打包的软件包几乎总是以 RPM 格式提供。因此，当你开始在互联网上搜寻 Red Hat 软件（稍后将介绍）时，请寻找专门为你所使用的 Red Hat Linux 或 Fedora Core 版本构建的 RPM 包软件仓库。

### 探索你的桌面

越来越多的高质量桌面应用程序被打包进 Red Hat Linux，主要作为 GNOME 或 KDE 桌面环境的一部分。换句话说，要开始寻找一些优秀的办公应用程序、游戏、多媒体播放器和通讯工具，你不必再看看桌面上的 Red Hat 菜单按钮。

因此，在你开始在互联网上四处寻找所需软件之前，先看看能否使用随 Red Hat Linux 已安装的软件。后续章节将介绍如何使用出版工具、玩游戏、处理多媒体和在互联网上通讯——所有这些都使用随本书附带光盘中的程序或易于获取的程序。附录 B 包含了随本书打包的 Red Hat Linux 完整版所包含的软件包列表。

> **提示：** 为了跟上 Red Hat Linux 发行版中软件包的修复，Red Hat 提供了一项自动下载和安装包的服务。第 10 章将向你展示如何使用 Red Hat Network 和 `update` 命令来更新你的 Red Hat Linux 软件。

### 在互联网上寻找应用程序

如果你还不知道想用的应用程序名称，在互联网上有很多地方可以寻找 Linux 应用程序。如果你知道想要什么，最好的选择可能是去一个专门为 Red Hat Linux 和 Fedora 构建了软件包的软件仓库。

以下是一些你可以浏览以寻找在 Linux 上运行的软件的网站：

- **Freshmeat** (www.freshmeat.net) — 该站点维护着一个庞大的 Linux 软件索引。你可以按关键字搜索软件项目，或按类别浏览软件。
- **SourceForge** (www.sourceforge.net) — 该站点托管着数千个开源软件项目。你可以从 SourceForge 站点下载这些项目的软件和文档。
- **Tucows Linux 站点** (linux.tucows.com) — Tucows Linux 网站上提供免费和商业 Linux 软件。该站点还提供关于 Linux 的新闻文章和按类别列出的软件下载。

当你购买商业应用程序时，通常会获得光盘上的应用程序。安装通常经过简化，并提供纸质文档。当然，当你下载软件时，你会得到即时满足——当你购买时，你必须等待包裹通过邮件送达。

> **提示：** 有时软件包会同时提供 libc5 和 libc6 两种格式。这种标识指的是应用程序所使用的 C 编程语言库的版本。如果你有选择权，请选择 libc6 包。这些包兼容 Red Hat Linux 7 及更高版本（或任何 Linux 内核 2.2 及更高版本）。事实上，所有主要的 Linux 发行版现在都使用 libc6。更好的做法是寻找专门为你所使用的发行版指定的包（如 Fedora、Red Hat Linux 9 等）。

如果你已经大致知道要找什么，可以访问包含 RPM 包的 FTP 站点。你可以先阅读特定软件产品的 README 和 INDEX 文件以了解情况。当你找到想要的软件时，只需点击链接即开始将软件下载到你的计算机。以下是一些寻找 RPM 包特别好的站点：

- **Rpmfind** (www.rpmfind.net) — 该站点提供已打包为 Red Hat Package Management (RPM) 格式的开源软件。从此网站进行关键字搜索，然后从搜索结果中下载合适的 RPM。
- **FreshRPMs** (www.freshrpms.net) — 另一个提供大量高质量 RPM 的站点。
- **Red Hat FTP 镜像站点** (www.redhat.com/mirrors.html) — 访问此页面可获取包含可下载 Red Hat 软件的 FTP 站点列表。这些站点大多还提供各种可在 Linux 上使用的免费软件和共享软件应用程序。

通常，你不能仅下载单个软件包就让该包中的软件运行起来。许多包依赖于其他包。例如，用于播放音频和视频的软件包通常依赖于用于解码不同类型内容的其他软件包。为了解决这个问题，Red Hat Linux (Fedora Core) 包含了 yum 包。
