
其中 `name` 是包含 `function(void)` 的结构名称。之前初始化的队列通过：

```c
INIT_WORK(work, func, void);
PREPARE_WORK(work, struct work_struct, void);
```

其中 `work` 已经声明为 `work_struct`。`INIT_WORK()` 宏初始化 `list_head` 指针，`PREPARE_WORK()` 至少设置一次，当任务在队列中激活时不应调用 `PREPARE_WORK()`。虽然可以为任务设置自己的工作队列，但在大多数情况下，默认的工作队列（事件）足够了且更容易使用。任务通过此队列添加和刷新：

```c
schedule_work(struct work_queue *q);
flush_work(struct work_struct *work);
```

注意这些是导出给所有模块的工作队列函数；其他的导出给 GPL 模块。因此，创建自己的工作队列并使用它是为内核代码保留的。可以通过可以通过创建和销毁：

```c
struct work_queue *create_queue(const char *name);
destroy_workqueue(struct work_queue *queue);
```

其中 `name` 是线程列表中使用的名称，`work_struct` 描述工作本身（需要查看）。注意 `destroy_workqueue()` 在返回之前会刷新队列。将任务添加到工作队列并进行刷新的方法：

```c
queue_work(struct work_queue *q, struct work_struct *work);
flush_work(struct work_struct *work);
```

可以为指定的时间间隔调度工作队列执行：

```c
int schedule_delayed_work(struct work_struct *work, unsigned long delay);
cancel_delayed_work(struct work_struct *work);
```

```c
DECLARE_DELAY_WORK(name, func, void);
INIT_DELAY_WORK(work, func, void);
PREPARE_DELAY_WORK(work, struct work_struct, unsigned long delay);
```

其中 `delay` 用 jiffies 表示。可以使用 `cancel_delayed_work()` 来杀死挂起的请求。当利用任务在队列上睡眠的能力时：在唤醒之前队列上没有其他任务：实现提供了一种确保在进程上下文中返回的方法：

```c
typedef void (*work_func_t)(struct work_struct *work);
struct work_struct {
```
如果从进程上下文调用，它将返回 0，`fn(data)` 将立即运行。如果从中断上下文调用此函数，它将返回 1，函数将：

```c
schedule_work(struct work_queue *q);
```

## 20.5 创建内核线程 (Creating Kernel Threads)

内核线程的执行在许多方面与代表进程的线程不同。对于它们，它们始终在内核模式下运行。创建内核线程的函数和宏用于 `/usr/src/linux/include/kthread.h`。

```c
#include <kthread.h>

struct task_struct *kthread_run(int (*start)(void), void *data, const char *namefmt, ...);
struct task_struct *kthread_create(int (*start)(void), void *data, const char *namefmt, ...);
void kthread_bind(struct task_struct *, unsigned int cpu_mask);
int kthread_stop(struct task_struct *);
```

创建的将运行 `threadfunc(data)`，它将使用 `namefmt` 和任何后续参数作为其名称，显示在 `ps` 命令中。`kthread_create()` 函数在睡眠状态初始化进程；通常人们想让内核线程执行一些工作，直到它调用 `wake_up()`。然而，人们可能想先调用 `kthread_bind()`，这会将线程绑定到特定的 CPU。通过调用 `kthread_stop()` 终止线程。这设置了 `kthread_stop_flag`，唤醒线程并等待其退出。内核线程只能从进程上下文创建，因为它们的实现会等待资源。从原子上下文调用会导致内核崩溃。

- 一个旧的函数

- `kernel_thread(int (*fn)(void), void *arg, unsigned int flags);`

仍在内核的许多地方使用。使用更复杂且需要更多工作才能完成。不应在新代码中使用。

## 20.6 线程中断处理 (Threaded Interrupt Handlers)

2.60内核引入了一种编写中断处理的方法，其中半部由调度线程调用。此功能存在于实时内核中，其目的是减少延迟，并且可以禁用中断。

API 与普通中断处理略有不同，但现在通过函数请求 IRQ：

```c
request_threaded_irq(unsigned int irq, irq_handler handler, irq_handler_t thread_fn, unsigned long flags, const char *name, void *dev);
```

新点在于第三个参数 `thread_fn`，它本质上是一个半部。上半还有一个新的返回值 `IRQ_WAKE_THREAD`，应该在线程被唤醒时使用。因此上半部运行在硬中断上下文中，必须检查中断是否源自其设备。如果不是，则返回 `IRQ_NONE`；否则，如果不需要进一步调用中断，返回 `IRQ_WAKE_THREAD`。在这种情况下，它应该禁用设备上的中断。虽然这种方法尚未渗透所有中断处理，但最终可能会取代新驱动程序中的任务。可以预计这种方法会被逐渐。

实验 1：延迟函数

编写一个驱动程序，每当对设备进行 `write()` 时调度一个延迟函数。

在调度 tasklet 时打印 `current->pid`，然后在队列函数执行时再次打印。

实现此功能：

- tasklet

- 工作队列

可以使用你在练习中使用的相同测试程序。尝试调度多个延迟函数，看看它们是按 LIFO 还是 FIFO 顺序输出。如果多次调度该函数会发生什么？

## 实验 2: 共享中断与下半部

编写一个与你的网卡共享 IRQ 的模块。你可以通过链（chaining）或日志记录（journaling）产生一些网络中断。

将其设计为上半部（top half）和下半部（bottom half）。

在模块加载时检查 `/proc/interrupts`。

让模块记录中断半部被调用的次数。

使用以下方式实现下半部：

- tasklets

- 工作队列（work queues）

- 一个在模块初始化期间启动的后台线程，该线程在数据可用时被唤醒。请确保在卸载模块时杀死该线程，否则它可能会处于僵尸状态。

对于你使用的任何方法，上半部和下半部的调用次数相等吗？如果不相等，你可以采取什么措施？

## 实验 3: 生产者/消费者

你可能已经注意到你会丢失一些下半部。当在下半部完成之前到达多个中断时，就会发生这种情况。例如，同一个 tasklet 只能被放入队列。

编写一个可以“追赶”的下半部；即在被调用时消耗多个事件，清理挂起队列。

## 实验 4: 共享所有中断与下半部

扩展解决方案以共享所有可能的的中，并评估生产者/消费者问题。

## 实验 5: 共享所有中断、下半部与生产者/消费者问题

为上一个实验的生产者/消费者问题寻找解决方案。

## 实验 6: 线程中断处理程序

如果你运行 2.6.30 或更高版本的内核，请使用线程中断处理程序（threaded interrupt handler）解决生产者/消费者问题。

介绍了两种解决方案：一种针对单个共享中断，另一种是共享所有中断，并使用与之前练习相同的延迟参数。

## 实验 7: 在进程环境中执行

编写一个执行 `execute_in_process_context()` 的模块。它应该首先在进程环境中执行（在初始化期间执行即可），然后在在中断例程中执行。

你可以将最简单的中断实验适配到此。

确保打印返回值，以判断它是直接运行了函数，还是通过工作队列运行的。

# 第 21 章

## 硬件 I/O

![](img/4e539a55ab31f2c9df39e648783d8023_131_0.png)
