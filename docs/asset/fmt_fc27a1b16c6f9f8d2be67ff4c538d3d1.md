
```c
/*
 * fault_around() 尝试映射异常周围的几个页面。
 * 页面将被需要的希望由 finish_fault() 处理。
 * 它只会调用一次 map_pages且不跨越 VMA 边界。
 * fault_around 定义了我们尝试映射的字节数，
 * 要求它是 2 的幂或等于 PTE_PER_PTE。
 */
static vm_fault_t do_fault_around(struct vm_fault *vmf)
{
    unsigned long length;
    unsigned long nr_pages;
    unsigned long mask;
    unsigned long address;
    pte_t start_pageff;
    pte_t end_pageff;
    int off;

    nr_pages = fault_around_bytes >> PAGE_SHIFT;
    if (nr_pages < 1)
        nr_pages = 1;

    mask = (nr_pages << PAGE_SHIFT) - 1;
    address = vmf->address & ~mask;

    start_pageff = pte_alloc(vmf, address);
    if (!start_pageff)
        return VM_FAULT_OOM;

    end_pageff = pte_alloc(vmf, address + mask);
    if (!end_pageff) {
        pte_free(start_pageff);
        return VM_FAULT_OOM;
    }

    /* 映射 start_pageff 和 end_pageff 之间页面的实际
       逻辑在此之后，确保不跨越 VMA 边界，并对于
       不在页缓存中的页面使用 map_pages 处理器。 */
    
    // ... (实现细节已省略)
    return 0;
}
```

Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

这可能超出页表范围（注意，我们也会将其此范围限制在包含它的 VMA 范围内）。

例如，一个从 `0x200000` 开始 `0x200000` 字节的范围将终止于 `0xffffff`，而不会跨越边界。

- 回到代码，我们将之前获取的掩码应用于我们的 `our-address`，将其对齐到 `fault_around` 字节。我们必须考虑到 `0x51000` 的 `vm_start` 和 `0x5f000` 的地址，例如，考虑如果我们对齐到 `0x10000`，这将产生 `0x50000` 的地址，该地址在 VMA 之前。

如果对齐后的值超过了起始值，我们通过对 VMA 起始处进行“限制（clamping）”来解决这个问题。

- 之前，我们将 `_pgoff` 设置为 `struct vm_fault->pgoff` 字段（由 `linear_page_index()` 设置），该字段将是地址在 VMA 中的页偏移量。我们必须考虑到起始地址现在可能与此产生偏移，因此要从 `start_pgoff` 中减去适当的值。

- 接下来，我们必须获取要映射的包含性页偏移量 `end_pgoff`。我们使用“限制”将范围起始部分对齐到 VMA 起始处的这一事实，这带来了一个问题——这个值可能没有与 `nr_pages` 对齐，如果我们简单地加上 `nr_pages` 页，那么无论如何我们都会映射一个页边界。我们还可能编码 VMA 的末尾 `vm_end`。为了解决这个问题，我们必须在三个值中选择最小值——PTE 的末尾、`vm_end` 以及偏移了 `nr_pages - 1` 的偏移量。我们必须记住，我们的 `start_pgoff` 值不仅编码了地址在 VMA 内的偏移，还编码了 VMA 本身在底层页缓存对象（通常是文件）中的偏移，因此这在此处需要进行一些“协调操作”。为了获得将映射到 PTE 条目的偏移量，我们必须从 `start_pgoff` 中减去目标起始地址与 PTE 不对齐的部分，这是通过掩码 `PTE_PER_PTE` 的低位来实现，然后通过页表中的最大索引（`end_pgoff` 是包含性边界）进行偏移，即加上 `PTE_PER_PTE - 1`。我们将此置于 `end_pgoff`。得到的这两个值很简单——我们可以通过将其跨越的页数（通过 `ma_pages()`）加上 VMA 的 `start_pgoff` 并减去 1，来计算出 `vm_end` 的页偏移量。

- 我们拥有了 `start_pgoff` 和 `end_pgoff`，并准备好调用 `map_pages` 处理器了。

我们将在第 9 章页缓存章节中讨论默认的 `map_pages` 处理器。

## 6.6 MAP_PRIVATE 写时复制（Copy on write）异常

当通过 `mmap()` 获取指定 `MAP_PRIVATE` 的文件映射时，这需要特殊的处理——如果发生读缺页（read-fault），这将导致写缺页，而不是映射为只读，这在硬件上等同于共享映射。然而，一旦发生写缺页，folio 就会复制到一个匿名页中。因此产生了一个非匿名映射的边缘情况，该映射可以发生写时复制（CoW）异常。重要的是，如果文件被截断导致映射的页不再有效（例如，使用 `O_TRUNC` 标志打开文件，或调用 `fttruncate()` 且大小小于或等于已映射页的大小），则映射将失效，丢失在写入 CoW 页之前写入其中的所有数据。这使得这种类型的映射具有危险性——底层文件必须保持完好，它们才能保持有效。对于共享映射也是如此，但写入的数据将写回到底层文件，因此不会丢失。此边缘情况通过 `cow_fault()` 处理（不包含 cgroup 处理，超出讨论范围），如列表 6-9 所示。

```c
static vm_fault_t do_cow_fault(struct vm_fault *vmf) {
    struct vm_area_struct *vma = vmf->vma;
    vm_fault_t ret;
    if (unlikely(anon_vma_prepare(vma)))
        return VM_FAULT_OOM;
    vmf->cow_page = alloc_page_vma(GFP_HIGHER_MOVABLE, vma, vmf->address);
    if (!vmf->cow_page)
        return VM_FAULT_OOM;
    ret = __do_fault(vmf);
    if (unlikely(ret & (VM_FAULT_ERROR | VM_FAULT_NOPAGE | VM_FAULT_RETRY)))
        goto uncharge_out;
    if (ret & VM_FAULT_DONE_COW)
        return ret;
    copy_user_page(vmf->cow_page, vmf->page, vmf->address, vma);
    __SetPageUpdate(vmf->cow_page);
    ret |= finish_fault(vmf);
    lock_page(vmf->page);
    put_page(vmf->page);
    return ret;

uncharge_out:
    put_page(vmf->cow_page);
    return ret;
}
```

列表 6:9: mm/memory.c: do_cow_fault()

这在某种程度上镜像了 `do_anonymous_page()`（见列表 6-1），不同在于它不是通过 `alloc_zero_movable()` 分配页进行复制，而是通过 `alloc_page_vma()` 并指定 `GFP_HIGHER_MOVABLE` 分配。

在此之前，通过 `anon_vma_prepare()` 设置反向映射（再次见第 7 章），因为该异常已变为匿名。

然而，这与匿名页异常不同，我们必须调用 `do_fault()` 来填充 `vm_fault->page` 字段以将其复制到 `page`。如果分配失败，返回 `VM_FAULT_OOM` 表示内存不足。

如果发生错误，我们释放对 `cow_page` 的引用并退出。否则，如果返回 `VM_FAULT_DONE_COW`，表示写时复制已完成，我们可以直接返回。

如果两者都不是，我们现在拥有了页缓存条目的指针和 CoW 匿名页指针 `vmf->cow_page`。我们必须通过 `page_to_virt()` 获取内核地址，这在 64 位系统上等同于调用 `memcpy()`。

我们将 `PG_uptate` 标记分配给 `vmf->cow_page` 作为一个匿名页，在将异常完成（包括 PTE 条目）提交给 `finish()` 之前。

此时页已被 `do_fault()` 锁定，因此我们解锁它，并通过 `put_page()` 移除引用。最后，我们检查错误情况或指示 `cow_page` 未被使用。

## 6.7 非匿名共享写缺页

当非匿名页被共享映射（即 `mmap() MAP_SHARED`）且未被读取过，它将经历由 `do_shared_fault()` 处理的共享写缺页，如列表 6-30 所示。

```c
static vm_fault_t do_shared_fault(struct vm_fault *vmf) {
    struct vm_area_struct *vma = vmf->vma;
    vm_fault_t ret, tmp;
    ret = __do_fault(vmf);
    if (unlikely(ret & (VM_FAULT_ERROR | VM_FAULT_NOPAGE | VM_FAULT_RETRY)))
        return ret;
    /*
     * 检查备份空间是否想要知道页
     * 将变为可写
     */
    if (vma->vm_ops->page_mkwrite) {
        unlock_page(vmf->page);
        tmp = do_page_mkwrite(vmf);
        if (unlikely(tmp | (tmp & (VM_FAULT_ERROR | VM_FAULT_NOPAGE)))) {
            put_page(vmf->page);
            return tmp;
        }
    }
    ret = finish_fault(vmf);
    if (unlikely(ret & (VM_FAULT_ERROR | VM_FAULT_NOPAGE | VM_FAULT_RETRY))) {
        unlock_page(vmf->page);
        put_page(vmf->page);
        return ret;
    }
    ret |= fault_dirty_shared_page(vmf);
    return ret;
}
```

列表 6:30: mm/memory.c: do_shared_fault()

Linux 内存管理器（早期访问）© 2025 Lorenzo Stoakes

## 正如列表 6-31 所示，检查 `do_page_mkwrite()`（省略超出范围的交换逻辑）。

```c
/*
 * 通知地址空间该页即将变为可写，以便其
 * 能够禁止此操作，或等待页进入适当状态。
 * 我们在不持有锁的情况下执行此操作，以便它在需要时可以睡眠。
 */
static vm_fault_t do_page_mkwrite(struct vm_fault *vmf)
{
    vm_fault_t ret;
    struct page *page = vmf->page;
    unsigned int old_flags = vmf->flags;

    vmf->flags = FAULT_FLAG_WRITE|FAULT_FLAG_MKWRITE;
    ret = vmf->vma->vm_ops->page_mkwrite(vmf);
    /* 恢复原始标志，以防调用者感到意外 */
    vmf->flags = old_flags;
    if (unlikely(ret & (VM_FAULT_ERROR | VM_FAULT_NOPAGE)))
        return ret;
    if (unlikely(!ret & VM_FAULT_LOCKED))) {
        lock_page(page);
        if (page->mapping) {
            unlock_page(page);
            return 0; /* 重试 */
        }
        ret = VM_FAULT_LOCKED;
    } else {
        VM_BUG_ON_PAGE(!PageLocked(page), page);
        return ret;
    }
}
```

6-31: mm/memory.c: do_page_mkwrite()

这允许底层文件系统拒绝对页（folio）的写访问，或者在读映射变为可写时（从 `wp_page_shared()` 调用，在第 6.9 节讨论）或当共享映射在没有中间读取的情况下首次写入时，执行允许此类操作的操作。

这最终会调用 `vm_area_struct` (VMA) 的对象结构 `vm_operations_struct vm_ops->page_mkwrite` 处理程序，并带有 `FAULT_FLAG_WRITE` 和 `FAULT_FLAG_MKWRITE` 标志。

之后，如果发生错误或指示异常已处理，我们将退出。如果有必要，我们会重新锁定页，并且（指示文件截断或其他形式的失效导致其不再有效）相对于其相关的 `struct address_space` 对页进行失效，函数返回一个值，这告知 `do_shared_fault()` 异常已完成（并将重试）。

与其他异常处理程序的另一个不同之处是调用了 `fault_dirty_shared_page()`，它用于处理以下情况：要么只读非匿名映射转变为易变的（关于此类情况的递归请参见第 6.9 节），或者像这里一样，共享映射中新写入的页。该函数在调用时页是链接状态的，这意味着它可以依赖于页在整个操作期间保持稳定，并在完成操作后释放它。我们将该函数细节的讨论推迟到页缓存章节。

## 6.8 共享非匿名异常逻辑

非匿名异常处理程序处理共享逻辑——`__do_fault()`（它在页中执行实际的异常，并在执行时锁定它）以及 `finish_fault()`（它执行异常调入页的实际映射，并假设在执行该操作时它已锁定）。

让我们首先检查 `__do_fault()`，省略列表 6-32 所示的超出范围的页逻辑：

```c
/*
 * 进入时必须持有 mmap_lock，并可能根据标志和
 * vma->vm_ops->fault() 的返回值被释放。
 * 参见 filemap_fault() 和 lock_page_retry().
 */
static struct vm_fault __do_fault(struct vm_fault *vmf)
{
    struct vm_area_struct *vma = vmf->vma;
    struct vm_fault *ret;
    /* 在获取 page_lock 之前预分配 pte，因为这可能导致
    * memcg 回收死锁，因为它在等待回写中的页：
        lock_page(A)
        SetPageWriteback(A)
        unlock_page(A)
    * lock_page(B)
    * pte_alloc_one
        * shrink_page_list
        wait_on_page_writeback(A)
        SetPageWriteback(A)
        unlock_page(B)
    * flush A, B 以清除回写
    */
    if (pmd_none(*vmf->pmd) && !vmf->prealloc_pte) {
        vmf->prealloc_pte = pte_alloc_one(vma->vm_mm);
        if (!vmf->prealloc_pte) {
            return VM_FAULT_OOM;
        }
    }

    ret = vma->vm_ops->fault(vmf);
    if (unlikely(ret & (VM_FAULT_ERROR | VM_FAULT_NOPAGE | VM_FAULT_RETRY | VM_FAULT_DONE_COW))) {
        return ret;
    }
    if (unlikely(!ret & VM_FAULT_LOCKED))) {
        lock_page(vmf->page);
    } else {
        VM_BUG_ON_PAGE(!PageLocked(vmf->page), vmf->page);
    }
    return ret;
}
```

列表 6-32: mm/memory.c:_do_fault()
