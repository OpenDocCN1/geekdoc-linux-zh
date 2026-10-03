
# 列表 9-81: `include/linux/pagemap.h`: `__readhead_folio()`

该函数将重负载工作推给了 `__readhead_folio()`，并在完成后将 folio 的引用计数减至一次。我们在列表 9-82 中检查 `__readhead_folio()`（省略了一些可能会分散注意的检查）。

```c
static inline struct folio *__readhead_folio(struct readhead_control *ractl)
{
    struct folio *folio;

    ractl->nr_pages = ractl->batch_count;
    ractl->index_idx = ractl->batch_count;

    if (!ractl->nr_pages) {
        folio->batch_count = 0;
        return NULL;
    }

    folio = xa_load(&ractl->mapping->i_pages, ractl->index);
    ractl->batch_count = folio_nr_pages(folio);

    return folio;
}
```

# 列表 9-82: `include/linux/pagemap.h`: `__readhead_folio()`

所有操作都是按照 `struct readhead_control->_batch_count` 字段确定的粒度执行的，该字段在处理上一个 folio 的大小时会被设置。

这是因为 readhead 状态被设置为指向我们正在加载的 folio，因此在下一次迭代中，我们必须知道上一个 folio 的大小以便跳转到下一个。

这简单地使用 `xa_load()` 从当前 readhead 索引处的页缓存中检索 folio，如果超过了 readhead 的大小，则返回 NULL。

因此，该函数可以用于我们目前为止看到的循环中，以遍历 readhead 范围内的每个 folio。

## 9.8 周围缺页

为了尽量减少花费在内存缺页上的时间，页缺页机制会在 `do_read_fault()` 中对读缺页执行“周围缺页”（fault-around）。

重要的是，这只执行次要缺页（minor faults），即分批处理已经存在于页缓存中的内存，跳过任何需要主页缺页（major fault）的操作。

我们在页缺页章节的第 6.5 节中讨论了这种缺页机制，但为了方便起见，我们在这里重复审查 `do_fault_around()`（之前在列表 6-28 中显示），见列表 9-83。

```c
/*
 * do_fault_around() 尝试映射缺页地址周围的几个页面。希望
 * 这些页面很快就会被需要，这将减少需要处理的
 * 缺页次数。
 *
 * 它使用 vm_ops->map_pages() 来映射页面，如果页面尚未
 * 准备好映射，则跳过该页面：例如未更新、已锁定等。
 *
 * 此函数不会跨越 VMA 边界，以便仅调用一次
 * map_pages()。
 *
 * do_fault_around 定义了我们将尝试映射的页数。
 * do_fault_around() 期望该值被设置为一个幂且小于或等于
 * TRS_PER_PTE 的 2 次幂。
 *
 * vm 自然对齐的区域的虚拟地址
 * fault_around 会向下取整到机器页大小
 * （因此是对齐到页阶数）。这样更容易保证
 * 我们不会跨越页表边界.
 */
static vm_fault_t do_fault_around(struct vm_fault *vmf)
{
    unsigned long address = vmf->address, nr_pages, mask;
    pgoff_t start_pgoff = vmf->pgoff;
    pgoff_t end_pgoff;
    int off;

    nr_pages = READ_ONCE(fault_around_bytes) >> PAGE_SHIFT;
    mask = ~(nr * PAGE_SIZE - 1) & PAGE_MASK;
    address = max(address, mask, vma->vma_start);
    off = ((vmf->address - address) >> PAGE_SHIFT) & (TRS_PER_PTE - 1);
    start_pgoff = off;
    /*
     * end_pgoff 是页表的末尾、vm 的末尾
     * 或者从 start_pgoff 开始的 nr_pages，取决于哪个最近。
     */
    end_pgoff = start_pgoff;
    ((address) >> PAGE_SHIFT) & (TRS_PER_PTE - 1)) +
    TRS_PER_PTE - 1;
    end_pgoff = min3(end_pgoff, vma_pages(vmf->vma) + vmf->vma_pgoff -
    1); start_pgoff + nr_pages - 1);

    if (pmd_none(vmf->pmd)) {
        vmf->prealloc_pte = pte_alloc(vmf->vma->mm);
        if (!vmf->prealloc_pte)
            return VM_FAULT_OM;
    }

    return vmf->vma->vm_ops->map_pages(vmf, start_pgoff, end_pgoff);
}
```

列表 9-83: `memory/map.c`: `do_fault_around()`

简单来说，如果文件系统支持，它会读取数据（可以通过 `/sys/kernel/debug/fault_around` 调优）到缺页地址 64 KiB 或 16 个页面（如 x86）。我们将范围的起始对齐到缺页地址，然后对齐到页数（例如地址 `0x0` 将缺页 `0xffff` 范围内的页面）。我们将其限制在页表边界，以避免获取锁的复杂性问题。关于这种缺页的更多细节请见页章节第 6.5 节，我们将详细探索此代码。在这里我们将关注 `vma_area_struct (VMA)` 的 `vm_ops->map_pages()` 函数，它在此处执行重负载工作（作为 `struct vm_operations` 回调）。在读取数据和处理文件映射缺页时，文件可以自由操作，但在此情况下使用库函数。我们在列表 9-84 中检查此函数（排除超出范围的大页和硬件中毒）。

```c
vm_fault_t filemap_map_pages(struct vm_fault *vmf,
    pgoff_t start_pgoff, pgoff_t end_pgoff)
{
    struct vma_area_struct *vma = vmf->vma;
    struct file *file = vma->vm_file;
    struct address_space *mapping = file->f_mapping;
    pgoff_t last_pgoff = start_pgoff;
    unsigned long addr;
    XA_STATE(xas, mapping->i_pages, start_pgoff);
    struct folio *folio = NULL;
    struct page *page = NULL;
    unsigned int mmap_miss = READ_ONCE(file->f_ra.rmap_miss);
    vm_fault_t ret = 0;

    rcu_read_lock();
    folio = first_map_page(mapping, &xas, end_pgoff);
    if (!folio)
        goto out;

    :
    addr = vma->vm_start + ((start_pgoff - vma->vm_pgoff) << PAGE_SHIFT);
    vmf->pte = pte_offset_lock(vma->vm_mm, vmf->pmd, &vmf->ptl);

    do {
        page = folio_file_page(folio, xas_xa_index);
        if (mmap_miss > 0)
            mmap_miss--;

        addr += (xas.xa_index - last_pgoff) << PAGE_SHIFT;
        vmf->pte += xas.xa_index - last_pgoff;
        last_pgoff = xas.xa_index;

        /*
         * 注意：如果存在 PTE 标记，我们将它们留给特定的
         * 缺页路径处理，这将阻止
         * 周围缺页逻辑。
         */
        if (!pte_none(*vmf->pte))
            goto unlock;

        /* 我们正准备处理缺页 */
        if (vmf->address == addr)
            ret = VM_FAULT_NOPAGE;

        do_set_pte(vmf, page, addr);
        /* 无需失效：不存在的页面不会被缓存 */
        update_mm_cache(vma, addr, vmf->pte);
        folio_unlock(folio);
        continue;

    lock:
        folio_unlock(folio);
        folio_put(folio);
    } while ((folio = next_map_page(mapping, &xas, end_pgoff)) != NULL);

    pte_unlock(vmf->ptl);

out:
    rcu_read_unlock();
    WRITE_ONCE(file->f_ra.rmap_miss, mmap_miss);
    return ret;
}
```

列表 9-84: `file/map.c`: `filemap_map_pages()`

Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

此模拟了 `linear_page_index()` 中的逻辑，进一步的讨论请参阅围绕该列表 7-23 展开的讨论。

一旦获取此地址，我们就会通过 `pte_offset_map_lock()` 获取锁（关于页表和锁的详细信息，请参阅“虚拟内存”章节）。

获取此锁后，我们能够操作 PTE 条目，从而非常快速地执行一次缺页异常（minor fault）操作。

我们循环执行，在每次迭代中调用 `next_map_page()`（参见列表 ??）以获取下一个有效页。

请注意，在此阶段，通过调用 `update_page()` 调用的 `first_map_page()` 或 `next_map_page(both)` 已经增加了引用计数，并获取了 folio 的锁，同时也确保了它在更新期间是稳定的且没有被截断。

如果 folio 的大小大于 `order-0`，我们实际上可能会遇到同一个 folio，查找函数只是简单递增索引。我们在每个循环开始时，通过 `folio_file_page()` 确定当前索引处的 `struct subpage`。

我们跟踪 `struct file->f`、`struct file_page_state->imap_miss readacount`，我们在操作完成后对其进行更新。

在确定 PTE 是否为空之前，我们更新了偏移量以考虑到这可能是较大 folio 中的一个子页——只有在它为空时继续操作才是合法的，因此如果它是空的，我们就移动到下一页。

如果缺页异常字段 `struct vm_fault->address` 已经设置为目标地址，这表明文件系统特定的异常处理程序已经安装了地址，因此我们返回值 `VM_FAULT_NOPAGE` 以指示这一点。

在此阶段，我们实际设置 PTE 指向已找到的页，即通过 `do_set_pte()` 执行一次缺页异常（关于此函数的详细解释，请参见第 6.8 节中的列表 6-35）。

对于需要的架构（x86-64 不需要），通过 `update_mmu_cache()` 指明该页表已更新。在我们继续之前，任何 TLB 操作都不要求 PTE 条目必须为空。

在此之后，我们解锁 `struct folio` 并循环到下一页——记住，我们确保不会跨越页表边界，因此只需要为单个 PTE 获取一次此锁。

现在我们已经了该函数的核心逻辑，让我们回到列表 9-87 中的 `next_update_page()`。

```c
3265 static struct folio *next_update_page(struct folio folio,
3266             struct address_space *mapping,
3267             struct xa_state *xas, pgoff_t end_pgoff
3268 {
3269             unsigned long max_idx;
    do {
        if (!folio)
            return NULL;
        if (xas_retry(xas, folio))
            continue;
        if (xa_is_value(folio))
            continue;
        if (folio_test_locked(folio))
            continue;
        if (!folio_try_get_rc(folio))
            continue;
        /* 页是否移动或拆分了? */
        if (unlikely(folio != xas_reload(xas))
            goto skip;
        if (folio_test_updatate(folio) || folio_test_readahead(folio))
            goto skip;

    skip:
        if (!folio_trylock(folio))
            goto skip;
        if (folio->mapping != mapping)
            goto unlock;
        if (!folio_test_updatate(folio))
            goto unlock;
        max_idx = DIV_ROUND_UP(i_size_read(mapping)->host, PAGE_SIZE);
        if (xas->xa_index >= max_idx)
            goto unlock;
        return folio;

    unlock:
        folio_unlock(folio);

    skip:
        while (folio = xas_next_entry(xas, end_pgoff)) != NULL {
            return NULL;
        }
}
```
