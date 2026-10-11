
唯一的参数是期望的相对时间，单位为 `jiffies`。这个示例让任务进入为期 `s` 秒的可中断睡眠状态。因为任务被标记为 `TASK_INTERRUPTIBLE`，如果它接收到信号，将会提前唤醒。如果代码不处理信号，你可以使用 `TASK_UNINTERRUPTIBLE`。在调用 `schedule_timeout()` 之前，任务必须处于这两个状态之一，否则任务将不会睡眠。

注意，`schedule_timeout()` 会调用调度器；调用它的代码必须具备睡眠的能力。关于原子性和睡眠的讨论，请参考第 8 章和第 9 章。简而言之，你必须处于进程上下文且不持有锁。

## schedule_timeout() 实现

`schedule_timeout()` 函数非常直观。事实上，它是内核功能的一个简单应用，让我们来看它：

```c
signed long schedule_timeout(signed long timeout)
{
    struct timer timer;
    unsigned long expire;
    switch (timeout)
    {
        case MAX_SCHEDULE_TIMEOUT:
            schedule();
            goto out;
        default:
            if (timeout < 0)
            {
                printk(KERN_ERR "schedule_timeout: wrong timeout "
                      "value %lx from %p\n", timeout,
                      builtin_return_address(0));
                current->state = TASK_RUNNING;
            }
            goto out;
    }
}
```

```c
expire = timeout + jiffies;
```

```c
init_timer(&timer);
```

![](img/8bb65552497e0232bdfb63c158183c4f_254_0.png)

```c
timer.expires = expire;
timer.data = (unsigned long) current;
timer.function = process_timeout;
```

```c
add_timer(&timer);
schedule();
del_timer_sync(&timer);
```

`timeout = expire - jiffies;`

```c
out:
    return timeout < 0 ? 0 : timeout;
```

该函数创建了一个名为 `timer` 的定时器，并设置它在指定的定时器时钟周期后过期。它设置定时器在过期时执行 `process_timeout()` 函数。然后，它启用定时器并调用 `schedule()`。由于任务被挂起在 `TASK_INTERRUPTIBLE` 或 `TASK_UNINTERRUPTIBLE` 状态下，调度器不会运行该任务，而是选择一个新任务。

当定时器过期时，它运行 `process_timeout()`：

```c
void process_timeout(unsigned long data)
{
    wake_up_process((task_struct *) data);
}
```
