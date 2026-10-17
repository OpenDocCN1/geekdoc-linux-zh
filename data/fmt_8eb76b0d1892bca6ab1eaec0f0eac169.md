
## 使用 Shell 提示符

如果你的 Linux 系统没有图形用户界面（或者界面目前无法工作），你在登录后很可能会看到 Shell 提示符。从 Shell 输入命令可能是你使用 Linux 系统的主要手段。

普通用户的默认提示符只是一个美元符号：

```
$
```

`root` 用户的默认提示符是一个井（也称为哈希标记）：

```
#
```

## 第 2 章 + 从 Shell 运行命令 31

在大多数 Linux 系统中，`$` 和 `#` 提示符之前会显示你的用户名、系统名称和当前目录名称。例如，在名为 `/tmp` 的当前名为 `pine` 的计算机上，名为 `jake` 的用户登录提示符显示如下：

```
[jake@pine tmp]$
```

你可以更改提示符以显示任何你喜欢的字符——例如，你可以使用当前目录、日期、本地计算机名称或任何字符字符串作为你的提示符。要配置你的提示符，请参阅本章稍后的“设置你的提示符”部分。

虽然 Shell 提供了极其丰富的功能，但通过输入几个命令就可以轻松开始。尝试本节剩余部分显示的某些命令，以熟悉你当前的环境。

在接下来的示例中，符号 `$` 和 `#` 符号表示提示符。提示符后面跟着你输入的命令（然后按下 `Enter` 键或 `Return` 键，取决于你的键盘）。随后的行显示了该命令产生的输出。

## 使用终端窗口

在桌面 GUI 运行时，你可以打开一个终端模拟器程序（有时被称为 `Terminal`）来启动 shell。大多数 Linux 发行版都能让你轻松地从 GUI 进入 shell。以下是从 Linux 桌面启动终端的两种常用方法：

- 右键点击桌面。在弹出的上下文菜单中，找到 `Shells`、`New Terminal`、`Terminal Window`、`Xterm` 或某些类似的项目并选择它。
- 点击面板菜单。许多 Linux 桌面在屏幕底部包含一个面板，你可以从那里启动应用程序。例如，在 `Red Hat` 系统中，你可以选择 `Red Hat` 图标，然后选择 `Tools > Terminal` 打开终端。

在所有情况下，你都应该像在没有 GUI 的 shell 中一样可以输入命令。Linux 提供了不同的终端模拟器。以下是你的 Linux 系统使用的默认终端之一：

- `xterm` — 一种用于 `X Window` 系统的常用终端模拟器（事实上，我从未见过哪个主流 Linux 发行版的 `X Window System` 不包含 `xterm`）。尽管它不提供菜单或任何特殊功能，但在大多数支持 GUI 的 Linux 发行版中都可用。
- `gnome-terminal` — `GNOME` 自带的默认终端模拟器。它消耗的系统资源比 `xterm` 多，并且具有用于剪切和粘贴、打开新终端标签页或窗口的实用菜单。
- `kterm` — 带有 `KDE` 桌面环境的 `kterm` 终端模拟器。使用 `kterm`，你可以显示多语言文本编码和不同颜色的文本。

如果你不喜欢默认的终端模拟器，可以从 `Emulator` 列中输入一个命令名称来尝试其中一个。

## 使用虚拟终端

许多 Linux 系统（包括 `Fedora` 和 `Red Hat Enterprise Linux`）会在计算机上启动多个运行的终端。虚拟终端是一种在不运行 GUI 的情况下同时打开多个会话的方法。

你可以在虚拟终端之间切换，这可能允许你在 GUI 的工作区之间切换。按下 `Ctrl+Alt+F1`（或 `F2`、`F3`、`F4`，在 `Fedora` 和其他 Linux 系统上一直到 `F6`）来显示六个虚拟终端之一。虚拟终端之后的下一个工作区是 GUI，如果有四个虚拟终端，你可以通过按下 `Ctrl+Alt+F7` 返回 GUI（如果它正在运行）。对于具有四个虚拟终端的系统，通过按下 `Ctrl+Alt+F5` 返回到 GUI）。

## 选择你的 Shell

在 Linux 系统中，你的默认 shell 是 `bash`。要找到你当前的登录 shell 是什么，请输入以下命令：

```
$ echo $SHELL
/bin/bash
```

在这个示例中，它是 `bash` shell。还有许多其他 shell，你只需从当前 shell 中输入新 shell 的命令（`ksh`, `tcsh`, `csh`, `sh`, `bash` 等）即可激活不同的 shell。

> 大多数 Linux 系统都包含了本节中描述的所有 shell。某些较小的 Linux 发行版可能只包含一两个 shell。找到特定 shell 是否可用的最佳方法是输入该命令并查看它是否启动。

你可能想选择一个不同的 shell 使用，是因为：

- 你习惯于使用 `UNIX System V` 系统（通常默认为 `ksh`）或 `Sun Microsystems` 以及其他基于 `Berkeley UNIX` 的发行版（通常默认为 `csh`），并且你更倾向于使用这些环境的默认 shell。
- 你想运行为特定 shell 环境创建的 shell 脚本，并且你需要运行为这些脚本而制作的 shell，以便你测试或使用这些脚本。
- 你可能仅仅是觉得某一个 shell 的功能优于其他。例如，我所在的 Linux 用户组的一员更倾向于使用 `sh` 而不是 `bash`，因为他不喜欢 `bash` 设置别名（`aliases`）的方式。

尽管大多数 Linux 用户对某个 shell 或另一个 shell 有偏好，但当你知道如何使用其中一个 shell 时，通过偶尔参考该 shell 的 man 手页（例如，输入 `man bash`），你可以快速学习其他任何一个。大多数人使用 `bash` 是因为他们没有特定的理由去使用不同的 shell。在第 4 章中，你将学习如何为用户分配默认 shell。

以下章节介绍了 Linux 中提供的几个最常用的 shell。

### 使用 bash (以及早期的 sh) Shell

名字 `bash` 是 `Bourne Again Shell` 的缩写，承认了 `bash` 的根源来自 `Steve Bourne` 在 `AT&T` 贝尔实验室创建的 `Bourne shell`（`sh` 命令）。自由软件基金会的 `Brian Fox` 在 `GNU` 项目的赞助下创建了 `bash`。开发随后由西储储大学的 `Chet Ramey` 接手。

`Bash` 包含了最初为 `sh` 和 `ksh` shell 开发的功能，在每个 UNIX 系统中都包含了，以及 `csh` 功能。无论你使用的 Linux 系统，预计 `bash` 是默认 shell。本章的大多数示例都基于 `bash` shell。

### 使用 tcsh (以及早期的 csh) Shell

`csh` 是 C 语言 shell。`csh` shell 由 `Bill Joy` 创建，并在 `Berkeley UNIX` 系统（如 `Sun Microsystems`）中作为默认 shell 使用。原始 `csh` 的许多功能，如命令行编辑和它的历史机制，也包含在 `tcsh` 中。虽然在大多数 Linux 系统上你可以运行 `csh` 和 `tcsh`，但这两个命令指向同一个可执行文件。也就是说，启动 `csh` 实际运行的是 `tcsh` shell。

### 使用 ash

`ash` 是 `Berkeley sh` shell 的轻量级版本。它没有 `sh` 的许多基本功能，缺少命令历史等功能。`Kenneth Alsmith` 创建了 `ash`。

`ash` 是适用于资源较少的嵌入系统的良好 shell。`ash` shell 的大小只有 `bash` 的六分之一（`ash` 为 `100k`，`bash` 为 `680k`）。由于如今内存价格便宜，许多嵌入式和小型 Linux 系统都有空间包含完整的 `bash`。

### 使用 ksh

`ksh` shell 由 `David Korn` 在 `AT&T` 贝尔实验室创建，是 `sh` shell 的前身。它是 UNIX 系统的默认且最常用的 shell。`ksh` 的开源版本最初在许多基于 `rpm` 系统（如 `Fedora` 和 `Red Hat Enterprise Linux`）中作为 `pdksh` 包的一部分可用。现在，`David Korn` 已将原始 `ksh` shell 发布为开源，因此你可以在大多数 Linux 系统中作为 `k` 软件包的一部分找到它。

### 使用 zsh

`zsh` shell 是另一个 `sh` shell 的克隆。它符合 `POSIX` 标准（如同 `bash`），但包含一些不同的功能，例如拼写检查和不同的命令编辑方法。第一代 `Mac OS` 系统使用 `zsh` 作为默认 shell，尽管现在默认使用的是 `bash`。

## 探索 Shell

一旦你获得了 Linux shell 的权限，就可以通过输入一些简单的命令开始。本章稍后的“在 Linux 中使用 Shell”部分将提供有关选项、参数和环境变量的更多信息。目前，以下章节将帮助你探索 shell 的部分。

## 第 2 章 + 从 Shell 运行命令

## 35

![](img/a123b4f2456cac935474ae2401b95b01_66_0.png)

如果你不喜欢默认的 shell，只需输入你想临时尝试的 shell 名称即可。要永久更改你的 shell，请使用 `usermod` 命令。例如，要将名为 `chris` 的用户的 shell 更改为 `csh` shell，请在 shell 中以 `root` 用户身份运行输入以下命令：
