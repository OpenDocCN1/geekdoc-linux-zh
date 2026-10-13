
在 `rt_enterclass()` 中完成的其他清理工作——初始化 `rtproc` 的其他成员并设置 `rtproc` 和 `kthread` 结构中的指针——在上方未显示。

如果线程是从另一个 RT 线程 fork 的，它也会进入 RT 类，因为子线程在 `rt_fork()` 代码中继承了父线程的优先级时间片。RT 类中父子线程的执行顺序与 TS/IA 类线程不同。根据设计，当 TS/IA 类线程被 fork 时，子线程先执行（这在上一章讨论的 `vfork()` 情况下尤为如此）。RT 线程最终进入调度，而父线程继续运行，除非应用程序代码显式写了其他逻辑。

从时钟处理程序调用的 `rt_tick()` 代码决定线程的时间片是否过期。如果是，线程被强制放弃处理器；否则，继续运行。RT 类通过递减 `rtproc` 结构中的计数器 `rt_timeleft` 来跟踪处理器时间滴答。`rt_timeleft` 为零意味着时间片已用完。可以为 RT 类线程设置无限时间片。RT 调度中的 `rt_quantum` 值为 `-2` 被内核解释为无限时间片，在这种情况下，RT 线程将继续运行，除非它 [放弃]。

（注：提供的 OCR 文本后半部分包含重复片段和断点。我已经根据前半部分的逻辑进展和源文本对流程进行了清理。）

# Solaris 内核调度器 (Dispatcher)

如果已经配置且线程未绑定到特定的处理器集（set），则选择默认分区的 `cp_kp_queue`。任何调度类中的绑定线程（即使是 RT 实时线程）都会被放置在调度队列或其所绑定的处理器上。

线程在调度队列上的插入是通过针对每个处理器的调度队列的 `setfrontq()` 和 `setbackq()` 例程实现的，以及针对内核抢占队列（或队列队列）的 `setpkgq()` 实现的。`setfrontq()` 的作用是将线程置于调度队列的前端，其算法由如下伪代码表示。

```
setfrontq()

if (thread is swapped out or on swap queue)

    call disp_swapped_setrun()

    return

if (uniprocessor system)

    selected_cpu = t_cpu

if (MP system with 1 online CPU)

    selected_cpu = t_cpu

else if (thread is not bound)

    if (thread_priority >= kpreemptpri)

        call setcpu()

        return

    selected_cpu = t_cpu

    if (thread was running on the same partition that dispatch cpu belongs to)

        if (thread_priority < highest-priority thread sitting on the queue)

            selected_cpu = cpu_choose()

    else

        selected_cpu = disp_lowpri_cpu()
```

> /*
在此时，处理器和相关的调度队列已经准备
* */

将线程状态设置为 `TS_RUN` / 为可运行 /
增加调度队列结构上的可运行线程计数 - `disp_runnable`
在调度队列位图中（bitmap）放置线程以反映已添加的线程
将放置在队列上的线程的 `dispatch_queue` 位图设置为 * `disp_maxrunpri`
if (`priority > disp_maxrunpri`)
    `dispatch_queue->disp_maxrunpri = thread_priority`
call `cpu_resched()`

为 TS/IA 线程选择调度队列本质上是选择一个处理器，因为每个处理器都有自己的调度队列。在单处理器系统或仅有一个在线处理器的多处理器系统的伪代码中，处理器的选择变得轻而易举，这就是为什么代码在紧随交换出线程测试之后会预先测试这些条件。被交换出或位于交换队列中的线程在放置到调度队列之前需要被重新加载。

为了触动调度器（PID 0），`disp_swapped_setrun()` 将设置两个可能的标志之一：`wake_sched` 或 `wake_sec`，取决于线程的优先级。这些标志在时钟中断处理程序中进行测试，其中 `wake_sched` 每时钟中断检查一次，而 `wake_sched_sec` 每100 次时钟中断检查一次（即每秒一次）。优先级大于 99（最高 SYS 类优先级）的线程会立即唤醒调度器。

## 内核调度器 (Kernel Dispatcher)

中断 (`wake_sched`); 低优先级线程会导致 `wake_sched_sec` 获取，从而等待更长时间。

`setfrontq()` 中的下一个测试是针对绑定线程，使用了线程结构中的 `t_bound_cpu`。绑定线程的 `t_bound_cpu` 指针指向其所绑定的处理器。如果线程未绑定且优先级大于 `kpreemptpri`，则调用 `setkpri()` 将线程放入内核队列并返回。否则（未绑定且优先级小于 `kpreemptpri`），最初从 `t_cpu` 指针中选择一个 CPU（之前讨论的松散亲性），并完成处理器分区设置。直觉上，从线程的 `t_cpu` 结构中选择的处理器似乎属于同一线程的 `t_cpuapri` 指针所引用的处理器分区，但自上次以来可能已经进行了某些处理器集配置更改，因此该测试是必要的。

如果所选处理器位于某个分区，且该分区上线程的优先级大于或等于该处理器调度队列上的最高优先级线程，则保留所选处理器。否则，调用 `cpu_choose()` 在同一分区内寻找另一个处理器队列来放置该线程。如果分区失败（意味着所选处理器所属的分区与线程上次运行的分区不同），则 `setfrontq()` 会调用 `disp_lowpri_cpu()` 在线程的 `t_cpuapri` 分区中寻找一个处理器。此代码处理了自线程上次放置在调度队列上以来，处理器集配置发生了更改的情况。

`cpu_choose()` 例程寻找最适合放置线程的处理器。在 `cpu_choose()` 中，内核将线程上次运行以来所经过的时间（时钟滴答）与 `re_interval` 进行比较。如果线程不在队列上，则在时钟处理程序中通过 `ts_update_interval` 增加线程的 `t_dispatch_time`，内核将此值与 `rechoose_interval` 进行比较。如果 `t_disp_time` 小于 `rechoose_interval`，则保留线程在当前处理器。否则，调用 `disp_lowpri_cpu()` 寻找处理器。`disp_lowpri_cpu()` 搜索分区中具有最低优先级线程的处理器链表。一旦找到，线程将被插入所选处理器的调度队列中。

正如我们之前提到的，绑定线程被放置在其绑定的处理器的队列上；或者对于处理器集，使用带有 `rechoose_interval` 的松散亲性规则选择集内的一个处理器。一旦选择了处理器调度队列，将使用线程优先级来确定正确的优先级队列。记住，每个处理器的队列是队列的队列，在每个队列内部是线程的链表。

新插入的线程与队列的 `disp_maxrunpri` 进行测试。`cpu_resched()` 检查线程优先级以判断是否存在抢占。内核抢占意味着线程优先级高于当前线程但不高于 `kpreemptpri`。`cpu_resched()` 的工作如下伪代码所示。

```
cpu_resched()
  if (CPU is NOT IDLE AND thread priority > current thread priority)
    if (thread priority == preemptpri AND cpu_runn == 0)
      set cpu_runn in CPU structure
      set t_astflag in currently executing thread
      if (thread priority < preemptpri AND selected cpu is not CPU)
        poke_cpu()
  if (thread_priority <= preemptpri AND cpu_krun == 0)
    set cpu_krun in CPU structure
    if (selected cpu is not CPU)
      poke_cpu();
```
