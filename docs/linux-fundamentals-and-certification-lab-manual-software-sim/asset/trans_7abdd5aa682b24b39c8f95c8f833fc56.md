
## 更多管理任务

- **无选项** 显示当前用户正在运行的进程。

```text
# ps
  PID TTY          TIME CMD
12429 pts/1    00:00:00 su
12430 pts/1    00:00:00 bash
12485 pts/1    00:00:00 ps
```

- **u** 此选项显示与无选项时相同的信息，但提供更多细节。

```text
# ps u
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root      12429  0.0  0.0  4088   944 pts/1    S    10:12   0:00 [su]
root      12430  0.0  0.1  4344  1424 pts/1    S    10:13   0:00 -bash
root      12488  0.0  0.0  2616   676 pts/1    R    10:35   0:00 ps u
```

- **a** a 选项显示在终端上运行的所有进程。以下列表显示 su 是从 jsmith 的 bash shell 中运行以连接为 root 的。

```text
# ps au
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
jsmith    12395  0.0  0.1  4292  1376 pts/1    S    10:12   0:00 -bash
root      12429  0.0  0.0  4088   944 pts/1    S    10:12   0:00 [su]
root      12430  0.0  0.1  4344  1424 pts/1    S    10:13   0:00 -bash
root      12489  0.0  0.0  2624   684 pts/1    R    10:38   0:00 ps au
```

- **x** x 选项将显示所有进程，包括那些不是从终端运行的进程。init 进程是 Linux 操作系统上运行的第一个进程。它在启动时会生成许多进程，并且是所有进程的父进程。此选项将显示大量进程。你应该将其重定向到文件，或者使用 more 过滤器。以下是一个部分列表。

```text
# ps ax | more
  PID TTY          STAT   TIME COMMAND
    1 ?          S      0:27 init
    2 ?          SW     0:00 [migration/0]
    3 ?          SW     0:00 [migration/1]
    4 ?          SW     0:00 [khelperd]
```

- **l** l 选项将给出长格式。

```text
# ps axl | more
F   UID   PID  PPID PRI  NI  VSZ   RSS WCHAN   STAT TTY      TIME COMMAND
4     0     1     0   15   0  1384   488 schedu S    ?        0:27 init
5     0     2     0  -100  0     0     0 migrat SW   ?        0:00 [migration/0]
5     0     3     0  -100  0     0     0 migrat SW   ?        0:00 [migration/1]
1     0     4     1   15   0     0     0 contex SW   ?        0:00 [khelperd]
```

- **--user** 或 **-u** 使用此 GNU 选项查看任何用户的进程。

```text
# ps --user jsmith
  PID TTY          TIME CMD
13071 ?        00:00:00 sshd
13072 pts/1    00:00:00 bash
```

你可以将 -u 与 l 命令结合使用，以获得进程的长列表。

```text
# ps -u jsmith l
F UID PID PPID PRI NI VSZ RSS WCHAN STAT TTY TIME COMMAND
5 501 16619 16617 15 0 6772 1804 schedu S ? 0:00 [sshd]
0 501 16620 16619 15 0 4300 1376 wait4 S pts/0 0:00 -bash
```

- **f** 列出森林视图。所有进程都以某种方式相关联。Linux 操作系统是通过运行 init 进程启动的，所有其他进程都是从 init 生成的。森林视图展示了这种关系。以下是森林视图的部分列表。

```text
# ps axf | more
PID TTY STAT TIME COMMAND
1066 ? S 0:03 syslogd -m 0
1070 ? S 0:00 klogd -x
1088 ? S 0:00 [portmap]
1107 ? S 0:00 [rpc.statd]
1206 ? S 0:12 /usr/sbin/sshd
13766 ? S 0:00 \_ /usr/sbin/sshd
13768 pts/1 S 0:00 | \_ -bash
13882 ? S 0:00 \_ /usr/sbin/sshd
13884 pts/2 S 0:00 \_ -bash
13939 pts/2 R 0:00 \_\_ ps axf
13940 pts/2 S 0:00 \_ more
```

另一个可用于显示森林视图的命令是 **pstree**。pstree 可用于查看某个 PID 或某个用户的完整树结构。

### 完整森林：

```text
# pstree | more
init
|-atd
|-bdflush
|-crond
|-cupsd
|-esd
|-gdm-binary---gdm-binary-T X
| -gdmgreeter
|-gpm
|-kapmd
|-keventd
|-khubd
|-3*[kjournald]
|-klogd
|-kscan/DMA
|-kscan/HighMem
|-kscan/Normal
```

### 进程的层级结构：

```text
# pstree 1206
sshd--sshd---bash
\_sshd---bash---pstree
```

### 单个用户的层级结构：

```text
# pstree dangle
sshd---bash---setup---printconf-tui
```

了解 ps 的选项很有用；然而，一些实际例子将帮助你更好地理解。

列出 oracle 用户拥有的所有进程：`ps -fu oracle`

列出特定进程 ID 的进程信息：`ps -fp pid`。

杀死 apache 用户拥有的所有进程：`ps -fu apache | awk '{print $2}' | xargs kill`

按进程启动以来的经过时间排序列出进程：`ps -eo etime,pid,args | sort -rn`

## 使用 top

**top** 命令提供 Linux 系统进程的动态视图。默认情况下，top 将持续运行。它不仅显示正在运行的进程，还显示关于运行时间、系统内存使用率和交换空间使用情况的信息。top 的关键特性之一是它是交互式的，意味着它可以接受命令来更改显示、杀死进程和更改优先级。

问号 (?) 显示有效命令的列表。man top 命令也显示有关可用命令的信息。

```text
11:44:45  up 22 days,  59 min,   4 users,  load average: 0.04, 0.03, 0.02
96 processes:  95 sleeping,  1 running,  0 zombie,  0 stopped
CPU0  states:  0.3% user   0.0% system   0.0% nice   0.0% iwait  99.2% idle
CPU1  states:  0.0% user   0.3% system   0.0% nice   0.0% iwait  99.2% idle
Mem:  1030344k av, 1005228k used,  25116k free,  0k shrd,  132544k buff
      652164k actv,  564k in_d,  21088k in_c  706776k cached

Swap: 2040244k av,  42984k used, 1997260k free

  PID  USER     PRI   NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND
 14128 root     15  0  1152  1152  872 R    0.0  0.1   0:00  0 top
 14127 jsmith   25 10  1376  1376 1184 S    0.0  0.1   0:12  1 blaster
 14059 dngle    15  0  1344  1344 1072 S    0.0  0.1   0:00  1 bash
 14058 dngle    15  0  1828  1768 1436 S    0.0  0.1   0:00  1 sh
 14054 jsmith   15  0  7048  6968 5676 S    0.0  0.6   0:00  0 notification-
 14048 root     15  0   484   484  428 S    0.0  0.0   0:00  1 pam_timestamp
 14047 jsmith   15  0 13296  12M 8592 S    0.0  1.2   0:55  1 rhn-applet-gu
 14045 jsmith   15  0  4232  4232 3536 S    0.0  0.4   0:00  1 pam-panel-ico
 14043 jsmith   15  0  6812  6812 5636 S    0.0  0.6   0:01  1 eggcups
 14041 jsmith   15  0  6060  6056 5040 S    0.0  0.5   0:00  1 magicdev
 14039 jsmith   15  0 15996  15M 9064 S    0.0  1.5   0:03  1 nautilus
 14037 jsmith   15  0 10940  10M 8232 S    0.0  1.0   0:01  1 gnome-panel
 14033 jsmith   15  0  5852  5848 4740 S    0.0  0.5   0:00  1 metacity
 14030 jsmith   15  0  1772  1772 1436 S    0.0  0.1   0:00  0 xscreensaver
 14025 jsmith   15  0  1188  1188  996 S    0.0  0.1   0:00  1 fam
```

在这个 **top** 命令列表中，运行时间为 22 天，有 4 个用户和 96 个进程。它列出空闲内存为 25,116k，空闲交换空间为 199,726k。进程列表类似于 **ps** 命令。

top 中的 k 命令将删除进程。在使用此命令时的小心疏忽可能会导致严重问题。以安全模式启动可以消除意外杀死进程的可能性。要以安全模式启动，请使用 **top -s** 命令。

安全模式的外观和操作与普通模式相同；但是，如果你使用 k 命令，你将收到消息“无法在安全模式下杀死”。

top 的一个有用选项是“-n”选项。命令 `top -n 1 >> /top.file` 将保存一次 top 迭代的输出到文件 top.file。这是一种在长时间内收集系统性能信息的便捷方式。可以通过 cron 自动化和控制此命令。

如果你正在使用 KDE 或 GNOME，可以显示进程的图形界面。可用的操作和字段与命令行工具相同（图 11-6）。

图形工具提供 CPU 和内存/交换空间使用情况的图形视图（图 11-7）。可以设置属性来选择要显示的字段、更新间隔等。

![](img/37f079cee226b270f2e09b37a2e4a05d_311_0.png)

图 11-6  
GNOME 进程列表。

![](img/37f079cee226b270f2e09b37a2e4a05d_311_1.png)

图 11-7  
GNOME 系统监视器：

## 进程优先级

如本章前面所述，进程被分配优先级值。进程的优先级决定了它可用的 CPU 时间量。Linux 是多任务的，意味着它可以同时运行多个任务。然而，在大多数 Linux 系统上，只有一个 CPU。在这些系统上执行的进程必须轮流使用资源。即使在多处理器系统上，在任何给定时间都有如此多的进程在运行，以至于它们仍必须根据优先级共享 CPU 资源。

Linux 操作系统中使用两个命令来分配优先级——nice 和 renice。nice 命令以特定的优先级级别执行命令。renice 命令更改已经运行的进程的优先级级别。也可以使用 top 或 GNOME 系统监视器更改优先级。

优先级值的范围是从 -20（最高）到 19（最低）。nice 的语法是 nice [options] command，其中选项是 -n 或 --adjustment。要以起始优先级 10 启动名为 sniffer 的程序，使用 nice -n 10 sniffer 命令。

