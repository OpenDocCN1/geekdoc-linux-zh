
你可以向`run`命令传递你的程序通常情况下会接受的任何参数。通常情况下，GDB使用环境变量`$SHELL`的值来创建模拟环境。如果你需要，可以使用GDB的`set`和`unset`命令，在调试器中使用命令运行程序之前设置或取消环境变量。

要设置传递给程序的命令行参数，请输入`set arg arg1 arg2`，其中`arg1`和`arg2`（任意数量的参数）是被调试程序的选项和参数。使用`set environment env1 env2`作为你想要设置或取消的环境变量占位符。

## 在调试器中检查代码

函数`index_to_the_moon`中发生了什么导致了错误？你可以执行`backtrace`（或`bt`）命令来生成导致段错误的函数调用树。`backtrace`通常不会告诉你问题是什么，但它会更精确地显示你问题发生在何处。以下是你系统中示例的函数跟踪回溯：

```bash
(gdb) backtrace
#0 0x080483db in index_to_the_moon (ary=0xfffffc0) at debugme.c:24
#1 0x00008266 in main () at debugme.c:12
```

*(注：此处根据上下文逻辑补全了可能的回溯内容，原文中该部分为截断或示例)*

*(注：原文提供的 backtrace 示例在输入中似乎不完整，翻译时保持格式一致)*

# 第29章 ♦ 编程工具与实用程序 813

GDB还可以使用`whatis`命令告诉你变量的类型。GDB的`whatis`命令与`man -f`命令相当，后者在系统命令的`whatis`数据库中搜索这些系统命令的简短描述（手册页`whatis`数据库与GDB使用的`what`命令完全独立）。`man`的`whatis`数据库作用于系统命令，而GDB的`whatis`命令描述程序中使用的变量类型和其他数据结构。

```
(gdb) whatis i
type = int
(gdb) whatis ary
type = int *
(gdb) whatis index_to_the_moon
type = void (int *)
```

除非你已经知道程序中所有变量的类型（当然了！），否则这个功能似乎没用。但是，当你第一次需要调试别人的代码，或者修复一个几个月没见过源文件的多文件项目时，你会改变主意的。`whatis`命令还可以帮助你追踪由于给变量赋值不当的值导致的错误。

# 设置断点

在调试有问题的代码时，在某些点停止执行通常是有用的。也许你希望在代码进入已知有问题的区域之前停止执行。在其他情况下，你可以设置断点，以便在执行流的特定点查看某些变量的值。在其他情况下，你可能会发现停止执行以便逐条执行代码指令是很有用的。

GDB允许你在`de`若干种不同类型的代码结构上设置断点，包括行名和函数名，还允许你设置条件断点，即只有在满足特定条件时代码才会停止。要在某行设置断点，请使用以下语法：

```
(gdb) break linenum
```

要在代码进入函数时停止，请使用以下命令：

```
(gdb) break functionname
```

在何种情况下，GDB都会在执行指定行或进入指定函数之前停止执行。然后你可以使用`print`来显示变量（例如），或者使用`list`来查看正在执行的代码。如果你有一个多文件项目，并想在当前文件之外的行代码或函数中停止执行，请使用以下形式：

```
(gdb) break filename:linenum
(gdb) break filename:funcname
```

条件断点通常更有用。它们允许在满足特定条件时临时停止程序执行。设置条件断点的正确语法如下：

在前面的代码中，`expr`可以是任何求值结果为非零）的表达式。例如，以下命令会在变量`i`等于15时在调试的第24行停止执行：

```
(gdb) break 24 if i == 15
```

```
Starting: /home/kode/debug

Breakpoint 1 at debugme.c, line 24

ary[i] = i
```

停止时`i`的任意选择是为了演示条件断点。如你所见，`gdb`停止在第24行。快速`print`确认了它在`i`达到请求值时停止了：

```
(gdb) print i
```

在命中断点后恢复执行，输入`continue`。如果你设置了许多断点并忘记了哪些被触发了，请使用`info breakpoints`命令来刷新记忆。

# 源码操作

在多文件项目中通过GDB定位特定的变量或函数是轻而易举的事，只要你使用`-d`选项来告诉它去哪里查找额外文件。当并非所有的源代码都位于你的工作目录或程序的编译目录（记录在它的符号表中）时，这特别有帮助。要指定一个或多个包含源代码的额外目录，请使用一个或多个`dirname`选项启动GDB，如此示例所示：

```
$ gdb -d /source/project1 -d /old/project1 -d /home/ba/src
```

要在文件中查找特定字符串的下一次出现，请使用`search`命令。使用反向搜索（`reverse-search`）查找字符串的上一次出现。例如，如果你想在`debugme.c`中查找单词“return”的上一次出现（参见列表29-5），请使用反向搜索命令。GDB将遵循并显示：

```
(gdb) reverse-search return
```

`search`和`reverse-search`命令对于拥有几十或数百行的大型源文件特别有用。`reverse-search`命令的一个用途是找到变量第一次被使用或定义的文件和/或行。`search`命令同样允许你轻松地定位程序符号（变量、宏或函数）被使用的地方，也许找到意外更改变量的用法，或者在不该调用函数的地方。

## 总结

本章带你快速游览了Linux程序员使用的最常用的几个程序和实用程序。你学习了如何编译`GCC`程序，如何自动化编译程序，以及如何使用`ld`、`nm`和`ldconfig`等程序查找有关编程库的信息。你还学习了足够的源码控制系统`RCS`和`CVS`知识，能够熟悉它们的术语以及如何使用它们最基本的功能。最后，你学习了如何使用GNU调试器`GDB`来找出程序为何失败，或者至少在哪里失败。

# 介质

附带《Linux Bible 2006 Edition》的DVD和CD包含12种不同的Linux发行版。其中两个发行版可以直接从DVD启动并运行版`KNOPPIX`，或安装到你的硬盘（`Fedora Core`）。两个可以从CD启动并运行版（`Damn Small Linux`）并安装到你的硬盘（`Debian`）。其他的可以从这些介质之一刻录到CD-ROM中并单独安装。

关于在DVD上安装或启动各种Linux发行版的通用信息见第7章。使用和安装每个Linux发行版的特定说明包含在第三部分的其他章节中（见第8到第19章）。

![](img/a123b4f2456cac935474ae2401b95b01_848_0.png)

CD和DVD上的软件受GNU公共许可证（`GPL`）或介质上每个软件发行版包含的其他许可证的保护。请自风险使用DVD和CD上的软件（就像使用任何`GPL`软件一样）。请参考`README`、`RELEASE-NOTES`以及随每个发行版分发的任何许可许可文件，并确保你同意在使用软件时遵守它们所列出的条款。

# 在 DVD 上查找 Linux 发行版

以下章节描述了随附此书的DVD上的五种Linux发行版。`Fedora Core`和`KNOPPIX`可以从DVD直接启动。其他发行版位于DVD上的`distros`目录。

# Fedora Core 4 Linux

DVD包含了通常位于四张CD完整`Fedora 4`发行版。这是尝试书中书中大多数操作的推荐Linux发行版。你可以直接从DVD安装`Fedora 4`，而无需制作CD。

因为包含了完整的`Fedora 4 Linux`发行版，你可以访问广泛的软件包（1600多个），让你体验Linux作为桌面、服务器或程序员工作站。

安装和使用`Fedora 4`的详情见第8章。

如果你发现`Fedora Core 4`不够用，可以考虑购买《Fedora Enterprise Linux 4》（Wiley Publishing）以了解更多该发行版。虽然部分内容与本书重叠，但你将获得关于`Fedora Core 4`各类型服务器的完整覆盖。

# SUSE Linux

DVD上的五CD`SUSE 10.0 OS`安装（也称为`OpenSUSE 10.0`）镜像允许安装完整的`OpenSUSE`操作系统。`SUSE`由`Novell`开发并支持，`Novell`将`SUSE`作为更广泛的企业Linux和`NetWare`软件的一部分。`OpenSUSE`是`Novell`赞助、社区支持的免费Linux。
