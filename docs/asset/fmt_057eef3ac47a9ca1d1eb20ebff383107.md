
在这里，`p->run_list` 在 `task_struct` 结构体内声明为 `struct list_head run_list`，并作为列表的锚点。从列表中删除元素和添加（到列表的头或尾）是通过 `list_del()` / `list_add()` / `list_add_tail()` 宏完成的。下面的示例是将任务添加和从运行队列中移除：

```c
static inline void del_from_runqueue(struct task_struct * p)
{
    nr_running--;
    list_del(&p->run_list);
    p->run_list.next = NULL;
}

static inline void add_to_runqueue(struct task_struct * p)
{
    list_add(&p->run_list, &runqueue_head);
    nr_running++;
}

static inline void move_last_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add_tail(&p->run_list, &runqueue_head);
}

static inline void move_first_runqueue(struct task_struct * p)
{
    list_del(&p->run_list);
    list_add(&p->run_list, &runqueue_head);
}
```

## 2.5 等待队列

当进程请求内核做当前不可能但稍后可能变得可能的某件事时，进程会被挂起（睡眠），并在请求更有可能得到满足时被唤醒。用于此目的的内核机制之一是称为“等待队列”。

Linux 实现允许使用 `TASK_EXCLUSIVE` 标志进行唤醒语义。使用等待队列时，你可以使用一个众所周知的队列，然后简单地使用 `sleep_on` / `sleep_on_timeout` / `interruptible_sleep_on` / `interruptible_sleep_on_timeout`，或者你可以定义自己的等待队列，并使用 `add_wait_queue` / `remove_wait_queue` 将自己添加或移除，并在需要时使用 `wake_up()` / `wake_up_interruptible()` 进行唤醒。

等待队列第一种用法的示例是页分配器（在 `mm/page_alloc.c` 中；`__alloc_pages()`）和 `kswapd` 内核守护进程（在 `mm/vmscan.c` 中；`kswapd()`）之间的交互，通过等待队列 `kswapd_wait` 实现，该队列在 `mm/vmscan.c` 中声明；`kswapd` 守护进程在此队列上睡眠，每当页分配器需要释放一些页面时，它会被唤醒。

自主等待队列用法的示例是通过 `read(2)` 系统调用请求数据的用户进程和在中断上下文中运行以提供数据的内核之间的交互。中断处理程序可能如下所示（简化的 `drivers/char/rtc_interrupt()`）：

```c
static DECLARE_WAIT_QUEUE_HEAD(rtc_wait);
void rtc_interrupt(int irq, void *dev_id, struct pt_regs *regs)
{
    spin_lock(&rtc_lock);
    rtc_irq_data = CMOS_READ(RTC_INTR_FLAGS);
    spin_unlock(&rtc_lock);
    wake_up_interruptible(&rtc_wait);
}
```

因此，中断处理程序通过从某个设备特定的 I/O 端口读取数据（`CMOS_READ()` 宏转化为几对 `outb` / `inb`）来获取数据，然后唤醒在 `rtc_wait` 等待队列上睡眠的人。

现在，`read(2)` 系统调用可以这样实现：

```c
ssize_t rtc_read(struct file file, char *buf, size_t count, off_t *ppos)
{
    DECLARE_WAITQUEUE(wait, current);
    unsigned long data;
    ssize_t retval;
    add_wait_queue(&rtc_wait, &wait);
    current->state = TASK_INTERRUPTIBLE;
    do {
        spin_lock_irq(&rtc_lock);
        data = rtc_irq_data;
        rtc_irq_data = 0;
        spin_unlock_irq(&rtc_lock);

        if (data != 0)
            break;

        if (file->f_flags & O_NONBLOCK) {
            retval = -EAGAIN;
            goto out;
        }
        if (signal_pending(current)) {
            retval = -ERESTARTSYS;
            goto out;
        }
        schedule();
    } while(1);

    retval = put_user(data, (unsigned long *)buf);

    if (!retval)
        retval = sizeof(unsigned long);

out:
    current->state = TASK_RUNNING;
    remove_wait_queue(&rtc_wait, &wait);
    return retval;
}
```

`rtc_read()` 中发生的事情如下：

1. 我们声明一个等待队列元素，指向当前进程上下文。
2. 我们将该元素添加到 `rtc_wait` 等待队列中。
3. 我们将当前上下文标记为 `TASK_INTERRUPTIBLE`，这意味着在下一次休眠后它不会被重新调度。
4. 我们检查是否有数据可用；如果有，我们跳出循环，将数据复制到用户缓冲区，将自身标记为 `TASK_RUNNING`，从等待队列中移除自身并返回。
5. 如果尚未有数据，我们检查用户是否指定了非阻塞 I/O；如果是，则以 `EAGAIN`（等同于 `EWOULDBLOCK`）失败。
6. 我们还检查是否有挂起的信号；如果有，则通知“上层”在必要时重启系统调用。这里“必要时”指的是 `sigaction(2)` 系统调用中指定的信号处置细节。
7. 然后我们“切换出去”，即进入睡眠状态，直到被中断处理程序唤醒。如果我们没有将自身标记为 `TASK_INTERRUPTIBLE`，调度器可能会在数据可用之前更早地调度我们，从而导致不必要的处理。

值得指出的是，使用等待队列，实现 `poll(2)` 系统调用非常容易：

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
