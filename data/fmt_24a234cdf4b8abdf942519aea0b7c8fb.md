
更多内容请访问 www.unitded.com

# 276 第二部分 + 使用 Red Hat Linux

表 7-3（续）

| 游戏 | 描述 | 游戏 | 描述 |
| --- | --- | --- | --- |
| fish | fish 游戏。 | moon | 月亮游戏。 |
| hunt | hunt 游戏。 | rain | 雨水游戏。 |
| mille | mille 游戏。 | robots | 机器人游戏。 |
| monopoly | 大富游戏。 | salt | 盐游戏。 |
| phantasia | phantasia 游戏。 | quiz | 问答游戏。 |
| primes | 素数游戏。 | | |
| random | 游戏。 | snake | 蛇游戏。 |
| sail | sail 游戏。 | tetris | 俄罗斯块游戏。 |
| tetris | tetris 游戏。 | trek | 星穿越游戏。 |
| wargames | wargames 游戏。 | worm | 虫游戏。 |
| worms | worms 游戏。 | wump | 鼠穴游戏。 |

# xmame

Nicola Saloria 在 1997 年启动了 MAME 项目。许多模拟器被整合到一个名为 Multiple Machine Emulator (`MAME`) 的程序中。

## 支持的 xmame 硬件

为了控制你的游戏，`xmame` 支持多种游戏硬件，包括：

- **操纵杆**——Xame 支持 i386 风格驱动程序、Fm Town Pad、X11 扩展以及新的 i386 linux 1.x 驱动程序（如果这些驱动程序已编译进 Linux）。
- **鼠标**——移动屏幕指针的常用设备。
- **滚鼠**——在笔记本电脑上代替鼠标，用于控制指针移动。
- **游戏面板**——一个面板设备（通过 `/dev/pad0` 设备访问）。

对于声音，音频设备定义为 `/dev/dsp`。如果你想更改任何游戏控制设备或声音，可以编辑 `HOME/xmame` 目录下的 `xmamerc` 文件。你可以在 `/usr/lib11/games/xmame/xmamerc` 设置系统级配置信息。

要为特定游戏使用游戏设备，可以在 `xmame` 命令行指定。使用操纵杆用 `-add -joy`；使用鼠标用 `-add -mouse`；使用滚鼠用 `-add -track`；使用游戏面板用 `-add -pad`。（游戏面板需要 Linux FM-TOWNS 游戏面板驱动程序）。例如，为特定游戏添加鼠标，输入：

```
$ xmame -mouse game
```

## 获取和安装 xmame 游戏

`xmame` 软件包不带任何游戏。在 `xmame` 和其他模拟器上运行的游戏受版权保护，旨在用于其他

# 278 第二部分 使用 Red Hat Linux

在机器上，在没有拥有原始游戏机的情况下，获取这些游戏的副本是违法的。

供 `xmame` 使用的游戏以所谓的 ROM 镜像形式进行复制和分发。每个游戏通常存储在一个单一 zip 文件中，解压后是六个或更多供 `xmame` 使用的文件。ROM 镜像是通过特殊的硬件创建的，这些硬件可以从游戏卡带和其他介质上复制软件。由于这些游戏大部分受版权保护，因此 ROM 只能以特定方式使用，以免触法。

提供 ROM 下载的网站通常附有非常严厉的警告。同样，MAME 本身对如何使用 ROM 也给出了强力警告，并要求如果你重新打包 MAME，请不要在其中包含 ROM。当你访问 ROM 网站时，你将看到下载和使用 ROM 的规则。在继续之前，系统会要求你同意这些规则。警告通常包括以下内容：

- 你必须拥有你正在下载的游戏卡带。根据其中一些网站的规定，你有权对你购买的任何软件拥有一份备份副本。
- 你不得为了利出售 ROM。

![](img/0823b2119053dace3be4993846bb1ee1_309_0.png)

我建议不要使用任何受版权保护的游戏 ROM。如果你决定获取 ROM，你需要对自己行为的法律方面负责。

有些网站说，你被允许在 24 小内复制游戏 ROM，之后你必须购买该游戏机或删除该游戏。然而，这些网站也警告说，许多 ROM 在北美和中美洲无法合法使用。再次提醒，买家（在此情况下为下载者）要加小心。

## 寻找游戏 ROM 网站

寻找可在 `xmame` 中运行的 ROM 的最佳起点是 MAME ROM 网站 (http://surf.to/mameroms)。该网站有指向最新 MAME ROM 网站的链接。

检查你安装的 `xmame` 软件包附带的 `gamelist.txt` 文件。它列出了可以在 `xmame` 中运行的游戏，并描述了任何已知问题。检查此文件可以防止你在下载已知与你的游戏模拟器兼容的 ROM 上浪费时间。

## 安装游戏 ROM

当你查看 `gamelist.txt` 文件时，注意每个游戏都关联有一个目录名称。通常，该名称就是标识游戏的名称。你使用该名称创建 ROM 目录并在 `xmame` 命令行中请求游戏。以下步骤描述了如何安装一个名为 `hoohah.zip` 的虚拟 ROM 以供 `xmame` 使用：

- 1. 为游戏创建目录：

```
$ mkdir /usr/lib/games/xmame/hoohah
```

- 2. 将 zip 文件复制到 ROM 目录：

```
$ cp wherever/hoohah.zip /usr/lib/games/xmame/roms/hoohah/
```

- 3. 进入 ROM 目录并解压文件：

```
$ unzip -L hoohah
```

- 4. 尝试使用 `xmame` 命令查看 ROM 是否可用。例如：

```
$ xmame hoohah
```

- 再次，如果此命令不起作用，请检查：

  - `xmame` 命令是否在你的 `PATH` 中（或输入完整的 `PATH`）。
  - 游戏的 ROM 目录是否在基础 ROM 目录中（通过 `/usr/lib/games/xmame/xmame` 文件中的 `rompath` 值或你的 `$HOME/xmamefile` 设置 ROM 目录）。
  - 目录名称与游戏名称相同。
  - ROM 文件的大小写正确。当命令失败时，它将列出每个 ROM 的正确大小写（可能是小字母和数字）。

在 Linux 中，大小写很重要。在步骤 3 中，使用 `-L` 选项解压文件，使它们全部变为小写。如果 `xmame` 命令失败，它会告诉你缺少哪些 ROM 文件。确保文件存在且大小写正确。

已知问题列在 `/usr/doc/xmame*` 目录下的 `readme.unix`（针对通用问题）和 `gamelist.txt`（针对特定游戏问题）中。如果你遇到困难，可以尝试 MAME 新闻组：alt.games.mame。该组非常活跃，参与者非常有帮助。

# 商业版 Linux 游戏

商业软件供应商相信 Linux 将成为一个可行的平台。热门的商业游戏如《雷神》(Quake)、《神话 II》(Myth II) 和《文明：权力召唤》(Civilization: Call to Power) 都有供 Linux 的盒装版。为了支持这些游戏，Nvidia、ATI 和 Matrox 等显卡制造商提供了在 Linux 中运行的 3D 图形加速驱动程序。运行在 Linux上的商业游戏并不多，但一些最优秀的游戏正在进入 Linux。

www.unlimited.com 上的额外内容

为了直 Linux 游戏的最新水平，你需要尝试其中一些商业游戏。《文明：权力召唤》和《神话 II》等游戏的演示版提供了一个学习这些游戏的好方法，并帮助你决决定是否要购买完整版。这些演示版通常包含在互联网上与其他对战的功能。

下一节描述了一些 Linux 可用的最受欢迎的商业游戏。更多热门标题正在不断加入中。

- 如需查找最新的 Linux 游戏新闻，请尝试 Linux Gaming Tome (http://happypenguin.org) 和 Linux Games 网站 (www.linuxgames.com)。你也应该检查 Linux Games 网站 (www.linuxgames.com)。

## 文明：权力王国 (Civilization: Call to Power)

你可以通过《文明：权力王国》（CCP）构建在线文明。与早期的版本和免费衍生版（如本章前文描述的 Freeciv）一样，Linux 版本的《文明：权力王国》可以让你探索世界、建造城市并管理你的帝国。这个最新版本提供了多人网络竞技以及扩展功能，让你能将城市扩展到外层太空和深海。

CCP 由动动（www.activision.com）制作，尽管 Linux 版本是由 Loki Entertainment Software（www.lokigames.com）创建的。CCP 是历史上最畅销的游戏之一，因此，为 Linux 制作该产品的盒装版对 Linux 用户来说是一个非常大的加分。
