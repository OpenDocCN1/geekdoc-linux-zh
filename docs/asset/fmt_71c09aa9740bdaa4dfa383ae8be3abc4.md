
GDB 还可以使用 `whatis` 命令告诉你变量的类型。GDB 的命令与 `man` 命令相当，后者在系统命令数据库中搜索这些命令的简短描述（man 手页数据库与 GDB 使用的 `whatis` 命令完全独立）。`man` 作用于系统命令，而 GDB 的 `whatis` 命令描述程序中使用的变量和其他数据结构。

```gdb
(gdb) whatis i
type = int
(gdb) whatis ary
type = *
(gdb) whatis index_to_the_moon
type = void (int *)
```

这个功能可能看起来相当没用，因为当然你当然知道自己程序中所有变量的类型（对吧！）。但当你第一次必须调试他人的代码或必须修复一个几个月没见过源文件的多文件项目时，你会改变主意的。`whatis` 命令还可以帮助你追踪由于给变量分配不当值而导致的 bug。

## 设置断点

在调试问题代码时，在某些点停止执行通常很有用。也许你想在代码进入已知问题的区域之前停止执行。在其他情况下，你可以设置断点，以便在执行流的给定点查看变量的值。在其他情况下，你可能会发现停止执行以便逐条指令地执行代码是很有用的。

GDB 允许你在几种不同的代码结构上设置断点，包括行号和函数名，还允许设置条件断点，即只有在满足特定条件时代码才会停止。要在行号上设置断点，请使用以下语法：

```gdb
(gdb) break linenum
```

## 编程工具与实用程序

要在代码进入函数时停止执行，请使用：

```gdb
(gdb) break funcname
```

在任何情况下，GDB 都会在执行指定的行号或进入指定的函数之前停止执行。然后你可以使用 `print` 显示变量值（例如），或者使用 `list` 审查即将执行的代码。如果你有一个多文件项目，并想在当前源文件的代码行或函数中停止执行，请使用以下形式：

```gdb
(gdb) break filename:linenumber
(gdb) break filename:funcname
```

条件断点通常用。它们允许你在满足特定条件时临时停止执行。设置条件断点的语法如下：

```gdb
(gdb) break linenumber if expr
(gdb) break funcname if expr
```

在前面的代码中，`expr` 可以是任何求值为真（非零）的表达式。例如，以下 break 命令会在变量 `i` 等于 15 时在第 24 行停止执行：

```gdb
(gdb) break 24 if i == 15
Breakpoint 1 at 0x080483cb: file debugme.c, line 24.
(gdb) run
Starting program: /home/kwall/code/debugme
Breakpoint 1, index_to_the_moon (ary=0xbffff4b0) at debugme.c:24
ary[i] = 15;
```

### 源码源码

在多文件项目中，使用 GDB 定位特定的变量或函数是轻而易举的，前提是你使用 `-d` 选项告诉它去哪里寻找额外的源代码文件。当并非所有的源代码都位于当前工作目录或程序编译目录（GCC 在其符号表中已记录了该目录）时，这个选项就特别有用。

要指定包含源代码的一个或多个额外目录，请使用一个或多个 `-d dirname` 选项启动 GDB，如下示例所示：

```
$ gdb -d /source/project1 -d /opensource/project1 \
-d /home/bubble/src killerapp
```

要在当前文件中查找模式字符串的下一次出现，请使用 `search` 命令。使用 `reverse-search-string` 查找字符串的上一次出现。例如，如果你想在 `debugme.c` 中查找单词 "return" 的上一次出现（参见列表 30-5），请使用命令 `reverse-search return`。GDB 会配合并显示文本：

```
(gdb) reverse-search return
17 return ret;
```

`search` 和 `reverse-search` 命令对于拥有几十或数百行的大型源文件特别有用。`reverse-search` 命令的一个常见用途是找到变量首次被使用或定义的文件和/或行号。`search` 命令同样让你能够很方便地定位程序符号变量、宏或函数使用的每个位置，也许是为了找到意外更改变量的地方，或者找到在不该调用某个函数的地方。

## 总结

本章带你快速领览了 Linux 程序员使用的几个最常用的程序和实用工具。你学习了如何使用 GCC 编译程序，如何使用 `make` 自动完成程序编译，以及如何使用 `ldd`、`nm` 和 `ldconfig` 等工具查找有关编程库的信息。你还学习了足够的关于源码控制系统 RCS 和 CVS 的知识，能够熟悉其术语并使用它们最基本的功能。最后，你学习了如何使用 GNU 调试器 `GDB` 来找出程序失败的原因，至少是失败的位置。

# 附录 A

## 媒体

随附《Linux Bible 2009 版》的 DVD 和 CD 包含了多种你可以使用的 Linux 系统。其中某些 Linux 系统可以进行即时启动并运行，而另一些可以作为 Linux 系统永久安装到硬盘上。有些则两者兼顾。

这里包含的大多数 Linux 系统都是来自不同 Linux 项目的官方即时 CD 和安装 CD 的轻微修订版本。对这些 CD 所所的修改仅是为了让每个系统都能从 DVD 或 CD 上的单一启动界面启动。然而，一旦你选择了要启动的 Linux，它的行为应该与所选 Linux 项目的原始 CD 完全一致。

关于运行或安装 CD 和 DVD 上这些特定 Linux 发行版的通用信息请见第 8 章。使用和安装每个 Linux 发行版的具体说明包含在第五部分的其他章节（参见第 17 至 28 章）。

> DVD 和 CD 上包含的软件受 GNU 公共许可证 `GPL` 或介质中每个软件发行版包含的其他许可保护。自行风险使用 DVD 和 CD 上的软件（就像使用任何 GPL 软件一样）。请参考每个发行版随附的 README、RELEASE-NOTES 以及任何许可文件，并在使用软件前务必确认同意它们中列出的条款。

## 在 DVD 上查找 Linux 发行版

接下来的章节描述了随书附 DVD 上的 Linux 发行版。所有这些发行版都可以直接从 DVD 启动，尽管某些被设计作为即时 CD 运行，而另一些用于安装到硬盘。

### Fedora Linux

随书附的 DVD 包含了 Fedora 10 桌面即时/安装 CD 发行版，它通常位于单张 CD 上。Fedora 被用作书中许多过程的示例。你可以直接从 DVD 作为一个即时 CD 启动 Fedora，并使用该即时 CD 将相同的 Fedora 桌面永久安装到硬盘上。

要开始安装 Fedora，请将 DVD 插入电脑的 DVD 驱动器，重启并选择 `fedora`。安装和使用 Fedora 的细节请见第 18 章。书中描述的许多应用程序使用 Fedora 版本作为示例。如果应用程序不可用，请使用软件包管理器或 `yum` 命令从互联网安装该程序。

> 如果你喜欢 Fedora，可以考虑获取 Fedora 10 和 Red Hat Enterprise (Wiley Publishing, 2009) 以了解有关该发行版的信息。虽然部分内容与本书重叠，你会获得更多关于可用服务器的介绍。

### KNOPIX Linux

KNOPIX 5 即时 CD 发行版配置为从 DVD 启动。KNOPIX 是最流行的可启动 Linux，并提供了一些独特的功能使其与其他发行版区别来。要从 DVD 启动 KNOPIX，请将 DVD 插入电脑的 DVD 驱动器，重启并选择 `knopix`。使用各种方式配置 KNOPIX 的信息见第 21 章。

### Slackware Linux

DVD 包含了 Slackware 发行版。Slackware 是最古老的 Linux 系统，并在 Linux 爱好者中持续拥有忠实的追随者。要开始安装 Slackware，请将 DVD 插入电脑的 DVD 驱动器，重启并选择 `slackware`。第 24 章告诉你如何从书中的 DVD 或 CD 安装 Slackware。第 3 章描述了如何配置简单的管理器。

### Ubuntu Linux

DVD 包含 Ubuntu Intrepid 即时 CD。该镜像可即时运行，然后安装最小桌面系统。完成基本安装后可以从互联网进行进一步软件安装。要从 DVD 启动 Ubuntu 即时 CD 镜像，请将 DVD 插入电脑的 DVD 驱动器，重启并选择 `ubuntu`。电脑将启动一个用于桌面系统的 Ubuntu 即时版本。桌面图标让你将 CD 内容安装到硬盘。启动和安装 Ubuntu 的步骤见第 17 章。

### Mandriva Linux
