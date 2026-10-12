
| 1 | | | 43.1% | Tasks: 40, 29 thr |
| 2 | | | 33.1% | Load-average: 0.14 0.25 0.15 |
| Mem:| | | | 577/3953MB | Uptime: 00:04:31 |
| Swp:| | | | 0/010MB | |
| PID USER PID VIRT RES CPU MEM% TIME Command |
| 2171 ubuntu 20 0406 12240 6420 51.1 0.3 01:04:17 python -m Simple |
| 2172 ubuntu 20 02574 15012 13952 0.8 0.4 01:01:26 /usr/bin/docker |
| 918 root 20 0 2568 00 2.3 0.1 00:00:17 htop |
| 1229 mysqld 20 0 110M 4628 13744 0.0 11.7 01:03/57 /usr/bin/mysqld |

虽然 `top` 用于获取所有运行进程的概览，但 `pidstat` 命令可监控 MySQL（或任何其他任务名称）的 CPU 使用率：

```
$ pidstat -C mysql
```

```
ubuntu@ubuntu$: pidstat -C mysql
Linux 3.16.0-30-generic (ubuntu) 01/16/2016 _x86_64_ (2 CPU)
08:39:30 PM UID PID %system %guest %CPU CPU Command
08:39:30 PM 10S 8458 0.00 0.00 0.00 0.00 1 mysql
ubuntu@ubuntu:-$
```

通过 `pidstat`，您还可以通过进程 ID（PID）查询特定进程的统计信息，如下：

```
$ pidstat -p 1134
```

# 性能监控

5. 另一个有命令是 `vmstat`。它主要用于获取虚拟内存使用的详细信息，但也包含了类似于 `top` 命令的 CPU 指标：

```
ubuntu@ubuntu:~$ vmstat 1
proc    memory-------------swap--------system----cpu
  r  swpd free buff cache si so bo in  id  out cs us id wa st
  1   0 2933068 41284 46600   0   0  6  5 27 33  1  0 98  0
  0   0 2933068 41284 46600   0   0  0  0 40 77  1  0 99  0
  0   0 2933068 41284 46600   0   0  0  0 25  5  0 100
```

6. 另一个用于处理器统计的命令是 `mpstat`。它返回的统计信息类似于 `top` 或 `vmstat`，但局限于 CPU 统计。`mpstat` 不是 Ubuntu 默认安装包的一部分；你需要安装 `sysstat` 包才能使用 `mpstat` 命令：

```
$ sudo apt-get install sysstat -y
```

7. 默认情况下，`mpstat` 返回所有 CPU 的平均统计数据。可以使用标记 `-p` 来获取特定 CPU 的详细信息。以下命令将显示处理器 (0) 和处理器 (1) 的统计信息，并每 3 秒更新一次：

```
ubuntu@ubuntu:~$ mpstat -P 0 1
Linux 3.16.0-30-generic (ubuntu)  01/16/2016  x86_64  (2 CPU)
08:50:32 CPU     %user     %nice     %sys %iowait  %irq  %soft %steal %guest
             %idle
08:50:32 PM  0     0.36     0.00     0.36     0.00  0.00  0.55  0.00  0.00
             98.64
08:50:32 PM  1     2.24     0.00     0.22     0.09  0.00  0.00  0.00  0.00
             97.45
```

8. 另一个命令 `sar` (系统活动报告器) 提供了系统性能的详细信息。

以下命令将提取 `sar` 记录的 CPU 指标。标记 `-u` 将详细信息限制为仅 CPU，`-P` 将显示所有可用 CPU 的数据。默认情况下，`sar` 命令将输出限制为仅 CPU 详细信息：

```
$ sar -u -P ALL
```

```
ubuntu@ubuntu:~$ sar -u -P ALL
Linux 3.16.0-generic (ubuntu)          01/23/2016           x86_64_               (2 CPU)
08:34:56 AM    LINUX RESTART
08:35:01 AM    CPU     %user  %nice  %system %iowait  %steal  %idle
08:45:01 AM    all     2.38    0       6.39    1.20    0.00    89.42
08:45:01 AM    all     1.52    0       10.16   1.25    0.00    87.17
08:45:01 AM    all     3.38    0       4.00    1.07    0.00    91.55
Average        CPU     %user  %nice  %system %iowait  %steal  %idle
Average        all     2.38    0       6.99    1.20    0.00    89.42
Average        0       1.52    0      10.16   1.25    0.00    87.17
Average        1       3.38    0       4.00    1.07    0.00    91.55
```

9. 要使用 `sar` 获取当前利用率，请指定间隔，以及可选的计数值。以下命令将以每 2 秒为间隔输出 5 条记录：

```
$ ubuntu@ubuntu:~$ sar -u 2 5
Linux 3.16.0-generic (ubuntu)          01/23/2016           x86_64_               (2 CPU)
08:49:30 AM    CPU     %user  %nice  %system %iowait  %steal  %idle
08:49:32 AM    all     0.25    0.00   0.00    0.00    0.00    99.75
08:49:34 AM    all     0.00    0.00   0.25    0.00    0.00    99.75
08:49:36 AM    all     0.00    0.00   0.25    0.00    0.00    99.75
08:49:38 AM    all     0.00    0.00   0.25    0.00    0.00    100.00
08:49:40 AM    all     0.25    0.00   0.25    0.00    0.00    99.50
Average        all     0.10    0.00   0.15    0.00    0.00    99.75
```

10. 所有这些数据都可以存储由 `(-o)` 指定的文件。以下命令将在当前目录创建一个名为 `sarReport` 的文件，其中包含 CPU 利用率的详细信息：

```
$ sar -u -o sarReport 3 5
```

其他选项包括 `-u` 限制到 CPU，`-A` 获取全范围计数器，以及更多。检查 `man sar` 手册以获取特定计数器的标记。

# CPU 监控

### 工作原理...

本教程涵盖了著名的 CPU 监控工具，从最常用的命令 `top` 开始。

在前面的示例中，我们使用 `sar` 来获取系统当前状态的快速摘要。默认情况下，`top` 显示 CPU 使用率，它列在 `top` 输出的第三行。如果有多个 CPU，其使用率将合并显示在一个列中。当你按下 `1` 时，`top` 会列出所有 CPU。以下截图显示虚拟机上有两个 CPU：
