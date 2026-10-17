
```
RCV  SND   MSG  TIME   THRUPT   CPU    CPU    Snd   RCV
                send  rcv    lat
131070 131070 8192 60.00 798.59 9.28 11.34 1.903 2.327
131070 131070 8192 60.00 796.62 9.12 11.48 1.876 2.362
131070 131070 8192 60.00 800.74 9.14 11.78 1.869 2.411
131070 131070 8192 60.00 796.92 9.24 11.90 1.899 2.447
131070 131070 8192 60.00 800.05 9.20 11.48 1.885 2.350
```

`RCV` = RCV socket size (bytes)
`SND` = send socket size (bytes)
`MSG` = send msg size (bytes)
`TIME` = elapsed time (seconds)
`THRUPT` = throughput (10^6 bits/second)
CPU send = CPU utilization send local (%)
CPU rcv = CPU utilization receive remote (%)
Snd lat = Service Send local (us/KB)
RCV lat = Demand RCV remote (us/KB)

关于该基准测试及部分存档结果，请访问 [http://www.netperf.org](http://www.netperf.org)。

### SPEC SFS

SPEC ([http://www.spec.org/](http://www.spec.org/)) 提供用于网络文件系统的基准测试。目前主要用于基准测试 NFS v2 和 v3，同时对 UDP 和 TCP 传输层进行基准测试。SPEC SFS 还详细列出了所有常见的网络文件操作：创建目录、读取文件、写入文件、检查访问权限、删除文件、更新访问权限等。测试完成后，将生成每个操作的吞吐量。测试试图通过适当混合的操作来模拟真实世界的工作负载，因此结果应与任何合理的 NFS 工作负载相关。性能分析人员在得出过多结论之前，可能希望监控系统操作与 SPEC SFS 基准测试运行中发布的操作分解进行对比。

与其他基于 SPEC 的测试一样，存在严格的运行规则、配置要求、数据完整性要求和报告要求。仍然可以使用该测试进行内部测试，并用于比较环境中各种配置更改的结果。

## 应用基准测试

本节讨论以下基准测试：

- Java 基准测试 Volanornark、SPECjbb 和 SPECjvm
- PostMark
- 数据库基准测试

### Java 基准测试

用于比较 Java 实现、Java 设置或特定平台上的 Java 的三种常用基准测试是 Volanornark ([http://www.volano.com/benchmarks.html](http://www.volano.com/benchmarks.html))、SPECjbb 和 SPECjvm。Volanornark 是一个旨在模拟完全用 Java 编写的 Volano 聊天室应用的基准测试，它具有许多 Java 应用相似的特定应用特征。它模拟了在本地操作系统上实例化大量线程的长连接网络连接。由于该基准测试对延迟敏感且响应时间非常重要，Volanornark 基准测试的目标是在指定的响应时间内查看可以维持多少个到聊天室的连接。显然，您能在合理延迟下维持的连接越多，应用实现消耗的开销就越少。Volanornark 可以实现将服务器应用和所有客户端都运行在本地防火墙内，从而将网络组件从整体方程中分离出来，专注于 Java 实现及其底层性能特征。然而，更现实的工作负载涉及在网络上设置客户端，以驱动服务器。这有助于隔离应用性能以及整体 Java 性能。它还模拟了更合理的 Java 客户部署，其中 Java 用作客户端/服务器配置。

Java、SPECjvm 和 SPECjbb 相比此前讨论的基准测试增加了新的复杂性层面。前文提到的大多数基准测试可能会受到系统调优的显著影响。它们更容易受硬件配置更改、可用系统总内存等因素的影响。对于这些基准测试，相同的操作系统配置选项、硬件配置选项等往往主要因素。Java 本身有控制堆大小的配置参数、线程类型等。每个这些配置参数都会以某种不可预测的方式与测试及底层操作系统相互作用。因此，基准测试发布工作通常会运行一系列测试，在每一层级改变各种配置参数，以表征配置参数之间的潜在相互作用。这种技术对于查找系统的特定部分的最佳结果非常常见。然而，像这样的基准测试也可以用于建模各种配置更改的影响。在这种情况下，基准测试作为一个对照，用于比较各种更改。

将基准测试作为对照允许性能分析人员尝试不同版本的 Java、不同的操作系统以及 Java 的不同配置参数等。这为性能分析人员提供了关于优化类似工作负载的更多见解。

Volanornark 提供高级指标来表示吞吐量，包括发送消息数、接收消息数、总消息数以及每秒的整体消息吞吐量。以下是示例运行的输出。

```
$ volanornark 1024 1024 1000
Running with start heap = 1024 max heap=1024 msg_count=1000
[ JVMST08G: verbosegc is enabled ]
[ JVMST08: -verbosegc output will be written to stderr ]
<GC[0]> Expanded System Heap by 63336 bytes
Java version "1.4.1"
Java(TM) 2 Runtime Environment, Standard Edition (build 1.4.1)
Classic VM (build 1.4.1, J2SE 1.4.1 IBM build cxlc132dev-20030702 (JIT enabled: jitc))
Volanornark(TM) Benchmark Version 2.1.2
Copyright (C) 1996-1999 Volano LLC. All rights reserved.
Creating room number 1 ...
20 connections so far.
Creating room number 2 ...
40 connections so far.
Creating room number 3 ...
60 connections so far.
Creating room number 4 ...
80 connections so far.
Creating room number 5 ...
100 connections so far.
Creating room number 6 ...
120 connections so far.
Creating room number 7 ...
140 connections so far.
Creating room number 8 ...
160 connections so far.
Creating room number 9 ...
180 connections so far.
Creating room number 10 ...
200 connections so far.
Running the test ...
<AF[1]: Allocation Failure, need 528 bytes, 0 ms since last AF>
<AF[1]: managing allocation failure, action=1 (10/1019991016) [53683736/53683736]>
<GC[4]: GC cycle started Mon Nov 24 10:13:30 2003
<GC[4]: Freed 1018020216 bytes, 538 free
[1071903952/10736474752], in 83 ms>
<GC[4]: mark: 68 ms, sweep: 15 ms, compact: 0 ms>
<GC[4]: refs: soft 0 (age > 32), weak 0, final 0,
phantom 0>
<AF[1]: completed in 94 ms>
Test complete.
```

```
VolanoMark 版本 = 2.1.2
发送的消息数 = 200000
接收的消息数 = 380000
消息总数 = 400000
耗时 = 79.49 秒
平均吞吐量 = 每秒 50321 条消息
```

SPECjvm 是由标准性能评估公司（SPEC）控制并提供的基准测试。SPEC 衡量 JVM 的客户端性能，包括其在底层操作系统上的运行表现。SPECjvm 还衡量即时（JIT）编译器。底层操作系统和硬件性能也会影响 SPECjvm 的吞吐量测量。
