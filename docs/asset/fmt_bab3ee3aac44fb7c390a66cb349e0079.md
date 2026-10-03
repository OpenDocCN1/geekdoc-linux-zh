
# 运行代码

# 骇客 67

## Textdept 支持图形模式和文本模式

没有其他软件类别能像文本编辑器那样提供如此广泛的选择。`Textdept` 是一个极具前景的种子化且无干扰的设计，且在没有牺牲核心功能的情况下。它支持 Linux、macOS 和 Windows。

`Textdept` 确实非常成熟：它的开发始于十年前，在过去的十年里，开发者们每两个月就会进行一次工作。

`Textdept` 可以作为二进制文件在命令行中运行，也可以作为 GUI 应用程序运行。可执行文件大小约为 3MB，可以通过 USB 闪盘运行。这非常小，但它能够塞入极速高亮（支持约 100 种语言）以及更多功能。它的补全非常完整。对于我们这些没有摄影式记忆的人来说，它的功能至关重要。通过 `Ctrl + Enter` 进行自动补全可以处理你正在编辑的文件中的符号。你正在使用的语言符号可以配合 API 文档完美补全。

编辑器也是直观驱动的、轻量级且文档完备。一个在许多编辑器中找不到的有趣功能是为每个文件单独更改字体大小（参见文件属性）。如果你从远程更改，还可以运行名为 `textdept-curses` 的 `Textdept` 终端版本。

![](img/7d1dae30e3ad0209ad7d498c3a55d2ad_82_0.png)

```c
void line(int id, int addr = MAX_ADDR, size) {

    if ((address, size) != _AS_FREE) {

        list_address(id, address);

    }

    int page = addr / 1024;

    int offset = addr % 1024;

    if (page_table[page] == NULL) {

        page_table[page] = malloc(size);

    }

    page_table[page][offset] = id;

    if ((tap % 12) == (PAGE % size)) {

        return;

    }

    return time(id);

}
```

![](img/7d1dae30e3ad0209ad7d498c3a55d2ad_82_1.png)

作者：Graham Morrison

https://orbital.github.io/textdept/

# 使用 SystemTap 进行动态分析

# 骇客 68

在多线程程序中，源码中语句的顺序并不等于执行顺序，仅仅查看代码无法揭示程序操作的序列。你需要一些工具进行实时检查，也称为动态分析。

`SystemTap` 是其中一个工具，它的映射是主可执行文件。在 Ubuntu 和 openSUSE 上，你可以在默认仓库中找到 `systemtap`。你需要一个应该构建在发行版中的内核模块。在 Ubuntu 22.04 上，你应该安装 `systemtap-doc`；最新版本包含示例文件，将帮助你学习该工具。在损坏的 `SystemTap` 环境中通过 apt 安装。

`SystemTap` 允许你编写脚本并附加到内核中发生的所有事件。它的设计旨在安全地用于生产系统，例如野外环境中的死锁。

`SystemTap` 能做之一是帮助确定内存泄漏。你可以在 `/usr/share/systemtap/examples` 中找到许多示例。它跟踪函数调用，并计算头部等待锁的时间。运行几秒后停止它；它将在 VirtualBox (43297) 中运行，调用 85557a2b8c216 次，89519 us - 数值越小越好。

如果你有相同的问题，尝试添加 Ubuntu wiki 页面 Debug Symbols 中描述的新探针，`sudo apt install g++* get libdev-dbv-linux-` 并编译 `SystemTap` 源码。

作者：Violet Sinitaysn 和 Hans-Geörg Eisser

https://opensource.ubuntu.org/systemtap/

https://wiki.ubuntu.com/Debug/20Symbol%20Packages

酷酷 LINUX 版 - 2023

# 运行代码

![](img/7d1dae30e3ad0209ad7d498c3a55d2ad_83_0.png)

## 使用彩色工具替换 hexdump

![](img/7d1dae30e3ad0209ad7d498c3a55d2ad_83_1.png)

## 使用 GRV 管理你的 git 仓库

当以十六进制形式查看二进制文件时，你能够更深入地解码任何位置的字面值。你实际上能够看到模式甚至数据度量，因为我们可以查看数据为何通过内存。这使得十六进制值成为拥有所有字符的实用工具，特别是当文件被存储或可执行文件可能如何工作时。

我们许多人都在命令行使用 `git`，以至于很难想象使用 GUI 来让访问仓库变得简单。从命令行到桌面的上下文切换往往足以中断你的思路或注意力。但有一个非常有用的工具。

## 可运行代码

## 统计项目代码行数

你对代码项目的统计数据感兴趣吗？你可以使用 `wc` 处理源文件来获取行数，但简单的工具无法区分注释和代码。我们建议使用像 `cloc` 类的工具——它能够统计代码行数并为你提供项目概览。这个实用的助手可以统计空行、注释以及代码行（见图）。

`cloc` 将统计分析结果输出到标准输出。`cloc` 解析 Perl 5.6 或更高版本。在 Ubuntu 上，你可以安装该软件包；在其他发行版上，使用 `git clone`。`cloc` 能够超过 250 种编程语言。你可以使用 `cloc --show-lang` 获取完整列表。

## 黑客技巧 73

你可以指定要统计的文件或目录。`cloc` 还能理解压缩的 tar 或 ZIP 文件；该工具可以在你通过 `extract` 解压时提供帮助。该程序还会跟踪文件、目录和存档之间的变化。它的映射列出了各种不同的参数及其示例。

你可以将 `cloc` 的评估结果保存为 CSV、XML 或 YAML 格式，`sql-insert` 将为 SQL 数据库生成 INSERT 语句。

```
$esser@ps13:linux ~/local/src/utils
$esser@ps13:linux$ cloc
  8 files
  8 unique files
  00 ignored.
```

| language | files | blank | comment |
| --- | --- | --- | --- |
| C | 1 | 6836 | 21548 |
| C/C++ | 4 | 752 | 2123 |
| Java | 1 | 452 | 7460 |
| SUM | 8 | 19 | 210 |

github.com/AlDnial/cloc v1.86 Tw0.11 (75.5 files/s, 42787.7 lines/s)

> 作者：Uwe Wahlhardt

## 修复缩进等

一个经典工具是“indentor”（缩进器），它获取源代码并创建一个新版本，其中缩进和花括号的位置遵循固定规则。该家族中的一个示例是 `indent`。Unix 原生版本于 70 年代后期出现，Linux 上的版本最后更新于 1998 年。

对于更灵活的方法，请查看 `uncrustify`；它的功能不仅仅是缩进，你可以通过编写复杂的配置文件来配置它。该程序支持 C、C++、Object、D、Java、Python 等许多语言。要开始使用，软件包内容或网页上有 `uncrustify` 的示例文件。

我找到了一个 openSUSE 软件包并将其用于我所有的代码仓库。可以轻松地从当前版本检查更改：

安装后，获取一个源文件并运行

```
uncrustify -linux cfg testfile.c
```

这将创建一个新的 `testfile`，`uncrustify` 尝试对其进行（自动且完美格式化）并取得了成功，如图所示。

> 作者：Hans-Georg Eißer

`git clone https://github.com/uncrustify/uncrustify.git`

在我的测试中，我将以下命令构建项目：

```
cd uncrustify; make; cd build
make .. sudo make install
```

在 `uncrustify` 文件夹中运行。（在 Ubuntu 上，运行 `apt apt install cmake` 来获取该特定工具。）

https://en.wikipedia.org/wiki/Uncrustify (Unix)
https://uncrustify.sourceforge.net/
https://uncrustify.sourceforge.net/uncrustify.cfg

酷炫 LINUX 黑客技巧 - 2022 版

## 通过特版磨炼你的技能！

从我们的特版库中了解 Shell、LibreOffice、Linux 等更多内容。

《Linux Magazine》团队创建了一系列单行本，让你深入研究感兴趣的话题。
提供纸质版或数字版。

## 查看完整库！
shop.linuxnewmedia.com

# 游戏

你已经工作了几个小时，配置了系统、开发了新程序、完成了演示？现在是游戏时间了。

| | | |
|---|---|---|
| HACK 75 | 运行 Gamebuntu 设置脚本 | 89 |
| HACK 76 | SDLPoP: 波斯之王的克隆 | 89 |
| HACK 77 | Sonic Robo Blast 2 | 90 |
| HACK 78 | Teeworlds 多人平台跳跃游戏 | 90 |
| HACK 79 | 使用 DOSBox 运行旧 DOS 游戏 | 91 |
| HACK 80 | Crispy Doom 克隆 | 93 |
| HACK 81 | UnCiv 策略游戏 | 93 |
| HACK 82 | 空间站 14 | 94 |
| HACK 83 | 探索、扩张、消灭：玩 Ruler 2 | 94 |
| HACK 84 | Lutrs 游戏 | 95 |

# 游戏

## 黑客技巧 76: 运行 Gamebuntu 设置脚本

对于 Linux 玩家来说，这是一个兴奋的时刻，因为有很多工作正在为让 Linux 支持游戏而努力。这无疑主要归功于 Valve，他们在发布 Steam Deck 方面的表现令人惊叹，以及他们的游戏兼容层。还有许多其他调整，这些都是 Raj Saraswat 的心血，他是一位来自印度的 12 岁开发者，同时也负责了《波斯之王》——史上最优秀的 2D 平台和冒险游戏之一。该游戏最初于 1989 年在 Apple II 上发布，由 Jordan Mechner 开发，因几个原因而非常出色。当时的第一个角色动画在那个时代都是领先的。游戏具有超越时代的真实感，这正是游戏成功的原因。你身处一个地下城，有 60 分钟的时间逃生并救援。在数小时的游戏测试中，难度和流行程度经过微调，完美地让任务变得易于上手但不至于简单。寻找出口路过程中的敌人和挑战提供了足够的变性和挑战，让你痴迷其中，正如许多人一样。

Guntu 是一个全面的 Bash 脚本，汇总了与 Linux 游戏相关的所有内容。它是为可能安装某些东西的新用户设计的。虽然原作已经发布，但该系列在现代硬件上继续，硬组版本现在已使用 SDL 进行解构和重建，创建了 POP。它是游戏的完美复制，包括图形、声音、音乐和沉浸感。它对于 30 多年前的一代人和同时玩家来说也是全新的，而且非常好玩。这个版本包含了作弊（跳过关卡、房间导航）和控制器支持，并且尽可能现代化，在游戏进行时增加了视频回放功能，这让年轻一代或也许我们这些拥有相同机智和敏捷操作能力的人更容易上手。

喜欢 Ubuntu 但还不了解，或者想知道应该添加什么来创建一个完美的游戏系统？图形界面首先在窗口顶部显示一个/或引导查找器。点击此按钮将自动安装大量的游戏相关软件。这可能需要一些时间，因为要安装的内容正在增长。它包括诸如 Proton 内核（提供最新的显卡驱动程序）、带有 PulseAudio 效果的 OBS 以及用于麦克风录制的 NoisTorch。对于游戏，Guntu 增加了 Steam 和 Heroic Launcher 来访问你的游戏，以及用于 Windows 游戏的 Wine。前端创建了一个启动器来访问所有已安装内容的面向用户部分。这可能需要一些设置，例如登录 Epic Games Store 或 YouTube Studio，这会迅速成为你访问所有游戏内容的入口，并有力地提醒你 Linux 上可用的游戏软件有多么，而且未来会有更多。

作者：Graham Morrison

https://gitlab.com/rswat09

## 黑客技巧 77: Sonic Blast 2

小刺猬经常出现在开源游戏重制版中。这可能是因为 Sonic 是 1990 年代主机游戏的奇迹，那个十年见证了 Linux 的第二个维度，而且时间还不长到让当年的青少年成为如今的高级开发人员。`Sonic Blast 2` 是这一理论的证明，它不仅将开源与 Sonic 结合，还结合了那个时代的机制。游戏本身完全由粉丝制作，其根源可以追溯到 90 年代后期。它包含超过 25 个完全由社区创建的关卡，具有与原作相同的糖分驱动的平台跳跃风格，但不同的玩法被转换到了三维。而且不仅仅是《超级马里奥 64》那种整洁的多边形三维。

这篇惊人的粉丝同人（游戏类）开发时间几乎和它的灵感来源一样长，但它仍在进行更新。

| 分数 | 0 |
| 时间 | 0-22 |
| 环 | 2 |

如果你玩过 2D 版本，这个游戏会让你感到很熟悉。你可以扮演任何主要角色，他们都有自己的能力，并在这些关卡中穿梭的同时射击其他玩家。你不需要简单地指向移动方向的左或右，而是可以在所有方向移动。这是一种不寻常的机制，感觉像是在玩经典的双玩家坦克游戏，但增加了额外的技巧水平，包括重力、特效和类型。另一个独特元素是漫画风格的抓钩或用手臂荡秋，它可以让你像充满咖啡因的蜘蛛一样穿过关卡，导致了非常独特的玩法。

# 使用 DOSBox 运行旧 DOS 游戏

许多经典游戏都是为 MS-DOS 推出的——想想第一人称射击先驱《Quark》和《毁灭战士》（Doom），以及《猴子岛》等冒险游戏。这些许多游戏可以在互联网存档（Internet Archive）的软件库中找到（图1），但你现在如何玩它们呢？

当然，在真实电脑或虚拟机上安装 MS-DOS 或其免费克隆版本 FreeDOS 是完全可能的。但有一个工具可以简化这一切：`DOSBox` 是一个集成的 PC 和 DOS 模拟器，它可以将你 Linux 设备上的任何文件夹映射到内部的 `C:` 盘。

作为一个例子，让我们运行 1994 年发布的《毁灭战士 2》。首先，从互联网存档下载 Zip 压缩包（Doom2.zip）。创建一个 Doom2 文件夹并将 Zip 文件解压到：

```
cd ~/Downloads
```
