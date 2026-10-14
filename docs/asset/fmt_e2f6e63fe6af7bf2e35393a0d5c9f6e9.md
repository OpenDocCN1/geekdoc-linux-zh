
# 调度器使用的宏

`idle_task()` 返回一个代表空闲进程的 `task_struct` 指针。`can_schedule()` 返回给定的进程是否可以调度到特定的 CPU 上。来自 `kernel/sched.c` 的图 7.17 显示了这两个宏的替代形式，一种用于 SMP 情况，另一种用于单处理器情况。

```c
#ifdef CONFIG_SMP
#define idle_task(cpu) (init_tasks(cpu))
#define can_schedule(p, cpu) ((p)->cpus_allowed & (1UL << cpu))
#else
#define idle_task(cpu) (1)
#define can_schedule(p, cpu) (1)
#endif
```

## 7.4.2 计算进程的 `goodness`

图 7.18 展示了 `kernel/sched.c` 中的 `goodness()` 函数，相关讨论见第 7.1.3 节。

**第 180–181 行**

如果考虑的进程使用的是与当前进程相同的内存上下文，或者它没有自己的内存上下文，则它将获得 1 的加成。在第一种情况下，它是同一个进程中的线程；在第二种情况下，它是一个内核线程。在这两种情况下，如果被选中，都不需要更改内存上下文。

该行添加了根据 `nice` 计算的进程优先级。由于 `nice` 的范围从 -20（高优先级进程）到 +19（最低优先级进程），因此该值将是从 40（最高优先级）到 1（最低优先级）的数值。

时间片（quantum）跳过了第 191 行中针对实时进程的权重，以及刚刚计算的结果。

如果该进程不是 `SCHED_OTHER` 进程，那么它必须是 `SCHED_FIFO` 或 `SCHED_RR`。这些是实时固定优先级进程。在这种情况下，函数返回进程的实时优先级，并增加 1000。这保证了没有任何交互式进程能够超过它。因此，实际上，`rt_priority` 最高的进程将在下一次被调度。

### 7.4.3 确定进程的时间片

每次执行重新调度时，所有进程（无论就绪还是等待）的计数器字段（即时间片）都会被补充。图 7.19 中 `kernel/sched.c` 的代码显示了如何确定给任何特定进程的时间片。

```c
#if HZ < 200
#define TICK_SCALE(x) ((x) >>2)
#elif HZ < 400
#define TICK_SCALE(x) ((x)>>1)
#elif HZ < 800
#define TICK_SCALE(x) (x)
#elif HZ < 1600
#define TICK_SCALE(x) ((x)<<1)
#else
#define TICK_SCALE(x) ((x)<<2)
#endif
#define NICE_TO_TICKS(nice) (TICK_SCALE(20-(nice))+1)
```

图 7.19 确定时间片

- 59–69 时间片以节拍（ticks）或系统时钟中断为单位测量，因此当为特定进程确定时间片时，必须按照中断时钟的频率进行比例缩放。速度快的机器应该赋予更多的节拍。`TICK_SCALE()` 宏正是这样做的。
- 61–62 对于 `HZ` 小于 200 的，时间片除以 2。
- 63–64 对于 `HZ` 在 400 到 800 之间的，时间片不进行调整。
- 65–66 对于 `HZ` 在 800 到 1600 之间的，时间片乘以 2。
- 67–68 对于 `HZ` 超过 1600 的，时间片乘以 4。
