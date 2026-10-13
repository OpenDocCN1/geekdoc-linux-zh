
```
09:21:16.720000 reboot.nitec.com> brat.nitec.com: icmp:
echo request
09:21:16.720000 brat.nitec.com> reboot.nitec.com: icmp:
echo reply
09:21:17.730000 reboot.nitec.com> brat.nitec.com: icmp:
echo request
09:21:17.730000 brat.nitec.com> reboot.nitec.com: icmp:
echo reply
```

假设你在使用 FTP 服务器连接时遇到问题。你可以在局域网网关系统上使用 tcpdump 来查看发生了什么。例如，

```
tcpdump port ftp or ftp-data
```

显示源自你的网络并到达你的网络的与 FTP 相关的报文。

这使你能够在低级别调试网络问题。如果你在两台主机之间使用服务时遇到问题，请使用 tcpdump 来识别问题。

## traceroute

Syntax:

```
traceroute host or IP address
```

该程序可帮助你定位网络路由问题。traceroute 通过诱骗主机之间的网关对 ICMP TIME_EXCEEDED 请求做出响应来显示两台主机之间的路由。以下是从我的本地系统到 blackhole.nitec.com 主机的 traceroute 示例：

```
traceroute to blackhole.nitec.com (209.63.178.15), 30
hops max, 40 byte packets
1 router (206.171.50.49) 4.137 ms 3.995 ms 4.738 ms
2 PM3-001.v1.NET (206.171.48.10) 32.683 ms 33.295 ms
33.255 ms
3 HQ-CS001.v1.NET (206.171.48.1) 42.263 ms 44.237 ms
36.784 ms

4 ix.pxbi.net (206.13.15.97) 106.785 ms 63.585 ms
101.277 ms

5 ix.pxbi.net (206.13.31.8) 86.283 ms 64.246 ms 69.749 ms

6 ca.us.ixbm.net (165.87.22.10) 71.415 ms 72.319 ms
85.183 ms

7 mae.exli.net (198.32.136.128) 101.863 ms 80.257 ms
67.323 ms

8 y.exli.net (207.173.113.146) 71.323 ms 104.685 ms
110.935 ms

9 z.exli.net (207.173.113.217) 69.964 ms 137.858 ms
85.326 ms

10 zl.exli.net (207.173.112.251) 81.257 ms 107.575 ms
78.453 ms

11 209.210.249.50 (209.210.249.50) 90.701 ms 91.116 ms
109.491 ms

12 209.63.178.15 (209.63.178.15) 83.052 ms 76.604 ms
85.406 ms
```

每行代表一次跳数；跳数越多，路由通常越差。换句话说，如果源和目标之间只有少数几个网关，那么这两台主机之间的报文很可能会以相当快的速度传输。然而，这并非总是如此，因为单个缓慢的网关可能会破坏交付时间。使用 traceroute，你可以定位你的数据包的去向以及它们可能卡住的地方。定位问题点后，请联系相关负责人解决路由问题。

## Process Management Commands

本节讨论的命令用于管理进程——系统中的正在运行的程序。

### bg

Syntax:

```
bg
```

这是一个内置的 shell 命令，常见于流行的 shell 中。bg 命令允许你将挂起的进程放到后台。例如，假设你运行 du -a / | sort -m > /tmp/du.sorted 来按磁盘使用量（大小）顺序列出系统中的所有文件和目录，并将结果放入名为 /tmp/du.sorted 的文件中。根据系统中的文件数量，这可能需要一段时间。在这种情况下，你只需使用 Ctrl+Z 挂起命令行，然后输入 bg 将命令行涉及的所有命令发送到后台，从而返回 shell 提示符以供其他使用。

![](img/c2419364ebb911c809b6a79991707c27_611_0.png)

> 提示
> 如果你想从开始就让命令在后台运行，只需在命令行的末尾加上 & 即可。

要了解后台正在运行哪些命令，请输入 jobs，你将看到后台命令行的列表。要将命令从后台调回前台，请使用 fg 命令。

### fg

Syntax:

```
fg [%job-number]
```

这是一个内置的 shell 命令，常见于流行的 shell 中。fg 命令使你能够将后台进程调到前台。如果不带任何参数运行此命令，它会将你最后放到后台的命令调回前台。如果有多个命令在后台运行，你可以使用 jobs 命令找到作业编号，然后将该编号作为 fg 的参数以将命令调到前台。例如，如果 jobs 显示你有两个后台命令，你可以使用以下命令调出第一个放到后台的命令：

```
fg %1
```

### jobs

Syntax:

```
jobs
```

这是一个内置的 shell 命令，常见于流行的 shell 中。jobs 使你能够查看在后台运行或当前挂起的进程列表。

### Kill -signal PID

此命令用于向进程发送信号。Kill 可以是许多流行 shell（如 csh 和 tcsh）的内置 shell 命令。然而，也有一个外部 kill 程序，通常位于 /bin 目录中。两个版本的工作方式相同。要了解可通过 kill 向进程发送哪些信号，可以运行以下命令：

```
kill -l
```

你应该会看到类似以下的列表：

```
1) SIGHUP  2) SIGINT  3) SIGQUIT  4) SIGILL
5) SIGTRAP  6) SIGIOT  7) SIGBUS  8) SIGFPE
9) SIGKILL  10) SIGUSR1  11) SIGSEGV  12) SIGUSR2
13) SIGPIPE  14) SIGALRM  15) SIGTERM  17) SIGCHLD
18) SIGCONT  19) SIGSTOP  20) SIGTSTP  21) SIGTTIN
22) SIGTTOU  23) SIGURG  24) SIGXCPU  25) SIGXFSZ
26) SIGVTALRM  27) SIGPROF  28) SIGWINCH  29) SIGIO
30) SIGPWR
```

前面的输出由 GNU Bourne-Again Shell (/bin/bash) 中的内置 kill 命令产生。其他 shell 或 /bin/kill 命令可能会以略有不同的方式打印输出。例如，/bin/kill -l 产生以下输出：

```
HUP INT QUIT ILL TRAP IOT UNUSED FPE KILL USR1 SEGV USR2
PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU IO
XCPU XFSZ VTALRM PROF WINCH
```

例如，要向 PID 为 1234 的进程发送 SIGKILL（9），运行

```
kill -KILL 1234
```

或者你也可以运行

```
kill -9 1234
```

你可以使用信号的名称（不带 SIG 前缀）或使用其数值作为信号标识符，如前所示。

### killall

此实用程序允许你按名称终止进程。例如，如果你有一个名为 signal_demo.pl 的进程，并且想在不输入其 PID 的情况下终止它，可以运行

```
killall -KILL signal_demo.pl
```

当你不提供信号名称时，killall 会自动发送 SIGTERM 信号。然而，使用 killall 时要非常小心，因为它会终止指定命令的所有实例。有时，不必知道 PID 的便利性可能会适得其反。

### ps

此实用程序生成系统中所有进程的报告。例如，当我从登录 shell 运行 ps 时，它显示以下输出：

```
PID TTY STAT TIME COMMAND
31795 p7 S 0:00 -tcsh
31811 p7 R 0:00 ps
```

如你所见，ps 提供表格报告。这里，ps 显示我正在运行两个进程：-tcsh shell，实际上是作为登录 shell 运行的 /bin/tcsh shell，以及 ps 进程本身。表 A-1 解释了 ps 常见输出字段的含义。

### 表 A-1 ps 的输出字段

| 字段 | 说明 |
|---|---|
| USER or UID | 进程所有者的用户名。 |
| PID | 进程 ID。 |
| %CPU | 进程的 CPU 利用率。由于计算所依据的时间基准不同，这可能超过 100%。 |
| %MEM | 进程的内存（以千字节为单位）利用率百分比。 |
| SIZE | 进程使用的虚拟内存大小（以千字节为单位）。 |
| RSS | 常驻集大小或进程使用的实际内存大小（以千字节为单位）。 |
| TTY | 与进程关联的终端（tty）。通常 tty 名称会被缩短。例如，/dev/ttyp7 显示为 p7。 |
| STAT | 进程的状态。进程状态由字符表示，例如 R（运行或准备运行）、S（睡眠）、I（空闲）、Z（僵尸）、D（磁盘等待）、P（分页等待）、W（换出）、N（nice 降低优先级）、T（终止）、<（超级用户提高执行优先级）等。 |
| START | 进程启动时间或日期。 |
| TIME | 进程使用的总 CPU 时间。 |
| COMMAND | 正在执行的命令行。 |
| NI | nice 优先级数字。 |
| PRI | 进程优先级数字。 |
| PPID | 父进程的进程 ID（PID）。 |
| WCHAN | 进程睡眠的内核函数名称。函数名称从 /boot/System.map 文件中检索。 |
| FLAGS | 与进程关联的数字标志。 |

ps 实用程序还接受多个命令行参数。表 A-2 显示了常用的选项。

### 表 A-2 常用 ps 选项

| 选项 | 描述 |
|---|---|
| A | 显示所有用户所属的进程。 |
| E | 在正在执行的命令行之后显示进程环境变量。 |
| L | 以长格式显示输出。 |
| U | 显示用户名和进程启动时间。 |

