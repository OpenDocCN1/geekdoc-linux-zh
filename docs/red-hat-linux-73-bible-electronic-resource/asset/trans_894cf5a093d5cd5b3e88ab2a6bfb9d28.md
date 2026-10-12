
- TransGaming Technologies (www.transgaming.com) — 该公司的使命是将其他平台的游戏移植到 Linux 上。
- Tux Games (www.tuxgames.com) — 如果您准备好购买游戏，Tux Games 网站专门用于销售 Linux 游戏。除了提供 Linux 游戏新闻和产品外，该网站还列出了其畅销游戏，并发布了即将发布游戏的公告。

如果您对开发自己的游戏感兴趣，请尝试访问 Linux 游戏开发中心（http://lgdc.sunsite.dk）。

## 图形化游戏界面

大多数专门为 Linux 创建且需要图形界面的新游戏都提供了在 X 窗口系统下运行的版本。

## X 窗口系统

X 窗口系统（X）是每个 Red Hat Linux 桌面默认使用的图形界面。由于每个人都拥有 X，因此大多数新游戏都提供 X 版本。因为 X 没有为游戏提供专用的图形屏幕，所以性能可能会下降。如果你只需要一个 GUI 来玩游戏，X 中存在更多的开销，这些开销用于运行桌面和管理 X 应用程序，这超出了实际需求。

> **提示：** 通常是 X 窗口管理器消耗了大部分处理能力。如果你想在 X 中运行游戏，可以考虑使用 twm 窗口管理器，它消耗的系统资源非常少。

## WineX

TransGaming Technologies (www.transgaming.com) 正在开发基于 WINE 的产品，可在 Linux 中运行 Windows 游戏。使用 WineX，你目前已经可以在不做任何修改的情况下运行数十款为 Windows 系统创建的游戏。你可以以订阅方式从 TransGaming 下载 WineX。

## OpenGL 支持

许多 Linux 高级游戏依赖于 OpenGL (www.opengl.org) 图形环境进行高性能图形渲染。要查看依赖 OpenGL 的游戏（以及其他应用程序）列表，可以参考在 OpenGL 网站（www.opengl.org/users/apps_hardware_applications/linux_apps.html）上维护的“Linux 应用程序和工具”列表。

如果你没有较新型号的计算机，那么你现有的视频卡可能不支持当今某些要求较高的 Linux 游戏所需的 OpenGL 功能。你可能需要考虑用较新的卡替换该卡。

要在 XFree86 中实现硬件加速，使用的是 DRI（直接渲染基础架构）GLX 驱动程序。例外情况是，nVidia 显卡没有包含 DRI 驱动程序，因为 nVidia 为其显卡提供闭源的二进制驱动程序。由于 DRI 驱动程序实际上与支持的主板上使用的芯片组兼容，因此使用相同芯片组的板卡也可能得到支持。有关 DRI 支持哪些芯片组的更具体信息，请参阅 DRI 支持网页（http://dri.sourceforge.net/status.phtml）。

对于需要 3D 硬件加速的游戏，包括一些在 TransGaming 的 WineX 下运行的游戏，TransGaming 建议使用 nVidia GeForce 显卡。不需要 3D 硬件加速的游戏应该可以在大多数受 XFree86 4.0 及更高版本驱动程序支持的显卡上正常工作。

> **提示：** 要在 Voodoo 3 显卡上使用硬件 DRI 加速，必须将显示设置调整为使用 16bpp 分辨率。对于 Voodoo 5 显卡，仅支持 16bpp 和 24bpp 分辨率。

## Linux Super VGA 库

Super VGA Library (SVGALIB) 接口可以比 X 以更具专用性的方式运行游戏。SVGALIB 游戏会充满整个屏幕。因为 SVGALIB 可以在不管理桌面和其他应用程序（如 X 所做的）的情况下运行你的游戏，所以 SVGALIB 可以比 X 更快地运行某些游戏。当你运行 SVGALIB 应用程序时，它会接管屏幕和鼠标控制权。

> **注意：** svgalib 软件包不是基本 Red Hat Linux 操作系统的一部分。但是，它包含在 Red Hat Linux FTP 站点或 Red Hat 镜像站点上。

目前，SVGALIB 背后的开发工作似乎正在滞后。此外，下一节讨论的 GGI 项目最终可能会使 SVGALIB 过时。但到目前为止，它尚未过时。要使用专为 SVGALIB 设计的游戏，你需要安装 svgalib 软件包。

> **提示：** 如果你的鼠标在 SVGALIB 中不起作用，可能需要为 SVGALIB 配置它。为此，请编辑 `/etc/vga/libvga.config` 文件。此文件包含有关配置鼠标、键盘、监视器和视频芯片以使其在 SVGALIB 中正常工作的详细信息。

## X 窗口游戏

X 窗口系统为 Red Hat Linux 和其他 UNIX 系统中的游戏从基于字符的游戏过渡到基于图形的游戏创造了巨大机遇。（基于字符的游戏将在本章后面讨论。）因此，他们不再使用代表机器人和箭头的小字符符号，而是可以实际展示小机器人和箭头的图片。

Red Hat Linux 附带了许多引人入胜且可在 X 中运行的游戏。除非另有说明，本部分中描述的所有 X 游戏都是免费的。此外，Red Hat Linux 附带的每个主要桌面环境（在第 4 章中介绍）都有一套与之相关的游戏。

## Gnome 游戏

Gnome 游戏由一些旧的基于文本的 UNIX 游戏、一些纸牌游戏以及一批看起来很像 Windows 系统中常见游戏的游戏组成。如果你担心离开 Windows 时会失去最喜欢的桌面娱乐项目（如纸牌接龙、自由单元格和扫雷），请不要害怕。你可以在 Gnome 游戏中找到其中许多。

表 7-1 列出了通过从主 Gnome 菜单选择“程序 → 游戏”后可用的游戏。

**表 7-1：Gnome 游戏**

| 游戏 | 描述 | 游戏 | 描述 |
| :--- | :--- | :--- | :--- |
| AisleRiot (纸牌接龙) | 允许你从 28 种不同的纸牌接龙游戏中进行选择。 | Chess | X 中的 Gnuchess 游戏。（运行 xboard 和 gnuchess 命令。） |
| Chromium-Setup | 为 Chromium 设置技能级别、屏幕大小和声音等选项。 | Chromium | 在这款动作游戏中，你向战场上的部队提供物资。 |
| FreeCell | 一种流行的纸牌接龙游戏。 | FreeCiv (Engels 贴图集) | 在这款策略游戏中，你试图领导你的文明消灭所有其他文明。（使用 Engels 贴图集来表示城市、海洋和其他地形。） |
| FreeCiv (Trident 贴图集) | 在这款策略游戏中，你试图领导你的文明消灭所有其他文明。（使用 Trident 贴图集来表示城市、海洋和其他地形。） | FreeCiv Server (新游戏) | 玩 FreeCiv 所需的服务器程序。 |
| Gataxx | 一款棋类游戏，你翻转圆圈来吃掉敌方的棋子。 | Glines | 匹配一排五个彩色球来得分。 |
| Gnibbles | 在避开墙壁的同时引导一条蠕虫在屏幕上移动。 | GnobotsII | Gnobots 的后续版本，包含可移动的垃圾堆。 |
| Gnome Mines | 扫雷克隆版。点击安全区域并避开炸弹。 | Gnome-Stones | 在一个洞穴中移动，收集钻石，并避开岩石。 |
| Gnotravax | 俄罗斯方块四克隆版。移动方块，使每一侧的数字对齐。 | Gnotski | 移动棋子，以便让一个棋子逃脱。 |
| GTali | Yahtzee（大富翁掷骰游戏）克隆版。掷骰子以填满类别。 | Iagno | 翻转黑白棋子以操纵超过对手。 |
| Maelstrom | 驾驶太空船穿越小行星带。 | Mahjongg | 经典的东方牌类游戏。 |
| Same Gnome | 消除成群的球以获得高分。 | Tux Race | 驾驶企鹅在肚子上滑下山坡进行比赛。 |
| xbill | 防止 Bill 窃取操作系统。敲倒 Bill 并返回 OSS。 | xbl | 在这款类似俄罗斯方块的游戏中，放下 3D 方块并将它们拼合在一起。 |
| xpilot | 在这款多人 2D 空中战斗游戏中击落飞机。 | Xsnow | 为你的桌面添加下雪的背景。 |

## KDE 游戏

如果你安装 KDE，桌面将附带许多游戏。这些游戏也会显示在 Gnome 菜单中。要从 Gnome 菜单查看 KDE 游戏，请选择 KDE 菜单 → 游戏，然后从以下类别中选择你想要的游戏：街机、纸牌、棋类、战术/策略。KDE 中可用的游戏列在表 7-2 中。

> **交叉引用：** 关于 KDE 桌面的描述，请参见第 4 章。

