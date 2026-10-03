
**Listing 7-51: mmu/mmap.c: unmap_region()** 该函数初始化了一个 `struct mmu_gather` 对象，该对象将在整个操作中使用。执行失效操作的重型工作由 `mmu_vmas()` 处理。页表在执行 TLB 操作（通过 `tlb_finish_mmu()` 使 TLB 失效并释放内存）之前，通过 `free_pgtables()` 释放。

需要注意的是，在进行此调用之前，`vma` 要么没有附加到进程空间中的任何后续 VMA，要么已经从后续的 VMA 中解离。

这一点很重要，因为我们依赖这一事实来遍历受影响的 VMA（在第 7.1.5 节描述）。

## 7.1.2 MMU gather 初始化

`struct mmu_gather` 数据结构在整个 TLB 操作期间维护状态：

```c
/*
 * struct mmu_gather 是一个不透明类型，供 mm 代码用于传递
 * 体系特定代码为 tlb_remove_page 所需的任何数据。
 */
struct mmu_gather {
    struct mm_struct       *mm;
#ifdef CONFIG_MMU_GATHER_TABLE_FREE
    struct mmu_table_batch *batch;
#endif

    unsigned long           start;
    unsigned long           end;
    /*
     * 我们正在清空
     * 完整 mm 的操作中，可以进行一些优化
     */
    unsigned int            fullmm : 1;
    /*
     * 我们已经执行了一个需要
     * 刷新 tlb 的操作
     */
    unsigned int need_flush_all : 1;

    /*
     * 我们已经删除了页目录
     */
    unsigned int freed_tables : 1;

    /*
     * 记录在哪些层级清理了条目；
     */
    unsigned int cleared_ptes : 1;
    unsigned int cleared_pmds : 1;
    unsigned int cleared_puds : 1;
    unsigned int cleared_p4ds : 1;

    /*
     * 在 tlb_start_vma 中跟踪 VM_EXEC | VM_HUGTLB
     */
    unsigned int vma_exec : 1;
    unsigned int vma_huge : 1;
    unsigned int vma_pfn : 1;

    unsigned long batch_count;

#ifndef CONFIG_MMU_GATHER_NO_GATHER
    struct mmu_gather_batch *active;
    struct mmu_gather_batch local;
    struct page *pages[MMU_GATHER_BUNDLE];
#endif

#ifdef CONFIG_MMU_GATHER_PAGE_SIZE
    unsigned int page_size;
#endif
};
```

**Listing 7-52: include/asm-generic/tlb.h: struct mmu_gather**

最后，还有许多文档齐全的标志位和一个在 `batch` 字段中引用的 `struct mmu_table_batch` 对象，用于释放页表。页表大小（以适应巨页）存储在 `page_size` 字段中。

检查操作是否全部由 `CONFIG_MMU_GATHER_NO_GATHER` 决定，变量页大小是否由 `CONFIG_MMU_GATHER_PAGE_SIZE` 决定，以及页表 TLB 操作是否由 `CONFIG_MMU_GATHER_TABLE_FREE` 决定。现代架构通常会指定所有这些，x86-64 确实如此，我们将基于它们已指定的假设继续。

检查 Listing 7-53 所示的 `mmu_gather_batch`。

```c
struct mmu_gather_batch {
    struct mmu_gather_batch *next;
    unsigned int nr;
    unsigned int max;
    struct page *pages[];
};
```

**Listing 7-53: include/asm-generic/tlb.h: struct mmu_gather_batch**

`batch` 由页组成，这是一个正在进行 TLB 缓存失效的 `struct page` 对象数组，被定义为紧跟在其他字段之后的变长数组。它包含 `nr` 个页面，最多到 `max` 个，并指向任何下一个批次。

对于此对象的初始本地副本（通常在栈上）被设置为 `MMU_GATHER_BUNDLE`（硬编码为 8）。之后，为每个新批次分配基础页，并相应调整这些字段。

我们在 Listing 7-54 中检查了 `tlb_gather_mmu()`。

```c
/**
 * tlb_gather_mmu - 为页表销毁初始化一个 mmu_gather 结构
 *
 * @tlb: 要初始化的 mmu_gather 结构
 * @mm: 目标地址空间的 mm_struct
 *
 * 调用从 mm 初始化用于页表销毁的（栈上的）mmu_gather 结构。
 */
void tlb_gather_mmu(struct mmu_gather *tlb, struct mm_struct *mm) {
    __tlb_gather_mmu(tlb, mm, false);
}
```

**Listing 7-54: mmu/mmu_gather.c: tlb_gather_mmu()**

值得注意的是，它在整个进程空间范围内执行此操作，如 Listing 7-55 所示的 `tlb_gather_mmu_fullmm()`。

```c
/**
 * tlb_gather_mmu_fullmm - 为页表销毁初始化一个 mmu_gather 结构
 *
 * @tlb: 要初始化的 mmu_gather 结构
 * @mm: 目标地址空间的 mm_struct
 *
 * 调用从 mm 初始化用于页表销毁的（栈上的）mmu_gather 结构。
 */
void tlb_gather_mmu_fullmm(struct mmu_gather *tlb, struct mm_struct *mm) {
    __tlb_gather_mmu(tlb, mm, true);
}
```

**Listing 7-55: mmu/mmu_gather.c: tlb_gather_mmu_fullmm()**

它们之间的区别仅在于如何向 `__tlb_gather_mmu()` 传递参数，该函数如 Listing 7-56 所示执行重型工作。

```c
static void __tlb_gather_mmu(struct mmu_gather *tlb, struct mm_struct *mm,
                             bool fullmm)
{
    tlb->mm = mm;
    tlb->fullmm = fullmm;
#ifndef CONFIG_MMU_GATHER_NO_GATHER
    tlb->need_flush = 0;
    tlb->local->next = NULL;
    tlb->local->nr = 0;
    tlb->local->max = ARRAY_SIZE(tlb->pages);
    tlb->active = &tlb->local;
    tlb->batch_count = 0;
#endif

    tlb_table_init(tlb);
#ifdef CONFIG_MMU_GATHER_PAGE_SIZE
    tlb->page_size = 0;
#endif

    tlb_reset_range(tlb);
    inc_tlb_flush_pending(tlb->mm);
}
```

**Listing 7-56: mmu/mmu_gather.c: __tlb_gather_mmu()**

这初始化了 `mmu_gather` 对象的所有字段，在初始化 `tlb_table_init()` 之前将 `active` 指向本地，`tlb_reset_range()` 重置标志和结束值，如 Listing 7-57 所示。

```c
static inline void tlb_reset_range(struct mmu_gather *tlb)
{
    if (tlb->fullmm) {
        tlb->start = 0;
        tlb->end = TASK_SIZE;
    } else {
        tlb->start = TASK_SIZE;
        tlb->end = 0;
    }
    tlb->freed_tables = 0;
    tlb->cleared_ptes = 0;
    tlb->cleared_pmds = 0;
    tlb->cleared_puds = 0;
    tlb->cleared_p4ds = 0;
    /*
     * 不要重置 mmu_gather->vma* 字段，如果有中间刷新
     * 我们将再次调用 tlb_start_vma() 来设置它们。
     */
}
```

**Listing 7-57: include/asm-generic/tlb.h: tlb_reset_range()**

最后，我们调用函数 `inc_tlb_flush_pending()`，该函数增加 `mm_struct` 的 `tlb_flush_pending` 原子计数器以表示 TLB 刷新正在等待。在刷新操作完成后，将通过 `dec_tlb_flush_pending()` 减小该值，并通过 `mm_tlb_flush_pending()` 和 `mm_tlb_flush_nested()`（嵌套情况）进行检查。

## 7.1.3 VMA 取消映射

一旦我们建立了 `mmu_gather` 对象并准备好执行 TLB 操作，我们通过 `unmap_vmas()` 执行操作：

```c
/**
 * unmap_vmas - 由一组 VMA 列表覆盖的内存范围
 * @tlb: 调用者 struct mmu_gather 的地址
 * @vma: 起始 vma
 * @start_addr: 开始取消映射的虚拟地址
 */
```

**Listing 7-58: mm/memory.c: unmap_vmas()**

MMU 通知逻辑不在本文讨论范围内，尽管它简短地提供了一种机制，让相关方能够获得由例如虚拟化（为了管理客户内存）引起的关键内存管理通知。

除此之外，我们还建立了一个 `zap_details` 结构体状态，用于在擦除地址范围时。在地址范围内擦除页会移除它们的页表项，减少底层的 `struct folio->mapcount` 并执行清理工作。

`ZAP_FLAG_DROP_MARKER` 标志对用户有用，因此不在本书的讨论范围内。我们额外设置了 `even_cows` 选项，因为在此实例中我们执行的是无条件的解映射。

注意，输入参数 `vma` 仅仅是我们要遍历的范围中的第一个 VMA，将其每一个传递给 `unmap_single_vma()`（省略了超出范围的大页处理和适当处理），如 Listing 7-59 所示。

```c
static void unmap_single_vma(struct mmu_gather *tlb,
    struct vm_area_struct *vma, unsigned long start_addr,
    unsigned long end_addr,
    struct zap_details *details)
{
    unsigned long start = max(vma->vm_start, start_addr);
    unsigned long end;

    if (start >= vma->vm_end)
        return;

    end = min(vma->vm_end, end_addr);
    if (end <= vma->vm_start)
        return;

    if (unlikely(vma->flags & VM_PFNMAP))
        untrack_pfn(vma, 0, 0);

    if (start != end) {
        unmap_page_range(tlb, vma, start, end, details);
    }
}
```

**Listing 7-59: mm/memory.c: unmap_single_vma()**

对 PFN 映射的 `untrack_pfn()` 处理是特定于架构的，不在本书范围内。否则，在将 `start` 和 `end` 限制在当前 VMA 范围内后，它们会被转发到 `unmap_page_range()`，该函数会在指定的 vma 中擦除页范围。

## 7.1.4 擦除内存范围

检查 `unmap_page_range()`:

```c
void unmap_page_range(struct mmu_gather *tlb,
    struct vm_area_struct *vma,
    unsigned long addr, unsigned long end,
    struct zap_details *details)
{
    pgd_t *pgd;
    unsigned long next;

    BUG_ON(addr >= end);
    tlb_start_vma(tlb, vma);
    pgd = pgd_offset(vma->vm_mm, addr);
    do {
        next = pgd_addr_end(addr, end);
        if (pgd_none_or_clear_bad(pgd))
            continue;
        next = zap_pud_range(tlb, vma, pgd, addr, next, details);
    } while (pgd++, addr = next, addr != end);
    tlb_end_vma(tlb, vma);
}
```

**Listing 7-60: mm/memory.c: unmap_page_range()**

这遵循典型的页表遍历过程——通过 `pgd_offset()` 获取映射 `addr` 的 PGD 项的指针，然后通过 `pgd_addr_end()` 找到下一个 PGD 项。

它的不同之处在于，它使用了 `pgd_none_or_clear_bad(pgd)`，该函数通过 `pgd_none()` 检查 PGD 项是否为空，通过 `pgd_bad()` 检查它是否不符合预期，并且在此实例中清除该项。这在清除的情况下是有合理的，因为该项已损坏，而我们意图要清除它所代表的范围的至少部分，修复它的最佳手段是至少让它在已知所需状态的位置保持一致。

页表层次结构中的下一层由 `zap_pud_range()` 处理，我们稍后会返回它。

关于 MMU 收集逻辑，我们在这里的两个关键函数中看到——`tlb_start_vma()` 和 `tlb_end_vma()`，分别指示 TLB 刷新操作即将开始和即将结束。检查 Listing 7-61 所示的 `tlb_start_vma()`。

```c
/*
 * 在 tlb vma 处理的情况下
 */
void tlb_start_vma(struct mmu_gather *tlb, struct vm_area_struct *vma)
{
    if (tlb->fullmm)
        return;

    flush_cache_range(vma, vma->vm_start, vma->vm_end);
    tlb_update_flags(tlb, vma);
}
```

**Listing 7-61: include/asm-generic/tlb.h: tlb_start_vma()**

在指定了 `fullmm` 标志的情况下，无论如何，我们都是在整个进程空间上执行此操作，因此不需要考虑单个 VMA，在那种情况下函数只需直接退出。当然，在 `unmap_region()` 操作的上下文中，该标志不会被设置。

调用 `flush_cache_range()` 函数是为了确保对于需要手动缓存维护的架构，VMA 范围的 TLB 缓存是一致的，我们关注的 x86-64 不需要这一点。无论如何，都调用了 `tlb_update_flags()`，它会更新 `struct mmu_gather` 中的状态，如 Listing 7-62 所示。

```c
static inline void
tlb_update_flags(struct mmu_gather *tlb, struct vm_area_struct *vma)
{
    /*
     * tlb_range() 的实现只查看 VM_HUGE (tile,
     * 4k) 大页。
     *
     * tlb_range() 刷新 I-TLB 刷新 D-TLB。
     * 只有在 VMA 变化时才刷新。
     * 只有在 VMA 范围内才刷新。
     */
    tlb->vma_huge = vma->flags & VM_HUGETLB;
    tlb->vma_exec = vma->flags & VM_EXEC;
    tlb->vma_pfn = vma->flags & VM_PFNMAP;
}
```

**Listing 7-62: include/asm-generic/tlb.h: tlb_update_flags**
