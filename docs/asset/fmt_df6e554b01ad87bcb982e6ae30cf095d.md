
列出特定进程 ID 的进程信息：`ps -fp pid`。

杀死 `apache` 用户拥有的所有进程：`ps -fu apache | awk '{print $2}' | xargs kill`

按进程启动以来的经过时间排序列出进程：`ps -eo etime,pid,args | sort -rn`

## 使用 `top`

`top` 命令提供 Linux 系统进程的动态视图。默认情况下，`top` 将持续运行。它不仅显示正在运行的进程，还显示关于运行时间、系统内存使用率和交换空间使用情况的信息。`top` 的关键特性之一是它是交互式的，意味着它可以接受命令来更改显示、杀死进程和更改优先级。

问号 (`?`) 显示有效命令的列表。`man top` 命令也显示有关可用命令的信息。

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

在这个 `top` 命令列表中，运行时间为 22 天，有 4 个用户和 96 个进程。它列出空闲内存为 `25,116k`，空闲交换空间为 `199,726k`。进程列表类似于 `ps` 命令。

`top` 中的 `k` 命令将删除进程。在使用此命令时的小心疏忽可能会导致严重问题。以安全模式启动可以消除意外杀死进程的可能性。要以安全模式启动，请使用 `top -s` 命令。

安全模式的外观和操作与普通模式相同；但是，如果你使用 `k` 命令，你将收到消息“无法在安全模式下杀死”。

`top` 的一个有用选项是“-n”选项。命令 `top -n 1 >> /top.file` 将保存一次 `top` 迭代的输出到文件 `top.file`。这是一种在长时间内收集系统性能信息的便捷方式。可以通过 `cron` 自动化和控制此命令。

如果你正在使用 `KDE` 或 `GNOME`，可以显示进程的图形界面。可用的操作和字段与命令行工具相同（图 11-6）。

图形工具提供 `CPU` 和内存/交换空间使用情况的图形视图（图 11-7）。可以设置属性来选择要显示的字段、更新间隔等。

![](img/37f079cee226b270f2e09b37a2e4a05d_311_0.png)

图 11-6

`GNOME` 进程列表。

![](img/37f079cee226b270f2e09b37a2e4a05d_311_1.png)

图 11-7

`GNOME` 系统监视器：

## 进程优先级

如本章前面所述，进程被分配优先级值。进程的优先级决定了它可用的 `CPU` 时间量。Linux 是多任务的，意味着它可以同时运行多个任务。然而，在大多数 Linux 系统上，只有一个 `CPU`。在这些系统上执行的进程必须轮流使用资源。即使在多处理器系统上，在任何给定时间都有如此多的进程在运行，以至于它们仍必须根据优先级共享 `CPU` 资源。

Linux 操作系统中使用两个命令来分配优先级——`nice` 和 `renice`。`nice` 命令以特定的优先级级别执行命令。`renice` 命令更改已经运行的进程的优先级级别。也可以使用 `top` 或 `GNOME` 系统监视器更改优先级。

优先级值的范围是从 `-20`（最高）到 `19`（最低）。`nice` 的语法是 `nice [options] command`，其中选项是 `-n` 或 `--adjustment`。要以起始优先级 `10` 启动名为 `sniffer` 的程序，使用 `nice -n 10 sniffer` 命令。

在监控系统进程时，您可能会发现某些进程占用了过多的 `CPU` 时间。究竟多少时间算“过多”，只能通过在该进程运行的特定机器上的经验来学习。不过，有些进程占用时间过长的问题是显而易见的。例如，如果由 `jsmith` 拥有的一个进程始终占用 `70%` 的 `CPU` 时间，那么该进程可能存在问题。`renice` 程序可用于在不中断其操作的情况下更改进程的优先级。

`renice` 命令用于更改正在运行的进程的优先级。可以为 `PID`、进程组 (`pgrp`) 或用户名更改优先级。`renice` 的语法为 `renice priority [[-p] pid ...] [[-g] pgrp ...] [[-u] user ...]`，其中 `pid` 是进程 ID 列表，`pgrp` 是进程组 ID 列表，`user` 是用户名列表。例如，若要使用 `renice` 将用户 `jsmith` 的优先级更改为较低的值 `5`，请使用 `renice +5 -u jsmith` 命令。

您还可以更改多个用户或 `PID` 的优先级。例如，要将 `PID` `14343` 以及用户 `jsmith` 和 `dangle` 的优先级更改为 `10`，请使用 `renice +10 14343 -u dangle jsmith` 命令。此命令将 `PID` `14343` 以及由 `dangle` 和 `jsmith` 拥有的所有进程的优先级更改为 `10`。

## 终止、挂起和重启进程

进程并不总是按您的预期运行。原因可能是程序中的*错误*或硬件故障。例如，您可能编写了一个执行循环的脚本，其中包含一个编程错误，导致循环永远不会终止。请检查以下脚本：

```
# cat forever_loop
#!/bin/bash
I=0
J=10
until [ $I -ge $J ]; do
	echo The value of I is $I
	sleep 1
done
#
```

![](img/37f079cee226b270f2e09b37a2e4a05d_312_0.png)
