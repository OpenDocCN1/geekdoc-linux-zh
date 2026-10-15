
- 1 `UNIX/Linux` `ln`（链接）命令允许你为文件指定别名；`math` 和 `square` 是同一个文件。每创建一个链接，链接计数就增加 1。

- 2 列表显示所有这些文件都有相同的 `inode` 编号，也就是说它们其实是同一个文件，但可以通过不同名称访问。

# 说明（续）

3 现在，当 `square` 文件被自动加载时，函数 `square` 与它同名，因此会被调用。该文件中定义的其他函数都不能被引用，除非它们也按名称逐一被专门自动加载。

## 12.9 捕获信号

当程序运行时，如果你按下 `Ctrl-C` 或 `Ctrl-\`，程序会在信号到达时立即终止。有时你可能不希望程序在信号到达后立即终止。你可以选择忽略信号并继续运行，或者在实际退出脚本之前执行某种清理操作。`trap` 命令允许你控制程序在接收信号时的行为方式。

信号被定义为一种异步消息，由一个数字组成，可以从一个进程发送到另一个进程，也可以在按下某些键或发生异常事件时由操作系统发送给某个进程。5 `trap` 命令指示 `shell` 在收到信号时终止当前正在执行的命令。如果 `trap` 命令后跟单引号内的命令，这些命令将在收到指定信号时执行。使用 `kill -l` 命令可以获取所有信号及其对应编号的列表。

# 格式

```
trap 'command; command' signal
```

### 示例 12.59

```
trap 'rm tmp.$$; exit 1' 1 2 15
```

# 说明

当信号 1（挂断）、2（中断）或 15（软件终止）中的任何一个到达时，删除所有 `tmp` 文件，然后退出。

如果脚本运行期间有中断到达，`trap` 命令允许你以多种方式处理中断信号。你可以让信号正常执行（默认行为）、忽略该信号，或者创建一个在信号到达时调用的处理函数。关于信号编号及其对应名称的列表，参见表 12.12。6 输入 `kill -l` 可获得表 12.12 所示的输出。

5. Morris I. Bolsky 和 David G. Korn，《新 KornShell 命令与编程语言》（新泽西州恩格尔伍德克利夫斯：Prentice Hall PTR，1995），第 327 页。

6. 关于 UNIX 信号的完整讨论，参见 W. Richard Stevens，《UNIX 环境高级编程》（波士顿：Addison-Wesley Professional，1992）。

# 表 12.12 信号 a b

|  |  |  |

|---|---|---|

| 1) HUP | 12) SYS | 23) POLL |

| 2) INT | 13) PIPE | 24) XCPU |

| 3) QUIT | 14) ALRM | 25) XFSZ |

| 4) ILL | 15) TERM | 26) VTALRM |

| 5) TRAP | 16) URG | 27) PROF |

| 6) IOT | 17) STOP | 28) WINCH |

| 7) EMT | 18) TSTP | 29) LOST |

| 8) FPE | 19) CONT | 30) USR1 |

| 9) KILL | 20) CHLD | 31) USR2 |

| 10) BUS | 21) TTIN |  |

| 11) SEGV | 22) TTOU |  |

a. 该命令的输出可能因操作系统不同而略有差异。

b. 如需 UNIX 信号及其含义的完整列表，请访问 www.cybermagician.co.uk/technet/unixsignals.htm。如需 Linux 信号，请访问 www.comptedoc.org/os/linux/programming/linux_possignals.html。

## 12.9.1 伪信号或假信号

这三个假信号并不是真正的信号，而是由 `shell` 生成的，用于帮助调试程序。`trap` 命令将它们当作真实信号处理，定义方式也相同。伪信号列表参见表 12.13。

# 表 12.13 Korn Shell 伪 trap 信号

| 信号 | 作用 |

|---|---|

| DEBUG | 每执行一条脚本命令后，执行 `trap` 命令 |

| ERR | 如果脚本中的任何命令返回非零退出状态，则执行 `trap` 命令 |

| 0 或 EXIT | 如果 `shell` 退出，则执行 `trap` 命令 |

诸如 `HUP` 和 `INT` 这样的信号名通常以 `SIG` 为前缀，例如 `SIGHUP`、`SIGINT` 等。Korn `shell` 允许你使用信号的符号名，即去掉 `SIG` 前缀后的信号名，也可以使用信号的数值。参见示例 12.60。

## 12.9.2 重置信号

要将信号重置为默认行为，请在 `trap` 命令后跟信号名或信号编号。在函数中设置的 `trap` 仅对函数局部有效；也就是说，在设置它们的函数之外不可见。

# 示例 12.60

```
trap 2 or trap INT
```

# 说明

将信号 2（`SIGINT`）重置为默认动作。该默认动作是在按下中断键（`Ctrl-C`）时终止进程。

## 12.9.3 忽略信号

如果 `trap` 命令后跟一对空引号，则列出的信号将被进程忽略。

# 示例 12.61

```
trap "" 1 2   or   trap "" HUP INT
```

# 说明

信号 1（`SIGHUP`）和信号 2（`SIGINT`）将被 `shell` 进程忽略。

## 12.9.4 列出 trap

要列出所有 `trap` 及其分配的命令，请键入 `trap`。

# 示例 12.62

```
(The Script)
#!/bin/ksh
# Scriptname: trapping
# Script to illustrate the trap command and signals
# Can use the signal numbers or ksh abbreviations seen
# below. Cannot use SIGINT, SIGQUIT, etc.
1  trap 'print "Ctrl-C will not terminate SPROGRAM."' INT
2  trap 'print "Ctrl-\ will not terminate SPROGRAM."' QUIT
3  trap 'print "Ctrl-Z will not terminate SPROGRAM."' TSTP
4  print "Enter any string after the prompt.\nWhen you are ready to exit, type \"stop\"."
5  while true
do
```

# 示例 12.62（续）

```
6    print -n "Go ahead..."
7    read
8    if [[ $REPLY == ${s[top] } ]]
       then
9         break
       fi
10   done
```

（输出）

```
$ trapping
4 Enter any string after the prompt.
When you are ready to exit, type "stop".
6 Go ahead... > this is it^C
1 Ctrl-C will not terminate trapping.
6 Go ahead... > this is it again^Z
3 Ctrl-Z will not terminate trapping.
6 Go ahead... > this is never it^\ 
2 Ctrl-\ will not terminate trapping.
6 Go ahead... > stop
$
```

# 说明

+   1 第一个 `trap` 捕捉 `INT` 信号，即 `Ctrl-C`。如果在程序运行期间按下 `Ctrl-C`，将执行引号中的命令。程序不会中止，而是会打印“`Ctrl-C will not terminate trapping`”，并继续提示用户输入。

+   2 当用户按下 `Ctrl-\`（`QUIT` 信号）时，将执行第二个 `trap` 命令。程序将显示字符串“`Ctrl-\ will not terminate trapping`”，并继续运行。该信号（`SIGQUIT`）默认会终止进程并生成核心转储文件。

+   3 当用户按下 `Ctrl-Z`（`TSTP` 信号）时，将执行第三个 `trap` 命令。程序将显示字符串“`Ctrl-Z will not terminate trapping`”，并继续运行。如果实现了作业控制，该信号通常会使程序挂起到后台。

+   4 程序提示用户输入。

+   5 进入 `while` 循环。

+   6 打印字符串“`Go ahead...`”，程序等待输入（参见第 7 行）。

+   7 `read` 命令将用户输入赋给内建变量 `REPLY`。

+   8 如果 `REPLY` 的值与 `Stop` 或 `stop` 匹配，`break` 命令将使循环退出，程序终止。除非程序被 `kill` 命令杀死，否则输入 `Stop` 或 `stop` 是退出该程序的唯一方式。
