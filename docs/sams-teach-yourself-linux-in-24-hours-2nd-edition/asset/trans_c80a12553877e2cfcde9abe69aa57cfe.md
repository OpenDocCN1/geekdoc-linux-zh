
Moves are entered by specifying the column and row as a letter and number, as in the following example:

```
# gnuchess
Enter [moves] minutes[:sec] [increment][+]:
Computer
GNU Chess
```

```
8 : *R *N *B *Q *K *B *N *R
7 : *P *P *P *P *P *P *P *P
6 : + + + + + + + +
5 : + + + + + + + +
4 : + + + + + + + +
3 : + + + + + + + +
2 : P P P P P P P P
1 : R N B Q K B N R
a b c d e f g h
Playing without hashfile
1: White
Your move is?
Human
```

如果你不想指定计时器，只需在开始游戏后按 Enter 键即可。要将兵从底排向上移动两格，输入 e2e4，然后按 Enter 键。计算机随后会走子，并且棋子新位置会在你的显示器上更新。gnuchess 程序拥有超过 23 个命令行选项，并提供显示对弈模式、提示和计时游戏等功能。更多信息请参阅 gnuchess 手册页。

## 使用 Emacs 游戏

久负盛名的 emacs 编辑器（在第 14 小时“文本处理”中讨论过）不仅可以编辑文本、阅读邮件和处理你的约会，还附带了 18 种古怪的游戏和模式，可供你打发时间，例如 doctor、dunnet、psychoanalyze、pinhead 和 yow。

要玩文本冒险游戏 dunnet，请从命令行使用 emacs：

```
# emacs -batch -l dunnet
Dead end
You are at a dead end of a dirt road. The road goes to the east.
In the distance you can see that it will eventually fork off. The trees here are very tall royal palms, and they are spaced equidistant from each other.
```

这里有一把铲子。
>

该命令行启动游戏。在 > 提示符处，输入诸如 inventory、look 或 go east 之类的命令。要结束冒险，输入 quit。

## X Window 系统的游戏

在本节中，你将了解几种 X11 游戏。你可以玩的游戏超过二十几种，但与其全部讨论，下面几页重点介绍了几款最适合策略和动作的游戏。

如果你喜欢玩棋盘游戏，运气不错！本书的 CD-ROM 上有几种不错的 X Window 系统棋盘游戏。想要更多刺激？试试一些街机视频游戏——你一定能找到喜欢的。以下是其中仅有的几个列表：

- abuse——X 的未来战斗游戏
- acm——X 的空中战斗模拟器
- koules——X 的撞球撞墙游戏
- paradise——网络对战游戏
- scavenger——X11 版的 Lode-runner
- xchomp——经典的类似 Pac-Man 的游戏
- xdemineur——扫雷类型游戏
- xjewel, xxtrojka, xbl——类似俄罗斯方块的游戏
- xlander——月球着陆游戏
- xpilot——网络对战游戏
- xpuzzles——X11 的一系列益智游戏

## 使用 xboard 客户端玩国际象棋

国际象棋是一款经典游戏，你面临的主要挑战之一就是与电脑对弈。要在 X11 中玩国际象棋，请使用 xboard 客户端。该程序使用 GNU 国际象棋引擎，可以通过互联网或电子邮件对弈。

xboard 客户端（见图 20.5）识别许多 X11 Toolkit 选项，例如几何设置，并有 54 个不同的命令行选项。如果你的显示器小于 1024×768 像素，请使用 -size 或 -boardSize small 命令行选项使棋盘适合你的屏幕，如下所示：

```
# xboard -size small &
```

图 20.5
xboard X11 客户端可在你的显示器上、通过互联网或通过电子邮件玩国际象棋。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_464_0.png)

该命令行以较小的棋子启动 xboard。有关使用 xboard 的更多详细信息，请参阅 xboard 和 gnuchess 手册页。

## 玩 X11 扑克牌接龙

如果你喜欢玩纸牌接龙游戏，你会喜欢 xpat2 X11 客户端。该程序（见图 20.6）提供 14 种不同的接龙游戏，具有计分、提示、内置帮助和声音功能。像这样从终端窗口的命令行启动游戏：

```
# xpat2 &
```

图 20.6
X11 的 xpat2 接龙游戏提供 14 种不同的纸牌游戏。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_464_1.png)

xpat2 游戏由 Heiko Eissfeldt 和 Michael Bischoff 创建，位于 /usr/X11R6/bin 目录下。更多详细信息，请阅读 xpat2 手册页。

## 为 X11 玩双陆棋

对于双陆棋迷来说，xgammon 客户端（见图 20.7）提供了数小时的乐趣和练习。该游戏由 Lambert Klasen 和 Detlef Steuer 制作，需要 X Window 系统，并在 800x600 像素显示器上舒适运行。

像这样从终端窗口的命令行启动 xgammon：

```
# xgammon &
```

图 20.7
X11 的 xgammon 游戏提供多种玩法，例如电脑对人类，并提供具有挑战性的游戏。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_465_0.png)

xgammon 客户端有 21 个不同的命令行选项。若想尝试有趣的变化，可以观看电脑与自己对弈：

```
# xgammon -g cvc &
```

这将启动 xgammon 游戏，以便你观看对局。你也可以通过编辑棋盘并在游戏前将双陆棋子放置在不同位置来创建自己的挑战游戏。有关 xgammon 的详细信息，请阅读其手册页。

## 为 X11 玩 Galaga

视频动作街机游戏可以非常有趣，尤其是当它们具有出色的图形和音效时。如果你喜欢射击游戏，你会喜欢 Joe Rumsey 的 xgal 游戏。该 X11 客户端具有简单的键盘界面。

xgal 游戏（见图 20.8）有六个不同的命令行选项，但你可以在终端窗口中输入以下内容无需任何选项即可启动程序：

```
# xgal &
```

图 20.8
X11 的 xgal 游戏具有精美的街机动作和良好的音效。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_466_0.png)

开始游戏，按空格键。使用左右光标键移动你的飞船在屏幕上，并使用空格键射击。

## 使用 X11 客户端 xboing 打破乐趣

xboing 由 Justin C. Kibell 制作，是 X Window 系统的快节奏、街机品质的球拍和球游戏。该游戏具有出色的图形和音效，并提供数小时的乐趣。你可以从终端窗口的命令行启动 xboing 程序。游戏需要至少 1024×768 像素的显示器。

默认情况下，xboing 不使用声音，因此如果你想在游戏时听到声音，必须使用 -sound 命令行选项。使用 -speed 选项在玩游戏后设置球的动作速度以微调挑战：

```
# xboing -sound -speed 7
```

该命令行以启用声音和非常快的球速启动 xboing。另一个不错的选项是 -grab，它会将你的光标保持在 xboing X11 窗口内，防止你意外激活其他窗口而错过任何动作。有关玩此游戏的更多详细信息，请参阅 xboing 手册页。

## 为 X Windows 玩 Quake

Quake 由 id Software 制作，是 Doom 的后续游戏，Doom 是近年来风靡个人电脑界的最受欢迎的街机游戏之一。你在本书的 CD-ROM 上找不到副本，但你可以下载适用于 Linux 和 X11 的 Quake 版本。

你需要从 ftp://www.cdrom.com/pub/idgames/quake/ 下载 quake106.zip 共享软件资源文件（除非你拥有 Quake 副本），以及从 http://www.mikrus.pw.edu.pl/ids/quake/files.html 下载 quake.x11-1.0-1386-unknown-linux2.0.tar.gz 文件。按照安装说明为 OpenLinux 安装此版本的 Quake。Quake II 粉丝和有兴趣为互联网或网络游戏设置 Quake 服务器的 Linux 用户可以查看 xqf Quake 服务器浏览器和启动器。浏览至 http://www.linuxgames.com/xqf/。

导航到你安装 quake 的目录，并像这样从命令行启动 Quake：

```
# quake.x11
```

游戏以演示模式启动（图 20.9 显示了一些动作）。窗口可以用鼠标调整大小或在桌面上拖动。

图 20.9
玩 Linux 版 Quake 时不要丢掉你的头！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_467_0.png)

