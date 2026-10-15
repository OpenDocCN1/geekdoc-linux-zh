
各种开源游戏来自 Fedora 和 RHEL 并在 X 中运行。Fedora 的 GNOME 和 KDE 环境都包含了一组随这些桌面默认安装的游戏。此外，还可以从 Fedora 仓库中安装更多游戏。

Fedora 游戏近期的增长大部分来自 Fedora Games SIG（特殊兴趣小组）。你可以查看 SIG 的活动，以获取其他感兴趣尚未进入 Fedora 的游戏信息：http://fedoraproject.org/wiki/SIGs/Games。事实上，如果你知道某个在 Linux 中运行的流行游戏目前未出现在 Fedora 中，那么 Fedora Games SIG 之间很可能正在关于它的优缺点进行讨论。

# 第 7 章：在 Fedora 和 RHEL 中玩游戏

## 第二部分：使用 Fedora 和 RHEL

`fedora-games` 邮件列表上的讨论为我们揭示了为什么某些游戏很难为 Fedora 打包，以及为什么某些游戏因为不符合许可要求而无法进入 Fedora。例如，关于是否在 Fedora 中包含 Doom 第一人称射击游戏的讨论，是关于如何许可问题的一个有趣案例。尽管 Doom 引擎可以自由分发，但 Doom 引擎中的某些条款防止人们修改、反汇编或逆工程该软件。出于这一原因，Fedora 项目决定包含 `prboom` 开源 Doom 克隆版本和 `freedom` `doom` 数据文件。

Fedora Gaming SIG 的一项正在进行的活动是制作 Fedora 游戏 LiveCD/LiveDVD。请查看 Games LiveCD/LiveDVD 页面 (http://fedoraproject.org/wiki/SIGs/Games/GamesLive) 上预定用于实时媒体的游戏。

### GNOME 游戏

GNOME 游戏由一些旧纸牌游戏和许多看起来很像在 Windows 系统上找到的游戏组成。如果你担心离开 Windows 后会失去最喜欢的桌面消遣（如纸牌、空接龙或扫雷），请不要担心。你可以在 GNOME 游戏中找到其中许多游戏的克隆版本。

表 7-1 列出了来自 `gnome-games` 软件包的游戏。安装该包后，可以通过应用程序菜单中的“游戏”来运行这些游戏。在该版本中，该系统还可以运行某些 KDE 游戏（见表 7-2）。

| 表 7-1：GNOME 游戏 |
| 游戏 | 描述 |
| :--- | :--- |
| AisleRiot (solitaire) | 让你从 28 种不同的纸牌游戏中选择。 |
| Blackjack | 流行的纸牌游戏，你尝试凑齐 21 点。 |
| Five or More | 形成线以移除板上的彩色球。 |
| Four-In-A-Row | 掉落球以达成四连线。 |
| FreeCell Solitaire | 一种流行的纸牌游戏。 |
| lagno | 翻转黑白棋片以绕过对手。 |
| Klotski | 移动棋子让其中一个棋子逃脱。 |
| Mahjongg | 经典的亚洲棋牌。 |
| Mines | 扫雷克隆。点击安全区域并避开炸弹。 |
| Nibbles | 在屏幕上引导蠕虫并避开墙壁。 |
| Robots | Gnobots 的后期版本，包含可移动的垃圾堆，你试图让机器人在被抓住之前自毁。 |
| Same GNOME | 消除球群以获得高分。 |
| Sudoku | 经典逻辑游戏。 |
| Yahtzee | 掷骰子得分。 |
| Tetris | 移动方块以填满行。 |

### KDE 游戏

| 表 7-2：KDE 游戏 |
| 游戏 | 描述 |
| :--- | :--- |
| Asteroids | 射击飞船。 |
| Bouncing Balls | 掉落球。 |
| Chemical Compounds | 创建不同的化合物。 |
| Clickomania | 消除分组。 |
| Virtual Golf | 打一局高尔夫球。 |
| Conquest | 扩张你的帝国。 |
| Potato Guy | 构建你自己的脸。 |
| SameGame | 消除碎片。 |

要安装 Fedora 仓库中的游戏，请以 root 用户身份输入以下命令，并将 `game` 替换为表 7-3 中列出的游戏名称之一：

```bash
# yum install game
```

表 7-3 包含了 Fedora 仓库中不断增长的游戏列表示例。Fedora 中现在有超过 170 个游戏软件包。除另有说明，否则表 7-3 中的所有游戏都可以从应用程序菜单的“游戏”列表中启动。

#### 表 7-3：Fedora 中的游戏

| 游戏 | 描述 |
| --- | --- |
| Abe (`abe`) | 卷轴、平台跳跃、古代探索游戏。 |
| Beneath a Steel Sky (`beneath-a-steel-sky`) | 20 世纪 90 年代流行的商业虚构冒险游戏；设定在一个压抑的未来城市。 |
| BSD Games (`bsd-games`) | 追溯到 20 世纪 70 年代早期 UNIX 系统的文本牌牌和冒险游戏。（从 shell 运行。） |
| BFlag (`bzflag`) | 3D 多玩家坦克游戏。 |
| Celestia (`celestia`) | OpenGL 实时视觉空间模拟。（在“其他”菜单可用。） |
| CGoban (`cgoban`) | 用于下围棋的 X 盘。 |
| Crystal Stacker (`crystal-stacker`) | 作为水晶体，匹配三个或更多相同颜色。 |
| Cannon Smash (`csmash`) | 3D 乒乓。 |
| Enigma (`enigma`) | ATARI 游戏 Oxyd 的克隆。 |
| Flight Gear (`FlightGear`) | 飞行模拟软件。 |
| FooBilliard (`foobilliard`) | OpenGL 台球游戏。 |
| Fortune (`fortune-mod`) | 显示运气的程序。（通过输入 `fortune` 命令可用。） |
| Freeciv (`freciv`) | Freeciv 多玩家策略游戏。 |
| Freedom (`freedom`) | Doom 游戏引擎的数据（带有 `prboom` 软件包，它提供了 doom 引擎的开源移植）。 |
| Freedroid (`freedroid`) | C64 游戏 Paradroid 的克隆。 |
| Freedroid RPG (`freedroidpg`) | 以 Tux 为英雄的角色游戏 Freedroid 主题。 |
| GL-117 (`gl-117`) | 动作飞行模拟器。 |
| Gnofract 4D (`gnofract4d`) | Gnofract 4D 是一个基于 Gnome 的绘制分形的程序。（在“图形”菜单可用。） |
| Chess (`gnuchess`) | GNU 象棋程序。配合 socalled 软件包提供图形化国际象棋游戏。 |
| gnogo (`gnogo`) | 文本程序。（通过输入 `gnogo` 命令可用。） |
| Grhino (`rhino`) | 基于 GNOME 的黑白游戏。 |
| Lacewing (`lacemaking`) | 拥有不同类型飞船的小行星游戏。 |
| Lincity (`lincy-ng`) | 构建的模拟城市。 |
| LMarsbles (`lmbles`) | Atomix 克隆，你用大理石创建形状。 |
| LucidLife (`lucidlife`) | 康威伊生命模拟器。 |
| NetHack (`nethack`) | 单玩家类 Rogue 游戏，你可以在其中探索地下城。 |
| Neverball (`neverball`) | 让球滚过障碍赛。 |
| Maelstrom (`Maelstrom`) | 空间战斗游戏。 |
| Nexuiz (`nexuiz`) | 以死亡赛为主的第一人称射击（多人）。 |
| Powermanga (`powermanga`) | 街机 2D 射击游戏。 |
| PPRacer (`ppracer`) | 特色 Tux 的 3D 赛车。 |
| Qascade (`qascade`) | 经典益游戏。 |
| Raidem (`raidem`) | 俯视角 2D 射击游戏。 |
| Rogue (`rogue`) | 经典冒险游戏的图形版本。 |
| Scorched Earth (`scorched3d`) | 基于经典 DOS 游戏 Scorched Earth 的游戏。 |
| Sirius (`sirius`) | 用于 Gnome 的黑白游戏 |
| Sopwith (`sopwith`) | 该游戏的 SDL 移植。（通过输入 `sopwith` 命令可用。） |
