
Unix 和 Linux 系统很大程度上由在命令行执行的短小、简洁的命令组成。通常，每个命令至少对应一个 man 页（帮助页）。Linux man 手页与性别无关：man 代表 manual（手册）。

曾几何时，手页是随 Unix 系统附带的唯一文档。在某个地方，我们仍然保留着初当 Unix 用户和系统管理员时收到的薄书。它包含的所有都是手页，根据这些内容，我们应该安装 Unix 系统。多年以后，我们仍然首先查看手页，以快速了解一个命令的功能、在命令行上应该使用哪些参数或应该设置哪些值。

本附录将向你展示如何使用 `man` 命令，如何阅读和理解手页，以及如何找到其他可能帮助你理解正在研究的 Linux 命令的手页。手页本质上就是帮助文件。

# 查看手页的结构

你可以在系统中的多个目录找到手页：

- `/usr/man`
- `/usr/local/man`
- `/usr/X11/man`
- `/usr/lib/perl15/man`

## 第六部分：附录

每个目录都分为手册的子目录（称为章节 sections）。见表 D-1。

| 表 D-1: 手页章节及查找位置 |
|---|---|---|
| 手章节 | 章节涵盖内容 | 在此目录可用 |
| Man 1 | 用户命令 | `/usr/share/man/man1` |
| Man 2 | 系统调用 | `/usr/share/man/man2` |
| Man 3 | 库函数 | `/usr/share/man/man3` |
| Man 4 | 特殊文件 | `/usr/share/man/man4` |
| Man 5 | 文件格式 | `/usr/share/man/man5` |
| Man 6 | 游戏（看看大家都去那个章节了！） | `/usr/share/man/man6` |
| Man 7 | 杂项 | `/usr/share/man/man7` |
| Man 8 | 系统管理命令 | `/usr/share/man/man8` |
| Man 9 (mann) | nroff, troff, 和 groff (以及现在的 tk) 宏 | `/usr/share/man/man9` |

大多数目录包含多个章节。两个章节可能都包含同名命令的条目。例如，章节 1 有一个 `open` 命令，而章节 2 有一个 `open` 系统调用。为了确保你阅读的是正确的命令，可以在 man 行上指定命令。例如：`[paul@veracruz paul]$ man 2`

大多数手页章节（基本上是信息数据库）包含两个部分：

- 一个由名为 `intro.n` 的文件表示页面，其中 `n` 是与章节名称对应的数字。
- 所有命令、调用、库名和文件名，由名为 `command.n` 的文件表示，其中 `n` 是章节名称。

如果你使用 `cd` 切换到 `/usr/man/man1` 目录并执行 `1s` 命令，你会看到类似 `cat.1` 和 `grep.1` 的文件。奇怪的是，你没有找到名为 `cd.1` 的文件，因为 `cd` 命令内置在不同的 shell 中，它的文档包含在 `bash.1` 文件或 `csh.1` 文件中。

![](img/5275bfa3908ad63320aaea42eefe467c_393_0.png)

# 附录 D: 挖掘 Linux 手页

如果你使用 `bash` 作为 shell，可以按如下方式获取其他内置命令的信息：

```
[paul@veracruz paul]$ help
```

`intro` 页面简要描述了手册的该部分，并指示你是否需要了解该章节的特殊知识。例如打印一个 intro 页面：

```
[paul@veracruz paul]$ man 2 intro
```

或者

```
[paul@veracruz paul]$ man 3 intro
```

## 使用 man 命令

好了，如果你没听懂标题里的双关语，你需要多看一些动画（注：原文此处为 cartoons，可能是指演示或笔误）。

要开始使用手页，请遵循以下步骤：

1. 启动 Linux，以用户身份登录（普通用户或 root）。
2. 输入 `man` 命令。系统会询问你想要哪个手页。`man` 命令的语法（与其他许多命令一样）至少需要一个参数。
3. 通过输入 `man ls` 提供参数。第一个 `man` 是命令，第二个 `man` 告诉 Linux 你想要手册页本身的信息。系统可能会让你等一下，它会将页面格式化到屏幕上，然后显示该命令的参考页。请阅读第 15 章获取更多关于命令组织的信息。
4. 如果屏幕底部出现冒号 (::)，按下空格键查看下一页，或使用方向键在页面间移动。
5. 如果屏幕底部出现冒号 (::)，按下空格键查看下一页，或使用方向键在页面间移动。

## 描述

描述部分是对命令功能的简要介绍，随后将通过选项所指定的命令要执行的操作进行扩展说明。

描述的一个很好的例子是 `man` 命令自身的帮助页。

## 选项

选项部分告诉命令如何处理参数中的数据。

每个选项都会修改命令的行为，可能是剧烈的，也可能是细微的。

选项还可以向命令传递关于在哪里找到文件的信息。

三种类型的选项有：

- 无参数
- 附带参数
- 位置参数

无参数意味着该选项有一个连字符，后面跟着一个或多个单字符选项。例如：

```
[paul@veracruz paul]$ ps -ax
```

`A` 和 `x` 没有任何任何其他需要查看的值。但在接下来的命令中：

```
[paul@veracruz paul]$ ps 1pq -Pzklsa
```

`-P` 选项需要你提供一个参数，在这个例子中，是 `zklpsa`。

## 环境变量

有时候，为了减少你需要提供给命令的信息，你可以设置一个环境变量。每个 shell（或命令解释器）都有其工作运行的环境。这个环境（在创建时）由某些打开的文件、一些内存以及几乎总是存在的某些环境变量组成。

使用 `bash` shell，输入以下内容（如果你不确定是否在使用 `bash` shell，请在命令提示符下输入 `bash` 然后继续执行示例）：

```
[paul@veracruz paul]$ printenv
```

## 附录 D：挖掘 Linux 帮助页

你会看到类似这样的内容：

```
USERNAME=
COLORTERM=gnome-terminal
HISTSIZE=1000
HOSTNAME=veracruz.paunchy.net
LOGNAME=paul
HISTFILESIZE=1000
INIT_VERSION=sysinit-2.74
MAIL=/var/spool/mail/paul
LD_LIBRARY_PATH=/usr/local/applixware/axdata/axshlib/bin
TERM=xterm
PATH=/usr/bin:/usr/bin:/usr/local/bin:/usr/X11R6/bin:
/usr/X11R6:/usr/local/netscape:
/home/paul/bin:/usr/X11R6/bin:
/usr/local/netscape:/home/paul/bin
CONSOLE=/dev/console
KEDIR=/usr
HOME=/paul
INPUT=/etc/inputrc
PRELEVEL=N
RUNLEVEL=5
SHELL=/bin/bash
AUTHORITY=/home/paul/.authority
USER=paul
PGDBAT=/var/lib/pgsql
BASH_ENV=/home/paul/.bashrc
BOOT_IMAGE=linux
DISPLAY=0
SESSION_MANAGER=/local/atlas.paunchy.net:/tmp/.ICE-
unix/7376,tcp/atlas.paunchy.net:1371

OSTYPE=linux
WINDOWID=62914566
GEMSESSION=Default
LD_PRELOAD=/usr/local/lib/open.so
SHLVL=3
=/usr/bin/printenv
```

这个列表有很多环境变量，但我们没有空间描述它们的所有。所以，这里是最重要的几个：

- `PATH` 告诉 shell 查找命令的所有地方。
- `HOME` 告诉 shell 当你没有提供任何参数时应该去哪里。
- `OSTYPE` 告诉 shell 和程序它们正运行在什么样的操作系统上。

不同的 shell 有设置这些变量的不同方法（以及创建和设置），来告诉命令要做什么。

![](img/5275bfa3908ad63320aaea42eefe467c_398_0.png)

## 376 第六部分：附录

一个变量没有被设置为某些值（null）与一个不存在的变量（unset）不同，这些差异在命令之间各异。例如，在前面的列表中，第一个变量 `USERNAME` 被设置为了 NULL。这一事实是重要的。被设置为 NULL 而不是其他值的实对于各种程序也是重要的。

![](img/5275bfa3908ad63320aaea42eefe467c_399_0.png)

## 诊断
