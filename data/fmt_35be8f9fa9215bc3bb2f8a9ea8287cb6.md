
## 11.5.1 回收映射移除

当我们需要将脏 folio 写回磁盘时，无论是将 swap 缓存中由 swap 支持的 folio 写入磁盘上的 swap，还是写入脏文件支持的 folio，我们都通过 `pageout()` 执行此操作，我们在列表 11-71 中检查该函数（省略了作用外缓冲区处理、跟踪钩子和统计数据更新）。

```c
/*
 * pageout 由 shrink_page_list() 为每个脏页调用。
 * 调用 -> .writepage().
 */
static page_t pageout(struct folio *folio, struct address_space *mapping,
                      struct swap_ioc **plug)
{
    /*
     * 如果 folio 是脏的，只有当该写入
     * 是非阻塞的时才执行回写。为了防止此分配
     * 被 pagecache 活动
     * 阻塞。
     * 如果我们需要运行 get_block()，则会阻塞。我们可以对
     * PagePrivate 进行测试。
     */
    /* 如果此进程当前正针对此 folio 队列在
     * 执行 __generic_file_write_iter()，如果该操作
     * 会产生阻塞，我们就可以执行回写。
     */
    /* 如果 folio 是 swapcache，即使这会阻塞也将其写回，以进行
     * 某些节流。这发生是由于某种意外的，因为
     * swapping_dev_info 是失效的：它没有反映
     * swapdev 的拥塞状态。容易修复，有必要。
     */
    if (!is_page_cache_freeable(folio))
        return PAGE_KEEP;

    if (mapping) {
        return PAGE_KEEP;
    }
    if (mapping->a_ops->writepage == NULL)
        return PAGE_ACTIVATE;

    if (folio_clear_dirty_for_io(folio)) {
        int res;
        struct writeback_control wbc = {
            .sync_mode = WB_SYNC_NONE,
            .nr_to_write = SWAP_CLUSTER_MAX,
            .range_start = 0,
            .range_end = LLONG_MAX,
            .for_reclaim = 1,
            .plug = plug,
        };
        folio_set_reclaim(folio);
        res = mapping->a_ops->writepage(&folio->page, &wbc);

        if (res < 0)
            handle_write_error(mapping, folio, res);

        if (res == AOP_WRITEPAGE_ACTIVATE) {
            folio_clear_dirty(folio);
            return PAGE_ACTIVATE;
        }

        if (!folio_test_writeback(folio)) {
            /* 成功 */
            folio_clear_reclaim(folio);
        }

        return PAGE_CLEAN;
    }
}
```

列表 11-71: vmscan.c: `pageout()`

我们通过启动 `pageout()` 检查自上次检查以来是否有任何映射引用了此 folio，如果是，我们设置 `PG_referenced` 标志。

```c
static int is_cache_freeable(struct folio *folio)
/*
 * 即使这会阻塞也将其写回，以进行
 * 某些节流。
 */
{
    return folio_refcount(folio) == 1;
}
```

列表 11-72: vmscan.c: `pageout()`

`is_cache_freeable()` 确保我们不会尝试回收一个引用它的页缓存。

> 内核会特意努力快速激活可执行代码映射，因为回收它们在代码执行延迟方面的成本是高昂的。

如果 folio 被引用了但之前没有设置 `PG_referenced` 标志，且它是文件支持的并且可执行代码（如 `VM_EXEC` VMA 标志所示），我们将跳过双重引用检查，并简单通过 `PAGREF_ACTIVATE` 指示我们应该立即激活它。

如果 folio 被引用了但之前未被引用，我们将其旋转到 `PAGREF_KEEP` 索引的当前列表末尾。

如果自我们上次检查以来 folio 未被引用过，这表明它符合回收条件。如果 folio 是文件支持的，我们返回 `PAGREF_RECLAIM_CLEAN`，表示只有在干净时才回收，将脏数据留给回写处理。

否则，我们返回 `PAGREF_RECLAIM`，表示该 folio 可以直接进行回收。

## 11.5.2 回收映射移除

回收机制通过 `__filemap_remove_folio()` 从其包含的 `struct address_space` 对象的 xarray 中移除 folio，我们将在列表 9-89 和第 9 章第 9.9.1 节中检查该函数。

如果文件系统在其 `struct address_space_operations` 钩子的 `struct address_ops->free_folio` 中提供了一个 `free_folio()` 钩子，我们就调用它。

然后我们返回表示操作成功。

```c
if (!folio_test_swapcache(folio))
    spin_lock(&mapping->host->i_lock);
xa_lock_irq(&mapping->i_pages);
```

```c
refcount = 1 + folio_n_pages(folio);
if (!folio_test_ref(folio, refcount))
    goto cannot_free;
/* note: atomic cmpxchg in page_ref_free provides the smp_rmb */
if (unlikely(folio_test_dirty(folio))) {
    folio_ref_unfreeze(folio, refcount);
    goto cannot_free;
}
```

```c
if (folio_test_swapcache(folio)) {
    swp_entry_t swap = folio_swap_entry(folio);
    _delete_from_swap_cache(folio, swap, shadow);
    xa_lock_irq(&mapping->i_pages);
    put_swap_page(&folio->page, swap);
} else {
```

```c
void (*free_folio)(struct folio *);
free_folio = mapping->ops->free_folio;
_filemap_remove_folio(folio, shadow);
xa_lock_irq(&mapping->i_pages);
spin_unlock(&mapping->host->i_lock);
if (free_folio) {
    free_folio(folio);
}
return 1;
}
```

```c
cannot_free:
xa_unlock_irq(&mapping->i_pages);
if (!folio_test_swapcache(folio))
    spin_unlock(&mapping->host->i_lock);
return 0;
```

列表 11-73: mm/vmscan.c: `__remove_mapping()`

`remove_mapping()` 函数首先获取适当的锁，以便将 folio 从其映射中移除。

在我们执行虚拟引用计数检查后——我们必须避免重新回收那些被内核任务锁定的 folio，在此阶段，除了我们对 folio 页所采取的隔离处理外，我们预计页缓存或交换缓存还持有一个引用。

我们调用 `folio_ref_()`，它尝试将暴露的引用计数原子地交换为零。如果失败，则直接退出，因为我们无法将 folio 从映射中移除，因此无法继续释放它，从而终止。

我们双重检查 folio 是否为脏，取消冻结 folio，并考虑交换情况——即我们从交换缓存中删除该 folio。详细分析请参见第 12 章第 12.2.4 节。

否则，我们通过 `__filemap_remove_folio()` 从其包含的 `struct address_space` 对象的 xarray 中移除 folio，我们将在列表 9-89 和第 9 章第 9.9.1 节中检查该函数。

如果文件系统在其 `struct address_space_operations` 钩子的 `struct address_ops->free_folio` 中提供了一个 `free_folio()` 钩子，我们就调用它。

然后我们返回表示操作成功。

## 11.6 回收节流

## 11.6.1 通用回收节流

在某些情况下，我们必须暂停回收一段时间，因为回收由于某种原因没有取得进展。这在 `reclaim_throttle()` 中执行，我们稍后将在列表 11-75 中检查。

我们在图 11-23 中查看该函数的调用者。

![](img/d466eba53d24b7c77bd1b391fbb9172c_1086_0.png)

图 11-23: `reclaim_throttle()` 的调用者。

在直接回收的情况下，我们有特定的直接回收节流，用于处理由于非常缓慢的后端存储导致回收非常缓慢的情况。这种特定情况在 `throttle_direct_reclaim()` 中处理（参见列表 11-77），正如第 11.6.2 节所述。

此外，我们还考虑直接回收卡住且没有进展的情况，此时适当睡眠一段时间是合适的。这由 `shrink_zones()` 调用（参见列表 11-21 和第 11.3 节），它反过来调用 `consider_reclaim_throttle()`，我们将在列表 11-74 中检查它。

```c
static void consider_reclaim_throttle(struct pg_data_t *pgdat, struct scan_control *sc)
{
    /*
     * 如果回收的效率大于 12%，则
     * 唤醒所有处于 NOPROGRESS 节流状态的任务。
     */
    if ((sc)->nr_reclaimed > (sc)->nr_scanned >> 3) {
        wait_queue_head *wqh;
        wqh = &pgdat->reclaim_wait[VMSCAN_THROTTLE_NOPROGRESS];
        if (wait_active(wqh))
            wake_up(wqh);
    }

    /*
     * 不要在 NOPROGRESS 下节流 swapd 或 cgroup 回收，
     * 因为如果有太多页面正在回写并且在 LRU 尾部标记为立即回收，
     * 它们将在 VMSCAN_THROTTLE_WRITEBACK 处节流。
     */
    if (current_is_kswapd() || cgroup_reclaim(sc))
        return;

    /* 如果在高优先级下取得进展则节流。 */
    if ((sc)->nr_priority == 1 && !sc->nr_reclaimed)
        reclaim_throttle(pgdat, VMSCAN_THROTTLE_WRITEBACK);
}
```

列表 11-74: `consider_reclaim_throttle`

在此函数中，我们关注直接回收是否取得进展，此时睡眠一段时间是合适的。这由 `shrink_zones()` 调用（参见列表 11-21 和第 11.3 节），它反过来调用 `consider_reclaim_throttle()`，我们将在列表 11-74 中检查它。

在回收的效率大于 12% 时，唤醒所有处于 NOPROGRESS 节流状态的任务。
