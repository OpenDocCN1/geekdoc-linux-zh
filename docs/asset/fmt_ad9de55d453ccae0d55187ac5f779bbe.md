
- **中断上下文**：根据硬件中断控制器的请求（异步）。这种特殊上下文也是“原子上下文”，因为在该上下文中执行的代码无法阻塞。相反，中断是不可调度的。它们发生并执行中断处理程序，产生自己的上下文。`softirqs`、`tasklet` 和定时器运行在中断文中，这意味着它们不能调用阻塞函数。

延迟工作允许将上下文调度到稍后的点执行。被调度的代码可以通过**工作队列**或**线程中断**在进程文中运行（这两种方法都使用内核线程），也可以在中断文中通过**softirqs**、**tasklets**和**定时器**运行。工作队列和线程中断的中半部分是构建在可以阻塞的内核线程之上的，而 `tasklet` 和定时器是构建在不能调用阻塞函数的 `softirqs` 之上的。

## 第7 章

延迟工作被用于补充中断处理程序的功能，因为中断具有重要的要求和局限性：

- 中断处理程序的执行时间必须尽可能短。
- 在中断上下文（`interrupt context`）中，你不能使用阻塞调用。

在使用延迟工作时，你可以在中断处理程序中执行最少的时间敏感性必要工作，并从中断处理程序调度一个异步操作，在稍后中断开启时执行。

这种在中断中的延迟工作也被称为下半部（`bottom-half`），因为它的目的是执行来自中断处理程序（上半部，`top-half`）的剩余操作。上半部执行需要立即完成的任务，即对时间敏感的任务。基本上，上半部本身就是中断处理程序。上半部应该尽可能快完成，因为此时所有中断都是禁用的，它会调度下半部来处理复杂的逻辑。下半部执行延迟的剩余处理——即与时间相关的、不那么重要的操作。它由 `ISR`（中断服务程序）信号。下半部用于处理数据，让上半部处理新进入的中断。当下半部运行时，中断是开启的。如有必要，可以禁用中断，但通常应该避免这样做，因为这违背了下半部的基本目的——在监听新中断的同时处理数据。中断下半部在 Linux 中实现为中断上下文中的 `softirqs` 和 `tasklets`，或者通过进程上下文中的线程中断（`threaded irqs`）实现。

### Softirqs

`Softirqs` 运行在中断上下文中，指示执行对时间最敏感且重要的不需要睡眠的下半部处理工作。它们在所有中断处理程序完成并被任何上半部中断抢占后执行。设备驱动程序无法使用 `softirqs`，因为它们为内核子系统预留；编译时定义了固定数量的 `softirqs`。

```c
enum {
    HI_SOFTIRQ = 0,
    TIMER_SOFTIRQ,
    NET_TX_SOFTIRQ,
    NET_RX_SOFTIRQ,
    BLOCK_SOFTIRQ,
    IRQ_POLL_SOFTIRQ,
    TASKLET_SOFTIRQ,
    SCHED_SOFTIRQ,
    HRTIMER_SOFTIRQ,
    RCU_SOFTIRQ,
    NR_SOFTQS
};
```

### 在设备驱动程序中处理中断

每个类型都有特定的用途：

- `HI_SOFTIRQ` 和 `TASKLET_SOFTIRQ` -- 运行 `tasklets`（任务队列）。
- `TIMER_SOFTIRQ` -- 运行定时器。
- `NET_TX_SOFTIRQ` 和 `NET_RX_SOFTIRQ` -- 用于网络子系统。
- `BLOCK_SOFTIRQ` -- 用于 IO 子系统。
- `BLOCK_JOPOLL_SOFTIRQ` -- 用于 IO 子系统，在调用 `iopoll` 处理程序时提高性能。
- `SCHED_SOFTIRQ` -- 负载均衡。
- `HRTIMER_SOFTIRQ` -- 高精度定时器的实现。
- `RCU_SOFTIRQ` -- RCU 类型机制的实现。

优先级的是 `HI_SOFTIRQ` 类型 `softirqs`，之后是定义的其他 `softirqs`。`RCU_SOFTIRQ` 的优先级最低。

`Softirqs` 运行在中断上下文中，这意味着它们不能调用阻塞函数。如果 `softirq` 处理程序需要调用此类函数，必须调度工作队列（`work queues`）来执行这些阻塞调用。

### Tasklets

`Tasklet` 是一种构建在 `softirqs` 之上的运行在中断上下文中的下半部机制。`softirqs` 和 `tasklets` 的主要区别是 `tasklets` 可以动态分配，因此可以被设备驱动程序使用。`tasklet` 由 `tasklet` 结构体表示，并在使用前需要根据所需的其他内核结构进行初始化。

`Tasklets` 在 `HI` 和 `TASKLET` `softirqs` 中执行。它们在所有中断开启的情况下执行，给定的 `tasklet` 保证一次在一个 CPU 上执行。一个预初始化的 `tasklet` 定义如下：

```c
void handler(unsigned long data);
DECLARE_TASKLET(tasklet, handler, data);
DECLARE_TASKLET_DISABLED(tasklet, handler, data);
```

如果你想手动初始化 `tasklet`，请使用 `tasklet_init()` 函数。`tasklet` 简单地实现为一个函数。与 `softirqs` 不同，单个设备驱动程序就可以可以使用 `tasklets`。

```c
void handler(unsigned long data);
struct tasklet_struct tasklet;
tasklet_init(&tasklet, handler, data);
```

中断处理程序可以使用以下函数调度 `tasklet` 的执行：

```c
void task_schedule(struct tasklet_struct *tasklet);
void task_hi_schedule(struct tasklet_struct *tasklet);
```

使用 `tasklet_schedule()` 时，会调度一个 `TASKLET_SOFTIRQ` `softirq`，并且所有的 `tasklets` 都被调度为运行状态。对于 `tasklet_hi_schedule()`，则调度一个 `HI_SOFTIRQ` `softirq`。

### Timers

定时器是运行在中断上下文中基于 `softirqs` 的一种延迟工作类型，常用于 Linux 驱动程序。它们由 `timer_list` 结构定义。要使用定时器，必须先调用 `setup_timer()` 进行初始化：

```c
void setup_timer(struct timer_list *timer,
void (*function)(unsigned long),
unsigned long data);
```

```c
static struct miscdevice led_miscdevice = {
    .minor = MISC_DYNAMIC_MINOR,
    .name = "ledred"
};

static int __init_probe(struct platform_device *pdev) {
    int result, ret_val;
    struct device *dev = &pdev->dev;
    dev_info(dev, "platform_probe entry\n");
    s_pGpioRegisters = (struct GpioRegisters*)pdev->dev_iomap(dev, GPIO_BASE,
                        sizeof(struct GpioRegisters));

    SetGGPIOFunction(LedGpioPin, 0b001); /* Configure the pin as output */

    setup_timer(&s_BlinkTimer, BlinkTimerHandler, 0);
    result = mod_timer(&s_BlinkTimer, msecs_to_jiffies(s_BlinkPeriod));

    ret_val = device_create_file(&pdev->dev, &dev_attr_period);
    if (ret_val != 0) {
        dev_err(dev, "failed to create sysfs entry\
```

## 设备驱动中的中断处理

```c
.probe = my_probe,
.remove = my_remove,
.driver = {
    .name = "ledred",
    .of_match_table = my_of_ids,
    .owner = THIS_MODULE,
};
```

`module_platform_driver(my_platform_driver);`

`MODULE_LICENSE("GPL");`

`MODULE_AUTHOR("Alberto Liberal <aliberal@arroweurope.com>");`

`MODULE_DESCRIPTION("This is a blinking led driver");`
