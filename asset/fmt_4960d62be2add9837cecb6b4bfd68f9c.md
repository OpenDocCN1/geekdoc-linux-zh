
# `ps` 命令使用说明

默认 `ps` 列表中的列分别是进程标识符（PID）、执行命令的终端（TTY）、进程消耗的 CPU 时间（TIME）以及实际执行的命令（CMD），包括传递给程序的任何命令行选项。

或者，如果你想获取更多关于当前用户进程的信息，可以添加 `-f` 参数：

```
$ ps -f
UID PID PPID C STIME TTY TIME CMD
pwatters 29081 29079 0 10:40:30 pts/8 0:00 /bin/ksh
```

同样，显示了 PID、TTY、CPU 时间和命令。但是，还显示了 UID、父进程标识符（PPID）的 PID 以及进程的启动时间（STIME）。此外，还有一个废弃的列（C）用于显示进程利用率。

为了获取尽可能详细的信息，你还可以使用 `-l` 选项，它的意思是“长（long）——事实如此，如示例所示：

```
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
8 S 6049 29081 29079 0 51 20 e11b4830 372 e11b489c pts/8 0:00 ksh
8 R 6049 29085 29081 0 51 20 e101b0d0 512 pts/8 0:00 bash
```

在这里，你可以看到以下内容：

- 与进程相关的标志（F）
- 进程的状态（S）`29081` 是睡眠状态，S；`29085` 是运行状态，R
- 进程标识符 `29081` 和 `29085`
- 父进程标识符 `29079` 和 `29081`
- 进程利用率（废弃）
- 进程优先级（PRI），为 51
- Nice 值（NI），为 20
- 内存地址（ADDR），用十六进制表示 `e11b4830` 和 `e101b0d0`
- 大小（SZ），以千字节为单位，分别为 372KB 和 512KB
- 睡眠进程事件的内存地址（WCHAN），对于 PID `29081` 为 `e11b489c`
- 使用的 CPU 时间（TIME）
- 执行的命令（CMD）

## 查看系统所有进程

如果你是系统管理员，你可能不仅对自己的进程状态感兴趣；你可能想了解系统上活动运行的所有或某些进程的详情，可以通过许多方式实现。例如，你可以使用 `-A` 或 `-e` 选项生成进程列表，这两个任何一个都会提供机器上当前运行的所有进程的信息：

```
# ps -A
PID TTY TIME CMD
0 ? 0:00 sched
1 ? 0:01 init
2 ? 0:01 pageout
3 ? 0:49 fsflush
258 ? 0:00 ttymon
108 ? 0:00 rpcbind
255 ? 0:00 sac
60 ? 0:00 devfs
62 ? 0:00 devfs
157 ? 0:03 automount
110 ? 0:04 nis_cache
112 ? 165 ? syslog
```

同样，显示了 PID、TTY、CPU 时间和命令。列出的进程与调度器、其他应用程序和服务有关。熟悉系统的主进程以及它们消耗的 CPU 时间是一个良好的习惯。

`ps` 的功能之一是可以组合标志以打印更详细的列表。例如，你可以结合 `-A` 和 `-f` 产生详细的进程列表：

```
# ps -Af
UID PID C STIME TTY TIME CMD
root 0 Mar 20 ? 0:00 sched
root 1 Mar 20 ? 0:01 init
root 2 Mar 20 ? 0:01 pageout
root 3 Mar 20 ? 0:51 fsflush
root 258 255 Mar 20 ? 0:00 /usr/lib/ttymon
root 108 1 Mar 20 ? 0:00 /sbin/rpcbind
root 255 1 Mar 20 ? 0:00 /usr/lib/sac
root 60 1 Mar 20 ? 0:00 /usr/lib/devadm/deventd
root 62 1 Mar 20 ? 0:00 /usr/lib/devadm/devfsmd
root 157 1 Mar 20 ? 0:03 /usr/lib/autofs/automount
root 110 1 Mar 20 ? 0:01 /sbin/keyserv
```

![](img/11bcccd1804574cca0c3018732958dd5_200_0.png)

root      112 1 Mar 20 ? 0:05 /sbin/nis_cachemgr
root      165 1 Mar 20 ? 0:00 /sbin/syslogd

## 调度器格式与 `top`

`ps` 的另一个用途是按适用于调度器的格式处理进程信息：

```
# ps -c
BID CLS PRI TTY TIME CMD
29081 TS 48 pts/8 0:00 ksh
29085 TS 48 pts/8 0:00 bash
```

这可以与 `top` 命令配合使用，该命令显示用于进程调度的参数。这特别允许管理员确定系统当前可用的进程类，或将特定进程设置为交互或时间共享。你可以通过向 `top` 传递 `-l` 参数获取所有支持类的列表：

```
# top -l
CONFIGURED CLASSES
===================
SYS (Time Sharing)
TS (Interactive)
Configured TS Priority Range: -60 through 60
FX (Fixed priority)
Configured FX Priority Range: 0 through 60
```

你可以将其结合 `ps -c` 的 `-f` 显示标志获取更多信息：

```
$ ps -cf
UID PID PPID CLS PRI STIME TTY TIME CMD
paul 29081 29079 TS 48 10:40:30 pts/8 0:00 /bin/ksh
paul 29085 29081 TS 48 10:40:51 pts/8 0:00 /usr/local/bin/bash
```

如果你想获取由特定组用户执行的进程信息，可以在命令行上使用 `-g` 选项，后跟目标组的 GID。在这个示例中，所有来自用户 0 的进程将被打印：

```
$ ps -g 0
PID TTY TIME CMD
0 ? 0:00 sched
1 ? 0:01 init
2 ? 0:01 pageout
3 ? 9:51 fsflush
```

另一个常用的 `ps -j` 配置选项是显示会话标识符（SID）和进程组标识符（PGID），如下：

```
$ ps -j
```

| PID PGID SID TTY TIME CMD |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 29081 | 29081 | 29081 | pts/8 | 0:00 | ksh |
| 29085 | 29081 | 29085 | pts/8 | 0:00 | bash |

| PID LWP TTY TIME CMD |
| :--- | :--- | :--- | :--- | :--- |
| 29081 | 1 | pts/8 | 0:00 | ksh |
| 29085 | 1 | pts/8 | 0:00 | bash |

最后，你可以打印出系统中轻量级进程（LWP）的状态。这些是虚拟 CPU 资源，旨在根据其优先级和调度类最有效地利用 CPU 资源。这里有一个示例：

```
$ ps -L
```

| PID LWP TTY TIME CMD |
| :--- | :--- | :--- | :--- | :--- |
| 29081 | 1 | pts/8 | 0:00 | ksh |
| 29085 | 1 | pts/8 | 0:00 | bash |

## 使用 `top` 程序

如果你是管理员，你可能想监控系统上运行的所有进程，特别是当系统处于生产环境时。有 Bug 的程序会消耗大量的 CPU 时间，阻止应用程序履行职责。不断监控进程列表是必要的，特别是当性能开始下降时。你可以每隔五分钟输入一次 `ps -caf`，但一种更有效的方法是使用 `top` 程序交互式地监控系统中的进程，并使用它的“关键统计数据”，如 CPU 活动状态、实际和虚拟内存状态以及负载平均值。此外，最新的 top 可以从 http://ftp.groups.com/pub 下载。

`top` 读取 `/proc` 文件来生成其进程统计数据。这意味着 `top` 以 setuid 进程运行，除非它以 root 身份运行。相反地，允许非 root 用户运行它可能同样危险，因为 `top` 中的任何错误如果由 root 用户执行可能会影响系统。再次，setuid 进程是危险的，你应该评估在这种情况下可访问性与安全性之间的权衡是否值得。
