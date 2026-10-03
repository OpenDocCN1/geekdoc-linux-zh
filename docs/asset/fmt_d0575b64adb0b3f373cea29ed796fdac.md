
## 脏节流逻辑探索

我们从此处开始探索的脏节流逻辑涉及一些精细的数学计算。与其纠结于这些，我们将检查核心函数，将数学细节留给读者作为练习题。

注意在此函数以及许多其他函数中，对整数操作方式的选择非常仔细，例如在这里通过 `roundup_of_two()` 使用。为了简单起见，我们不仔细检查这些，而是关注该值最终代表什么。

注意该函数通过 `writeback` 参数传递了 `struct bdi_writeback->stats`。我们从 `struct bdi_writeback->written_stamp` 中减去上次获取带宽时的值。我们尝试获取一个在硬编码的 3 秒周期内的滚动平均值（与 `HZ` 值相乘以将其转换为内核时间）。如果 `elapsed` 周期恰好超过了这个写周期，则我们直接取写带宽（平滑写周期）并退出函数。否则，我们计算带宽等于 `period + elapsed`，提供硬编码 3 秒周期的滚动平均值。从 `struct bdi_writeback->write_bandwidth` 获取此值后，我们对之前的平均值进行一些仔细的平滑，将其赋值给 `struct bdi_writeback->avg_write_bandwidth`。

### 代码示例：带宽更新逻辑

```c
if (avg > 0 && avg >= (unsigned long)bw) {
    avg = (old - avg) >> 3;
}

if (avg < 0 && avg <= (unsigned long)bw) {
    avg += (old - avg) >> 3;
}

out:
/* 保持 avg > 0 以保证如果存在脏 wbs 则 tot > 0 */
avg = max(avg, 1L);

if (wb_has_dirty(wb)) {
    long delta = avg - wb->avg_write_bandwidth;
    WARN_ONCE(atomic_long_add(delta, &wb->to_write_bandwidth) <= 0);
}

wb->write_bandwidth = bw;
WRITE_ONCE(wb->avg_write_bandwidth, avg);
```

## 脏位置控制比例

在检查脏率计算之前，让我们思考在 `struct dirty_throttle_control->pos_ratio` 中维护的脏位置比例。该值在 `wb_position_ratio()` 中确定，我们在列表 10-86 中检查。如所述，这是一个我们用于缩放脏率限制的系数，使每个线程在回写压力下收敛于目标，限制在 0 到 2 之间，允许脏率较低时翻倍，或在脏率高到阻塞块设备时变为硬限制。我们在图 14 中检查该值如何维护。其意图是保持位置比例为 1，仅当脏率与线程数缩放不同时才变化。

脏位置控制比例在 `wb_position_ratio()` 中确定，我们在列表 10-86 中检查。为了简单省略了块限制的处理（由 `BDI_CAP_STRICT` 指定）以及会使函数过于复杂的注释。

### 列表 10-86：mm/page-writeback.c: wb_position_ratio()

```c
static void wb_position_ratio(struct dirty_throttle_control *dtc)
{
    struct bdi_writeback *wb = dtc->wb;
    unsigned long line_bw = READ_ONCE(wb->avg_bandwidth);
    unsigned long freerun = dirty_freerun(dtc->thresh, dtc->bg_thresh);
    unsigned long limit = hard_dirty_limit(dtc_dom(dtc), dtc->thresh);
    unsigned long wb_thresh = dtc->wb_thresh;
    unsigned long x;
    unsigned long setpoint;               /* 脏页的目标平衡点 */
    unsigned long wb_setpoint;
    unsigned long span;
    unsigned long pos_ratio;               /* 用于缩放速率限制 */
    long x_intercept;

    dtc->pos_ratio = 0;

    if (unlikely(dtc->dirty >= limit))
        return;

    setpoint = (freerun + limit) / 2;

    pos_ratio = pos_ratio_polynom(setpoint, dtc->dirty, limit);

    /*
     * 我们上面根据全局情况计算了基本的 pos_ratio。
     */

    /*
     * 如果 wb 超过/低于其脏页份额，我们希望
     * 进一步调低/调高 pos_ratio。这是通过以下机制实现的。
     */

    if (unlikely(wb_thresh > dtc->thresh))
        wb_thresh = dtc->thresh;

    /*
     * wb_thresh 接近 0 可能并不是因为设备
     * 慢，而是因为很长时间没有活动。
     * 决定一个合理的（希望 IO 高效的）
     * 阈值，这样偶尔的写入就不会被阻塞，
     * 活跃的写入可以快速增加阈值。
     */

    wb_thresh = max(wb_thresh, limit - dtc->dirty) / 8;

    /* 将全局 setpoint 缩放到 wb 的：
     * wb_setpoint = setpoint * wb_thresh / thresh
     */

    x = div_u64((u64)wb_thresh << 16, dtc->thresh | 1);
    wb_setpoint = setpoint * (u64)x >> 16;

    /*
     * 在单一 wb 情况下，如 (thresh - wb_thresh ~= 0) 所示，
     * 使用 span=(8*write_bw)，并在 JBOD 情况下过渡到 wb_thresh。
     */

    /*
     * wb_thresh thresh - wb_thresh
     * span * (8 * write_bw) + * wb_thresh
     * thresh thresh
     */

    span = (dtc->thresh - wb_thresh + 8 * line_bw) * (u64)x >> 16;

    x_intercept = wb_setpoint + span;

    if (dtc->wb_dirty >= x_intercept) {
        pos_ratio = div64_u64(pos_ratio * (x_intercept - wb_setpoint),
                              (x_intercept - dtc->wb_dirty) | 1);
    } else {
        pos_ratio /= 4;
    }

    /*
     * wb 预留区域，防止脏页池溢出和磁盘
     * 闲置
     * 它可能会将全局脏页的控制点推得
     * 比设置点更高。
     */
    x_intercept = wb_thresh / 8;
    if (dtc->wb_dirty < x_intercept) {
        if (dtc->wb_dirty > x_intercept / 8)
            pos_ratio = div_u64(pos_ratio * x_intercept,
                                dtc->wb_dirty);
        else
            pos_ratio *= 8;
    }
    dtc->pos_ratio = pos_ratio;
}
```

我们不会深入探讨数学原理，而是将对该逻辑进行一些简单的观察。

如果全局脏页数量超过了脏阈值（在 `limit` 中指定），则我们不计算该比例，而是将其设置为零，从而获得最大的进程暂停。

我们注意到，设置点（`setpoint`）被确定为 `dirty_freerun()` 确定的 `freerun` 值（见列表 10-80）与 `hard_dirty_limit()` 确定的脏阈值之间的中间值（由于 cgroup writeback 不在本书的讨论范围内，我们只考虑该值等于全局脏阈值的情况）。

`dirty_freerun()` 函数将 `freerun` 区域确定在后台阈值和脏阈值之间的中间位置，这使得设置点确定为该值与脏阈值之间的中间值。

默认情况下，`vm.dirty_background_ratio` 被设置为可写内存的 10%，而 `vm.dirty_ratio` 被设置为 20%。这意味着由于故障导致的 `freerun`（即未尝试节流脏页）最多可应用到可写内存的 15%，设置点为 17.5%。

虽然我们不会检查数学推导，但观察列表 10-87 中的 `pos_ratio_polynom()` 是很有启发意义的。

### 列表 10-87：mm/page-writeback.c: pos_ratio_polynom()

```c
/*
 * setpoint - dirty
 * f(dirty) := 1.0 + (--------------------)
 *    limit - setpoint
 *
 * 这是一个三次多项式，受限于
 * (1) freerun = 2.0 => 足够快地增加脏页 dirty_ratelimit
 * (2) f(setpoint) = 1.0 => 平衡点
 * (3) flimit = 0 => 硬限制
 * (4) df/dx < 0 => 负反馈控制
 * (5) 越接近设置点，|df/dx| 越小（反之亦然）
 * => 对大误差响应迅速；在设置点附近振荡较小
 */

static long long pos_ratio_polynom(unsigned long setpoint,
                                   signed long dirty,
                                   signed long limit)
{
    long long pos_ratio;
    long long x;

    x = div64_s64((s64)dirty - (s64)setpoint << RATELIMIT_CALC_SHIFT,
                  (limit - setpoint) | 1);
    pos_ratio = x;
    pos_ratio = pos_ratio * x >> RATELIMIT_CALC_SHIFT;
    pos_ratio = pos_ratio * x >> RATELIMIT_CALC_SHIFT;
    pos_ratio += 1 << RATELIMIT_CALC_SHIFT;

    return pos_ratio;
}
```

值得注意的是，采用这些长度是为了使用整数进行此计算（内核无法安全地执行浮点运算），为了绕过脏页速率（该比例实际上是脏页速率的浮点倍数），我们通过 `RATELIMIT_CALC_SHIFT`（10 位）对计算进行位移，并在完成后移回。

该函数计算的比例为 `1 + (setpoint - dirty) / (limit - setpoint)`，其中 `dirty` 是脏页总数，`limit` 是脏阈值。

该比例在脏页数量与设置点之间发散，占全局脏页控制范围（设置点到脏阈值之间）的比例，即如果此范围较小，则比例更高；如果很大则反之。

如果脏页数量超过设置点，该方程的第二部分将为负值，导致脏页速率缩小；否则为正值，导致脏页节流率放大。

回到列表 10-86 中的 `wb_position_ratio()`，我们观察到一旦获得此 `pos_ratio` 值，我们必须考虑脏 `bdi_writeback` 特定阈值相对于全局脏阈值 `struct dirty_throttle_control->thresh` 的比例。

因此我们获得了一个缩放后的 `bdi_writeback` 特定设置点，等于 `setpoint * wb_thresh / thresh`，然后用于相应地缩放 `pos_ratio`。

我们再次跳过该函数的数学细节，因为它们在某种程度上超出了本书范围。

## 脏限制

在我们检查了全局和 `bdi_writeback` 特定的阈值后，让我们看看这些值是如何计算的。全局值在 `domain_dirty_limits()` 中计算，如列表 10-88 所示（writeback 逻辑不在范围内）。

### 列表 10-88：mm/page-writeback.c: domain_dirty_limits()

```c
/**
 * domain_dirty_limits - 为 bdi 计算 thresh 和 bg_thresh
 * @dtc: 感兴趣的 dirty_throttle_control
 */
static void domain_dirty_limits(struct dirty_throttle_control *dtc)
{
    unsigned long available_memory = dtc->avail;
    unsigned long dirty_bytes;
    unsigned long bg_bytes;
    /* 将比例转换为 PAGE_SIZE */
    unsigned long ratio = (vm_dirty_ratio * PAGE_SIZE) / 100;
    unsigned long bg_ratio = (vm_dirty_background_ratio * PAGE_SIZE) / 100;
    unsigned long thresh;
    unsigned long bg_thresh;
    struct task_struct *tsk;

    if (vm_dirty_bytes)
        thresh = DIV_ROUND_UP(vm_dirty_bytes, PAGE_SIZE);
    else
        thresh = (ratio * available_memory) / PAGE_SIZE;

    if (vm_dirty_background_bytes)
        bg_thresh = DIV_ROUND_UP(vm_dirty_background_bytes, PAGE_SIZE);
    else
        bg_thresh = (bg_ratio * available_memory) / PAGE_SIZE;

    if (bg_thresh >= thresh)
        bg_thresh = thresh / 2;

    tsk = current;

    if (rt_task(tsk)) {
        bg_thresh += bg_thresh / 4 + global_wb_domain.dirty_limit / 32;
        thresh += thresh / 4 + global_wb_domain.dirty_limit / 32;
    }
    dtc->thresh = thresh;
    dtc->bg_thresh = bg_thresh;
}
```

该函数从 `vm_dirty_bytes` 全局变量获取值并将其放入字节数，从 `vm_dirty_background_bytes` 获取并放入字节数，从 `vm_dirty_ratio` 获取并放入 `ratio`，从 `vm_dirty_background_ratio` 获取并放入 `bg_ratio`。

代码随后应用这些可调参数——如果指定了 `vm_dirty_bytes`，则计算阈值（以页为单位）并按页面大小对齐；否则，如果指定了 `vm_dirty_ratio`，则取该比例并乘以 `struct dirty_throttle_control->avail`（之前已设置为列表 10-78 所示通过 `global_dirtyable_memory()` 计算的可用脏字节数），并除以页面大小以获得存储的阈值页数。

同样的过程也适用于存储在 `bg_thresh` 中的背景阈值。

最后，我们考虑背景阈值错误地大于脏阈值的情况，这是不允许的。在这种情况下，我们将背景阈值设置为脏阈值的一半。

对于具有实时优先级的线程有一些特殊处理，会增加阈值，然后将 `domain_dirty_limits()` 的 `thresh` 和 `bg_thresh` 字段赋值为上述计算值。

我们在 `wb_dirty_limits()` 中确定 `bdi_writeback` 特定的阈值，该函数见列表 10-89。

### 列表 10-89：mm/page-writeback.c: wb_dirty_limits()

```c
static inline void wb_dirty_limits(struct dirty_throttle_control *dtc)
{
    struct bdi_writeback *wb = dtc->wb;
    unsigned long wb_reclaimable;
    /*
     * wb_thresh 不像 dirty_thresh 那样被视为限制因素，
     * 原因如下：
     * - 在 JBOD 设置中，wb_thresh 波动很大
     * - 在带有硬盘和 U 盘的系统中，U 盘可能会以某种方式
     *   进入状态 (wb_dirty >> wb_thresh)，要么是因为
     *   wb dirty 初始很高，要么是因为 wb_thresh 降得很低。
     */
}
```
