
`udelay`使用启动时的`BogoMIPS`速率，你无法依赖精确的微秒级。你可能想过启动时显示的`BogoMIPS`速率意味着什么以及它的用途；它是启动时的一个校准循环，用于测量微秒速度。因此，它与硬件速度直接相关（因此被称为`BogoMIPS`，意为虚假的），但它确实提供了一种为截止日期准确指定延迟操作的方法。

> 永远不要使用`udelay`超过一两个毫秒，因为这会导致`BogoMIPS`速率高的机器上发生溢出。事实上，非常确定你真的需要延迟这个东西！如果你需要暂停比这更长，请循环指定的次数并在每次`udelay`一毫秒，如下：

```c
/* 延迟 10 毫秒 */
int i;
for (i = 0; i < 10; i++)
    udelay(1000);
```

你也可以使用`mdelay`，它是一个为你完成完全相同操作的宏：

```c
/* 延迟 10 毫秒 */
mdelay(10);
```

## 定时器

内核定时器是驱动程序中跟踪时间的极佳方法。与其循环并忙等待某个时间过期，你应该利用可用的定时器函数。正如我们之前看到的，定时器还可以用于以固定间隔轮询设备。定时器实现为双向链表，格式如下：

```c
struct timer_list {
    struct timer_list *next;
    struct timer_list *prev;
    unsigned long expires;
    unsigned long data;
    void (*function) (unsigned long);
};
```

你可以在`linux/timer.h`中找到此定义。为了简单起见，你永远不需要接触`next`和`prev`指针；事实上，你不应该这样做。内核在内部使用这些指针并为我们完成了这些工作。有趣的部分可以在`kernel/sched.c`中找到。`add_timer`负责获取必要的锁，我们实际上不需要担心`internal_add_timer`的内部工作原理。不同的锁定方案将在以后讨论SMP（对称多处理）和重入代码问题时介绍。

`init_timer`的作用完全正如提示所言——初始化定时器以供使用。在实际上，它将`next`和`prev`更新为空指针，这样重复添加的定时器将不会被察觉。这也是`schar`程序中使用的这种技术，用于检测内部定时器是否已经设置。让我们看看`schar`的代码，展示了定时器在该上下文中是如何被使用的。定时器的初始化如下：

```c
static struct timer_list schar_timer;
```

这段代码来自`init_module`，只是为稍后的使用准备定时器。

```c
init_timer(&schar_timer);
```

`schar_open`设置了定时器，前提是它还没有被另一个读取器设置过。

```c
if (!pending(&schar_timer)) {
    schar_timer.function = &schar_timer_handler;
    mod_timer(&schar_timer, SCHAR_TIMER_DELAY);
}
```

最重要的是`timer_handler`函数，它的引用被传递给`schar_timer`的函数成员值。

```c
static void schar_timer_handler(unsigned long data) {
    /* 再次设置定时器 */
    if (schar_pool < schar_pool_min) {
        schar_pool += SCHAR_INC;
        schar_timer.expires = jiffies + schar_timer_delay;
        schar_timer.function = &schar_timer_handler;
        add_timer(&schar_timer);
        MSG("setting timer up again, %ld data now\n");
    }
    /* 如果模块正在使用中，我们可能有一个读取器在等待
        数据。唤醒所有等待数据的进程。 */
    if (MOD_IN_USE && schar_pool > 0) {
        wake_up_interruptible(&schar_wq);
        wake_up_interruptible(&schar_poll_read);
    }
    return;
}
```

语法非常直观，我们不会将其解释到死。`data`在`schar`中完全没有使用，因为我们只为处理程序维护了一个定时器。我们可以为读取器和写入器都添加一个定时器，让`data`的值表示`SCHAR`或`WRITER`。

## 出处理器

与其放弃并等待某个时间过期，挂起当前执行并在稍后恢复可能是有益的。这里还有几个，但它们并不相关。如果你愿意，可以在`sched.h`中查找。

因此在调用调度器之前，将`current->state`设置为`TASK_INTERTIBLE`或`TASK_UNTIBLE`。使用哪一个取决于进程正在等待的条件。只有当在请求未就绪时让它唤醒没有意义时，才应该使用后者（不可中断状态）。对于大多数问题，情况并非如此；如果你`grep`Linux源码，你会发现一些页面实际上使用了`TASK_UNTIBLE`。然而，一个例子是属于进程的页面正在换入；我们不希望进程在任务完成之前唤醒。

演示这些原理的代码如下：

```c
current->state = TASK_INTERTIBLE;
schedule();
```

现在进程已经放弃了处理器，调度器开始运行。但我们如何知道进程何时返回？如果没有其他合适的进程可以运行，任务将被再次选中运行，我们几乎会立即回到原地。这时`schedule_timeout`登场了；你调用它而不是`schedule`，它会返回剩余睡眠的`jiffies`数量。调度器保证在指定的超时到期之前不会选择该进程进行执行。

```c
/* 让进程等待一秒 */
current->state = TASK_INTERTIBLE;
schedule_timeout(HZ);
```

# 第 18 章

该值表示进程在再次被唤醒之前应该睡眠的`jiffies`数。`schedule_timeout`的内部机制相当有趣；它是通过内核定时器辅助实现的，而`data`参数是当前进程的地址。在添加定时器后，`schedule_timeout`会调用自己。定时器只需通过`data`地址唤醒进程。如果你感兴趣，可以查看`kernel/sched.c`。

# 任务队列 (Task Queues)

我们讨论过如何使用定时器在未来的某个时间点唤醒进程。虽然定时器非常方便，但延迟执行某些工作也很有用。当我们处理中断处理程序和下半部（bottom halves）时，这一点变得特别有趣，任务队列与它们密切相关。现在我们先专注于任务队列，将中断处理的讨论留到下一节。

```c
struct tq_struct {
    struct list_head head; /* 活跃 bh 的链表 */
    unsigned long sync;      /* 必须初始化为零 */
    void (*routine)(void *);  /* 要调用的函数 */
    void *data;              /* 函数的参数 */
};
```

该定义位于`linux/queue.h`中。按照惯例，你不需要接触所有字段。`next`在内部用于将已队列的任务保持在链表中，而`sync`确保任务在运行之前不会被重复入队。这会损坏链表，因此如果你尝试将任务入队两次，该操作将被忽略。

内核中存在一些预定义的任务队列，但让我们先看看如何定义自己的：

```c
DECLARE_TASK_QUEUE(q_task);
struct tq_struct q_run = { NULL, 0, (void *)q_task_handler,
    &q_task };
```
