
如果锁是自适应互斥锁且未被持有，则`mutex_enter()`的调用者获得该锁的所有权。如果两个条件都不成立，即锁被持有或锁是自旋锁，则代码进入`mutex_vector_enter()`函数来获取锁。`mutex_vector_enter()`代码首先测试锁类型。对于自旋锁，处理器当前的优先级中断级别（PIL）被保存在`m_oldspl`中，然后测试锁。如果锁未被持有，则设置锁（在`m_spinlock`中）并返回调用者。如果锁被持有，则强制调用者进入自旋循环，在循环中递增循环计数器（用于统计目的，即`lockstat(1M)`数据），并且代码在每次循环中检查锁是否仍被持有。一旦锁被释放，代码跳出循环，获取锁，并返回调用者。

自适应锁需要多做一点工作。当代码进入自适应代码路径（在`mutex_vector_enter()`中）时，它会递增`cpu_sysinfo.mutex_adenters`（adaptive lock enters，自适应锁进入）字段，这反映在`mpstat(1M)`的`smtx`列中。`mutex_vector_enter()`然后再次测试以确定锁是否被拥有（持有），因为在调用`mutex_enter()`和当前到达`mutex_vector_enter()`代码之间的时间间隔内，锁可能已被释放。如果自适应锁未被持有，`mutex_vector_enter()`会尝试获取该锁。如果成功，代码返回。

如果锁被持有，`mutex_vector_enter()`通过遍历CPU结构并将锁的`m_owner`与CPU结构的`cpu_thread`字段进行比较，来确定锁所有者是否正在运行。（`cpu_thread`包含当前在CPU上执行的线程的内核线程地址。）匹配表示持有者正在运行，这意味着自适应锁将自旋。不匹配则表示所有者没有在运行，在这种情况下，调用者必须阻塞。在阻塞的情况下，进入内核旋转门（turnstile）代码以定位或获取一个turnstile，为将内核线程放置在与此turnstile关联的睡眠队列上做准备。

turnstile的放置分两个阶段进行。在`mutex_vector_enter()`确定锁持有者没有在运行后，它进行一个turnstile调用来查找turnstile，在锁中设置等待者（waiters）位，并重新测试所有者是否在运行。如果是，代码释放turnstile并进入自适应锁自旋循环，该循环尝试获取锁。否则，

这段代码将内核线程放到一个回转门（睡眠队列）上，并将线程状态改为睡眠。这实际上结束了 `mutex_vector_enter()` 中的事件序列。

从 `mutex_vector_enter()` 返回时，要么调用者成功获取了锁，要么调用线程位于与该锁关联的回转门睡眠队列上。无论哪种情况，都会更新 `lockstat(1M)` 数据，反映锁类型、自旋时间或睡眠时间，作为 `mutex_vector_enter()` 中完成的最后一项工作。

`lockstat(1M)` 是一个内核锁统计命令，在 Solaris 2.6 中引入。它提供有关内核互斥锁和读写锁的详细信息。

前面段落所描述的算法总结如下伪代码所示。

```
mutex_vector_enter()
    if (lock is a spin lock)
        lock_set_spl() /* enter spin-lock specific code path */
        increment cpu_syncinfo.adjustments
spin_loop:
    if (lock is not owned)
        mutex_trylock() /* try to acquire the lock */
        if (lock acquired)
            goto bottom
        else
            continue /* lock being held */
    if (lock owner is running on a processor)
        goto spin_loop
    else
        lookup turnstile for the lock
        set waiters bit
        if (lock owner is running on a processor)
            drop turnstile
            goto spin_loop
        else
            block /* the spin / sleep queue associated with the turnstile */

bottom:
    update lockstat statistics
```

当线程在锁保护的数据区域完成工作后，它会调用 `mutex_exit()` 代码来释放锁。该入口点以汇编语言实现，处理释放无等待线程的自适应锁这一简单情况。如果没有线程在等待该锁，只需清除锁字段（`m_owner`）并返回即可。除简单情况外，C 语言函数 `mutex_vector_exit()` 从 `mutex_exit()` 进入。

对于自旋锁，锁字段会被清除，处理器恢复到进入锁代码之前所运行的 PIL 级别。对于自适应锁，必须从回转门中选择一个等待线程（如果有多个等待线程），将其状态从睡眠改为可运行，并放入调度队列，以便其执行并获取锁。如果释放锁的线程是优先级继承的受益者，即当具有更好优先级的调用线程无法获取锁时，该线程的优先级得到了提升，那么释放锁的线程的优先级将被重置为继承之前的优先级。优先级继承在“回转门与优先级继承”一节（第 89 页）中讨论。

当释放自适应锁时，代码会清除 `m_owner` 中的等待者位，并调用 `turnstile` 函数唤醒所有等待者。熟悉操作系统睡眠/唤醒机制的读者可能听说过一种被称为*惊群*情况的特殊行为：许多因同一资源而阻塞的线程同时被唤醒，然后疯狂地争抢该资源（此处为互斥锁）——如同一大群四条腿的大型野兽奔向同一个目标。系统行为往往表现为运行队列从相对较小变成很大（所有线程都被唤醒并变为可运行状态），CPU 利用率很高，直到某个线程获取资源，此时大量线程再次睡眠，运行队列恢复正常，CPU 利用率趋于平稳。这是一种任何操作系统都可能发生的通用行为。

在 Solaris 7 中调用 `mutex_vector_exit()` 所使用的唤醒机制看似是在公开招引惊群效应，但在实践中证明并非问题。主要原因是，等待互斥锁的线程发生阻塞的情况很罕见；大多数时候线程会自旋。即使出现阻塞情况，通常也不会达到大量线程阻塞在互斥锁上的程度——惊群问题的特征之一就是资源争用导致大量线程睡眠。实现互斥锁的内核代码段在设计上既短又快，因此锁不会持有太久。需要较长锁持有时间的代码使用读写锁（写锁），它通过选择性唤醒算法提供互斥语义。当然，选择读写锁而非互斥锁还有其他原因，最明显的是允许多个读取者查看受保护的数据。

在接下来的章节中，我们将区分 Solaris 2.5.1 和 2.6 中互斥锁的实现。如前所述，Solaris 2.5.1 和 2.6 与前面描述的 Solaris 7 行为相似，尤其是在锁获取（`mutex_enter()`）方面。更显著的差异存在于锁释放算法及相关的唤醒行为中。

### 3.5.2.1 Solaris 2.6 互斥锁实现差异

首先，检查锁结构，如图 3.6 所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_120_0.png)

Solaris 2.6 在同一结构中定义了所有可能的互斥锁类型。自旋锁与 Solaris 7 相同，只是增加了一个类型字段。自适应互斥锁拥有更多字段，这些字段大多不言自明。`m_owner_lock` 与 Solaris 7 中的 `m_owner` 相同；它就是锁本身，其值在锁被持有时表示持有者的 kthread ID。`m_waiters` 存储等待内核线程的遍历 ID，`m_wlock` 是一个调度器锁（参见第 97 页的“调度器锁”），用于同步对互斥锁中 `m_waiters` 字段的访问。`m_type` 描述锁类型（自适应或自旋）。

除了结构差异之外，Solaris 2.6 在锁获取（`mutex_enter()`）方面，汇编和 C 代码的基本设计与实现基本相同。差异存在于睡眠机制中——Solaris 7 中回转门的实现得到了改进。这些差异体现在为辅助回转门分配和优先级继承而调用的接口和子程序上。（参见第 89 页的“回转门与优先级继承”。）

在锁释放方面，Solaris 2.6 分别实现了释放自旋锁和自适应锁的独立例程：`mutex_vector_exit()` 和 `mutex_adaptive_release()`。当释放一个有待等待线程的自适应锁时，2.6 的代码只会唤醒优先级最高的线程。如果有多个相同（最高）优先级的线程在等待同一把锁，则选择等待时间最长的线程。

### 3.5.2.2 Solaris 2.5.1 互斥锁实现差异
