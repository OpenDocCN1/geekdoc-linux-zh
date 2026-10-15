
| | %usr | %sys | %idle | %read/s | %cache/s | %writ/s | %pread/s | %pwrit/s | %busy | avque | blks/s | avwait |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:30 | 32 | 68 | 0 | | | | | | | | |
| 07:48:31 | 0 | 0 | 100 | | | | | | | | | |
| 07:48:30 | | | | | | | | | | | | |
| 07:48:31 | | | | | | | | | | | | |
| Average | | | | | | | | | | | | |

| | rawch/s | canch/s | outch/s | rcvin/s | xtmin/s | mdmin/s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 0 | 0 | 147 | | | |
| Average | 0 | 147 | | | | |

| | scall/s | sread/s | swit/s | fork/s | rchar/s | wchar/s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 2637 | 0 | 95 | 15.79 | 15.79 | 0 |
| Average | 0 | 95 | 15.79 | 15.79 | 0 |

| | swpin/s | bswin/s | swot/s | bswot/s | pwsch/s |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 0.0 | 0.0 | 0.0 | 0.0 | 0 |
| Average | 0.0 | 0.0 | 0.0 | 0.0 | 0 |

| | iget/s | name/s | dirbk/s |
| :--- | :--- | :--- | :--- |
| 07:48:31 | 0 | 195 | 121 |
| Average | 0 | 195 | 121 |

| | runq-sz | runploc | swpq-sz | swploc |
| :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | | 2.0 | 526 |
| Average | | 2.0 | 526 |

| | proc-sz | inod-sz | file-s | lock-s |
| :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 45986 | 0 | 973/4508 | 0 |
| Average | 357 | 0 | 357/357 | 0 |

| | msg/s | sema/s |
| :--- | :--- | :--- |
| 07:48:31 | 0.00 | 0.00 |
| Average | 0.00 | 0.00 |

| | atch/s | pgin/s | pgin/s | pflt/s | vflt/s | lock/s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 0.00 | 0.00 | 0.00 | 505.26 | 1036.84 | 0.00 |
| Average | 0.00 | 0.00 | 0.00 | 505.26 | 1036.84 | 0.00 |

| | pgout/s | pgout/s | pgfree/s | pgscan/s | ufs_ip |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 07:48:31 | 0.00 | 0.00 | 0.00 | 0.00 |
| Average | 0.00 | 0.00 | 0.00 | 0.00 |

| | freeswap | |
| :--- | :--- | :--- |
| 07:48:31 | 15084 | 122421 |
| Average | 15084 | 122421 |

| | sml_mem_alloc | lg_mem alloc_fail | ovsz_alloc_fail |
| :--- | :--- | :--- | :--- |
| 07:48:31 | 2617344 | 1874368 | 0 | 1719092 | 1094546 | 0 |
| Average | 186953 | 133883 | 0 | 1227922 | 781815 | 0 |

## 更高级的图形化性能工具

命令行是 UNIX 生活的一部分。UNIX 诞生于命令行，并且仍然主要基于命令行。虽然在执行命令时需要了解很多知识，特别是涉及到系统性能时，通过我刚刚涵盖的许多命令可以进行深入挖掘。

大多数 UNIX 变体都提供图形化性能工具。某些系统自带基础性能工具，但如果你想进行高级性能分析，通常会使用高级性能工具。我们将在接下来的章节中快速查看几个性能工具。

图 11-1 显示了本章许多示例使用的 Red Hat Linux 系统自带的三个性能工具：

### 系统监控 (htop) 窗口，带有条形图显示 CPU、MEM、SW 和 LA、单个进程信息以及有用数据。

![](img/6969df54e516231f8e64fd177ac127_775_0.png)

- 显示负载平均值的 top 窗口。
- 每个状态的进程数量。
- 进程状态的时间百分比。
- 单个进程相关的信息。
- 以及其他有用数据。
- 显示 CPU0 和 CPU1 利用率 100% 的 os 窗口。

图 11 Red Hat Linux 性能工具截图

图中显示的三个性能工具分别是右下角的 `xview`、屏幕顶部的系统监控（System Monitor）以及左下角的 `top`。系统监控在屏幕顶部提供条形图，指示 CPU、内存、交换分区和局域网的使用情况。随后会为系统上的每个进程提供表格数据。系统监控是 `top` 的图形化版本，我通过命令 `grep for graphical top` 调用的。`xview` 是一个小型负载计，可以持续运行，并在右下窗口显示系统活动的的条形图。这是 X Windows 操作系统的查看程序，因此名为 `xview`。在图中你可以清楚地看到条形图，因为它是一个基于颜色的应用程序，而书是黑白打印的。不过，条形图在计算机屏幕上是清晰的。UNIX 系统上最后也是最常用的工具是运行在左下角 `xterm` 中的字符版本 `top`。`top` 存在于许多 UNIX 变体中并提供了许多有用的系统信息。

显示的有用 `top` 系统数据包括：

- 最后 1、5、15 分钟的负载平均值。
- 现有进程数以及每个状态的进程数。
- 系统中每个处理器处于各种处理器状态的时间百分比。

这些信息也包含在系统监控窗口底部（被 `top` 和 `xview` 窗口覆盖）。

- PID - 进程 ID 号。
- USER - 进程所有者的名称。
- PRI - 进程的当前优先级。
- NI - Nice 值，范围从 -20 到 +20。
- SIZE - 进程的总大小（单位：千字节）。
- RSS - 进程的驻留内存大小（单位：千字节）。
- STATE - 进程的当前状态。
- TIME - 进程消耗的系统和 CPU 秒数。
- %CPU - CPU 使用率百分比。
- %MEM - 内存使用率百分比。
- COMMAND - 当前正在运行的命令进程名称。

与我们涵盖的大多数命令一样，`top` 在不同的 UNIX 变体之间有所不同。你可能会在不同的 UNIX 变体上看到某些不同的字段。当我坐在任何 UNIX 系统前时，我通常有信心运行 `top` 并快速看到系统的运行情况。大多数版本的 `top` 运行都是基于字符的应用程序，因此你甚至不需要图形终端即可运行它们。在本示例中，我在 X 终端内以字符模式运行了 `top`。

本示例使用的系统有两个 CPU。如果你仔细查看 `xosview` 窗口，你会发现 CPU0 和 CPU1 的使用率均为 100%。获取此截图时，我正在该系统上编译 Linux 内核，这消耗了系统在短时间的 CPU 资源。

![](img/6969df54e516231f8e64fd1177ac1127_777_0.png)

# HP GlancePlus/UX

系统短时间的 CPU 资源。你可以从 `top` 和系统监视器窗口中看到，用于编译内核的 `ecl` 程序正在消耗系统中大量的 CPU 资源。

图 11-1 展示了不同的工具如何帮助查看系统资源的消耗。`xsview` 提供了系统资源消耗情况的快速参考和图形概述。然后可以使用 `top` 和系统监视器确定消耗最多系统资源的特定进程。

![](img/6969df54e516231f8e64fd1177ac1127_778_0.png)

# HP GlancePlus/UX

使用 UNIX 命令更好地了解系统正在做什么需要你做大量工作。在第一种情况下，发布 UNIX 命令可以让你获得优势，即获取关于系统这一秒发生发生的数据。遗憾的是，你并不总是能发布额外的命令来更深入地探测你感兴趣的区域（例如某个进程）。

现在我将描述另一种技术——一种可以帮助实时获取有用信息、允许你调查特定进程且不会让你埋没在报告中的工具。该工具是 HP GlancePlus/UX (GlancePlus)。该工具运行在多个 UNIX 变体上，包括 Solaris、HP-UX 和 AIX。

GlancePlus 可以在字符模式或图形模式下运行。我选择使用字符版本的 GlancePlus，因为它可以在任何显示器（无论是图形还是字符）上运行，而且 Motif 版本的 GlancePlus 使用的许多颜色在书中显示效果不好。使用字符模式时，我的示例在书中的显示会清晰得多。我建议你尝试两个版本的 GlancePlus，看看你更喜欢哪一个。

示例使用的系统有 8 个处理器、4 GB 内存，以及连接到上面大量的 EMC Symmetrix 磁盘。

图 11-2 显示了 Glance-Plus 的几个交互式屏幕之一。这一个是进程列表（Process List）屏幕，也称为全局（Global）屏幕。这是启动 GlancePlus 时的默认屏幕。

图 11-2 所示屏幕有两个特征值得立即注意：

- 屏幕顶部的四个直方图提供了你的 CPU、磁盘、内存和交换分区利用率的图形化表示，这种格式比列数字更易理解。
- “进程摘要”（Process Summary）具有与 `ps -ef` 相似的列，许多系统管理员对此非常熟悉且习惯。然而，GlancePlus 额外提供了额外功能，可以通过指定阈值来过滤掉使用资源极少的进程。

使用 GlancePlus，你可以从许多领域仔细观察你的系统，包括：

- 进程列表 (Process List)
- CPU 报告 (CPU Report)
- 内存报告 (Memory Report)
- 交换分区 (Swap Space)
- 磁盘详情 (Disk Detail)
- 局域网详情 (LAN Detail)
- 按系统的 NFS (NFS by System)
- PRM 摘要（进程资源管理器）
- 按文件系统的 I/O (I/O by File System)
- 按磁盘的 I/O (I/O by Disk)
- 按逻辑卷的 I/O (I/O by Logical Volume)

![](img/6969df54e516231f8e64fd1177ac1127_779_0.png)

# HP GlancePlus/UX

- 系统表 (System Tables)

图 11-2 是一张 GlancePlus 截图。

![](img/6969df54e516231f8e64fd1177ac1127_780_0.png)

示例中的图 11-2 GlancePlus/UX 进程列表截图告诉我们你的系统资源处于什么水平，我将从这里开始描述。我在便携电脑上使用终端模拟器显示 GlancePlus。我发现许多系统管理员使用 PC 和终端模拟器来执行 UNIX 管理功能。请记住，此屏幕上的信息可以按你选择的任何间隔进行更新。

运行在你系统上的进程列表（Process List）屏幕底部。由于 UNIX 系统通常有许多进程在运行，你可能希望考虑使用命令为 CPU 利用率设置阈值。例如，如果你设置了百分之五的阈值，只有在间隔内平均 CPU 利用率超过百分之五的进程会被显示。还可以指定其他类型的阈值，例如使用的 RAM 数量（驻留大小 Resident Size）。如果你设置了阈值，只会看到你感兴趣的进程，即那些消耗最多系统资源的进程。

每个符合你定义的阈值要求的活动进程都有一行。显示的进程可能多于页。屏幕右下角的消息指示你当前处于哪一页。你可以使用 'f' 向前滚动查看下一页，使用 'b' 向后滚动。通常只有少数进程消耗了你系统的大部分资源，我建议设置阈值使只显示一页进程。GlancePlus 中有一整系列命令。本节最后的图表显示了 GlancePlus 识别的命令。以下是进程标题的简要概述：

- **Process Name**（进程名称）：加载可执行程序使用的名称或缩写。
- **PID**：进程标识符。
- **PPID**：父进程的 PID。
- **Pri**：进程的优先级。数字越小，优先级越高。系统级进程通常运行在 0 到 127 之间。其他进程通常运行在 128 到 255 之间。“Nice”进程是优先级最低的，数字最大。
- **User Name**（用户名）：启动进程的用户名称。
- **CPU Util**（CPU 利用率）：第一个数字是该进程在更新间隔内消耗的 CPU 利用率百分比。注意，对于我们的八处理器系统，最大值为 800%。第二个数字是自调用 GlancePlus 以来该进程消耗的 CPU 利用率百分比。大多数管理员让 GlancePlus 在其系统上持续运行，并设置较低的更新间隔。由于 GlancePlus 使用的系统开销非常小，这样做几乎没有副作用。

### Cum CPU（累积 CPU）
- 进程使用的总 CPU 时间。GlancePlus 使用“midaemon”来收集信息。如果 midaemon 在进程之前启动，你将获得进程使用的累积 CPU 时间的准确测量。

### Disk I/O Rate（磁盘 I/O 速率）
- 第一个数字是上一个更新间隔内每秒平均磁盘 I/O。第二个数字是自 GlancePlus 启动或进程启动以来的平均磁盘 I/O 速率。磁盘 I/O 可以有许多不同的含义。磁盘 I/O 可能意味着首次从磁盘读取数据块并放入 RAM，也可能是完全的分页和交换。某些进程比其他进程需要多多的磁盘 I/O。然而，当此数字很大时，请仔细检查你是否有 RAM。记住，页出（pageout）活动（如禁用和交换）归属于 vhand 进程。

### RSS Size（RSS 大小）
- 进程消耗的 RAM 数量（单位为 KB）。这被称为驻留大小（Resident Size）。与进程相关的位于 RAM 中的内容都包含在此列中，例如进程的数据、栈、文本和共享内存段。这是一个很好的检查条列。由于系统经常被错误地假设为 CPU 密集型，我总是特意查看此列，以识别主应用程序正在使用的 RAM 数量。这通常能揭示很多问题。某些应用程序使用少量的 RAM 但使用大型数据集，这一点在进行 RAM 计算时经常被忽视。此列显示了你的进程当前正在使用的所有 RAM。

### Block On（阻塞于）
- 进程阻塞（无法运行）的原因。如果进程当前处于阻塞状态，你会看到原因。如果进程正在运行，你将看到它上一次阻塞的原因。进程阻塞的原因有很多。在 *Thd Cnt* 之后是进程阻塞的最常见原因列表。

### Thd Cnt（线程计数）
- 当前进程的线程总数。

### Abbreviation Reason for the Blocked Process（阻塞进程缩写原因）
| Abbreviation（缩写） | Reason（原因） |
| :--- | :--- |
| CACHE | 等待缓存缓冲区可用 |
| DISK | 等待磁盘操作完成 |
| INODE | 等待 inode 操作完成 |
| IO | 等待非磁盘 I/O 完成 |
| IPC | 等待共享内存操作完成 |
| LAN | 等待 LAN 操作完成 |
| MESG | 等待消息队列操作完成 |
| NFS | 等待 NFS 请求完成 |
| PIPE | 等待管道数据 |
| PRI | 因为优先级更高的进程正在运行 |
| RFA | 等待远程文件访问（Remote File Access）完成 |
| SEM | 等待信号量可用 |
| SLEEP | 因为进程调用了 sleep 或 wait |
| SOCKT | 等待 socket 操作完成 |
| SYS | 等待系统资源 |
| TERM | 等待终端传输 |
| VM | 等待虚拟内存操作完成 |
| OTHER | 等待 GlancePlus 无法判断的原因 |

### CPU Report Screen Description（CPU 报告屏幕说明）
如果进程列表屏幕显示 CPU 过载，你可能需要参考图 11-3 所示的 CPU 报告屏幕。它可以提供关于 GlancePlus 报告的七种状态的有用信息。

## Chap. 11 Introduction to UNIX Performance Tools（第 11 章 UNIX 性能工具介绍）

![](img/6969df54e516231f8e64fd1177ac1127_787_0.png)

# GlancePlus/UX

## 内存报告界面描述

图 11-5 显示的内存报告界面提供了关于几种类型内存管理事件的信息。统计以计数的形式显示，而不是百分比。您可能希望在系统大部分空闲时查看这些计数，并观察随着系统负载逐渐增加时发生了什么。根据您的经验，发生的瓶颈远多于 CPU 瓶颈，因此您可能会发现这个界面非常有价值。

![](img/6969df54e516231f8e64fd1177ac1127_790_0.png)

| 事件 | 当前计数 | 累计计数 | 当前速率 | 累计速率 | 高速率 |
|---|---|---|---|---|---|
| 缺页 (Page Faults) | 1164 | 776476 | 223.8 | 297.8 | 4226.6 |
| 页入 (Page In) | 2 | 12147 | 0.3 | 4.6 | 102.6 |
| 页出 (Page Out) | 0 | 11 | 0.0 | 0.0 | 0.3 |
| 已支付 KB (KB Paid) | 0kb | 2.2kb | 0.0 | 0.0 | 61.3 |
| 已页出 KB (KB Paged Out) | 0kb | 44kb | 0.0 | 0.0 | 1.5 |
| 激活 (Reactivations) | 0 | 0 | 0.0 | 0.0 | 0.0 |
| 取消 (Deactivations) | 0 | 0 | 0.0 | 0.0 | 0.0 |
| 已去激活 KB (KB Deactivated) | 0kb | 0 | 0.0 | 0.0 | 0.0 |
| 虚拟内存读取 (VM Reads) | 0 | 156 | 0.0 | 0.0 | 3.3 |
| 虚拟内存写入 (VM Writes) | 0 | 11 | 0.0 | 0.0 | 0.3 |

总 VM : 519.9sb 系统内存 : 218.8mb 用户内存 : 724.5mb 物理内存 : 4.00gb
活动 VM : 34.3sb 缓冲/缓存 : 818.7kb 空闲内存 : 2.20gb

图 11-5 HP GlancePlus/UX 内存报告截图

## 第 11 章 UNIX 性能工具简介

每个内存管理事件都显示了以下五项统计数据：

- 当前 (Current)：在最后一个时间间隔内发生事件的次数。如果您更新时间间隔，计数会发生变化，因此您可能希望选择一个您感到舒适的间隔并保持不变。
- 累计 (Cumulative)：自 GlancePlus 启动以来该事件的所有计数总和。
- 当前速率 (Current Rate)：每秒发生的事件次数。
- 累计速率 (Cum Rate)：在累计收集间隔内的平均速率。
- 高速率 (High Rate)：记录的最高速率。

以下是所提供统计数据的各个内存管理事件的简要描述：

- 缺页 (Page Faults)：任何地址转换错误，如回收 (reclaims)、pid 错误等。
- 页入/页出 (Page In/Page Out)：数据页从虚拟内存（磁盘）移动到物理内存（页入），或反之亦然（页出）。
- 已页入 KB (KB Paged In/原文误)：由于缺页而页入的数据量。
- 已页出 KB (KB Paged Out)：页出到磁盘的数据量。
- 激活/取消 (Reactivations/Deactivations)：在内存中交换进程的次数。内存 不足的系统将花费大量时间在 RAM 和内存之间交换进程。如果发生了大量此类交换，您可能会遇到高 CPU 利用率，并看到某些其他统计数据也随之增加。这些可能只是正在交换的症状。

| 属性 | 描述 |
| --- | --- |
| 已激活 KB (KB Reactivated) | 由于之前 RAM 不足导致进程被交换出，重新交换入 RAM 的信息量。 |
| 已去激活 KB (KB Deactivated) | 移动到磁盘时交换出的信息量。 |
| 虚拟内存读取 (VM Reads) | 读取磁盘的虚拟内存总次数。此数字越高，系统访问磁盘越越频繁。 |
| 虚拟内存写入 (VM Writes) | 内存管理 I/O 的总计数。 |

内存界面上还包含以下值：

| 属性 | 描述 |
| --- | --- |
| 总 VM (Total VM) | 所有进程使用的总虚拟内存量。 |
| 活动 VM (Active VM) | 所有活动进程使用的虚拟内存量。 |
| 系统内存 (Sys Mem) | 用于系统的内存量。 |
| 缓冲缓存大小 (Buf Cache Size) | 缓冲缓存当前的大小。 |
| 用户内存 (User Mem) | 用于用户的内存量。 |
| 空闲内存 (Free Memory) | 当前未分配使用的 RAM 量。 |
| 物理内存 (Phys Memory) | 系统中的总 RAM 容量。 |

此界面提供了大量关于内存子系统如何被使用的信息。您可能希望在系统大部分空闲和重度使用时查看某些统计数据并进行比较。值得记录的一些良好数字是“空闲内存”（以查看在任何情况下您是否有空闲 RAM）和“总 VM”（查看为所有进程分配了多少虚拟内存）。内存 充足的系统将有可用内存；内存 不足的系统将分配大量的虚拟内存。

## 磁盘报告描述

磁盘报告界面出现在图 11-5 中。磁盘报告界面提供了关于几种类型内存管理事件的信息。统计以计数的形式显示，而不是百分比。您可能希望在系统大部分空闲时查看这些计数，并观察随着系统负载逐渐增加时发生了什么。根据您的经验，发生的瓶颈远多于 CPU 瓶颈，因此您可能会发现这个界面非常有价值。

756 第 11 章 UNIX 性能工具介绍

![](img/6969df54e516231f8e64fd1177ac1127_797_0.png)

| | | | | | | |
|---|---|---|---|---|---|---|
| B3692A GlancePlus B.11.011 | 12:21:21 | rp-ux6 9000/800 | 当前 | 平均 | 高峰 |
| CPU利用率 | SU | | | | 3% | 16% | 85% |
| 磁盘利用率 | | | | | 0% | 23% | 93% |
| 内存利用率 | S SU | UB | B | | 43% | 44% | 51% |
| 交换利用率 | | | UR | R | | 36% | 41% | 57% |

- GlancePlus 快捷菜单
- h - 在线帮助 | q - 退出 (或 e) | A - 列表
- g - 进程列表 | d - 磁盘报告 | P - PRM 组列表
- a - CPU 处理器 | i - 文件系统 IO | Y - 全局系统调用
- c - CPU 报告 | u - 按磁盘 IO | F - 进程打开文件
- e - 内存报告 | v - 逻辑卷 | M - 进程内存区域
- t - 系统表 | n - NFS 全局活动 | R - 进程资源
- t - 交换空间 | I - 按接口网络 | W - 进程等待状态
- s - 交换等待 | K - 磁盘全局 | L - 进程系统调用
- g - 全局等待 | T - 进程列表 | E - 进程 DCE
- g - 全局线程 | U - 事务跟踪 | D - 进程操作
- g - 线程资源 | H - 告警历史 | Y - 调整进程优先级
- t - 线程等待 | s - 选择进程
- s - 选择磁盘/NFS/应用/事务/线程

| 输入命令或功能键：第 1 页，共 2 页 |
| 命令 | 重置 | 调整 | 下一个 | 进程 | 调用 | 刷新 |
|---|---|---|---|---|---|---|
| 列表 | 到零 | 打印间隔 | 键值阈值 | Shell | 屏幕 |
| 702,1 | 通过 TELNET 访问 HP7002-192.6.16 | 输入 | 插入 | 数字大写锁定 | 停止 |

图 11-7 HP GlancePlus/UX 命令列表屏幕 1

GlancePlus/UX

| | | | | 当前 平均 高峰 |
|---|---|---|---|---|---|---|---|
| B3692A GlancePlus 8.11.01 | | 12:22:07 | rp-ux8 9000/800 | | 4% | 16% | 85% |
| CPU利用率 | SU | | | | 1% | 22% | 93% |
| 磁盘利用率 | F | UB | | | 43% | 44% | 51% |
| 内存利用率 | S SU | | | | 38% | 41% | 57% |
| 交换利用率 | U | UR | B | | | | | |

rp-ux8 - 反映 1

![](img/6969df54e516231f8e64fd1177ac1127_798_0.png)

GlancePlus 控制键菜单

- 命令菜单 b - 向后翻页 (或 -) < - 显示上一页
- 调用 Shell f - 向翻页 (或 +, 空格) > - 显示下一个逻辑屏幕
- 在线帮助 q - 退出 (或 e) z - 将统计数据重零
- 打印切换 r - 刷新屏幕 (或 L) <cr> - 更新当前屏幕
- 调整间隔 o - 进程阈值选项

| 命令 | 重置 | 打印 | 调整 | 下一个 | 进程 | 调用 | 刷新 |
|---|---|---|---|---|---|---|---|
| 列表 | 到零 | 切换 | 间隔 | 键值 | 阈值 | Shell | 屏幕 |
| 701.1 | 通过 TELNET 访问 HP70092-192.6.16 | | | | 输入 | 数字 | 大写 | 停止 |

第 2 页，共 2 页

图 11-8 GlancePlus/UX 命令列表屏幕 2

## 使用 VantagePoint Performance Agent 识别瓶颈

VantagePoint Performance Agent 允许您查看许多与系统性能相关的指标，帮助您识别系统瓶颈颈。您可以使用 GlancePlus 的图形版本（称为 `gpm`）来指定想要跟踪的指标。然后您可以在 `gpm` 界面中查看它们并以多种不同的方式进行排序。

以下是系统中可能遇到的最主要的瓶颈类型以及与每种瓶颈相关的指标。这些信息由惠普性能专家 Doug Grumman 和 Stephen Ciullo 提供。

### 1. 使用 VantagePoint Performance Agent 的 CPU 瓶颈：
- 全局 CPU 利用率持续偏高，满足 `GBL_CPU_TOTAL_UTIL>90%` 且符合下一项。
- 由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE>3` 表明存在显著的*运行队列*或*平均负载*。
- 查找因优先级被阻塞的进程，`PROC_STOP_REASON=PRI`。

### 2. 使用 VantagePoint Performance Agent 的系统 CPU 瓶颈（与1相同，但增加了第一项）：
- 大部分 CPU 时间消耗在内核模式，满足 `GBL_CPU_SYS_MODE>`
- 全局 CPU 利用率持续偏高，满足 `GBL_CPU_TOTAL_UTIL>90%` 且符合下一项。
- 由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE>3` 表明存在显著的运行队列或平均负载。
- 查找因优先级被阻塞的进程，`PROC_STOP_REASON=PRI`。

### 3. 上下文上下文切换（与2相同，但增加了第一项）：
- 大部分 CPU 时间消耗在内核模式，满足 `GBL_CPU_SYS_MODE>`
- 全局 CPU 利用率持续偏高，满足 `GBL_CPU_TOTAL_UTIL>90%` 且符合下一项。
- 由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE>3` 表明存在显著的运行队列或平均负载。
- 查找因优先级被阻塞的进程，`PROC_STOP_REASON=PRI`。

### 4. 使用 VantagePoint Performance Agent 的用户 CPU 瓶颈（与1相同，但增加了第一项）：
- 大部分 CPU 时间消耗在用户模式，满足 `GBL_USER_MODE>`
- 全局 CPU 利用率持续偏高，满足 `GBL_CPU_TOTAL_UTIL>90%` 且符合下一项。
- 由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE>3` 表明存在显著的运行队列或平均负载。
- 查找因优先级被阻塞的进程，`PROC_STOP_REASON=PRI`。

### 5. 使用 VantagePoint Performance Agent 的磁盘瓶颈：
- 至少有一个设备的利用率持续偏高，`BYDSK_UTIL>50%`。
- 队列长度大于零，`BYDSK_QUEUE>0`。
- 因各种原因阻塞 I/O 的进程或线程，`PROC_STOP_REASON=CACHE, IO`。

### 6. 使用 VantagePoint Performance Agent 的缓冲区缓存瓶颈：
- 至少有一个磁盘利用率中等，`BYDSK_UTIL>25`
- 队列长度大于零，`BYDSK_QUEUE>0`。
- 缓冲区缓存命中率低，`GBL_MEM_HIT_PCT<90%`。

### 7. 使用 VantagePoint Performance Agent 的内存瓶颈：
- 内存利用率高，`GBL_MEM_UTIL>95%`。
- 显著的页面交换或任何激活，`GBL_MEM_PAGEOUT_RATE>1` 或 `GBL_MEM_SWAP_RATE>0`。

### 8. 使用 VantagePoint Performance Agent 的网络瓶颈：
- 网络包速率高，`GBL_NET_PACKET_RATE>=average`。注意这取决于配置。
- 存在任何输出队列，`GBL_NET_OUTQUEUE>0`。
- 因网络阻塞的进程或线程数量高于正常，`PROC_STOP_REASON=NFS, LAN, RPC` 或 `SOCKET` `GBL_NETWORK_SUBSYSTEM_QUEUE>average`。

GlancePlus/UX

- 一个 CPU 系统利用率高，而其他 CPU 处于空闲状态，`CPU_INTERRUPT_TIME>30`。
- 使用 `lanadmin` 检查频繁的输出丢弃或过度冲突。

为了识别系统中的问题，必须首先在系统运行良好且没有问题时对其进行表征。如果您的系统在某些方面开始性能下降，可以将运行良好的系统性能数据与存在问题的系统数据进行比较。

VantagePoint Performance Agent 安装在分布式环境中的各个系统中。它在单个系统中收集资源和性能测量数据。Vantage-Point Performance Analyzer/UX 管理控制通常安装在管理系统上，用于分-

运行历史性的 VantagePoint Performance Agent 数据。你还可以设置由 VantagePoint Performance Agent 触发的异常条件警报。例如，如果 VantagePoint Performance Agent 检测到异常条件（如 CPU 利用率超过 90%），它就会产生一条警报消息。这些警报消息将通过 VantagePoint Performance Analyzer/UX 显示。我们将在接下来的示例中使用 VantagePoint Performance Analyzer/UX；然而，实际上有三个 VantagePoint Performance 组件：

- Monitor（监控器）：通过接收 VantagePoint Performance 的警报并显示警报提供警报监控能力。
- Planner（规划器）：通过对 VantagePoint Performance 数据进行外推提供预测能力。
- Analyzer（分析器）：分析来自多个系统的 VantagePoint Performance 数据并显示数据。你可以同时查看多个系统的数据。

在示例中，我们将与单个系统一起工作。我们将获取大约一周内收集的 VantagePoint Performance 数据并显示其中部分。在此示例中，我们不会从多个分布式系统获取数据，在示例中仅使用一台服务器。

HP VantagePoint Performance Agent 会生成包含系统资源消耗信息的日志文件。HP VantagePoint Performance Agent 运行时间越长，在日志文件中记录的数据就越详细。我经常被邀请审查运行不佳的系统以提出系统升级建议。我通常运行 HP VantagePoint Performance Agent 至少一周，以便获得足够长时间的日志信息来获取有用数据。

# HP VantagePoint Performance Agent 和 HP VantagePoint Performance Analyzer/UX

对于某些系统，这段时间是几个月。对于其他负载正常的系统，一周的时间可能足够。

在运行 VantagePoint Performance 一周后，我调用了 VantagePoint Performance Analyzer/UX 来查看一周内系统资源的利用率。我们将查看的图表是 CPU、内存和磁盘。图 11-9 显示了周的全局 CPU 摘要：

![](img/6969df54e516231f8e64fd1177ac1127_804_0.png)

图 11-9 Global CPU Summary

你可以使用 VantagePoint Performance Analyzer/UX 调整此图中各种想象的功能。遗憾的是，书中的颜色丢失了。图中使用的颜色允许您在计算机屏幕上查看图表时辨别参数。总 CPU 利用率始终是图中的最高点，它是系统模式和用户模式利用率之和。

图 11-9 显示了经典的 CPU 利用率，高峰时段反映高 CPU 利用率，非高峰时段反映低 CPU 利用率。然而，在某些方面，此图可能是误导性的。因为每三小时出现一个数据点（因此每 24 小时有八个刻度），你无法获得更短时间窗口内的实际 CPU 利用率视图。例如，我们可以精确地看到早上什么时间 CPU 开始被高强度使用。我们可以看到它在第二个和第三个刻度之间，但这是一个很长的时间段——上午 6:00 到 9:00 之间。在一天结束时也存在同样的粒度不足的问题。我们看到第五和第七个刻度之间 CPU 利用率明显下降，但这并没有给我们提供一个清晰的视图。图 11-10 显示了更短时间窗口内的 CPU 利用率。

![](img/6969df54e516231f8e64fd1177ac1127_805_0.png)

图 11-10 Global CPU Summary - Short Time Period

图 11-10 显示了较短时间窗口内更细粒度的 CPU 利用率。该窗口更细的粒度清楚地显示了全发生的活动峰值。例如，上午 8:30 出现了一个明显的登录峰值。

内存利用率也可以在一周内绘制图表，如图 11-11 所示。

![](img/6969df54e516231f8e64fd1177ac1127_806_0.png)

图 11-11 Global Memory Summary

用户利用率是图表的底线，大致对应于之前显示的 CPU 利用率。用户内存利用率在非高峰时段较低，在高峰时段较高。

系统内存利用率是图表的中间线，它在整个周内保持得相当稳定。

总内存利用率始终是图表的顶线，它是系统和用户利用率之和。它随着用户利用率的上升而波动，因为系统内存利用率基本不变。

此图中数据点之间三小时的间隔可能无法提供我们所需的粒度。图 11-12 显示了更短时间窗口内的内存利用率。

![](img/6969df54e516231f8e64fd1177ac1127_807_0.png)

图 11-12 Global Memory Summary - Short Time Period

图 11-12 显示了较短时间窗口内更细粒度的内存利用率。你现在可以精确看到内存利用率在大约一天内的变化。

磁盘利用率也可以在一周内绘制图表，如图 11-13 所示。

# HP VantagePoint Performance Agent 和 HP VantagePoint Performance Analyzer/UX

| File Show Settings | Global Disk (Points Every 3) |
| :--- | :--- |
| Disk UTIL PEAK | Disk LOGL_IO |
| Disk PHYS_IO | Disk PHYS_BYTE |

![](img/6969df54e516231f8e64fd1177ac1127_808_0.png)

图 11-13 Global Disk

与 CPU 和内存图一样，这是整周的磁盘使用情况。我们希望查看更短的时间窗口。图 11-14 显示了短窗口内的磁盘利用率。

# Chap. 11 Introduction to UNIX

| File Show Settings | Global Disk (Points Every 5) |
| :--- | :--- |
| Disk UTIL PEAK | Disk LOGL_IO |
| Disk PHYS_IO | Disk PHYS_BYTE |

![](img/6969df54e516231f8e64fd1177ac1127_809_0.png)

图 11-14 Global Summary - Short Time Period

这个大约三小时的短窗口显示了更多细节。半夜出现了巨大的磁盘活动峰值。这些可能是由于多种原因，包括批处理作业或系统备份。你不限于查看单个系统资源的参数。你还可以查看许多系统资源的使用情况，如图 11-15 所示。

# HP VantagePoint Performance Agent 和 HP VantagePoint Performance Analyzer/UX

- CPU TOTAL UTIL
- ACTIVE_PROC
- DISK UTIL PEAK
- MEM PAGEOUT RATE
- MEM SWAPOUT RATE
- SWAP SPACE UTIL
- NFS CALL RATE
- NET PACKET RATE

![](img/6969df54e516231f8e64fd1177ac1127_810_0.png)

图 11-15 Global Summary History

此图中包含许多系统资源，包括 CPU、磁盘和内存。同时显示这么多系统资源时，你希望查看更短的时间段。图 11-16 显示了短时间窗口内的参数。

![](img/6969df54e516231f8e64fd1177ac1127_811_0.png)

图 11-16 Global Summary - Short Time Period

图 11-16 显示了短时间窗口内许多系统资源利用的更细粒度。你现在可以查看各种系统资源与其他资源之间的关系。

你可以使用名为 `perfstat` 的实用命令来查找系统中运行的 VantagePoint Performance Analyzer/UX 的状态。以下示例显示了带有 `-?` 选项执行 `perfstat` 命令以查看所有 `perfstat` 选项：

# # perfstat -?
```
