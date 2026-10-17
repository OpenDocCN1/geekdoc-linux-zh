
该函数汇总了页面最近接收到的引用次数。如果设置了 `PG_referenced`，这显然是一个引用并会相应计数。根据之前的讨论，如果该位被设置，则会被移除。

如果页面映射到某些地址空间，则对该页面的引用必须通过页表中的硬件特定位来确定。回第 4.8 节，`page_referenced_anon` 计算匿名映射中页面的访问次数，而 `page_referenced_file` 对基于文件的映射执行相同的操作。例如，在 IA-32 和 AMD64 上，通过累加指向目标页且设置了 `PG_BIT_ACCESSED` 位（该位由硬件自动更新）的页表项数量来计算。

`page_referenced_file` 要求页面必须锁定（例如，为了防止内核在操作页面时因截断操作而删除了映射）。如果将一个未解锁的锁传递给 `page_referenced`，则页面会被锁定。对于初始已锁定的页面，将执行最后一个 `else` 分支，因为 `TestSetPageLocked` 在将 `PG_locked` 位置 1 之前会返回其当前值。如果在此期间页面被内核的其他部分锁定了，那么等待锁释放是没有意义的。相反，引用计数器加 1，因为至少发起锁定的页面对该页面有访问权限。

注意，`page_referenced`（通过 `page_referenced_file` 和 `page_referenced_anon` 用的 `page_referenced_one`）如果页面正在换出且属于持有交换令牌（swap token）的进程，也会将其标记为已引用——即使它没有从某处被访问。这防止了该页面被回收，并在频繁交换的情况下提高性能。详见第 18.7 节中关于该机制的细节。

最后，还有 `mark_page_accessed` 需要考虑。其实现非常直接：

```c
swap.c

void fastcall_mark_page_accessed(struct page *page)
{
    if (!PageActive(page) && PageReferenced(page) && PageLRU(page)) {
        activatePage(page);
        ClearPageReferenced(page);
    } else if (!PageReferenced(page)) {
        SetPageReferenced(page);
    }
}
```

该实现描述了图 18-13 所示的转换。它们在表 18-1 中也进行了总结。

| 表 18-1：交换页面状态 |
| 初始状态 | 目标状态 |
| 非活跃，未引用 | 非活跃，已引用 |
| 非活跃，已引用 | 活跃，未引用 |
| 活跃，未引用 | 活跃，已引用 |

## 18.6.4 区域收缩（Shrinking Zones）

收缩区域的例程由内核的其他部分提供以下信息（等）：

- 需要处理的 NUMA 区域及其包含的内存区域。
- 需要换出的页面数量。
- 在操作中止之前，可能检查以确定它们是否适合交换的最大页面数。
- 分配给释放页面尝试的优先级。这不是经典 Unix 意义上的优先级（因为这在内核中意义不大），而是一个指定内核需要新内存紧急程度的整数。当作为预防措施在后台换出页面时，这不像内核检测到内存短缺并迫切需要内存完成操作时那样直接。

页面选择从 `shrink_zone` 开始。但在讨论代码之前，必须引入一些基础设施。

### 控制扫描

使用一个持有参数的特殊数据结构来控制扫描操作。注意，这不仅用于从高层函数向低层函数传递如何继续的指令，还用于向反向传播结果。它通知调用者操作是否成功：

```c
mm/vmscan.c

struct scan_control {
    /* 由扫描的非活跃页面数量递增 */
    unsigned long nr_scanned;
    /* 此上下文的 GFP 掩码 */
    gfp_t gfp_mask;
    int my_writepage;
    /* 页面可以作为回收的一部分进行交换吗？ */
    int my_swap;
    ...
    int swappiness;
    int all_unreclaimable;
    int order;
}
```

元素的含义在变量名中得到了很好的反映：

- `nr_scanned` 向调用者报告扫描了多少非活跃页面，并用于参与页面回收的内核函数之间的通信。
- `gfp_mask` 指定在调用回收函数时上下文中有效的分配标志。它之所以重要，是因为在页面回收期间需要分配空内存。如果启动回收的上下文不允许睡眠，则此约束必须向下传递给所有函数；这正是 `gfp_mask` 的设计目的。
- `may_page` 选择内核是否允许将页面写入后备存储。当内核以第 17.13 节描述的循环模式运行时，需要禁用此属性。
- `may_swap` 决定是否允许交换作为页面回收尝试的一部分。交换仅在两种情况下被禁止：如果页面回收代表软件挂起机制运行，如果 NUMA 节点显式禁用了交换。这些可能性在书中未考虑。
- `swap_cluster_max` 实际上与交换无关，但它为每个 LRU 列表中至少处于一个回收步骤的页面数量提供了一个阈值。通常，它被设置为 `SWAP_CLUSTER_MAX`，默认为 32。
- `swapiness` 控制内核尝试换出页面的积极程度，值范围在 0 到 100 之间。默认情况下，使用 `vm_swapiness`。标准设置为 60，但可以通过 `/proc/sys/swapiness` 进行调整。
- `all_unreachable` 用于报告所有区域中的内存完全可能不可达的糟糕状况（注：OCR 文本为 "all_unreachable"，根据上下文可能可能是 "all_unreclaimable"）。

## 第 18 章：页面回收与交换

如果其中一个值大于或等于当前交换簇（swap cluster）中的最大页号，则该区域元素的值被重置为 0，并保留局部变量 `nr_active` 或 `nr_inactive` 的值；否则，区域值保持不变，局部变量被设置为 0。

这种行为确保了除非活动页和非活动页的数量超过了 `sc->swap_cluster_max` 指定的阈值，否则内核不会启动后续操作，正如函数的后续部分所示：

```c
mm/vmscan.c

while (nr_active || nr_inactive) {
    if (nr_active) {
        sc->nr_to_scan = min(nr_active,
        (unsigned long)sc->swap_cluster_max);
        nr_active -= sc->nr_to_scan;
        shrink_active_list(nr_to_scan, zone, sc, priority);
    }
    if (nr_inactive) {
        sc->nr_to_scan = min(nr_inactive,
        (unsigned long)sc->swap_cluster_max);
        nr_inactive -= sc->nr_to_scan;
        nr_reclaimed += shrink_inactive_list(nr_to_scan, zone, sc);
    }
    ...
}
    return nr_reclaimed;
}
```
