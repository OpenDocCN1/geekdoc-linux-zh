
folio_mark_dirty(folio);

if (fail) {
    put_swap_page(&folio->page, entry);
    return false;
}

Listing 12-20: mm/swap_state.c: add_to_swap()

我们使用 `folio_alloc_swap()` 开始分配交换项，我们将在列表 12-21 中检查它（省略了大页和 cgroup 的处理）。

这使用了每个 CPU 的交换缓存，并尝试从这里分配，而不是从介质（文件）分配交换项。如果分配成功，返回的 `swap_entry_t` 指示它包含的具体文件偏移量。如果没有足够的空间分配交换，我们返回 false。如果我们成功分配了交换项，则继续通过 `add_to_swap_cache()` 将其添加到交换缓存中。此时，将 folio 标记为脏是非常关键的，我们预计会如此。

交换内存 1128

Linux 内存管理器 (早期访问版) © 2025 Lorenzo Stokes

Linux 内存管理器（早期访问）© 2025 Lorenzo Lorenzo Stoakes

```c
120          address_space->nrpages += nr;
121      mod_node_page_state(page, pgdat(page), NR_FILE_PAGES, nr);
122      mod_lruvec_page_state(page, NR_SWAPCACHE, nr);
123 unlock:
124      xas_unlock_irq(xas);
125      while (xas_nomem(&xas, gfp));
126
127      if (lvas_error(&xas))
128          return 0;
129
130      ClearPagesSwapCache(page);
131      page_ref_sub(page, nr);
132      return xas_error(&xas);
133  }
```

列表 12-2: mm/swap_state.c: add_to_swap_cache()

在 `add_to_swap_cache()` 中，我们可以观察到通过 `swap_address_space()` 获取的 `struct address_space` 对象（如列表 12-4 所示）利用 `struct address_space->pages` xarray 来存储交换页（有关 xarray 的更多信息，请参阅第 9 章第 9.2 节）。

我们不会深入讨论这里使用的 xarray 原语（再次，请参见第 9.2 节的详细分析），而是讨论如何更新 folio 和交换地址空间，以标记该 folio 处于交换缓存中。

我们通过 `swp_offset()` 获取交换地址空间内的偏移量（参见列表 12-6），然后构建 xarray 状态，以便遍历 folio 中包含的相关的子页。

在这种情况下，folio 优于 `order-0` 的唯一情况是它是一个透明巨页（Transparent Huge Page）。这超出了本书的范围，但我们可以看到通过 `tp_nrpages()` 获取子页数量（它仅仅查找复合页数，关于复合页的更多详细信息，请参阅第 2 章）。

我们通过 `page_ref_add()` 增加引用计数来固定 folio，并并通过 `SetPageSwapCache()` 宏生成的辅助函数用 `PG_swapcache` 标志标记 folio。

对于 folio 的每个子页，我们通过使用 `set_page_private()` 函数将其 `struct page_private` 字段设置为描述其在该交换地址空间中位置的 `swap_entry_t`。注意，如果是复合 folio，我们会对每个条目加上子页索引偏移，以考虑到其在 xarray 中的偏移。

我们在第 12.1.2 节中讨论如何访问此 folio。它最终通过 `folio_mapping()` 访问，我们在列表 12-8 中检查其与交换相关的部分。

我们更新 `struct address_space->nrpages` 字段以计算交换地址空间中的条目数量，并相应地更新统计数据。

交换内存 1131

最后，如果没有发生错误，我们直接退出；否则，我们清除 folio 的 `PG_swapcache` 标志，通过 `page_ref_sub()` 取消其固定并返回错误。

## 12.2.2 设置页表交换条目

回到图 12-1，我们观察到在向交换缓存中添加条目后，回收程序将通过 `try_unmap()` 移除页表映射，我们在列表 12-23 中检查它。

```c
/**

 * try_to_unmap - 尝试移除指向 folio 的所有页表映射。

 * @folio 要取消映射的 folio。

 * @flags: 动作和标志

 * 尝试移除所有映射到此

 * @folio 的页表条目。调用者负责在需要时检查 folio

 * 是否仍映射（使用 TTU_SYNC 防止计数竞争）。

 * 上下文：调用者必须持有 folio 锁。

 */

void try_to_unmap(struct folio *folio, enum ttu_flags flags) {

    struct rmap_walk_control rwc = {

        .rmap_one = try_to_unmap,

        .arg = (void *)flags,

        .done = page_not_mapped,

        .anon_lock = folio_anon_read,

    };

    if (flags & TTU_RMAP_LOCKED)
        rmap_walk_locked(folio, &rwc);
    else
        rmap_walk(folio, &rwc);

}
```

列表 12-23: mm/rmap.c: try_unmap()

`try_unmap()` 函数利用反向映射（详情参见第 7 章）找到可能引用指定 folio 的 `struct vm_area_struct` (VMA) 映射，并调用指定的回调函数 `try_to_unmap()`，我们在列表 12-4 中检查其交换特定的代码。

如果 `page_not_mapped()` 函数返回 `true`，则停止遍历；`folio_mapped()` 返回 `false` 则原子地检查 `struct folio->mapcount` 是否大于零（这等于 folio 的映射数减一，值为 0 则表示未映射）。

我们将 `ttu_flags` 传递给指定操作选项的函数，我们不会详细检查这些。

第 22 章

我们在列表 12-4 中检查 `try_to_unmap_one()` 中的交换特定逻辑（交换处理、`shrink_page_list()` 设置的 TTU 标志、MMU 通知器、巨页处理、`userfault`、架构特定的虚拟化、通过 `madvise()` 懒惰释放、高 RSS 处理、架构特定的 PTE 处理）。

```c
static bool try_to_unmap_one(struct folio *folio, struct vm_area_struct *vma,
                               unsigned long address, void *arg) {

    struct mm_struct *mm = vma->vm_mm;
    DEFINE_FOLIO_WALK(page, vma, address, 0);
    pte_t pteval;
    struct page *subpage;
    bool ret = true;
    enum ttu_flags flags = (enum ttu_flags)arg;

    while (page_mapped_walk(page)) {

        /* 如果 folio 处于 mlock 中，我们不能交换它 */

        if (!flags & TTU_NORE_MLOCK) &&
            (vma->vm_flags & VM_LOCKED) {

            /* 恢复丢失的 mlock */
            mlock_folio(folio, vma);
            page_mapped_done(page);
            ret = false;
            break;
        }

        subpage = page(pte_fn(*page) - pte_fn(folio));
        address = page->address;
        anon_exclusive = folio_test_anon(folio) &&
                         PageAnon(subpage);

        if (folio_test_hugelb(folio)) {

        } else {

            /* 杀死页表条目。当需要清除
            PageAnon() 时，我们必须 flush。 */

            if (should_defer_flush(mm, flags) && anon_exclusive) {
                pteval = pte_get_and_clear(address, page);
            } else {
                pteval = pte_clear_flush(vma, address, page);
            }

            /* pte 消失后在 folio 上设置脏标记 */

            if (pte_dirty(pteval))
                folio_mark_dirty(folio);

            if (PageHWPoison(subpage) && !(flags & TTU_IGNORE_HWPOISON)) {

            } else if (test_anon(folio)) {
                swap_entry_t entry = { .val = page_parse(subpage)};
                pte_t swp_pte;

                if (swap_duplicate(entry) < 0) {
                    set_pte_at(mm, address, page, pteval);
                    ret = false;
                    page_mapped_done(page);
                    break;
                }

                if (anon_exclusive &&
                    page_try_share_anon_rmap(subpage)) {
                    swap_free(entry);
                    set_pte_at(mm, address, page, pteval);
                    ret = false;
                    page_mapped_done(page);
                    break;
                }

                dec_mm_counter(mm, MM_ANONPAGES);
                inc_mm_counter(mm, MM_SWAPENTS);
                swp_pte = swap_entry_to_pte(entry);

                if (anon_exclusive)
                    swp_pte = pte_swp_mk(swp_pte);

                if (pte_soft_dirty(pteval))
                    swp_pte = pte_mksoft_dirty(swp_pte);

                set_pte_at(mm, address, page, swp_pte);
            } else {
                page_remove_rmap(subpage, vma, folio_test_hugetlb(folio));
                folio_put(folio);
            }
        }
    }
    return ret;
}
```

列表 12-24: mm/rmap.c: try_to_unmap_one() 交换逻辑

`try_to_unmap_one()` 函数开始时声明了一个 `page_vma_mapped_walk` 类型（参见列表 12-25），用于在遍历映射 folio 的页表时线程状态，通过 `DEFINE_FOLIO_VMA_WALK()` 初始化并通过 `page_mapped_walk()` 迭代。

```c
struct page_vma_mapped_walk {
    unsigned long pfn;
    unsigned long nr_pages;
    pgoff_t pgoff;
    struct vma_area_struct *vma;
    unsigned long address;
    pmd_t *pmd;
    pte_t *pte;
    spinlock_t *flags;
    unsigned int flags;
};
```
