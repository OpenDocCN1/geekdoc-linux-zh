
```
agonzalez@ubuntu:~$ sleep 30 &
[1] 26717
agonzalez@ubuntu:~$ sleep 60 &
[2] 26718
agonzalez@ubuntu:~$ jobs
[1]- Running sleep 30 &
[2]+ Running sleep 60 &
```

图 5.63：后台运行命令的示例以及 `jobs` 命令的输出示例。

前台进程可以通过先停止它（`Ctrl-Z`）然后运行命令 `bg` 发送到后台，如图 5.64 所示：

```
agonzalez@ubuntu:~$ sleep 120
Z
[1]+ Stopped sleep 120
agonzalez@ubuntu:~$ jobs
[1]+ Stopped sleep 120
agonzalez@ubuntu:~$ bg
[1]+ sleep 120 &
agonzalez@ubuntu:~$ jobs
[1]+ Running sleep 120 &
```

图 5.64：后台和前台进程的示例。

可以使用 `fg` 命令将进程从后台移动到前台。可以通过添加参数 `%N` 指定 ID（`bg` 命令也是如此）；图 5.65 显示了一个示例：

```
agonzalez@ubuntu:~$ sleep 30 &
[1] 26721
agonzalez@ubuntu:~$ sleep 60 &
[2] 26722
agonzalez@ubuntu:~$ fg %1
sleep 30
```

图 5.65：使用 `fg` 命令的示例。

当用户会话关闭时，后台进程会被杀死。为了避免这种行为并保持进程继续运行，Linux 提供了两个选项：

-   运行名为 `disown` 的内置命令，将后台运行的进程与当前用户关联。

-   使用应用程序 `nohup` 执行后台进程，例如：`nohup myapplication &`。

## 进程优先级操作

Linux 使用调度器来分配资源以执行系统任务。某些进程需要比其他进程更高的优先级，特别是那些访问系统资源或 Linux 内核的进程。

-   实时进程：这些进程能够在时间内运行而不被任何其他进程中断。这些进程的系统优先级范围在 1（低）到 99（高）之间。

-   普通进程：这些进程可以被需要访问系统资源的更高优先级的进程所中断。这些进程有一个 `nice` 值，表示获取资源的优先级。这些值的范围从 -20（高优先级）到 +19（低优先级）。普通进程的默认 `nice` 值为 0。负值（高优先级）只能由管理员指定。

`ps` 命令和 `top` 命令的 `-l` 选项显示运行进程的优先级和 `nice` 值。本节将重点介绍如何更改进程的 `nice` 值。

图 5.6 显示了带有选项 `-l` 的 `ps` 命令显示优先级和 `nice` 值的输出示例：

```
agonzalez@ubuntu:-$ ps -l -q $(pidof top)
F S UID PID PPID PRI NI ADDR SZ WCHAN TTY TIME CMD
0 S 26699 26628 0 14:57 pts/1 00:00:02 top
```

# 第 6 章

## 监控系统资源

## 引言

本章介绍了如何在 Linux 系统中监控系统资源。它将介绍现代系统中 CPU 和内存的工作原理，以及用于检查状态的常用工具，以便在出现问题或过载时进行故障排除。

其他需要监控以避免应用程序停机的重要资源还有磁盘使用情况和可用空间。本文将描述不同的工具来检查当前状态并检测磁盘的物理状态。

网络监控已成为 Linux 系统中最重要的任务之一，特别是当系统中为虚拟机和容器提供连接性而引入复杂网络之后。

本章的最后一部分重点关注磁盘配额和资源限制，帮助在普通用户访问系统时保护系统，防止资源耗尽。

## 结构

在本章中，我们将讨论以下主题：

- 监控 CPU 资源
- 监控内存资源
- 监控磁盘使用情况和可用空间
- 监控网络资源
- 配额与限制

## 监控 CPU 资源

中央处理器（CPU），即处理器，执行从系统接收的指令。在现代系统中，有三个重要的概念需要理解，以便监控并解释从工具接收到的数据：

- CPU 插槽 (CPU Socket)：计算机主板上用于安装 CPU 芯片的插座。
- CPU 核心 (Core)：读取和执行指令的独立处理单元。在现代系统中，一个 CPU 包含多个核心。
- CPU 线程 (Thread)：线程是操作系统指令的队列。现代系统支持超线程，从而允许两个线程。

例如，如果一个系统有两个插槽，每个 CPU 有四个核心，并且启用了超线程，那么它将有 8 个可用核心和 16 个线程。它能够每个周期运行 8 条操作系统指令，但每个周期可以拥有多达 16 个任务的队列。

物理服务器的一个高级概念是非均匀内存访问（NUMA）。这种架构相对于处理器将内存划分为本地内存和远程内存。CPU 访问分配的本地内存的性能优于通过互连访问远程内存。图 6.1 显示了一个具有两个两个 NUMA 节点、一个插槽和四个核心的节点表示：

![](img/bcd1b6709d1a6bc46b09b8587284794e_180_0.png)

图 6.1：标准 Linux 文件系统层次结构。boost: org

## 获取 CPU 信息

第 3 章《使用命令行界面》中描述的命令显示了与 CPU 插槽、核心、线程和 NUMA 相关的重要信息。图 6.2 显示了一个具有两个 CPU 插槽且每个插槽八个内核节点。

```
[root@server ~]# lscpu | grep --color=never -E "^(CPU|Thread|Core|Socket|NUMA)"
CPU(s):
  32
Thread(s) per core: 2
Core(s) per socket: 8
Socket(s):
  2
NUMA node(s):
  2
NUMA node0 CPU(s): 0-7,16-23
NUMA node1 CPU(s): 8-15,24-31
```

图 6.2：使用 `lscpu` 命令获取 CPU 信息。

`hwloc` 包中的 `lstopo-no-graphics` 部分提供了 NUMA 架构以及 CPU 与本地内存之间关系的极佳可视化效果。图 6.3 展示了与图 6.2 相同服务器的该命令输出示例。

![](img/bcd1b6709d1a6bc46b09b8587284794e_181_0.png)

图 6.3：`lstopo-no-graphics` 命令的输出示例。

`/proc/cpuinfo` 文件包含所有处理器（核心/线程）的列表，并带有每个处理器的详细信息。图 6.4 显示了使用 `grep`、`sort` 和 `uniq` 创建报告以统计每个插槽中有多少个 CPU 的示例：

```
[root@server ~#] grep "physical id" /proc/cpuinfo | sort|uniq -c
  16 physical id             0
  16 physical id             1
```

图 6.4：从文件 `/proc/cpuinfo` 获取信息

获取处理器信息的其他示例命令如下：

- `lshw -class processor` (或 `lshw -class processor -short`)
- `dmidecode -t Processor`
- `nproc` (仅显示处理器数量)
- `hwinfo --cpu --cpu`

## 理解系统负载和平均负载

系统负载是衡量计算机系统执行计算工作量的指标。平均负载代表一段时间内的系统负载。负载为 140% 的处理器表示其运行过载了 40%，正如负载为 30% 的处理器在观测期间内空闲占了 70% 的时间一样。CPU 负载用小数表示，例如 1.40 表示 140%，0.30 表示 30%。

在 Linux 中理解 CPU 负载的一个常见类比是与流量有关。单核 CPU 就像道路上的单条车道。拥有更多的核心和 CPU 就像拥有更多的车道，这样负载就可以舒适地分布在它们之间。这如图 6.5 所示：

![](img/bcd1b6709d1a6bc46b09b8587284794e_182_0.png)

图 6.5：与处理器、负载和流量的类比

拥有多个可用 CPU，任务分布在不同的 CPU 之间，而负载与 CPU 的数量有关。系统负载为 3.00 表示使用了 66.7% 的可用资源。

## uptime 命令和 /etc/loadavg 文件

第 3 章《使用命令行界面》中描述的 `uptime` 命令用于查看系统运行了多久，提供一个简单的概述。`uptime` 显示 CPU 负载。Linux 系统的平均负载代表 1 分钟、5 分钟和 15 分钟。图 6.6 说明过去 1 分钟的平均值为 0.13，5 分钟为 0.07，15 分钟为 0.05：

```
[root@server ~]# uptime
16:44:42 up 73 days, 10:00, 2 users,  load average: 0.13, 0.07, 0.05
```
