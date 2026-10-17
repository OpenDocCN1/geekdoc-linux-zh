
# 2020国际计算机研讨会 (ICS) ｜｜实时多处理器 Linux 内核延迟最小化的实证方法

摘要—本文研究了 `Linux` 内核的实时能力，以及消除实现延迟潜力所需的某些根本性障碍的增强措施。针对硬实时限制，本文同时考虑了性能和可调度性，处理了两个问题领域的交汇点：1) 维护 `Linux` 内核开发和尽力而为维护；2) 最小化调度开销。我们使用 `PREEMPT_RT` 方法提供了内核能力和可抢占性，获得的结果证明了较小的改进即可实现实时性能的提升。

另一项与 `Linux` 相关的后续工作是 Castro 等人 [4]，他们构建了新工具，用于在线检查不变性以及调度活动的可视化，同时分析了 `Linux` 上同步事件处理的性能退化情况。

## I. 引言

完全公平调度器 `CFS` [5] 是一种进程调度器，合并到 `Linux v2.6.23` 中，是默认调度器，其处理下一个任务的复杂度为 `O(1)`，提供了静态延迟。在基于源码的实时系统的其他部分，延迟包括用于调度截止期的最少时间，如图 1 所示。

实时任务的处理取决于系统在界限时间间隔到达事件的能力。多核核心架构对于汽车工业和驾驶系统 [1] 来说是一项极其严峻的挑战，尽管将异构系统整合到单一设备具有成本效益的优势。

开发了一种用于调度的可视化新工具 [6]，允许开发者记录调度器状态，包括执行中的进程 `PID`、调度器运行队列中的 `PID`、上下文切换点、中断进入/退出、事件或每个处理器核心。它与基于方法的工具（例如每 [7]）不同，具有目标系统的高保真和保真跟踪，在 `Linux` 内部实现并具有可变规模，以捕捉持续少于几十微秒的偶尔短突发事件的影响。

硬件平台的格局已存在一段时间，`SoC` 供应商适用于多核实时系统解决方案。我们的目标是产生一个基于多处理器 `Linux` 的支持实时限制的静态和动态工作负载的平台。

尽管有详细的结果，但由于这些实例的存在，我们无法捕获最坏执行时间 `WCET` 的整个行为。该调度基准测试过程由启动基准、循环和循环中的进程组成。

## II. 相关工作

此外，过去使用的典型工作负载的行为和特征（如基准测试 [8] 和 [9]）来自真实的实时系统。结果，我们创建了一个测试框架，托管了一组在“`mict`” [10] 后测量实时机器人系统执行行为的算法。这里“`mict`”代表运动控制，它可以编译为用户程序或内核模块。

像 `Xenomai` [3] 这样的双内核系统部署了一个与 `Linux` 内核并行运行微内核，而像 `PREEMPT_RT` 的内核方案使得实时成为可能。Niem 在大多数测试中表现更好，抖动更小。此类双内核系统的主要问题是有人需要维护微内核和硬件，这是一巨大的工程，并且不符合 `Linux` 内核社区接受的倾向性。

## III. 方法论

程序定时器过期 有效定时器过期任务唤醒 调度持续 开始 `CTA` 任务切入

`RQ` 延迟等 唤醒延迟 `CTX` 延迟 执行

图 1. 典型唤醒延迟。调度持续是指调度器选择下一个任务所花费的时间。

![](img/e0a93935afd7f6816e94f3b1e80fc509_1_0.png)

图 2. `iMX6` Sabre 上的 `Mctest`。横轴表示运行了哪些测试。

![](img/e0a93935afd7f6816e94f3b1e80fc509_1_1.png)

提供了系统内核和用户空间 I/O 开销的洞察，这在内核模式文中启用。

## IV. 实验

我们在 2 个基于 `Cortex-A9` 的板卡上进行了实验（见表 I），这些板卡应用于工业自动化。每个测试运行带有最小根文件系统的 `Linux` 内核 4.4 和 4.`PREEMPT` [11]。我们对绑定内核调优技术的经验包括任务隔离 [12]、测试过的内核 `L1` 和 `L2` 缓存锁定功能 [14]。在 `NX+ iMX6` Sabre 上对比了使用和不使用这些技术的结果。测量结果如图 2、3 和 4 所示，验证了这些调优技术的有效性并提供了基准结果。我们能够将唤醒抖动减少最多 15us 和 17us。这表明默认调度器损害了实时性能。这种调度开销可以分为两部分：调度开销和 `SMP` 缓存竞争。通过 `L2` 缓存锁定，我们能够缓解大部分缓存竞争，但仍保留了最大 76us 的部分抖动。

![](img/e0a93935afd7f6816e94f3b1e80fc509_1_2.png)

图 3. 带有无滴特性和 `L2` 缓存锁定的 `iMX6` Sabre 上的 `Mctest`

### A. 消除系统调用

相比之下，我们使用了内核空间测量的调度器，如图5和66所示，`WCF` 为 27us 和 17us。通过这些结果，我们能够识别系统调用中抖动的来源。为了减轻这一点，我们建议首先编写实时内核模块。这是繁琐的且调试过程困难。因此，使用第二种方法扩展内核模式 `Linux` (`KML`) [15]，允许用户程序运行在内核地址空间中。系统变成跳转而不是会捕获处理器的指令。此外，这将在系统执行期间切换出内核时减轻缓存竞争。此外，我们在 `KML` 中封装了用户空间编程并带有 `WCET` 以获得更好的可解释性。`Linux` 内核模块在 `KML` 中带有 `WCET` 的用户空间编程结果。

### B. 调度器开销测量

识别出调度器是抖动的来源后，我们应用了建议的调度分析工具来评估并识别调度过程的哪部分是抖动的来源。从 `IRQ` 延迟和上下文延迟，我们想要评估调度持续时间。传统的这种延迟使用 `CFS` 算法预测，复杂度被认为 `O(1)`，但结果各异。在切换过程中，我们使用建议的分析器记录调度器运行队列的增量，

### 表 I 实验平台

| 平台名称 | `Intel Cyclone Kit` | `NXP LMX6 Sabre` |
|---|---|---|
| 处理器 | 双核 `ARM-A9` | 四核 `ARM-A9` |
| RAM | 1 GB | 1 GB |
| 额外配置 | 无 | 在隔离的 `CPU1` 上开启 `L2` 锁定，实时任务绑定到 `CPU1` |

![](img/e0a99335afd7f6816e94f3b1e80fc509_2_0.png)

图 5. `iMX6` Sabre 上的内核 `mcelest`

![](img/e0a99335afd7f6816e94f3b1e80fc509_2_1.png)

图 6. 无负载的调度持续时间

![](img/e0a99335afd7f6816e94f3b1e80fc509_2_2.png)

图 6. 带有隔离 `CPU`、无滴特性和 `L2` 缓存锁定的 `iMX6` Sabre 上的内核 `mcelest`

### C. 不同负载条件下的调度持续时间

为了测量调度抖动的来源，我们在分析会期间在 `Cyclone B` 系统上结合调度器创建一个带有 `FIFO` 调度策略和高优先级的额外负载。我们创建了一个

图 12 显示了在没有 `L2` 缓存的 `CPU` 上运行的结果。与结果相比，在双核 `SMP` 下，

![](img/e0a93935afd7f6816e94f3b1e80fc509_3_0.png)

![](img/e0a93935afd7f6816e94f3b1e80fc509_3_1.png)

图 11. 在不同核心上内存受限负载 `cyclistist`（压力测试为 8 个 `vm` 线程，工作大小=16M）的调度耗时

![](img/e0a93935afd7f6816e94f3b1e80fc509_3_2.png)

图 8. `CPU` 受限负载 `cyclistist`（压力测试为 8 个 `cpu` 线程）的调度耗时

![](img/e0a93935afd7f6816e94f3b1e80fc509_3_3.png)

图 12. 某些核心上内存受限负载 `cyclistist`（压力测试为 8 个 `vm` 线程，工作大小=16M）的调度耗时

图 9. 内存受限负载 `cyclistist`（压力测试为 8 个 `vm` 线程，工作大小=16M）的调度耗时

此结果显示平均延迟和抖动略有改善，这意味着共享 `L2` 缓存以及动态数量的加载任务与实时任务的共享是调度耗时的来源。因此，减少动态分配、实时 `CPU` 隔离和缓存锁定可以防止调度耗时的增加，将其保持在约 10us 的稳定值。

## V. 结论

![](img/e0a93935afd7f6816e94f3b1e80fc509_3_4.png)

我们通过对内核调度器进行分析并测量延迟，评估了实时行为。中断处理机制的设计可能会导致长长的操作系统延迟。提出的方法通过隔离 `CPU`、无滴答内核，通过各种应用特性改进了任务响应能力，并已通过测试。

图 10. I/O 受限负载 `cyclistist`（压力测试为 8 个线程）的调度分布

## 参考文献

[1] S.-H. Wang, S.-W. Cheng, and C.-C. J. Huang, “Pyarna: Linux-based experimental platform for constructing self-driving miniature vehicles,” in Intelligent Computing. Springer International Publishing, 2019, p. 985–994.

[2] F. Reghenzi, G. Massari, and W. Fornacci, “The real-time Linux kernel on preempt,” ACM Computing Surveys (CSUR), vol. 52, no. 1, p. 1–30, 2019.

[3] C.-C. Chen, C.-B. Lin, and C.-K. Wu, “Performance evaluation of xenonai 3,” in Proceedings of the 17th Real-Time Linux Workshop (RTLiWS), Graz, Austria, 2015, p. 1–6.

[4] I.-P. Lee, J. Limon, F. Guin, V. Quera, and A. Fedorov, “The Linux scheduler: A decade of wasted cores,” in Proceedings of the Eleventh European Conference on Computer Systems. New York, USA, ACM, 2016, p. 11–16. Online: Available: http://doi.org/10.1145/2903118.2903126

[5] doc-scheduler. [Online]. Available: https://www.kernel.org/doc/Documentation/scheduler/scheduler-design.html

[6] sch-scheduler. [Online]. Available: https://github.com/onyyang/rt-scheduler

[7] Perf wiki. [Online]. Available: https://perf.wiki.kernel.org/benchmarks. [Online]. Available: https://github.com/linux/kernel/master/tools/

[8] v8-tests. [Online]. Available: https://github.com/google/v8/master/test/

[9] Suite of real-time-tests. [Online]. Available: https://git.kernel.org/pub/scm/linux/linux/kernel/rt-tests

[10] mect. [Online]. Available: https://github.com/onyyang/mect [Online]. Available: https://github.com/onyyang/mect/master/realtime/

[11] realtime-linux [linux wiki]. [Online]. Available: https://www.kernel.org/doc/latest/rt-process/index.html

[12] M. Krassansky. Cpi isolation extensions. [Online]. Available: https://arxiv.org/abs/2209.07827

[13] J. Corbet. (nearly) full ticks scheduler in 3.10. [Online]. Available: https://tor.net/Articles/549680

[14] Cache-lockdown. [Online]. Available: https://developer.apple.com/documentation/dd0246h/functional/cache-operation/cache-lockdown

[15] T. Meng. Kernel mode: Execute processes in kernel mode. [Online]. Available: http://github.com/siss.is.u-tokyo.ac/~#kernel

[16] V. Sun. Second mode Linux: Transparent an operating system protected by a type theory, in ASIAN 2003: Advances in Computing Science – Programming Languages and Distributed Computation. Berlin, DE: Springer, 2003, p. 3–17.

[17] vdo - overview of the virtual edf dynamic object. [Online]. Available: http://man7.org/linux/manpages/vdo.7
