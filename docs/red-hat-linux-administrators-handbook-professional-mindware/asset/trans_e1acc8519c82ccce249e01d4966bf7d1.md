
如图所示，`ps` 提供了一份表格形式的报告。在这里，`ps` 显示我正在运行两个进程：`tcsh` shell，它实际上是以登录 shell 形式运行的 `/bin/tcsh` shell；以及 `ps` 进程本身。表 6-1 解释了 `ps` 常见输出字段的含义。

## 表 6-1 `ps` 的输出字段

| 字段 | 说明 |
| :--- | :--- |
| USER 或 UID | 进程所有者的用户名。 |
| PID | 进程 ID。 |
| %CPU | 进程的 CPU 使用率。由于计算此值的时间基准不同，该值有可能超过 100%。 |
| %MEM | 进程内存（以千字节计）的使用百分比。 |
| SIZE | 进程使用的虚拟内存大小（以千字节计）。 |
| RSS | 常驻集大小或进程使用的物理内存大小（以千字节计）。 |
| TTY | 与该进程关联的终端（`tty`）。通常，TTY 名称会被缩写。例如，`/dev/tty7` 显示为 `pt7`。 |
| STAT | 进程状态。进程状态由字符表示，例如 **R**（运行中或准备运行）、**S**（睡眠）、**T**（空闲）、**Z**（僵尸）、**D**（磁盘等待）、**P**（分页等待）、**W**（已交换出）、**N**（由 `nice` 降低优先级）、**T**（终止）、`<`（超级用户提升执行优先级）等。 |
| START | 进程启动时间或日期。 |
| TIME | 进程使用的总 CPU 时间。 |
| COMMAND | 正在执行的命令行。 |
| NI | Nice 优先级数值。 |
| PRI | 进程优先级数值。 |
| PPID | 父进程的进程 ID（PID）。 |
| WCHAN | 进程正在睡眠的内核函数名称。该函数名称取自 `/boot/System.map` 文件。 |
| FLAGS | 与进程关联的数值标志。 |

`ps` 实用程序还接受多个命令行参数。表 6-2 显示了常用选项。

## 表 6-2 常用的 `ps` 选项

| 选项 | 描述 |
| :--- | :--- |
| a | 显示属于所有用户的进程。 |
| e | 在执行命令行的后面显示进程的环境变量。 |
| l | 以长格式显示输出。 |
| u | 显示用户名和进程启动时间。 |
| w | 以宽格式显示输出。通常，如果输出无法适合一行，则会被截断。使用此选项可以防止截断。 |
| t | 显示与 TTY 设备关联的进程。 |
| x | 显示没有控制 TTY 的进程。 |

以下是使用 `ps` 选项的几个示例。要查看您当前正在运行的所有进程，请运行以下命令：

```bash
ps u
```

前一条命令的输出示例如下：

```text
USER  PID %CPU %MEM  SIZE  RSS TTY STAT START TIME COMMAND
kabir 18 0.0 0.8 1556 1040 p5 S 08:41 01:00 -tcsh
kabir 135 0.0 0.8 1560 1040 p7 S 09:03 01:00 -tcsh
kabir 852 53.8 0.6 1604 788 p5 R 09:33 01:04 perl ./eatcpu.pl
kabir 855 0.0 0.3 848 45 p7 R 09:34 01:00 ps u
```

这显示了用户 kabir 正在运行的所有进程。请注意，`ps` 本身列在输出中。前两行显示 kabir 正在运行两个 `tcsh` shell 会话。第三行非常有趣，因为它显示名为 `eatcpu.pl` 的 Perl 脚本正在使用大约 53.8% 的 CPU。STAT 标志表明，Perl 脚本和 `ps` 实用程序是这里唯一正在运行（或可运行）的进程。通过查看 TTY 字段，你可以知道哪个进程连接到哪个 TTY。在下一个示例中，`ps` 被指示显示所有进程（排除未与控制 TTY 关联的那个）：

```bash
ps au
```

要了解某个特定用户拥有哪些进程，请运行

```bash
ps au | grep 用户名
```

其中*用户名*是实际用户的名称。

例如，`ps au | grep sheila` 将显示用户 sheila 正在运行的所有交互式进程（与 TTY 关联的进程）。通常，普通用户不允许运行守护进程或与 TTY 不关联的进程。然而，如果你只是想查看是否存在任何用户（不限于特定用户）的此类进程，请运行

```bash
ps aux
```

*x* 选项指示 *ps* 列出已脱离终端的进程。你可以通过查看 *TTY* 字段来识别这些进程，该字段显示 *?* 而不是 *TTY* 设备（如 *p7* (`/dev/ttyp7`)）的缩写名称。

要查找进程的父进程的 *PID*，请运行

```bash
ps l PID
```

其中 *PID* 是该进程的 *PID*。

例如，如果你想查找 *PID* 为 123 的进程的父进程，请运行 `ps l 123`，父进程的 *PID* 将列在报告的 *PPID* 字段中。

要确定哪些初始环境变量可供进程使用，请运行

```bash
ps e
```

环境信息附加在 *COMMAND* 字段之后。

### 注意
普通用户不能使用 *e* 选项来查看其他用户进程的环境信息。这是一个安全特性。只有 root 或等效超级用户才能查看所有进程的环境信息。

## 向运行中的进程发送信号

Linux，以及通常所有 UNIX 系统，都提供了一种向进程发送各种信号的方法。信号是一种异常，通常用于指示进程执行常规操作以外的动作。例如，如果需要终止一个进程，你可以发送一个终止信号。用于向进程发送信号的命令称为 *kill*。这是一个令人困惑的名称，因为 `kill` 可以发送任何有效的信号，而不仅仅是终止进程的信号。

### 使用 `kill`

`kill` 命令可以是许多流行 shell（如 `csh` 和 `tcsh`）的内置命令。但是，也有一个外部 `kill` 程序，通常位于 /bin 目录中。这两个版本的工作方式相同。要了解可以通过 `kill` 向进程发送哪些信号，请运行以下命令：

```bash
kill -l
```

你应该看到如下类似的列表：

```text
1) SIGHUP    2) SIGINT    3) SIGQUIT   4) SIGILL
5) SIGTRAP   6) SIGIOT    7) SIGSEGV   8) SIGFPE
9) SIGKILL   10) SIGUSR1   11) SIGUSR2  12) SIGTSTP
13) SIGCONT  14) SIGCHLD  15) SIGTTIN  16) SIGTTOU
17) SIGIO    18) SIGURG    19) SIGXCPU  20) SIGXFSZ
21) SIGVTALRM 22) SIGPROF  23) SIGWINCH 24) SIGUSR1
25) SIGUSR2  26) SIGRTMIN  27) SIGRTMIN+1 28) SIGRTMIN+2
29) SIGRTMIN+3 30) SIGRTMIN+4 31) SIGRTMIN+5 32) SIGRTMIN+6
```

*注：上述列表是用于更正原文中 OCR 可能存在的错误。根据提供的原始文本，信号列表可能存在格式错误，以下提供两种可能的输出形式，请根据实际系统环境确认。*

你应该看到如下类似的列表：

```text
1) SIGHUP    2) SIGINT    3) SIGQUIT   4) SIGILL
5) SIGTRAP   6) SIGIOT    7) SIGSEGV   8) SIGFPE
9) SIGKILL   10) SIGUSR1   11) SIGUSR2  12) SIGTSTP
13) SIGCONT  14) SIGCHLD  15) SIGTTIN  16) SIGTTOU
17) SIGIO    18) SIGURG    19) SIGXCPU  20) SIGXFSZ
21) SIGVTALRM 22) SIGPROF  23) SIGWINCH 24) SIGUSR1
25) SIGUSR2
```

前面输出的产生于 GNU Bourne-Again Shell（`/bin/bash`）中的内置 `kill` 命令。其他 shell，或 `/bin/kill` 命令可能会生成不同的输出。例如，`/bin/kill -l` 产生以下输出：

```text
HUP INT QUIT ILL TRAP IOT NUSUED FPE KILL USR1 SEGV USR2
PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU ITO
XCPU XFSZ VTALRM PROF WINCH
```

请注意，这两个 `kill` 命令在它们产生的 `-l` 输出方面有所不同。实际上，如果你使用 `/bin/csh`（C shell）或 `/bin/tcsh`（增强型 C shell）并运行带有 `-l` 选项的内置 `kill` 命令，你会得到另一个与这些都不匹配的列表。为了确定 Red Hat Linux 下真正可用的信号，并交互式地演示如何使用 `kill` 向进程发送各种信号，我编写了一个名为 `gen_signal_demo.pl` 的 Perl 脚本，如列表 6-1 所示，用于识别我的 Red Hat Linux 系统上可用的信号。

## 列表 6-1 `gen_signal_demo.pl`

```perl
#!/usr/bin/perl
#
#  第 6 章
#
#  作者：kibir@nitec.com
#
#  目的：生成一个 Perl 脚本，该脚本安装
#       所有可能信号的信号处理程序。
#       此脚本用于交互式地演示如何捕获信号。
#
#  说明：我不尝试阻止脚本为不可中断的信号
#       （KILL, STOP）安装无用的信号处理程序。
#
#       此脚本严格仅用于演示目的。
#
#  语法：gen_signal_demo.pl > signal_demo.pl
#-------------------------------------------------

# 首先生成 #!/usr/bin/perl 行
#
print <<SBANG;
#!/usr/bin/perl

SBANG

foreach $signal (keys %SIG) {
```
