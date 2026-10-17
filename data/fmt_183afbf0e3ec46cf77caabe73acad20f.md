
要为特定游戏设备，请在 `xmame` 命令行中指定。要使用摇杆，添加 `-joy`；要使用鼠标，添加 `-mouse`；要使用轨迹球，添加 `-trak`；要使用游戏手柄，添加 `-pad`。（游戏手柄需要 Linux FM-TOWNS 游戏手柄驱动程序）。例如，为特定类型的游戏添加鼠标：

```
xmame -mouse
```

## 获取并安装 xmame 游戏

`xmame` 包不包含任何游戏。由于运行在 `xmame` 和其他模拟器上的游戏受版权保护，并且是为了其他机器设计的，因此在没有拥有原始街机的情况下获取这些游戏的副本是非违法的。

`xmame` 可以的游戏以被称为“ROM 镜像”的形式复制和分发。每个游戏通常存储在一个单一 `zip` 文件中，该文件被解压为六个或更多 `xmame` 使用的文件。ROM 镜像是由特殊的硬件创建的，这些硬件可以从游戏卡和其他介质上复制软件。由于由于大多数游戏都受版权保护，因此 ROM 只能以特定的方式使用以防违法。

提供 ROM 下载的网站带有非常强烈的警告。同样，MAME 本身对如何使用 ROM 给出了强力警告，并要求如果你重新封装 MAME，不要在其中包含 ROM。当你访问 ROM 下载网站时，你将看到下载和使用 ROM 的规则。在继续之前，你会被要求同意这些规则。警告通常包括以下内容：

- ◆ 你必须拥有你正在下载的游戏卡带。根据其中一些网站的规定，你有权获得你所购买的任何软件的备份副本。
- ◆ 你不得为了利润出售 ROM。

我建议你不要使用任何受版权保护的游戏 ROM。如果你决定获取 ROM，你将负责研究你行为的法律方面的问题。

有些网站说，你被允许 24 小时内复制游戏 ROM，之后你必须购买该游戏机或删除该游戏。然而，这些网站还警告说，许多 ROM 在北美和中美洲无法合法使用。再次提醒，请买家（在此例中为下载者）小心。

![](img/176fafece2d30daee750bc078e898ee4_282_0.png)

## 寻找游戏 ROM 网站

寻找在 `xmame` 中运行的 ROM 的最佳起点是 MAME ROM 网站 (`http://surf.to/mameroms`)。该网站有指向最新 MAME ROM 网站的链接。以下是你可以访问的一些网站：

- ROMs Central (`http://www.download.net/arcade/roms/`) — 包含数百个游戏的 ROM，以及图片和描述。
- ROM Finder (`http://romfinder.com/`) — 包含数十种游戏系统的 ROM。它还包含一个用于搜索游戏 ROM 的搜索工具。

检查你安装的 `xmame` 包附带的 `gameslist.txt` 文件。它列出了已知可以在 `xmame` 上运行的游戏，并描述了任何已知问题。检查此文件可以防止你浪费时间下载那些与你的游戏模拟器无法运行的 ROM。

## 安装游戏 ROM

当你查看 `gameslist.txt` 文件时，请注意每个游戏都关联有一个目录名称。通常，该名称就是你创建 ROM 目录以及在 `xmame` 命令行中运行游戏的名称。以下步骤描述了如何安装一个名为 `hoohah.zip` 的虚构 ROM 以供 `xmame` 使用：

1. 为游戏创建目录：

```
mkdir /usr/lib/games/mame/hoohah
```

2. 将文件复制到 ROM 目录：

```
cp wherever/hoohah.zip /usr/lib/games/mame/hoohah/
```

3. 进入 ROM 目录并解压文件：

```
unzip -L hoohah
```

4. 尝试使用 `xmame` 命令查看 ROM 是否可用。例如：

```
xmame hoohah
```

再次，如果此命令不起作用，请检查：

- `xmame` 命令是否在你的 `PATH` 中。
- 目录名称是否正确。
- 文件是否在正确的目录中。
- 你是否有足够的磁盘空间存放解压后的文件。

![](img/176fafece2d30daee750bc078e898ee4_284_0.png)

# 第 7 章 ♦ 在 Red Hat Linux 上玩游戏 255

《Myth II》由 Bungie Software (`http://www.bungie.com`) 创建，并由 Loki Entertainment Software (`http://www.lokigames.com`) 移植到 Linux。这个版本的热门游戏《Myth》包含了改进的图形和新场景。

提供一个演示版，它可以在 Red Hat Linux 上运行良好。一如常例，你需要一台性能强大的计算机（至少需要 Pentium 133 MHz 处理器、32MB 内存、80MB 交换空间和 100MB 磁盘空间）。多用户网络游戏需要网络硬件（网卡或拨号上网）以及一张用于听音频的声卡。要获取演示版，请访问 Myth II 页面 (`http://lokigames.com/products/myth2`) 并点击“Download Demo”链接查找可以获取演示版的网站。图 7-8 显示了《Myth II》的截图。

![](img/176fafece2d30daee750bc078e898ee4_286_0.png)

图 7-8：使用战士、弓箭手和矮人在《Myth II》中战斗。

## 恐鬼传说 竞技场

《Quake》系列的最新版本《Quake III Arena》提供了 Linux 版本。《Quake》是 id Software 对其《Doom》系列推出的重大续作。与《Doom》一样，《Quake》是一款第一人称（视角）游戏，你穿过走廊寻找物资。与《Doom》一样，核心点是射击大量怪物。然而，怪物种类更加多样，并且有不同的优缺点。还需要执行复杂的任务。

尽管《Quake III Arena》与其他《Quake》版本一样由 id Software 创建，但该产品的 Linux 版本是由 Loki Entertainment Software (`http://www.lokigames.com`) 移植的。本书出版时，该产品售价为 49.95 美元。如果你想尝试《Quake III Arena》，有一个演示版。与其他游戏的演示版不同，这个演示版对视频的要求更为苛刻。在开始下载之前，请检查 Quake III 常见 (`http://www.lokigames.com/support/quake3/quake3faq.php3`) 以确认你是否拥有所需的硬件和软件。要获取演示版，请访问：`http://www.quake3arena.com/demo`。图 7-9 显示了《Quake III Arena》演示版的设置界面。

![](img/176fafece2d30daee750bc078e898ee4_287_0.png)

**图 7-9**：使用 Loki 的演示版尝试《Quake III Arena》。

要查找有关《Quake III Arena》的最新信息，请访问 Quake 3 首页 (`http://www.quake3arena.com`)。

## 总结

虽然 Red Hat Linux 尚未成为主导游戏平台，但 Red Hat Linux 上仍然运行着许多你可以投入时间的游戏。进入 Linux 的旧版 UNIX 游戏包括各种基于文本和基于 X Window 的游戏。这里有卡牌游戏、策略游戏以及一些动作游戏。

对于针对特定游戏机和街机的游戏，模拟器在 Linux 系统中提供了一个环境，可以在其中运行这些游戏。互联网上有数百个游戏 ROM 可用，尽管版权法限制了你可以合法下载和使用的内容。

在商业方面，Red Hat Linux 系统可以使用 Linux 版文明：权力之召（Civilization: Call to Power）、《Myth II》和《Quake III Arena》。这些游戏中的大多数提供了极佳的图形和动画，但它们需要特定的显卡和驱动程序才能有效运行。

# Red Hat Linux 中的多媒体

这些 UNIX 系统（如 Red Hat Linux）曾经仅通过屏幕上的文字呈现，图形视频显卡和接口（如 X Window 系统）的进步使得使用强大的计算系统变得更加友好。通过向你的 Red Hat Linux 系统添加声卡和一些现代软件，你现在可以在曾经只有文字的地方体验音乐、特效、动画和视频。

在本章中，你将学习如何向 Red Hat Linux 系统添加音频、视频和其他多媒体支持。本章描述了如何配置声卡使其与 Red Hat Linux 配合。然后它将告诉你如何获取并使用软件从 Red Hat Linux 系统播放音乐 CD 和各种格式的音频。

网络上常见的视频片段有 AVI、MPEG 和 QuickTime 等格式。此外，为了查看网页上大量的 RealMedia 内容，Real Networks 创建了一个可以在 Linux 下运行的 RealPlayer 软件版本。本章描述了如何获取该播放器以及如何找到供其使用的内容。

## 听音频

如果你想让电脑发出的声音不仅仅是 PC 扬声器偶尔出的“叮”声，你需要为电脑添加一张声卡。如果游戏依赖音效或对你说话，游戏就是添加声卡的一个理由。此外，声卡还允许你播放音乐并使用电话软件在互联网上与他人通信。
