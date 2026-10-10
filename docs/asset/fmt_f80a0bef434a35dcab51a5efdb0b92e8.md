
> **注意：** 您可以在 BlenderArtists.org 网站上参与 Blender 艺术家和游戏开发者的社区。该网站提供了许多关于 Blender 的有用论坛，包括几个关于 Blender 游戏引擎的活跃论坛。

## 快速上手 Linux 游戏

如果你正在运行 Linux 系统，并希望立即开始玩游戏，这里有一些建议：

- **检查游戏菜单** — Fedora 的默认安装程序已预装了一系列游戏。如果你在 Linux 中运行 GNOME 桌面环境，请从面板中选择“应用程序”→“游戏”。你应该能够选择各种街机、卡牌、棋盘、策略及其他游戏，供你消遣一段时间。
- **为你所在 Linux 发行版打包的游戏** — 许多最受欢迎的开源游戏已被打包以便在你的 Linux 发行版上运行。在 Fedora 中，打开“添加/删除软件”（`PackageKit`）窗口，并选择“游戏”，即可查看你可以下载并游玩的 200 多款游戏列表。
- **其他开源游戏** — 如果你想要的开源游戏并未为你的发行版打包，请尝试访问该游戏的项目站点以获取游戏。互联网上有一些网站包含游戏列表以及通往每个游戏站点的链接。维基百科的 Linux Gaming 页面（<http://en.wikipedia.org/wiki/Linux_gaming>）和 Linux Game Tome（<http://happyypenguin.org>）是很好的起步资源。
- **商业 Windows 游戏** — 最新的商业电脑游戏并非全部都移植到了 Linux。盒装 Linux 商业游戏包括 Unreal Tournament 2003 和 2004，以及大约 50 款已移植到 Linux 运行的一流商业游戏。使用来自 `cedeega.com` 的 `Cedeega`，你可以让数百款流行的 Windows 游戏运行起来。要查看你想要游玩的游戏是否已在 Cedeega 中验证可运行，请访问 Transgaming Games Database（<http://www.cedeega.com/gamesdb/>）查看其状态。有关此产品的更多信息，请访问 CrossOver Games 站点（<http://www.codeweavers.com/products/cxgames/>）。

> **注意：** 第 5 章更详细地介绍了 WINE，它是 Cedeega 和 CrossOver Games 背后的基础技术。有关通过虚拟化运行 Windows 操作系统的更多信息，请参阅第 25 章。

在游玩某些要求较高的 3D 游戏之前，你需要检查你的硬件能否支撑这些游戏。某些需要 3D 硬件加速支持的游戏需要更多内存、更快的处理器以及在 Linux 中运行的特定显卡。有关 Linux 显卡的更多信息，请参阅第 3 章。

以下是 Fedora 和许多其他 Linux 发行版上可提供的快速游戏列表，你可以尝试一下。我按照从“简单且令人上瘾”到“复杂且令人上瘾”的顺序列出了它们：

- **Blood Frontier**（<http://www.bloodfrontier.com/>）— 这款第一人称射击游戏在 Linux、Windows、Mac OS X 和 BSD UNIX 上运行。基于 Cube Engine 2（一款游戏引擎）的转换版，截至本文撰写时，Blood Frontier 仍处于测试版阶段。
- **Frozen Bubble**（<http://www.frozen-bubble.org>）— Frozen Bubble 游戏常被称为最具上瘾性的 Linux 游戏。射击冰冻的气泡和缓慢向你降落的彩色气泡群。消除三个或以上的气泡，直到它们全部消失（或掉落冻结你）。该游戏支持多人游玩。（安装 `frozen-bubble` 软件包并从游戏菜单中选择它。）
- **Gweled**（<http://seblestaing.free.fr/gweled>）— 在这款流行的 Bejeweled 游戏的克隆版中，交换棋盘上的两个宝石以匹配三个或更多宝石（垂直或水平方向）。（安装 `gweled` 软件包并从游戏菜单中选择 Gweled。）
- **WarZone 2100**（<http://wz2100.net/>）— 这款 1999 年的即时战略游戏于 2004 年以开源形式发布。建立基地，在其中设计和建造车辆和武器，建立结构，并研究新技术以进行全球战争。（安装 `warzone2100` 软件包并从游戏菜单中选择 Warzone 2100。）
- **Quake 3 Arena**（<ftp.idsoftware.com>）— Quake 系列中有几款第一人称射击游戏可供从 id Software 下载。在 Fedora 中，安装 `quake3` 软件包并选择 Quake 3 Arena。启动的应用程序允许你下载 Quake3 数据文件的演示版本，这些文件可以免费下载。阅读并接受许可条款以下载数据文件并开始游玩 Quake 3 Arena 演示版。请注意，id Software 的 FTP 站点 `ftp.idsoftware.com` 包含 Quake 4 和其他游戏的 Linux 下载内容。
- **Vega Strike**（<http://vegastrike.sourceforge.net>）— 在这款 3D 动作、太空模拟游戏中探索宇宙。接受运送货物的任务，成为赏金猎人，或在太空中巡逻。在这个 3D 环境中，你可以与调酒师聊天或观看新闻广播，以了解宇宙中的事件。（要在 Fedora 中游玩此游戏，请安装 `vegastrike` 软件包并从游戏菜单中选择 Vega Strike。）

> **注意：** 尽管 Linux 在游戏支持方面取得了进步，但仍有许多流行的 Windows 游戏无法在 Linux 上运行。因此，一些 PC 玩家在电脑上保留一个独立的 Windows 分区，以便启动 Windows 来玩特定游戏。有关 Linux 和 Windows 双启动的更多信息，请参阅第 2 章。

## Linux 游戏基础知识

Fedora 软件仓库中“游戏”组包含 200 多个软件包。因此，如果你只是想寻找一些消遣游戏或现在公开提供的旧版商业游戏，可以从查看该仓库开始。然而，如果你对了解在 Linux 上运行的新商业游戏感兴趣，或者想了解 Linux 游戏的总体状况，有几个你应该查看的网站。

GNOME 游戏包括一些古老的卡牌游戏和一堆看起来很像你在 Windows 系统上会找到的游戏。如果你担心离开 Windows 后会失去你最喜欢的桌面消遣（如 Solitaire、FreeCell 或 Minesweeper），请不必担心。你可以在 GNOME 游戏下找到许多它们的克隆版。如果你安装了 KDE，`kdegames` 软件包中有一堆游戏。如果你没有安装 KDE 桌面，你可以从随书附带的 DVD 中单独安装 `kdegames` 软件包，或者通过 Internet 使用 `yum install kdegames` 安装。要在应用程序菜单中查看 KDE 游戏（以及一些 GNOME 游戏），请选择“游戏”，然后选择你想要玩的游戏。我发现 Shisen-Sho（一种麻将变体）特别令人上瘾。

## 在哪里获取有关 Linux 游戏的信息

要查找可用于 Linux 的最新游戏新闻以及下载站点的链接，请访问可用的几个网站。以下是一些供你起步的站点：

- **TransGaming Technologies Cedeega**（<http://www.cedeega.com>）— 该公司的使命是将来自其他平台（Windows）的游戏带到 Linux。TransGaming 是 Cedeega 的提供商，Cedeega 以前称为 WineX，是一个强大的工具，允许你在 Linux 系统上游玩数百款 PC 游戏。
- **The Linux Game Tome**（<http://happypenguin.org>）— 该网站特色是一个包含大量在 Linux 上运行的游戏描述和评论的数据库。你可以对该网站列出的游戏进行关键字搜索。该网站还包括获取不同游戏的链接，以及其他游戏站点的链接。
- **Linuxgames.com**（<http://www.linuxgames.com>）— 该网站可以让你深入了解 Linux 游戏的现状。它有通往 HOW-TO 和常见问题解答（FAQs）的链接，以及讨论 Linux 游戏的论坛。还有通往包含特定游戏信息的网站的链接。
- **Wikipedia**（<http://en.wikipedia.org>）— 在过去几年里，Wikipedia 已成为获取有关可用于 Linux 的商业和开源游戏信息的一个极好的资源。从 Wikipedia 中，有一个开源游戏列表（<http://en.wikipedia.org/wiki/List_of_open_source_games>）和一个通用的 Linux 游戏页面（<http://en.wikipedia.org/wiki/Linux_games>）。
