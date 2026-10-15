
```
root 2257 1 14:28 ? 00:00:00 /usr/bin/jserver

xfs 2293 1 14:28 ? 00:00:01 xfs -dropprivoir -daemon

daemon 2312 1 14:28 ? 00:00:00 dbus-daemon-1 --system

dbus 2331 1 14:28 ? 00:00:00 dbus-daemon-1 --scan

root 2347 1 14:28 ? 00:00:00 mdadm --monitor tty

root 2389 1 14:28 ? 00:00:00 /usr/sbin/mingetty tty

root 2390 1 14:28 ? 00:00:00 login - root

root 2391 1 14:28 tty3 00:00:00 /usr/sbin/mingetty tty3

root 2399 1 14:28 tty4 00:00:00 /usr/sbin/mingetty tty4

root 2407 1 14:28 tty5 00:00:00 /usr/sbin/mingetty tty5

root 2415 1 14:28 tty6 00:00:00 /usr/sbin/mingetty tty6

root 2423 1 14:28 ? 00:00:00 /usr/bin/gdm-binary -nodaem

root 2824 2823 0 14:28 ? 00:00:00 /usr/sbin/utd -nodaem

root 2839 2824 4 14:28 ? 00:00:38 /usr/X11R6/bin/X:0 -audit 0 -auth

/var/gdm:/0.Xauth -nolisten tty v7

root 2901 2824 0 14:28 ? 00:00:01 gnome-session

root 3193 3192 0 14:29 ? 00:00:00 gnome-pty-helper

root 3232 2390 0 14:29 pty 1/1 00:00:00 bash

root 3429 3194 0 14:41 tty2 00:00:00 -bash

00:00:00 ps -ef

root@server1]#
```

如前面的输出所示，`init`守护进程启动了其他守护进程（`PID=1`），因为这些守护进程的父进程 ID（`PPID`）为 1。此外，对于不在终端上运行的守护进程，TTY 列中显示为 `?`。

## 10 管理 Linux 进程

由于 `ps -ef` 命令的输出在 Linux 服务器上可能有几百行，通常会将其输出管道到 `less` 命令或 `grep` 命令，以便只显示特定信息。例如，要只显示输出中的 shell，使用以下命令：

```
[@server1]# ps -ef | grep bash

root 3194 3192 0 14:29 pts/1 00:00:00 bash

root 3232 2390 0 14:30 tty2 00:00:00 bash

root 3431 3194 0 14:44 tty2 00:00:00 grep

[@server1]#
```

注意 `grep` 命令也会显示在 shell 旁边，因为它在执行 `ps` 命令时正在运行。`-e` 和 `-f` 是常用的选项，但 `-l` 选项提供的信息更多。查看 tty 进程的示例：

```
[@server1]# ps -l

F S UID C PRI NI ADDR WCHAN TTY TIME CMD

S 0 3232 3192 0 75 0 1238 tty2 00:00:00 bash

R 0 3438 3232 0 77 0 744 - tty2 00:00:00 ps

[@server1]#
```

### 查看进程 439

进程优先级（`PRI`）由内核使用；范围在 0（高优先级）到 127（低优先级）之间。nice 值（`NI`）可以间接影响优先级；范围在 -20（较高优先级）到 19（较低优先级）之间。前面输出中的 `ADDR` 表示进程的内存地址，而 `WCHAN` 表示进程正在等待。此外，进程大小（`SZ`）也会列出，并以字节为单位；它通常等同于执行文件的大小。

`ps` 命令的选项以连字符开头；这些被称为 Berkeley 风格选项。最常用的是 `e` 和 `x` 选项，它们列出跨终端且不在终端上运行的进程，如下所示：

```
[server1 root]# ps

PID TTY STAT TIME COMMAND

1 ? S 0:05 [init]

2 ? S 0:00 [ksoftirqd/0]

3 ? S 0:00 [events/0]

4 ? S 0:00 [kblockd/0]

6 ? S 0:00 [khelper]

5 ? S 0:00 [khubud]

7 ? S 0:00 [pdfflush]

8 ? S 0:00 [pdfflush]

10 ? S 0:00 [aio/0]

9 ? S 0:00 [kswapd0]

114 ? S 0:00 [kseriod]

153 ? S 0:00 [journalad]

347 ? S < 0:00 udevd

1681 ? S 0:00 syslogd -m 0

1685 ? S 0:00 klogd -x

1706 ? S 0:00 portmap

1726 ? S 0:00 rpc.statd

1754 ? S 0:00 rpc.idmapd

1798 ? S 0:00 hcid: processing events

1804 ? S 0:00 /usr/sbin/sddp

1811 ? S < 0:00 [krfcommd]

1870 ? S 0:00 /usr/sbin/acpid

1880 ? S 0:00 /usr/sbin/atd

1915 ? S 0:00 cuspd

2110 ? S 0:00 /usr/sbin/sshd

2125 ? S 0:00 minited -stayalive-pidfile

2144 ? S 0:00:00 sendmail: accepting connections

2165 ? S 0:00:01 /usr/bin/spamd -d -c -a -m5 -H

2220 ? S 0:00:00 /usr/sbin/httt

2221 2220 0 14:28 ? 00:00:00 htt_server -nodaem

2232 ? S 00:00:00 /usr/sbin/cannaserver -syslog -u

2245 ? S 00:00:00 crond

2257 ? S 00:00:00 /usr/bin/jserver

2293 ? S 00:00:01 xfs -dropprivoir -daemon

2312 ? S 00:00:00 dbus-daemon-1 --system

2331 ? S 00:00:00 dbus-daemon-1 --scan

2347 ? S 00:00:00 mdadm --monitor tty

2389 ? S 00:00:00 /usr/sbin/mingetty tty

2390 ? S 00:00:00 login - root

2391 tty3 00:00:00 /usr/sbin/mingetty tty3

2399 tty4 00:00:00 /usr/sbin/mingetty tty4

2407 tty5 00:00:00 /usr/sbin/mingetty tty5

2415 tty6 00:00:00 /usr/sbin/mingetty tty6
```

## 查看进程

### 表 10-1 ps 命令的常用选项

| 选项 | 描述 |
| :--- | :--- |
| `-e` | 显示所有在终端上运行的进程，以及不在终端上运行的进程（守护进程） |
| `-f` | 显示每个进程的完整列表，包括 UID、PID、PPID、CPU 占用率、启动时间、处理器时间和命令名称 |
| `-l` | 显示每个进程的详细列表信息，包括标志、状态、UID、PID、PPID、CPU 占用率、优先级、nice 值、地址、大小、WCHAN 和命令名称 |
| `a` | 显示所有在终端上运行的进程 |
| `x` | 显示所有不在终端上运行的进程 |

`ps` 命令不是查看进程信息的唯一命令。内核在 `/proc` 目录下导出了所有进程子目录；每个子目录的名称以其包含的进程的相应 PID 命名，如下所示：

```
root@server1]# ls /proc

10 2110 2859 3193 9 filesystems mtrr

11 2125 2390 3194 acpi fs net

114 2144 2391 3140 aide partitions

153 2153 2399 3142 bluetooth interrupts pci

1681 2165 2407 3144 buddyinfo iomem scsi

1685 2175 2415 3146 bus ports self

1706 2190 2422 3148 cmdline irq have

1726 2220 2824 3132 cpuinfo kscore stat

1754 2221 2889 3151 create kmsg swaps

1798 2292 2901 3154 process loadavg sys

1804 2255 2964 3177 disstats sysrq-trigger

1821 2257 2978 3179 d mdstat sysvipc

1870 2293 2981 3181 3 dri meminfo tat

1880 2312 2983 3188 6 driver misc uptime

1915 2331 2985 3190 7 execdomains modules version

2 2347 2987 3192 8 fb mounts vmstat
```

因此，任何程序都可以读取 `/proc` 目录来显示进程信息。除了 `ps` 之外，最常用的显示进程程序是 **top** 及其变体。`top` 命令显示一个按处理器时间组织的交互式屏幕列表。使用最多处理器时间的进程将列在屏幕顶部。当你输入 `top` 命令时显示的屏幕示例所示：

```
top - 15:02:13 up 35 min, 3 users, load average: 0.11, 0.26, 0.25

Tasks: 81 total, 2 running, 79 sleeping, 0 stopped, 0 zombie

Cpu(s): 8.4 us, 3.8% sy, 0.3% id, 5.2% wa, 0.3% hi, 0.0% si

Mem: 257108kb total, 248228kb used, 8880k free, 174166 buffers
```

- - Z,B 全局：'Z' 颜色映射；'B' 禁用/启用粗体
- l,t,m 切换摘要：'l' 负载平均；'t' CPU 统计；'m' 内存信息
- l,I 切换 SMP 视图：'i' 单/独立状态；'I' Irix/Solaris 模式
- f,o 字段/列：'f' 添加或删除；'o' 更改显示顺序
- F 或 O 选择排序字段
- <, 移动排序字段：<' 下一列左移；'> 下一列右移
- R 切换正常/反向排序
- c,i,S 切换：'c' 命令行显示；'y' 任务 ID；'S' 累计时间
- x,y 切换高亮：'x' 排序字段；'y' 运行任务
- z,b 切换：'z' 颜色/单色；'b' 粗体/反转（仅当 'x' 或 'y' 时有效）
- u 显示特定用户
- n 或 # 设置显示的最大任务数
- k,r 操作任务：'k' 杀死；'r' 调整优先级
- d 或 s 设置更新间隔
- w 写入配置文件
- q 退出

（ 带有 '.' 显示的命令需要可见的任务显示窗口 ）
按 'h' 或 '?' 获取窗口帮助，
按任何其他键继续

## 杀死进程

如前所述，大量的流氓进程和僵尸进程占用系统资源，应该向它们发送 kill 信号以终止它们并提高整体系统性能。发送 kill 信号最常用的命令是 `kill` 命令。`kill` 命令可以向特定进程发送 64 种不同的 kill 信号，每个信号的操作方式都不同。要查看不同的 kill 名称和关联数字，请使用 `kill` 命令的 `-l` 选项，如下所示：

```
# 示例命令
```

## 第 10 章 管理 Linux 进程

大多数命令如 `ls`、`find` 和 `grep` 都是存在文件系统中的二进制程序，直到执行时才会运行。它们用特定的编程语言编写，并编译成只有计算机才能理解的二进制格式。其他命令如 `cd` 和 `exit` 是内置在内存中运行的 BASH shell 中的，被称为 shell 函数。Shell 脚本也可以包含二进制程序列表、shell 函数以及供 shell 按照顺序执行的特殊结构（special constructs）。

在执行编译后的程序或 shell 脚本时，解释你输入的命令的 BASH shell 会创建一个新的 BASH shell。这个过程被称为“分叉（forking）”，由 BASH shell 中的 `fork` 函数执行。该新 shell 然后将使用其 `exit` 函数执行二进制程序或 shell 脚本。在二进制程序或 shell 脚本完成后，新的 BASH shell 使用其 `exit` 函数终止自身，并将控制权返回给原始 BASH shell。原始 BASH shell 使用其 `wait` 函数等待新的 BASH shell 完成上述任务，然后向用户返回提示符。图 10-3 描绘了用户在命令行输入 `ls` 命令时的这一过程。

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_463_0.png)

图 10-3 进程分叉

## 在后台运行进程

如上一节所述，BASH shell 会分叉出一个子 shell 来执行 Linux 系统上的大多数命令。遗憾的是，原始 BASH shell 必须等待子 shell 中的命令完成后，才会显示 shell 提示符以接受新命令；以这种方式运行的命令被称为前台进程（foreground processes）。

或者，你可以通过在命令后添加 ampersand (`&`) 来省略图 10-3 所示的 `wait` 函数。以这种方式运行的命令被称为后台进程（background processes）。当命令在后台运行时，shell 会立即返回 shell 提示符，让用户输入另一个命令。要在后台运行示例命令，你可以输入以下命令：

```
@server1 root# sample &

[1] 2583

@server1 root# _
```

> 命令与 ampersand (`&`) 之间的空格是可选的；命令 `sample&` 等于前面输出中的命令 `sample&`。

shell 返回 PID（上例中为 2583）和后台作业 ID（上例中为 1），这样你就可以对其运行的后台作业进行操作。进程启动后，你可以使用 `ps` 命令查看 PID，或使用 `jobs` 命令查看后台作业 ID，如下所示所示：

```
@server1 root# jobs

[1]+ Running sample &

@server1 root# ps | grep sample

2583 tty2 00:00:00 sample

@server1 root# _
```

要终止后台进程，你可以像本章前面所示那样向 PID 发送 `kill` 信号，或者向后台作业 ID。后台作业 ID 必须以 `%` 符号为前缀才能终止之前创建的 sample 后台进程。对于 `SIGINT` 信号，你可以使用以下命令：

```
@server1 root# jobs

[1]+ Running sample &

@server1 root# kill -2 %1

@server1 root# jobs

@server1 root# _
```

你也可以使用 `killall -2` 命令或 `top` 工具来终止上例中使用的 sample 后台进程。

后台进程启动后，可以使用前台 (`fg`) 命令加上后台作业 ID 将其移动到前台。同样，前台进程可以使用 `Ctrl+z` 键组合暂停，并使用后台 (`bg`) 命令发送到后台。`Ctrl+z` 键组合为前台进程分配作业 ID，该 ID 用作 `bg` 命令的参数。要在后台启动示例并移动到前台，然后暂停并再次移动到后台，可以使用以下命令：

```
[root@server1]# sample & 

[1] 7519

[root@server1]# bg %1

sample
```

```
[Ctrl]-z

[1]+ Stopped sample

[root@server1]# bg %1

[1]+ sample &

[root@server1]# jobs

[1]+ Running sample &

[root@server1]# #
```

当 shell 中有多个后台进程在执行时，`jobs` 命令用 `+` 符号表示最近的一个，用 `-` 符号表示次近的。如果你在未指定后台作业 ID 的命令中使用 `%` 符号，则命令将作用于最近的后台进程。以下输出显示了一个示例，其中启动了四个 sample 进程并使用 `%` 符号发送了 `SIGQUIT` kill 信号：

```
[root@server1]# sample &

[1] 7605

[root@server1]# sample2 &

[2] 7623

[root@server1]# sample3 &

[3] 7621

[root@server1]# sample4 &

[4] 7629

[root@server1]# jobs sample &

[2] Running sample2 &

[3]- Running sample3 &

[4]+ Running sample4 &
```
