

该函数返回一个指针，指向至少 *size* 字节的虚拟连续内存。发生错误时，该函数返回 *NULL*。该函数可能会进入睡眠状态，因此不能从中断上下文或不允许阻塞的其他情况中调用。

若要释放通过 *vmalloc*() 获取的内存分配，请使用

```c
void vfree(const void *addr)
```

此函数释放从 *addr* 开始的内存块，该内存块之前是通过 *vmalloc*() 分配的。该函数也可能进入睡眠状态，因此不能在中断上下文中调用。它没有返回值。

使用这些函数很简单：

```c
char *buf;

buf = vmalloc(16 * PAGE_SIZE); /* 获取 16 页 */
if (!buf)
      /* 错误！内存分配失败 */

/*
 * buf 现在指向至少 16*PAGE_SIZE 字节
 * 的虚拟连续内存块
 */

      使用完内存后，请务必使用以下方法释放它：

vfree(buf);
```

## Slab 层

分配和释放数据结构是任何内核中最常见的操作之一。为了便于频繁地分配和释放数据，程序员通常会引入 *free lists*（空闲链表）。空闲链表包含一块可用的、已分配的数据结构。当代码需要新实例化的数据结构时，它可以从空闲链表中获取一个结构，而不是分配足够的内存并设置该数据结构。稍后，当不再需要该数据结构时，它会被返回到空闲链表，而不是被释放。从这个意义上说，空闲链表充当了一个对象缓存，缓存了一种经常使用的 *类型* 的对象。

内核中空闲链表的主要问题之一是缺乏全局控制。当可用内存不足时，内核无法通知每个空闲链表缩小其缓存大小以释放内存。内核完全不了解这些随机空闲链表。为了解决这个问题并整合代码，Linux 内核提供了 slab 层（也称为 slab 分配器）。slab 层充当通用的数据结构缓存层。

Slab 分配器的概念首次实现在 Sun Microsystem 的 SunOS 5.4 操作系统中。1 Linux 的数据结构缓存层共用相同的名称和基本设计。

Slab 层试图利用几个基本原则：

-   常用的数据结构往往会被频繁分配和释放，因此将它们缓存起来。
-   频繁的分配和释放可能导致内存碎片（无法找到足够大的连续可用内存块）。为防止这种情况，缓存的空闲链表是连续排列的。因为释放的数据结构会返回到空闲链表，所以不会产生碎片。
-   在频繁分配和释放时，空闲链表可以提供更好的性能，因为释放的对象可以立即返回给下一个分配请求。
-   如果分配器了解对象大小、页面大小和总缓存大小等概念，它可以做出更明智的决定。
-   如果缓存的一部分是按处理器分配的（对于系统中的每个处理器都是独立且唯一的），那么分配和释放操作可以在没有 SMP 锁的情况下进行。
-   如果分配器具有 NUMA 感知能力，它可以从与请求方相同的内存节点满足分配请求。
-   存储的对象可以进行对齐，以防止多个对象映射到同一缓存行。

Linux 中的 slab 层就是基于这些前提设计并实现的。

### Slab 层的设计

Slab 层将不同的对象分为称为缓存（caches）的组，每个组存储不同类型的对象。每种对象类型都有一个缓存。例如，一个缓存用于进程描述符（task_struct 结构的空闲链表），而另一个缓存用于 inode 对象（struct inode）。有趣的是，k malloc() 接口是构建在 slab 层之上的，使用了一组通用缓存。

然后，这些缓存被划分为 slabs（slabs，这也是该子系统的名称由来）。slab 由一个或多个物理连续的页面组成。通常，slab 仅由单个页面组成。每个缓存可能由多个 slab 组成。

每个 slab 包含一定数量的对象，这些对象就是被缓存的数据结构。每个 slab 处于三种状态之一：full（满）、partial（部分）或 empty（空）。Full slab 没有空闲对象。（slab 中的所有对象都已分配。）Empty slab 没有已分配的对象。（slab 中的所有对象都是空闲的。）Partial slab 有一些已分配的对象和一些空闲的对象。当内核的某部分请求新对象时，如果存在 partial slab，则请求从 partial slab 中满足。否则，请求从 empty slab 中满足。如果不存在 empty slab，则创建一个。显然，full slab 永远无法满足请求，因为它没有空闲对象。这种策略减少了碎片。

让我们以 inode 结构为例，它是磁盘 inode 的内存表示（参见第 13 章，“虚拟文件系统”）。这些结构被频繁创建和销毁，因此通过 slab 分配器管理它们是合理的。因此，struct inode 是从 inode_cache 缓存中分配的。（这种命名约定是标准的。）该缓存由一个或多个 slab 组成——由于对象众多，可能有大量 slab。每个 slab 包含尽可能多的 struct inode 对象。当内核请求新的 inode 结构时，内核从 partial slab 中返回一个已分配但未使用的结构的指针，或者如果没有 partial slab，则从 empty slab 中返回。当内核使用完 inode 对象后，slab 分配器将该对象标记为空闲。图 12.1 图示了缓存、slab 和对象之间的关系。

![](img/48bc90306f7476ca73ca7a99267ff690_273_0.png)

图 12.1  缓存、slab 和对象之间的关系。

每个缓存由一个 kmem_cache 结构表示。此结构包含三个列表——slabs_full、slabs_partial 和 slabs_empty——存储在 kmem_list3 结构内部，该结构在 mm/slab.c 中定义。这些列表包含与该缓存关联的所有 slab。Slab 描述符 struct slab 表示每个 slab：

```c
struct slab {
    struct list_head  list;   /* full, partial, 或 empty 列表 */
    unsigned long     colouroff; /* slab 颜色化的偏移量 */
    void              *s_mem;  /* slab 中的第一个对象 */
    unsigned int      inuse;   /* slab 中已分配的对象数 */
    kmem_bufctl_t     free;    /* 第一个空闲对象（如果有）*/
};
```

Slab 描述符是在 slab 外部的一般缓存中分配，还是在 slab 本身的开头部分内部分配。如果 slab 的总大小足够小，或者内部空闲空间足够容纳描述符，描述符就存储在 slab 内部。

Slab 分配器通过 __get_free_pages() 与底层内核页面分配器交互来创建新的 slab：

```c
static void *kmem_getpages(struct kmem_cache *cachep, gfp_t flags, int nodeid)
{
    struct page *page;
    void *addr;
    int i;

    flags |= cachep->gfpflags;
    if (likely(nodeid == -1)) {
        addr = (void *)__get_free_pages(flags, cachep->gfporder);
        if (!addr)
            return NULL;
        page = virt_to_page(addr);
    } else {
        page = alloc_pages_node(nodeid, flags, cachep->gfporder);
        if (!page)
            return NULL;
        addr = page_address(page);
    }

    i = (1 << cachep->gfporder);
    if (cachep->flags & SLAB_RECLAM_ACCOUNT)
        atomic_add(i, &slab_reclaim_pages);
    add_page_state(nr_slab, i);
    while (i--) {
        SetPageSlab(page);
        page++;
    }
    return addr;
}
```

此函数使用 __get_free_pages() 分配足以容纳缓存的内存。该函数的第一个参数指向需要更多页面的特定缓存。第二个参数指向传递给 __get_free_pages() 的标志。（注意该值是如何与其他值进行二进制按位或运算的。这会将缓存所需的默认标志添加到 flags 参数中。分配的大小（2 的幂）存储在 cachep->gfporder 中。前面的函数比预期的稍显复杂，因为代码使分配器具有 NUMA 感知能力。当 nodeid 不为负一时，分配器尝试从与请求方相同的内存节点满足分配请求

