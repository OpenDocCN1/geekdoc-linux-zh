
```c
struct mm_struct {
    struct vm_area_struct *mmap; /* 内存区域列表 */
    struct rb_root mm_rb; /* VMA 的红黑树 */
    struct vm_area_struct *mmap_cache; /* 最后使用的内存区域 */
    unsigned long free_area_cache; /* 地址空间空洞列表 */
    pgd_t *pgd; /* 页全局目录 */
    atomic_t mm_users; /* 地址空间使用者 */
    atomic_t mm_count; /* 主要使用计数器 */
    int map_count; /* 内存区域数量 */
    struct rw_semaphore mmap_sem; /* 内存区域信号量 */
    spinlock_t page_table_lock; /* 页表锁 */
    struct list_head mmlist; /* 所有 mm_struct 的列表 */
    unsigned long start_code; /* 代码起始地址 */
    unsigned long end_code; /* 代码结束地址 */
    unsigned long start_data; /* 数据起始地址 */
    unsigned long end_data; /* 数据结束地址 */
    unsigned long start_brk; /* 堆起始地址 */
    unsigned long brk; /* 堆最终地址 */
    unsigned long start_stack; /* 堆栈起始地址 */
    unsigned long arg_start; /* 参数起始位置 */
    unsigned long arg_end; /* 参数结束位置 */
    unsigned long env_start; /* 环境起始位置 */
    unsigned long env_end; /* 环境结束位置 */
    unsigned long rss; /* 已分配的页 */
    unsigned long total_vm; /* 页总数 */
    unsigned long locked_vm; /* 锁定页数量 */
    unsigned long saved_auxv[AT_VECTOR_SIZE]; /* 保存的 auxv */
    cpumask_t cpu_mask; /* 惰性 TLB 切换掩码 */
    mm_context_t context; /* 架构特定数据 */
    unsigned long flags; /* 状态标志 */
    int core_waiters; /* 线程核心转储等待者 */
    struct core_state *core_state; /* 核心转储支持 */
    spinlock_t ioctx_lock; /* AIO I/O 列表 */
    struct hlist_head ioctx_list; /* AIO I/O 列表 */
};
```

`mm_users` 字段是使用此地址空间的进程数量。例如，如果两个线程共享此地址空间，`mm_users` 等于 2。`mm_count` 字段是 `mm_struct` 的主要引用计数。所有 `mm_users` 等同于 `mm_count` 的一次递增。因此，在之前的示例中，`mm_count` 仅为 1。如果有九个线程共享一个地址空间，`mm_users` 将是 9，但 `mm_count` 仍然仅为 1。只有当 `mm_users` 达到零（即使用某个地址空间的所有线程退出时），`mm_count` 才会递减。当 `mm_count` 最终达到零时，不再有任何剩余引用该 `mm_struct`，并且会被释放。

当内核操作地址空间并需要增加其关联引用计数时，内核会递增 `mm_count`。拥有两个计数器使内核能够区分主使用计数器（`mm_count`）和使用该地址空间的用户进程数量（`mm_users`）。

`mmap` 和 `mm_rb` 字段是两种不同的数据结构，包含相同的内容：该地址空间中的所有内存区域。前者以链表形式存储它们，而后者以红黑树形式存储它们。红黑树是一种二叉树；与所有二叉树一样，搜索给定元素是一个 `O(log n)` 的操作。关于红黑树的进一步讨论，请参见本章后面的“内存区域的链表和树”。

尽管内核通常避免使用两种数据结构来组织相同数据所带来的额外负担，但这里的冗余却很有用。作为链表的 `mmap` 数据结构允许简单且高效地遍历所有元素。另一方面，作为红黑树的 `mm_rb` 数据结构更适合搜索给定元素。内存区域将在本章后面详细讨论。内核并未复制 `mm_struct` 结构；只是复制了包含的对象。在树上覆盖链表，并使用两者来访问同一组数据，有时被称为线程化树。

所有的 `mm_struct` 结构都通过 `mmlist` 字段串联成一个双向链表。列表中的初始元素是 `init_mm` 内存描述符，它描述了 `init` 进程的地址空间。该列表通过 `mmlist_lock` 保护，防止并发访问，该锁定义在 `kernel/fork.c` 中。

## 分配内存描述符

与给定任务关联的内存描述符存储在任务进程描述符的 `mm` 字段中。（进程描述符由 `task_struct` 结构体表示，定义在 `<linux/sched.h>` 中。）因此，`current->mm` 是当前进程的内存描述符。`copy_mm()` 函数在 `fork()` 期间将父进程的内存描述符复制给子进程。`mm_struct` 结构体通过 `kernel/fork.c` 中的 `allocate_mm()` 宏从 `data_cachep` slab 缓存中分配。通常，每个进程接收一个独特的 `mm_struct`，从而拥有独特的进程地址空间。

进程可以通过 `clone()` 的 `CLONE_VM` 标志选择与子进程共享地址空间。此时，该进程被称为线程。回顾第 3 章“进程管理”，这本质上是 Linux 中普通进程和所谓线程之间唯一的区别；Linux 内核在其他方面不区分它们。对于内核来说，线程只是共享某些资源的普通进程。

如果指定了 `CLONE_VM`，则不会调用 `allocate_mm()`，进程 `mm` 字段被设置为指向父进程的内存描述符，通过 `copy_mm()` 中的以下逻辑实现：

```c
if (!clone_flags & CLONE_VM) {
    /*
     * current is the parent process and
     * task is the child process during a fork()
     */
    atomic_inc(&current->mm->mm_users);
    task->mm = current->mm;
}
```

### 销毁内存描述符

当与特定地址空间关联的进程退出时，调用定义在 `kernel/exit.c` 中的 `exit_mm()` 函数。该函数执行一些清理工作并更新一些统计数据。然后调用 `mmput()`，该函数将内存描述符的 `mm_users` 用户计数器递减。如果用户计数达到零，则调用 `mm_drop()` 递减 `mm_count` 使用计数器。如果该计数器最终为零，则调用 `free_mm()` 宏，通过 `kmem_cache_free()` 将 `mm_struct` 返回给 `mm_cachep` slab 缓存，因为该内存描述符没有任何用户。

### mm_struct 与内核线程

内核线程没有进程地址空间，因此也没有关联的内存描述符。因此，内核线程的进程描述符的 `mm` 字段为 `NULL`。这就是内核线程的定义——没有用户上下文的进程。

缺乏地址空间没有问题，因为内核线程从不访问任何用户空间内存。（它们会访问谁的内存？）由于内核线程在用户空间中没有页面，它们不值得拥有自己的内存描述符和页表。（页表将在本章后面讨论。）尽管如此，内核线程需要访问一些数据，例如页表，即使是访问内核内存也是如此。为了在不浪费内存于内存描述符和页表，也不浪费处理器周期在每次内核线程开始运行时切换到新地址空间的情况下，为内核线程提供所需的数据，内核线程使用之前运行过的任务的内存描述符。

每当进程被调度时，进程 `mm` 字段引用的进程地址空间会被加载。进程描述符中的 `active_mm` 字段随后被更新以引用新的地址空间。内核线程没有地址空间，`mm` 为 `NULL`。因此，当内核线程被调度时，内核注意到 `mm` 为 `NULL`，并保持之前进程的地址空间加载状态。然后内核更新内核线程进程描述符的 `active_mm` 字段，使其引用之前进程的内存描述符。内核线程随后可以按需使用之前进程的页表。由于内核线程不访问用户空间内存，它们只利用地址空间中与内核内存相关的信息，而这对于所有进程都是相同的。

## 虚拟内存区域

内存区域结构体 `vm_area_struct` 代表内存区域。它定义在 `<linux/mm_types.h>` 中。在 Linux 内核中，内存区域通常被称为虚拟内存区域（缩写为 VMA）。
