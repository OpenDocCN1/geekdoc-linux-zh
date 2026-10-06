
## 第 11 章 定制游戏 Linux 启动 CD

如果你对电脑游戏感兴趣，Linux 中有大量的机会等待着你。这里有数百种令人愉悦的游戏供你选择，而且对你如何使用它们几乎没有任何限制。能够利用硬件加速显卡的游戏也在作为开源游戏进行发行，以制作出更多令人惊叹的游戏。

在你创建一个游戏启动 CD 之后，你就可以把那张充满活力的可启动 CD 交给你的年轻人了，里面运行着你为他们精心挑选的海量游戏。或者，你也可以制作一张 CD 随身携带你喜欢的开源游戏，这样在在途中时就不会感到无聊。如今可用于游戏的开源软件如此丰富，大多数游戏启动 CD 发行版已经发展成了 DVD 发行版。

本章通过几种方法描述了你自己在组装自己的启动 CD 或 DVD 时可能会觉得感兴趣的话题：

- **游戏启动 CD——已经存在几个 Linux 游戏启动 CD 供你尝试。** 由于可用软件非常多，许多最流行的游戏启动 CD 已经扩展到了 DVD。`Games Knoppix` 的 DVD 版本为 2.7GB；SuperGamer 游戏启动 CD (`www.pclinuos.com/forum/index.php?board=31,0`) 约为 3.7GB。
- **免费游戏——免费和开源游戏（根据 GPL 或类似的许可协议分发）对于原创游戏或传统电脑游戏的克隆版来说非常丰富。你会找到数不完的纸牌牌游戏、迷宫游戏、棋盘游戏等。近年来，人们还创建了更复杂的动作和策略游戏供免费分发。

如果你想组装一个可以自由分发的启动 CD，可以查看几个可用应用程序列表。在本章的后半部分，我将带你挑选 Linux Live Game Project CD 中包含的游戏。

- **商业游戏和演示版 (demos)**——当然，许多最流行的电脑游戏是为了销售而创建的。大多数商业电脑游戏是为 Microsoft Windows 平台制作的，但一些商业游戏已经移植到了 Linux。

虽然在启动 CD 上包含大多数商业 Linux 游戏可能是不合法的，但在某些情况下，你可以获得将这些游戏包含在 Linux CD 中的许可。我们将在本章后后部分描述围绕重新分发 Linux 游戏的某些许可问题。

- **经典商业游戏**——你可能可以在启动 CD 上合法地包含一些最初为 PC 或游戏机创建的商业游戏。这并不是说因为某公司不再销售某款游戏，你直接把它包含在你的启动 CD 中就是没问题的。大多数公司不会因为游戏不再推销就简单地放弃其版权。

在某些情况下，经典游戏的权利已进入公有领域。在另一些情况下，Linux 中提供了游戏机模拟器，你可以购买游戏本身并在这些模拟器上运行。在另一种情况下，商业游戏的部分可能已经进入了公有领域，而对仍受保护的部分可能创建了开源克隆版本，以便整个游戏可以自由分发。《毁灭战士》就是这样一个游戏的例子。

- **显卡支持**——在 Linux 中获得 3D 游戏支持的一个大障碍是获取支持硬件加速的显卡驱动程序。Linux 提供了 Nvidia 和 ATI 显卡的闭源驱动程序，但重新分发这些驱动程序时受到限制，有时会阻碍这些驱动程序与同一台机器上的开源视频驱动程序良好协作。在本章的后半部分，我描述了获取驱动程序以运行更高级的 3D 图形游戏的方法。

首先，本章将带你了解一些可用的 Linux 启动 CD。然后它描述了你可以包含在自己的 CD 中的开源游戏，以便你能够自由分发你的 CD。本章还包含了对名为 Linux Live Game Project (LLGP) 启动 CD 的 Knoppix 定制版的描述。

### 第 11 章 定制游戏 Linux 启动 CD

本章将介绍关于在 CD 上包含受过或目前仍受 GPL 类型以外许可协议保护的软件的问题。这些类型的游戏包括商业销售的游戏，或者具有你可能解决或无法解决的其他许可障碍的游戏。

### 寻找 Linux 游戏启动 CD

专门用于游戏应用的 Linux CD 范围涵盖了从纯开源游戏启动 CD 到包含运行商业演示版和 3D 游戏能力的 CD 不等。要使用其中一些启动 CD，你需要特殊的显卡和大量的 RAM 才能有效运行。以下章节包含了一些游戏启动 CD 和 DVD 的示例。

#### GamesKnoppix 启动 CD 和 DVD

`GamesKnoppix` 游戏启动 CD 既有启动 CD (700MB) 版本也有 DVD (2.7GB) 版本。与许多 Knoppix 重制版不同，GamesKnoppix 移除了 OpenOffice suite（仅节省了约 200MB）和大量 KDE 应用，为大量游戏留出空间。

除了包含许多开源游戏（在本章后面描述）之外，GamesKnoppix KDE 还包含了在 Linux 中原生运行的商业游戏演示版；你可以尝试 `Marble Blast` 和 `Ghost Tanks` 等游戏的演示版，以及 `Mutant Storm` 和 `Space Tripper`。务必使用 3D 图形加速硬件来运行这些游戏。（DVD 上不提供演示版。）

对于支持的游戏 ROM 或可执行文件，可以使用以下模拟器：

- **Atari**——包含了用于运行 Atari 800、Atari 800 XL、Atari 130 XE 和 Atari 5200 的命令。
- **MAME**——多机模拟器 可能是 Linux 上最流行的游戏模拟器。MAME 经过测试可以运行 70 年代、80 年代和 90 年代的经典游戏。你需要法的 ROM 才能使用该模拟器。
- **DOS**——如果你有旧的 DOS 游戏，可以使用 `dosbox` 命令运行最初为 DOS 操作系统创建的保护模式游戏。
- **Amiga**——对于在 Commodore Amiga 500、1000 和 2000 上运行的游戏，可以使用 UAE Amiga 模拟器。这些机器基于 Motorola 68x0 芯片。
- **Nintendo**——`znmes` 工具是任天堂系统的模拟器。

游戏模拟器的存在是 GamesKnoppix 不同于其他启动 CD 的特征之一。然而，如果你没有游戏 ROM，模拟器本身就没用。不过，这张启动 CD 有约 300 个游戏让你忙碌。查看 GamesKnoppix 网站 (`http://games-knoppix.unix-ag.kl.de/gamelist-4.0.2-0.3.txt`) 获取可用游戏的列表。

GamesKnoppix 的界面是熟悉且稳定的 Knoppix 4.0.1 KDE 桌面。除了游戏模拟器，你可以在 GamesKnoppix DVD 上尝试数百种游戏。游戏菜单包含 50 多种街机游戏和近 20 种策略游戏。还有一个给玩的 Potato Guy 游戏。图 11-1 显示了 GamesKnoppix 显示游戏 (`foobilliard`)、太空游戏 (`kasteroids`) 以及一个在土豆上贴脸的游戏 (Potato Guy)。

#### PCLinuxOS SuperGamer

如果你想测试电脑硬件玩游戏的极限，SuperGamer 启动 DVD（基于 PCLinuxOS）拥有许多你可以运行的 3D 加速游戏。SuperGamer 还没有主页，但你可以从以下了解更多信息：

PCLinux OS 上的 SuperGamer 论坛 (`www.pclinux.com/forum/index.php?board=31.0`)。

为了玩 3D 加速游戏，SuperGamer 包含了 Nvidia 驱动；建议使用 Nvidia 显卡（至少为 FX5500）以获得 3D 游戏的最佳性能。

> 注意：如果你没有 Nvidia 显卡，在其他显卡上尝试使用 3D 加速时，可能会遇到驱动冲突。当我尝试在一台带有旧 Intel i810 的机器上运行时，，需要 3D 加速的游戏无法运行（提示 GLX 不可用）。我卸载了 Nvidia 驱动并重启了系统。之后，我能够使用正确的 i810 驱动运行 3D 加速。（运行并不快，因为那是一台内存较小的旧机器，但确实可以运行。）

运行这些游戏还需要大量的内存。如果内存小于 512MB 且处理器低于 1GHz，不要期望获得很好的性能。

PCLinuxOS SuperGamer DVD 包含了这些可玩的演示和 3D 游戏：

- *毁灭战士与雷神*(Doom and Quake)——DVD 上有热门的《毁灭战士 3》(`www.doom3.com`) 和《雷神 4》(`www.quake4game.com`) 第一人称射击游戏的演示。
- 《要塞风垒：敌人之地》(The Return to Castleenstein: Enemy Territory)演示 (`http://games.activision.com/wolfenstein`)。在游戏中，你可以从希姆勒和他的邪恶神秘军手中拯救世界。
- *不死球*(Neverball)——在这款动作与动作游戏中，让球通过障碍赛。你可以从 Icculus 集合 (`http://iculus.org/neverball`) 了解更多信息。该 DVD 中还包含了基于相同技术的微型高尔夫游戏《Neverbutt》。
- *BFlag*——使用这款 3D 坦克大战游戏 (`www.bf.org`) 与电脑或通过互联网组队比赛。
- *企鹅人赛手*(PlanetPenguin Racer)——在这款 3D 计时赛游戏中，帮助企山用肚子爬山 (`http://projects.planetpenguin.de/race/`) (`www.ufoai.net`)。
- *UFO：外星入侵*(UFO: Alien Invasion)——在这款战术游戏中与敌对外星战斗。
- *美国陆*(America's Army)——这款由美国陆赞助的视频游戏旨在描述士兵在军队不同职业中的训练活动。游戏包含了从训练活动到多人操作。更多信息请见 `www.americasarmy.com`。

除了游戏外，SuperGamer 还包含了一些用于数字图像（GQView, GIMP, Xsane 等）、音频（Kaboodle, KsCD 和 Xmms）和视频（Realplayer, TVtime 和 Xine）的多媒体应用程序。网络菜单还有一套良好的通信应用程序（文件传输、即时消息、电子邮件等）。

图 11-2 显示了 SuperGamer 桌面的示例，显示了《维斯诺斯之战》（Battle of Wesnoth）和 MMMS 播放器。

### 运行 Linux 游戏项目 Live CD

作为游戏 Live CD 的示例，我包含了 Linux 游戏项目 (LLGP) Live CD (`http://tuxgamers.altervista.org`)。这很好地代表了 Knoppix 如何通过定制来满足特定目的。在这种情况下，目的是玩游戏。LLGP Live CD还将游戏限制在添加的游戏和免费开源游戏中，因此在使用或分发所描述的任何游戏都没有问题。

LLGP Live CD 中包含了数百种游戏。尽管没有包含任何商业游戏或游戏演示，但该 Live CD 包含许多有趣且具有挑战性的游戏。要查看 Live CD 中包含的游戏，请参考项目的[游戏列表页面](http://tuxgamers.altervista.org/List_of_games)。

### 306 Live Linux CDs

除了游戏外，SuperGamer 还包含了一些用于数字图像（GQView, GIMP, Xsane 等）、音频（Kaboodle, KsCD 和 Xmms）和视频（Realplayer, TVtime 和 Xine）的多媒体应用程序。网络菜单还有一套良好的通信应用程序（文件传输、即时消息、电子邮件等）。

### 自定义游戏 Live Linux CD

| 游戏名称 | DEBIAN 软件包名称 | 描述 |
| --- | --- | --- |
| Circus Linux | circuslinux, circuslinux-data | 小丑们试图通过从平台发射彼此来戳破气球。 |
| Conquest | conquest-data, conquest-gl, conquest-libs, conquest-server | 多人合作太空冒险游戏。 |
| Egoboo | egoboo, egoboo-data | 类似于 NetHack 的 3D 地牢探索冒险游戏。 |
| Frozen-Bubble | frozen-bubble, frozen-bubble-data | 通过射向相同颜色的泡泡组来破破泡泡。 |
| Galaga GalagaHyperspace | xgalaga | Galaga 太空射击游戏的 X 版本。 |
| GL-117 | g1-117, g1-117-data | 动作战斗机模拟器。 |
| Heroes (SDL 版本) | heroes-common, heroes-sdl, heroes-sound-effects, heroes-sound-tracks | 在这种蠕虫风格游戏中，在收集道具时避开障碍和墙壁。 |
| Kasteroids | kasteroids | 在这款经典游戏的 KDE 版本中避开并摧毁行星。 |
| KBounce | kbounce | Jeeeball 的 KDE 克隆版。 |
| KFoulEggs | kfouleggs | 日本游戏棉花消除的 KDE 克隆版。 |
| KGoldrunner | kgoldrunner | Loderrunner 街机游戏的 KDE 克隆版。 |
| KSirtet | ksirtet | 俄罗斯方块和消除游戏的 KDE 克隆版。 |
| KSmilTris | ksmiletris | 带有笑脸的俄罗斯方块 KDE 克隆版。 |

### 表 11-1 续

| 游戏名称 | DEBIAN 软件包名称 | 描述 |
| --- | --- | --- |
| KSnakeRace | ksnake | KDE 大蛇。 |
| KSpaceDuel | spaceduel | KDE 双人太空街机游戏。 |
| KTron | ktron | 电子光子的 KDE 克隆版。 |
| Kobo Deluxe | kobodeluxe | 太空战斗游戏。 |
| Kolf | kolf | KDE 微型高尔夫。 |
| LBreakout | 1breakout2 | 反弹球游戏的克隆版。 |
| Mad Bomber | madbomber | 在 Kaboom! 的克隆版中在炸弹落地前接住它们。 |
| Mangoquest | mangoquest, mangoquest-data | 第一人称迷宫游戏《蓝芒果探险》。 |
| Neverball Neverput | neverball, neverdata | 在 Neverball 中，你通过倾斜地板让球到达目的地。Neverput 是一款 3D 高尔夫游戏。 |
| Nibbles | gnome-games, gnome-games-data | GNOME 桌面游戏中的大蛇游戏。 |
| Penguin Command | penguin-command | 通过发射导弹和智能弹来防御城市。 |
| Pinball | pinball | 弹球机模拟器。 |
| Powermanga | powermanga, powermanga-data, powermanga-base | 图形化 3D 射击游戏。 |
| Race | race | 3D 俯视角赛车游戏。 |
| Robots | gnome-games, gnome-games-data, gnome-games-extra-data | GNOME 机器人游戏。 |

### 自定义游戏 Live CD

| 游戏名称 | DEBIAN 软件包名称 | 描述 |
| --- | --- | --- |
| Slune | slune | 赛车和 3D 碰撞游戏。 |
| Starfighter | starfighter, fighter-data | 卷屏 2D 射击游戏。 |
| SuperTux | supertux, superdu-data | 2D 跳跃跑酷卷屏游戏中的 Tux 企鹅。 |
| TORCS | torcs, torcs-data, torcs-data-cars-extra, torcs-data-tracks-oval, torcs-data-tracks-road | 3D (OpenGL) 赛车模拟器 |
| Thrust | thrust | 在这款经典 Commodore 64 游戏的克隆版中从太空摧毁核反应堆。 |
| Toppler | toppler | Nebulus 游戏克隆版。 |
| Trophy | trophy, trophy-data | 2D 赛车动作游戏。 |
| Tux: A Quest for Herring | tux-aqfh | 带企鹅去寻找金鲱鱼的任务。 |
| TuxRacer | tuxracer, tuxracer-data, tuxracer-extras | 让 Tux 企鹅肚肚子滚下山进行比赛。 |
| TuxType | tuxtype | 向企鹅 Tux 学习打字。 |
| TuxKart | tuxkart, tuxkart-data, tuxkart-extras | Tux 3D 卡丁车赛。 |
| Typespeed | typespeed | 在单词在页面上穿过时打字消除它们。 |
| Wing | wing, wing-data | Galaga 风格的太空射击游戏。 |
| XBill | xbill | 防止 Windows 病毒感染电脑。 |

### 表 11-1 续

| 游戏名称 | DEBIAN 软件包名称 | 描述 |
| --- | --- | --- |
| XBlast-TNT XBlast-TNT-mini | xblast, xblast-data, xblast-sound, xblast-tnt, xblast-tnt-images, xblast-tnt-levels, xblast-tnt-mini, xblast-tnt-models, xblast-tnt-sound | 在这款太空射击游戏中炸飞对手。 |
| XKoules | koules | 基于 X 的太空动作游戏。 |
| Xscavenger | xscavenger | 用于 X 的平台类游戏。 |
| Xsoldier | xsoldier | X 士兵游戏。 |
| Xboing | xboing | X 消除游戏。 |
| Xbreaky | xbreaky | X 风格的弹球游戏。 |
| Xacer | xracer, xracer | 赛车游戏。 |
| Xscorch | xscorch | 火球地球。 |
| Zblast | zblast, zblast-data | 射击游戏。 |

# 表 11-3 LLGP 中的纸牌游戏

| 游戏名称 | DEBIAN 包名称 | 描述 |
| :--- | :--- | :--- |
| AisleRiot Solitaire | gnome-games, gnome-data | 纸牌游戏 |
| Blackjack | gnome-games, gnome-data | 黑色赌场纸牌游戏 |
| FreeCell Solitaire | gnome-games, gnome-data | 从 sol 引擎运行的免费细胞游戏 |
| Gnome Blackjack | gnome-games, gnome-data | GNOME 黑色赌场游戏 |
| Gnome FreeCell | gnome-games, gnome-data | GNOME 免费细胞游戏 |
| Gnome Solitaire Games | gnome-games, gnome-data | 为 GNOME提供的若干纸牌游戏 |
| KPoker | koker | KDE 扑克游戏 |
| Lieutenant Skat | 1skat | Skat纸牌游戏 |
| Patience | kpat | KDE Patience 纸牌游戏 |
| Penguin Canfield | ace-of-penguins | 企鹅版本的 canfield |
| Penguin Freecell | ace-of-penguins | 企鹅版本的 freecell |
| Penguin Golf | ace-of-penguins | 企鹅版本的高尔夫纸牌游戏 |
| Penguin Solitaire | ace-of-penguins | 企鹅版本的经典纸牌游戏 |
| Penguin Thornq | ace-of-penguins | 企鹅版本的 thornq 纸牌游戏 |
| PySol | pysol | 基于 Python 的纸牌游戏 |
| XSkat | 1skat | KDE Lieutenant Skat 纸牌游戏 |
| XSkat via IRC | 1skat | 通过 IRC 在线玩的 KDE Skat 游戏 |

## 商业游戏许可协议

通过专注于基于 Knoppix 构建并包含 Debian/Knoppix 软件存储库中包的 LLGP live CD，我成功规避了一些与许可相关的复杂问题。事实上，如果你想确保能够自由重新分发你构建的任何 live CD，只要你坚持使用仔细审查许可协议的成熟 Linux 发行版（Debian、Fedora 和 Gentoo）存储库中的软件，就可以避开大多数专利和版权侵权问题。

然而，有时你可能想要包含一个或多个受商业或其他非 GPL 许可涵盖的游戏。通用的法是：如果某个软件的版权所有者没有将其发布到公有领域，你就不能假设可以使用和重新分发该软件。即使所有者不再销售该产品，即使该公司已不存在，这仍然成立。

但是，在某些情况下，你可能可以在个人或重新分发的 live CD 上包含商业游戏软件。以下是一些示例：

- 商业演示版——Linux 商业游戏制作商可能乐意让你分发其商业游戏的演示版。在此之前，你需要联系制作商获取书面许可。我听说 GarageGames.com 已经允许某些 live CD 重新分发其演示版。记住，你分发的演示版可能包含一些示例材料。
- 源驱动——为了在 Nvidia 和 ATI 卡上进行高质量 3D 游戏，你需要包含来自这些制造商的闭源驱动。在许多情况下，人们认为此类驱动可以自由重新分发（参见 `https://www.nvidia.com/object/nv_swlicense.html`）。

然而，开源纯主义者认为，在分发闭源驱动时，你并不知道驱动是如何感染你的 Linux 内核的。事实上，取决于你如何配置这些驱动，它们可能会破坏你的内核使用其他视频驱动的能力（早些我提到过我的 i586 主板与 Nvidia 驱动冲突的案例）。

- 向公众发发的商业产品——某些游戏在停止作为可行产品多年后实际上被发布到了公有领域。然而，如果你想在你的 live CD 上包含此类游戏软件，你应该确保整个产品是可修改的并且可以自由重新发布的。

## 第 11 章 定制游戏类 Live Linux CD

一个稍显棘手的案例是热门的第一人称射击游戏 Doom 的免费发布。虽然该游戏发布时被允许完全可重新分发，但 Doom 共享软件 Wad 中仍留有一项条款：“你不能：修改、翻译、反汇编、反编译、反向工程或基于该软件创建衍生作品。”

由于更改代码的能力是 Fedora Linux 等软件项目的一个重要元素，该项目决定用 Freedom 包替换掉违规部分（Doom 引擎）。Freedom 是完全从头开始编写的 Doom 引擎，因此对于接收它的人来说，它是被经过了修改的。

另一个可以用来玩向公众发发的游戏的游戏软件是 ScrumVM (`scummvm.org`)。LucasArts 最初创建了 SCUM 来制作许多游戏，如《猴子岛》（Monkey Island）、《帐篷之日》（Day of the Tentacle）和《坎迪亚传说》（Legend of Kyandia）。ScrumVM 根据 GPL 发布，可以玩许多最初运行在 SCUM 上的游戏。详情请参见 ScrumVM 兼容性列表 (`scummvm.org/compatibility.php`)。

此类中已发布到公有领域的游戏包括《钢铁天空》（Beneath a Steel Sky，于 2003 年 8 月作为免费软件提供）和《亚马逊女王号》（Flight of the Amazon Queen）。这些游戏包含在某些 live 游戏 CD/DVD 中，例如 GamesKnopix DVD。

调查不同游戏软件相关许可问题的优秀地方包括处理 Linux 发行版中应包含或不包含哪些内容的邮件列表。例如，Fedora Extras 列表曾对游戏许可问题进行过多次讨论（`www.redhat.com/mailman/listinfo/fedora-extras-list`）。

## 创建 FEDORA 游戏 Live CD

为了说明如何构建你自己的游戏 CD，如下所示：

## 定制多媒体 Live CD

创建、处理和显示多媒体内容长期以来一直是 PC 用户的喜爱好。如今的计算机被认为应该让你能够播放音乐、观看电影并处理你的数字图像。免费和开源多媒体应用的改进，为那些正在组装专注于多媒体应用的基于 Linux 的 CD 的人员提供了丰富的选择。

本章涵盖的多媒体 Live CD 分为两类：

- **多媒体播放器**——通过专门播放视频、音乐和幻灯片，多媒体播放器 Live CD 可以被压缩到非常小的体积。仅占用几兆字节磁盘空间允许这些播放器完全运行在 RAM 中，而 CD 或 DVD 驱动器可以用于存放音乐或电影。
- **多媒体制作工具**——对于 Web 设计师、音乐家、图形艺术家和动画师来说，Live CD 提供了一种制作高质量数字艺术的工具手段。许多开源工具在图像处理（The GIMP）和 3D 动画（Blender）领域开始与商业产品竞争。

为了说明多媒体播放器，我在本章中增加了对 GeeXBox 的描述。除了描述如何将 GeeXBox 作为多媒体播放器使用外，我还描述了 GeeXBox Generator，它可以用于向经过重制的 GeeXBox 多媒体播放器 ISO 镜像添加内容、编码器和个人设置。

在多媒体工具箱领域，我描述了 live CD。Dybolic 包含了 100 多开源应用程序，这些应用程序可以用于专门制作和发布多媒体内容的桌面系统。

### Linux Live CD

无论你对播放还是制作多媒体内容感兴趣，有一个问题跨越这两个领域：在 Linux 中获取音频和视频内容的合法编码器。因此，在跳转到不同类型的多媒体 Live CD 之前，请阅读以下章节以了解与播放音乐和电影所需的软件相关的问题。

## 理解多媒体版权和专利问题

通过 GNU 通用公共许可证（参见 `www.gnu.org/copyleft`）和相似的许可协议对软件进行许可，自由和开源软件运动使得像 Linux 这样的自由分发操作系统成为可能。然而，从头编写软件并根据 GPL 许可这些工作可能无法无法软件的自由分发。在自由软件开发领域，没有哪个问题比多媒体更具争议。

特别是与音频和视频编码器（编码器/解码器）免费分发的问题源于几个问题，包括：

- **专利**——许多用于创建和播放商业音乐及视频的音频和视频标准包含专利技术。任何编写音乐和视频播放器的人都会面临这些版税持有者的索赔，要求为软件创建者分发的每个播放器或编码器付费。
- **《数字千年版权法案》(DMCA)**——DMCA 是美国国会于 1998 年通过的一项法案，该法规定在美国创建规避版权保护措施的技术是非法的。

软件专利索赔的威胁自人们开始分发自由软件以来就一直笼罩在自由开源软件运动之上。为了应对今天的长期斗争，主要的软件供应商一直在收集从数据库结构到你在互联网上点击购买商品的一切相关的专利组合。然而，在短期内，某些诉诉讼性的软件组件是那些与多媒体许可相关的。

从理论上说，你应该理解与你使用的每种软件相关的许可安排。现实中，我们大多数人取决于商业软件供应商或为我们消费创建和/或重新发布软件的开源软件组织的法律解释。因此，我并不是针对对书中所描述的软件可以做什么和不能做什么提供法律建议（我没有资质做这一点），而是转述关于什么和什么不被认为是多媒体自由分发软件的一般解释。

如果你是从头创建音频或视频内容，可以使用开源音频视频编码器。你用这些开源多媒体播放器创建的任何内容都可以与播放器和编码器本身一起自由分发。你甚至可以将这些编码器和播放器包含在你自己的产品中，只要你遵守与它们相关的许可（这通常要求你提供源代码）。

- **音频 (Ogg Vorbis 和 FLAC)**——Xiph 会 (`www.xiph.org`) 产生的 Ogg Vorbis 是 MP3 音频编码的高效、高质量竞争对手。Ogg 是媒体容器，Vorbis 是音频编码器。Ogg Vorbis 是一种非专利、免专利和免版税的音频格式，可以在高压缩率下产生高质量音频。
- 自由无损音频编码器 (`FLAC`) 是另一个由 Xiph.org (`http://flac.sourceforge.net`) 赞助的音频格式。FLAC 音频文件比类似的 Ogg Vorbis 或 MP3 文件大得多，但这种格式具有某些压缩功能，且没有明显的音频质量损失。
- 几乎每个适用于 Linux 的音频和视频播放器（ogg123, xmms, mplayer, vlc 以及其他）都支持 Ogg Vorbis 音频。
- **视频 (Theora)**——Theora (`www.theora.org`) 是由 Xiph.org 赞助的免费视频编码器，Theora 基于几年前发布到公有领域的 VP3 编码器（参见 `www.theora/svn.html`)。可以使用 Cinelerra (`http://cinelerra.org`) 和 `ffmpeg2theora` 等工具创建 Ogg音频/视频文件。开源视频播放器（包括 VLC 播放器、Helix 播放器、Totem 和 mplayer）可以播放 Ogg Theora 内容。

在多媒体工具箱领域，我描述了 live CD。Dybolic 包含了 100 多开源应用程序，这些应用程序可以用于专门制作和发布多媒体内容的桌面系统。

## 第 12 章 定制多媒体 Live CD

### 多媒体播放器 Live CD

对于多媒体播放器型的 Live CD，你基本上想要包含播放器应用程序（音乐、视频和图像播放器）以及获取内容的方法。另一个问题是硬件支持。为了充分利用多媒体播放器的性能，你可能希望包含对特种显卡、声卡、PCMCIA 卡和电视调谐器卡的支持。

开源音乐和图像播放器随处可见。也有开源视频播放器；但获取播放某些类型视频内容所需的解码器可能会更加棘手（这一点稍后讨论）。至于如何获取要播放的内容，多媒体播放器提供了一种或多种获取内容的方法：

- **在 Live CD 上**——如果你正在重新制作一个 Live CD 并且有可用空间，你可以添加尽可能多的能够放入 Live CD 本身的内容的内容。这样你就不需要访问 Live CD 以外的任何介质即可播放内容。
EMoviX 项目是 MobiX 项目的衍生，它是媒体播放器的一个示例，旨在让你向 Live CD 中添加视频，以便在启动时就能直接播放视频。GeeXBox 项目生成了 GeeXBox Generator，它可以让你向个人的 GeeXBox Live CD 添加解码器和内容。
- **CD 或 DVD**——由于大多数商业音乐和电影分别存储在 CD 和 DVD 上，因此任何有效的音乐或电影播放器都需要处理这些内容。像 GeeXBox 和 MobiX 这样的小型 Live CD 完全在内存中运行，因此 CD 或 DVD 驱动器可以用来插入你选择的介质。
- **硬盘或其他存储介质**——通过检测和自动挂载硬盘分区，多媒体播放器 Live CD 可以让用户浏览计算机硬盘以查找他们想要播放的内容。只要 Live CD 包含了对硬盘上文件系统的支持（特别是大多数 Windows 系统支持的 NTFS），你就可以播放从计算机操作系统（通常是 Windows）添加的任何内容。

大多数多媒体 Live CD 都包含将 Live CD 系统连接到局域网（LAN）或互联网的支持。对有线卡的支持允许你配置网络连接（或通过 DHCP 自动完成）。无线网络支持并不常见，但在某些情况下可以通过 PCMCIA 卡实现。之后，你可以使用应用程序从网络获取内容。这些应用程序可能包括：

- **网络文件系统**——如果你的局域网支持文件共享应用程序，如 Windows 文件共享（Samba、SMB 或 CIFS）或 Linux 文件共享（NFS），你可以挂载包含播放内容的共享远程文件夹或目录。
- **网络文件传输**——通过连接到 FTP 仓库，你可以选择这些仓库中包含的内容。
- **流媒体内容**——通过包含可以播放流式音频和视频的媒体播放器，你可以从 Live CD 播放该类型的内容。

以下章节包含了几种多媒体播放器 CD 的描述。描述包括每个 Live CD 支持的功能信息以及你播放内容的方法。你还会找到关于解码器的描述，以便你播放额外类型的音频和视频内容。

### 运行 GeeXBox 开源媒体中心

由于对播放各种音频和视频内容进行了精细的调优，GeeXBox 开源媒体中心可以成为一个真正的 Linux 发行版。GeeXBox 1.0 ISO 镜像仅为 6.3MB。考虑到它包含的功能，这一成就是是非常惊人的。功能包括：

- **播放音乐 CD**——在 GeeXBox 加载到内存并开始运行后，你可以插入标准的音频光盘。你可以使用简单的键盘控制（基本上是 mplayer 自带的那些）跳转到不同的曲目并调整音量。
- **播放视频 DVD**——同样，使用 mplayer，GeeXBox 能够播放各种音频和视频内容的 DVD。你必须包含的 GeeXBox 版本必须具备解密 CSS 加密的能力，并能够播放通过 DVD 交付的大多数商业电影。（DeCSS 以及与播放商业 DVD 和其他视频内容相关的法律问题在本章的较早部分已讨论。）
- **播放 SVDC、VCD 或 XCD**——VCD 和 XCD 都是音频和视频内容的格式。VCD 支持 MPEG1 流，而另一方面，包含 MPEG2 流的 XCD 可以包含不同类型的音频视频内容，包括 MPEG4、VP3、XVID、OGG 等。
- **从硬盘播放文件**——GeeXBox 在挂载时会自动在 `/mnt` 目录的挂载点上对本地硬盘进行分区，因此存储在本地计算机任何文件系统上的任何内容都可以从 GeeXBox 界面选择并播放。

支持的文件系统包括 ext2、ext3、ReiserFS、ISO 9660、UDF 和 VFAT。NTFS 和 xBSD U 文件系统以只读方式支持。支持的文件共享文件系统包括 NFS、CIFS 和 Samba (SMB)。

- **播放电视**——同时支持模拟电视卡和数字电视广播 (DVB)，因此你可以通过 GeeXBox 看电视。

GeeXBox 最初是为了播放 DivX 电影而创建的，现在支持多种视频格式，其中大多数可以通过内置的 mplayer 媒体播放器软件获得。这些内容包括 MPEG 1、MPEG 2 和 MPEG 4（DivX、XVid、H.264 等）。只要你有适当的解码器，你还可以播放 RealMedia 和 Windows Media 电影。

支持的流媒体内容包括 Ogg Matroska、变比特率 (VBR)、变帧率 (VFR)、AAC、Ogg Vorbis、Real Video (RV) 和 SHOUT。

### 使用硬件

要显示和播放多媒体，请使用显示器和声卡。分辨率为 800x600，某些支持 640x480。电视标准包括 NTSC、PAL 和 SECAM。

提供网络连接，请使用以太网卡。在许多情况下，可以使用 DHCP 服务。

### 使用 GeeXBox 控制

所有分区都挂载在 `/mnt` 目录下，名称与其分区编号相关。例如，第一个 IDE 磁盘上的第一个分区 (`/dev/hda1`) 将挂载在 `/mnt/Disk 1 Part 1`。使用左右箭头在目录结构中移动以找到要播放的媒体文件。

在选择任何要播放的内容之前，有一些命令是可以用的。选择 M 显示或隐藏 GeeXBox 菜单。选择 S 切换到电视输出。当你播放音频或视频内容时，可以使用常规 mplayer 功能进行控制。

要选择其他播放选项，请从 GeeXBox 主菜单中选择 Options。在 Options 菜单中，你可以执行调整视频播放比例、切换到电视输出、切换垂直同步以及设置睡眠定时。

通常，如果你插入 DVD，它会自动开始播放电影。通过从 Options 列表中选择 Autoplay Mode 可以禁用该功能。然后进入 DVD 设置并选择 DVD Navigation Menu。下次你打开 DVD 时，就可以像使用标准 DVD 播放器一样使用 DVD 导航菜单。启用 DVD 导航菜单后，可以使用表 12-2 所示的键进行操作。

### 重新生成 GeeXBox

GeeXBox ISO 生成器允许你使用现有的二进制文件重建 GeeXBox，让你完全按照你想要的方式使用 GeeXBox。软件提供了以某种方式包含内容、解码器或设置的方法，从而完全个性化你自己的 GeeXBox 版本。

## 第 12 章 定制多媒体 Live Linux CD

## 表 12-1 音/视频播放控制

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| 0 或 * | 增大量 | 9 或 / | 减音量 |
| 右箭头 | 前进 10 秒 | 左箭头 | 后退 10 秒 |
| 上箭头 | 前进 1 分钟 | 下箭头 | 后退 1 分钟 |
| P 或空格键 | 暂停/恢复音频视频播放 | M | 音频静音 |
| 1 | 降低对比度 | 2 | 增大对比度 |
| 3 | 降低亮度 | 4 | 增大亮度 |
| 5 | 增大色调 | 7 | 降低饱和度 |
| 8 | 增大饱和度 | 0 | 屏幕显示（开启/关闭） |
| > | 到播放列表中的下一项 | < | 播放列表中的上一项 |
| F | 全屏模式（开启/关闭） | J | 开启/关闭字幕 |
| Z | 字幕延迟 (+0.1 秒) | X | 减少字幕延迟 (-0.1 秒) |
| Q 或 ESC | 退出 | K | 停止

## 表 12-2 DVD 菜单导航

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| 0 | 查看 DVD 菜单 | Enter | 选择选中的项目 |
| 2 | 光标向下 | 4 | 光标向左移动 |
| 6 | 光标向右移动 | 8 | 光标向上 |

### Live Linux CDs

你可以在 Linux、Mac OSX 或 Windows 系统上重新生成 GeeXBox。要开始重新生成自己的 GeeXBox，请执行以下操作：

- 1. **下载 GeeXBox ISO 生成器**——访问 GeeXBox 下载页面 (`www.geebox.org/downloads.html`) 并选择 i386 或 PowerPC 版本。然后选择最近的下载地址将 geebox-generator 包下载到硬盘上。或者参考附录 A 获取使用本书附带 CD 中包含的 GeeXBox-generator 的信息。
- 2. **解压 geebox-generator 包**——将 geebox-generator 包保存到有足够空间进行你所需的重新生成的分区。该软件仅需约 13MB 空间，但如果你在重新生成的 GeeXBox ISO 中添加模块，可能会占用多得空间。在 Linux 中解压包，输入以下命令：

```bash
