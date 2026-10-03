
# Linux 内存管理器（早期访问）© 2025 由 Lorenzo Stoakes

```c
/**
 * struct xarray - XArray 的锚点。
 * @xa_lock: 保护 XArray 内容的锁。
 * 使用 xarray 时，请静态定义它或将其嵌入你的数据结构中。
 * 它是一个非常小的数据结构，因此通常没有必要单独
 * 分配它并在数据结构中保留指向它的指针。
 * 同样可以使用 xarray_lock 来保护你自己的数据结构。
 * 如果数组中的所有条目均为 NULL，则 @xa_head 为 NULL 指针。
 * 如果数组唯一的非 NULL 条目位于索引 0，则 @xa_head 指向该
 * 条目。如果数组中的任何其他条目非 NULL，则 @xa_head 指向
 * 一个 @xa_node。
 */
struct xarray {
    spinlock_t xa_lock;
    /* 私有：数据结构的其他部分不应直接使用。 */
    gfp_t      xa_flags;
    void      *rcu;
    void      *xa_head;
};
```

Listing 9-1: linux/xarray.h: struct xarray

它包含一个自旋锁 (`xa_lock`)，用于无法仅通过 RCU 完成的操作；一个可以指定 xarray 标志的标志位 (`xa_flags`) 以及 xarray 树的头部 `xa_head`。后两个字段是私有的，不打算在 xarray 代码之外使用。

我们可以通过检查列表 9-2 中的 `XARRAY_INIT()` 来看到新分配的 xarray 对象的结构。

```c
#define XARRAY_INIT(name, flags) {
    .xa_lock = SPIN_LOCK_UNLOCKED(name.xa_lock),
    .xa_flags = flags,
    .xa_head = NULL
};
```

Listing 9-2: linux/xarray.h: XARRAY_INIT()

如列表 9-1 中的注释所示，`NULL` 条目表示数组完全为空，如果数组仅包含索引 0 处的一个条目，它将包含在 `xa_head` 中。

xarray 中的元素可以是什么值？这在列表 9-3 中有描述。

```c
/*
 * 条目的低两个位决定了 XArray 如何解释
 * 内容：
 *
 * 00: 指针条目
 * 10: 内部条目
 * x1: 值条目或标记指针
 *
 * 尝试在 XArray 中存储内部条目是一个错误。
 *
 * 大多数内部条目是指向树中下一个节点的指针。
 * 以下内部条目具有特殊含义：
 *
 * 0-62: 兄弟条目
 * 256: 重试条目
 * 257: 零条目
 *
 * 错误也作为内部条目表示，但使用负空间
 * (-4094 到 -2)。它们永远不会存储在槽数组中；仅
 * 由正常 API 返回。
 */
```

```c
#define BITS_PER_XA_VALUE (BITS_PER_LONG - 1)
```

Listing 9-3: include/linux/xarray.h: BITS_PER_XA_VALUE()

这解释了为什么被 xarray 引用的指针必须是 4 字节对齐的——为了在指针类型的低两个位中容纳这些标识符。

这解释了为什么存储在 xarray 内部的内部值必须是 `LONG_MAX` 或更小的正值——我们牺牲了一位给这个值，使其成为这种值。

xarray API 的用户不应遇到内部条目，除非发生错误，只需关心条目是否为值，或者通过列表 9-4 所示的 `xa_is_value()` 来判断。

```c
/**
 * xa_is_value() - 判断条目是否为值。
 * @entry: XArray 条目。
 *
 * 上文：任何上下文。
 * 返回：如果条目是一个值，返回 true；如果是指针，返回 false。
 */
static inline bool xa_is_value(const void *entry)
{
    return (unsigned long)entry & 1;
}
```

Listing 9-4: include/linux/xarray.h: xa_is_value()

我们可以通过列表 9-5 所示的 `xa_to_value()` 提取值。

```c
/**
 * xa_to_value() - 获取存储在 XArray 条目中的值。
 * @entry: XArray 条目。
 *
 * 上文：任何上下文。
 * 返回：存储在 XArray 条目中的值。
 */
static inline unsigned long xa_to_value(const void *entry)
{
    return (unsigned long)entry >> 1;
}
```

Listing 9-5: include/linux/xarray.h: xa_to_value()

并通过列表 9-6 所示的 `xa_mk_value()` 首先生成它。

```c
/**
 * xa_mk_value() - 从整数创建 XArray 条目。
 * @v: 要存储在 XArray 中的值。
 *
 * 上文：任何上下文。
 * 返回：适合存储在 XArray 中的条目。
 */
static inline void *xa_mk_value(unsigned long v)
{
    WARN_ON((long)v < 0);
    return (void *)(v << 1);
}
```

Listing 9-6: include/linux/xarray.h: xa_mk_value()

/* 私有 */

```c
static inline struct xa_node *xa_to_node(const void *entry)
{
    return (struct xa_node *)((unsigned long)entry - 2);
}
```

Listing 9-13: include/linux/xarray.h: xa_to_node() 以及通过 `xa_mk_node()` 构建，如列表 9-14 所示。

/* 私有 */

```c
static inline void *xa_mk_node(const struct xa_node *node)
{
    return (void *)((unsigned long)node | 2);
}
```

Listing 9-14: include/linux/xarray.h: xa_mk_node()

当内部条目不引用节点或错误时，它将利用虚拟地址空间范围的低位，用作以下特殊用例之一（如列表 9-3 中的注释所示）：

- **兄弟条目 0 - 62** - 用于高级 xarray API。这表示多个索引共享 xarray 中的同一个条目，其值表示该条目相对于所跨越条目的偏移量。
- **重试条目 256 – X_RETRY_ENTRY** - 用于高级 xarray API。表示另一个线程持有 `xa_lock` 并在中间更新条目。为了避免在更新条目时发生可能丢失的引用，请重新操作。
- **零条目 257 – X_ZERO_ENTRY** - 表示该条目非空，但代表 `NULL` 值。在普通 API 中（参见下文第 9.2.1 节对 xarray API 的讨论），这些简单地表示为 `NULL` 值，但高级 API 可能会遇到这些值。

也就是说，一个节点提供了 xarray 的内部结构——它本质上是一个基数树，经过优化可以处理任意地址范围，这改进了之前的内核基数树实现。

我们在列表 9-15 中检查了 `struct xa_node` 数据结构。

```c
/*
 * @count 是 ->slots 数组中每个非 NULL 元素的计数
 * 无论它是值条目、重试条目、用户指针、
 * 兄弟条目还是指向树的下一的指针。
 * @nr_values 是 ->slots 中每个元素的计数，
 * 该元素要么是值条目或者是值条目的兄弟。
 */
struct xa_node {
    unsigned char shift;      /* 每个槽位的剩余位数 */
    unsigned char offset;     /* 父节点中的槽位偏移 */
    unsigned char count;      /* 条目总计数 */
    unsigned char nr_values;  /* 值条目计数 */
    struct xa_node __rcu *parent; /* 树顶为 NULL */
};
```

Listing 9-15: include/linux/xarray.h: struct xa_node
