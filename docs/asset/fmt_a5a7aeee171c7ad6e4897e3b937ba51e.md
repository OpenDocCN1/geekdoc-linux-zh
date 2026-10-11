
`MODULE_DESCRIPTION("This is button platform driver");`

# int_imx_key.ko

```
root@imx7dev:~# insmod int_imx_key.ko /* 加载模块 */
```

按下按钮产生中断
```
root@imx7dev:~# cat /proc/interrupts /* 查看 linux中断号 (20) 和硬件中断号 (10)，用于 gpio 控制 */
root@imx7dev:~# rmmod int_imx_key.ko /* 移除模块 */
```

# 第 7 章 设备驱动程序中的中断处理

## 延迟工作 (Deferred Work)

Linux内核在两种文中执行操作：

1. **进程上下文 (Process context)**：当内核代表用户进程执行操作（例如执行系统调用）时所处的模式。由工作队列（Workqueues）和线程中断（threaded interrupts）调度的延迟工作执行在进程文中；这些线程在内核空间运行，但不代表任何用户进程。进程文中的代码可以阻塞。

2. **中断上下文 (Interrupt context)**：来自硬件中断（异步请求）。这种特殊上下文也称为“原子上下文”，因为在该文中执行的代码无法阻塞。另一方面，中断是不可调度的。中断发生并执行中断处理程序产生自己的上下文。软中断、任务链（tasklets）和定时器在中断文中运行，这意味着它们不能调用阻塞函数。

延迟工作是一类内核机制，允许在稍后调度执行代码。这些调度的代码可以通过工作队列或线程中断在进程文中运行，也可以通过软中断、任务链和定时器在中断文中运行。总而言之，延迟工作的主要类型是内核线程和软中断。工作队列和线程中断的中断部实现在可以阻塞的内核线程之上，而任务链和定时器实现在不能调用函数的软中断之上。

![](img/6ae71abd6b0ad652145782465527d4b_284_0.png)

延迟工作用于补充中断处理程序的功能，因为中断有重要的要求和局限性：

- 中断处理程序的执行时间必须尽可能小

- 在中断文中，你不能使用阻塞调用

通过延迟工作，你可以在中断处理程序中执行最少的工作，并调度一个异步操作在稍后运行以执行剩余操作。这种用于中断的延迟工作也称为下半部（bottom-half），因为其目的是执行来自中断处理程序（上半部）的剩余动作。**上半部 (top-half)** 执行需要立即完成的事情，即关键任务。基本上，上半部就是中断处理程序。由于所有中断都是禁用的，它应该尽快完成。它调度下半部来处理复杂的处理。**下半部 (bottom-half)** 执行剩余的处理——即依赖性的、不关键的操作。它由 ISR 信号。下半部用于处理数据，让上半部处理新进入的中断。当下半部运行时，中断是开启的。如果必要，可以禁用中断下半部，但通常应避免这样做，因为这违背了下半部的基本目的——在监听新中断的同时处理数据。中断下半部在 Linux 中实现为中断文中软中断和任务链，或通过进程文中线程中断实现。

## 软中断 (Softirqs)

软中断是运行在中断文中下半部处理的形式，适用于长时间的非阻塞处理程序。它们在所有中断处理程序完成后执行，在内核恢复调度进程之前，因此不允许睡眠。软中断尽可能早地执行，但保持可中断状态，以便执行可以被任何上半部抢占。驱动程序无法使用软中断，它们为各种内核子系统保留。由于由于原因，在编译时定义了固定数量的软中断。对于当前内核版本，类型如下：

每种类型都有特定的用途：

- `HI_SOFTIRQ` 和 `TASKLET_SOFTIRQ` - 运行 tasklet

- `TIMER_SOFTIRQ` - 运行定时器

- `NET_TX_SOFTIRQ` 和 `NET_RX_SOFTIRQ` - 用于网络子系统

- `BLOCK_SOFTIRQ` - 用于 I/O 子系统

- `BLOCK_JOPOLL_SOFTIRQ` - 用于 I/O 子系统，在 iopoll 处理程序被调用时提高性能

- `SCHED_SOFTIRQ` - 负载均衡

- `HRTIMER_SOFTIRQ` - 高精度定时器的实现

- `RCU_SOFTIRQ` - RCU 类型机制的实现

优先级最高的是 `HI_SOFTIRQ` 类型软irqs，之后是定义的其他 softirqs。`RCU_SOFTIRQ` 的优先级最低。

Softirqs 在中断上下文中运行，这意味着它们不能调用阻塞函数。如果 softirq 处理程序需要调用此类函数，可以调度工作队列（work queues）来执行这些阻塞调用。

![](img/6ae71abd6b0ad6512145782465527d4b_286_0.png)

### Tasklets

Tasklet 是延迟工作的一种特殊形式，与 softirqs 一样在中断上下文中运行。softirqs 与 tasklets 之间的主要区别在于 tasklets 可以动态分配，因此它们可以被设备驱动使用。tasklet 由 `struct tasklet` 表示，与其他许多内核结构一样，它在在使用之前需要进行初始化。

Tasklets 在 `HI` 和 `TASKLET` softirqs 中执行。它们在所有中断开启的情况下执行，由给定的 tasklet 保证一次只在单个 CPU 上执行。一个预初始化的 tasklet 可以定义为：

```
void handler(unsigned long data);
DECLARE_TASKLET(tasklet, handler, data);
DECLARE_TASKLET_DISABLED(tasklet, handler, data);
```

如果你想使用 `tasklet_init()` 函数手动初始化 tasklet。tasklet 简单地实现为一个函数。与 softirqs 相，单个设备驱动可以轻松地使用 tasklets。

```
void handler(unsigned long data);
struct tasklet_struct tasklet;
tasklet_init(&tasklet, handler, data);
```

中断处理程序可以通过以下方式调度 tasklet 执行：

```
void tasklet_schedule(struct tasklet_struct *tasklet);
void tasklet_hi_schedule(struct tasklet_struct *tasklet);
```

当使用 `tasklet_schedule` 时，会调度一个 `TASKLET_SOFTIRQ` softirq 并运行所有调度的 tasklet。对于 `tasklet_hi_schedule`，会调度一个 `HI_SOFTIRQ` softirq。

### 定时器

定时器是一种非常经常使用的延迟工作类型。它们由 `timer_list` 结构定义。它们在中断上下文中运行，并在 softirqs 之上实现。要使用定时器，必须首先调用 `setup_timer()` 进行初始化：

```
void setup_timer(struct timer_list *timer,
               (*function)(unsigned long),
               unsigned long data);
```

前一个函数初始化了结构的内部字段，并将函数与定时器处理程序关联。

调度定时器通过 `mod_timer()` 完成：

```
int mod_timer(struct timer_list *timer, unsigned long expires);
```

其中 `expires` 参数是未来运行处理程序函数的时间。该函数可以用于在处理函数内部调度或重新调度定时器。

定时器的时间单位是 `jiffie`。一个 jiffie 的绝对值取决于平台，可以使用 `HZ` 宏来查找，它定义了 1 秒的 jiffies 数。在 jiffies（jiffies_value）和秒（seconds_value）之间转换，使用的公式如下：

```
jiffies_value = seconds_value * HZ;
seconds_value = jiffies_value / HZ;
```

内核维护了一个计数器，包含自上次启动以来的 jiffies 数量，可以通过 `jiffies` 全局变量或宏访问。你可以用它为定时器计算未来的时间：

```
#include <linux/jiffies.h>
unsigned long current_jiffies, next_jiffies;
unsigned long seconds = 1;

current_jiffies = jiffies;
next_jiffies = jiffies + seconds * HZ;
```
