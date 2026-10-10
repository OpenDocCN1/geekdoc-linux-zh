
$ glxinfo | grep rendering

direct rendering: Yes

此示例显示支持直接渲染。如果不支持，输出将显示 No 而不是 Yes。即使不支持 DRI，您可能仍可以使用来自 NVIDIA 的高端显卡获得最佳游戏体验，ATI 略次之。虽然 DRI 支持可能很重要，但许多游戏支持 OpenGL 渲染，这是 NVIDIA 和 ATI 显卡都支持的功能。

# 第二部分：使用 Fedora 和 RHEL

## 284

| 游戏名称 | 描述 |
|---|---|
| KGrunner | 策略益智游戏。 |
| KJumping Cube | 点击方格增加数字并占领邻近方格。 |
| KMines | 扫雷克隆。点击安全区域并避开炸弹。 |
| KNetWalk | 用尽可能少的回合构建局域网（LAN）。 |
| Kolor Lines | 移动弹珠以形成五连线并得分。 |
| Konquest | 在这款多人游戏中扩张你的星际帝国。 |
| KsirK | 征服整个世界。 |
| Kubrick | 一类魔方类型的游戏。 |
| Potato Guy | 构建你自己的土豆脸。 |
| SameGame | 消除游戏道具以得分。 |
| KSudoku | 日式逻辑游戏。 |

KDE 菜单上的游戏从消遣性的到极具挑战性的不等。如果你习惯在 Windows 上玩游戏，KMines 和 Patience（纸牌牌）看起来会像老朋友。KAsteroids 和 KBlocks 适合无脑游戏分类。

# 从 Fedora 仓库添加更多游戏

Fedora 仓库包含比上述表格列出的更多的游戏。由于 Fedora Games SIG（特别小组）是一项持续进行的计划，你可以检查 Fedora 项目网站，通过打开 PackageKit 窗口并选择“Games”（游戏），查看此处显示的更多游戏是否在 Fedora 中可用。

你可以从书中附带的 DVD 安装每个游戏。但是，并非 Fedora 仓库中所有的可用游戏都包含在 DVD 中。要检查后期添加的软件包，输入 `yum groupinfo games`。要从 Fedora 仓库安装某个版本的游戏，请以 root 用户身份输入以下命令，将 `game` 替换为表 7-3 列出的任一游戏名称：

```
# yum install game
```

表 7-3 包含了来自 Fedora 仓库的不断增长的游戏列表示例。现在 Fedora 中有超过 200 多个游戏包。除另有说明外，表 7-3 中的所有游戏都可以从应用程序菜单的“游戏”列表中启动。

# 第 7 章：在 Fedora 和 RHEL 中玩游戏

## 285

### 表 7-3：Fedora 中的游戏

| 游戏名称 | 描述 |
| --- | --- |
| Abe (`abe`) | 滚屏、平台跳跃、探索古代金字塔的游戏。 |
| Beneath a Steel Sky (`beneath-a-steel-sky`) | 20 世纪90 年代流行的商业科幻冒险游戏，背景为一个压抑的未来主义城市。 |
| BSD Games (`bsd-games`) | 来自 1970 年代早期 UNIX 系统的文本卡牌游戏和冒险游戏。（从 shell 运行。） |
| BFlag (`bzflag`) | 30D 多人战斗游戏。 |
| Celestia (`celestia`) | OpenGL 实时视觉空间模拟。（可在“其他”菜单可用。） |
| CGoban (`cgoban`) | 用于下棋的 X 盘。 |
| Crystal Stacker (`crystal-stacker`) | 水晶落下，匹配三个或更多相同颜色的水晶。 |
| Cannon Smash (`csmash`) | 3D 乒乓球游戏。 |
| Enigma (`enigma`) | Atari 游戏 Oxyd 的克隆。 |
| Extreme Tuxacer (`extremetuxacer`) | 以 Tux 为主角的 3D 赛车游戏。 |
| Flight Gear (`FlightGear`) | 飞行模拟软件。 |
| FooBilliard (`foobilliard`) | OpenGL 台球游戏。 |
| Fortune (`fortune-mode`) | 一个通过输入 `fortune` 命令来显示运势的程序。） |
| Freeciv (`freeciv`) | Freeciv 多人策略游戏。 |
| Freedom (`freedom`) | Doom 游戏引擎的数据文件（配合 `prboom` 包使用，该包提供了 doom 引擎的开源端口）。 |
| Freedroid (`freedroid`) | C64 游戏 Parroid 的克隆。 |
| Freedroid RPG (`freedroidpg`) | Freedroid 主题的角色扮演游戏。 |
| GL-17 (`gl-17`) | 以 Tux 为主角的 3D 赛车游戏。 |
| Gnofract4 (`gnofract4`) | Freedroid 主题的角色扮演游戏。（可在“其他”菜单可用。） |
| Chess (`chess`) | 棋服务器（ICS）提供的图形界面。棋游戏。 |
| Gnogo (`gnogo`) | 用于下棋的 X 盘。（在图形可用。） |
| Rhino (`rhino`) | 棋服务器（ICS）提供的图形界面。棋游戏。 |
| Laceways (`laceways`) | 空间游戏。 |

## 286 第二部分：使用 Fedora 和 RHEL

| 游戏名称 | 描述 |
| --- | --- |
| Lincy (`lincy`) | 构建城市。 |
| Marbles (`marbles`) | Rogue 类游戏。 |
| Lucidlife (`lucidlife`) | 命运。 |
| Neth (`neth`) | 探索地下牢。 |
| Neverball (`neverball`) | 多人游戏。 |
| Maelstrom (`maelstrom`) | 策略游戏。 |
| Powermanga (`powermanga`) | 策略。 |
| Qcascade (`qcascade`) | 第一人射击。 |
| Quake3 (`quake3`) | 第一人射击。 |
| Quake-demo (`quake-demo`) | 第一人射击。 |
| Raid (`raid`) | 经典主题。 |
| Scorched (`scorched`) | 经典主题。 |
| Sirius (`sirius`) | 开源游戏。 |
| Sopwith (`sopwith`) | 空间游戏。 |
| Starfighter (`starfighter`) | 经典主题。 |
| Superux (`supertux`) | 经典主题。 |
| Torcs (`torcs`) | 赛车游戏。 |
| Uqam (`uqam`) | 经典主题。 |
| Vega (`vega`) | 3D。 |
| Viruskiller (`viruskiller`) | 入侵类游戏。 |
| Wesoth (`wesoth`) | 幻想主题。 |
| Worminator (`worminator`) | 多人。 |
| Xboard (`xboard`) | 棋。 |
| Xilot-ng (`xilot-ng`) | 空间。 |

## 287

| 游戏名称 | 描述 |
| --- | --- |
| Xplanet (`xplanet`) | 渲染图像。 |
| Zasx (`zasx`) | 星星风格。 |

# 象棋游戏

象棋是计算机上最早运行的游戏之一。虽然游戏本身没有改变，但在计算机上的玩法已经发生了。Fedora 中提供的可用象棋程序可以让你与电脑对战（文本或图形模式）、让电脑自己对战，或重玩游戏。你可以通过象棋服务器（ICS）在互联网上与其他对战。

`xboard` 程序是一个基于 X 的游戏，为 `gnuchess` 提供图形界面。GNU Chess（由 `xboard` 和 `gnu` 包表示）自称为一个社区象棋程序。它有许多贡献者，并寻求在象棋社区之间促进“更开放友好的共享环境”。使用 `xboard`，你可以鼠标移动棋子。

要与电脑对战，请在终端窗口输入 `xboard`。只需通过鼠标移动棋子。在 `xboard` 窗口中，选择 Mode -> Two Machines 让电脑自己对战。图 7-1 显示了正在进行的双人游戏。

你可以通过连接到象棋服务器使用 `xboard` 进行在线对战。要作为 ICS 启动 `xboard`，输入以下命令行：

```
$ xboard -ics -icshost name
```
