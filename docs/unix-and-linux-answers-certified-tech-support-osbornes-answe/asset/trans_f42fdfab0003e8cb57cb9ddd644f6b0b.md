

## KORN SHELL 中的预定义变量

### 如何重新定义一个预定义变量？

实际上，我们在第 5 章中向你展示了如何做到这一点，当时我们重新定义了 PS1 变量以更改提示符。表 13-4 显示了 Korn shell 设置的参数和变量，表 13-5 显示了 Korn shell 的各个方面使用的参数和变量。

| Parameter | Meaning or Use |
|---|---|
| # | 当前设置的定位参数的数量 |
| - | 启动时传递给 shell 的标志，或由 set 命令传递 |
| ? | 上一个命令以十进制返回的值 |
| $ | 当前 shell 的进程号 |
| _ | 最初是 shell 或脚本的完全限定路径名。自动重新分配给前一个命令的最后一个参数 |
| ! | 上一个后台命令的进程号 |
| ERRNO | 最后一次失败的系统调用设置的 errno 的值 |
| LINENO | 当前正在执行的脚本的行号 |
| OLDPWD | 由 cd 设置的上一个工作目录 |
| OPTARG | getopts 命令返回的最后一个选项 |
| OPTIND | getopts 命令返回的最后一个选项的索引（位置） |
| PPID | shell 父进程的进程 ID |
| PWD | 当前工作目录 |
| RANDOM | 一个介于 0 和 32767 之间的伪随机整数，每次引用该参数时都会更改，使用前一个值作为种子 |
| REPLY | 由 select 语句设置，或由不带参数的 read 设置 |
| SECONDS | shell 启动以来的秒数 |

表 13-4 Korn Shell 设置的参数

| Parameter | Meaning or Use |
|---|---|
| CDPATH | cd 命令的搜索路径 |
| COLUMNS | 当前编辑窗口的列数 |
| EDITOR | 用于命令行编辑的默认编辑器 |
| ENV | 调用 shell 时要执行的脚本的路径名 |
| FCEDIT | fc 命令的默认编辑器 |
| HISTFILE | 命令历史文件的路径名 |
| HISTSIZE | 历史文件中保留的命令数。默认值是 128 |
| HOME | 主目录。cd 命令的默认目标 |
| IFS | 内部字段分隔符，通常为空格、制表符和换行符 |
| LINES | 当前显示窗口的行数 |
| MAIL | 用户的默认邮件文件 |
| MAILCHECK | 检查 $MAIL 或 $MAILPATH 文件中是否有新邮件到达的频率。默认为 10 分钟（600 秒） |
| MAILPATH | 可能的邮件目标列表，以冒号分隔 |
| PATH | 命令执行搜索路径 |
| PS1 | 主命令行提示符（默认为 "$ "） |
| PS2 | 次要命令行提示符（默认为 "> "） |
| PS3 | select 循环内使用的提示符字符串（默认为 "#? "） |
| PS4 | 执行跟踪提示符（默认为 "+ "） |
| SHELL | shell 的路径名 |
| TMOUT | 如果设置为 >0，则在 PS1 提示符下未输入命令时 shell 自动终止的时间 |
| VISUAL | 默认命令行编辑器。覆盖 EDITOR |

表 13-5 Korn Shell 变量和参数

## 流程控制

### Korn shell 为我提供了哪些流程控制结构？

如果你打算用任何编程语言或环境完成很多工作，你必须有某种形式的流程控制。Korn shell 也不例外。它提供了以下结构：

- if/then/else
- for
- while
- until
- case
- select

这是一个足够的流程控制语句选择，但不幸的是语法并不完全用户友好。你可能会发现需要一定的试错才能全部做对。

### 在 Korn shell 中使用 if/then/else 语句有什么棘手之处？

这些结构是程序中最基本、最常用的流程控制形式。首先你询问某事是否属实，如果是，你就做某事。如果不是，你可能会做别的事，或者什么都不做。基本语法是

```
if condition
then
statements
[elif condition2
then statements]
[else
statements]
fi
```

每个 if 都由对应的 fi 关闭，并且可以在其中包含 else 和 elif（else if）测试和语句。但使整个结构工作的关键是构造的条件部分。在这里，Korn shell 赋予了我们一些能力。条件可以是典型的布尔类型的简单测试，例如这些：

```
if [[ $DISPLAY = "rc1:0.0" ]]
if [[ $n == 1 ]]
if [[ $y >= 17 ]]
```

