
如果从设备驱动程序或任何注册并产生中断的内核模块中调用 `init` 代码，则会在参数列表中添加一个中断阻塞块饼干（interrupt block cookie）。中断阻塞块饼干是设备驱动程序在设置其中断向量和参数时的一种抽象。如果从设备驱动程序调用 `mutex_init()` 是为了初始化一个用于高级中断处理程序的互斥锁，则锁类型被设置为自旋。否则，初始化一个自适应锁。测试标准是传递的中断块中的中断级别；（在 SPARC 系统上）级别 10 是高级中断，因此需要自旋锁。初始化代码根据锁的类型清除互斥结构中的大部分字段。自旋锁中的 `m_dummylock` 被设置为全 1（`0xFF`）。我们稍后会看到为什么。

从 `mutex_init()` 调（每个初始化时间仅调用一次）的主要互斥函数是用于获取锁的 `mutex_enter()` 和用于释放锁的 `mutex_exit()`。`mutex_enter()` 假设锁是可用的自适应锁。如果锁已被持有或是自旋锁，则进入一次 `mutex_vector_enter()`。这是一种性能优化。`mutex_enter()` 用汇编代码实现，由于其入口点是为简单情况（自适应锁且未持有）设计的，因此当这些条件成立时，为了获取锁而执行的代码量是极小的。此外，内核中自适应锁远多于自旋锁，使得测试在大多数情况下都是有效的。这里就是空位（dummy）派上用场的地方：`mutex_enter()` 在锁的第一个字节上执行比较交换（compare-and-swap）指令以测试值。在自旋锁上，会测试 `m_dummylock` 字段在数据结构中的位置以及 SPARC 处理器的字节端序。由于 `m_dummylock` 总是被设置（在 `mutex_init()` 中被设置为 1），自旋锁的测试将失败。对于持有的自适应锁测试也会失败，因为该锁在测试字段中具有非零值。也就是说，对于持有的自适应锁，`m_owner` 字段将有一个 kthread 指针值。

如果锁是自适应互斥且未被持有，`mutex_enter()` 的调用者将获得锁的所有权。如果这两个条件都不满足（即锁被持有或锁是自旋锁），代码首先进入 `mutex_vector_enter()` 函数进行类型分类。互斥锁测试锁类型。对于自旋锁，根据处理器的当前优先级中断级别（PIL）设置 `m_oldsp` 字段并对锁进行测试。如果未被持有，则设置锁（`m_spinlock`）并返回调用者。

被持有的锁会强制调用者进入自旋循环，在其中为了统计目的会增加循环计数器；`lockstat(1M)` 数据，并且代码在每次循环中都会检查锁是否仍被持有。一旦锁被释放，代码将跳出循环，获取锁并返回调用者。

自适应锁需要更多的工作。当代码进入自适应代码路径（在 `mutex_vector_enter()` 中）时，会增加 `cpu_sysinfo.mutex_adensters`（自适应锁字段），这反映在 `mpstat(1M)` 的 `smtx` 列中，然后再次测试以确定锁是否被拥有（持有），因为在调用 `mutex_vector_enter()` 到 `mutex_vector_enter()` 代码当前点的时间范围内，锁可能已被释放。如果自适应锁未被持有，`mutex_vector_enter()` 尝试获取锁。如果成功，代码返回。

如果锁被持有，`mutex_vector_enter()` 通过遍历 CPU 结构并测试锁所有者与 CPU 结构中的 CPU 线程（CPU 包含当前在 CPU 上执行的线程的内核线程地址）来确定所有者正在运行。匹配表示持有者正在运行，这意味着自适应锁将自旋。不匹配意味着所有者未运行，在这种情况下调用者必须阻塞。在阻塞情况下，将进入内核转门（turnstile）以定位或获取转门，为将内核线程放置在与转门相关的睡眠队列上做准备。

转门的放置分为两个阶段。在 `mutex_vector_enter()` 确定锁持有者未运行后，它会调用转门锁来锁定转门，设置锁中的等待者，并重新测试所有者是否正在运行。如果是，代码将释放转门并进入自适应锁自旋循环，尝试获取它。否则，代码将内核线程放置在转门（睡眠队列）并将线程状态更改为睡眠。这有效地结束了 `mutex_vector_enter()` 中的事件序列。

退出 `mutex_vector_enter()` 后，要么调用者获取了其尝试获取的锁，要么调用线程处于与锁相关的转门队列上。无论何种情况，`lockstat(1M)` 数据都会更新，反映锁类型、自旋时间或睡眠时间，作为 `mutex_vector_enter()` 完成的最后项工作。

`lockstat(1M)` 是在 Solaris 2.6 中引入的内核锁统计命令。它提供了关于内核互斥锁和读/写锁的详细信息。

## 互斥锁 (Mutex Locks)

前几段描述的算法在下面的伪代码中总结。

```
mutex_vector_enter(){
    if (lock is a spin lock)
        lock_set_spi() /* 进入自旋锁特定的代码路径 */
        increment cpu_sysinfo.ademters.
    spin_loop:
        if (lock is not owned)
            mutex_trylock() /* 尝试获取锁 */
            if (lock is acquired)
                goto bottom
        else
            continue /* 锁正持有 */
        if (lock owner is running on a processor)
            goto spin_loop
        else
            lookup turnstile for the lock
            set waiters bit
            if (lock owner is running on a processor)
                drop turnstile
                goto spin_loop
        else
            block /* 与闸机关联的睡眠队列 */
bottom:
    updatelockstatistics
```
