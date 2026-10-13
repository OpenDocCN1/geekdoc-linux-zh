
您可以按天、小时、分钟甚至秒来指定宽限期。例如，下面示例中，磁盘空间限制（以块为单位）的宽限期为 7 天，而文件数量（inode）的宽限期仅为 5 小时：

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 7 days, file grace period:
5 hours
```

## 监控磁盘使用情况

要了解特定用户使用了多少磁盘空间，请按如下方式运行 quota 命令：

```
quota -u username
```

例如：

```
quota -u kabir
Disk quotas for user kabir (uid 500):
Filesystem blocks quota limit grace files quota limit grace
/dev/sda5 0 1024 4096 1 128 512
```

您可以使用相同命令来监控组的磁盘使用情况，如下所示：

```
quota -g group
```

当您发现用户或组超出限制时，可以向他们发送电子邮件，以便将磁盘使用量降至可接受的限制。

## 进程管理

### 控制和监控进程

守护进程通常在启动时由 init 进程启动。您可以通过重新配置 /etc/inittab 以及 /etc/rc.d 目录中的运行级别配置文件和脚本来控制启动时运行哪些守护进程。除了守护进程之外，您运行的其他类型的进程称为用户进程或交互式进程。您通过 shell 运行交互式进程。每个标准 shell 都提供一个命令行，用户可在其中输入程序名称。当用户在命令行中输入有效的程序名称时，shell 会复制自身作为一个新进程，并用命令行中指定的程序替换该新进程。换句话说，shell 将命名程序作为另一个进程运行。

要获取系统上所有正在运行进程的信息，您运行名为 ps 的实用程序。

### 使用 ps 获取进程状态

这个巧妙的实用程序会生成系统中所有进程的报告。例如，当我从登录 shell 运行 ps 时，它显示以下输出：

```
PID TTY STAT TIME COMMAND
31795 p7 S 0:00 -tcsh
31811 p7 R 0:00 ps
```

如您所见，ps 提供了一个表格报告。在这里，ps 显示我正在运行两个进程：-tcsh shell，实际上是作为登录 shell 运行的 /bin/tcsh shell，以及 ps 进程本身。表 6-1 解释了 ps 常用输出字段的含义。

表 6-1 ps 的输出字段

| 字段 | 说明 |
|---|---|
| USER or UID | 进程所有者的用户名。 |
| PID | 进程 ID。 |
| %CPU | 进程的 CPU 利用率。由于计算所依据的时间基准各不相同，因此该值可能超过 100%。 |
| %MEM | 进程的内存（以千字节为单位）利用率百分比。 |
| SIZE | 进程使用的虚拟内存大小（以千字节为单位）。 |
| RSS | 常驻集大小或进程使用的实际内存大小（以千字节为单位）。 |
| TTY | 与进程关联的终端（tty）。通常 tty 名称会被缩短。例如，/dev/ttyp7 显示为 p7。 |
| STAT | 进程状态。进程状态由字符表示，例如 R（运行或准备运行）、S（睡眠）、I（空闲）、Z（僵尸）、D（磁盘等待）、P（分页等待）、W（换出）、N（nice 降低优先级）、T（终止）、<（执行优先级由主管提高）等。 |
| START | 进程启动时间或日期。 |
| TIME | 进程使用的总 CPU 时间。 |
| COMMAND | 正在执行的命令行。 |
| NI | nice 优先级数字。 |
| PRI | 进程优先级数字。 |
| PPID | 父进程的进程 ID（PID）。 |
| WCHAN | 进程睡眠时所在的内核函数名称。函数名称从 /boot/System.map 文件中获取。 |
| FLAGS | 与进程关联的数字标志。 |

ps 实用程序还接受多个命令行参数。表 6-2 显示了常用的选项。

### 表 6-2 常用 ps 选项

| 选项 | 描述 |
|---|---|
| a | 显示所有用户所属的进程。 |
| e | 在正在执行的命令行之后显示进程环境变量。 |
| l | 以长格式显示输出。 |
| u | 显示用户名和进程启动时间。 |
| w | 以宽格式显示输出：通常，如果输出无法在一行中容纳，则会被截断。使用此选项可以防止截断。 |
| txx | 显示与 xx tty 设备关联的进程。 |
| x | 显示没有控制 tty 的进程。 |

下面提供了使用 ps 选项的几个示例。

要随时查看您正在运行的所有进程，请运行以下命令：

```
ps u
```

下面显示了前述命令输出的示例：

```
USER PID %CPU %MEM SIZE RSS TTY STAT START TIME COMMAND
kabir 18 0.0 0.8 1556 1040 p5 S 08:41 0:00 -tcsh
kabir 135 0.0 0.8 1560 1040 p7 S 09:03 0:00 -tcsh
kabir 852 53.8 0.6 1604 788 p5 R 09:33 0:04 perl ./eatcpu.pl
kabir 855 0.0 0.3 848 484 p7 R 09:34 0:00 ps u
```

这显示了名为 kabir 的用户正在运行的所有进程。请注意，ps 本身也列在输出中。前两行显示 kabir 正在运行两个 tcsh shell 会话。第三行非常有趣，因为它显示名为 eatcpu.pl 的 Perl 脚本使用了大约 53.8% 的 CPU。STAT 标志表明 Perl 脚本和 ps 实用程序是这里唯一正在运行（或可运行）的进程。

通过查看 TTY 字段，您可以判断哪个进程附加到哪个 tty。

在下一个示例中，ps 被告知显示所有进程（不包括与任何控制 tty 无关的进程）：

```
ps au
```

要了解特定用户拥有哪些进程，请运行

```
ps au | grep username
```

其中 username 是实际用户的名称。

例如，ps au | grep sheila 将显示名为 sheila 的用户正在运行的所有交互式进程（与 tty 关联的进程）。通常，普通用户不允许运行守护进程或与 tty 无关联的进程。但是，如果您只是想了解是否存在任何用户的此类进程，请运行

```
ps aux
```

x 选项指示 ps 列出与终端分离的进程。您可以通过查看 TTY 字段来识别这些进程，该字段显示 ? 字符而不是 tty 设备（如 p7（/dev/ttyp7））的缩写名称。

要查找进程父进程的 PID，您可以运行

```
ps l PID
```

其中 PID 是该进程的 PID。

例如，如果您想查找 PID 为 123 的进程的父进程，请运行 ps l 123，父进程的 PID 将列在报告的 PPID 字段中。

要确定进程可用的初始环境变量，请运行

```
ps e
```

环境信息附加到 COMMAND 字段。

![](img/c2419364ebb911c809b6a79991707c27_139_0.png)

### 注意

普通用户不能使用 e 选项查看其他用户进程的环境信息。这是安全功能。只有 root 或等效超级用户才能查看所有进程的环境信息。

## 向正在运行的进程发出信号

Linux 以及所有 UNIX 系统通常都提供向进程发送各种信号的方法。信号是一种异常，通常用于指示进程执行与通常不同的操作。例如，如果需要终止一个进程，可以向其发送终止信号。向进程发出信号的命令称为 kill。名称令人困惑，因为 kill 可用于发送任何有效信号，而不仅仅是终止进程的信号。

### 使用 kill

kill 命令可以是许多流行 shell（如 csh 和 tcsh）的内置 shell 命令。但是，还有一个外部 kill 程序，通常位于 /bin 目录中。两个版本的工作方式相同。要了解可通过 kill 向进程发送哪些信号，可以运行以下命令：

```
kill -l
```

您应该会看到类似以下内容的列表：

```
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL
5) SIGTRAP 6) SIGIOT 7) SIGBUS 8) SIGFPE
9) SIGKILL 10) SIGUSR1 11) SIGSEGV 12) SIGUSR2
13) SIGPIPE 14) SIGALRM 15) SIGTERM 17) SIGCHLD
18) SIGCONT 19) SIGSTOP 20) SIGTSTP 21) SIGTTIN
22) SIGTTOU 23) SIGURG 24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGIO
30) SIGPWR
```

前面的输出是由 GNU Bourne-Again Shell（/bin/bash）中的内置 kill 命令产生的。其他 shell 或 /bin/kill 命令可能会以略有不同的方式打印输出。例如，/bin/kill -l 产生以下输出：

```
HUP INT QUIT ILL TRAP IOT UNUSED FPE KILL USR1 SEGV USR2
PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU IO
XCPU XFSZ VTALRM PROF WINCH
```
