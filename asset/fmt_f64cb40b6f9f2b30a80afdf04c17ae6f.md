
### 代码片段：`shrink_inactive_list()` 实现 (第 1 部分)

```c
2401 static unsigned long
2402 shrink_inactive_list(unsigned long nr_to_scan, struct lruvec *lruvec,
2403                      struct scan_control *sc, enum lru_list lru)
2404 {
2405     LIST_HEAD(page_list);
2406     unsigned long nr_scanned;
2407     unsigned int nr_reclaimed = 0;
2408     unsigned long nr_taken;
2409     struct reclaim_stat stat;
2410     bool file = is_file_lru(lru);
2411     enum vm_event_item item;
2412     struct pglist_data *pgdat = lruvec_pgdat(lruvec);
2413     bool stalled = false;
2414 
2415     while (unlikely(too_many_isolated(pgdat, file, sc))) {
2416         if (stalled)
2417             return 0;
2418         /* 等待回收器一会。 */
2419         stalled = true;
2420         reclaim_throttle(pgdat, VMSCAN_THROTTLE_ISOLATED);
2421         /* 我们正要死亡并释放我们的内存。现在返回。 */
2422         if (fatal_signal_pending(current))
2423             return SWAP_CLUSTER_MAX;
2424     }
```

### 代码片段：`shrink_inactive_list()` 实现 (第 2 部分)

```c
2425     lru_add_drain();
2426 
2427     spin_lock_irq(&lruvec->lru_lock);
2428     nr_taken = isolate_lru_pages(nr_to_scan, lruvec, &page_list,
2429                                  &nr_scanned, sc, lru);
2430     spin_unlock_irq(&lruvec->lru_lock);
2431 
2432     if (nr_taken == 0)
2433         return 0;
2434 
2435     nr_reclaimed = shrink_page_list(&page_list, pgdat, sc, &stat, false);
2436 
2437     spin_lock_irq(&lruvec->lru_lock);
2438     move_pages_to_lru(lruvec, &page_list);
2439     spin_unlock_irq(&lruvec->lru_lock);
2440 
2441     lru_note_cost(lruvec, file, stat.nr_pageout);
2442 
2443     free_unref_page_list(&page_list);
2444 
2445     /*
2446      * 如果扫描了未进入 IO 队列的脏页，
2447      * 意味着刷新器（flushers）没有尽工作。
2448      * 这发生在内存压力将脏页推到 LRU 末尾，但尚未突破脏
2449      * 限制且脏数据尚未过期时。也可能发生在脏页
2450      * 比例的增长不是因为写入，而是通过内存
2451      * 压力回收了所有干净缓存。在某些情况下，
2452      * 刷新器简单无法跟上分配
2453      * 速率。如果刷新器处于睡眠状态，则通知它们。
2454      */
2455     if (stat.nr_unqueued_dirty == nr_pages)
2456         wakeup_flusher_threads(WB_REASON_VMSCAN);
2457 
2458     sc->nr_dirty += stat.nr_dirty;
2459     sc->nr_congested += stat.nr_congested;
2460     sc->nr_unqueued_dirty += stat.nr_unqueued_dirty;
2461     sc->nr_writeback += stat.nr_writeback;
2462     sc->nr_immediate += stat.nr_immediate;
2463     sc->nr_taken += nr_taken;
2464     if (file)
2465         sc->nr_file_taken += nr_taken;
2466 
2467     return nr_reclaimed;
2468 }
```

### 列表 11-61: `mm/vmscan.c:shrink_inactive_list()`

`shrink_inactive_list()` 是通过初始化一组局部变量来实现的，包括我们用于存储待考虑回收的隔离 folio 的 `page_list`。然后我们检查是否需要通过 `too_many_isolated()` 进行节流。我们希望尝试批量处理此类情况，以便一次性删除它们，而不是逐个删除，因此将这些 folio 添加到 `folio_to_free` 列表中，并在跳到下一个 folio 之前，清除其 LRU 特有的 `PG_lru`、`PG_active` 和 `PG_unevictable` 标志。

否则，我们通过 `lruvec_add_folio()` 将 folio 添加到指定的 LRU 列表（参见列表 11-13 和第 11.2.2 节）。

然后，我们通过 `folio_nr_pages()` 计算我们移动的基础页数量，并累加到 `nr_moved` 中。

最后，我们将所有待释放的 folio 放入输入列表以供调用者释放（这样做是为了效率考虑），在返回移动的基础页计数之前。

```c
/*
 * 如果扫描了未进入 IO 队列的脏页，
 * 意味着刷新器（flushers）没有尽工作。
 * 这发生在内存压力将脏页推到 LRU 末尾，但尚未突破脏
 * 限制且脏数据尚未过期时。也可能发生在脏页
 * 比例的增长不是因为写入，而是通过内存
 * 压力回收了所有干净缓存。在某些情况下，
 * 刷新器简单无法跟上分配
 * 速率。如果刷新器处于睡眠状态，则通知它们。
 */
if (stat.nr_unqueued_dirty == nr_pages)
    wakeup_flusher_threads(WB_REASON_VMSCAN);

sc->nr_dirty += stat.nr_dirty;
sc->nr_congested += stat.nr_congested;
sc->nr_unqueued_dirty += stat.nr_unqueued_dirty;
sc->nr_writeback += stat.nr_writeback;
sc->nr_immediate += stat.nr_immediate;
sc->nr_taken += nr_taken;
if (file)
    sc->nr_file_taken += nr_taken;

return nr_reclaimed;
```

### 列表 11-62: `mm/vmscan.c:too_many_isolated()`

`too_many_isolated()` 函数只考虑直接回收，因为后台回收无法像直接回收那样扩展。我们统计不活跃页的总数，并将其与隔离页的数量进行比较。如果隔离页超过不活跃页的八分之一，我们通过 `throttle()` 触发回收节流（参见列表 11-75 和第 11.6 节）。在内存压力下，大量任务尝试分配，我们会隔离大量 folio 以考虑回收，这可能导致 LRU 缩小并产生抖动和 OOM。

```c
/*
 * 直接回收器可能会从 LRU 列表中隔离大量的 folio
 * 以进行重新调度，导致 LRU 缩小并产生抖动
 * 和 OOM。
 */
static int too_many_isolated(struct pglist_data *pgdat, int file,
                             struct scan_control *sc)
{
    unsigned long inactive, isolated;
    bool too_many;

    if (current_is_kswapd()) {
        return 0;
    }

    if (file) {
        inactive = page_state(pgdat, NR_INACTIVE_FILE);
        isolated = page_state(pgdat, NR_ISOLATED_FILE);
    } else {
        inactive = page_state(pgdat, NR_INACTIVE_ANON);
        isolated = page_state(pgdat, NR_ISOLATED_ANON);
    }

    /* GFP_IO 或 GFP_FS 分配允许隔离更多的页，不会被直接回收阻塞。 */
    if ((sc->gfp_mask & (GFP_IO | GFP_FS)))
        inactive >>= 3;

    too_many = isolated > inactive;

    /* 因为太多，唤醒被限制的任务。 */
    if (!too_many) {
        wake_throttle(pgdat);
    }
    return too_many;
}
```

---

### `shrink_page_list()` 主循环逻辑

图 11-22: `shrink_page_list()` 主循环逻辑

我们在代码列表 11-63 中检查了 `shrink_page_list()`（省略了范围外的实时调度钩子、cgroup 逻辑、调试断言、巨页逻辑、NUMA 降级、统计更新、buffer 空闲头部和热插拔支持）。

### 列表 11-63: `mm/vmscan.c:shrink_page_list()` (第 1 部分)

```c
1589 static unsigned int shrink_page_list(struct list_head *page_list,
1590                                      struct pglist_data *pgdat,
1591                                      struct scan_control *sc,
1592                                      struct reclaim_stat *stat,
1593                                      bool ignore_references)
1594 {
1595     LIST_HEAD(ret_pages);
1596     LIST_HEAD(free_pages);
1597     unsigned int nr_reclaimed = 0;
1598     memset(stat, 0, sizeof(*stat));
1599 
1600 retry:
1601     while (!list_empty(page_list)) {
1602         struct address_space *mapping;
1603         struct folio *folio;
1604         enum page_references references = PAGEREF_RECLAIM;
1605         bool dirty, writeback;
1606         unsigned int nr_pages;
1607 
1608         folio = lru_to_folio(page_list);
1609         list_del(&folio->lru);
1610 
1611         if (!folio_trylock(folio))
1612             goto keep;
1613 
1614         nr_pages = folio_nr_pages(folio);
1615 
1616         /* Account the number of base pages */
1617         sc->nr_scanned += nr_pages;
1618 
1619         if (unlikely(folio_test_evictable(folio)))
1620             goto activate_locked;
1621 
1622         if (!sc->may_unmap && folio_mapped(folio))
1623             goto keep_locked;
1624     }
```

我们首先初始化本地状态，包括 `ret_pages` 列表，这些我们将通过 `page_list` 返回给调用者的 folio，以便将其放入合适的 LRU 列表——我们不能回收它们；以及 `free_pages` 列表，用于那些我们已经回收并准备好释放的 folio，我们会在操作结束时对其进行批量释放。

在循环期间，我们通过 `lru_to_folio()` 从孤立 folio 输入列表的尾部读取一个 folio，并通过 `list_del()` 将该 folio 从输入列表中删除。

稍后我们会在循环结束时将未回收的 folio 附加（拼接）到空输入列表末尾，这些 folio 将返回给调用者以放回相应的 LRU。

在每次迭代中，我们乐观地尝试锁定 folio——当我们有其他可以考虑回收的 folio 时，我们不希望阻塞。如果我们在代码列表 11-69 中看到这些标签：

如果 folio 被驱逐（已锁定）或通过 `folio_test_evictable()` 检查被标记为不可驱逐，那么我们就激活它，以便让它避开可以回收的 folio。

如果 folio 被用户态映射，但 `struct scan_control->may_unmap` 为 `false`，则我们不被允许取消映射，无法回收它，并让它一直旋转到列表末尾。

在确保可以继续后，我们检查回写（writeback）folio，我们在代码列表 11-64 中检查了它们。

### 列表 11-64: `mm/vmscan.c:shrink_page_list()` - Writeback 处理

```c
/*
 * 脏页数量决定了节点是否被标记
 * reclaim_congested。如果 LRU 尾部全是脏的未队列 folio，
 * kswapd 仍会停止并写入 folio。
 */
folio_check_writeback(folio, &dirty, &writeback);
if (dirty || writeback)
    stat->nr_dirty += nr_pages;

if (dirty && !writeback)
    stat->nr_unqueued_dirty += nr_pages;

/*
 * 如果 folio 在 LRU 中的循环速度之快，
 * 以至于标记为立即回收的 folio 第二次到达
 * LRU 末尾，则将此 folio 视为拥塞。
 */
if (writeback && folio_test_reclaim(folio))
    stat->nr_congested += nr_pages;

if (folio_test_writeback(folio)) {
    if (current_is_kswapd() &&
        folio_test_reclaim(folio) &&
        test_bit(PGDAT_WRITEBACK, &pgdat->flags)) {
        stat->nr_immediate += nr_pages;
        goto activate_locked;
    } else if (folio_test_writeback(folio)) {
        /*
         * 如果 folio 在 LRU 中的循环速度之快，
         * 以至于标记为立即回收的 folio 第二次到达
         * LRU 末尾，则将此 folio 视为拥塞。
         */
        if (writeback && folio_test_reclaim(folio))
            stat->nr_congested += nr_pages;
    }
}
```

等待，让我们重新检查代码块的文本，因为它有些碎片化。我将根据标准的内核模式进行重构。
