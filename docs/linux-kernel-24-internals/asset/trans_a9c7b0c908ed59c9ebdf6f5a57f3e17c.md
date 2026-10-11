

} while(1);
retval = put_user(data, (unsigned long *)buf);
if (!retval)
    retval = sizeof(unsigned long);

out:

current->state = TASK_RUNNING;
remove_wait_queue(&rtc_wait, &wait);
return retval;
}

`rtc_read()` 中发生的事情如下：

- 1. 我们声明一个等待队列元素，指向当前进程上下文。
- 2. 我们将该元素添加到 `rtc_wait` 等待队列中。
- 3. 我们将当前上下文标记为 `TASK_INTERRUPTIBLE`，这意味着在下一次休眠后它不会被重新调度。
- 4. 我们检查是否有数据可用；如果有，我们跳出循环，将数据复制到用户缓冲区，将自身标记为 `TASK_RUNNING`，从等待队列中移除自身并返回。
- 5. 如果尚未有数据，我们检查用户是否指定了非阻塞 I/O；如果是，则以 `EAGAIN`（等同于 `EWOULDBLOCK`）失败。
- 6. 我们还检查是否有挂起的信号；如果有，则通知“上层”在必要时重启系统调用。这里“必要时”指的是 **sigaction(2)** 系统调用中指定的信号处置细节。
- 7. 然后我们“切换出去”，即进入睡眠状态，直到被中断处理程序唤醒。如果我们没有将自身标记为 `TASK_INTERRUPTIBLE`，调度器可能会在数据可用之前更早地调度我们，从而导致不必要的处理。

值得指出的是，使用等待队列，实现 **poll(2)** 系统调用非常容易：

```c
static unsigned int rtc_poll(struct file *file, poll_table *wait)
{
    unsigned long l;

    poll_wait(file, &rtc_wait, wait);

    spin_lock_irq(&rtc_lock);
    l = rtc_irq_data;
    spin_unlock_irq(&rtc_lock);

    if (l != 0)
        return POLLIN | POLLRDNORM;
    return 0;
}
```

所有工作都是由与设备无关的函数 `poll_wait()` 完成的，该函数执行必要的等待队列操作：我们只需将其指向由我们的特定设备中断处理程序唤醒的等待队列即可。

## 2.6 内核定时器

现在让我们将注意力转向内核定时器。内核定时器用于在未来指定时间分发特定函数（称为“定时器处理程序”）的执行。主要数据结构是 `include/linux/timer.h` 中声明的 `struct timer_list`：

```c
struct timer_list {
    struct list_head list;
    unsigned long expires;
    unsigned long data;
    void (*function)(unsigned long);
    volatile int running;
};
```

`list` 字段用于链接到内部列表中，由 `timerlist_lock` 自旋锁保护。`expires` 字段是当 `function` 处理程序应通过传入 `data` 作为参数时被调用时的 `jiffies` 值。`running` 字段在 SMP（对称多处理）系统中用于测试定时器处理程序是否正在其他 CPU 上运行。

函数 `add_timer()` 和 `del_timer()` 分别将给定定时器添加到列表或从列表中移除。当定时器过期时，它会被自动移除。在使用定时器之前，必须通过 `init_timer()` 函数对其进行初始化。并且在添加之前，必须设置 `function` 和 `expires` 字段。

## 2.7 下半部（Bottom Halves）

有时，将中断处理程序内部要执行的工作量拆分为立即工作（例如确认中断、更新统计数据等）和可以推迟到稍后、当中断启用时再执行的工作（例如对数据进行后处理、唤醒等待此数据的进程等）是合理的。

下半部是用于延迟执行内核任务的最早机制，自 Linux 1.x 起就已可用。在 Linux 2.0 中，增加了一种称为“任务队列”的新机制，这将是下一节讨论的主题。

下半部由 `global_bh_lock` 自旋锁进行序列化，即任一 CPU 上同一时间只能运行一个下半部。然而，在尝试执行处理程序时，如果无法获取 `global_bh_lock`，下半部会被标记（即调度）为待执行状态——这样处理就可以继续，而不必对 `global_bh_lock` 进行忙等待。

总共只能注册 32 个下半部。操纵下半部所需的函数如下（所有函数都导出供模块使用）：

- `void init_bh(int nr, void (*routine)(void))`：将由 `routine` 参数指向的下半部处理程序安装到插槽 `nr` 中。该插槽应在 `include/linux/interrupt.h` 中以 `XXXX_BH` 的形式进行枚举，例如 `TIMER_BH` 或 `TQUEUE_BH`。通常，子系统的初始化例程（对于模块来说是 `init_module()`）会使用此函数来安装所需的下半部。
- `void remove_bh(int nr)`：执行与 `init_bh()` 相反的操作，即卸载安装在插槽 `nr` 中的下半部。此处不进行错误检查，因此，例如，`remove_bh(32)` 会导致系统恐慌/错误。通常，子系统的清理例程（对于模块来说是 `cleanup_module()`）使用此函数来释放插槽，以便稍后被其他子系统重用。（TODO：如果 /proc/bottom_halves 能列出系统中所有已注册的下半部不是更好吗？那意味着 `global_bh_lock` 显然必须被改为读写锁）
- `void mark_bh(int nr)`：标记插槽 `nr` 中的下半部以供执行。通常，中断处理程序会在“更安全的时间”标记其下半部以执行（这就是其名称的由来！）。

下半部是全局锁定的任务片段（tasklet），因此问题“下半部处理程序何时执行？”实际上就是“任务片段何时执行？”。答案是在两个地方：a) 每次调用 `schedule()` 时，以及 b) `entry.S` 中每次中断/系统调用返回路径时。（TODO：因此，`schedule()` 的情况实际上很无聊——它就像添加又一个非常非常慢的中断，为什么不干脆从 `schedule()` 中彻底移除 `handle_softirq` 标签？）

## 2.8 任务队列

任务队列可以被视为旧下半部的动态扩展。事实上，在源代码中它们有时被称为“新”下半部。更具体地说，上一节讨论的旧下半部具有以下局限性：

- 1. 只有固定数量（32 个）。
- 2. 每个下半部只能与一个处理函数相关联。
- 3. 下半部在持有自旋锁的情况下被消耗，因此它们不能阻塞。

因此，通过任务队列，可以将任意数量的函数链接起来，并在稍后按顺序处理。使用 `DECLARE_TASK_QUEUE()` 宏创建新的任务队列，并使用 `queue_task()` 函数将任务加入队列。然后可以使用 `run_task_queue()` 处理任务队列。除了创建自己的任务队列（并且必须手动消耗它）之外，你还可以使用 Linux 预定义的任务队列，这些队列在已知点被消耗：

- 1. `tq_timer`：定时器任务队列，在每次定时器中断以及释放 tty 设备（关闭或释放半打开的终端设备）时运行。由于定时器处理程序在中断上下文中运行，`tq_timer` 任务也在中断上下文中运行，因此不能阻塞。
- 2. `tq_scheduler`：调度器任务队列，由调度器消耗（也在关闭 tty 设备时消耗，类似 `tq_timer`）。由于调度器在正在重新调度的进程上下文中执行，`tq_scheduler` 任务可以做任何它们喜欢的事情，即阻塞、使用进程上下文数据（尽管它们为什么要这样做呢），等等。
- 3. `tq_immediate`：这实际上是一个下半部 `IMMEDIATE_BH`，因此驱动程序可以执行 `queue_task(task, &tq_immediate)`，然后标记 `bh`（`IMMEDIATE_BH`）以在中断上下文中消耗。
- 4. `tq_disk`：由低级块设备访问（和 RAID）用于启动实际请求。此任务队列导出给模块使用，但不应用于其设计目的以外的特殊用途。

除非驱动程序使用自己的任务队列，否则它不需要调用 `run_tasks_queues()` 来处理队列，除非在以下解释的情况下例外。

如果记得驱动程序可以在队列上调度任务，而这些任务只在特定设备实例仍然有效期间才有意义——这通常意味着直到应用程序关闭它——那么 `tq_timer/tq_scheduler` 任务队列不仅在通常的地方被消耗，还在其他地方（关闭 tty 设备只是一个例子）被消耗的原因就显而易见了。因此，驱动程序可能需要调用

