
通过读取`/proc/version`文件的内容也可以获取内核版本信息。

`xview` 你可以使用 `xview` 实用程序显示若干系统参数的状态，如 CPU 使用率、平均负载、内存使用、交换空间使用、网络使用、中断和串口端口状态。

要使用 `xview`，你必须首先安装 `xview` 包。要启动 `xview`，打开终端窗口并输入 `xview`。将显示一个类似下面的窗口：

# 图 5-18 xosview

![](img/1402b35af63db85442c13e1f1f80f4_535_0.png) 由 Novel, Inc. 提供

每个进程状态都显示为被分为颜色标记区域的水平条。每个区域代表正用于特定用途的资源百分比。当你查看完信息后，可以通过关闭窗口退出。

## vmstat

使用 `vmstat` 可以获取虚拟内存统计报告。如果你在命令后添加一个数字，这定义了获取更新信息的秒间隔。如果你添加第二个数字，则定义了收集和显示信息的间隔次数。

命令的简单示例所示：

```
$ vmstat --swap--io--system----cpu-----

procs ----------memory---- free buff cache si bo bo in ce us sy id wa st

r 1 0 swpd 0 333232 35324 327692 0 0 8 5 18 55 0 0 99 0 0
```

命令的输出组织成几个部分。第一部分（`procs`）包含有关进程的信息。名为 `r` 的列包含等待运行时间的进程数。第二列 `b` 包含处于不可中断睡眠状态的进程数。

第二部分（`memory`）包含有关内存使用的信息。第一列（`swpd`）显示使用的虚拟内存量。下一列（`free`）包含空闲内存量。第三列（`buff`）显示缓冲区大小。

作为缓冲区使用的内存量以及第四列（`cache`）显示了作为缓存使用的内存量。

第三部分（`swap`）提供了有关交换的信息：交换入（`si`）和交换出（`so`）。

下一部分（`io`）显示了磁盘上的输入/输出操作：`bi`（块）显示每秒读取的块数，`bo`（块）显示每秒写入的块数。

最后两个部分（`system` 和 `cpu`）显示有关系统的信息。

接下来的示例展示了执行某些 I/O 密集型任务时信息是如何变化的。在这种情况下，运行了 `find` 命令（为了提高可读性，缩短了行）：

```
dal: --vstat 2 #

procs          --memory--------swap----io----system-----

r b free buff cache si bo bo in cs

0 0 03329836 35392 327736 0 0 8 15 58

0 1 03318854 35972 338268 0 0 298 0 154 675

0 1 03315360 38420 338752 0 0 1922 912 620 947

1 0 03310752 42272 339316 0 0 1244 566 295

1 0 03306536 45864 339936 0 1 1796 579 2447

0 1 03302352 46848 341268 0 1 950 972 311 852

0 1 03302284 51356 340818 0 0 556 184 999
```

如果你对磁盘相关信息感兴趣，请使用 `-d` 选项：

```
dal: --vstat -d

disk: ----------reads--------------------------writes-

--IO------------------------------------

total merged sectors ms total merged sectors ms

cur sec

sda0 268853 7059 678616 160372 15852 36726 429984 148200

0 140

sda1 34 1154 1874 612 0 0 0 0 0

sda2 18 133 698 400 0 0 0 0 0

sda3 26577 5752 67540 157772 15852 36726 429984 148200

0 139

sr0 0 0 0 0 0 0 0 0

loop0 0 0 0 0 0 0 0 0

loop1 0 0 0 0 0 0 0 0

loop2 0 0 0 0 0 0 0 0

loop3 0 0 0 0 0 0 0 0

loop4 0 0 0 0 0 0 0 0

loop5 0 0 0 0 0 0 0 0

loop6 0 0 0 0 0 0 0 0

loop7 0 0 0 0 0 0 0 0
```

使用 `-s` 选项显示不同内存相关信息的摘要：

# sar

```
dal:~ # vmstat -s

3898824 total memory

615162 used memory

315552 active memory

227616 inactive memory

3283212 free memory

66144 swap cache

342968 total swap

0 used swap

1044216 free swap

17122 non-user cpu ticks

11833 nice-user cpu ticks

3802 system cpu ticks

378673 idle cpu ticks

13854 IO-wait cpu ticks

16 IRQ cpu ticks

33 softirq cpu ticks

0 stolen cpu ticks

339408 pages paged in

210856 pages paged out

0 pages swapped in

0 pages swapped out

697276 interrupts

2107864 CPU context switches

1250231620 boot time

6319 forks
```

自 `sysstat` 包，安装了两个监控工具：`sar` 和 `sadc`。这两个工具都通过 `/etc/cron.d/sysstat` 中的 `cron` 任务调度。这是一个指向 `/etc/sysstat/sysstat.cron` 的符号链接，该文件在 `/etc/init.d/sysstat` 脚本启动时创建。通过 `cron` 会启动两个脚本：

- `/usr/lib/sa/sa1`。此脚本每 10 分钟运行一次 `sad`（系统活动数据收集器）。收集的信息追加到文件 `/var/log/sa/sad` 中，其中 `sad` 代表当天（例如 `/var/log/sa/sa7`）。数据以二进制格式存储。

- `/usr/lib/sa/sa2`。此脚本每 6 小钟运行一次 `sar`（系统活动报告）。它将 `sad` 字段转换为人类可读的格式并存储在 `/var/log/sa/sar` 中。当然，`sar` 也可以从命令行交互式运行。对于所有选项，如果交互式运行 `sar`，通常需要提供间隔和次数。以下示例显示了 CPU 利用率：

## 使用监控工具

```
dal:~ # sar -u 2
Linux 2.6.27.19-5e (dal)          08/17/09          686
12:56:41 CPU    %user %nice %system    iowait  %steal %idle
12:56:43 all     0.49     0.00    2.44    46.21   0.00 50.86
12:56:45 all     0.73     0.00    1.95    47.20   0.00 50.12
12:56:47 all     0.74     0.00    1.96    46.81   0.00 50.49
12:56:49 all     1.44     0.00    2.39    44.98   0.00 51.20
12:56:51 all     0.25     0.00    0.76    49.87   0.00 49.11
Average:              all     0.73     0.00    1.91    46.99   0.00 50.37
```

监控磁盘 I/O 显示如下：
