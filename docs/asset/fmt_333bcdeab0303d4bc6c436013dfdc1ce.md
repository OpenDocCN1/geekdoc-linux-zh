
## `rmqueue_bulk()`

```c
static int rmqueue_bulk(struct zone *zone, unsigned int order,
    unsigned long count, struct list_head *list,
    int migrateype, unsigned int alloc_flags)
{
    int i, allocated = 0;

    /* 调用者必须持有 IRQ-安全的 pcp->lock 以禁用 IRQ。 */
    spin_lock(&zone->lock);

    for (i = 0; i < count; ++i) {
        struct page *page = __rmqueue(zone, order, migrateype,
            alloc_flags);
        if (unlikely(page == NULL))
            break;
        if (unlikely(check_pcp_refill(page, order)))
            continue;

        /*
         * 由 expand() 返回的拆分伙伴页以物理页顺序
         * 在此接收。页面被添加到调用者列表的尾部。
         * 从调用者的角度来看，在某些条件下，链表按页码
         * 排序。这对于可以从头部转发方向的 IO
         * 设备是有用的，且也是按物理页顺序。这对于物理页
         * 排序正确时可以合并 IO 请求的 IO 设备是有用的。
         */
        list_add_tail(&page->pcp_list, list);
        allocated++;
    }

    /*
     * i 个页面已从伙伴列表中移除，即使某些泄漏
     * 到 check_pcp_refill 失败未根据 i 调整 NR_FREE_PAGES。
     * 不要与 'allocated' 混淆，它是添加到 pcp 列表的
     * 数量。
     */
    mod_page_state(zone, NR_FREE_PAGES, -(i << order));
    spin_unlock(&zone->lock);
    return allocated;
}
```

`rmqueue_bulk()` 尝试带有 `__alloc__` 标志从区域的 `migrate_type` 空闲列表中移除指定阶数的页面并将其添加到列表，返回实际分配的页面数量。重头工作由之前的示例 `__rmqueue()` 完成，并通过 `check_pcp_refill()` 检查页面状态，该函数确保返回的页面是有效的，通常以避免释放后使用的错误（bug）。

## 2.8.7 新页面的准备

当页面准备好从伙伴分配器返回时，它需要一些最后的准备。这是通过列表 2-73 所示的 `prep_page()` 完成的，它由 `get_page_from_freelist` 和 `__alloc_bulk()` 调用。

```c
static void prep_page(struct page *page, unsigned int order,
    gfp_t gfp_flags)
{
    /*
     * 释放页面的逻辑比分配简单——
     * 分配需要特殊处理（在原子上下文中或递归
     * 文件锁中），而释放页面仅仅是将其放在哪里
     * 以及在可能的情况下进行合并。
     */
    if (gfp_flags & ALLOC_COMPUND))
        set_pagecompound(page);
    post_page(page);
}
```

所有页面都调用 `post_page()` 以执行初始化：
- 通过 `set_page_counted()` 清空 `page->private`。
- 通过 `set_page_counted()` 将计数设为 1。
- 对于 `GFP_ZERO`，所有页面调用 `if_set_zero()`。

## 2.9 释放页面

内核分配的页面具有引用计数，因为它们可能被不同的进程使用（例如共享映射）。计数存储在 `page->refcount` 中（等效于 `folio->refcount`）。该字段跟踪页面的“用户”数量，当计数为零时最终释放页面。`get_page()` 或 `folio_get()` 增加引用计数，而 `put_page()` 或 `folio_put()` 减少它。`put_testzero()` 原子地减少引用计数并检查它是否为零。这被所有释放函数使用。

内核页的释放通常由 `free_pages()` 执行，或者通过内存分配器直接执行。用户页使用 `release_pages()`（见第 7.1 节）。

最终所有进入两个地方：`free_unref_commit()` 或 `_free_one_page()`，前者将页面添加到 PCP 列表，后者将其添加到底层空闲列表。这些构成了分配器释放机制的核心。

释放页面的逻辑比分配它们简单——分配需要特殊处理（在原子上下文中或递归文件系统锁中），而释放页面仅仅是将其放在哪里以及在可能的情况下进行合并。

底层机制并不复杂，不需要以图表形式可视化，相反我们直接检查相关函数。

然而，复杂性在于释放机制有许多入口点，这考虑了释放的页面可能是 0 阶或复合的，可能是批量释放的，以及上述引用计数机制。我们在图 2-22 中可视化了这一点。

注意：
- 表示导出的函数。
- 表示最终到达的关键函数。

释放页面的两个关键函数是 `free_unref_page_commit()` 和 `_free_one_page()`，前者将页面添加到 PCP 列表，后者将其添加到底层空闲列表。让我们先查看 `free_unref_page_commit()`，如列表 2-74 所示。

```c
static void free_unref_page_commit(struct zone *zone, struct per_cpu_pages *pcp,
    bool free_high)
{
    __count_vm_event(PGFREE);
    pindex = order_to_pindex(migratype, order);
    list_add(&page->pcp_list, &pcp->lists[pindex]);
    pcp->count += 1 << order;

    /*
     * 由于存储在 PCP 上的 THP 高阶阶页可能导致
     * 碎片化，当 PCP 在大量进行释放而没有分配时，
     * 限制其存储的页面数量。批量释放停止后剩余的部分
     * 将从 vmstat 刷新上下文中驱空。
     */
    free_high = (pcp)->free_factor && order && order <= PAGE_ALLOC_COSTLY_ORDER);

    high = nr_pcp_high(pcp, zone, free_high);
    if (pcp)->count >= high) {
        int batch = READ_ONCE(pcp->batch);
        free_pppages_bulk(zone, nr_pcp_free(pcp, high, batch,
        free_high, pcp, pindex);
    }
}
```

代码初始部分非常直接——我们确定要将页面放入哪个 PCP 列表，将其放置在那里并更新统计数据。这里唯一的复杂性在于决定何时将 PCP 列表中的页面释放回底层的空列表。
我们通过 `nr_pcp_high()` 确定何时将 PCP 页面刷入空列表。
该函数计算当前 CPU 的 PCP 空闲页的有效高水位（high watermark）。
当我们确定 PCP 页面需要刷回空列表时，我们通过 `free_pppages_bulk()` 执行操作，该函数通过 `nr_pcp_free()` 确定我们要释放多少页面。
如果设置了 PCP `free_factor`，且该页面是高阶的且阶数符合出现在 PCP 列表的条件，我们会设置 `free_high` 变量。虽然你可能认为在一个专门为释放 PCP 页面设计的函数中这是没有必要的，但如果启用了透明巨页（THP），PCP 列表中也可能存在巨大页。
我们在列表 2-75 中检查了 `nr_pcp_high(struct ... )`。

```c
static int nr_pcp_high(struct per_cpu_pages *pcp, struct zone *zone,
    bool free_high)
{
    int high = READ_ONCE(pcp->high);
    if (unlikely(high || free_high))
        return 0;
    if (!test_bit(ZONE_RECLAIM_ACTIVE, &zone->flags))
        return high;
    /* 如果回收（reclaim）处于激活状态，限制 pcp
     * 列表中的页面数量 */
    return min(READ_ONCE(pcp->batch) << 2, high);
}
```

我们可以看到，如果没有设置 PCP 高水位（这应该只发生在内核早期阶段）或者设置了 `free_high`，我们指示无论如何都应该刷新 PCP 列表。

正如列表 2-74 中的注释所示，当从 PCP 列表中执行了分配但没有随后的释放且该页面是高阶的时，会设置 `free_high`。这是因为 PCP 列表上的高阶页总是可以被拆分为低阶页（而反之则不然）。你会注意到内存管理子系统包含了大量的启发式算法（heuristics）。这些是基于真实经验优化的结果。

接下来，如果区域（zone）内没有指示进行回收（reclaim），我们使用 PCP 列表指定的高水位水平。如果是，则选择批次大小（batch size）乘以 4 与高水位之间较小的一个（通常前者要小得多）。这同样是一个调优的启发式算法。

我们可以看到，PCP 页面优先从空闲列表分配到每个核心的缓存页面中，通过这样做，我们避免了昂贵的区域锁，从而提高了内存分配和释放的性能。查看列表 2-76 所示的 `nr_pcp_free()`。

```c
static int nr_pcp_free(struct cpu_pages *pcp, int high, int batch,
    bool free_high)
{
    int min_nr_free, max_nr_free;
    /* 如果批量释放高阶页，则释放所有。 */
    if (unlikely(free_high))
        return pcp->count;
    /* 检查 PCP 禁用或启动页集禁用 */
    if (unlikely(high < batch))
        return 1;
    /* 在列表中至少保留 pcp->batch 个页面 */
    min_nr_free = batch;
    max_nr_free = high - batch;
    /*
     * 每当在没有任何分配的情况下连续释放页面时，
     * 都将页面数量翻倍。
     */
    batch <<= pcp->free_factor;
    if (batch < max_nr_free)
        pcp->free_factor++;
    batch = clamp(batch, min_nr_free, max_nr_free);
    return batch;
}
```

与其 `nr_pcp_high()` 一致，如果设置了 `free_high`，我们在一个批次后清理 PCP 页面。此外，如果 PCP 被禁用或我们处于启动阶段，我们一次释放一个页面。然而在某些情况下，我们观察到以下过程：
- 设置边界：`min_nr_free` 设置为批次大小，`max_nr_free` 设置为批次的 PCP 高水位。我们总是至少释放一个批次，但在 PCP 上至少保留一个批次的页面。
- 将批次大小乘以 `free_factor`，如果这种增加没有超过要驱空的最大页面数，则增加 `free_factor`。正如第 2.7 节所述，这是一个启发式算法，确保存储在 PCP 列表上的页面与从它们分配的页面成比例，如果没有发生分配，则返回回空列表的页面数量将呈指数级增加。
- 最后，我们将要驱空的页面数量限制在 `min_nr_free` 到 `max_nr_free` 范围内。

`free_pppages_bulk()` 正如其名，它如列表 2-77 所示批量释放数量 PCP 页面。

```c
static void free_pppages_bulk(struct *zone, int count, ...)
{
    int min_pindex = 0;
    int max_pindex = NR_PCP_LISTS - 1;
    unsigned int order;
    bool isolated_pageblocks;
    /* 确保 count 正确，否则会卡在 while (list_empty(list)) 循环中。 */
    count = min(pcp->count, count);
    /* 确保请求的索引首先被驱空。 */
    pindex = pindex - 1;
    /* 调用者持有 pcp->lock 这样中断被禁用。 */
    spin_lock(&zone->lock);
    isolated_pageblocks = has_isolate_pageblock(zone);
    while (count > 0) {
        spin_unlock(&zone->lock);
        /* 以轮询方式从列表中移除。 */
        do {
            if (++pindex > max_pindex)
                pindex = min_pindex;
            list = &pcp->lists[pindex];
            if (!list_empty(list))
                break;
            if (pindex == max_pindex)
                max_pindex--;
        } while (pindex == min_pindex)
        min_pindex++;
        order = pindex_to_order(pindex);
        nr_pages = 1 << order;
        BUILD_BUG_ON(MAX_ORDER) >= (1<<NR_PCP_ORDER_WIDTH);
        do {
            int mt;
            page = list_last_entry(list, struct page, pcp_list);
            mt = get_pcpage_mtype(page);
            /* 必须删除以防损坏 pcp 列表 */
            list_del(&page->pcp_list);
            count = --nr_pages;
            pcp->count < count;
            if (freeblock_pcp_prepare(page))
                continue;
            /* MIGRATE_ISOLATE 页面不应进入 pcplists */
            VM_BUG_ON(PAGE(is_isolate(mt), page);
            /* 页块可能已被隔离时 */
            if (unlikely(isolated_pageblocks))
                mt = get_pageblock_mtype(page);
            _free_one_page(page, page_to_pfn(page), zone, order,
            mt, FPI_NONE);
            trace_mm_page_pcpu_drain(page, order, mt);
        } while (count > 0 && !is_empty(list));
    }
}
```

- 如果区域（zone）内存在隔离的页块（pageblocks），则 PCP 页面可能在释放后就已经被隔离；为了安全起见，在此情况下我们获取了的迁移类型（migrate type）的页块。
- 最后，调用 `__free_one_page()` 执行释放页面的重型工作。该函数假设持有区域锁（zone lock）。

## 2.9.0.1 FPI 标志

空闲内部（FPI）标志会调整页面释放行为。
查看列表 2-79 所示的 `__free_one_page()` 签名。
