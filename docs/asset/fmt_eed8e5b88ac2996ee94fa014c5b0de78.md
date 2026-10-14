
如果你想强化在上一个项目中用过的技能，为什么不玩玩大大陆式三牌 Briscola 呢——这是一种简单且传统的意大利纸牌游戏（见图 9-15）？与 Python 脚本 `pyWings` 不同，Briscola 是另一种风格的脚本，用名为 Tcl 的脚本语言编写，并使用名为 Tk 的工具来创建图形界面。

![](img/58abec7ac6c22ade6357fd77ea421da3_216_0.png)

图 9-15：Briscola 游戏

## 9C-1: 获取 Briscola

你已经准备好开始“安装” Briscola 了。

要做到这一点，只需打开 Terminal 窗口，输入以下命令字符串，然后按回车：

```
wget http://www.rigacci.org/comp/software/briscola/briscola-4.1.tar.gz
```

注意：如果你通过这种方式下载 Briscola 遇到任何问题，也可以从本书的网站下载：http://www.edgy-penguins.org/UFNG/

在你的 Terminal 窗口中，你会看到 `wget` 正在运行，它连接到存储 Briscola 的站点并下载文件。完成后，你将在你的家目录中找到 Briscola 的 tar 包。

## 9C-2: 解压 Briscola tar 包并重命名 Briscola 文件夹

解压 Briscola tar 包的过程与 `pyWings` 基本上相同；然而，Briscola 已经封装在它自己的文件夹中，你不需要为它创建一个特殊的文件夹。

虽然我确定你现在已经熟悉操作了，但我会再告诉你一遍。只需打开 Terminal 窗口，输入以下命令，并按回车：

```
tar -xzf briscola*.
```

现在家目录中会出现一个名为 `Briscola-4.1` 的新文件夹，里面包含了所有的 Briscola 文件。为了方便以后处理，让我们把文件夹名称缩短为 `briscola`。你已经知道如何通过右键方法完成操作，但这次让我们通过命令行来实现。要做到这一点，你可能会很惊讶地发现可以使用 `mv` 命令，后面跟上你要更改的文件名，最后是新文件名。

通过输入以下命令并按回车尝试一下：

```
mv briscola-4.1 briscola
```

## 9C-3: 准备 Briscola 脚本

大多数程序以 tar 包形式提供时都会包含一个 `README` 文件，它告诉用户如何安装该程序。与 `pyWings` 类似，Briscola 也包含一个 `README` 文件，它告诉我们如何安装和运行它。我们将编辑位于 `briscola` 目录下的文件。

要按照 `README` 文件的说明，请执行以下步骤：

- 在 Terminal 窗口中输入 `cd briscola` 并回车，进入该目录以编辑 `briscola` 文件。
- 使用 Pico 编辑器，输入 `pico briscola` 并回车。
- 在编辑器中，将第一行的 `#!/bin/bash` 改为 `#!/usr/bin/env wish`。
- 将第二行的 `set prefix = .` 改为 `set prefix = /usr/share/games`。
- 按键盘上的 CTRL-X。
- 输入 `y` 并按回车以保存你的更改。

## 9C-4: 将 Briscola 文件夹移动到全局位置

你可以将 Briscola 文件夹移动到 `LocalApps` 文件夹并像运行 `pyWings` 那样运行它，但这次让我们尝试一种不同的方法，将其移动到全局区域。这不仅可以防止它被意外清理，还能让同一台电脑上的其他用户玩游戏。你需要使用 `sudo` 命令来操作，以便获得对这些文件夹的写入权限。

要做到这一点，只需在 Terminal 窗口输入以下命令并按回车：

```
sudo mv briscola /usr/share/games
```

当提示输入密码时，输入密码并回车。

## 9C-5: 为 Briscola 创建启动链接

即使你已经将 Briscola 移动到了全局位置，你仍然无法通过简单的单词命令来运行它，因为 `briscola.tk` 文件不在系统的命令搜索路径中。就像你对 `pyWings` 执行的那样：

- 输入 `ln -s /usr/share/games/briscola.tk /usr/local/bin/briscola` 并按回车，为 `briscola` 文件创建一个链接。
- 现在你只需在 Terminal 中输入 `briscola` 即可运行游戏。

实际上运行。一旦完成此翻译，计算机就不再需要处理这些高级指令了；它在每次运行程序时，只需读取翻译后的版本即可。这就像拥有一本外文书的译文，你可以随地阅读。由于计算机可以运行编译后的程序而无需同时使用解释器，因此编译程序的运行速度比脚本快。因此，所有操作系统的大多数应用程序都是编译过的。

## 基础知识

从源代码编译应用程序并安装它的实际过程非常简单——真正是“一、二、三”就能瞬间完成的魔术。基本上，在从压缩文件（通常是 tarball 格式）中提取源代码后，你将使用以下命令来完成任务：

```
./configure
```

配置一个 `makefile`，它为 `make` 命令提供指令。

```
make
```

将源代码翻译成计算机可以理解的目标代码。

```
sudo make install
```

让你在受保护的文件夹中获得写入权限，然后安装应用程序。

```
make clean
```

在过程完成后清理遗留文件（清理现场）。

我知道这听起来有很多命令，但正如我常说的，实际执行页面上显示的内容要容易得多，所以不要害怕。

## 9D-1: 安装你需要的工具

在进行其他事情之前，你必须让系统准备好执行你要求的任务。由于 Ubuntu 是为普通用户设计的，它并没有自带你从源代码编译应用程序所需的各种程序和库。幸运的是，完成工作所需的所有内容都可以 Ubuntu 软件中心获得。为了给本章的工作（以及你未来可能自行完成许多许多工作）做好准备，请搜索并安装以下包：

- `build-essential`
- `libgtk2.0-dev`

## 9D-2: 下载并提取 Xmahjongg 文件

为了获得从源代码编译程序的实操经验，你将操作一个名为 `Xmahjongg` 的游戏，如图 9-17 所示。如果你尝试使用 Ubuntu 发行版自带的 `Xmahjongg` 版本，你会发现它对眼睛更友好，色彩更丰富（访问项目网站 http://www.lcdf.org/xmahjongg/ 可以一略其全彩模式的盛况）。

![](img/58abec7ac6c22ade6357fd77ea421da3_222_0.png)

图 9-17：Xmahjongg 游戏

`Xmahjongg` 可以通过 Ubuntu 软件中心获取，因此没有绝对按照你即将采取的方法进行安装，但这样做提供了一个学习如何从源代码编译程序的机会。代码量并不大，所以不会花费太多时间，而且不需要任何调试。

要开始，你首先必须在 http://www.lcdf.org/xmahjongg/xmahjongg/ 下载 `Xmahjongg` 项目页面。下载 tarball `xmahjongg-3.7.tar.gz`，如果有更新的版本则下载新版本。不要下载页面上提供的任何其他类型的文件。

如果你愿意，也可以使用你在项目 9C-1 中学会的 `wget` 命令下载 `Xmahjongg` tarball。只需打开终端窗口，遵循以下命令，并按回车键：

```
wget http://www.lcdf.org/xmahjongg/xmahjongg-3.7.tar.gz
```

一旦文件位于你的硬盘上，就解压 `xmahjongg-3.7.tar.gz` 文件。你可以像在本章早期学到的那样使用命令行，也可以通过双击文件将其内容拖入适当的文件夹中。
