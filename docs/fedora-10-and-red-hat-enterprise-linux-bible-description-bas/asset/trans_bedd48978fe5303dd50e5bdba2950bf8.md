

# 286 第2部分：使用 Fedora 和 RHEL

| 游戏 | 描述 |
| --- | --- |
| KMines | 扫雷游戏克隆。点击安全区域并避开炸弹。 |
| Kolor Lines | 移动弹子形成五连线并得分。 |
| Konquest | 在这款多人游戏中扩张你的星际帝国。 |
| Potato Guy | 构建你自己的土豆人脸。 |
| SameGame | 消除类游戏以得分。 |

KDE 菜单上的游戏从消遣性的到极具挑战性的不等。如果你习惯了在 Windows 中玩游戏，KMines 和 Patience 看起来会像老朋友一样。KAsteroids 和 KPoker 适合无脑筋类游戏类别。

# 从 Fedora 存储库添加更多游戏

随着 Fedora 继续其作为红帽企业级 Linux（RHEL）产品试验场的角色，一些仅限软件的软件包被从所谓的 Core（核心）中移出。幸运的是，其中许多包被推入了 Fedora Extras。随着 Fedora Extras 和 Core 的合并，所有游戏现在都回到了主仓库。

由于 Fedora Games SIG（特别兴趣小组）是一项持续进行的倡议，你可以打开 PackageKit 并选择游戏，检查 Fedora 项目 网站查看是否有比表 7-3 所示更多的 Fedora 可用游戏。

你可以从此书随附的 Fedora DVD 安装每个游戏。Fedora 存储库中的大多数（但不是所有）游戏都包含在 DVD 中。要检查后来添加的软件包，输入 `yum groupinfo games`。要安装 Fedora 存储库中的游戏版本，使用以下类型，将游戏替换表 7-3 列出的名称：

```
yum install game
```

表 7-3：Fedora 中的游戏

| 游戏 | 描述 |
| --- | --- |
| Abe (abe) | 滚动、平台跳跃类游戏。 |
| Beneath a Steel Sky (beneath-a-sky) | 追溯到 1990 年代初期的流行未来城市冒险游戏。 |
| BSD Games (bsd-games) | 基于文本的卡牌游戏和冒险游戏。 |
| BZFlag (bzflag) | 3D 多人坦克战游戏。 |

# 第 7 章：Fedora 和 RHEL 中的游戏

| 游戏 | 描述 |
| --- | --- |
| Celestia (celestia) | OpenGL 实时空间模拟。 |
| CGoban (cgoban) | 用于玩围棋的 X 盘。 |
| Crystal Stacker (crystaler) | 当水晶掉落时，匹配三个或更多同色的。 |
| Cannon Smash (csmash) | 3D 网球游戏。 |
| Enigma (enigma) | ATARI 游戏的克隆。 |
| Extreme Tuxracer (extremetuxacer) | 具有 Tux 的 3D 赛车游戏。 |
| GL-117 (gl117) | 飞行模拟器（3D OpenGL）。（运行 shell。） |
| Flight Gear (FlightGear) | 飞行模拟器。 |
| FooBilliard (foobilliard) | OpenGL 台球游戏。 |
| Fortune (fortune) | 显示围棋的程序。 |
| Freeciv (freeciv) | Freeciv 多人策略游戏。 |
| Freedom (freedom) | Doom 引擎的开源移植（带有 prboom 软件包）。 |
| Freedroid (freedroid) | 以 Tux 为主角的角色扮演游戏。 |
| Freedroid RPG (freedroidpg) | Freedroid 主题。 |
| Gnofract 4D (gnofract4d) | 用于绘制分形的 Gnome 程序。（在 Graphics 菜单下。） |
| Chess (chnuss) | GNU 象棋程序。 |
| gnogo (nugo) | 基于文本的围棋程序。（通过 gnogo 命令可用。） |
| Rhino (rhino) | GNOME Base的反向游戏。 |
| Lacemaking (lacemaking) | 排序不同类型的飞船游戏。 |
| Lincy (incity-ng) | 构建模拟城市。 |
| LMables (imarbles) | Atomix 克隆，你需要找出弹子。 |
| LucidLife (lucidlife) | 威生命模拟器。 |
| NetHack (nethack) | 探索地下城的单人 Rogue 类游戏。 |
| Neverball (neverball) | 让球通过障碍赛。 |
| Maelstrom (maelstrom) | 宇宙战斗游戏。 |
| Nexuiz (nexuiz) | 以死亡赛为向的第一人射击游戏（多人）。 |

# 第二部分：使用 Fedora RHEL

| 游戏 | 描述 |
| --- | --- |
| Powermanga (powermanga) | 街机 2D 射击游戏。 |
| Cascade (cascade) | 经典谜游戏。 |
| Quake 3 Arena Engine (quake3) | Quake 3 Arena 引擎，用于玩基于此引擎的第一人射击游戏。 |
| Quake 3 Demo (quake3-demo) | Quake 3 锦标赛演示程序（将下载文件）。 |
| Raidem (raidem) | 俯视 2D 射击游戏。 |
| Rogue (rogue) | 经典冒险游戏的图形版本。 |
| Scorched Earth (scorched3d) 基于经典 DOS 游戏 Scorched Earth 的游戏。 |
| Sirius (sirius) | Gnome 跳黑棋。 |
| Sopwith (sopwith) | sopwith 游戏的 SDL 移植。（通过 `sopwith` 命令可用。） |
| Starfighter (starfighter) | Project: Starfighter，太空街机游戏。（通过 `/usr/games/starfighter` 命令可用。） |
| SuperTux (supertux) | 类似于 Mario Bros 的跳跃游戏。 |
| TORCS (torcs) | 开源赛车模拟器。 |
| The Ur-Quan Masters (uqm) | The Ur-Quan Masters，经典游戏 Star Control II 的移植。 |
| Vega Strike (vegaastrike) | 太空飞行模拟器（3D OpenGL）。 |
| Virus Killer (viruskiller) | 病毒入侵电脑的疯狂射击游戏。 |
| Battle for Wesnoth (wesnoth) | 奇幻主题回合策略游戏。 |
| Worminator (worminator) | 多关射击游戏。 |
| Chess (xboard) | X Window 棋盘。 |
| X Pilot (xpilot-ng) | 太空街机游戏。 |
| xplanet (xplanet) | 将行星图像渲染到 X 窗口。 |
| Zasch (zasch) | 增强功能的游戏。 |

