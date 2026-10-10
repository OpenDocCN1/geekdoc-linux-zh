
如果指定了超时时间，调度器可以基于优先级决定从运行队列中选择另一个进程。

> [3] 这些调度器特性随着 2.6.23 内核中 CFS 调度器的出现而发生了变化。Linux 进程调度器将在第 19 章“用户态中的驱动程序”中进行讨论。

另外两个有助于睡眠等待的函数是 `wait_event_timeout()` 和 `msleep()`。它们都是借助 `schedule_timeout()` 实现的。当你的代码希望在一个指定条件变为真或发生超时时恢复执行时，使用 `wait_event_timeout()`。`msleep()` 则用于睡眠指定的毫秒数。

这种长延迟技术仅适用于从进程上下文使用。不能从中断上下文进行睡眠等待，因为中断处理程序不允许调用 `schedule()` 或 `sleep`。（关于在中断上下文中执行代码的“应该做”和“不应该做”事项列表，请参见第 4 章中的“中断处理”。）虽然可以从中断上下文中进行短时间的忙等待，但在那种上下文中进行长时间的忙等待被视为不可饶恕的错误。同样禁忌的是在中断禁用的情况下进行长时间的忙等待。

内核还提供了定时器 API，以便在未来某个时间点执行函数。你可以使用 `init_timer()` 动态定义一个定时器，或使用 `DEFINE_TIMER()` 静态创建一个。完成此操作后，使用处理函数的地址和参数填充 `timer_list`，并使用 `add_timer()` 将其注册：

```c
#include <linux/timer.h>

struct timer_list my_timer;

init_timer(&my_timer);        /* 也可参见 setup_timer() */
my_timer.expire = jiffies + n*HZ; /* n 是以秒为单位的超时时间 */
my_timer.function = timer_func;   /* n 秒后要执行的函数 */
my_timer.data = func_parameter;   /* 传递给 timer_func 的参数 */
add_timer(&my_timer);          /* 启动定时器 */
```

请注意，这是一个单次触发的定时器。如果你想周期性地运行 `timer_func()`，还需要在 `timer_func()` 内部添加上述代码，以便在下一次超时后调度自身：

```c
static void timer_func(unsigned long func_parameter)
{
    /* 执行需要周期性完成的工作 */
    /* ... */

    init_timer(&my_timer);
    my_timer.expire   = jiffies + n*HZ;
    my_timer.data     = func_parameter;
    my_timer.function = timer_func;
    add_timer(&my_timer);
}
```

你可以使用 `mod_timer()` 更改 `my_timer` 的过期时间，使用 `del_timer()` 取消 `my_timer`，并使用 `timer_pending()` 检查 `my_timer` 当前是否处于挂起状态。如果你查看 `kernel/timer.c`，你会发现 `schedule_timeout()` 内部使用的是这些相同的 API。

像 `clock_settime()` 和 `clock_gettime()` 这样的用户空间函数用于从用户空间访问内核定时器服务。用户应用程序可以使用 `settimer()` 和 `gettimer()` 在指定超时间隔到期时控制警报信号的传递。

## 短延迟

在内核术语中，低于最小时间间隔（jiffy）的延迟属于短持续时间。这种延迟通常来自进程和中断上下文。由于不可能使用基于 jiffy 的方法来实施低于最小时间间隔的延迟，因此上一节中讨论的睡眠等待方法不能用于小超时时间。唯一的解决方案是忙等待。

实现短延迟的内核 API 包括 `mdelay()`、`udelay()` 和 `ndelay()`，它们分别支持毫秒、微秒和纳秒延迟。这些函数的实际实现是特定于架构的，并且可能并非在所有平台上都可用。

短时间的忙等待是通过测量处理器执行一条指令所需的时间，并循环必要的迭代次数来实现的。正如本章前面所讨论的，内核在启动期间执行此测量，并将值存储在一个名为 `loops_per_jiffy` 的变量中。短延迟 API 使用 `loops_per_jiffy` 来确定需要忙循环的次数。为了在手握过程中实现 1 微秒的延迟，USB 主机控制器驱动程序 `drivers/usb/host/ehci-hcd.c` 调用 `udelay()`，该函数内部使用 `loops_per_jiffy`：

```c
do {
    result = ehci_read(ehci, ptr);
    /* ... */
    if (result == done) return 0;
    udelay(1);     /* 内部使用 loops_per_jiffy */
    usec--;
} while (usec > 0);
```

## Pentium 时间戳计数器

**时间戳计数器** (TSC) 是存在于 Pentium 兼容处理器中的一个 64 位寄存器，用于计算自启动以来处理器消耗的时钟周期数。由于 TSC 以处理器周期速度递增，因此它提供高分辨率定时器。TSC 通常用于代码的性能分析和插桩。使用 `rdtsc` 指令访问 TSC，以微秒精度测量中间代码的执行时间。TSC 滴答值可以通过除以 CPU 时钟速度转换为秒，该速度可以从内核变量 `cpu_khz` 中读取。

在以下代码片段中，`low_tsc_ticks` 包含 TSC 的低 32 位，而 `high_tsc_ticks` 包含高 32 位。低 32 位取决于处理器速度可能在几秒内溢出，但对于许多代码插桩目的来说已经足够了，如下所示：

```c
unsigned long low_tsc_ticks0, high_tsc_ticks0;
unsigned long low_tsc_ticks1, high_tsc_ticks1;
unsigned long exec_time;
rdtsc(low_tsc_ticks0, high_tsc_ticks0);  /* 之前的时间戳 */
printf("Hello World\n");              /* 要分析性能的代码 */
rdtsc(low_tsc_ticks1, high_tsc_ticks1);  /* 之后的时间戳 */
exec_time = low_tsc_ticks1 - low_tsc_ticks0;
```

在 1.8GHz Pentium 机器上，测量的 `exec_time` 为 871（或半微秒）。

对高分辨率定时器（`CONFIG_HIGH_RES_TIMERS`）的支持已合并到 2.6.21 内核中。它利用特定于硬件的高速定时器为 `nanosleep()` 等 API 提供高精度功能。在 Pentium 级机器上，内核利用 TSC 来提供此功能。

## 实时时钟

RTC 在非易失性内存中跟踪绝对时间。在 x86 PC 上，RTC 寄存器构成了由电池供电的一小块 [4] *互补金属氧化物半导体* (CMOS) 内存顶部的少数位置。在第 5 章“字符驱动程序”中的图 5.1 中，可以看到传统 PC 架构中 CMOS 的位置。在嵌入式系统中，RTC 可能是处理器内部的，或者通过第 8 章“I²C 和 SPI 协议”中讨论的 I²C 或 SPI 总线外部连接。

> [4] RTC 电池可以使用多年，通常比计算机的使用寿命更长，因此你永远不需要更换它们。

你可以使用 RTC 执行以下操作：

- 读取和设置绝对时钟，并在时钟更新期间生成中断。
- 生成频率从 2HZ 到 8192HZ 不等的周期性中断。
- 设置闹钟

许多应用程序需要绝对时间或 *wall time* 的概念。因为 `jiffies` 是相对于系统启动时间的，所以它不包含 wall time。内核在一个名为 `xtime` 的变量中维护 wall time。在启动期间，通过读取 RTC 将 `xtime` 初始化为当前的 wall time。当系统停止时，wall time 被写回 RTC。你可以使用 `do_gettimeofday()` 以硬件支持的最高分辨率读取 wall time：

```c
#include <linux/time.h>
static struct timeval curr_time;
do_gettimeofday(&curr_time);
my_timestamp = cpu_to_le32(curr_time.tv_sec); /* 记录时间戳 */
```

还有一些功能可供用户空间代码访问 wall time。它们包括以下函数：

- `time()`，返回日历时间，即自纪元（1970 年 1 月 1 日 00:00:00）以来的秒数
- `localtime()`，以分解格式返回日历时间
- `mktime()`，执行与 `localtime()` 相反的操作

从用户空间使用 RTC 的另一种方法是使用字符设备 `/dev/rtc`。一次只允许一个进程访问此设备。

我们将在第 5 章和第 8 章中更多地讨论 RTC 驱动程序。在第 19 章中，我们开发了一个示例用户应用程序，它使用 `/dev/rtc` 以微秒精度执行周期性工作。

