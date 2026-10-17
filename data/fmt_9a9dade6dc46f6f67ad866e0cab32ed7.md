
# 第 10 章：管理系统

通过 `ps`、`top` 等命令，你可以查看系统上每个应用程序消耗了多少内存。然而，内核本身也有自己的内存来跟踪其资源，这被称为内核内存缓存（kernel slab）。你可以使用 `vmstat` 命令显示内核 slab 内存统计（来自 `/proc/slabinfo`），如下所示：

```
$ vmstat -m | less Page through kernel slab memory cache

Cache Num Size Pages

f_nat:help 2 13 308 13

f_nat:base 0 0 276 14

bridge_fdb_cache 0 0 64 59

extext3_inode_cache 1236 2928 488 8

extext3_kattr 29 156 48 78
```

slab 内存缓存显示了每个缓存名称、该缓存类型的活动对象数量、该缓存类型的可用对象总数、缓存大小（字节）以及每个对象的页数。你可以使用 `slabtop` 以面向屏幕的视图（类似于 `top` 命令）显示内核内存信息：

```
$ slabtop

Active / Total Objects (% used) : 49127 / 70942 (69.2%)

Active / Total Slabs (% used) : 3094 / 3094 (100.0%)

Active / Total Cache (% used) : 101 / 145 (69.7%)

Active / Total Size (% used) : 8830.29K / 12013.73K (73.5%)

Minimum / Average / Maximum Object : 0.01K / 0.17K / 128.00
```

| OBJECT USE OBJ SIZE SLABS OBJ/SLAB CACHE NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 11600 | 4303 | 37% | 0.13K | 400 | 29 | 16000 dentry_cache |
| 2928 | 1246 | 42% | 0.48K | 366 | 8 | 13400 radix_tree_node |
| 4355 | 2535 | 58% | 0.28K | 335 | 13 | | |
| 219 | 219 | 100% | 0.04K | 219 | 1 | 876K slab-4096 |

`slabtop` 每三秒更新一次。默认情况下，slab 缓存按每个缓存中的对象数量（第一列）排序。按下 `c` 键可以按缓存大小排序（如上一个示例所示）。

## 监控 CPU 使用率

CPU 负载过高是系统中需要查找性能问题的另一个明显之处。之前显示的 `vmstat` 命令可以产生与 CPU 使用相关的基本统计数据（用户活动、系统活动、空闲时间、I/O 等待时间和从虚拟机中窃取的时间）。然而，`iostat` 命令（来自 `sys` 包）可以生成更详细的 CPU 利用率报告。

以下是使用 `iostat` 显示 CPU 利用率报告的两个示例：

```
$ iostat -c    CPU stats every 3 seconds (starting apps)

Linux 2.6.21-01394.fc7 (davinci)           08/10/2007

avg-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00      0.00     0.00    99.50

avg-cpu:     %user     %system %iowait     %steal     %idle

           28.71      0.00      5.45    18.32    47.52

avg-cpu:     %user     %system %iowait     %steal     %idle

           98.99      0.00      1.01     0.00     0.00

av-cpu:     %user     %system %iowait     %steal     %idle

           99.50      0.00      0.50     0.00     0.00
```

```
$ iostat -c    CPU stats every 3 seconds (copying files)

Linux 2.6.21-01394.fc7 (davinci)           08/10/2007

avg-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00      0.00     0.00     0.00

avg-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00     24.88    74.63     0.00

avg-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00     10.00    89.50     0.00

av-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00     17.41    82.09     0.00

av-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00     14.65    85.35     0.00
```

第一个 `iostat` 示例从空闲系统开始，然后启动了几个应用程序。你可以看到大部分处理是在用户空间完成的。第二个 `iostat` 示例显示了大文件从一个磁盘复制到另一个磁盘的情况。这表明大部分的时间花费在系统级别（也称为内核空间，在这种情况下是读写磁盘分区）。注意，文件复制会导致较高的 I/O 等待时间（`%iowait`）。

以下是使用 `iostat` 带有时间戳打印 CPU 利用率的示例：

```
$ iostat -c -t    Print timestamp with CPU utilization

Linux 2.6.21-01394.fc7 (davinci)           08/10/2007

Time: 29:28:03

avg-cpu:     %user     %system %iowait     %steal     %idle

           0.50      0.00      0.00     0.00    99.50

$ iostat -c -t    Repeat every 2 seconds for 10 times
```

如果你想知道哪些进程消耗了最多的资源，可以使用 `top` 命令。输入 `top` 然后按 `Shift+p` 按 CPU 使用率排序（默认值）：

```
$ top             Display running processes and sort by CPU usage

Tasks: 120 total,      2 running, 116 sleeping,      0 zombie

Cpu(s): 88.6% us, 6.0% sy, 0.0% ni, 3.3% id, 4.0% wa, 0.0% hi, 0.0% si

Mem: 482992 total, 476884 used, 6108 free

Swap: 5863716 total, 1162552 used, 4697464 free, 529844 cached

| PID | USER | PR | VIRT | RES | S | MEM | TIME+ | COMMAND |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 9648 | | 16 | 309n | 123m | R | 72.6% | 28:55.22 | firefox-bin |

| 552 | | 15 | 762m | 65m | S | 15.6% | 04:27.0 | X |
```
