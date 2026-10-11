

## 一天中的时间

221

```c
usec += (xtime.tv_nsec / 1000);
} while (read_seqretry(&xtime_lock, seq));
```

该循环会重复执行，直到读取者确信在没有写入干预的情况下读取了数据。如果在中断发生并在此循环期间更新了 xtime，返回的序列号将无效，循环会再次重复。

获取墙上时间的主要用户空间接口是 `gettimeofday()`，它在 `kernel/time.c` 中实现为 `sys_gettimeofday()`：

```c
asmlinkage long sys_gettimeofday(struct timeval *tv, struct timezone *tz)
{
    if (likely(tv)) {
        struct timeval ktv;
        do_gettimeofday(&ktv);
        if (copy_to_user(tv, &ktv, sizeof(ktv)))
            return -EFAULT;
    }
    if (unlikely(tz)) {
        if (copy_to_user(tz, sys_tz, sizeof(sys_tz)))
            return -EFAULT;
    }
    return 0;
}
```

如果用户提供了非空的 `tv` 值，则调用依赖于架构的 `do_gettimeofday()`。该函数主要执行前面讨论过的 xtime 读取循环。同样，如果 `tz` 不为空，系统时区（存储在 `sys_tz` 中）将被返回给用户。如果将墙上时间或时区复制回用户空间时出现错误，该函数将返回 `-EFAULT`。否则，返回零表示成功。

内核还实现了 `time()` 系统调用，但 `gettimeofday()` 在很大程度上取代了它。C 库还提供了其他与墙上时间相关的库调用，例如 `ctime()` 和 `ftime()`。

`settimeofday()` 系统调用将墙上时间设置为指定值。它需要 `CAP_SYS_TIME` 权限。

除了更新 xtime 之外，内核对当前墙上时间的使用频率远不如用户空间高。一个显著的例外是文件系统代码，它在 inode 中存储各种时间戳（如访问时间、修改时间等）。

> 2 然而，某些架构并没有实现 `sys_time()`，而是规定通过在使用 C 库中的 `gettimeofday()` 来模拟它。

## 定时器

定时器——有时也称为动态定时器或内核定时器——对于管理内核代码中的时间流至关重要。内核代码经常需要延迟执行某个函数直到稍后的时间。在前面的章节中，我们看了半机制的使用，这对于将工作推迟到稍后处理非常有用。不幸的是，“稍后”的定义故意非常模糊。半机制的目的并不是延迟工作，而只是不在当前时刻做工作。我们需要的是一个能够延迟指定时间量的工具——肯定不会少于这个时间，而且希望不会比这长多少。解决方案就是内核定时器。

定时器使用很简单。你进行一些初始设置，指定过期时间，指定在该过期时执行的函数，然后激活定时器。给定的函数将在定时器过期后运行。定时器不是循环的。定时器在过期后会被销毁。这是其被称为“动态”的原因之一：定时器被不断地创建和销毁，并且对定时器的数量没有限制。定时器在整个内核中都很常用。

### 使用定时器

定时器由 `struct timer_list` 表示，它在 `<linux/timer.h>` 中定义：

```c
struct timer_list {
    struct list_head entry;      /* entry in linked list of timers */
    unsigned long expires;       /* expiration value, in jiffies */
    void (*function)(unsigned long);
    /* the timer handler function */
    unsigned long data;          /* lone argument to the handler */
    struct tvec_t_base_s *base;  /* internal timer field, do not touch */
};
```

幸运的是，定时器的使用不需要深入了解这个数据结构。建议不要随意修改它，以保持代码对未来变更的前向兼容性。内核提供了一组与定时器相关的接口，使定时器管理变得容易。所有内容都在 `<linux/timer.h>` 中声明。大部分实际实现位于 `kernel/timer.c`。

创建定时器的第一步是定义它：

```c
struct timer_list my_timer;
```

接下来，必须初始化定时器的内部值。这是通过一个辅助函数完成的，并且必须在调用任何定时器管理函数之前完成：

```c
init_timer(&my_timer);
```

现在，根据需要填充其余的值：

```c
my_timer.expires = jiffies + delay;  /* timer expires in delay ticks */
my_timer.data = 0;                  /* zero is passed to the timer handler */
my_timer.function = my_function;     /* function to run when timer expires */
```

`my_timer.expires` 值指定以绝对时钟滴答数为单位的超时值。当当前 `jiffies` 计数等于或大于 `my_timer.expires` 时，处理函数 `my_timer.function` 将以 `my_timer.data` 作为唯一参数运行。从 `timer_list` 的定义中可以看出，函数必须符合以下原型：

```c
void my_timer_function(unsigned long data);
```

`data` 参数允许你使用相同的处理函数注册多个定时器，并通过参数来区分它们。如果你不需要参数，可以简单地传递零（或任何其他值）。

最后，你激活定时器：

```c
add_timer(&my_timer);
```

就这样，定时器开始运行了！请注意过期值的重要性。内核在当前时钟滴答计数等于或大于指定过期值时运行定时器处理程序。虽然内核保证不会在定时器过期之前运行任何定时器处理程序，但在运行定时器时可能会有延迟。通常，定时器在其过期时间附近运行得相当接近；然而，它们可能会延迟到过期后的第一个定时器滴答才执行。因此，定时器不能用于实现任何类型的硬实时处理。

有时你可能需要修改已激活定时器的过期时间。内核实现了一个函数 `mod_timer()`，它更改给定定时器的过期时间：

```c
mod_timer(&my_timer, jiffies + new_delay);  /* new expiration */
```

`mod_timer()` 函数也可以操作已初始化但未激活的定时器。如果定时器未激活，`mod_timer()` 将激活它。如果定时器未激活，该函数返回零；如果定时器已激活，则返回一。无论哪种情况，从 `mod_timer()` 返回时，定时器都已被激活并设置为新的过期时间。

如果你需要在定时器过期之前使其失效，请使用 `del_timer()` 函数：

```c
del_timer(&my_timer);
```

该函数适用于已激活和未激活的定时器。如果定时器已经未激活，该函数返回零；否则，该函数返回一。请注意，对于已过期的定时器，你不需要调用此函数，因为它们会被自动删除。

在删除定时器时，必须防范一种潜在的竞态条件。当 `del_timer()` 返回时，它仅保证定时器不再处于活动状态（即它将来不会被执行）。然而，在多处理器机器上，定时器处理程序可能已经在另一个处理器上执行。要使定时器失效并等待可能正在执行的定时器处理程序退出，请使用 `del_timer_sync()`：

```c
del_timer_sync(&my_timer);
```

与 `del_timer()` 不同，`del_timer_sync()` 不能从中断上下文中使用。

### 定时器竞态条件

由于定时器相对于当前执行代码是异步运行的，因此存在几种潜在的竞态条件。首先，切勿将以下代码作为简单的 `mod_timer()` 的替代品，因为这在多处理器机器上是不安全的：

```c
del_timer(my_timer);
my_timer->expires = jiffies + new_delay;
add_timer(my_timer);
```

其次，在几乎所有情况下，你都应该优先使用 `del_timer_sync()` 而不是 `del_timer()`。否则，你无法假设定时器当前没有正在运行，而这正是你最初调用它的原因！想象一下，在删除定时器后，代码继续释放或操纵定时器处理程序使用的资源。因此，推荐使用同步版本。

最后，你必须确保保护在定时器处理函数中使用的任何共享数据。内核异步运行该函数，相对于其他代码而言。定时器相关的数据应按照第 8 章和第 9 章“内核同步简介”中讨论的方式进行保护。

### 定时器实现

内核在半上下文中以软中断的形式执行定时器，这在定时器中断完成后发生。定时器中断处理程序运行 `update_process_times()`，它调用 `run_local_timers()`：

```c
void run_local_timers(void)
{
    hrtimer_run_queues();
    raise_softirq(TIMER_SOFTIRQ);  /* raise the timer softirq */
    softlockup_tick();
}
```

`TIMER_SOFTIRQ` 软中断由 `run_timer_softirq()` 处理。该函数在当前处理器上运行所有已过期的定时器（如果有）。

定时器存储在链表中。然而，如果内核要么不断遍历整个列表寻找已过期的定时器，要么保持列表按过期值排序，那将是不方便的；定时器的插入和删除会变得开销很大。相反，内核根据过期值将定时器分为五组。随着过期时间的临近，定时器在这些组之间向下移动。这种分区确保了在大多数定时器软中断执行期间，内核只需做很少的工作就能找到已过期的定时器。因此，定时器管理代码是高效的。

