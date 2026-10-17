
# 第 10 章

Linux 内存管理器（早期访问）© 2025 Lorenzo Stoakes

## 列表 10-58: fs/writeback.c: writeback_sb_inodes(inode) 初始检查

```c
1802          redirty_tail(inode, wb);
1803          continue;
1804      }
1805      /*
1806        * 该 inode 属于不同的 superblock。
1807        * 返回调用者以释放该锁
1808        * 并锁定下一个 superblock。
1809        */
1810      break;
1811  }
1812 
1813  /*
1814      * 不要管新的 inode 或正在释放的 inode，
1815      * 它们现在不需要周期性回写，
1816      * 后者的回写由释放器处理。
1817      */
1818 
1819      spin_lock(&inode->i_lock);
1820      if (inode->state & (I_NEW | I_FREEING | I_WILL_FREE)) {
1821          redirty_tail_locked(inode, wb);
1822          spin_unlock(&inode->i_lock);
1823          continue;
1824      }
1825      if ((inode->state & I_SYNC) && wbc.sync_mode == WB_SYNC_ALL)
1826      {
1827          /*
1828          * 如果此 inode 锁定回写且我们正在
1829          * 进行数据完整性回写，将其移动
1830          * 到 b_more_io以便回写继续处理
1831
1832          * 其他 b_io 上的节点。
1833
1834
1835          * 我们在完整扫描 b_io 后将再次
1836
1837          * 将对此 inode 进行回写。
1838          */
1839          requeue_io(inode, wb);
1840          spin_unlock(&inode->i_lock);
1841
1842          continue;
1843      }
1844      spin_unlock(&wb->list_lock);
1845      /*
1846      * 如果设置了 I_SYNC 且正在进行
1847      * WB_SYNC_NONE 回写，我们已将 inode 入队。因此此处捕捉
1848      * WB_SYNC_ALL 情况。
1849      */
1850      if (inode->state & I_SYNC) { /* 此函数释放 i... */
1851          /* 等待 I_SYNC.*/
1852          inode_sleep_on_writeback(inode);
1853          /* inode 可能已消失，重新开始 */
1854          spin_lock(&wb->list_lock);
1855          continue;
1856      }
```

为了了解此检查的上下文，我们检查 `writeback_sb_inodes()` 是如何被调用的。它是由 `__writeback_inodes_wb()`（参见列表 10-56）或 `writeback()`（参见列表 10-55）调用的。

在一种情况下，`__writeback_inodes_wb()` 由 `writeback_inodes_wb` 调用，后者指定了一个未指明 `sb` 的 `struct wb_writeback_work` 结构体，并反向遍历 inode，通过 `struct inode->i_sb` 指定超级块来调用 `writeback_sb_inodes()`；或者由 `wb_writeback()` 调用，后者仅在未指定 `struct writeback->work` 的情况下才调用。

当我们对 inode 队列时，使用 `move_expired_inodes()`（参见列表 10-47，当此函数由列表 10-46 所示的 `queue_io()` 调用时，我们确保 inode 是按超级块分组的）。

因此，在出现自 `__writeback_inodes_wb()` 的回写的情况下，对 `work->sb` 的测试并不适用，它直接跳出循环（从而排除了该函数），导致 `__writeback_inodes_wb()` 迭代到下一个超级块，该超级块在卸载时会被锁定的。

另一种情况是从 `wb_writeback()` 的调用（参见列表 10-55），其中 `wb_writeback_work->sb` 是被指定的。

`struct wb_writeback_work->sb` 参数在两个地方设置：`__writeback_inodes_sb()`（参见列表 10-42）和 `sync_inodes_sb()`（参见列表 10-39），这些一个由 `sync()` 或 `syncfs()` 系统调用触发，后者遍历所有超级块并限制于单个。

我们可以在图 10-7 中观察这些函数如何工作以及如何唤醒回写刷器（flusher）。

在这些实例中，当我们通过 `queue_io()` 队列时，属于任何超级块的 inode 确实可以被用于回写，我们将其添加到 `struct bdi_writeback->wb_dirty` 列表中。

由于我们依赖于 inode 按超级块进行分区，通过在每次遇到无关 inode 时简单的继续循环，我们最终将达到“重新标记脏”（redirty）的 inode，这些 inode 最终需要回写。

由于我们持续对 inode 进行“重新标记脏”，它们最终会被再次拾起。如果它们是属于 `struct bdi_writeback->work_list` 中特定同步结构 `struct wb_writeback` 任务的 inode，它们将直接由 `wb_workfn()` 调度到以后（参见列表 10-44）；如果它们被设置为后台或更新刷新，这些将由 `wb_workfn()` 处理并进入队列。我们可以在图 10-10 中看到此逻辑如何适配到 `wb_writeback()`。

“重新标记脏”过程是由列表 10-59 所示的 `redirty_tail()` 执行的。

## 列表 10-59: fs/fs-writeback.c: redirty_tail()

```c
1308 static void redirty_tail(struct inode *inode, struct bdi_writeback *wb)
1309 {
1310     spin_lock(&inode->i_lock);
1311     redirty_tail_locked(inode, wb);
1312     spin_unlock(&inode->i_lock);
1313 }
```

这锁定了 inode 并将实际的重新标记脏推迟到列表 10-60 所示的 `redirty_tail_locked()`。

## 列表 10-60: fs/fs-writeback.c: redirty_tail_locked()

```c
/*
 * 为 inode 重新标记脏：设置其变脏的时间戳，并将其移动到
 * 其所属超级块脏 inode 列表的最远端。
 * 在标记 inode 的 ->dirtied 之前，我们检查它是否已经是
 * b_dirty 列表上最近被标记为脏的 inode。如果是那样，
 * 则该 inode 在写入过程中可能已经被重新标记为脏，
 * 我们不重置其变脏时间（dirtied when）。
 */
static void redirty_tail_locked(struct inode *inode, struct bdi_writeback *wb)
{
    assert_spin_lock(&inode->i_lock);

    if (!list_empty(&wb->b_dirty)) {
        struct inode *tail;

        tail = wb_inode(wb->b_dirty.next);
        if (time_before(inode->dirtied, tail->dirtied)) {
            inode->dirtied = jiffies;
        }

        inode_list_move_locked(inode, wb, &wb->b_dirty);
        inode->i_state |= ~I_SYNC_QUEUED;
    }
}
```

这使用 `inode_list_move_locked()` 将 inode 移动到 `struct bdi_writeback->b_dirty` 列表的尾部，清除其 `I_SYNC_QUEUED` 标志以指示该 inode 不再处于队列状态（该标志由列表 10-47 所示的 `more_expired_inodes()` 设置）。

> **注意**
>
> 尽管函数名为 `redirty_tail_locked()`，但 `inode_io_list_move_locked()` 函数最终调用的是 `list_move()` 而不是 `move_tail()`，这意味着 inode 实际上被放置在 `struct bdi_writeback->b_dirty` 的头部而非尾部。然而，由于我们是反向处理 inode，因此该 inode 被放置在该列表的末尾，从而被视为脏的。

我们必须小心 inode 的时间戳，维护 `struct bdi_writeback->b_dirty` 中 inode 的顺序至关重要，因此在将 inode 放置于列表头部之前，我们检查现有的头部。如果它比这旧（它是列表中最年轻的），我们就将其标记为当前时间。

回到我们正在检查的列表 10-58 `writeback_sb_inodes()` 初始检查，我们获取 `struct inode->i_lock` 以在后续检查时保持 inode 稳定。

我们检查 inode 是新的、正在释放还是即将被释放。正如注释所示，这些情况目前都不需要。我们在持有 inode 锁的情况下直接使用 `redirty_tail_locked()` 重试 inode，并继续处理下一个。

最后，我们检查 inode 正在被回写的情况。这可能发生在 `writeback_single_inode()` 被触发以立即回写 inode 时。为了简洁起见，我们不检查 `writeback_single_inode()`，它仅使用用户指定的回写对象显式回写单个 inode。在这些调用之间，inode 通过 `I_SYNC` 标志进行序列化，该标志在检查完成后立即设置。

这种情况有两种变体——回写完成意味着数据已写入磁盘而不仅仅是被调度回写，这由 `struct wb_writeback->sync_mode` 设置为 `WB_SYNC_ALL` 表明。在不需要的情况下，我们可以通过将其放入 `struct bdi_writeback->b_io_list` 来重新队列 inode 以待以后处理。

## 列表 10-61: fs/fs-writeback.c: requue_io()

```c
/*
 * bdi->b_io 列表耗尽后，重新队列 @inode。
 */
static void requue_io(struct inode *inode, struct bdi_writeback *wb)
{
    inode_list_move_locked(inode, &wb->b_io_more);
}
```

你可以在图 10-10 中的 `writeback()` 中观察 `struct bdi_writeback->b_io_more` 如何被处理。注意该列表中的所有项都会被立即用于下一次 `queue_io()` 调用（参见列表 10-46）。

然而，我们需要同步，我们并不移动 inode，而是通过 `inode_sleep_on_writeback()` 等待回写过程完成。一旦这些检查完成，我们就准备在列表 10-62 所示的 `writeback_sb_inodes()` 中进行实际的回写。

## 列表 10-62: fs/fs-writeback.c: __writeback_sb_inodes() writeback

```c
inode->state = I_SYNC;

wb_attach_and_unlock_inode(&wb, inode);

write_chunk = writeback_chunk_size(wb, work);

wb.nr_to_write = write_chunk;

wb.pages_skipped = 0;
```

```c
/*
 * 使用 I_SYNC 将 inode 固定在内存中。当它被设置时，
 * evict_inode() 将等待以便 inode 无法释放。
 */

__writeback_single_inode(inode, wbc);

wbc_detach_inode(wbc);

work->nr_pages -= write_chunk - wbc->nr_to_write;

write = write_chunk - wbc->nr_to_write - wbc->pages_skipped;

wrote = write < 0 ? 0 : write;

total_write += wrote;
```

我们首先通过 `I_SYNC` 标记正在处理回写的 inode，防止内核的任何其他部分同时尝试回写（即 `writeback_single_inode()`）或从内存中驱逐 inode 元数据。

`wbc_attach_and_unlock_inode()` 函数不在讨论范围内，因为它特定于 cgroup 管理的回写，但注意其函数名暗示了 inode 锁。

在此处我们确定一次操作中回写多少页。对于同步回写（即 `struct wb_writeback_work->sync_mode` 设置为 `WB_SYNC_ALL`）或所有带有 `wb_writeback_work->tagged` 回写的任务，这种分块并不适用（这适用于 `inodes_sb_nr()` 和 `inodes_wbc()`，两者都由 `sync()` 和/或 `fsync()` 调用）。

我们将 `writeback_chunk_size()` 的描述推到列表 10-102 的第 10.14 节，因为这直接涉及内核内的脏数据限流逻辑。

再次，`wbc_detach_inode()` 函数不在本书范围内。其功能因此在 `__writeback_single_inode()` 中执行，我们在下面的列表 10-67 中检查了它。

回写启动后，统计数据将相应更新——`struct wb_writeback_work->nr_pages` 减去已回写或跳过的页数，实际写入的页添加到 `total_write` 计数器，该计数器最终返回给调用者。

最后，我们检查列表 10-63 中核心循环末尾的回写后处理。

## 列表 10-63: 回写后处理

```c
/*
 * 如果 @inode 仍为脏，则重新队列。小心，因为 @inode
 * 在此期间可能切换到另一个 wb。
 */
tmp_wb = inode_to_wb_and_lock_list(inode);

spin_lock(&inode->i_lock);
    if (!(inode->i_state & I_DIRTY_ALL))
        total_write++;
        requeue_inode(inode, tmp_wb, &wbc);
        inode_sync_complete(inode);
spin_unlock(&inode->i_lock);

if (unlikely(tmp_wb != wb)) {
    spin_unlock(&tmp_wb->list_lock);
    spin_lock(&wb->list_lock);
}

/*
 * 跳出到 wb_writeback() 并留足够的空间来检查
 * 背景阈值和其他终止条件。
 */
if (total_write) {
    if (time_is_before_jiff(start_time + HZ / 100UL))
        break;
    if (work->nr_pages <= 0)
        break;
}

return total_write;
```
