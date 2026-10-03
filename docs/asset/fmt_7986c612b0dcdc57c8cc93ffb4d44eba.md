
`unmap_mapping_range(mapping, holebegin, 0, 1);`

Listing 9-94: mmap/truncate_pagecache()

这取消映射了已经缩小的 folio 部分（如果确实使用 `unmap_mapping_range()` 来执行取消映射，我们在第 9.9.3 节中检查这一点）。

取消映射在截断之前执行一次，之后又执行一次，注释指出，这样做是为了减少截断需要执行的操作数量，并处理任何晚到的写时拷贝（Copy-on-Write）异常。

它将实际的截断推给了 `truncate_inode_pages()`，我们将在列表 9-96 中检查。

在检查此之前，我们先检查列表 9-95 中的 `truncate_inode_pages_final()`。

```c
/**
 * truncate_inode_pages_final - 在 inode 销毁前截断*所有*页面
 * @mapping: 要截断的映射
 * 在 inode->i_rwsem 保护下（并序列化）
 * 文件系统必须在 .evict_inode 路径中使用此函数，以通知
 * VM 这是最后的截断，且 inode 即将移除。
 * void truncate_inode_pages_final(struct address_space *mapping)
 */
```

```c
/*
 * 页面无法参与常规的 inode 生命周期周期管理（无法调用 input()），
 * 因此可能与 inode 拆卸发生竞争。在地址退出时告诉它，
 * 这样它就不会在最后的截断开始后安装驱逐信息。
 */
```

```c
mapping_set_exiting(mapping);
```

```c
if (!mapping_empty(mapping)) {
    /*
     * 由于截断使用了无锁树查找，
     * 循环树锁以确保任何没有看到 AS_EXITING 的
     * 正在进行的修改在开始最后的截断之前完成。
     */
    xa_lock_irq(&mapping->_i_pages);
    xa_unlock_irq(&mapping->_i_pages);
}
```

```c
truncate_inode_pages(mapping, 0);
```

Linux 内存管理器（早期访问版）The Linux Memory Manager (Early Access) © 2025 by Lorenzo Stoakes

488 }

Listing 9-95: mm/truncate.c: truncate_inode_pages_final()

此函数在 inode 被完全销毁之前被调用，它最终将截断操作（由于文件正在被移除，大小设置为零）推给了 `truncate_inode_pages()`，我们将在列表 9-96 中检查。

```c
/**
 * truncate_inode_pages - 从某个偏移开始截断*所有*页面
 * @mapping: 要截断的映射
 * @start: 开始截断的偏移量
 *
 * 在 inode->i_rwsem 和 mapping->invalidate_lock
 * 保护（并序列化）调用。
 *
 * 注意：当此函数返回时，指定范围内可能有一个
 * 正在删除的页面（使用 __filemap_remove_folio()）。因此
 * 即使在截断了整个映射后，此函数返回时 mapping->nrpages
 也可能不为零。
 */
truncate_inode_pages(struct address_space *mapping, loff_t lstart)
{
    truncate_inode_pages_range(mapping, lstart, (loff_t)-1);
}
EXPORT_SYMBOL(truncate_inode_pages);
```

Listing 9-96: mm/truncate.c: truncate_inode_pages_range()

此函数调用 `truncate_inode_pages_range()` 并指定结束为无边界。我们在列表 9-98 中检查此函数。
内核还提供了 `truncate_pagecache_range()`，我们将在列表 9-97 中检查。

```c
/**
 * truncate_pagecache_range - 取消映射并移除被“打洞”的页缓存
 * @inode: 节点
 * @start: 洞的起始偏移量
 * @end: 洞的最后一个字节的结束
 *
 * 此函数通常在文件系统释放与空闲范围相关的资源
 *（例如释放块）之前调用。这样一来，页缓存始终在逻辑
 * 上与磁盘格式保持一致，文件系统将不必处理诸如
 * 对一个底层块已释放释放的页面调用 writepage 的情况。
 */
truncate_pagecache_range(struct inode *inode, loff_t lstart, loff_t len)
{
```

746 第 9 章

```c
struct address_space *mapping = inode->mapping;
loff_t unmap_start = round_up(lstart, PAGE_SIZE);
loff_t unmap_end = round_down(1 + len, PAGE_SIZE) - 1;
```

```c
/*
 * 这种舍对目前仅用于示例：unmap_mapping_range
 * 将其洞向外扩展，而我们希望向内收缩洞。
 * 现有的 truncate_pagecache_range 调用者会先执行
 * 自己的页面运行。注意 unmap_mapping_range
 * 允许所有情况的 holelen，且我们允许 -1 表示文件末尾。
 */
```

```c
/*
 * 与 truncate_pagecache 不同，unmap_mapping_range 只被调用
 * 次（在截断页缓存之前），且没有 "even_cows" 标志：
 * 打洞操作不应移除洞中的 COW 页面。
 */
```

```c
if ((u64)unmap_end > lstart)
    unmap_mapping_range(mapping, unstart,
        1 + unmap_end - unmap_start, 0);
truncate_inode_pages_range(lstart, len);
```

Listing 9-97: mm/truncate.c: truncate_pagecache_range()

这为文件系统提供了“打洞”的方法，即删除文件的部分内容使其被视为稀疏文件。当我们这样做时，必须取消映射被打洞的范围并在该范围内进行截断。

此函数通过 `unmap_mapping_range()` 取消映射打洞的范围，并在 `truncate_inode_pages_range()` 中截断打洞的范围，我们将在列表 9-98 中检查（排除了实时调度器提示和调试检查）。

```c
/**
 * truncate_inode_pages_range - 由起始和结束偏移量指定的页面范围
 * @mapping: 要截断的映射
 * @lstart: 开始截断的偏移量
 * @len: 要截断的偏移量（包含）
 *
 * 截断页缓存，移除指定偏移量之间的页面
 * （并对部分页面置零）
 */
```

Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

```c
364 folio = __filemap_get_folio(mapping, lstart >> PAGE_SHIFT, FGP_LOCK,
365 0);
```
366 if (folio) {
367 same_folio = lend < folio_pos(folio) + folio_size(folio);
368 if (!truncate_inode_partial_folio(folio, lstart, len)) {
369 start = folio->index + folio_nr_pages(folio);
370 if (same_folio) {
371 end = folio->index;
372 }
373 folio_unlock(folio);
374 folio_put(folio);
375 folio = NULL;
376 }
```

377 378 if (!same_folio) folio =

```c
380 if (folio) {
381 if (!truncate_inode_partial_folio(folio, lstart, len)) {
382 end = folio->index;
383 folio_unlock(folio);
384 folio_put(folio);
385 }
```

列表 9-100: mm/truncate.c: truncate_inode_pages_range() 部分截断 (Partial Truncation)

我们首先设置 `same_folio` 来指示该范围在同一页内的起始和结束位置。我们稍后对其进行纠正，以考虑高阶 folio（higher order folios）。

- 我们使用 `FGP_LOCK` 表示该 folio 应该被锁定，并传递给 `__filemap_get_folio(mapping)` 以获取 folio。如果该锁当前正被竞争，它将等待锁可用。
- 一旦获取到，我们会更新 `same_folio` 以考虑到 folio 可能是高阶的，在调用 `truncate_inode_partial_folio()` 之前执行实际的繁重工作。
- 在这种情况下，如果是一个较大的 folio 且我们无法将其拆分，我们会更新整个截断范围的起始（可能还有结束）位置以跳过它（尽管这种行为不在本书的讨论范围内）。
- 在执行此操作后，我们会解锁并释放 folio 的引用计数，然后在对范围的端点执行相同的操作。
- 完成后，我们继续执行操作的第二次遍历，我们将在列表 9-101 中探讨它。

```
401 if (!find_get_entries(mapping, index, end - 1, &fbatch, indices)) {
402 /* 如果从开始之后的所有项都了，我们就完成了 * */
```

第 9 章

Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

```
if (index == start)
    break;
/* 否则重启以确保所有项都消失 */
    index = start;
    continue;

for (i = 0; i < folio_batch_count(&batch); i++) {
    struct folio *folio = fbatch.folios[i];

    /* 我们依赖删除操作不会改变 page->index */
    index = indices[i];

    if (xa_is_value(folio))
        continue;

    folio_lock(folio);

    folio_wait_writeback(folio);
    truncate_inode_folio(mapping, folio);
    folio_unlock(folio);
    index = folio_exindex(folio) + folio_nr_pages(folio) - 1;

truncate_folio_batch_exceptions(mapping, &batch, indices);
folio_batch_release(&batch);
index++;
}
```

列表 10-1: truncate.c: truncate_inode_pages_range() 第二次遍历 (Second Pass)

在这次遍历中，我们通过 `find_get_entries()` 获取原始项（参见列表 9-40 和第 9.5.1 节）。

我们像之前一样继续。如果 `find_get_entries()` 失败（因为所有项都已删除），那么如果操作已部分完成，我们重启以确保获取所有内容，否则终止。

注意，我们可能会遇到被上一次遍历删除的项。我们依赖于以下事实：即使在项被删除时，我们也特意保留了 `struct folio->index` 字段，以便跟踪范围内的索引（这些由 `find_get_entries()` 放置在 `indices` 数组中）。

- 我们跳过非指针项，然后特意等待 folio 锁可用（参见列表 9-137），然后再等待任何回写完成（参见列表 9-146 和第 9.11 节关于 folio 锁定细节）。
- 通过依赖 `truncate_inode_folio()` 执行实际的截断，确保了如果 folio 未被截断，它是稳定的。

页面缓存 (Page Cache) Linux 内存管理器（早期访问版）© 2025 Lorenzo Stoakes

## 接下来我们在列表 9-10 中检查 `truncate_inode_folio()`

```c
190 int truncate_inode_folio(struct address_space *mapping, struct folio *folio)
191 {
192 if (folio->mapping != mapping)
193         return -EIO;
194
195     truncate_cleanup_folio(folio);
196     filemap_remove_folio(folio);
197     return 0;
198 }
```

列表 9-10: mm/truncate.c: truncate_inode_folio()

此函数假设传入的 folio 已锁定，如果其他人先到达那里，我们无可做并返回错误表示这是意外的。我们通过 `truncate_cleanup_folio()` 执行截断（我们在列表 9-103 中检查它），通过 `filemap_remove_folio()` 完全移除 folio（参见：

```
163 /*
* 如果 truncate 无法从页面中移除 fs-private 元数据，
164 页面将变成孤儿（orphaned）。它将留在 LRU 中，并且如果我们在与 filemap_fault() 竞争，
165 被映射。
166 * 如果 folio->mapping 不再等于 mapping，我们需要退出。
167 这种情况发生在：a) 当我们等待锁时 VM 回收了页面，
168 b) 并发的 invalidate_mapping 先到达那里，
169 c) tmpfs 在 tmpfs 和 address_space 之间切换页面。
 */
172 static void truncate_inode_folio(struct folio *folio)
173 {
174     if (folio_mapped(folio))
175         unmap_mapping_folio(folio);
176
177     if (folio_has_private(folio))
178         folio_invalidate(folio, 0, folio_size(folio));
179
180     /*
181      * 某些文件系统在失效后重新标记页面为脏
182      * VM 取消了脏位（例如 ext3 日志）
183      * 因此，脏检查被放在失效之后
184      */
185     folio_cancel_dirty(folio);
186     folio_clear_mapped(folio);
187 }
```

列表 9-103: mm/truncate.c: truncate_cleanup_folio()

如果 folio 当前处于映射状态（通过 `unmapping_folio()` 中的 `folio_mapped()` 推断，参见列表 9-106），我们对其取消映射。如果 folio 具有指示文件系统必须失效的私状态，在这种情况下调用 `folio_invalidate()`，由于 `struct address_space->_ops` 中指定的 `address_space_operations` 类型拥有 `invalidate_folio()` 处理器，这会调用该处理程序。最后，我们有一些边界情况需要处理——在移除标记之前通过 `folio_cancel_dirty()` 撤销一个脏标记。最后在列表 9-104 中处理 `truncate_inode_partial_folio()`（省略了范围之外的页面处理）。

- * 处理部分 folio。如果拆分操作与我们竞争，folio 可能完全在范围内。如果不是，我们清空 folio 在 `[start, end)` 范围内的部分，然后如果它很大，则将其拆分。`split_page_range()` 会丢弃可能位于 i_size 以下的页面，我们依赖调用者丢弃位于新创建 folio 中的页面。
- * 如果拆分失败，调用者可以避免丢弃整个顽固不被拆分的 folio。
