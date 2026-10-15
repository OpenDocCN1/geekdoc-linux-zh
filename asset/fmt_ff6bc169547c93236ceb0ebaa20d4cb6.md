
`cv_timedwait_sig()` — 测试定时器过期。如果定时器已过期，`cv_timedwait_sig()` 返回 `-1`，除非存在待挂信号；此时，返回 `0`。如果两个条件均为假，`cv_timedwait_sig()` 调用 `realtime_timeout()` 设置调用队列条目并处理 `SC_BLOCK` 激活。如果为假，`cv_timedwait_sig()` 调用 `cv_block_sig()`。从 `cv_block_sig()` 返回后，测试是否有待挂信号。如果存在待挂信号，`cv_timedwait_sig()` 调用 `setrun()`；否则调用 `swwtch()`。如果 `SC_BLOCK` 激活为真，`cv_timedwait_sig()` 移除线程超时并返回 `-1`，除非存在待挂信号，则返回 `0`。

上述所有入口都指向内核代码 `cv_block()` 和 `cv_block_sig()`，后者只是在线程中设置 `T_WAKEABLE` 标志并调用 `cv_block()`。`cv_block()` 对各种状态标志进行额外检查，并通过 `CL_SLEEP()` 宏调用类特定的睡眠函数，这对于 TS 类线程解析为 `ts_sleep()`。`ts_sleep()` 代码的意图是在标记了提升标志时提高线程的优先级。结果是，`kthread` 被放置在睡眠队列的最优位置，以便在发生唤醒时进行快速调度。否则，根据线程等待运行的时间重置优先级。

并不是每次进入 `ts_sleep()` 都会为内核线程分配 `SYS` 优先级。线程结构中的标志以及 `kthread` 的类特定数据（TS 类中的 `ts_data`）指定了是否需要内核优先级。如果线程持有读/写锁或内存页锁，则标记 `SYS` 优先级。对于大多数情况，不需要 `SYS` 优先级，因此不会分配给线程。RT 类没有睡眠例程；因此不需要优先级调整。`ts_sleep()` 函数如伪代码所示：

## Solaris 内核调度器

```
ts_sleep() {
    if (SYS priority requested) /* t) kpri_req flag *
        在 kthread 中设置 TSXPRI 标志
        将 t_pri 设置为请求的 SYS 优先级 /* t_pri = ts_kpris[arg] *
        设置 kthread 返回标志 /* ts_trapret *
        设置线程睡眠标志 /* ..., .astflag *
    else if (ts_diswait = ts_maxwait /* 线程等待 *
        计算新的用户模式优先级
        设置 ts_timeleft = ts_dptbl(ts_cpupri).ts_quantum
        设置 ts_diswait = *
        在线程中设置全局优先级 (t_pri)
        if (线程优先级 < 调度队列最大优先级)
            调用 cpu_surrender() /* 抢占 *
    else if (已经是 SYS 优先级)
        将线程设置为 TS 类优先级
    清除 kthread 中的 TSKPRI 标志
        if (线程优先级 < 调度队列最大优先级)
            调用 cpu_surrender() /* 抢占 *
}
```

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

如果线程等待了长时间，则进入上述 `ts_sleep()` 第二段中的线程优先级设置。

等待，该序列在图 9.15 中以图形形式表示。

![图 9.15 在 ts_sleep() 中设置线程优先级](img/a866795bf21add85c994851c49.png)

代码将返回 `cv_block()`，其中 `kthread` 的 `wchan` 设置为条件变量的地址，`kthread` 的 `obj_ops` 设置为条件变量操作的地址。

## 头文件 `<sys/subject.h>`

如果你查看 `/usr/include/subject.h`，你会找到同步对象操作的定义。

```
typedef struct _sobj_ops {
    syncobj_t sobj_type;
    kthread_t (*sobj_owner)();
    void (*sobj_unsleep)(kthread_t *);
    void (*sobj_change_pri)(kthread_t *, pri_t, pri_t);
} sobj_ops_t;
```

这是一个通用结构，用于操作系统支持的所有类型的同步对象。注意同一头文件中的枚举成员；它们描述了……该对象为同步对象特定的几个例程提供了占位符，这些例程在内核线程睡眠期间可能需要调用。在条件变量的情况下（示例），`sobj_ops` 结构填充了 `cv_owner()`、`cv_unsleep()` 和 `cv_change_pri()` 函数的地址，并将 `sobj_type` 设置为 `SOBJ CV`。

当正确设置 `kthread` 的等待通道（wait channel）和同步对象指针后，通过对条件变量地址进行哈希找到正确的睡眠队列，并插入 `sleepq` 头部。接下来，增加条件变量中的 `cv_waiters` 字段以反映另一个内核在对象上发生阻塞，并将线程状态设置为 `TS_SLEEP`。调用 `sleep_insert()` 函数将内核插入睡眠队列中的正确位置（基于优先级）。现在 `kthread` 处于 `TS_SLEEP` 状态，正在等待唤醒。

### 9.3.4 唤醒机制

对于每一个 `cv_wait()`（或变体），都有对应的唤醒调用使用 `cv_signal()`、`cv_broadcast()` 或 `cv_unsleep()`。在实践中，当前的 Solaris 版本没有调用 `cv_unsleep()`。`cv_signal()` 唤醒一个线程，而 `cv_broadcast()` 唤醒在同一条件变量上睡眠的所有线程。以下是唤醒事件的序列。

- `cv_broadcast()` 函数通过对作为参数传递的条件变量地址调用哈希函数，简单地定位睡眠队列的地址，清除条件变量中的 `cv_waiters` 字段（所有线程都将唤醒，因此条件变量应该反映出零等待线程），并调用 `sleepq_wakeall(chan)`。

+ 在 Solaris 7 中，`sleep_wakeall_chan()` 会遍历等待该特定条件变量的内核线程链表，并对每个 `kthread` 调用 `sleep_pq_unlink()`。`sleep_pq_unlink()` 将该 `kthread` 从睡眠队列链表中移除，调整指针（`t_prifront`、`t_prback`）并返回到 `sleep_wakeall_chan()`。

+ 在返回到 `sleep_wakeall_chan()` 时，`kthread` 的 `t_chan` 和 `t_sobj_ops` 字段会被清除，并调用特定调度调度类的唤醒代码。

对于 TS/IA 线程，代码是 `ts_wakeup()`；对于 RT 线程，代码是 `rt_wakeup()`。在 Solaris 2.5 和 Solaris 2.6 中，队列是一个单链表，`kthread` 中包含 `t_link` 指针。

Solaris 2.5 和 Solaris 2.6 并没有 `sleep_unlink()` 函数，因此 `sleep_wakeall_chan()` 会将每个线程从列表中移除，并将线程的 `t_link`、`t_chan` 和 `t_sobj_ops` 字段设置为 `NULL`。

+ `cv_signal()` 通过对条件变量的地址进行哈希，在 `sleep_head` 数组中定位正确的索引，条件变量中的 `cv_waiters` 字段减 1（因为只有一个线程将获得唤醒），并调用 `sleep_wakeone_chan()`。

+ `ts_wakeup()` 将内核线程放回调度队列，以便其在处理器上执行。
