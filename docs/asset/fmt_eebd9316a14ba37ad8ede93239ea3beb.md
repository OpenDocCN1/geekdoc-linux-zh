
热点进程的默认显示包含有用信息，包括任务运行下的用户名、优先级、`nice`值、请求的内存分配、实际使用、共享内存、进程状态、总可用物理内存的百分比、CPU 时间以及短命令行。在交互式模式下工作时，可以使用 `-f` 关更改这些字段，如图 3.1 所示。

一眼看，显示的列表可以提供潜在问题或瓶颈的指示。你可能会发现某些进程可能在使用过多的内存或 CPU，

# 第 3 章 基础教育

当前字段：`AEHI00TWKNMbcdfgplirsuyvz(X` 为窗口 1:Def

通过字段名切换字段，输入任何其他键返回

```
* PID = 进程 ID
* USER = 用户名
* PR = 优先级
* NI = Nice 值
* VIRT = 虚拟内存 (kb)
* RES = 驻留内存 (kb)
* SHR = 共享内存 (kb)
* S = 进程状态
* CPU = CPU 时间
* TIME = CPU 时间（百分分之一）
* W = 内存使用 (kb)
* PPID = 父进程 ID
* USER = 实际用户
* GID
* GROUP = 组名
* TTY = 类型
* P = SWAP
* L = 使用大小 (kb)
* F = 核心时间
* C = 代码大小 (kb)
* D = 数据大小 (kb)
* uFLT = 缺页
* DIRT = 脏页计数
* YCHAN = 在函数中睡眠
* FLUSH = 页面缓存
* B = 糟糕程度
* oom score (糟糕性评分)
* AD = oom 调整 (2X)
* COMMAND = 命令名/行
```

![](img/68d6731afe4338e918be0906dc327e1c_42_0.png)

标志：

00000001 PF ALIONMANN

图 3 Top 命令字段

> 版权所有 ©-Intel Corporation。保留所有权利。

寻找似乎陷入死循环而没有任何进展、异常时间或其他异常的进程，这些可以进一步指导你的调查。对 `top` 的输出进行光标检查有助于缩小问题范围，然后你可以使用 `ps` 命令对其进行探索。

`top` 命令带有几个实用的开关和快捷键：

- `-b` - 在 `top` 模式运行。
- `d` - 更改刷新延迟（默认为 3 秒）。
- `u` - 显示匹配给定 UID 或用户名的进程。
- `p` - 监控逗号分隔的列表，最多包含 20 个进程；如果你怀疑某些进程是系统问题的罪祸首，这非常有用。
- `r` - 为匹配 ID 的进程重优先级。正值将降低进程优先级。负值可能仅供 root 进程使用，标准用户无法重启属于别人的进程。
- `k` - 杀死匹配 ID 的进程。默认情况下，使用 `SIGTERM`。
- `q` - 退出。

摘要命令也非常有用。它们影响信息的显示方式并帮助你过滤或排序数据。例如，“t”将根据任务状态显示进程，“m”将根据内存使用量以顶部向下的方式显示它们，“I”将切换显示

## 系统状态概况 33

有时，取决于控制台屏幕的大小，可能无法显示所有核心（例如 `cpu0`, `cpu1` 等），并且必须使用单视图。与 `top` 不同，

```
ps -ef
```

> 版权所有 ©Intel Corporation。保留所有权利。

或者，可以使用 BSD 语法：

```
ps aux
```

> 版权所有 ©Intel Corporation。保留所有权利。

显著选项包括：

```
ps -eo pid,tid,class,rtrio,ni,psr,stat,wchan,comm
```

PID TID CLASS RTRIO NI PSR %CPU WCHAN

1 TS 0 19 23 0 Ss

2 TS 0 19 36 0 S

3 TS 0 19 0 0 S

### 第 3 章 基础调查

| PID | MEM | TTY | S | COMMAND |
|---|---|---|---|---|
| 6 | 6 | 99139 | 0 | 0.0 S | stopper_th migration/0 |
| 7 | 7 | 99139 | 0 | 0.0 S | watchdog/0 |
| 8 | 8 | 99139 | 1 | 0.0 S | softer_th migration/1 |
| 10 | 10 | -019 | 1 | 0.0 S | run_ksoftirqd softirqd/1 |
| 12 | 12 | 99139 | 1 | 0.0 S | watchdog/1 |
| 13 | 13 | 99139 | 2 | 0.0 S | stopper_th migration/2 |

输出包含按 PID 排序的进程列表。第二列包含线程 ID，也称为轻量级进程 (`LWP`)。`RTrio` 在这种情况下指的是实时优先级。`NI` 列告诉我们进程的 `nic`，而 `PRI` 列报告动态优先级。`PSR` 是分配给任务的。我们还需要 CPU 使用率和任务状态。`WCHAN` 指进程等待的最后一个内核函数（等待通道），例如，这可以用于调试似乎阻塞或停止的进程。最后，我们有命令。BSD 语法也非常有用。默认视图提供的信息与 UNIX 输出相似但也存在差异。`VSZ` 和 `RSS` 列报告虚拟内存和驻留集合大小，类似于 `top` 命令。`STAT` 列显示每个 PID 的字符状态。可用状态有很多。例如，“s”指的是部分，“N”用于优先级较低的进程（`NI`），“I”意味着进程是多线程，等等。`START` 显示命令启动的时间，如果进程是在去年启动的，则报告年份。命令行，直到打印缓冲区宽度，通常是标准输出。内核线程用方括号标记，它们的内存和 CPU 使用量为零。

```
ps aux
```

USER PID %CPU %MEM VSZ RSS TTY STAT TIME COMMAND

root 1 0.0 0.0 10540 112 7 Ss 2014 6:51 [kthread]

root 2 0.0 0.0 0 0 7 S 2014 0:28 [kthread]

## 系统状态概况 35

| root | 3 | 0.0 | 0.0 | 0 | 0.7 | S | 2014 156:02 [ksoftirqd/0] |
| root | 5 | 0.0 | 0.0 | 0 | 0.7 | S | 2014 0:14 [kworker/u0] |
| root | 6 | 0.0 | 0.0 | 0 | 0.7 | S | 2014 263:50 [migration/0] |
| root | 2161 | 0.3 | 0.0 | 0 | 0.7 | S | 01:01 1:44 [kworker/10:1] |
| igor | 2368 | 0.0 | 0.0 | 4612 2396 | TN | 09:04 0:00 /nfs/process.bin |
| igor | 2787 | 0.0 | 0.0 | 4616 2400 | S | 09:25 0:00 /nfs/process.bin |
| root | 5226 | 0.0 | 0.0 | 0 | 0.7 | S | 2014 15:29 [kworker:28:1] |
| root | 5289 | 0.0 | 0.0 | 4004 184 | 7 | S | 2014 0:00 /sbin/scpid |
| 100 | 5302 | 0.0 | 0.0 | 47944 6396 | Ss | 2014 0:59 /bin/dbus-daemon |

### 第 3 章 基础调查

恰好与环境问题相关。然而，这并不意味着两者之间存在联系，你应该避免根据对日志的粗略观察做出任何草率的假设。

你的调查流程应该是数据驱动的。基于初始数据假设一个理论，扩展检查以创建理解的更多维度，提出解决方案，然后测试你的想法是否正确。这意味着你应该在对要查看什么有确定的想法之后再去查看日志。让我们检查两部分日志。

```
Sep 22:28:21 test01 automount[3619]: attempting to mount /nfs/disks/checks

Sep 22:28:21 test01 automount[3619]: attempting to mount /nfs/disks/sh

Sep 22:28:21 test01 automount[3619]: lookup(program): lookup for sh failed

Sep 22:28:21 test01 automount[3619]: failed to mount /nfs/disks/sh

Sep 22:28:21 test01 automount[3619]: mounted /nfs/disks/checks
```
