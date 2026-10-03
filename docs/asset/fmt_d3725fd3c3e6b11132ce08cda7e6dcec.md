
# 列表 10-63: fs/wb-writeback.c:wb_inodes() 后缀

我们开始查找与 inode 关联的当前 `struct bdi_writeback` 对象。如果实施了 cgroup 组调度的写回，这可能会发生变化，我们对此留了考虑（尽管这部分的讨论超出了本书的范畴）。如果 inode 元数据被写入，我们还会增加 `total_write`。

此时有两个函数处于激活状态——`requeue_inode()`，它决定 inode 是否需要重新入队列或其写回是否已完成；我们将在列表 10-64 的 `inode_sync_complete()` 中检查它，其核心任务是清除 inode 的 `I_SYNC` 标志，唤醒任何等待该它的进程。

此后，函数将检查硬编码的十分之一秒的间隔时间是否超过了之前存储的操作的操作开始时间，如果是的话，我们将跳出循环并返回 `wb_writeback()`（参见列表 10-55），并按照图 10-10 所示继续进行，在发生了会导致写回终止的竞争情况的情况下。

`requeue_inode()` 中的重队列逻辑至关重要的是检查了 inode 是否已完全写出、剩余部分以及将 inode 放置的位置。我们将在列表 10-64 中检查它（省略了范围外的脏数据处理）。

### 列表 10-64: fs/writeback.c: requeue_inode()

该函数处理每个 inode，决定是通过 `dirty_tail_locked()`（参见列表 10-60）将其放回 `struct bdi_writeback->b_dirty` 列表、通过 `requeue_io()`（参见列表 ??）将 I/O 重队列到 `struct bdi_writeback->b_io` 列表，还是通过 `inode_cgwb_move_to_attached()`（参见列表 10-65）从这些列表中移除。

我们在图 10-11 中探讨此函数的逻辑。

图 10-11：request_inode() 逻辑

我们首先检查 inode 是否正在被释放，以便最终被驱逐。此外，否则写回代码将跳过释放 inode，不会产生影响。

然后我们考虑在执行同步写回时的一种特殊情况，即 inode 可能会被重新启动并处理。我们通过重置 `inode->dirtied` 时间戳为现在来避免这种情况，这会导致 `wb_writeback()`（参见列表 10-55）在下次循环中，如图 10-10 所示。

接下来我们确定是否由于文件系统拒绝写回而跳过了某些页，该计数维护在 `writeback_control->pages_skipped` 中。如果是这样，那么我们无法对该 inode 继续操作（可能需要释放锁），因此我们通过 `dirty_tail_locked()` 弄脏该 inode（参见列表 10-60）。

然后我们考虑 inode 仍然脏的情况——在此实例中我们必须要求 inode，因为它尚未完成写回 I/O。

我们通过使用与 inode 关联的 `address_space` 的 `mapping_tagged()` 来确定是否仍然脏。如果是，我们根据剩余脏数据继续。

在这种情况下，我们已经写入了或超过了当前块的大小，我们需要通过 `queue_io()`（参见列表 ??）请求后续 I/O。

如果不是数据切片不足以写回整个 inode，我们采取安全路径并简单通过 `dirty_tail_locked()` 弄脏 inode。

如果与 inode 关联的页不是脏的，但 inode 指明元数据需要写回，在此实例中我们也 `dirty_tail_locked()`。

```c
/**
 * inode_cgwb_move_to_attached - 将 inode 放入 wb_attached 列表
 * @inode: 持有 i_lock 的感兴趣的 inode
 * @wb: bdi_writeback
 * 
 * 从 wb 中移除 inode 并在必要时放入 _attached
 * 列表。只有附加到 cgwb 的 inode 会保留在此列表中。
 */
static void inode_cgwb_move_to_attached(struct inode *inode, struct bdi_writeback *wb)
{
    assert_spin_locked(&wb->list);
    assert_spin_locked(&inode->i_lock);
    inode->i_state &= ~I_SYNC_QUEUED;
    if (wb != inode->io_list->bdi->wb)
        list_move(&inode->io_list, wb->b_attached);
    else
        list_del_init(&inode->io_list);
    wb_io_lists_depopulated(wb);
}
```

### 列表 10-65: inode_cgwb_move_to_attached(struct inode *inode, struct bdi_writeback *wb)

```c
list_empty(wb->b_io) && list_empty(wb->b_io) {
    clear_bit(wb->has_dirty_io, wb->state);
    WARN_ON_ONCE(atomic_sub_return(wb->avg_write_bandwidth,
        wb->bdi->tot_write_bandwidth) < 0);
}
```

### 列表 10-66: fs/fs-writeback.c: wb_io_lists_depopulated

当 `struct bdi_writeback` 列表为空时，这将重置 `wb_has_dirty_inode` 标记并更新回写统计数据。

```c
/*
 * 将 inode 及其脏页（或其部分脏页，取决于
 * @wb->nr_to_write 的值）写入磁盘，并从 i_state 中清除相关的脏位标记。
 * 这不会将 inode 从其所在的回写列表中删除，除非
 * 通过时间戳过期将其从 b_dirty_time 移动到 b_dirty。
 * 其他情况下由调用者处理回写列表。
 * 调用者还负责预先设置 I_SYNC 标记，并在之后
 * 调用 inode_sync_complete() 来完成同步。
 */
static int
writeback_single_inode(struct inode *inode, struct writeback_control *wbc)
{
    struct address_space *mapping = inode->i_mapping;
    long nr_to_write = wbc->nr_to_write;
    unsigned dirty;
    int ret;

    WARN_ON(inode->i_state & I_SYNC);
    ret = do_writepages(mapping, wbc);

    /*
     * 确保等待元数据的写入完成。
     * 这对于在数据 I/O 完成后修改元数据的
     * 文件系统至关重要。我们不对 sync(2) 回写进行这样做，
     * 因为它有独立的外部 I/O 完成路径和 ->sync_fs
     * 用来保证 inode 元数据被正确回写。
     */
    if (wbc->sync_mode == WB_SYNC_ALL && !wbc->for_sync) {
        int err = filemap_fdatasync(mapping);
        if (ret == 0)
            ret = err;
    }

    /*
     * 从 i_state 中获取并清除脏标记。这需要在调用
     * writepages 之后执行，因为某些文件系统可能会在
     * writepages 期间重试 inode 以释放。它还需要在
     * 处理时间戳过期后执行，因为那可能也会标记 inode。
     */
    spin_lock(&inode->i_lock);
    dirty = inode->i_state &= ~I_DIRTY_PAGES; 

    /*
     * 与 __mark_inode_dirty() 中的 smp_mb() 配对使用。这允许
     * inode_dirty() 在不获取 i lock 的情况下测试 i_state，
     * 要么看到 I_DIRTY 位被清除，要么我们看到脏的
     * inode。
     * 即使 @mapping 仍有脏页，I_DIRTY_PAGES 也会被一起清除。
     * 如果必要，在 smp_mb() 之后会恢复该标记。
     * 这保证了 __mark_inode_dirty() 要么看到清除的
     * I_DIRTY_PAGES，要么我们看到 PAGECACHE_TAG_DIRTY。
     */
    smp_mb();
    if (mapping_tagged(mapping, PAGECACHE_TAG_DIRTY)) {
        inode->i_state = I_DIRTY_PAGES;
    }
    spin_unlock(&inode->i_lock);

    /* 如果只设置了 I_DIRTY_PAGES，则不写入 inode */
    if (dirty & ~I_DIRTY_PAGES) {
        int err = write_inode(inode, wbc);
        if (ret == 0)
            ret = err;
    }

    return ret;
}
```

### 列表 10-67: fs/writeback.c: __writeback_single_inode()

此函数立即调用了列表 10-23 和第 10.10 节所示的 `writepages()`，它执行实际的回写。剩余的函数清理任务在完成后完成。

我们涵盖了同步回写的情况，这种情况并非源于 `sync()` 或 `syncfs()` 等同步系统。在其他情况下，写入操作由调用函数 `writeback_inodes_sb()`（见列表 10-40）和 `sync_inodes_sb()`（见列表 10-39）处理，因此在这些实例中，`writeback_single_inode()` 不执行工作。对于其他同步情况，情况并非如此，我们必须显式说明，这是通过我们在后续文件回写第 10.13 节的列表 10-72 中检查的 `filemap_fdatawait()` 实现的。

在此函数的所有调用中，无论操作结果如何，在 `struct inode->i_lock` 下 inode 的脏标记都会被清除。

如果我们随后发现至少一个页缓存包含的 inode 数据仍为脏，我们无论如何都会通过仔细的锁协商来更新 inode 状态，将内存屏障与 `__mark_inode_dirty()`（见列表 10-2）配对，允许后者在不加锁的情况下检查 `inode->i_state`。最后，如果 inode 元数据是脏的，则通过 `write_inode()` 回写 inode，但这超出了本书的范畴。

# 10.13 文件回写

我们已经看到回写是如何以文件为粒度进行的，但还有另一种进行回写的方法——以页为粒度进行。用户可以通过 `fsync()` 或 `fdatasync()` 调用请求将打开的文件描述符同步到磁盘，并通过 `msync()` 请求对 `mmap()` 映射文件的单个页进行同步。

> **注意** 用户也可以通过 `sync_file_range()` 指定打开的文件描述符的单个页的同步，然而，非常不建议使用该系统因为它是危险的，因此我们不进行详细检查。在任何情况下，该系统最终都会调用我们在这里检查的相同函数。我们在第 10-6 节和图 10-4 中检查了这些同步方法，它们最终会调用内核函数 `filemap_flush()`（见列表 10-68）、`file_write_and_range()`（见列表 10-74）和 `filemap_fdatawait()`（见列表 10-72）。此外，我们观察到 `writeback_single_inode()`（见列表 10-67）调用了 `filemap_fdatawait()`。
