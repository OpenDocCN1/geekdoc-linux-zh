
高级练习 733

- 11. 修改 `foreach_1` 程序（第 721 页），使其接受要 `exec` 的命令作为参数。
- 12. 重写 `while_1` 程序（第 722 页），使其运行更快。使用内置的 `time` 来验证执行时间的改进。
- 13. 编写你自己的 `find` 版本并命名为 `myfind`，将输出写入到文件 `findout`，且不包含错误信息的干扰（例如当你没有权限搜索某个目录时）。`myfind` 命令应该接受与 `find` 相同的选项和参数。你能想出一种 `myfind` 不按预期工作的情况吗？
- 14. 当为 `foreach_1` 脚本（第 721 页）提供 20 个或更少的参数时，为什么 `tomany` 之后的命令没有被执行？（为什么没有 `exit` 命令？）

# 本章内容

- Z Shell 基础 736
- 变量 741
- 内置命令 767
- 命令行编辑 791
- Shell 程序 808
- Z Shell 选项 824

## Z Shell 与高级 Shell 编程

Z Shell (zsh) 结合了 Bourne Again、TC 和 C Shell 的许多特性。此外，zsh 还整合了许多新功能。由于 zsh 提供的功能和配置选项非常多，本章重点关注最常用的部分，并跳过了一些较为晦涩的内容。本章还解释了如何自定义 zsh 以满足你的需求。如果你以前用过 `csh` 或 `tsh`，可以配置 zsh 使其行为与 `csh` 和 `tsh` 相同。如果你用过 Korn Shell，设置 zsh 工作得像 ksh 一样可能对你有帮助。

本章基于前面章节关于 Shell 和 Shell 编程的内容（假设你阅读了第 12 至第 14 章）。

在介绍之后，本章开始讨论变量和 Shell 内置命令。接下来讨论命令行编辑，随后是一个关于命令处理的章节，描述了 Shell 在处理命令行时所采取的各种步骤。然后，关于 Shell 编程的详细章节讨论了递归，并引导你构建两个较长的 Shell 程序。本章以 Z Shell 选项列表结束。

## Red Hat 未随系统自动安装 Z Shell

完整的 Red Hat 磁盘集包含了 `zsh` rpm 文件（第 928 页）。你也可以从 Red Hat 网站或 www.rpmfind.net 下载。

## Z Shell、Korn Shell 和 Pd-ksh

完整的 Korn Shell 现在已作为商业产品供 GNU/Linux 使用，Korn Shell 的大多数用户依赖于其领域实现 Pd-ksh（用于公有领域 ksh；程序名称为 `pdksh`）。尽管 `pdksh` (ww.cs.mun.ca/~michael/pdksh) 提供了 Korn Shell 的大部分基本功能，但它缺少一些让 Korn Shell 成为编写 Shell 脚本强大语言的高级功能。这些功能中的大部分（以及部分）在 zsh 中。事实上，如果将 Z Shell 链接到文件名 `/bin/ksh`，运行 `/bin/ksh` 将导致 Z Shell 以一个非常类似于 Korn Shell 的默认配置启动。

## Z Shell 基础

如果你想将 Z Shell 作为你的登录 shell，请运行 `csh` 并如“进入和退出 TC Shell”（第 683 页）所述指定路径 `/bin/zsh`。或者，超级用户可以设置 `/etc/passwd` 文件来实现相同目的。

Z Shell 的基本行为模仿了其他 shell：你输入一个命名为可执行程序或脚本的命令，可选地带有由命令解释的参数。你可以通过按下 `RETURN` 键来修正错误。在第 37 页，你还可以使用 Z Shell 强大的命令行编辑（第 791 页）和历史编辑（第 795 页）来创建和修改命令行。

与 `bash` 和 `tsh` 一样，zsh 在执行命令之前会评估变量、搜索别名和函数、扩展模糊的文件引用并处理重定向。理解这些步骤执行的精确顺序是重要的，因为它们会影响命令行的含义。在详细描述命令行处理中的步骤之前，本章先描述了 shell 的其他方面。请参阅第 797 页的“处理命令”。

## 运行脚本

要执行 Z Shell 脚本，使用脚本名称作为 `zsh` 的参数：

```
zsh % zsh script_name
```

上述命令无论你正在使用哪种 shell 都会调用 `zsh`。如果你对包含脚本的文件具有执行权限，你可以使用文件名作为命令：

```
zsh % script_name
```

当脚本的第一行以 `#!/bin/zsh` 开头时， Z Shell 会运行该脚本，无论你从哪个 shell 调用该脚本（第 564 页）：

## 启动文件

Z Shell 使用了许多与 `bash` 相同的环境变量，并增加了其他几个。你可以设置这些变量，以及建立这些变量的命令，在 Z Shell 启动文件（表 15-1）中设置这些变量（除非使用 `-f`）。

| 启动文件 | |
| :--- | :--- |
| `/etc/zsh` | 超级用户创建，用于建立 zsh 的默认特性。它是启动时第一个被读取的文件。 |
| `~/zenv` | 你在家目录中创建，用于设置覆盖 `/etc/zsh` 的变量。它是第二个被读取的文件。 |
| `/etc/zprofile` | 超级用户创建，用于建立 login shell 的默认特性。在 login shell 启动（或带 `-l` 参数调用 zsh）时读取。 |
| `~/zprofile` | 你在家目录中创建，用于设置覆盖 `/etc/zprofile` 的变量。在 login shell 启动（或带 `-l` 参数调用 zsh）时读取。 |
| `/etc/zshrc` | 超级用户创建，用于建立交互式 shell 的默认特性。仅交互式 shell 读取。 |
| `~/.zshrc` | 你在家目录中创建，用于设置覆盖 `/etc/zshrc` 的变量。仅交互式 shell 读取。 |

由于 `.zenv` 是唯一用于 zsh 初始化的文件（除非使用 `-f`），你可以将所有的变量初始化和选项设置放在此文件中。如何使用其他启动文件取决于你如何使用 zsh：调用 zsh 是登录 shell 还是交互式 shell？示例的 `.zenv`、`.profile` 和 `.zrc` 文件如下。这些文件中的某些命令在本章后面将不会被介绍。在任何启动文件中，你希望能够处理的函数：

```
% cat .zenv
MAIL=/usr/spool/mail/${LOGIN}?
MANPATH=/usr/man:/usr/X11R6:/usr/local/man
PATH=$HOME/bin:/usr/local/bin:/usr/bin/X11:/usr/bin:/bin:
export MAIL MANPATH PATH
umask 002
% cat .profile
FCEDIT=/usr/bin/vim
PS1='$ '
PS2='>
HISTSIZE=256
stty kill '^u' erase '^h' intr '^Ac' quit '^\'
export FCEDIT PS1 PS2 HISTSIZE
```
