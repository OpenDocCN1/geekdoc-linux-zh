
你可能需要以 root 身份登录以执行 `install` 命令。一旦你编译并运行了 Sabre，其结果将令人印象深刻（见图 24.4）。

另一个值得尝试的飞行模拟器是 FlightGear。该项目包含一个充满场景和其他图形的独立包，以及一个文档包。

FlightGear 需要一张 3D 显卡。构建它的完整源码包位于 CD 盘的 `/Source/Games/FlightGear`。

![](img/ba933c244f3be8993f8191427d25c74c_125_1.png)

### 图 24.4
Sabre 在 Linux 上提供了令人印象深刻的飞行模拟体验。

![](img/ba933c244f3be8993f8191427d25c74c_126_0.png)

与 Sabre 一样，由飞行模拟器爱好者创建的网站位于 `http://www.flightgear.org/`，拥有完整的文档、大量的图像以及邀请其他爱好者参与开发的邀请。

## 运行游戏

许多街机游戏使用不同的主题，在游戏场上移动、捕捉物体、吃东西等。其中最广为人知的之一是吃豆人（Pacman）。Linux 上有多个版本的吃豆人可用。`pacman` 程序（用于 KDE）与原始街机游戏惊人地相似（见图 24.5）。然而，它包含了幽灵组、水果以及许多小点，并遵循了吃豆人中使用的原始游戏模式。

![](img/ba933c244f3be8993f8191427d25c74c_126_1.png)

### 图 24.5
Pacman 是适用于运行 KDE 系统的吃豆人克隆版。

![](img/ba933c244f3be8993f8191427d25c74c_127_0.png)

Pacman 位于 CD 的 `/Binaries/Games/`。按照以下步骤将其安装在你的 Red Hat 6 系统上：

```
$ cp /mnt/cdrom/binaries/pacman/pacman-binary.tgz /home/nwell/part6

$ cd /home/nwells/part6

$ tar xzvf pacman-binary.tgz

$ cd pacman-0.2.4

$ make install
```

你可能需要以 root 身份登录以使用 `make` 命令。会出现许多屏幕文本。

## 最优的 Linux 策略游戏 117

或者你也可以使用这些命令从 CD 中 `/Binaries/Games/KDE` 子目录下的 `rpm` 文件向你的系统添加 KDE 游戏包。

```
# rpm -Uvh /mnt/cdrom/Binaries/Games/KDE/kdegames-sirtet-1_1_1-1rh5x_i386.rpm
```

```
## /opt/kde/bin/ksirtet
```

图 24.8 显示了一场 Ksirtet 游戏。

### 图 24.8
Sirtet 是标准 KDE 游戏包的一部分。

![](img/ba933c244f3be8993f8191427d25c74c_132_0.png)

# 25 极优的 Linux 策略游戏

![](img/ba933c244f3be8993f8191427d25c74c_132_1.png)

对于那些喜欢比街机游戏节奏更慢的人（也许你可以在读邮件的间隙玩），策略游戏提供了一个受欢迎的休息。

## 118 让 Linux 变成终极玩家

本节描述了 Linux 上的棋盘游戏、卡牌游戏等。它还包含了标准 KDE 和 Gnome 游戏包中包含的策略游戏的若干说明。

### 玩国际象棋

终策略游戏是国际象棋。Linux 从一开始就支持 `gnuchess` 基础引擎象棋，但现在有了图形界面，可以让这个强大的程序在你的桌面上变得更有趣。

要在 Linux 中玩图形化游戏，你需要两个包：游戏引擎的 `gnuchess` 以及提供界面的 `xboard`。这些包通常包含在标准的 Linux 发行版中。如果你没有它们，这两个包都包含在 CD 的 `/Binaries/Games/chess` 目录中（`rpm` 格式）。使用这些命令安装它们：

```
# rpm -Uvh /cdrom/mnt/Binaries/Games/chess/xboard-4.0.03.1386.rpm

# rpm -Uvh /cdrom/mnt/Binaries/Games/chess/gnuchess-4.0.p1793.1386.rpm
```

安装这些包后，使用此命令开始一局国际象棋：

```
$ xboard
```
