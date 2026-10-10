
```c
void *vmalloc(unsigned long count);
```

这里 `count` 是请求的分配大小。该函数返回内核虚拟地址。

`vmalloc()` 比 `kmalloc()` 享有更大的分配大小限制，但速度较慢，且不能从中断上下文调用。此外，你不能使用 `vmalloc()` 返回的物理不连续内存来执行*直接内存访问*（DMA）。高性能网络驱动程序通常在设备打开时使用 `vmalloc()` 来分配大型描述符环。

内核提供了更复杂的内存分配技术。这些包括*旁路缓冲区*、*slabs* 和*内存池*，超出了本章的范围。

### 查看源代码

内核启动以执行位于 `arch/x86/boot/` 目录下的实模式汇编代码开始。查看 `arch/x86/kernel/setup_32.c` 以了解保护模式内核如何获取实模式内核获得的信息。

第一条启动消息由驻留在 `init/main.c` 中的代码打印。深入了解 `init/calibrate.c` 以了解 BogoMIPS 校准，并查看 `include/asm-your-arch/bugs.h` 以洞察架构相关的检查。

内核中的定时器服务包括位于 `arch/your-arch/kernel/` 中的架构相关部分和实现在 `kernel/timer.c` 中的通用部分。对于相关定义，请查看头文件 `include/linux/time*.h`。

`jiffies` 定义在 `linux/jiffies.h` 中。`HZ` 的值取决于处理器，可以在 `include/asm-your-arch/param.h` 中找到。

内存管理源位于顶层的 `mm/` 目录中。

**表 2.1** 总结了本章中使用的主要数据结构及其在源代码树中定义的位置。**表 2.2** 列出了本章中使用的主要内核编程接口及其定义的位置。

### 表 2.1. 数据结构摘要

| 数据结构 | 位置 | 描述 |
| :--- | :--- | :--- |
| HZ | `include/asm-your-arch/param.h` | 系统定时器每秒滴答的次数 |
| loops_per_jiffy | `init/main.c` | 处理器在 1 个 jiffy 内执行内部延迟循环的次数 |
| timer_list | `include/linux/timer.h` | 用于保存你希望在未来某个时间点执行的例程的地址 |
| timeval | `include/linux/time.h` | 时间戳 |
| spinlock_t | `include/linux/spinlock_types.h` | 一种自旋锁定机制，以确保只有一个线程进入临界区 |
| semaphore | `include/asm-your-arch/semaphore.h` | 一种睡眠锁定机制，允许预定数量的用户进入临界区 |
| mutex | `include/linux/mutex.h` | 替代 `semaphore` 的新接口 |
| rwlock_t | `include/linux/spinlock_types.h` | 读者-写者自旋锁 |
| page | `include/linux/mm_types.h` | 内核对物理内存页的表示 |

### 表 2.2. 内核编程接口摘要

| 内核接口 | 位置 | 描述 |
|---|---|---|
| `time_after()` | `include/linux/jiffies.h` | 将当前的 jiffies 值与指定的未来值进行比较 |
| `time_after_eq()` | `include/linux/jiffies.h` | 将当前的 jiffies 值与指定值进行比较 |
| `time_before()` | `include/linux/jiffies.h` | 将当前的 jiffies 值与指定值进行比较 |
| `time_before_eq()` | `include/linux/jiffies.h` | 将当前的 jiffies 值与指定值进行比较 |
| `schedule_timeout()` | `kernel/timer.c` | 在指定超时时间过后调度进程运行 |
| `wait_event_timeout()` | `include/linux/wait.h` | 如果指定条件变为真或发生超时，则恢复执行 |
| `DEFINE_TIMER()` | `include/linux/timer.h` | 静态定义一个定时器 |
| `init_timer()` | `kernel/timer.c` | 动态定义一个定时器 |
| `add_timer()` | `include/linux/timer.h` | 在超时时间过后调度定时器执行 |
| `mod_timer()` | `kernel/timer.c` | 更改定时器到期时间 |
| `timer_pending()` | `include/linux/timer.h` | 检查当前定时器是否处于挂起状态 |
| `udelay()` | `include/asm-generic/delay.h`, `arch/x86/lib/delay.c` | 忙等待指定的微秒数 |
| `rdtsc()` | `include/asm-x86/msr.h` | 获取 Pentium 兼容处理器上的 TSC 值 |
| `do_gettimeofday()` | `kernel/time.c` | 获取挂钟时间 |
| `local_irq_disable()` | `include/asm-generic/system.h` | 禁用本地 CPU 的中断 |
| `local_irq_enable()` | `include/asm-generic/system.h` | 启用本地 CPU 的中断 |
| `local_irq_save()` | `include/asm-generic/system.h` | 保存中断状态并禁用中断 |
| `local_irq_restore()` | `include/asm-generic/system.h` | 将中断状态恢复为调用对应的 `local_irq_save()` 时的状态 |
| `spin_lock()` | `include/linux/spinlock.h`, `kernel/spinlock.c` | 获取自旋锁。 |
| `spin_unlock()` | `include/linux/spinlock.h` | 释放自旋锁 |
| `spin_lock_irqsave()` | `include/linux/spinlock.h`, `kernel/spinlock.c` | 保存中断状态，禁用本地 CPU 的中断和抢占，并锁定临界区以规范其他 CPU 的访问 |
| `spin_unlock_irqrestore()` | `include/linux/spinlock.h`, `kernel/spinlock.c` | 恢复中断状态和抢占，并释放锁 |
| `DEFINE_MUTEX()` | `include/linux/mutex.h` | 静态声明一个互斥量 |
| `mutex_init()` | `include/linux/mutex.h` | 动态声明一个互斥量 |
| `mutex_lock()` | `kernel/mutex.c` | 获取互斥量 |
| `mutex_unlock()` | `kernel/mutex.c` | 释放互斥量 |
| `DECLARE_MUTEX()` | `include/asm-generic/semaphore.h` | 静态声明一个信号量 |
| `init_MUTEX()` | `include/asm-generic/semaphore.h` | 动态声明一个信号量 |
| `up()` | `arch/x86/kernel/semaphore.c` | 释放一个信号量 |
| `down()` | `arch/x86/kernel/semaphore.c` | 获取一个信号量 |
| `atomic_inc()`, `atomic_inc_and_test()`, `atomic_dec()`, `atomic_dec_and_test()`, `clear_bit()`, `set_bit()`, `test_bit()`, `test_and_set_bit()` | `include/asm-generic/atomic.h` | 用于执行轻量级操作的原子操作 |
