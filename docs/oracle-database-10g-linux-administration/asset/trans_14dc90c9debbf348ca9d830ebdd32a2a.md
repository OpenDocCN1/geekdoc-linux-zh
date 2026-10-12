
## 第 10 章：在 Linux 上调优 Oracle 和 RAC 251

使用 1 作为实例编号

*指定要选择的快照天数*

-----------------------------------------------

输入天数 (n) 将列出最近 (n) 天的快照。不指定数字按 <return> 将列出所有已完成的快照。

列出所有已完成的快照

| 实例 | 数据库名称 | 快照 ID | 快照开始时间 | 快照 | 级别 注释 |
|---|---|---|---|---|---|
| orcl | ORCL | | 1 05 Jun 2004 22:41 | | 5 |
| | | | 2 06 Jun 2004 12:42 | | 5 |

指定开始和结束快照 ID

-----------------------------------

Enter value for begin_snap: 1
Begin Snapshot Id specified: 1

Enter value for end_snap: 2
End Snapshot Id specified: 2

*指定报告名称*

-----------------------------------------------------

默认报告文件名是 sp_1_2。要使用此名称，按 <return> 继续，否则输入其他名称。Enter
value for report_name:
userReport.txt
使用报告名称 JuneReport.txt

STATSPACK 报告

其后是 Statspack 报告本身。此外，Statspack 报告会写入您对 spreport.sql 脚本中提出的问题的回答所指定的文件中。

一旦您拥有 Statspack 报告，您就可以开始分析 Oracle 实例以及部分会话的运行情况。

## 解析 Statspack 数据

Statspack 数据位于由 spreport.sql 创建的报告文件中。该报告已为您计算了许多 Oracle 统计信息。这些信息对于实例调优和应用调优都非常有用。以下是 Statspack 所提供的一些示例。
Statspack 报告以关于数据收集和 Statspack 报告的信息开始，如下所示：

STATSPACK 报告

| 数据库名称 | 数据库 ID | 实例 | 实例编号 | 版本 | RAC 根 |
|---|---|---|---|---|---|
| ORCL | 105394617 | orcl | 1 | 10.1.0.2.0 | NO |
| | | | | | ptc6.perftuning. |
| | | | | | com |

快照 ID | 快照时间 | 会话数 | 游标/会话 | 注释
---|---|---|---|---
Begin Snap: | 1 05-Jun-04 22:41:49 | 14 | 5.4 | 
End Snap: | 2 06-Jun-04 12:42:35 | 14 | 5.0 | 
Elapsed: | 840.77 (mins) | | | 

其后是关于内存配置以及系统在测量间隔期间所承受负载的信息。如下所示：

### 缓存大小（结束）

Buffer Cache: 24M Std Block Size: 8K
Shared Pool Size: 96M Log Buffer: 256K

### 负载概要

| | 每秒 | 每次事务 |
|---|---|---|
| Redo size: | 647.77 | 7,103.81 |
| Logical reads: | 18.84 | 206.57 |
| Block changes: | 3.97 | 43.51 |
| Physical reads: | 0.58 | 6.37 |
| Physical writes: | 0.23 | 2.48 |
| User calls: | 0.06 | 0.68 |
| Parses: | 0.70 | 7.70 |
| Hard parses: | 0.01 | 0.07 |
| Sorts: | 0.48 | 5.25 |
| Logons: | 0.02 | 0.22 |
| Executes: | 1.65 | 18.08 |
| Transactions: | 0.09 | |

% Blocks changed per Read: 21.06 Recursive Call %: 99.26
Rollback per transaction %: 2.57 Rows per Sort: 10.07

完成必要的维护工作并获得背景信息后，您可以开始查看实际的调优信息。出现的第一条信息是有关缓冲区缓存和共享池的缓存信息，如下所示：

### 实例效率百分比（目标 100%）

Buffer Nowait %: 100.00 Redo Nowait %: 99.99
Buffer Hit %: 96.62 In-memory Sort %: 100.00
Library Hit %: 99.35 Soft Parse %: 99.06
Execute to Parse %: 57.43 Latch Hit %: 100.00
Parse CPU to Parse Elapsed %: 93.74 % Non-Parse CPU: 69.69

| 共享池统计信息 | 开始 | 结束 |
|---|---|---|
| Memory Usage %: | 70.36 | 83.46 |
| % SQL with executions>1: | 68.63 | 73.23 |
| % Memory for SQL w/exec>1: | 54.27 | 53.24 |

除了缓存统计信息外，还列出了大量等待事件以及消耗资源最多、运行时间最长的 SQL 语句的信息，并按各种资源排序。这对于查找消耗资源最多的 SQL 非常有用，这些语句是调优的良好候选对象。

Statspack 提供的一个非常有用的功能是列出非默认的 Oracle 初始化参数。这对于判断是否有明显的东西调优不当或根本未配置非常有帮助。这通常是我调优系统的起点：寻找明显的问题。

## 等待事件调优

借助提供的 Oracle 统计信息，您通常可以通过使用等待事件和会话等待事件来调优 Oracle SQL 语句，从而取得相当好的效果。这些信息通常可以提供有关各个会话正在等待什么的有价值的信息。一些常见的等待事件涉及缓冲区或闩锁。由于等待事件数量众多，这里无法全部涵盖。

市场上有多款第三方工具，例如 Veritas 的 Indepth，实际上通过监控等待事件来监控系统。如果您知道系统正在等待哪些事件，通常可以更有效地进行调优。等待统计是调优系统的好方法，因为您直接针对性能问题的核心；耗时最多的部分。基于等待的调优可能非常有效，但应与其他调优方法（如实例调优和 I/O 调优）结合使用。

## 硬件调优

第三种调优类型是硬件调优。硬件调优涉及重新配置或为系统添加新硬件以提高性能。当您已超出系统的硬件资源时，通常需要进行硬件调优。这在 I/O 子系统和系统 RAM 上最常见。当系统资源已被消耗，且调优应用程序和 Oracle 实例以减少资源使用并未足够改善性能时，您几乎别无选择，只能添加更多硬件。

硬件调优与本书记载的容量规划和 sizing 在性质上相似。

硬件通常应作为最后的手段；然而，它通常是首选手段。这是因为添加新硬件比花费时间和精力找出真正问题要容易。有时这可以暂时奏效，但最终您会达到添加更多硬件变得不可能或成本过高的地步。这并不是说硬件调优不必要；只是它不应该是调优系统的第一步。

## 监控 Linux 系统

除了通过 Statspack 监控 Oracle 系统外，监控 Linux 系统也很重要。Linux 系统中可调优的参数并不多，然而，调优不当的系统可能会因此出现严重的性能问题。一些参数涉及必须为 Oracle 分配的资源，包括共享内存和信号量。如本书记载所示，这些参数可以在 /etc/sysctl.conf 参数文件中设置。让我们看一下其中几个参数。

以下是 /etc/sysctl.conf 中为共享内存和信号量设置的參數：

```
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
```

这些参数配置共享内存段可以有多大。按此设置，您可以拥有高达 2GB 的 SGA（假设没有其他程序使用共享内存）。要查看当前正在使用的共享内存和信号量，请使用 Linux ipcs 命令，如下所示：

```
[root@ptc6 root]# ipcs

-------- Shared Memory Segments ----------
key        shmid    owner    perms      bytes      nattch     status
0x00005643 0        root     666        1024       1
0x00005654 32769    root     666        1024       1
0x00000000 262146   gdm      777        196608     2          dest
0x00000000 327683   gdm      777        196608     2          dest
0x54250c38 360452   oracle   640        188747776  15

-------- Semaphore Arrays -----------
key        semid    owner    perms      nsems      status
0x00005653 0        root     666        1
0x460de1d4 196609   oracle   640        127
0x460de1a5 327978   oracle   640        127
0x460de1a6 262147   oracle   640        127

--------- Message Queues --------
key        msqid    owner    perms      used-bytes   messages
```

安装 Oracle 所需的额外调优参数包括以下内容：

```
fs.file-max = 65536
net.ipv4.ip_local_port_range = 1024 65000
```
