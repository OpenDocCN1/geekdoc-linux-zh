
| 游戏 | 描述 |
| --- | --- |
| **战术与策略** |  |
| KJumping Cube | 点击方格以增加数字并占领相邻方格。 |
| KAtomic | 移动棋子以创建不同的化学化合物。 |
| Konquest | 在这个多人游戏中扩张你的星际帝国。 |
| Kolor Lines | 移动弹珠形成五子连珠并得分。 |
| KMines | 扫雷克隆版。点击安全区域并避开炸弹。 |
| KSokoban | 日本仓库管理员游戏。 |
| SameGame | 消除游戏棋子以得分。 |

KDE 菜单上的游戏从消遣到相当具有挑战性不等。如果你习惯在 Windows 中玩游戏，KMines 和 Patience 会像老朋友一样。KAsteroids 和 K Poker 适合无脑游戏类别。对于智力挑战（看起来比实际更难），请尝试 KSokoban。对于 GNOME 菜单上的具有挑战性的多人游戏，请尝试 FreeCiv。对于国际象棋爱好者，有 Chess（gnuchess 的 xboard 版本）。

## 国际象棋游戏

国际象棋是计算机系统上最早玩的游戏之一。虽然游戏多年来没有改变，但它在计算机上的玩法已经改变。Red Hat Linux 附带的国际象棋程序集让你可以与计算机对战（文本或图形模式）、让计算机自相对抗，或重放存储的国际象棋游戏。你甚至可以使用 Internet Chess Servers（ICS）在 Internet 上与其他用户对弈国际象棋。

xboard 程序是一个基于 X 的国际象棋游戏，为 gnuchess 提供图形界面。GNU Chess（由 gnuchess 包表示）将自己描述为一个协作式国际象棋程序。它有许多贡献者，并寻求在国际象棋社区中推进“更开放、更友好的分享环境”。使用 xboard，你可以用鼠标移动图形棋子。要与计算机对战，请从 Red Hat 菜单中点击 Games → More Games → Chess，然后只需用鼠标移动一枚棋子开始。在 xboard 窗口中，选择 Mode → Two Machines 让计算机自行对战。选择 File → Load Game 以便以便携游戏记谱法（PGN）加载游戏。图 7-1 显示了正在进行的“Two Machines”游戏的 xboard 窗口。

![](img/27a85d56d393921ced6412ae6e8336bf_271_0.png)

图 7-1：在棋盘窗口中，你可以设置 xboard 以便与计算机对战或重放保存的游戏。

你可以通过将 xboard 会话连接到 Internet Chess Server（ICS）来在线与其他人对战。要将 xboard 作为 ICS 的界面启动，请点击 Extras → Games → Chess 或输入以下命令行：

```
$ xboard -ics -ichost name
```

在此示例中，name 应替换为 ICS 主机的名称（请参阅下面的主机列表）。在 ICS 模式下，你可以只是观看游戏、与其他用户对战，或重放已完成的游戏。ICS 主机充当一个聚集地，供爱好者在 Internet 上与其他人对弈国际象棋、观看游戏、参加锦标赛或只是结识国际象棋人士。以下是你可以通过将上面的 name 替换为下面所示的地址来连接的 ICS 主机计算机：

- **互联网国际象棋俱乐部：** ICC (chessclub.com)
- **Chess.net** (chess.net)
- **免费互联网国际象棋服务器** (freechess.org)

## Freeciv

使用 Freeciv，你可以创建一个文明，与竞争的文明争夺世界主导权。Red Hat Linux 附带的 Freeciv 版本包含客户端软件（用于玩游戏）和服务器软件（用于连接玩家）。你可以连接到自己的服务器并自行尝试游戏，或（通过网络连接）在 Internet 上与多达 14 名其他玩家对战。

你可以从 Red Hat 菜单（作为非 root 用户）通过点击 Games → More Games → FreeCiv（Isometric tile set）启动 FreeCiv。如果 FreeCiv 未启动，请尝试从终端窗口输入以下命令启动：

```
$ civ &
```

图 7-2 显示了启动 FreeCiv 时出现的两个窗口。Connect to FreeCiv Server 窗口包含你的用户名、主机名和端口号。FreeCiv 窗口是游戏进行的地方。

![](img/27a85d56d393921ced6412ae6e8336bf_272_0.png)

**图 7-2：** 通过 FreeCiv 建立文明并与其他人竞争。

> **注意：** 如果 FreeCiv 无法启动，一个原因可能是你以 root 身份登录。你必须以普通用户身份登录才能运行 `civ` 命令。

### 启动 FreeCiv

如果你愿意，可以先独自玩几局游戏，以便在与网络上的其他人对战之前熟悉游戏。以下步骤说明如何启动你的第一个练习 FreeCiv 游戏。

1. 从 Red Hat 菜单启动 FreeCiv（Games → More Games → FreeCiv，或输入 `civ&`）。  
   FreeCiv 窗口出现，如图 7-2 所示。

2. 从终端窗口输入以下命令启动 FreeCiv 服务器：

```
$ civserver
This is the server for FreeCiv version 1.13.0
You can learn a lot about FreeCiv at http://www.freeciv.org/
2: Now accepting new client connections.
> For introductory help, type 'help'.
>
```

3. 点击 Connect to Freeciv Server 窗口中的 Connect。

4. 从服务器提示符输入以下内容：

```
> start
> Starting game.
> 2: Loading rule sets
>
```

客户端上会出现一个“你将成为哪个国家？”窗口，如图 7-3 所示。

![](img/27a85d56d393921ced6412ae6e8336bf_273_0.png)

5. 从服务器提示符启动 Freeciv 后，选择一个国家、领导人姓名、你的性别以及城市风格，然后点击 OK。此时，你可以返回 FreeCiv 窗口。

### 开始使用 FreeCiv

查看 FreeCiv 窗口。以下是开始时应了解的内容。（你可以在 FreeCiv 网站 www.freeciv.org 找到更多帮助。）

- 点击 Help 按钮获取在游戏过程中对你有用的各个主题的专题信息。
- 世界（默认）为 80 x 50 方格，每次可见 11 x 8 方格。
- 活动方格包含活动单位的图标（与方格地形交替闪烁）。
- 有些方格包含特殊资源。按住鼠标中键可了解方格包含哪些特殊资源。（对于双键鼠标，按住 Ctrl 键并点击鼠标右键。）多试几次以熟悉周围的土地。此操作还会识别地形上的任何单位以及单位的统计数据。
- 要查看 11 × 8 视野区域外的世界，请点击地图外的滚动条。起初外部世界是黑色的。随着单位的增加，靠近这些单位的区域将变得可见。（按字母 c 返回地图的活动部分。）
- FreeCiv 窗口左上角有一个概览地图。随着世界的文明化，这提供了一个了解正在发生的事情的良好概览。在概览地图上右键单击某点可将视口居中于该处。
- 菜单栏包含可用于玩游戏的按钮。Game 菜单让你更改设置和选项、查看玩家数据、查看消息并清除日志。Kingdom 菜单让你更改税率、查找城市并发动革命。View 菜单让你在地图上放置网格或居中视图。Orders 菜单是你选择建造项目和采取行动的地方。Reports 菜单让你显示与城市、军事、贸易和科学相关的报告，以及其他特殊报告。
- 文明经济的摘要显示在概览地图下方。信息包括人口数量、当前年份、国库中的金钱以及分配给税收、奢侈品和科学的金钱百分比。
- 概览信息下方有十个图标，表示金钱在奢侈品（一名娱乐者）、研究（一名研究员）和税收（一名税务员）之间的分配。本质上，这些图标表示你的资源有多少用于改善社区的这些属性。
- 当你完成本回合的所有移动时，点击 Turn Done。旁边的一个灯泡指示你的研究进度（每回合增加）。一个太阳图标起初是清晰的，但会因污染而变得更亮，以警告可能的全球变暖。政府符号表示你以专制政府开始。最后一个图标告诉你本回合剩余的时间。

单位框显示当前单位的信息。你开始时拥有两个 Settlers 单位和一个 Explorer 单位。

### 建立你的文明

开始建立你的文明。以下是 FreeCiv 手册建议尝试的内容：

- 要更改资金分配，请选择 Kingdom → Tax Rates。移动滑块重新分配分配给奢侈品、研究和税收的资产百分比。尝试提高研究并减少税收来开始。
