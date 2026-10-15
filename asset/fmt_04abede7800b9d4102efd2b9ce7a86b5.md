
# 8.1.5.2 核心非快速 GUP 函数

所有非快速 GUP 函数最终都会调用 `__get_user_pages_locked()`。该 GUP 的大部分用于处理异常重试逻辑，这发生在 `lock` 参数不为 NULL 的地方。检查函数开头，调用者整体不希望重试：

```c
/*
 * 请注意，此函数与 __get_user_pages 不同，
 * 在没有 FOLL_NOWAIT 的情况下，nr_pages > 0 时不会返回 0。
 */
static __always_inline long __get_user_pages_locked(struct mm_struct *mm,
      unsigned long start,
      unsigned long nr_pages,
      struct page **pages,
      struct vm_area_struct **vmas,
      int *locked,
      unsigned int flags)
{
    long ret, pages_done;
    bool lock_dropped;

    if (locked) {
        /* 如果返回 VM_FAULT_RETRY，vmas 将失效 */
        BUG_ON(vmas);
        /* 检查调用者是否初始化 locked */
        BUG_ON(*locked != 1);
    }

    if (flags & FOLL_PIN) {
        /* ... 为了省略省略实现 ... */
    }

    return 0;
}
```

## mm_set_has_pinned_flag(mm->flags);

```c
/*
* FOLL_PIN 和 FOLL_GET 是互斥的。传统的行为
* 是如果调用者填充了 pages[]（但由于疏忽没有
* 指定 FOLL_GET），则继续设置 FOLL_GET，
*
* 这种做法是针对 FOLL_GET 的，而不是针对较新的 FOLL_PIN。
 * FOLL_PIN 总是期望 pages 不空，但没有必要进行断言，
 * 因为任何失败都会足够明显。
 */
if (pages && (flags & FOLL_PIN)) {
    flags = FOLL_GET;
}

pages_done = 0;
lock_dropped = false;

for (;;) {
    ret = __get_user_pages(mm, start, nr_pages, flags, vmas, locked);
    if (!locked) {
        /* VM_FAULT_RETRY 无法触发，跳过 */
        return ret;
    }
}
```

列表 8-30: mm/mm.c: `get_user_pages_locked()` 非重试逻辑

我们在执行 `__get_user_pages()` 中的繁重工作之前，执行一些性检查，如果指定了页面但缺少此标志，则设置 `FOLL_GET`。如果页面需要固定，我们还会为前述的 `mm_struct` 对象设置 `MMF_HAS_PINNED` 标志。

锁管理器决定缺页机制返回的 `VM_FAULT_RETRY` 或 `VM_FAULT_COMPLETED` 是否可以被处理。当文件支持的 folio 通常为了回写而被锁定，且缺页处理程序设置了 `FAULT_FLAG_ALLOW_RETRY` 标志时（有关此特定行为，参见第 6 页关于缺页异常和页缓存处理程序的节），便会返回这些值。

当此标志被设置且无法获取锁时，会释放 `struct mm->mmap_lock` 以避免在回写操作阻塞，并在不等待锁释放的情况下进展，从而减少对 `mmap_lock` 的竞争。
只有能够处理锁被释放的函数才能做到，具体来说 `get_user_pages_remote()` 和 `get_user_pages_unlocked()` 及其调用者——它们通过向锁参数传递 NULL，因此在这些情况下会跳过此逻辑。

检查处理此情况的函数部分部分为了清晰起见，从循环开始重新）：

```c
for (;;) {
    ret = __get_user_pages(mm, start, nr_pages, flags, pages,
    vmas, locked;
```

```c
/* VM_FAULT_RETRY 或 VM_FAULT_COMPLETED 无法返回错误 */
if (!locked) {
    BUG_ON(ret < 0);
    BUG_ON(ret >= nr_pages);
}

if (ret > 0) {
    nr_pages = ret;
    pages_done += ret;
    if (!nr_pages)
        break;
}

if (*locked) {
    /*
     * VM_FAULT_RETRY 没有触发，或者是一个
     * FOLL_NOWA。
     */
    if (pages_done)
        pages_done = ret;
    break;
}

/*
 * VM_FAULT_RETRY 已触发，因此跳转到发生故障的偏移。
 * 对于预取情况 (!pages)，我们只更新计数。
 */
if (likely(pages))
    pages += ret;
start += ret << PAGE_SHIFT;
lock_dropped = true;

retry:
```

```c
/*
 * 在触发 VM_FAULT_RETRY 的地址上重复执行，
 * 同时使用 FAULT_FLAG_ALLOW_RETRY 和
 * FAULT_FLAG_TRIED。注意 GUP 可能会被
 * 信号中断，因此在再次尝试之前
 * 我们需要检查它，否则可能会无限循环。
 */
if (fatal_signal_pending(current)) {
    if (!pages_done)
        pages_done = -EINTR;
    break;
}
```

```c
ret = mmap_read_lock_killable(mm);
if (ret) {
    BUG_ON(ret > 0);
    if (!pages_done)
        pages_done = ret;
    break;
}

*locked = 1;
ret = __get_user_pages(mm, start, 1, flags | FOLL_TRIED,
    pages, NULL, locked);
if (!locked) {
    /* 继续重试直到成功 */
    BUG_ON(ret != 0);
    goto retry;
}

if (ret == 1) {
    BUG_ON(ret > 1);
    if (!pages_done)
        pages_done = ret;
    break;
}

nr_pages--;
pages_done++;
if (!nr_pages)
    break;

if (likely(pages))
    pages++;
start += PAGE_SIZE;
if (lock_dropped && *locked) {
    /*
     * 我们让调用者知道临时释放了锁，
     * 保护的临界区域丢失了。
     */
    mmap_read_unlock(mm);
    *locked = 0;
}
return pages_done;
```

列表 8-31: mm/get_user_pages() 重试逻辑如下：

1.  通过 `_get_user_pages()` 尝试处理地址处的 `nr_pages`。
2.  断言没有发生错误且处理的页面比预期的多（`_get_user_pages()` 返回正数或负数错误）。
3.  如果我们处理了足够的页面，更新 `nr_pages` 和 `pages_done`，退出循环。
4.  我们现在处于仍有页面的位置——如果锁已释放，我们不在重试逻辑中，必须退出。
5.  如果提供了 `pages` 数组，则根据处理的页面数量更新偏移。
6.  无论是否指定了偏移和设置了锁释放，在重新获取锁之前，我们让调用者知道锁已释放。
7.  通过 `fatal_signal_pending()` 检查是否有致命信号。如果是，则此操作无效，我们应该退出循环。
8.  通过 `read_lock_killable()` 尝试重新获取 `struct mm->mmap_lock` 的读锁。如果失败，我们返回错误。
9.  在 `_get_user_pages()` 中尝试使用 `FOLL_TRIED` 以指示我们已获取一次（如果锁已释放），从第 6 步继续重试此操作直到成功或发生错误。
10. 成功后，如果我们完成了，更新计数和偏移，退出循环；否则从第 1 步重复整个操作直到完成或发生错误。

```c
/**
 * _get_user_pages() - 在内存中固定页面
 * @mm:
 *    目标 mm 的 mm_struct
 * @start: 起始用户地址
 * @nr_pages: 从 start 到固定的页面数
 * @gup_flags: 修改固定的标志
 * @pages: 接收固定页面指针的数组。
 *    长度至少为 nr_pages。或者如果调用者仅确保页面发生缺页，则为 NULL。
 * @vmas: 对应每个页面的 vmas 指针数组。
 *    如果调用者不需要，则为 NULL。
 * @locked:
 *    我们是否持有 mmap_lock
 * 返回固定的页面数（可能小于请求的数量），或错误。
 * 关于返回值的详情：
- 如果 nr_pages 为 0，返回 0。
- 如果 nr_pages > 0，但某些页面已固定，返回 -errno。
- 如果 nr_pages > 0，且某些页面已固定，返回固定的页面数。再次，这可能小于 nr_pages。
- 当需要重试缺页时，可能返回 0 值。
- 调用者负责通过 `put_page()` 释放 @pages。
- @vmas 仅在 mmap_lock 持有时有效。
- 必须在持有 mmap_lock 时调用。它可能会被释放。见下文。
- __get_user_pages 遍历进程页表，并对每个用户地址在给定时刻对应的每个页面获取引用。也就是说，它获取线程在那个时刻访问给定用户虚拟地址时会访问的页面。
- 这不能保证在 __get_user_pages 返回时页面存在于用户映射中，在某些情况下可能是完全不同的页面（例如，如果 mmappagecache 已失效，则不会被完全释放）。而且主要只关心页面包含在*某个时间点*有效的数据。通常，IO 或类似操作无法保证任何内容，因为锁无法持有到系统调用边界。
- 如果 @gup_flags & FLAG_WRITE ==，则必须写入页面。如果写入了页面，必须在页面处理完成后并在调用 `put_page` 之前调用 `@set_page_dirty`（或相应的 `@set_page_dirty_lock`）。
- 如果 @locked != NULL，当 `up_read()` 释放 mmap_lock 时，@locked 将设置为 0。这可能发生在 @gup_flags 没有 HAVE_NOTIFY 时。
- 使用此类 @locked 和 @gup_flags 组合的调用者必须仅以读持有 mmap_lock，并识别其被释放的情况。
- 在大多数情况下，应该使用 `__get_user_pages` 或 `get_user_pages_fast` 代替 `__get_user_pages`。只有在某些特殊的 @gup_flags 时，才使用 `__get_user_pages`。
 */
```

```c
unsigned int gup_flags, struct page **pages,
struct vm_area_struct **vmas, int *locked)
```

```c
{
long ret = 0, i = 0;
struct vm_area_struct *vma = NULL;
struct follow_page_context ctx = { NULL };
if (!nr_pages)
    return 0;
start = untagged_addr(start);
VM_BUG_ON(||pages) !!(gup_flags & (FOLL_GET | FOLL_PIN));
/*
 * 如果设置了 FOLL_FORCE，则不强制完整扫描，因为提示
 * 缺页信息与使用该地址空间的任务的引用行为
 * 无关
 */
if ((gup_flags & FOLL_FORCE))
    gup_flags |= FOLL_NUMA;
```

# Linux 内存管理器（早期访问版） © 2025 Lorenzo Stoakes
