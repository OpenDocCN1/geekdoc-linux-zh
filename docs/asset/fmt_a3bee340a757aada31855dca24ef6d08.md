
`obase=16` 设置输出进制为十六进制；`ibase=8` 设置输入进制为八进制。`400` 是八进制的，`77` 是八进制的，`3f` 是八进制的。你输入 `10*3` 等于 `18`。然而，输出进制是十六进制，得到 `18`。

# 24小时自学学会 Shell 编程

| 第18小时：杂项工具 |
|---|---|
| `eval` 命令 | `expr` 命令 |
| `type` 命令 | `bc` 命令 |
| `sleep` 命令 | remsh/rsh/rcmd/remote（远程 Shell） |
| `find` 命令 | 总结 |
| xargs | 术语 |

© Copyright Macmillan Publishing. 版权所有。

# 24小时自学学会 Shell

## remsh/rcmd/remote（远程 Shell）

如果你通过网络连接了多个 UNIX 系统，可以调用远程 Shell 在远程系统上运行命令并将其输出返回到屏幕：

`remsh who`

这显示了谁登录了远程系统。基本语法是：

```
remsh remote-sys unix-command
```

`remote-sys` 是运行给定命令的远程系统名称。你可以将文本传递给 `remsh`，将其传递给远程系统上的 `unix-command`。远程系统 `unix-command` 的任何标准输出将传递到你系统的标准输出，根据需要可以重定向。不同类型的 UNIX 系统对此命令有不同的名称，包括 `remsh`, `rsh`, `rcmd`, `remote`。

检查你系统上的页面以查看哪个命令是正确的。为了避免与受限 Shell 命令 `rsh` 混淆，有时通过 `/usr/lib/rsh` 调用它。

使用远程 Shell 需要设置 `/etc/hosts.equiv`，这表示两个系统之间的信任关系。最简单的信任设置是将每个系统名称放在对方系统的 `hosts.equiv` 中。通常两个系统中都会添加相同的用户账户。这样，在一个系统上由用户运行的远程命令在另一个系统中具有相同的权限。要使用此功能，`/.hosts` 必须包含另一个系统名称。

这是一个更复杂的示例，允许我们将整个整个目录复制到远程系统：

```
cd /sourcedir

find . -print | cpio -ocva |\nremsh remote_sys { cd /destdir\; cpio -icdum \ }
```

`find` 命令将文件列表传递给 `cpio`，后者将其复制到标准输出。这些内容通过远程 Shell 连接到远程系统，文件在其中被恢复到目标的目标目录。注意，许多特殊字符必须转义——即在前面加反斜杠——这样它们会在远程系统上解析，而不是本地系统。

# 24小时自学 Shell 编程

目录索引

第 18 小时：杂项工具 上一章 下一章

### 本章章节：

| eval 命令 | expr 命令 |
| :--- | :--- |
| : 命令 | bc 命令 |
| type 命令 | remsh/rcmd/remote (远程外壳) |
| sleep 命令 | 总结 |
| find 命令 | 问题 |
| xargs | 术语 |

### 总结

在本章中，你查看了若干种杂项工具：

- `eval`
- `:`
- `type`
- `sleep`
- `find`
- `xargs`
- `expr`
- `bc`
- `remsh/rsh/rcmd/remote`

本章的大部分内容花在了 `find` 命令的基础基础知识上。仔细查阅 `find` 的帮助页（`man page`），你可以看到其他我没有涵盖的、对脚本非常有用的 `find` 选项。

### 问题

1. 你正准备运行一个名为 `process2` 的自定义命令，但你首先想确定该命令所在的位置。给出一个实现此功能的 UNIX 命令。

2. 你如何确定 `/data` 下所有包含名为 `process2` 文件的目录，并允许任何可能的前缀或后缀（例如，你想寻找类似 `process2-doc` 的名称）。

3. 你如何将变量 `PRICE` 中的数值增加到当前值的 3.5 倍？允许小数点后保留两位。

### 术语

`no-op`（无操作命令）一种什么都不执行的命令，因此可以在语法要求命令的地方作为虚拟命令或占位符使用。

`built-in`（内置命令）代码属于 shell 的一部分，而不是存在于独立磁盘文件中的实用程序（后者在执行之前必须读取到内存中）。

`reserved word`（保留字）一种未引号的单词，用于组合命令或选择性执行命令，例如：`if`、`then`、`else`、`elif`、`fi`、`case`、`esac`、`for`、`while`、`until`、`do` 或 `done`。

`remainder function`（取余函数）除法运算的结果，即不能整除时。

`inode`（索引节点）文件系统中的一个表项，包含所有者、权限、修改日期和访问日期等信息。

# 24 小时自学 Shell 编程

第 18 小时：杂项工具 | 上一章 | 下一章

### 本章章节：
（见上方目录索引中的表格）

### 总结

在本章中，你查看了若干种杂项工具：

- `eval`
- `:`
- `type`
- `sleep`
- `find`
- `xargs`
- `expr`
- `bc`
- `remsh/rsh/rcmd/remote`

本章的大部分内容花在了 `find` 命令的基础知识上。仔细查阅 `find` 的帮助页（`man page`），你可以看到其他我没有涵盖的、对脚本非常有用的 `find` 选项。

### 问题

1. 你正准备运行一个名为 `process2` 的自定义命令，但你首先想确定该命令所在的位置。给出一个实现此功能的 UNIX 命令。

2. 你如何确定 `/data` 下所有包含名为 `process2` 文件的目录，并允许任何可能的前缀或后缀（例如，你想寻找类似 `process2-doc` 的名称）。

3. 你如何将变量 `PRICE` 中的数值增加到当前值的 3.5 倍？允许小数点后保留两位。

### 术语

`no-op`（无操作命令）一种什么都不执行的命令，因此可以在语法要求命令的地方作为虚拟命令或占位符使用。

`built-in`（内置命令）代码属于 shell 的一部分，而不是存在于独立磁盘文件中的实用程序（后者在执行之前必须读取到内存中）。

`reserved word`（保留字）一种未引号的单词，用于组合命令或选择性执行命令，例如：`if`、`then`、`else`、`elif`、`fi`、`case`、`esac`、`for`、`while`、`until`、`do` 或 `done`。

`remainder function`（取余函数）除法运算的结果，即不能整除时。

`inode`（索引节点）文件系统中的一个表项，包含所有者、权限、修改日期和访问日期等信息。

# 24 小时自学 Shell 编程

第 18 小时：杂项工具 | 上一章 | 下一章

### 本章章节：
（见上方目录索引中的表格）

## 19：处理信号

除了表 19.1 中列出的信号外，你偶尔可能会看到对 0 的引用，这更多是 shell 的约定而不是真实的信号。当脚本通过 0 退出时，shell 会向自己发送一个信号。

对 Shell 重要的信号

| 名称 | 数值 | 描述 |
| :--- | :--- | :--- |
| SIGHUP | 1 | 挂断 (Hang up) |
| SIGINT | 2 | 键盘中断 (Interrupt) |
| SIGQUIT | 3 | 键盘退出 (Quit) |
| SIGKILL | 9 | 杀死信号 |
| SIGALRM | 14 | 闹钟 |
| SIGTERM | 15 | 终止 |

### 获取信号列表

系统理解的所有信号都列在 C 头文件 `signal.h` 中。该文件在不同系统中有所不同。一些常见的位置包括：

- Solaris 和 HPUX: `/usr/include/sys/signal.h`
- Linux: `/usr/include/asm/signal.h`

系统理解信号列表的另一种方法是使用 `kill` 命令的 `-1` 选项。例如，在 Solaris 系统上的输出如下：

```
kill -1

1) SIGHUP 2) SIGINT 3) SIGABRT 4) SIGILL

5) SIGTRAP 6) SIGBUS 7) SIGEMT 8) SIGFPE

9) SIGKILL 10) SIGIO 11) SIGSEGV 12) SIGSYS

13) SIGPIPE 14) SIGALRM 15) SIGTERM 16) SIGUSR1

17) SIGUSR2 18) SIGCHLD 19) SIGPWR 20) SIGWINCH

21) SIGURG 22) SIGIO 23) SIGSTOP 24) SIGTSTP

25) SIGCONT 26) SIGTTIN 27) SIGTTOU 28) SIGVALRM
```
