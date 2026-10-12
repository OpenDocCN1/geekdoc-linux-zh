
# `malloc()`

`malloc()` 函数的工作方式与 `kmalloc()` 类似，但它分配的内存在虚拟上是连续的，而不物理上一定连续。`malloc()` 返回的页面在用户空间分配函数处理器的虚拟地址空间内是连续的，但无法保证它们在物理 RAM 中实际上是连续的。`kmalloc` 函数保证页面在物理上是连续的（且虚拟上也是连续的）。`malloc()` 函数仅确保页面在虚拟地址空间内是连续。它通过分配非连续的物理内存块并“修复”页表，将内存映射到本地地址空间的一个连续块中来实现这一点。

在大多数情况下，硬件要求物理连续的分配。在许多架构上，硬件设备位于内存管理单元（`MMU`）的另一侧，因此无法理解虚拟地址。结果就是硬件设备以物理连续块的形式工作的内存区域。仅供软件使用的内存块——例如处理过的缓冲区——使用虚拟连续内存是没问题的。在你的编程中，你永远感知不到这种区别。对内核而言，所有内存在逻辑上都是连续的。

尽管在某些情况下需要物理连续内存，但大多数内核代码使用 `kmalloc()` 而不是 `malloc()` 来获取内存。这是出于性能考虑。`malloc()` 函数为了映射虚拟地址空间中的非连续页面，必须专门设置页表项。糟糕的是，通过 `malloc()` 获取的页面必须由其各个页面单独管理（因为它们是不连续的），这会导致比直接使用映射内存时得多的 `TLB` 抖动（thrashing）。由于这些考虑，只有在绝对必要时才使用 `malloc()`——通常是为了获取非常大的内存区域。例如，当模块动态插入内核中时，它们被加载到通过 `malloc()` 创建的内存中。

`malloc()` 定义在 `<linux/malloc.h>` 中，实现在 `mm/malloc.c` 中。其用法与用户空间的 `malloc()` 典型：

```c
void * malloc(unsigned long size)
```

该函数返回一个指向至少 `size` 字节虚拟连续内存的指针。如果出错，函数返回 `NULL`。该函数可能会睡眠，因此不能在中断上下文或其他不允许阻塞的情况下调用。

要释放通过 `malloc()` 获取的分配内存，请使用

```c
void vfree(void *addr)
```

`TLB`（转换对备缓冲区）是大多数架构使用的一种硬件缓存，用于缓存虚拟地址到物理地址的映射。这极大地提高了系统性能，因为大多数内存访问都是通过虚拟地址完成的。

# 第 11 章 内存管理

该函数释放从 `addr` 开始的之前通过 `vmalloc()` 分配的内存块。该函数也可以睡眠，因此不能在中断上下调用。它没有返回值。

这些函数的用法非常简单：

```c
char *buf;

buf = vmalloc(16 * PAGE_SIZE); /* 获取 16 个页 */

if (!buf) {
    /* 错误！未能分配内存 */
}
```

```c
/*
 * buf 现在指向至少 16*PAGE_SIZE 字节
 * 的虚拟连续内存块
 */
```

当你完成对该内存的使用后，确保使用 `vfree(buf);` 释放它。

# Slab 层 (Slab Layer)

分配和释放数据结构是任何内核内部最常见的操作之一。为了方便频繁分配和释放数据，程序员通常会引入空闲列表（free lists）。即一组可用的、已经分配的数据结构。当代码需要某个数据结构的新实例时，它可以从空闲列表中获取一个结构，而不是重新分配足够的内存并进行初始化。

# Slab 层频繁使用的数据

Slab 层试图尝试利用以下几个基本原则：

- 频繁使用的数据结构往往会被分配和释放，因此将其缓存。
- 频繁的分配和释放可能导致碎片（无法找到连续的大内存块）。为了防止这一点，使用空闲列表
- 空闲列表在频繁分配时提高了性能，因为空对象可以立即返回。
- 如果分配器感知缓存大小、页面大小和总缓存大小等概念，它可以做出更智能的决策。
- 如果缓存的一部分是每个处理器的（每个处理器独有的），则分配和释放不需要 SMP 锁。
- 分配器是 NUMA 感知的，它可以从请求的相同节点完成分配。
- 存储的对象可以进行着色（coloring），以防止多个对象映射到相同的缓存行。

Linux 中的 Slab 层是根据这些原则设计并实现的。

# Slab 层的设计

Slab 层将对象分为称为缓存（caches）的组，每个缓存存储不同类型的对象。每种类型有一个缓存。例如，一个缓存用于进程描述符（`task_struct` 结构的空闲列表），而另一个缓存用于 `inode` 对象（`struct inode`）。`kmalloc()` 接口构建在 Slab 层之上，使用了一系列特定目的缓存。

缓存随后被分为 `slab`（这也是该子系统的命名来源）。`Slab` 由一个或多个物理连续的页面组成。通常，`Slab` 由单个页面组成。每个 `Slab` 包含若干个正在被创建的对象。每个 `Slab` 处于三种状态之一：满（full）、部分（partial）或空（empty）。满 `Slab` 没有空闲对象（`Slab` 中的所有对象已分配）。部分 `Slab` 有一些已分配对象和空闲对象。当内核请求新对象时，将从部分 `Slab` 满足（如果存在），否则从空 `Slab` 满足。如果没有空 `Slab`，则创建一个新的 `Slab`。

让我们以 `inode` 结构为例，它是 `inode` 在内存中的表示（见第 12 章）。这些结构频繁地创建和销毁，因此通过 Slab 分配器管理它们是合理的。因此，`struct inode` 是从 `inode_cachemem` 分配（这种命名约定是标准做法）。该缓存由一个或多个 `slab` 组成，因为有很多对象。每个 `slab` 尽可能包含尽可能 `struct inode` 对象。当内核请求一个新的 `inode` 结构时，内核会从部分 `slab`（partial slab）中返回一个已分配且未使用的结构指针；如果没有部分 `slab`，则返回一个空 `slab`。当内核完成对 `inode` 对象的使用后，`slab` 分器会将该对象标记为空闲。

11.1 图展示了缓存（caches）、`slabs` 和对象（objects）之间的关系。

![](img/b4e9c660c15aebea5f8b13c670002b29_221_0.png)

图 11.1 缓存、slabs 和对象之间的关系。

每个缓存由一个 `kmem_cache_s` 结构表示。该结构包含三个列表——`slabs_full`、`slabs_partial` 和 `slabs_empty`——存储在 `kmem_list3` 结构内部。这些列表包含了所有与缓存相关的 `slab`。`slab` 描述符结构表示每个 `slab`：

```c
struct slab {
    struct list_head list;          /* 满、部分或空列表列表 */
    unsigned long colorinfo;        /* slab 颜色的偏移量 */
    void *s_mem;                   /* slab 中的第一个对象 */
    unsigned int inuse;            /* slab 中已分配的对象 */
    kmem_bufftl_t free;             /* 第一个空闲对象，如果有的话 */
};
```

slab 描述符要么在 slab 外部的通用缓存中分配，要么在 slab 内部的起始处分配。如果 slab 的足够足够小，或者内部缓存空间足够容纳该描述符，则将描述符存储在 slab 内部。

slab 分配器通过 `__get_free_pages__()` 与底层内核页分配器接口创建新的 `slab`：

```c
static void *kmem_getpages(kmem_cache_t *cachep, int flags, int nodeid) {
    struct page *page;
    void *addr;
    int i;

    flags |= cachep->gfpflags;

    if (likely(nodeid == -1)) {
        addr = (void*)__get_free_pages(flags, cachep->gfporder);
        if (!addr) {
            return NULL;
        }
        page = virt_to_page(addr);
    } else {
        page = alloc_pages_node(nodeid, flags, cachep->gfporder);
        if (!page) {
            return NULL;
        }
        addr = page_address(page);
    }

    for (i = 1 << cachep->gfporder; ;
        if (cachep->flags & SLAB_RECLAIM_ACCOUNT) {
```
