
# Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

## 回收与内存压力

### `balance_pgdat()` 函数分析

```c
/*
 * 对于 kswapd, balance_pgdat() 将跨越节点从允许调用者
 * 使用的区域回收页面，直到至少有一个区域达到
 * Balanced。
 *
 * 返回 kswapd 回收的阶数。
 * kswapd 按照 highmem-normal->dma 方向扫描区域。它会跳过
 * free_pages > high_wmark_pages(zone) 的区域，但一旦某个区域的
 * free_pages < high_wmark_pages(zone)，该区域中的任何页面
 * 或更低页面都可以被回收，直到至少有一个可用的区域达到
 * Balanced。
 */
```

```c
static int balance_pgdat(pg_data_t *pgdat, int order, int highest_zoneid) {
    int i;
    unsigned long nr_sort_reclaimed;
    unsigned long nr_boost_reclaim;
    unsigned long zone_boosts[MAX_NR_ZONES] = { 0, };
    bool boosted;
    struct zone *zone;
    struct scan_control sc = {
        .gfp_mask = GFP_KERNEL,
        .order = order,
        .may_unmap = 1,
    };
    set_task_reclaim_state(current, &sc.reclaim_state);
    count_vm_event(PAGEOUTRUN);
```

我们通过初始化状态并设置 `struct task_struct->rs` 指向在 `struct scan_control.reclaim_state` 字段中新初始化的 `struct reclaim_state` 对象来开始 `balance_pgdat()`。

`reclaim_state` 字段目前用于跟踪 slab 占用的数量。内核 slab 分配不在本书范围内，但广义来说，它是内核允许高效子页大小分配机制，即内核中的 `malloc()`。

由 slab 分配的对象也可以维护在缓存中以提高效率，这些缓存可以在回收期间被收缩以释放内存，这就是在这里测量的内容。

接下来，我们的间接回收通过 `PAGEOUTRUN` 事件值发生。

### 区域提升（Zone Boost）

```c
/*
 * 考虑回收提速（reclaim boost）。注意区域提升保留在
 * 原处，以便接近水位线的并行分配会
 * 停顿或进行直接回收，直到 kswapd 完成。
 */
```

```c
nr_boost_reclaim = 0;
for (i = 0; i <= highest_zoneid; i++) {
    zone = pgdat->node_zones + i;
    if (!managed_zone(zone)) {
        continue;
    }
    nr_boost_reclaim += zone->watermark_boost;
    zone_boosts[i] = zone->watermark_boost;
}
boosted = nr_boost_reclaim;
```

**列表 11-32: mm/vmscan.c `balance_pgdat()` 函数区域提升（Zone Boost）**

我们跳过任何不通过 `managed_zone()` 测试的、由伙伴页面分配器控制的页面，然后通过 `high_wmark_pages()` 获取该区域的高水位值。

这会针对指定的阶数（order）的区域通过函数 `zone_wmark_ok_safe()` 进行检查，该函数最终会调用 `zone_wmark_ok()`（见第 2.8.2 节和第 2 章中的列表 2-59）。

如果没有区域可以检查，说明我们成功了；否则，如果没有区域足够的空闲页，我们指示失败。

我们测量节点内被提升的区域，将提升的页面总数聚合到 `nr_boost_reclaim` 中，并在本地 `zone_boosts` 数组中记录每个区域的提升情况。

区域提升在发生迁移碎片（migrate fragmentation）时执行，并为每个水位增加一个因子。

我们将在第 2.5 节和第 2 章中讨论迁移类型，但广义来说，这是物理内存页的一个属性，决定了内存是否是可移动的，以便我们将可移动内存与不可移动内存（该内存用于内核分配）分开，这样我们就不会产生碎片，并通过让可移动内存与不可移动内存交织来释放更高阶的页组（folios）。

然而，在找不到所需的迁移类型页块的情况下（再次在第 2 章中涵盖，但广义上页块是物理连续的、阶数为 `order pageblock` 的内存块，在 x86-64 上阶数是 9）。

这在 `steal_suitable_fallback()` 中执行（见列表 2-68 和第 2 章的第 2.8.6 节）。如果发生这种情况，我们希望确保尽快修复碎片，通过在 `boost_watermark()` 中将每个水位增加固定数量的页面来实现，每次最多增加一个页块的大小。

当我们这样做时，会在 `wakeup()` 中在物理页面分配时（针对该节点）主动唤醒该节点的 `kswapd`（见第 2.3 节和第 2 章中的列表 2-60）。我们这样做是为了防止迁移类型块的进一步污染，从而减少碎片。

如果节点是平衡的，否则本将需要回收，我们使用在整个过程中收集的信息来决定是否执行间接回收以释放内存，以避免进一步的迁移窃取。

我们现在已经检查了如何判断一个节点（node）是否平衡，现在可以检查间接回收的下一个阶段（如图 11-10 所示），通过 `balance_pgdat()` 对节点进行平衡，我们从列表 11-32 开始分析（省略了范围之外的 PSI 内存压力钩子、lockdep、cgroup、空闲处理以及 buffer head 越界）。
