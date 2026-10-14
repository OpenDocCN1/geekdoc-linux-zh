
`wget -o logfile -c "ftp://ftp.linuxgames.com/loki/demos/myth2/myth2-demo.run"`

只需输入 `./myth2_demo.run` 创建 `myth2_demo` 目录并安装游戏。进入新目录，阅读 README 文件，然后运行 `./setup.sh` 来确定游戏所需的系统架构。在 `myth2_demo` 目录中输入 `./myth2` 即可开始游戏。

## 玩 Myth2

Demo 版从一段描述故事场景的短电影开始，配有出色的配乐。当电影结束时，你将看到图 14-6 所示的不详屏幕。

选择 Preferences（设置）来设置图 14-7 所示各种选项。

![](img/43a9671cef617c9c7a18f7a6904433f1_358_0.png)

图 14-6：Myth2 的问候

![](img/43a9671cef617c9c7a18f7a6904433f1_358_1.png)

图 14-7：在 Myth2 中设置你的偏好

设置完成后点击 OK，然后选择 Tutorial（教程）学习如何控制战斗。骑士、弓箭手、矮人和法师是你装备并引导进入战斗的角色类型，以拯救 Madrigal 的好子民。

![](img/43a9671cef617c9c7a18f7a6904433f1_362_0.png)

图 14-11：RT2 启动菜单

![](img/43a9671cef617c9c7a18f7a6904433f1_362_1.png)

图 14-12：RT2 教程

... 取于你对资源的智能利用，以及应对土匪、火车事故和股市反转等变故的能力。

一旦你掌握了教程，就是时候建立你的帝国了。返回**主（Main）**菜单并选择**新场景（New Scenario）**，选择新的地图和难度级别，然后点击**确定（OK）**开始游戏。图 14-13 显示了新场景设置窗口。

![](img/43a9671cef617c9c7a18f7a6904433f1_363_0.png)

图 14-13：在《铁路大亨头II》中选择新场景

![](img/43a9671cef617c9c7a18f7a6904433f1_363_1.png)

图 14-14：来自“美国腹地”场景的芝加哥

图 14-14 显示了“美国腹地”场景中芝加哥地区的地图。

如你所见，画面非常精美，即使放大到高细节也是如此。音频支持同样出色，包含了完整的火车各种声音和噪音，并有与你当前位置合适的背景音。设计者值得赞赞的是，尽管声音持续存在，但从不让人厌烦，而且似乎始终与屏幕上的活动完美融合。

## 离开这列火车

RT2 易于学习，但极具挑战性。像 Myth2 一样，它实现了 Loki 为 Linux 游戏玩家提供顶级游戏体验的目标，拥有一流的画面、音效和高度智能的游戏策略。如果你对通过建造自己的铁路来积累财富感兴趣，或者你只是喜欢火车的外观和声音，那么你需要玩玩 RT2。这是来自 Loki 的另一款“最推荐”游戏。

## Clanbomber

- 作者：Andreas Hundt, Denis Oliver Kropp
- 介绍版本：1.00
- 网站：http://www.clanbomber.de
- FTP 站点：无
- 维护：是

内容摘要：简单、嘈闹的游戏体验，适合老少皆宜。

Clanbomber 以受欢迎的《炸弹仔》（Bomberman）游戏为模型。Clanbomber 的主要活动包括在游戏区域移动并放置非常响亮的爆炸物来清除对手（当然，对手也在试图对你做同样的事）。你可以与电脑控制玩家玩家，但作者建议与八位朋友一起玩最有趣。

### 获取与构建

Clanbomber 需要 zLib、ClanLib 和 Hermes 库来提供图形和音频支持，这些库都可以在 Clanbomber 网站获得。安装好这些库后，从 www.clanbomber.de 下载最新版本的 Clanbomber。将包放在你的 `/home` 或 `/usr/local/` 目录下，并使用 `tar xvzf clanbomber-latest.tar.gz` 解压。进入新的 Clanbomber 目录并运行 `./configure`，然后执行 `make` 和（作为 root）`make install`。现在让我们玩 Clanbomber 吧！

### 玩 Clanbomber

在 xterm 窗口命令行提示符或控制台中输入 `clanbomber`。系统将询问应使用何种视频显示类型。输入相应的类型；经过短暂的启动屏幕后，你将看到图 14-15 所示显示。

![](img/43a9671cef617c9c7a18f7a6904433f1_365_0.png)

图 14-15：Clanbomber 主菜单

![](img/43a9671cef617c9c7a18f7a6904433f1_365_1.png)

图 14-16：Clanbomber 中的玩家设置

![](img/43a9671cef617c9c7a18f7a6904433f1_366_0.png)

图 14-17：开始 Clanbomber

打开**选项（Options）**菜单来切换音乐轨道和其他各种设置。按 `esc` 键返回**主（Main）**菜单，然后选择**本地游戏（Local Game）**。当菜单打开时，选择**玩家设置（Player Setup）**来选择玩家并设置队伍。图 14-16 显示了**玩家设置**窗口。

完成玩家设置后，返回**本地游戏**菜单。设置回合时间和获胜所需的的分数，选择一张地形地图并开始游戏。将出现图 14-17 所示的屏幕。

从这里开始，放置炸弹和躲避对手放置的炸弹是你的主要活动。随着棋盘上的格子被炸毁，会发现各种新技能（例如投掷炸弹和二合一爆炸）。获得技能很容易，但要有效使用它需要策略和时机。

| 应用名称 | 描述 | 版本 | 作者/制造商 |
|---|---|---|---|
| Sequencer Plus Gold | MIDI 排序器 | 4.09 | Voyetra Technologies (http://www.voyetra.com) |
| Sideman D/TX | 合成器编辑器 | | Voyetra Technologies (http://www.voyetra.com) |
| M/pc | 算法音乐生成器 | 1.10b | Voyetra Technologies (http://www.voyetra.com) |
| Drummer | 鼓点作曲器 | 2.0 | Cool Shoes Software (已不可用) |
| RAVEL | MIDI 编程环境 | 3.0 | Jim Brinkley (http://ftp.cs.psdx.edu/pub/music/ravel/) |
| MusicBox | MIDI 编程环境 | | John Dunn (http://algoart.com) |

DOSemu 软件包提供的音频支持说明非常简单：它与 `/dev/midi` 或 `/dev/sequencer` 建立链接，所有对 MIDI 硬件的原生调用都会被 DOSemu 拦截并重定向到适当的 Linux MIDI 设备。然而，Voyetra 的软件除非存在 Voyetra MIDI 接口 (VAPI) 驱动，否则不会传输或接收 MIDI 数据，这带来了一个问题：只有一个 VAPI 驱动有效 (`vapimpu.com`)，而且仅限于某些版本级别 (`1.26` 和 `1.33`)。为了使用这些驱动程序之一，你必须添加 IRQ 数字。以下是我在 DOSemu 中加载 VAPIMPU 驱动使用的命令：

```
vvapimpu /IRQ:7
```
