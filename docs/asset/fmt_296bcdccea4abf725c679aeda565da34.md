
函数 `second_overflow()` 来自第 15.2.4.1 节，用于处理闰秒和时钟加速。在代码的位置，它被调用一次。

## 15.2.3 通过一个滴答更新时间钟

定时器中断被用于更新计算机时间钟等。但由于此中断频率的微小不规则，时钟在一段时间内可能会快或慢。使用了复杂的算法同步外部时间源。该源更新内核变量，然后由本节及后续节中的函数读取。在描述按一个定时器中断相应量更新时钟函数之前，我们必须首先检查代码中的许多常量。

### 15.2.3.1 定点值

通常，时间量以整数微秒存储，但在某些情况下需要更高的精度，因此时间值以定点格式存储。高位表示整数微秒，低位表示二进制分数（1/2、1/4 等）。使用纳秒存储值似乎更有逻辑，但 32 位字段不足以存储所有涉及的值。

即使使用定点，也不可能让所有值的小数位于位于相同。花费了大量精力确保变量永不溢出或下溢。这导致使用了多种不同的缩放因子。图 15.12 来自 `<linux/timex.h>` 显示了控制这些定点值的常量。

```c
92 #define SHIFT_KG 6
95 #define MAXTC 6
111 #define SHIFT_SCALE 22
112 #define SHIFT_UPDATE (SHIFT_KG+MAXTC)
113 #define SHIFT_USEC 16
114 #define FINEUSEC (1L << SHIFT_SCALE)
115
116 #define MAXPHASE 512000L
117 #define MAXFREQ (512L << SHIFT_USEC)
118 #define MAXTIME (200L << PPS_AVG)
119 #define MINSEC 1L

121 #define NTP_PHASE_LIMIT (MAXPHASE << 5)
```

图 15.12 时间常数和小数点

该因子用于阻尼第 15.2.4.4 节所示锁相环中的调整量。

结合上一行的 `SHIFT_KG`，`MAXTC` 用于建立第 112 行 `SHIFT_UPDATE` 的值。

这在 `time_phase` 变量中建立了小数点，用于积累时钟领先或落后的微秒分数。这在实际上是时钟微秒字段的扩展。其用法在第 15.2.3.2 节中讨论。

这是本地时钟与外部源之间允许的最大差异，单位为微秒。它的初始化值为 512.000 μs。

这是本地时钟频率与外部源频率之间的最大差异。它初始化为 512，格式为 `SHIFT_USEC`。

这是在接收每秒脉冲（PPS）信号时可接受的最大误差。`PPS_AVG` 是平均常数 (2)。

这是更新之间的最小间隔，单位为秒。

如果使用了 NTP 协议，则这是 NTP 时间与本地时间之间可以处理的最大差异。它是 `MAXPHASE` 的 32 倍，即 16 秒。

## 15.2.3.2 推进日期时间时钟滴答（clock tick）

图 15.13 所示的来自 `kernel/timer.c` 的函数将时钟的微秒字段增加一个滴答（tick），并考虑了任何为实现的减速或加速调整。它在每次定时器中断时被调用一次。

```
38 int tickadj = 500/HZ ? 1;
56 long time_phase;
59 long time_adj; /* tick adjust (scaled 1/HZ) */
62 long time_adjust;
63 long time_adjust_step;
463 static void update_wall_time_one_tick(void)
464 {
465 if ((time_adjust_step = time_adjust) != 0) {
475 if (time_adjust > tickadj)
476 time_adjust_step = -tickadj;
477 else if (time_adjust < -tickadj)
478 time_adjust_step = -tickadj;
481 time_adjust -= time_adjust_step;
483 xtime.tv_usec += tick + time_adjust_step;
488 time_phase += time_adj;
489 if (time_phase <= -FINEUSE) {
490 long ltemp = -time_phase >> SHIFT_SCALE;
491 time_phase += ltemp << SHIFT_SCALE;
492 xtime.tv_usec -= ltemp * ltemp;
493 }
else if (time_phase >= FINEUSE) {
495             ltemp = time_phase >> SHIFT_SCALE;
496             time_phase -= ltemp << SHIFT_SCALE;
497             xtime.tv_use += ltemp;
498                                }
499                                }
```

图 15.13 通过一个滴答更新时钟

- 38 这是在调整运行快或运行慢的时钟时，每个滴答可以进行的最大调整。它始终以微秒测量。如果 `HZ` 小于 500（标准 HZ 为 100），则 `500/HZ` 为正。在这种情况下，`tickadj` 的值为 `500/HZ`，但如果 `HZ` 大于 500，则 `tickadj` 将为 0。在这种情况下，它被设置为最小 1 微秒。

- 56 该变量用于累计时钟领先或落后的微秒分数，因此它被用作 `xtime` 微秒字段的扩展。它以缩放微秒的形式维护，用 `SHIFT_SCALE`（22 位）建立小数点。

- 59 这是在每次定时器中断时时钟必须调整或延迟的微秒分数。因为它是一个分数，所以它以缩放格式维护。它通过 `second_overflow()` 更新（见第 15.2.4.4 节和 15.2.4.5 节）。

- 62 该变量仅在系统连接到外部时间源时使用。在这种情况下，在每个同步点，微秒的总调整（向后或向前）会被写入那里。`update_wall_time_one_tick()` 函数返回此值，按一定量更新时钟，并减少相应数量的 `time_adjust`。

- 63 这是每个滴答调整日期时间时钟的微秒数，因此它是 `time_adjust` 的一个分数。它在 `update_wall_time_one_tick()` 函数内部使用。

- 465–482 如果时钟与外部源不同步，则不会一次性更新。大的跳跃（特别是回拨）可能会导致依赖时间戳的子系统（例如文件系统）不一致。相反，在每个滴答更新日期时间时钟时，会对要增加的微秒数进行微小的调整。这段代码计算时钟是否需要调整，如果需要，调整多少。

- 465 `time_adjust` 变量指示时间是否需要调整，如果需要，调整多少。这由外部源设置，因此在这里将被读取。如果没有外部源，它仍具有 0 的私有值，并将跳过第 475–482 行。如果 `time_adjust` 不为零，意味着时钟将运行更快（正值）或更慢（负值）。`time_adjust_step` 变量是每个滴答微秒字段增加的量。

- 475–478 时钟的任何调整都不会一次性完成，而是分多个步骤完成。这种步骤被限制在 `-tickadj ... +tickadj` 范围内执行。如果调整量（`time_adjust`）足够小，则可以在一步内完成。

- 475–476 如果 `time_adjust` 大于 `tickadj`，则 `time_adjust_step` 设置为 `-tickadj`。

- 477–478 如果 `time_adjust` 小于 `-tickadj`，则 `time_adjust_step` 设置为 `-tickadj`。

- 481 `time_adjust` 减去 `time_adjust_step`。

- 483 `xtime.tv_usec` 增加 `tick + time_adjust_step`。

- 488 `time_phase` 增加 `time_adj`。

- 489 如果 `time_phase` 小于等于 `-FINEUSE`，

- 490 `long ltemp = -time_phase >> SHIFT_SCALE;`

- 491 `time_phase` 增加 `ltemp << SHIFT_SCALE`。

- 492 `xtime.tv_usec` 减去 `ltemp * ltemp`。

- 493 如果 `time_phase` 大于等于 `FINEUSE`，

- 495 `ltemp = time_phase >> SHIFT_SCALE;`

- 496 `time_phase` 减去 `ltemp << SHIFT_SCALE`。

- 497 `xtime.tv_use` 增加 `ltemp`。

## 15.2.4 精炼时钟准确性
