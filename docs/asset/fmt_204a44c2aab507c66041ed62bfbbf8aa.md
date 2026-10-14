
# `skb_queue_tail`

### 名称

`skb_queue_tail` — 在列表尾部队列缓冲区

### 概要

```
void skb_queue_tail (struct sk_buff_head * list, struct sk_buff * newsk);
```

### 参数

- `list`: 要使用的列表
- `newsk`: 要队列的缓冲区

### 描述

在列表尾部队列缓冲区。此函数会获取列表锁，可以安全地与其他加锁的 `&sk_buff` 函数一起使用。

一个缓冲区不能同时放在两个列表中。

## `__skb_dequeue`

### 名称

`__skb_dequeue` — 从队列头部移除

### 概要

```
struct sk_buff * __skb_dequeue (struct sk_buff_head * list);
```

### 参数

- `list`: 要出队列的列表

### 描述

移除列表头部。此函数不获取锁，因此必须在持有相应锁的情况下使用。对于空列表返回 `NULL`。

## `skb_dequeue`

### 名称

`skb_dequeue` — 从队列头部移除

### 概要

```
struct sk_buff * skb_dequeue (struct sk_buff_head * list);
```

### 参数

- `list`: 要出队列的列表

### 描述

移除列表头部。此函数会获取锁，因此可以安全地与其他加锁的列表函数使用。对于空列表返回 `NULL`。

## `skb_insert`

### 名称

`skb_insert` — 插入缓冲区

### 概要

```
void skb_insert (struct sk_buff_head * list, struct sk_buff * old, struct sk_buff * newsk);
```

### 参数

- `list`: 要使用的列表
- `old`: 要插入的缓冲区
- `newsk`: 要队列的缓冲区

### 描述

在列表开始处队列缓冲区。此函数不获取锁……等等。

## `skb_append`

### 名称

`skb_append` — 追加缓冲区

### 概要

```
void skb_append (struct sk_buff_head * list, struct sk_buff * old, struct sk_buff * newsk);
```

### 参数

- `list`: 要使用的列表
- `old`: 要插入的缓冲区
- `newsk`: 要队列的缓冲区

### 描述

在列表末尾队列缓冲区。此函数会获取列表锁，可以安全地与其他加锁的 `&sk_buff` 函数一起使用。

## `skb_unlink`

### 名称

`skb_unlink` — 从列表中移除缓冲区

### 概要

```
void skb_unlink (struct sk_buff * skb);
```

### 参数

- `skb`: 要移除的缓冲区

### 描述

在列表开始处队列缓冲区。等等……即使不知道它在哪个列表中也能工作，这在某些时候非常方便。这也意味着当你移除它时，*列表必须存在*。因此，在销毁列表之前，必须移除其内容。

要添加的数据量

## 描述

此函数扩展缓冲区起始处的已用数据区域。如果这超过了缓冲区的总头部空间（headroom），内核将触发崩溃（`panic`）。返回指向额外数据第一个字节的指针。

## `skb_pull`

### 名称

`skb_pull` — 从缓冲区头部移除数据

### 概要

```
unsigned char * skb_pull (struct sk_buff *skb, unsigned int len);
```

### 参数

- `skb`: 要使用的缓冲区
- `len`: 要移除的数据量

### 描述

此函数从缓冲区头部移除数据，并将内存归还给头部空间（headroom）。返回缓冲区中下一个数据的指针。一旦数据被拉取，未来的推送（push）将覆盖旧数据。

## `skb_headroom`

### 名称

`skb_headroom` — 缓冲区头部的字节数

### 概要

```
int skb_headroom (const struct sk_buff *skb);
```

### 参数

- `skb`: 要检查的缓冲区

### 描述

返回 `&skb_buff` 头部可用空间的字节数。

## `skb_tailroom`

### 名称

`skb_tailroom` — 缓冲区尾部的字节数

### 概要

```
int skb_tailroom (const struct sk_buff *skb);
```

### 参数

- `skb`: 要检查的缓冲区

### 描述

返回 `skb_buff` 尾部可用空间的字节数

## `skb_reserve`

### 名称

`skb_reserve` — 调整头部空间

### 概要

```
void skb_reserve (struct sk_buff *skb, unsigned int len);
```

### 参数

- `skb`: 要修改的缓冲区
- `len`: 要移动的字节数

### 描述

通过减少尾部空间（tail room）来增加空 `&sk_buff` 的头部空间。这只允许空缓冲区。

## `skb_trim`

### 名称

`skb_trim` — 移除缓冲区的末部

### 概要

```
void skb_trim (struct sk_buff *skb, unsigned int len);
```

### 参数

- `skb`: 要修改的缓冲区
- `len`: 新长度

### 描述

通过移除尾部数据来裁剪缓冲区长度。如果缓冲区长度已经小于指定的长度，则不进行修改。

## `skb_orphan`

### 名称

`skb_orphan` — 孤立缓冲区

### 概要

```
void skb_orphan (struct sk_buff *skb);
```

### 参数

- `skb`: 要孤立的缓冲区

### 描述

如果缓冲区当前有所有者，则我们调用所有者的析构函数并使 `skb` 变为无所有。缓冲区继续存在，但不再由其原所有所有。

## `skb_queue_purge`

### 名称

`skb_queue_purge` — 清空列表

### 概要

```
void skb_queue_purge (struct sk_buff_head * list);
```

### 参数

- `list`: 要清空的列表

### 描述

删除 `&sk_buff` 列表上的所有缓冲区。每个缓冲区都从列表中移除并释放一个引用。此函数会获取列表锁，并且对于其他列表锁函数来说是原子的。

## `__skb_queue_purge`

### 名称

`__skb_queue_purge` — 清空列表

### 概要

```
void __skb_queue_purge (struct sk_buff_head * list);
```

### 参数

- `list`: 要清空的列表

### 描述

删除 `&sk_buff` 列表上的所有缓冲区。每个缓冲区都从列表中移除并释放一个引用。此函数不获取列表锁，调用者必须持有相关锁才能使用它。

## `__dev_alloc_skb`

### 名称

`__dev_alloc_skb` — 为发送分配一个 skbuff

### 概要

```
struct sk_buff * __dev_alloc_skb (unsigned int length, int gfp_mask);
```

### 参数

- `length`: 要分配的长度
- `gfp_mask`: 获取空页掩码，传递给 `alloc_skb`（等待，传递给内部分配器）

### 描述

分配一个新的 `&sk_buff` 并将其使用计数设置为 1。该缓冲区内置了未指定的头部空间。用户应该分配他们认为需要的头部空间，而无需考虑已内置的空间。内置空间用于优化。

如果没有可用内存，则返回 `NULL`。

## `dev_alloc_skb`

### 名称

`dev_alloc_skb` — 为发送分配一个 skbuff

### 概要

```
struct sk_buff * dev_alloc_skb (unsigned int length);
```

### 参数

- `length`: 要分配的长度

### 描述

分配一个新的 `&sk_buff` 并将其使用计数设置为 1。该缓冲区内置了未指定的头部空间。用户应该分配他们认为需要的头部空间，而无需考虑已内置的空间。内置空间用于优化。

如果没有可用内存，则返回 `NULL`。虽然此函数分配内存，但它可以在中断中调用。

## `skb_cow`

### 名称

`skb_cow` — 需要时拷贝 skb 的头部

### 概要

