
要解压缩文件，使用以下命令：

```
# uncompress file.Z
```

与 gzip 类似，你必须指定一个带有 .Z 扩展名的文件名，否则 uncompress 会报错。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_136_0.png)

> 想了解 Linux 的其他压缩工具吗？在你的系统上查找 zip、unzip、zipcloak、zipnote、zipsplit、zless、zcat、znew、zmore、zcmp、pack、compact、shar、unshar 或 zforce。你可能找不到全部已安装，但你可以在喜爱的 Linux 软件站点（如 http://metalab.unc.edu/pub/Linux）找到与 OpenLinux 兼容的版本。

## Summary

## 摘要

本小时介绍了创建、删除、移动、复制、搜索、保存以及压缩文件和目录所需的基本 OpenLinux 命令。随着你在练习中对 OpenLinux 了解得更多，你将在基本知识之上构建更复杂和定制的命令。

## Q&A

## 问答

Q OpenLinux 还有其他文件压缩程序吗？

A 有的。你可能可以通过 bzip2 命令获得更好的压缩效果。该程序使用与 gzip 不同的压缩算法，并随 OpenLinux 包含在 /bin 目录下。你可以通过 .bz2 扩展名识别这些归档文件。

Q 我看到过一些扩展名为 .uu 的文件，想知道这些是否是压缩文件？

Q 如何查看二进制文件内部的内容？如果我尝试使用 cat 或 less 命令，会看到很多乱码。

A 尝试使用 strings 命令。有关如何将 strings 与 less 一起使用，请参阅第 6 小时“使用 Shell。”

Q 如何获取磁带归档中每个文件的更多信息？我知道 t 选项会显示文件和目录名称。

A 在 tar 命令行中使用 v 选项与 t 选项一起，可以查看磁带归档中每个项目的权限、所有者、组、文件大小、日期、时间以及名称。

## Exercises

## 练习

- 1. tar 程序可以在归档操作期间执行文件压缩。使用 tar 创建一个测试目录的压缩磁带归档。
- 2. OpenLinux 中包含了一些其他压缩程序。它们的名字是什么？（提示：使用你认为“apropos”合适的命令！）
- 3. 如何找到 OpenLinux 发行版中包含的所有压缩文件？

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_138_0.png)

## Hour 6

## 第 6 小时

## Using the Shell

## 使用 Shell

在本小时中，你将了解 shell。尽管在过去 10 年中个人计算的趋势是从命令行转向点按式界面，但 shell 在 Linux 中仍然非常活跃，并且被许多 Linux 程序使用。

本小时不会详细介绍 Linux 或 UNIX shell 的历史，也不会在命令行界面是否更容易或更好使用的问题上站队。也不涉及 shell 编程——本小时甚至整本书都没有足够的篇幅来做到这一点。本小时将讨论你可以在 OpenLinux CD-ROM 上找到的不同 shell，展示如何使用 shell 使你的 Linux 体验更愉快，并介绍使用 shell 和命令行的基础知识。

## What is a Shell?

## 什么是 Shell？

如果你没有使用 X Window System，shell 就是你使用的重要程序之一。shell 为 Linux 提供接口以便运行程序。事实上，shell 只是另一个 Linux 程序。

尽管你可以不使用 shell 设置和运行 Linux（有关详细信息，请参阅第 21 小时“基本系统管理”），即使你使用图形界面程序，你也可能会发现需要使用 shell 的命令行。

shell 是一个命令解释器，可用于启动、挂起、停止甚至编写程序。shell 是 Linux 的一个组成部分，也是 Linux 和 UNIX 设计的一部分。如果把 Linux 内核想象成球体的中心，shell 就是围绕内核的外层。当你从 shell 或其他程序向 Linux 传递命令时，内核（通常）会做出适当的响应。

shell 的类型有很多，但除了第 5 小时“操作和搜索命令”中讨论的视觉 shell Midnight Commander 外，你的 CD-ROM 上至少有五种。你可以通过查看 /etc/passwd 文件的内容或在文件中搜索你的用户名来确定登录 Linux 时使用的 shell。请看以下示例：

```
# fgrep bball /etc/passwd
bball:x:100:100:William H. Ball,,,:/home/bball:/bin/bash
```

你的 shell 列在 passwd 文件条目的末尾（fgrep 搜索示例中的 /bin/bash）。

## What Shells are Available?

## 可用的 Shell 有哪些？

本节列出了 OpenLinux 可用的 shell，以及每个 shell 的一些独特功能以便你入门。这些 shell 都可以运行程序，你可能想探索每个 shell 以了解其工作原理。本节还强调了 shell 之间的一些差异，并指出了重要的配置文件。

所有这些 shell 都支持使用内置的 cd，即 change directory，或更改目录命令来更改目录。有趣的是，ash 和 tcsh shell 没有内置的 pwd，即 print working directory，或打印工作目录命令，必须改用 /bin 目录下的 pwd 命令。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_139_0.png)

> 你在第一次安装 OpenLinux 时选择了在 OpenLinux 会话中使用特定的 shell。如果你想更改此默认 shell，请使用 chsh 命令，后跟你想使用的 shell 的完整路径名。例如，要将默认更改为 bash，请使用 chsh 以及其 -s 选项，如下所示：
> 
> # chsh -s /bin/bash

这些 shell，列在表 6.1 中，具有很多很多功能。请详细阅读每个 shell 的手册页。一些需要查找和探索的功能包括以下内容：

- shell 的内置命令有哪些？
- 如何处理作业控制（或后台进程，本章后面“在后台运行程序”一节中讨论）？
- shell 是否支持命令行编辑？
- shell 是否支持命令行历史？
- 重要的启动或配置文件有哪些？
- 每个 shell 重要的环境变量有哪些？
- 我可以使用哪些命令行提示？
- 支持哪些编程结构？

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_140_0.png)

> OpenLinux 中还包含其他几个 shell：tcsh，一个简单的 shell 和 Tcl 解释器；wish，X11 的窗口 shell；scotty，一个 Tcl 解释器和 shell；以及 rsh，用于通过网络运行命令的远程 shell。有关详细信息，请参阅 tcsh、wish、scotty 和 rsh 手册页。

TABLE 6.1 SHELLS INCLUDED IN THE OPENLINUX DISTRIBUTION

表 6.1 OpenLinux 发行版中包含的 Shell

| Name | Description |
|------|-------------|
| ash | Compact sh-compatible shell |
| bash | Bourne Again Shell (ksh- and sh- compatible) |
| csh | symbolic link to tcsh |
| ksh | pdksh, public domain Korn (ksh- compatible) shell |
| sh | symbolic link to bash |
| tcsh | csh-compatible shell |
| zsh | Z-shell; a csh-, ksh-, and sh- compatible shell |

| 名称 | 描述 |
|------|-------------|
| ash | 紧凑的 sh 兼容 shell |
| bash | Bourne Again Shell（ksh 和 sh 兼容） |
| csh | 指向 tcsh 的符号链接 |
| ksh | pdksh，公共领域 Korn（ksh 兼容）shell |
| sh | 指向 bash 的符号链接 |
| tcsh | csh 兼容 shell |
| zsh | Z-shell；csh、ksh 和 sh 兼容 shell |

## Features of ash

## ash 的功能

ash shell 由 Kenneth Almquist 编写，是 Linux 可用的最小 shell 之一。该 shell 有 24 个不同的内置命令和 10 个不同的命令行选项。ash shell 支持大多数常见的 shell 命令，例如 cd，以及大多数正常的命令行运算符（本章后面“理解 Shell 命令行”一节中讨论）。

这是一个流行的 shell，通常在你以单用户模式启动 OpenLinux 时使用（在 LILO 启动提示符下键入 linux single）或用于救援模式或 Linux 磁盘版。小的可执行文件大小，通常是 bash shell 的十分之一，使 ash 成为小型文件系统的理想 shell。

## Features of the Default Linux Shell—bash

## 默认 Linux Shell 的功能——bash

bash，或 Bourne Again Shell，由 Brian Fox 和 Chet Ramey 编写，是 OpenLinux 最受欢迎的 shell 之一。它具有 48 个内置命令和十几个命令行选项。bash shell 与 sh shell 完全一样，并且在 /bin 目录下有一个名为 sh 的符号链接指向 bash shell。

bash 不仅像 sh shell 一样工作，还具有 csh 和 ksh shell 的功能。由于 bash 使用非常广泛，本小时的示例使用它。稍后你将学习如何使用 bash shell 自定义命令行提示。

bash shell 具有许多功能。你可以使用箭头键滚动浏览之前的命令（历史功能），可以编辑命令行，如果忘记程序名称，甚至可以使用文件名补全向 shell 请求帮助。你只需键入命令的一部分然后按 Tab 键即可。例如，如果你键入 l 并按 Tab 键，你会看到以下内容：

```
# l<TAB>
laser      less      listres   locale     look       lsac
last       lesskey   lkbib     localedef  lookbib    lsattr
lastb      let       lmorph    locate     lpq        lsc
latex      lex       ln        lockfile   lpr        lsl
lbxproxy   lha       lndir     logger     lprm       lynx
ld         lightning loadkeys  login      lptest     lz
ld86       lisa      loadunimap logname    ls
ldd        lispmtopgm local     logout     lsa
```

bash shell 会列出所有以字母 l 开头的已知命令（或当前目录中的任何可执行文件）。如果记不住复杂的命令名称，这非常方便。

bash shell 还具有内置帮助，可列出所有内置命令以及每个命令的帮助。例如：

```
# help
GNU bash, version 1.14.7(1)
Shell commands that are defined internally. Type 'help' to see this list.
Type 'help name' to find out more about the function 'name'.
Use 'info bash' to find out more about the shell in general.
```
