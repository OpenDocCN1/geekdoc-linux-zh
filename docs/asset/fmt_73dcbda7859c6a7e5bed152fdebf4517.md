
最后，`__mlunlock_page()` 执行与 `__mlock_page()` 逆的操作。这些函数都与专门用于 `mlock()` 操作的 `mlock_pvec` folio 批量交互。核心清空函数在 `mlock_pagevec()` 中调用特定的 drain 函数：

```
/* mlock_pagevec() 派自 pagevec_lru_move_fn()：
 * 也许未来可以使用其中的某些页面指针标志，
 * 但现在仅将其保留用于 mlock。我们可以使用三个独立的
 * pagevec 代替，但感觉用一个会更好（解锁一个整个 pagevec
 * 不需要先清空锁定 pagevec）。
 */
```

```c
static void mlock_pagevec(struct pagevec *pvec)
{
    struct lruvec *lruvec = NULL;
    unsigned long mlock;
    struct page *page;
    int i;

    for (i = 0; i < pagevec_count(pvec); i++) {
        page = pvec->pages[i];
        mlock = (unsigned long)page & (LRU_PAGE | NEW_PAGE);
        page = (struct page *)(unsigned long)page - mlock);
        pvec->pages[i] = page;
    }

    if (mlock & LRU_PAGE)
        lruvec = __mlock_page(page, lruvec);
    else if (mlock & NEW_PAGE)
        lruvec = __mlock_new_page(page, lruvec);
    else
        lruvec = __munlock_page(page, lruvec);

    if (lruvec)
        unlock_page_lruvec_irq(lruvec);
        release_pages(pvec->pages, pvec->nr);
        pagevec_reinit(pvec);
}
```

Listing 11-103: mlock/c.mlock_pagevec()

folio 批量中每个 folio 的低位用于识别该 folio 是旨在调用 `__mlock_page()`（设置了 `LRU_PAGE`）、`__mlock_new_page()`（设置了 `NEW_PAGE`）还是 `__munlock_page()`（未设置低位标志）。该函数根据需要调用相应的 drain 函数，通过 `unlock_page_lruvec_irq(lruvec)` 释放持有的 lru，通过 `release_pages()` 减少 folio 引用，并通过 `pagevec_reinit()` 清空 folio 批量供使用。当 folio 批量满时最终调用 `mlock_pagevec()` 的函数如下：

```c
/**
 * mlock_folio - mlock 一个已在 LRU 上（或临时离开 LRU）的 folio
 * @folio: 要 mlock 的 folio。
 */
void mlock_folio(struct folio *folio)
{
    struct pagevec *pvec;

    local_lock(&mlock_pvec.lock);
    pvec = this_cpu_ptr(&mlock_pvec.vec);

    if (!folio_test_set_mlocked(folio)) {
        int nr_pages = folio_nr_pages(folio);
        zone_mod_folio(folio, NR_MLOCK);
        count_vm_events(INVECTABLE_PGMLOCKED, nr_pages);
    }
    folio_get(folio);
    if (!pagevec_add(pvec, mlock_lru(folio->page)) ||
        folio_test_large(folio) || lru_cache_disabled())
        mlock_pagevec(pvec);
    local_unlock(&mlock_vec.lock);
}
```

Listing 11-104: mm/mlock.c: mlock_folio()

```c
/**
 * mlock_new_page - mlock 一个不在 LRU 上的新分配页面
 * @page: 要锁定的页面，普通页面或 THP 头。
 */
void mlock_new_page(struct page *page)
{
    struct pagevec *pvec;
    int nr_pages = thp_nr_pages(page);

    local_lock(&mlock_vec.lock);
    pvec = this_cpu_ptr(&mlock_vec.vec);
    SetPageLocked(page);
    zone_mod_state(page, NR_MLOCK);
    count_vm_events(INVECTABLE_PGMLOCKED, nr_pages);

    get_page(page);
    if (!pagevec_add(pvec, mlock_new(page)) ||
        PageHead(page) || lru_cache_disabled())
        mlock_pagevec(pvec);
    local_unlock(&mlock_vec.lock);
}
```

Listing 11-105: mm/mlock.c: mlock_new_page()

```c
/**
 * munlock_page - unlock 一个页面
 * @page: 要解锁的页面，普通页面或 THP 头。
 */
void munlock_page(struct page *page)
{
    struct page *pvec;

    local_lock(&mlock_vec.lock);
    pvec = this_cpu_ptr(&mlock_vec.vec);
    /*
     * TestClearPagelocked(page) 必须留给 __munlock_page()，
     * 它将检查页面是否 mlocked。
     */
    if (page_add(pvec, page) ||
        PageHead(page) || lru_cache_disabled())
        mlock_pagevec(pvec);
    local_unlock(&mlock_vec.lock);
}
```

Listing 11-106: mm/munlock.c: munlock_page()

这些函数都执行相似的操作——它们获取 folio 批量锁以禁用抢占，或清除 `PG_mlocked` 标志，更新统计信息，通过 `folio_get()` 或旧式的 `get_page()` 增加 folio 引用，然后尝试将 folio 添加到每个 CPU LRU 列表（通过 `page_add()`），如果是复合页面（通过 `folio_test_large()` 测试）或 LRU 缓存禁用则跳。最后释放本地锁。

不同之处之一是设置一个标志，指示批量中的每个 folio 应该将其应用于 `__mlock_lru()` 以分配 `LRU_PAGE` 以及 `mlock_new()` 以分配 `LRU_NEW`。

## 11.7.12 Folio Batch Drain

当批量被“清空”时，会调用它们的 drain 回调并为了性能进行批量处理。批量满时通过 `folio_batch_add_and_move()` 逐个发生 drain，以及在某些情况下执行每个 CPU 全局 drain。每个 CPU 全局 drain 的关键函数是 `lru_add_drain_cpu()`（它假设已禁用持有，通常通过获取锁来实现）：

```c
/* 清空 cpu 的 folio_batch 中的页面。
 * "cpu" 是当前 CPU 且抢占已被禁用；
 * 或 "cpu" 正在被热插拔且已经失效。
 */
void lru_add_drain_cpu(int cpu)
{
    struct cpu_fbatches *fbatches = &per_cpu(cpu_fbatches, cpu);
    struct folio_batch *fbatch = &fbatches->lru_add;

    if (folio_batch_count(fbatch))
        folio_move_lru(fbatch, lru_add_fn);

    fbatch = &per_cpu(lru_rotate, cpu);
    /* 下面的禁用中断充当屏障。 */
    if (data_race(folio_batch_count(fbatch))) {
        unsigned long flags;
        /* 中断在此死亡没有损害 */
        local_irqsave(lru_rotate.lock, flags);
        folio_move_lru(fbatch, lru_move_tail_fn);
        local_irqrestore(lru_rotate.lock, flags);
    }
    fbatch = &fbatches->lru_deactivate_file;
    if (folio_batch_count(fbatch))
        folio_move_lru(fbatch, lru_deactivate_file_fn);

    fbatch = &fbatches->lru_deactivate;
    if (folio_batch_count(fbatch))
        folio_move_lru(fbatch, lru_deactivate_fn);

    fbatch = &fbatches->lru_lazyfree;
    if (folio_batch_count(fbatch))
        folio_move_lru(fbatch, lru_lazyfree_fn);

    folio_activate_drain(cpu);
}
```

Listing 11-107: mm/swap:c: lru_add_drain_cpu()

注意 `data_race()` 用于表示预期存在数据竞争并且是可以接受的，显式禁用针对此处的 KCSAN 检查（这是一个超出本文范围的话题）。它按顺序调用 `folio_batch_move_lru()`：

- 通过 `lru_add_fn` 添加 folio。
- 通过 `lru_move_tail_fn` 执行可回收旋转。
- 通过 `lru_deactivate_file_fn` 执行文件去激活。
- 通过 `lru_deactivate_fn` 执行去激活。
- 通过 `lru_lazyfree_fn` 执行延迟释放。

Linux 内存管理器（早期访问）© 2025 Lorenzo Stokes

## 通过 lru_lazy_drain() 进行 Folio 懒惰释放

## 通过 folio_activate_drain() 和 folio_activate_fn() 进行 folio 激活

```
mlock() folios 分别在 mlock_page_drain_local() 和
mlock_page_drain_remote() 中被释放，它们执行了类似的作用，仅在本地情况下显式地获取
page 本地锁，并显式检查 CPU 是否处于离线状态，因此在远程情况下不需要锁：
```

```c
213 void mlock_page_drain_local(void)
214 {
215 struct pagevec *pvec;
216
217 local_lock(&mlock_pvec.lock);
218 pvec = this_cpu_ptr(&mlock_pvec.vec);
219 if (pagevec_count(pvec))
220 mlock_pagevec(pvec);
221 local_unlock(&mlock_pvec.lock);
222 }
```

Listing 11-108: mlock/mmock.c: mlock_page_drain_local()

```c
224 void mlock_page_drain_remote(int cpu)
225 {
226 struct pagevec *pvec;
227
228 WARN_ON_ONCE(cpu_online(cpu));
229 pvec = &per_cpu(mlock_pvec.vec, cpu);
230 if (pagevec_count(pvec))
231 mlock_pagevec(pvec);
32 }
```

Listing 11-109: mlock/mmock.c: mlock_page_drain_remote()

这两者都调用了第 11.7.11 节描述的 `mlock_pagevec()`。

核心 folio 和 mlock 批量释放函数都从多个调用点被调用：

```c
727 void lru_add_drain(void)
728 {
729 local_lock(&cpu_fbatches.lock);
730 lru_add_drain_cpu(smp_processor_id());
731 local_unlock(&cpu_fbatches.lock);
732 mlock_page_drain_local();
733 }
```

Listing 11-110: mm/swap.c: lru_add_drain()

这是关键函数。它在调用 `lru_add_drain_cpu(cpu)` 之前应用一个本地锁，然后调用 `mlock_page_drain_local()` 来处理 mlock folios。

1108 第 11 章

# Linux 内存管理器（早期访问）© 2025 Lorenzo Stokes

函数 `lru_add_and_bh_lrus_drain()` 执行了相同的操作，它还通过 `invalidate_bh_lrus_cpu()` 调用了缓冲区头 LRU 列表的失效。这出了本节的讨论范围：

```c
/*
 * 它在 SMP 情况下从每个 CPU 的工作队列上下文中被调用，因此
 * lru_add_cpu 和 invalidate_bh_lrus_cpu 应该在同一个 cpu 上运行。
 * 在 SMP 中这不应该是问题，因为核心只有一个，且锁会禁用抢占。
 */
static void lru_add_and_bh_lrus_drain(void)
{
    local_lock(&cpu_fbatches.lock);
    lru_add_cpu(smp_processor_id());
    local_unlock(&cpu_fbatches.lock);
    invalidate_bh_lrus_cpu();
    mlock_page_drain_local();
}
```

Listing 11-111: mm/swap.c: lru_add_and_bh_lrus_drain()

此函数由 `lru_add_per_cpu()` 调用，而后者又被 `lru_add_drain_all()` 轮流调用（更多细节请见下文）。

最后，是 `lru_add_drain_zone()`，它由压缩任务调用：在 `compact_zone()` 中（更多细节请参阅压缩章节）：

```c
void lru_add_cpu_zone(struct zone *zone)
{
    local_lock(&cpu_fbatches.lock);
    lru_add_cpu(smp_processor_id());
    drain_local(pages);
    local_unlock(&cpu_fbatches.lock);
    mlock_page_drain_local();
}
```

Listing 11-112: mm/swap.c: lru_add_drain_cpu_zone()

这里的关键区别在于调用了 `drain_local_pages()`，它将所有 Per CPU Pages (PCP) 释放到空闲列表。

到为止，我们创建的是在特定 CPU 上释放 folios 的，而不是释放所有 CPU。这由 `lru_add_drain_all()` 处理，它调用了 `_lru_add_drain_all()`。

检查此函数，为了清晰起见，去掉了仔细的同步处理：

```c
/*
 * 不需要任何 CPU 热插锁，因为我们依赖于每个 CPU 的 kworkers
 * 在 page_alloc_cpu_drain 回调在离线 cpu 上执行之前已经关闭了。
 * 在持有 CPU 热插锁的情况下调用此函数实际上会导致
 * 通过工作队列观察间接依赖。
 */
```

内存回收与内存压力 1109

# Linux 内存管理器（早期访问）© 2025 Lorenzo Stokes
