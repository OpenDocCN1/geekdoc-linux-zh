
| `BH_Delay` | 缓冲区尚未关联磁盘上的块（延迟分配）。 |
| `BH_Boundary` | 缓冲区形成连续块的边界——下一个块是不连续的。 |
| `BH_Write_EIO` | 缓冲区在写入时发生了 I/O 错误。 |
| `BH_Ordered` | 有序写入。 |
| `BH_Eopnotsupp` | 缓冲区发生了“不支持”错误。 |
| `BH_Unwritten` | 已在磁盘上为缓冲区分配了空间，但实际数据尚未写出。 |
| `BH_Quiet` | 抑制此缓冲区的错误。 |

`bh_state_bits` 枚举还包含列表中的最后一个值 `BH_PrivateStart` 标志。这不是一个有效的状态标志，而是对应于其他代码可以使用的第一位可用位。所有等于或大于 `BH_PrivateStart` 的位值都不由块 I/O 层本身使用，因此这些位对于想要在 `b_state` 字段中存储信息的单个驱动程序来说是安全的。驱动程序可以基于此标志来确定其内部标志的位值，并放心它们没有侵犯块 I/O 层使用的官方位。

`b_count` 字段是缓冲区的使用计数。该值由两个内联函数增加和减少，这两个函数都定义在 `<linux/buffer_head.h>` 中：

```c
static inline void get_bh(struct buffer_head *bh) {
	atomic_inc(&bh->b_count);
}

static inline void put_bh(struct buffer_head *bh) {
	atomic_dec(&bh->b_count);
}
```

在操纵缓冲区头之前，你必须通过 `get_bh()` 增加其引用计数，以确保缓冲区头不会被从你手中释放。当完成对缓冲区头的操作后，通过 `put_bh()` 减少引用计数。

给定缓冲区对应的磁盘上的物理块是 `b_blocknr`——`b_bdev` 描述的块设备上的逻辑块。

给定缓冲区对应的内存中的物理页面是 `b_page` 指向的页面。更具体地说，`b_data` 是指向块（存在于 `b_page` 某处）的指针，其长度为 `b_size` 字节。因此，块在内存中从地址 `b_data` 开始，到地址 `(b_data + b_size)` 结束。

缓冲区头的目的是描述磁盘上的块与内存中的物理缓冲区（特定页面上的字节序列）之间的这种映射。作为这种缓冲区到块映射的描述符是该数据结构在内核中的唯一角色。

在 2.6 内核之前，缓冲区头是一个更为重要的数据结构：它是内核中的 I/O 单位。缓冲区头不仅描述了磁盘块到物理页的映射，还充当所有块 I/O 的容器。这有两个主要问题。首先，缓冲区头是一个庞大且笨重的数据结构（现在已稍微缩小），以缓冲区头为单位操纵数据既不清爽也不简单。相反，内核更喜欢以页面为单位工作，页面简单并能提供更好的性能。描述每个单独缓冲区（可能比页面小）的大缓冲区头效率低下。因此，在 2.6 内核中，大量的工作致力于使内核直接以页面和地址空间为单位工作，而不是以缓冲区为单位。其中一些工作在第 16 章“页面缓存和页面写回”中讨论，那里讨论了 `address_space` 结构和 `pdflush` 守护进程。

缓冲区头的第二个问题是它们只描述单个缓冲区。当用作所有 I/O 操作的容器时，缓冲区头迫使内核将潜在的大型块 I/O 操作（例如写操作）拆分为多个 `buffer_head` 结构。

这会导致不必要的开销和空间消耗。因此，2.5 开发内核的主要目标之一是引入一种新的、灵活的、轻量的容器来处理块 I/O 操作。其结果就是 `bio` 结构，将在下一节中讨论。

## bio 结构

内核中块 I/O 的基本容器是 `bio` 结构，它定义在 `<linux/bio.h>` 中。该结构以`段`的列表形式表示正在飞行（`active`）中的块 I/O 操作。一个段是内存中连续的缓冲区块。因此，单个缓冲区在内存中无需连续。通过允许缓冲区以块的形式描述，`bio` 结构使得内核能够从内存中的多个位置对单个缓冲区执行块 I/O 操作。这种向量 I/O 被称为`分散-聚集`（`scatter-gather`）I/O。

以下是定义在 `<linux/bio.h>` 中的 `struct bio`，每个字段都添加了注释：

```c
struct bio {
      sector_t                bi_sector;      /* associated sector on disk */
      struct bio *            bi_next;         /* list of requests */
      struct block_device *   bi_bdev;         /* associated block device */
      unsigned long           bi_flags;        /* status and command flags */
      unsigned long           bi_rw;           /* read or write? */
      unsigned short          bi_vcnt;         /* number of bio_vecs off */
      unsigned short          bi_idx;          /* current index in bi_io_vec */
      unsigned short          bi_phys_segments;/* number of segments */
      unsigned int            bi_size;         /* I/O count */
      unsigned int            bi_seg_front_size;/* size of first segment */
      unsigned int            bi_seg_back_size; /* size of last segment */
      unsigned int            bi_max_vecs;     /* maximum bio_vecs possible */
      unsigned int            bi_comp_cpu;     /* completion CPU */
      atomic_t                bi_cnt;          /* usage counter */
      struct bio_vec *        bi_io_vec;       /* bio vec list */
      bio_end_io_t            bi_end_io;       /* I/O completion method */
      void *                  bi_private;      /* owner-private method */
      bio_dtor_t *            bi_dtor;         /* destructor method */
      struct bio_vec          bi_inline_vecs[0]; /* inline bio vectors */
};
```

`bio` 结构的主要目的是表示正在飞行中的块 I/O 操作。为此，该结构中的大部分字段都是与内部簿记相关的。最重要的字段是 `bi_io_vec`、`bi_vcnt` 和 `bi_idx`。图 14.2 展示了 `bio` 结构及其相关组件之间的关系。

![](img/48bc90306f7476ca73ca7a99267ff690_321_0.png)

### I/O 向量

`bi_io_vec` 字段指向一个 `bio_vec` 结构数组。这些结构用作特定块 I/O 操作中的单个段列表。每个 `bio_vec` 都被视为形式为 `<page, offset, len>` 的向量，它描述了一个特定的段：其所在的物理页、块在页中的位置（作为偏移量）以及从给定偏移量开始的块长度。这些向量的完整数组描述了整个缓冲区。`bio_vec` 结构定义在 `<linux/bio.h>` 中：

```c
struct bio_vec {
    /* pointer to the physical page on which this buffer resides */
    struct page *bv_page;
    /* the length in bytes of this buffer */
    unsigned int bv_len;
    /* the byte offset within the page where the buffer resides */
    unsigned int bv_offset;
};
```
