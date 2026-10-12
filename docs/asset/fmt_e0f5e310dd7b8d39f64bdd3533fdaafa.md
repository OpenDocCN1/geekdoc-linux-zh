
`unsigned long next_jiffies;`

`ktime_t idle_expires;`

};

各个元素的使用方式如下：

- `sched_sched` 表示用于实现滴的定时器。
- 当前运行模式存储在 `nohz_mode` 中。有三种可能性：

```c
tick.h
enum tick_nohz_mode {
    NOHZ_MODE_INACTIVE,
    NOHZ_MODE_LOWRES,
    NOHZ_MODE_HIGHS,
};
```

如果周期性滴处于激活状态，则使用 `NOHZ_MODE_INACTIVE`；另外两个常量表示分别根据低分辨率和高分辨率定时器使用了动态滴。

- `idle_tick` 存储在滴被禁用之前的最后一个滴的过期时间。当滴再次启用时，知道这一点很重要，因为下一次滴必须恰好在滴从未被禁用时的相同时间出现。可以使用存储在 `idle_tick` 中的值作为基础计算出合适的时间点。通过加上足够数量的滴间隔来获得下一次滴的过期时间。否则，该值为 0。

- 如果周期性滴被停止，则 `tick_stopped` 为 1，也就是说，如果当前没有基于滴的任务需要执行。

其余字段用于簿记录：

- `idle_jiffies` 存储周期性滴被禁用时的 `jiffies` 值。
- `idle_calls` 统计内核尝试去激活周期性滴的频率。这些值有所不同，是因为如果下一次滴仅隔一个 `jiffy`，内核就不会去禁用滴。
- `idle_sleeptime` 存储周期性滴被禁用的精确时间（使用当前最佳分辨率）。
- `sleep_length` 存储滴将保持禁用状态的时间，即滴被禁用的时间与调度发生的下一次滴之间的时间差。
- `idle_sleeptime` 累积了滴被禁用期间花费的总时间。
- `next_jiffies` 存储下一个定时器过期的 `jiffy` 值。
- `idle_expires` 存储经典定时器到期的时间。与上述值不同，该值的分辨率尽可能高，且不是 `jiffies` 单位。

在 `tick_sched` 中收集的统计信息通过 `/proc/timer_list` 暴露给用户。

`tick_cpu_sched` 是一个全局每个 CPU 变量，提供一个 `struct tick_sched` 实例。这是必要的，因为禁用滴本质上是每个 CPU 工作的，而不是整个系统全局的。

## 15.2 低分辨率系统的动态滴

考虑内核不使用高分辨率定时器且仅提供低分辨率的情况。在这种场景下，动态滴是如何实现的？回想一下，定时器软中断 `htimer_run_queues` 用于处理高分辨率定时器队列，即使底层的时钟事件设备只有低分辨率。再次，我强调，这并没有为定时器提供更好的分辨率，而是使得独立于时钟分辨率使用现有框架成为。

### 切换到动态滴

`htimer_run_queues` 使用 `tick_check_oneshot_change` 来决定是否可以激活高分辨率定时器。此外，内核会检查在低分辨率系统上是否可以启用动态滴。这在两个条件下是可能的

- 可用支持单次模式的时钟事件设备。
- 未启用高分辨率。

如果两者都为假，则调用 `tick_nohz_switch_to_nohz` 来激活动态滴。然而，这最终并没有启用动态滴。如果在编译时禁用了对无滴（tickless）的支持，该函数是一个空占位函数，内核将保持在周期性滴模式。否则，内核将如图 15-19 所示运行。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_968_0.png)

**图 15-19：`tick_nohz_switch_to_nohz` 代码流程图。**

过渡到动态滴最重要的变化是将设备设置为单次模式，并安装滴处理器。新的 `handler_nohz_handler` 承担了两个责任：

1. 执行滴所需的所有操作。
2. 重新调度设备以便下一次滴过期。

满足这些要求的代码如下：

```c
kernel/time/tick_sched.c
static void tick_nohz_handler(struct clock_event_device *dev)
{
    struct tick_sched *ts = get_cpu(tick_sched);
    struct pt_regs *regs = get_regs();
    int cpu = smp_processor_id();
    ktime_t now = ktime_get();
    dev->next_event.tv64 = KTIME_MAX;
}
``` (注：原文代码中 `ktime_now = ktime_get();` 处可能存在变量定义差异，此处根据上下文保持逻辑一致性)

如果滴是激活的，那么 `tick_nohz_reprogram` 将定时器设置在下一个 `jiffy` 过期。当处理耗时过长且下一次滴位于过去时，循环确保确保成功：

```c
kernel/time/tick-sched.c
/* 当我们处于空闲状态时不重启 */
if (ts->tick_stopped)
   return;
while (tick_nohz_reprogram(ts, now)) {
   now = ktime_get();
   tick_do_update_jiffies64(now);
}
```

在 `tick_sched` 中收集的统计信息通过 `/proc/timer_list` 暴露给用户。

`tick_cpu_sched` 是一个全局每个 CPU 变量，提供一个 `struct tick_sched` 实例。这是必要的，因为禁用滴本质上是每个 CPU 工作的，而不是整个系统全局的。

### 动态滴处理器

新的 `handler_nohz_handler` 承担了两个责任：

1. 执行滴所需的所有操作。
2. 重新调度设备以便下一次滴过期。

满足这些要求的代码如下：

```c
kernel/time/tick_sched.c
static void tick_nohz_handler(struct clock_event_device *dev)
{
    struct tick_sched *ts = get_cpu(tick_sched);
    struct pt_regs *regs = get_regs();
    int cpu = smp_processor_id();
    ktime_now = ktime_get();
    dev->next_event.tv64 = KTIME_MAX;
}
```

如果 CPU 负责提供全局滴，那么调用 `tick_do_update_jiffies64` 就足够了，它会处理一切。`update_process_times` 和 `profile_tick` 接管了本地滴的职责，正如你已经多次看到过的。

关键部分是替换滴设备。如果这种滴机制被停止，CPU 将进入完全睡眠。注意 `next_event.tv64 = KTIME_MAX` 确保事件设备不会很快过期，或者在实际目的上永远不会过期

### 更新 Jiffies

全局滴设备调用 `tick_do_update_jiffies64` 来更新全局 `jiffies_64` 变量，这是低分辨率定时器处理的基础。在使用周期性滴时，这相对简单，因为每当 `jiffy` 过去就会调用该函数。当启用动态滴时，当所有系统的 CPU 都空闲并提供全局滴时，会出现解决方案。这需要 `tick_do_update_jiffies64` 考虑到。让我们直接看代码：

```c
kernel/time/tick-sched.c
static void tick_do_update_jiffies64(ktime_t now)
{
   unsigned long ticks = 0;
   ktime_t delta;
   delta = ktime_sub(now, last_jiffies_update);
}
```

由于该函数需要判断自上次更新以来是否超过了一个 `jiffy`，因此必须计算当前时间与 `last_jiffies_update` 之间的差值。

# 第 15 章：时间管理

如果上一次更新距离超过了一个 `tick` 周期（`tick period`），则自然需要更新 `jiffies`：

```c
kernel/time/tick-sched.c
if (delta.tv64 >= tick_period.tv64) {
    delta = ktime_sub(delta, tick_period);
    last_jiffies_update = ktime_add(last_jiffies_update,
                               tick_period);
}
```
