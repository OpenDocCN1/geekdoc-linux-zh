
如有必要，来自 `help` 命令的在线帮助包含大量详细信息。

某些外部程序可能与 `bash` 内置命令具有相同的名称。如果你想运行任何此类外部程序，必须明确指定该程序的完整路径名。否则，`bash` 将执行同名内置命令。

![](img/792720823146d68f19fd50c99ebfce4b_764_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_764_1.png)

# 740 探索 Shell 脚本基础

## bash Shell 内置命令概述

| 此功能 | 执行以下操作 |
| :--- | :--- |
| `.` `filename` `[arguments]` | 使用可选参数从指定文件中读取并执行命令。（工作方式与 `source` 命令相同。） |
| `:` `[arguments]` | 扩展参数但不处理它们 |
| `[` `expr` `]` | 计算表达式 `expr`，如果 `expr` 为真，则返回零状态 |
| `alias` `[name[=value] . . . ]` | 定义一个别名 |
| `bg` `[job]` | 将指定作业放到后台。如果未指定作业，则将当前正在执行的命令放到后台。 |
| `bind` `[-m keymap] [-lvd] [-q name]` | 将按键序列绑定到宏 |
| `break` `[n]` | 退出 `for`、`while` 或 `until` 循环。如果指定了 `n`，则退出第 `n` 层包围的循环。 |
| `builtin` `builtin_command` `[arguments]` | 执行 shell 内置命令 |
| `cd` `[dir]` | 将当前目录更改为 `dir` |
| `command` `[-pVv]` `cmd` `[arg . . .]` | 使用指定参数运行命令 `cmd`（忽略任何名为 `cmd` 的 shell 函数） |
| `continue` `[n]` | 开始 `for`、`while` 或 `until` 循环的下一次迭代。如果指定了 `n`，则开始第 `n` 层包围循环的下一次迭代。 |
| `declare` `[[-frx] [name[=value]]]` | 声明具有指定名称的变量，并可选地为其分配一个值。 |
| `dirs` `[-l]` `[+/-n]` | 显示当前记住的目录列表 |
| `echo` `[nE]` `[arg . . .]` | 在标准输出中显示参数 |
| `enable` `[-n]` `[-all]` `[name . . .]` | 启用或禁用指定的内置命令 |
| `eval` `[arg . . .]` | 将参数连接起来并作为命令执行 |
| `exec` `[command [arguments]]` | 用运行指定命令的新进程替换当前 shell 实例 |
| `exit` `[n]` | 以状态码 `n` 退出 shell |
| `export` `[-nf]` `[name[=word]] . . .` | 定义指定的环境变量并将其导出到未来进程 |
| `fc` `-s` `[pat=rep]` `[cmd]` | 在将模式 `pat` 替换为 `rep` 后重新执行命令 |
| `fg` `[jobspec]` | 将指定作业放到前台。如果未指定作业，则将最近的作业放到前台。 |
| `getopts` `optstring name [args]` | 获取可选参数（在 shell 脚本中用于从命令行提取参数时调用） |
| `hash` `[-r]` `[name]` | 记住指定命令的完整路径名 |
| `help` `[cmd...]` | 显示指定内置命令的帮助信息 |
| `history` `[n]` | 显示过去的命令，或者如果你指定了数字 `n`，则显示过去 `n` 条命令 |
| `jobs` `[-lnp]` `[ jobspec ... ]` | 列出当前活动的作业 |
| `kill` `[-s sigspec \| -sigspec]` `[pid \| jobspec]` | 终止一个进程 |
| `let` `arg (arg...)` | 评估每个参数，如果最后一个参数为 0，则返回 1 |
| `local` `[name=[value] ...]` | 创建具有指定名称和值的局部变量（用于 shell 函数中） |
| `logout` | 退出登录 shell |
| `popd` `[+/ -n]` | 从目录栈中移除条目 |
| `pushd` `[dir]` | 将指定目录添加到目录栈的顶部 |
| `pwd` | 打印当前工作目录的完整路径名 |
| `read` `[-r]` `[name...]` | 从标准输入读取一行并解析它 |
| `readonly` `[-f]` `[name...]` | 将指定变量标记为只读，以便之后不能更改这些变量 |
| `return` `[n]` | 以返回值 `n` 退出 shell 函数 |
| `set` `[ -abefhkmnptuvxLDCHP]` `[ -o option]` `[arg...]` | 设置各种标志 |
| `shift` `[n]` | 使第 `n+1` 个参数变为 `$1`，第 `n+2` 个参数变为 `$2`，等等 |
| `source` `filename (arguments)` | 从文件中读取并执行命令 |
| `suspend` `[-f]` | 停止执行，直到接收到 SIGCONT 信号 |
| `test` `expr` | 计算表达式 `expr`，如果 `expr` 为真，则返回零 |
| `times` | 打印从 shell 运行的进程的累积用户时间和系统时间 |
| `trap` `[-l]` `[cmd]` `[sigspec]` | 当接收到信号 `sigspec` 时执行 `cmd` |
| `type` `[-all]` `[-type]` `[-path]` `name` `[name ...]` | 指示 shell 如何解释每个名称 |
| `ulimit` `[-HSacdfmstpvuv [limit]]` | 控制 shell 可用的资源 |
| `umask` `[-S]` `[mode]` | 设置文件创建掩码——文件的默认权限 |
| `unalias` `[-a]` `[name ...]` | 取消定义指定的别名 |
| `unset` `[-fv]` `[name ...]` | 移除指定变量的定义 |
| `wait` `[n]` | 等待指定进程终止 |

表 3-1

# 第 4 章：Perl 编程

## 本章内容

- 编写你的第一个 Perl 程序
- 概览 Perl
- 理解 Perl 包和模块
- 在 Perl 中使用对象

在编写脚本方面，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动化例行的系统管理任务，例如查找可以归档和删除以释放磁盘空间的旧文件。

Perl 是一种脚本语言，这意味着你不需要编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，解释器执行 Perl 脚本。这种能力使得编写和测试 Perl 脚本变得容易，因为你不需要经历典型的编辑-编译-链接循环来编写 Perl 程序。

除了编程简便性之外，Perl 流行的另一个原因是 Perl 是免费分发的，并且可用于各种各样的操作系统，包括 Linux 以及许多其他系统，如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Mac OS X。

在本章中，我将向你介绍 Perl 脚本编写。

## 理解 Perl

官方上，Perl 代表 *实用提取报告语言*（*Practical Extraction Report Language*），但 Perl 的创建者 Larry Wall 说，人们经常将 Perl 称为 *病态的电色垃圾列表器*（*Pathologically Electic Rubbish Lister*）。正如这些名称所示，Perl 最初被设计用于从文本文件中提取信息并生成报告。

Perl 诞生于 1986 年，最初是 Larry Wall 创建的一种系统管理工具。随着时间推移，Perl 通过不断累积许多新的特性和功能而成长。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过以指定格式添加新模块来扩展 Perl。

忠实于其作为系统管理工具的起源，Perl 多年来一直深受 UNIX 系统管理员的欢迎。最近，当万维网（或简称为 Web）变得流行并且需要通用网关接口（CGI）程序时，对于已经熟悉该语言的人来说，Perl 成为了自然的选择。Perl 近期流行度的激增主要归因于 Perl 在编写 Web CGI 程序中的应用。当然，随着人们更多地关注 Perl，他们发现 Perl 的用途远不止于 CGI 编程。进而，这使得 Perl 在用户中更加流行。

Perl 在多种计算机系统上可用，因为像 Linux 操作系统一样，Perl 可以自由分发。

如果你熟悉 shell 编程或 C 编程语言，你可以很快掌握 Perl。如果你从未编写过程序，精通 Perl 可能需要一些时间。我鼓励你从 Perl 特性的小子集开始，忽略那些你立即无法理解的内容。然后，慢慢将 Perl 特性添加到你的技能库中。

## 确定你是否有 Perl

在你继续 Perl 教程之前，检查你的 Linux 系统是否安装了 `perl` 程序。输入以下命令：

```
which perl
```
