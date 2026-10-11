
## 决策过程与调度

决策过程与线程公平性和调度延迟有着直接关联。公平性可以描述为所有线程不仅都能取得向前进展，而且以均衡的方式做到这一点的特性。公平性的对立面被称为饥饿（starvation），即某个线程无法取得任何向前进展的情况。公平性往往难以证明，因为它代表了全局性能与局部性能之间的一种妥协练习。调度延迟描述的是线程进入可运行状态（TSRUN）与实际在处理器上运行（TSONPROC）之间的实际延迟。低效的调度延迟行为会导致应用程序响应时间出现可察觉的延迟。一个高效且有效的 CPU 调度器对于计算平台的运行至关重要；它决定在什么时间运行哪个任务（线程）以及运行多久。实时任务和时间共享任务是有区别的，每种类别揭示了不同的目标。这两者都通过嵌入在调度器中的不同调度策略来实现。

Linux 为每个任务分配一个静态优先级，该优先级可以通过 `nice()` 接口进行修改。Linux 拥有多个优先级类别，区分实时任务和时间共享任务。优先级值越低，任务的逻辑优先级越高，换句话说，其总体重要性越高。在此上下文中，当详细阐述优先级的增加和减少时，讨论总是指代逻辑优先级。实时任务的优先级始终高于时间共享任务。

被称为 O(1) 调度器的 Linux 2.6 调度器，是一种多队列调度器，它为每个 CPU 分配一个实际的就绪队列，从而促进了一种 CPU 本地调度方法。O(1) 标签描述的是检索的时间复杂度；换句话说，它指的是这样一个特性：无论系统负载如何，下一个要运行的任务将在恒定的时间内被选中。

之前的 Linux 调度器版本使用“goodness”概念来确定接下来要执行哪个线程。所有可运行任务都保存在单个就绪队列中，该队列表示处于 TSRUN（TASK_RUNNABLE）状态的线程的链表。在 Linux 2.6 中，单个就绪队列锁被替换为每 CPU 锁，从而在 SMP 系统上确保了更好的可扩展性。O(1) 调度器采用的每 CPU 就绪队列方案将就绪队列分解为若干桶（按优先级顺序排列），并利用位图来标识持有可运行任务的桶。定位下一个要执行的任务需要读取位图以找到第一个持有可运行任务的桶，并选择该桶的就绪队列中的第一个任务。

每 CPU 就绪队列由两个任务列表向量组成，分别标记为 active（活跃）向量和 expired（过期）向量。每个向量索引代表一个可运行任务列表，各自位于其相应的优先级级别。经过一段时间的执行后，任务会从 active 列表移动到 expired 列表，以确保所有可运行任务都有机会执行。随着 active 数组变为空，通过修指针交换 expired 向量和 active 向量。

偶尔会调用负载均衡算法来重新平衡就绪队列，以确保每个 CPU 拥有相似数量的可用任务。如前所述，调度器必须决定接下来运行哪个任务以及运行多久。Linux 内核中的时间量子（time quanta）被定义为系统时钟节拍（tick）的倍数。一个节拍定义为两个连续定时器中断之间的固定时间差（$1/HZ$）。在 Linux 2.6 中，HZ 参数设置为 1,000，这意味着中断例程 `scheduler_tick()` 每毫秒调用一次，此时正在执行的任务会被计费一个节拍。将 HZ 参数设置为 1,000 并不会提高系统的响应能力，因为实际的调度器时间片不受此设置的影响。对于主要以数值密集型模式执行的系统，HZ=1,000 的设置可能并不合适。在这样的环境中，系统整体性能可能受益于将 HZ 参数设置为较低的值（约为 100）。

除了静态优先级（`static_prio`），每个任务还维护一个有效优先级（`prio`）。这种区分是为了考虑基于特定任务最近睡眠平均值（`sleep_avg`）的某些优先级奖励或惩罚。睡眠平均值考虑了任务最近被取消调度的节拍数。任务的有效优先级决定了其在就绪队列优先级列表中的位置。当任务的有效优先级超过其静态优先级达到一定级别时，该任务被声明为交互式。这种情况只能基于任务累积的睡眠平均值节拍。嵌入在 Linux 2.6 中的交互式估算框架自动且透明地运行。在 Linux 中，高优先级任务达到交互状态所需的睡眠平均值比低优先级任务小得多。由于任务的交互性是通过睡眠平均值估算的，I/O 密集型任务是达到交互状态的潜在候选者，而 CPU 密集型任务通常不被视为交互式任务。

实际时间片定义为任务在不将 CPU 自愿让渡给另一个任务的情况下可执行的最大时间，它是普通任务静态优先级的一个简单线性函数。优先级本身被映射到 `MIN_TIMESLICE` 到 `MAX_TIMESLICE` 的范围内，其中默认值分别设置为 10 和 200 毫秒。任务的优先级越高，其时间片越大；每当发生一个定时器节拍，任务的运行时间片就会递减。如果递减到 0，调度器将补充时间片，重新计算有效优先级，并将任务重新入队：如果任务被归类为交互式，则进入 active 向量；如果任务被认为是非交互式的，则进入 expired 向量。此时，系统从 active 数组中调度另一个任务。这种场景确保了 active 数组中的任务在任何过期任务有机会再次运行之前先被执行。如果任务被取消调度，其时间片不会在唤醒时补充；然而，由于其累积的睡眠时间，其有效优先级可能已经改变。如果所有可运行任务都用尽了时间片并移动到了过期列表，那么 expired 向量和 active 向量将被交换。这种技术确保了 O(1) 调度器无需遍历可能很大的任务列表，这在 Linux 2.4 调度器中是必需的。新设计的问题是，由于潜在的交互性，可能会出现 active 队列中仍有可运行任务且这些任务未被迁移到 expired 列表的情况。可能会有任务因 CPU 时间不足而饥饿；为了解决饥饿问题，如果第一个迁移到 expired 列表的任务比 `STARVATION_LIMIT`（设置为 10 秒）更旧，且 active 和 expired 数组被交换。

## 摘要

总而言之，虽然 Linux 是一个虚拟内存系统，但它利用了多种类型的地址。这为进程提供了公平的方式来访问内存并运行至完成。Linux 内核用于管理内存的数据结构是复杂的。然而，不同的内核函数需要不同的地址类型。

## 参考文献

- [1] Arcangeli, A. "Evolution of Linux Towards Clustering," EFD R&D Clamart, 2003.
- [2] Axboe, J. "Deadline I/O Scheduler Tunables," SUSE, 2003.
- [3] Corbet, J. "A New Deadline I/O Scheduler," http://lwn.net/Articles/10874.
- [4] "Anticipatory I/O Scheduling," http://lwn.net/Articles/21274.
- [5] "The Continuing Development of I/O Scheduling," http://lwn.net/Articles/21274.
- [6] "Porting Drivers to the 2.5 Kernel," Linux Symposium, Ottawa, Canada, 2003.
- [7] Iyer, S. and P. Drushel. "Anticipatory Scheduling: A Disk Scheduling Framework to Overcome Deceptive Idleness in Synchronous I/O," SOSP, 2001.
- [8] Irwin, Lee W. III. "A 2.5 Page Clustering Implementation," Linux Symposium, Ottawa, 2003.
- [9] "VM Tuning," IBM Technical Document, 2003.
- [10] Nagar, S., H. Franke, J. Choi, C. Seetharaman, S. Kaplan, N. Singhvi, V. Kashyap, and M. Kravetz. "Class-Based Prioritized Resource Control in Linux," 2003 Linux Symposium.
- [11] McMenney, P. "Stochastic Fairness Queueing," INFOCOM, 1990.
- [12] Molnar, I. "Goals, Design and Implementation of the New Ultra-scalable O(1) Scheduler," (sched-design.txt) 2003.
- [13] Mosberger, D. and S. Eranian. IA-64 Linux Kernel, Design and Implementation, Prentice Hall, NJ, 2002.
- [14] Shriver, E., A. Merchant, and J. Wilkes. "An Analytic Behavior Model with Readahead Caches and Request Reordering," Bell Labs, 1998.
- [15] Wienand, I. "An Analysis of Next Generation Threads on IA64," UNSW, HP, 2003.

