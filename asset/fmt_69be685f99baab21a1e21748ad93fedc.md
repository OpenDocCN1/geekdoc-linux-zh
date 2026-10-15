
### 表 B.2 SuSE Linux 微型教程

| 名称 | 配置三键串口鼠标 |
| Windows-Modem-Sharing | 通过 TCP/IP 共享 Linux 调制解调器 |
| WordPerfect | 在 Linux 上运行 WordPerfect |
| X-Big-Cursor | 使用 X Window 系统创建大光标 |
| XFree86-XInside | 将 XFree86 modeline 转换为 XInside/XiGraphics modeline |
| Xtermm-Title | 更改 xtermm 的标题 |
| ZIP-Drive | 在 Linux 下设置和使用 Iomega Zip 驱动 (PPA) |
| ZIP-Install | 在 Zip 磁盘上安装 Linux |

# 常用 Linux 命令与工具

# C

# 附录

第五部分

本附录并非取代帮助手册 (`man pages`)，也没有详细列出每个命令的所有选项。你可以在这些程序的帮助手册中找到所需的大部分信息或者

许多描述也带有示例。如果这些示例并非显而易见，则会提供解释。这并不是一个详尽的列表——SuSE Linux 带有许多更多命令——但这些是最常用的，你会发现自己会反复使用它们。

为了保持简单，命令按字母顺序列出；然而，以下是 10 个最常用的命令列表，它们通常被认为是使用 SuSE Linux 控制台或命令行时必不可少的：

- `cat`
- `cd`
- `cp`
- `find`
- `grep`
- `ls`
- `less`
- `rm`
- `pico`
- `mv`

通过使用这 10 个命令，你将能够维护你的 SuSE Linux 系统。

# 通用指南

随 SuSE Linux 分发的许多程序都源自 UNIX 世界的对应程序，并继承了其简洁、有时晦涩的命名风格。通常情况下，修改已存在的内容会引导你使用一个名称以 `ch` 开头的命令。如果你想完全执行某项操作，命令通常以 `rm` 开头。例如，要创建一个新目录，使用 `mkdir`；要删除一个目录，使用 `rdir`。

# 列表

本附录列出的命令是 SuSE Linux 中一些最常用的。对于这些每个命令，帮助手册都可以提供额外信息以及示例。在命令看起来含义模糊的情况下，会提供示例。以下示例在 `bash` 或 `pdksh` 中有效。在 `tsh` 中的等效命令是 `source`。以下示例执行该命令：

在任何其他命令后的 `&` 运算符告诉计算机在后台运行该命令。通过将作业放在后台，用户随后可以继续使用该 shell 处理其他命令。如果命令在后台运行，用户可以继续使用该 shell 处理其他命令。

任何其他命令后的 `&` 运算符告诉计算机在后台运行该命令。通过将作业放在后台，用户随后可以继续使用该 shell 处理其他命令。如果命令在后台运行，用户可以继续使用该 shell 处理其他命令。

`|` (`管道`) 运算符在第一个命令执行失败时执行第二个命令。例如，将命令的输出输出到文件。这种 shell 运算符输入。。。，，，，，， shell 文件：

`|` (`管道`) 运算符在第一个命令执行失败时执行第二个命令。例如，将命令的输出输出到文件：

`>` (`标准输出`) 运算符将命令的输出重定向到文件。例如，将命令的输出输出到文件。

`>` (`标准输出`) 运算符将命令的输出重定向到文件。例如，将命令的输出输出到文件。

`>>` (`追加`) 运算符会将命令的输出追加到文件的末尾。例如，将命令的输出追加到文件。

`>>` (`追加`) 运算符会将命令的输出追加到文件的末尾。例如，将命令的输出追加到文件。

`<` (`标准输入`) 运算符将命令的输入重定向到文件。例如，从文件中读取输入。

`<` (`标准输入`) 运算符将命令的输入重定向到文件。例如，从文件中读取输入。

`<<` (`在此处文档`) 运算符告诉 shell 在遇到结束符之前读取输入。例如，使用 shell：

`<<` (`在此处文档`) 运算符告诉 shell 在遇到结束符之前读取输入。例如，使用 shell：

`<<` (`在此处文档`) 运算符告诉 shell 在遇到结束符之前读取输入。例如，使用 shell：

`<<` (`在此处文档`) 运算符告诉 shell 在遇到结束符之前读取输入。例如，使用 shell：

# a2ps

`a2ps` 命令将多页 ASCII 格式化为单页，节省金钱并减少打印机损耗。当你安装了打印机后，每页打印两个页面：

# adduser

`adduser` 命令用于 root（或具有权限的人）创建新用户。`adduser` 命令后面跟着要创建的账户名称：

# agetty

设置登录参数，例如终端类型、速度和协议。你可以配置 `/etc/itab` 文件使用 `agetty` 监控连接。该程序可以在登录时显示消息或运行程序。

# alias

`alias` 命令用于为命令创建别名或替代名称。通常，这些别名是实际命令的缩写。在示例中，用户（可能是 DOS 用户）为目录列表添加了 `dir` 的别名：

输入 `alias` 本身会给出你所有的别名。例如，SuSE Linux 的默认输出如下：

```
$ alias
alias+=pushd
alias='popd'
alias ..='cd ..'
alias ...='cd ../.'
alias dir='ls -l'
alias dos2unix='recode ibmpc:lat1'
alias ls='ls -aF'
alias la='ls -la'
alias ll='ls -l'
alias ls='ls $LS_OPTIONS'
alias ls-l1='ls -1'
alias md='mkdir -p'
alias o='less'
alias rd='rmdir'
alias rehash='hash -r'
alias unix2dos='recode lat1:ibmpc'
alias unzip='unzip -L'
alias which='type -p'
```

# apropos <parameter>

`apropos` 命令字面意思是“适当的”或“关于”。当后接参数时，`apropos` 搜索包含该参数的帮助手册，对所有帮助手册进行关键词搜索。等效命令是 `man -k <parameter>`。

# ash

`ash` 是一个简单的 shell，其功能类似于 `sh` 或 Bourne Again SHell。`ash` shell 通过符号链接 `bsh` 运行，该链接位于 `/bin` 目录下。

# at

`at` 用于在指定的时间运行程序。你可以使用 `at` 命令在命令行或文件中指定一个时间，来调度任务或作业运行。

# atq

使用 `atq` 列出等待作业队列。`atq` 命令会打印 `at` 命令的等待作业或事件的列表（通常位于 `/var/spool/at` 目录下）。

# atrm

使用 `atrm` 删除指定的作业。`atrm` 命令用于移除队列中的一个或多个作业。用户或 root 操作员可以使用 `atrm` 命令来删除待处理的事件（停止 `at` 命令的运行）。

# bash

`bash` 是 GNU Bourne Again SHell。作为 SuSE Linux 的默认 shell，`bash` 具有许多功能，例如命令行编辑、内置帮助和命令历史。`bash` shell 也可以通过 `/bin` 目录下的符号链接 `sh` 运行。

# batch

`batch` 命令根据平均负载运行作业。该程序用于在计算机达到特定的平均负载时运行事件，该负载是由 `/proc` 目录下 `loadavg` 文件中的实时值决定的。`batch` 还有其他选项；详情请阅读命令手册页。

# bc

`bc` 是一种计算器语言，是一个用于构建计算器程序和工具的解释器和语言。你可以使用这个解释器和语言来编写自定义计算器。

# bg

`bg` 命令用于强制让挂起的进程在后台运行。例如，假设你在前台启动了一个命令（没有在命令后使用 `&`），并意识到它需要花费一段时间，但你仍然需要你的 shell。你可以使用 `Ctrl+Z` 将当前进程挂起。然后，你可以让它保持挂起状态——就像你拨打了电话公司一样——或者输入 `bg` 将该进程放入后台，释放你的 shell 以允许你执行其他命令（可以使用 `fg` 将命令带回前台）。

# bind

`bind` 用于 `ksh`，允许用户更改键组合的行为以用于命令行编辑。许多人会将上、左、右方向键进行绑定，以便它们的工作方式与 Bourne Again Shell (`bash`) 相同。该命令使用的语法为：

```
bind <key sequence> <command>
```

以下是 `bind` 命令的示例，用于创建向上向下滚动历史列表以及在命令行向左向右移动的绑定：

```
bind '[[prefix-2
bind 'XA=up-history
bind 'XB=down-history
bind 'XC=forward-char
bind 'XD=backward-char
```

![](img/cbac72550c7126a22162e94d91a0c360_1032_0.png)

# cat
