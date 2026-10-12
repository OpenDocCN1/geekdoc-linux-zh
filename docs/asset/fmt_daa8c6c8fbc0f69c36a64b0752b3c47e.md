
`pageset` 是一个数组，包含许多条目，其最大可能的 CPU 数量为：

```c
... that holds many entries as the maximum possible number of CPUs.
```

`NR_CPUS` 在单核系统上的值为 1，但在 SMP 系统上可能在 2 到 32 之间。

`pageset` 是一个类型为 `per_pageset` 的数组，其定义如下：

```c
struct per_pageset {
    struct cpu_pages pcp[2]; /* 0: hot, 1: cold */
    cacheline_aligned;
};
```

该结构包含两个条目，第一个用于管理热页，第二个用于管理冷页。

```c
struct cpu_pages {
    int count; /* number of pages in the list */
    int high; /* high watermark, emptying */
    int batch; /* chunk size */
    struct list_head list; /* list of pages */
};
```

`count` 记录了列表中的页面数量，`high` 是水位线。当 `count` 的值超过 `high` 时，这表示页面过多。当没有元素时，列表会被重新填充。

`pages` 是一个双向链表，持有每 CPU 的页面，并使用标准方法处理。

如果可能，每 CPU 缓存不会用单个页面进行填充。`batch` 是单次通过中添加页面数量的指南。

图 3-6：双处理器系统上的每 CPU 缓存。

水位线的计算以及缓存数据结构将在第 3.4.2 节中详细讨论。

# 第 3 章：内存管理

分配器（一种将完整页面划分为较小部分的方法，见第 3.6.1 节），可以保证它仅供内核使用，而不是从其他地方；因此映射信息是多余的。相反，内核可以重新解释该字段以找到有多少小对象正在使用。这种双重解释在数据结构定义如下：

```c
<mm_types>
struct page {
    union {
        atomic_t _mapcount; /* mm 中映射的 pte 计数，
           * 用于显示 pte 是否映射
           * 并限制反向查找。
           */
        unsigned int inuse; /* SLUB: 对象数量 */
    };
```

注意 `atomic_t` 和 `unsigned int` 是不同的数据类型——前者允许原子性地更改值，对并发访问是安全的，而后者是经典的整数。`atomic_t` 提供 32 位，在 Linux 支持的每种架构上，整数都提供相同位数。现在，你可能想将定义“简化”如下：

```c
struct page {
    ...
    atomic_t counter;
};
```

但这种风格很糟糕，内核开发人员完全无法接受。存根代码访问其对象计数器时不需要原子性，这应该反映在数据类型中。最重要的是，代码在子系统中的可读性会受到影响。虽然 `_mapcount` 和 `inuse` 清晰简洁地描述了元素的含义，但 `counter` 几乎可以代表任何内容。

## page 的定义

该结构定义为：

```c
<mm.h>
struct page {
    unsigned long flags;      /* 原子标志位
```

> 在内核 2.6.3 之前，情况并非如此。Spar 架构只能为原子操作提供 24 位，因此所有架构都必须遵守这一限制。幸运的是，这个问题现在已经通过 Spar 特定代码的改进得到了解决。

```c
    unsigned int inuse; /* SLUB: 对象数量 */
);
struct {
    unsigned long private; /* 映射私有不透明数据：
    * 通常用于 buffer_heads
    * 如果设置了 PagePrivate；用于
    * 如果设置了 PageSwapCache；用于 swp_entry_t；
    * 如果设置了 PG_buddy；指示 buddy 系统中的顺序。 */
    struct address_space *mapping; /* 如果低位为0，则指向
    * inode address_space 或 NULL。
    * 如果页面被映射为匿名内存，
    * 低位被设置，
    * 指向 anon_vma 对象：
    * 见下文 PAGE_MAPPING_ANON。 */
};
struct kmem_cache *slab; /* SLUB: 指向 slab 的指针 */
struct page *first_page; /* 复合尾页 */
union {
    pgoff_t index; /* 映射内的偏移。
    freelist; /* SLUB: 空闲列表需要 slab 锁 */
};
struct list_head lru; /* 页面交换列表，例如 active_list
    * 受 zone->lru_lock 保护！ */
};
```

```c
#if defined(WANT_PAGE_VIRT)
    void *virtual; /* 内核虚拟地址（如果未 kmapped，即未 hemapped） */
#endif
```

`slab`、`freelist` 和 `inuse` 被 slab 分配器使用。我们不需要担心这些特殊安排，如果编译内核时启用了 slab 分配器支持，它们就不会被使用，因此为了简化，我省略了后续讨论。

每个页帧由此结构以体系无关的格式描述，不依赖于所使用的 CPU。slab 元素，页面结构包含了许多其他元素，这些元素只能在其他地方内核子系统的范围内准确解释。尽管如此，我将提供该结构内容的概述，尽管这意味着引用后面的章节。

- `flags` 存储描述页面属性的体系无关标志。我将在下文中讨论不同的标志选项。
- `count` 是一个计数器，表示内核对该页面的引用次数。当其值达到 0 时，内核知道该页面当前未使用，可以移除。如果其值大于 0，则该实例不应从内存中移除。如果你不熟悉计数器，应该咨询附录 C 获取更多信息。
- `_mapcount` 表示页表中有多少项指向该页面。
- `lru` 是一个列表头，用于将页面保持在各种列表中，允许将页面分为不同的类别，最重要的是活动和非活动页面。第 18 章的讨论将回到这些列表。

内核允许将相邻页面组合成更大的复合页面。集群中的第一个页面是 `head` 页，而所有其他页面都是 `tail` 页。所有尾页的 `first_page` 都指向头页。

- `mapping` 规定了页帧所在的地址空间。`index` 是内存内的偏移。地址空间是一个非常通用的概念，例如在将文件读入内存时。地址空间用于将文件内容（数据）与读取内容的内存区域相关联。通过一种小技巧，`mapping` 不仅可以持有一个指针，还可以存储关于页面是否属于与地址空间关联的匿名区域的信息。如果 `mapping` 中的位值为 1，则指针指向的不是 `address_space` 实例，而是另一个数据。

```c
如果 mapping 中的位值为 1，则指针指向的不是 address_space 实例，而是另一个数据。
```
