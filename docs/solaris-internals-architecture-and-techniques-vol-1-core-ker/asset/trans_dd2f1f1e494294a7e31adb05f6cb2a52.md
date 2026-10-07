
内核必须恢复被中断线程的状态以便其能够继续执行。被中断的线程会被取消固定（因中断而被抢占的线程被认为是固定的），并调用内核的 `resume_from_interrupt()` 汇编程序来恢复被中断线程的状态。

如果该线程不是中断线程，代码将测试内核线程中的交接指针（`t_handoff`）。非空的 `t_handoff` 指针表示该进程应该交由另一个线程，以支持调度器激活（Scheduler activations）（调度器激活首次在 Solaris 2.6 中引入，并在第 407 页的[调度器激活](Scheduler Activations）中进行了讨论）。

简而言之，调度器激活的目标之一是为内核调度程序与用户线程库之间提供一个通信框架。这种通信改进了用户线程的调度，并减少了当进程中所有 LWP（轻量级进程）都被阻塞时，可运行线程获取 LWP 的延迟。回想早前的讨论，用户级线程（通过 `thr_create(3T)` 或 `pthread_create(3T)` 调用创建的线程）由用户线程调度器映射到 LWP 上。如果进程中的所有 LWP 都被阻塞且存在可运行的用户线程，则用户线程调度器将缺乏所需的资源（即 LWP）来调度用户线程。在 Solaris 2.6 之前，内核实现了一种信号机制（使用 `SIGWAITING`）来增加可用 LWP 池。

通过调度器激活，内核和用户线程库之间建立了一条通信路径。如果该进程已经建立了激活，则可能有一个现成的 LWP 池，在这种情况下，`t_handoff` 指针将不为空。如果是如此，则会调用内核处理函数，并最终进入内核 `resume()` 代码，将与 `t_handoff` 关联的内核上下文切换到处理器上。

如果当前线程不是中断线程且不需要交接，`sw()` 会调用 `disp()` 函数，`disp()` 函数是寻找最高优先级线程以进行运行的代码段，它将线程状态设置为运行（`TS_ONPROCESS`），并安排其切换到处理器上。在高级层次上，`disp()` 函数在调度队列中搜索最高优先内核线程，从搜索当前处理器的队列开始——即执行 `disp()` 代码的处理器。如果这些搜索结果为空，代码将搜索多处理器系统上其他处理器的调度队列，寻找可运行的内核线程。如果在调度队列上没有找到线程，处理器将执行其空闲线程，该线程执行一个紧凑循环，在每次通过循环时测试是否有可运行线程，如果运行计数大于 0，则进入 `sw()`。

对最高优先级线程的搜索从内核抢占队列开始，当前处理器引用该队列并与 `cp_kp_queue` 链接。在系统中，一个具有多个处理器分区的系统（每个处理器组——回想每个处理器组有一个内核抢占队列），属于执行处理器的处理器分区的抢占队列是被首先搜索的。

## 内核调度程序

执行处理器的所属分区被首先搜索。`cp_kp_queue` 的搜索如下伪代码所示。

```
kpq = 指向内核抢占队列的指针
dq = 指向处理器调度队列的指针
while ( priority = kpq->dispmaxunpri > 0 ) AND
    ( priority = dq->dispmaxunpri ) AND
    ( the current CPU IS NOT OFFLINE ) AND
    thread_pointer = disp_next(pointer, kpq) != NULL
        if (disp_ratify(thread_pointer, kpq) != NULL)
            return(thread_pointer)
```

上述查询搜索循环根据队列的 `disp_maxunpri` 验证优先级值（该值反映了位于队列上的最高优先级线程），确保当前处理器未离线，并调用调度程序 `disp_get()` 从内核抢占队列中获取最高优先级线程。`disp_get()` 找到最高优先级的无绑定线程，调用 `disp_eq()` 将线程从调度队列中移除，并将线程指针返回给 `dispatch()`。如果没有找到任何内容，则返回 NULL 值。

```
disp_getbest()
    dpq = 调度队列指针（此例中的 cp_kp_queue）
    priority = dq->disp_max_unbound_pri
    if (priority == -1)
        return (NULL)
    queue = dq->disp_q[pri];
    thread_pointer = queue->dq_first;
    遍历线程链表
        if (没有无绑定线程)
            return NULL
        else
            thread_pointer = 找到的线程
            dispatch(thread_pointer)
            设置线程 t_disp_queue, processorus->cpu_dispatch, 线程状态为 ONPROC
            return (thread_pointer)
```

如果在 `disp_getbest()` 中找到无绑定线程，该线程将从 `dispq()` 中出队，线程的 `t_dispatch` 队列指针被设置为引用处理器的 cpu 结构 dispatch 指针，设置为选定的线程指针，且线程状态为 `ONPROC`。

`disp_get()` 负责更新调度队列数据结构，并将选定的线程从队列中移除。它递减 `drnnable`（维护所有队列的总计数）以及相应的优先级（参见第 368 页的图 9.5）。如果每个优先级队列的计数 `dq_srcount` 为 0，则更新队列位图以反映队列为空。`disp_gact` 位图使用集合来反映每个优先级队列上是否存在可运行线程；对应于零队列的位会被清零。`disp_maxrunpri` 和 `disp_maxunpri` 也会更新，以反映队列中的最高优先级。

一旦完成了线程选择并从队列中移除线程，代码返回 `disp()`，它调用 `disp_ratify()` 以确保选定的线程实际上是最佳运行候选。调度程序内部使用的细粒度锁允许对队列进行并发更改，由于此原因，选择了“选择-验证”（select-and-ratify）算法。选择阶段完成后，进入 `disp_ratify()` 完成验证阶段。验证代码简单比较选定线程的优先级与 `maxrunpri` 值。如果选定线程的优先级大于 `maxrunpri`，则通过；否则重新进入循环寻找最佳可运行线程。如果在 `disp_ratify()` 执行时队列上出现了更高优先级的线程，则通过调用 `selectfront()` 将选定线程放回队列。

如果在内核抢占队列上未找到线程，则测试每个处理器的 `disp_maxrunpri`。值为 -1 表示队列为空为空。在这种情况下，代码搜索系统上其他处理器的队列，从 `disp_getwork()` 代码开始，该代码寻找具有最高优先级线程的处理器。然后，使用之前的 `disp_getbest()` 和 `disp_ratify()` 函数。

如果当前处理器的 `disp_maxrunpri` 显示有可运行线程，则从最高优先级队列中移除第一个线程，更新队列数据（`disp_runnable`、`dq_nrcount`、`disp_qactmap`、`disp_maxunbound_pri`、`disp_maxrunpri`），验证选择，并 `disp()` 返回线程指针给 `swch()`。

如果在任何调度队列上未找到工作，则通过将线程指针设置为从处理器 cpu 结构引用的 `cpu_idle_thread` 选择空闲线程。空闲线程指针返回给 `swch()`。

回到 `swch()` 后，带有线程（或空闲线程）指针，调用内核 `resume()` 代码来处理处理器上的线程切换。`resume()` 使用汇编语言实现，因为上下文切换过程需要与处理器硬件进行底层接触，原因有两个：保存被切换线程的硬件上下文，以及设置硬件寄存器和其他上下文信息，以便新线程开始执行。

## 9.3 内核睡眠/唤醒机制

内核线程的典型周期不仅包括在处理器上的执行时间，还包括等待请求资源变得可用的时间。一个

