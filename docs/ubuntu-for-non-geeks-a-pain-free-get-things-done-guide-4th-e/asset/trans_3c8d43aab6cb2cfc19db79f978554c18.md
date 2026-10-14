

GNOME（GNOME 版的日本弹珠匹配游戏 Same Game）、Tali（用骰子玩的古罗马扑克形式）、Iagno（Reversi 的 GNOME 克隆版）、Nibbles（那种老式的贪吃蛇游戏）、Five or More（基于老 Windows 游戏 Color Lines 的匹配游戏）、Robots（一个奇怪的小“经典”游戏，你要在其中躲避机器人）、Blackjack 和 Chess。

![](img/f7cef0df22f9dba5a41777808c98eece_344_0.png)

图 17-2：Tetravex

![](img/f7cef0df22f9dba5a41777808c98eece_344_1.png)

图 17-3：Klotski

这些游戏捆绑为一个名为 GNOME Games 的单一软件包。要通过 Ubuntu 软件中心下载并安装该软件包，只需搜索 gnome-games，然后安装它。安装完成后，游戏将出现在应用程序菜单的游戏部分。

## 17A-2：安装一些 Linux 经典游戏：Frozen Bubble、Tux Racer 和 Pingus

还有一些其他游戏可能被称为 Linux 经典游戏，要么是因为它们是 Linux 原创，要么是因为它们以企鹅为主题，以纪念 Linux 可爱的企鹅吉祥物 Tux。其中最著名且最受欢迎的是 Frozen Bubble（图 17-4）。Frozen Bubble 堪称终极 Linux 经典：它为 Linux 编写，以 Linux（企鹅）为主题，而且 Linux 版本总是第一个发布。此后它已被移植到 Mac OS、Windows，甚至 iPhone 和 Android 系统，但 Frozen Bubble 的灵魂纯粹是企鹅。

![](img/f7cef0df22f9dba5a41777808c98eece_345_0.png)

图 17-4：Frozen Bubble

Frozen Bubble 的目标很简单：通过匹配相同颜色的气泡清除屏幕，然后进入下一关。这听起来可能很无聊，但别担心——你很快就会上瘾。

要获取 Frozen Bubble，在 Ubuntu 软件中心搜索 frozen-bubble 并安装它。然后你可以通过选择 应用程序 ▸ 游戏 ▸ Frozen-Bubble 来运行 Frozen Bubble。

另一个你可能感兴趣的 Linux 主题游戏是 Extreme Tux Racer（图 17-5）。这是一款相当奇怪（但有趣）的赛时游戏，你需要引导 Tux 在一条长长的冰山小道上滑行。不过，你应该注意，除非你有加速显卡，否则 Extreme Tux Racer 会运行得非常缓慢。如果你不确定你的电脑能否胜任，就试试看吧——反正它是免费的！

要安装 Extreme Tux Racer，在 Ubuntu 软件中心搜索 extreme tux racer 并安装它。它将出现在游戏菜单中。

与 Extreme Tux Racer 不同，Pingus（图 17-6）是一款没有特殊图形要求的游戏。它是一款迷宫游戏，基于老经典游戏 Lemmings。你的目标是带领你的一群可爱的小企鹅安全到达每个关卡的终点，不要让它们在等待它们的危险障碍物上撞得粉碎。游戏附带 22 个可玩关卡，如果你感觉冒险，你可以尝试玩一些未测试的关卡——有超过 200 个！有关如何玩这些额外关卡的说明，请访问 http://pingus.seul.org/faq.html/。

要玩 Pingus，在 Ubuntu 软件中心搜索 pingus 并安装它。你会在预期的位置找到它，在游戏菜单中。

![](img/f7cef0df22f9dba5a41777808c98eece_346_0.png)

图 17-5：Extreme Tux Racer

![](img/f7cef0df22f9dba5a41777808c98eece_346_1.png)

图 17-6：Pingus

## 3D 游戏

我到目前为止提到的大多数游戏都有一点……嗯……二维。当然，2D 游戏可以很有趣——我肯定已经把我生命的很大一部分浪费在数独上——但它们没有那种从射击成群的外星人或把高性能跑车撞向墙壁中获得的刺激感。

不幸的是，游戏设计师传统上忽视 Linux 而专注于规模大得多的 Windows 市场，因此直到几年前，可供选择的 Linux 友好型 3D 游戏很少。随着企鹅的日益流行，人们开始注意到了这一点，现在越来越多的 Windows 游戏附带了 Linux 版本。

开源游戏社区也取得了长足的进步，现在有一些质量非常高的游戏。在本节中，我将介绍我最喜欢的几款游戏，首先确保你的电脑能够承受 3D 图像的压力。

## 检查硬件加速

要玩 3D 游戏，你需要一张能够处理硬件加速的显卡。如果没有硬件加速，你的电脑处理器必须自己尝试完成所有花哨的图形渲染（这并不是它的设计用途），因此你的游戏运行速度会慢得像蜗牛，甚至根本无法运行。大多数现代显卡都内置了某种硬件加速支持，但是否启用取决于你显卡的 Linux 驱动程序状态。你可以在 https://wiki.ubuntu.com/HardwareSupportComponentsVideoCards/ 了解你的显卡的 3D 支持情况。

如果你只是想知道是否具有玩游戏所需的最低加速级别，请打开终端（应用程序 ▸ 附件 ▸ 终端），输入 glxinfo | grep rendering，然后按 ENTER。（该垂直线是“管道”符号，通常可以通过按 SHIFT 和 \ 键插入。）如果收到 glxinfo 未安装的消息，请使用 Ubuntu 软件中心安装 mesa-utils，然后重试。

如果硬件加速已启用，你将在终端中看到 direct rendering: Yes。这是个好消息，因为这意味着你可以跳到下一节，尽情享受三维游戏的乐趣。

如果你收到的消息是 direct rendering: No，则需要安装不同的图形驱动程序才能使硬件加速工作。请参阅第 394 页的“Games/Compiz Don’t Work: Installing Accelerated Graphics Drivers”以获取说明。

> 注意 许多 Linux 默认图形驱动程序无法处理抗锯齿，这是一种去除图形锯齿边缘使其看起来更平滑、更逼真的功能。如果你不能没有抗锯齿，你还应该参阅第 21 章，了解安装更好图形驱动程序的信息。

