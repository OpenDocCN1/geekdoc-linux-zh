
# Linux 内存管理器 (早期访问)

## 脏页写回速率限制与线程节流

```c
if (pause < -HZ) {
    current->dirty_paused = now;
    current->nr_dirty = 0;
} else if (period) {
    current->dirty_paused += period;
    current->nr_dirty = 0;
} else if (current->nr_dirty_paused <= pages_dirtied)
```

```c
1785
1786    current->nr_dirtied_pause += pages_dirtied
1787    break;
1788}
1789if (unlikely(pause > max_pause)) {
1790    /* 针对偶尔性掉落的线程速率限制 */
1791    now += min(pause - max_pause, max_pause);
1792    pause = max_pause;
1793}
1794pause:
1811    set_current_state(TASK_KILLABLE);
1812    wb->dirty_sleep = now;
1813    schedule_timeout(pause);
```

**列表 10-100: mm/page-writeback.c: balance_dirty_pages() 线程使用**

我们建立了脏页写入速率限制并在 `dirty_ratelimit` 中对其限制，并根据之前确定的区域比例和 `task_ratelimit` 中的此值对其进行缩放。然后我们使用这些值通过 `wb_max_pause()`（见列表 ?）和 `wb_min_pause()`（见列表 10-96）来确定允许的最大和最小线程时间。

否则，我们将 `period` 设置为 `pages_dirtied`。`pages_dirtied` 参数被设置为当前线程的 `task_struct->nr_dirty`，即自上次以来的脏页数。我们将此结果乘以 `HZ` 以将秒转换为 jiffies。该值（以 jiffies 为单位）继续表示在速率限制下产生这些脏页所需的时间。然后，我们通过减去当前线程的 `task_struct->dirty_paused_timestamp` 来获取暂停时间，如果我们产生脏页的速度比限制允许的快，这个数字就是正数。

如果带宽更新不是空闲的（即 `struct bdi_writeback` 仍在经历着足够规律的写回），我们尝试在未来的周期内通过更新虚拟时间来进行补偿；否则只需重置，因为它可能是一个较轻的脏页产生。

最后，如果带宽更新不是空闲的（即 `struct bdi_writeback` 仍在经历着足够规律的写回，这通过检查当前时间是否小于带宽更新队列预定运行的时间点，即 `struct bdi_writeback->bw_time_stamp + BANDWIDTH_INTERVAL` 来判断）。

在此例中，调用了 `wb_update_bandwidth()`（见列表 108-92 带有 `update_ratelimit`），导致调用了 `wb_update_ratelimit()`（见列表 109-92），从而更新宽度和脏页速率统计。

（注：此处原文似乎存在逻辑重复或截断，翻译已根据上下文进行对实翻译）

**列表 10-99: mm/page-writeback.c: balance_dirty_pages() 收集统计**

我们首先确定全局脏页数量是否处于自由运行状态（freerunning regime，见图 10-13）。在这种情况下，我们完全不暂停线程。这种状态在系统中通常在大部分时间内运行。

在此例中，我们通过 `dirty_poll_interval()` 确定速率限制的轮询间隔（见列表 ??）。然后将其分配给 `struct task_struct->nr_dirty_pause` 以实现这种速率限制。

当 `struct task_struct->dirty_paused` 和 `struct task_struct->nr_dirty_fields` 此时，我们会重置它们，以表示我们认为该线程是新的，并且正在重置自上次暂停以来的脏页数。

在自由运行情况退出循环并返回后，如果我们不在自由运行状态，则我们处于全局脏页控制范围内，并应用大部分节流。因此，我们在此基础上继续执行。

我们首先通过 `wb_dirty_limits()` 确定 `bdi_writeback` 特有的脏页限制，我们之前在列表 10-89 中探讨过它。

在我们确定全局是否超过了 `struct bdi_writeback` 的脏页阈值并将其放入 `dirty_exceeded` 后，为了限制目的，我们也将其设置在 `struct bdi_writeback->dirty_exceeded` 中。

我们通过 `wb_position_ratio()` 计算全局 `struct dirty_throttle_control` 对象的区域比例（见列表 10-86），并将全局脏页节流对象的指针拷贝到 `sdtc` 中。

最后，如果带宽更新不是空闲的（即 `struct bdi_writeback` 仍在经历着足够规律的写回，这通过检查当前时间是否小于带宽更新队列预定运行的时间点，即 `struct bdi_writeback->bw_time_stamp + BANDWIDTH_INTERVAL` 来判断）。

在此例中，调用了 `wb_update_bandwidth()`（见列表 108-92 带有 `update_ratelimit`），导致调用了 `wb_update_ratelimit()`（见列表 109-92），从而更新宽度和脏页速率统计。

**列表 100. 接下来我们对调用线程进行实际解析，在下文中探讨：**

```c
/* 根据所选 dt 进行节流 */
dirty_ratelimit = READ_ONCE(wb->dirty_ratelimit);
task_ratelimit = ((u64)dirty_ratelimit * sdtc->pos_ratio) >> 
RATELIMIT_CALC_SHIFT;

max_pause = wb_max_pause(wb, sdtc->wb->dirty);
min_pause = wb_min_pause(wb, sdtc->wb->dirty_pause);
task_ratelimit, dirty_ratelimit,
nr_dirty_paused);

if (unlikely(task_ratelimit == 0)) {
    period = max_pause;
    pause = max_pause;
    goto parse;
}
period = HZ * pages_dirtied / task_ratelimit;
pause = period;
if (current->dirty_paused) {
    pause = now - current->dirty_paused;
}
```

```c
+   * 对于小于思考时间的情况（ext3/4 可能会在 I/O 中
* 阻塞高达 800ms；
* 在频率低得多的），尝试通过更新虚拟时间
* 在未来的周期内进行补偿；否则只需
* 进行重置，因为它可能是一个较轻的脏页产生。
```

```c
if (pause < -HZ) {
    current->dirty_paused = now;
    current->nr_dirty = 0;
} else if (period) {
    current->dirty_paused += period;
    current->nr_dirty = 0;
} else if (current->nr_dirty_paused <= pages_dirtied)
```

```c
1785
1786    current->nr_dirtied_pause += pages_dirtied
1787    break;
1788}
1789if (unlikely(pause > max_pause)) {
1790    /* 针对偶尔性掉落的线程速率限制 */
1791    now += min(pause - max_pause, max_pause);
1792    pause = max_pause;
1793}
1794pause:
1811    set_current_state(TASK_KILLABLE);
1812    wb->dirty_sleep = now;
1813    schedule_timeout(pause);
```

**列表 10-100: mm/page-writeback.c: balance_dirty_pages() 线程使用**

我们建立了脏页写入速率限制并在 `dirty_ratelimit` 中对其限制，并根据之前确定的区域比例和 `task_ratelimit` 中的此值对其进行缩放。然后我们使用这些值通过 `wb_max_pause()`（见列表 ?）和 `wb_min_pause()`（见列表 10-96）来确定允许的最大和最小线程时间。

否则，我们将 `period` 设置为 `pages_dirtied`。`pages_dirtied` 参数被设置为当前线程的 `task_struct->nr_dirty`，即自上次以来的脏页数。我们将此结果乘以 `HZ` 以将秒转换为 jiffies。该值（以 jiffies 为单位）继续表示在速率限制下产生这些脏页所需的时间。然后，我们通过减去当前线程的 `task_struct->dirty_paused_timestamp` 来获取暂停时间，如果我们产生脏页的速度比限制允许的快，这个数字就是正数。

（注：原文似乎存在逻辑重复或截断，翻译已根据上下文进行对实翻译）

...，因为它可能是一个较轻的脏页产生。

```c
else {
    pages = min(wb->avg_write_bandwidth / 2,
    global_wb_domain.dirty_limit / DIRTY_SCOPE);
    pages = min(pages, work->nr_pages);
    pages = round_down(pages + MIN_WRITEBACK_PAGES,
    MIN_WRITEBACK_PAGES);
}

return pages;
```

**Listing 10-102: fs/fs-rw-writeback.c: writeback_chunk_size()**

如果用户指定了回写（writeback）应该是同步的，则我们不应用任何限制，并尽可能多地进行回写。此操作部分是为了如注释所描述的那样，避免活锁（live locks）。

否则，我们可能会将任何操作限制在 `struct bdi_writeback` 对象的平均带宽上（即需要发生 1/2 次回写），或者如果数值较小，则限制为由 `DIRTY_SCOPE` 缩放后的脏数据阈值，即限制为可脏页的 1/8。

这进一步受限于 `struct wb_writeback->nr_pages` 的写入页面计数，然后向下取整到 `MIN_WRITEBACK_PAGES` 限制，该限制被设置为 4 MiB 数据（对于页大小为 4 KiB 的系统为 1024 个页）。

所有这些设计旨在启发式地避免锁问题并提高性能。

## 10.25 后台回写阈值

在检查当前 `struct bdi_writeback` 对象是否超过后台脏数据阈值时，我们使用 `wb_over_bg_thresh()`，它由 `vk_check_background_flush()` 和 `wb_writeback()` 调用。

我们在列表 10-103 中检查这一点，省略了 cgroup 的处理部分。

```c
/**
 * wb_over_bg_thresh - wb 是否需要回写？
 * @wbdi: 所关注的 bdi_writeback
 *
 * 决定后台回写是否应该继续写入 @wb 或它已经*足够干净*。
 *
 * Return: 如果应该继续回写，则返回 @true。
 */
bool wb_over_bg_thresh(struct bdi_writeback *wbdi)
{
    struct dirty_throttle_control gdtc_stor = { GDTC_INIT(wb) };

    struct dirty_throttle_control *const gdtc = &gdtc_stor;
}
```

```c
1971 unsigned long reclaimable;
1972 unsigned long thresh;
1973
1974
/*
 *  balance_dirty_pages() 但忽略了正在写入的页面，
 * 因为我们试图决定是否将更多页面放入回写状态。
 */
gdtc->avail = global_dirtyable_memory();
gdtc->dirty = global_node_page_state(NR_FILE_DIRTY);
domain_dirty_limits(gdtc);

if (gdtc->dirty > gdtc->bg_thresh)
    return true;

thresh = wb_calc_thresh(gdtc, gdtc->bg_thresh);
if (thresh < 2 * wb_stat_error())
    reclaimable = wb_stat_sum(wb, WB_RECLAIMABLE);
else
    reclaimable = wb_stat(wb, WB_RECLAIMABLE);

if (reclaimable > thresh)
    return true;

return false;
```

**Listing 10-103: mm/page-writeback.c: wb_over_bg_thresh()**

此函数类似于一个微型的 `balance_dirty_pages()`（见上面的列表 10-97），只是为了确定是否超过了后台阈值而进行了简化。

建立了一个全局的 `dirty_throttle_control` 状态对象 `gdtc`，通过 `global_dirtyable_memory()` 分配给 `avail` 的可脏内存（见列表 10-78）以及写回脏页面数量在这里并不被考虑，因为它们在通用的脏数据节流逻辑中，我们正在尝试查看是否需要回写脏页面。

我们如列表 10-88 所示通过 `domain_dirty_limits()` 建立阈值，然后简单地查看 `struct dirty_throttle_control->value` 是否超过了计算出的后台阈值。如果是，我们则返回表示阈值已突破，因为全局脏页面超过了全局后台阈值。

如果不是如此，我们在 `struct bdi_writeback` 对象的粒度上执行额外的检查。

我们调用 `wb_calc_thresh()` 来确定 `struct bdi_writeback` 指定的脏回写量，我们在列表 10-104 中检查它。

```c
776 unsigned long wb_calc_thresh(struct bdi_writeback *wb, unsigned long thresh)
777 {
778     struct dirty_throttle_control gdtc = { GDTC_INIT(wb,
779                               .thresh = thresh };
780     return __wb_calc_thresh(&gdtc);
781 }
```

**Listing 10-104: mm/page-writeback.c: __wb_calc_thresh()（见列表 10-90），使用针对 `struct dirty_throttle_control` 对象的 `__wb_calc_thresh()` 包装来传递状态。**

我们获取的 `WB_RECLAMABLE` 统计数据（注意低计数以避免不准确）指示了脏页的数量（尽管尚未被回写）。

如果这超过了 `struct bdi_writeback` 对象的硬脏阈值，我们启发式地认为这值得后台回写，从而返回表示阈值已突破，否则不返回。

# 回收与内存压力

当请求的内存超过了在不消耗内存储备的情况下当前提供的内存时，就会产生内存压力。回收（Reclaim）是内核缓解内存压力的手段。这至关重要，因为 Linux 在页缓存中大量地缓存文件数据，并允许内存过度提交。

回收有两种形式——间接回收（当区域低于水位线时发生）和直接回收（当内存降至其极值时发生）。本章将详细探讨回收机制。

**Linux 内存管理器（早期访问）© 2025 Lorenzo Stoakes 著**

`WMARK_LOW` 不允许组合 `__GFP_ATOMIC` 和 `__GFP_DIRECT_RECLAIM` 标志。

如果是这样，则发出警告并清空 `__GFP_ATOMIC`。

在 `___alloc_pages()` 中分配失败

通过 `gfp_to_alloc_flags()` 确定分配标志。

通过 `first_zones_zonelist()` 确定首选区域。

retry 标签，详见图 11-3 或图 11-4。

如果设置了 `ALLOC_KSWAPD`，则通过 `wake_all_kswapds()` 为所有节点执行间接唤醒（见第 11.4 节）。

将页面返回给调用者。

检查间接回收是否节省了我们，尝试通过 `get_page_from_freelist()` 分配，此时处于 `WMARK_MIN` 空闲水位。

是

?成功了吗？

否

如果必须遵守标记且 `order > PAGE_ALLOC_COSTLY_ORDER`，或者 `order > 1` 且分配不可移动，则可以尝试压缩。

通过 `__alloc_pages_direct_compact()` 尝试早期直接压缩。

是

尝试压缩吗？

否

如果设置了 `ALLOC_KSWAPD`，调用 `wake_all_kswapds()`，以防我们返回了睡眠。

否

成功了吗？

是
