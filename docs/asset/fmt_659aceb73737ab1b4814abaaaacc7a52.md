
```
if (list3->free_objects > list3->free_limit) {

    list3->free_objects -= cache->num;

    slab_destroy(cache, slab);

} else {

    list_add(&slab->list, &list3->slabs_free);

}
} else {

    list_add(&slab->list, &list3->slabs_partial);

}

list_add(&slab->list, &list3->slabs_partial);
```

如果删除后缓存中的所有对象都未使用（`slab->inuse == 0`），则该 slab 通常放置在 `slabs_free` 列表中。

异常情况：缓存中的空闲对象数量超过了预定义的限制 `free_limit`。在这种情况下，使用 `slab_destroy` 将整个 slab 返回给伙伴系统。

如果 slab 同时包含已使用和未使用的对象，则它会被插入缓存的 `slabs_partial` 列表中。

## 销毁缓存

必须调用 `kmem_cache_destroy` 函数来销毁一个仅包含使用对象的完整缓存。该函数主要用于移除那些想要返回其所分配的所有内存空间的模块¹。

由于实现本身没有揭示任何新内容，我们将仅概述移除缓存所需的主要步骤：

- 逐个扫描 `slabs_free` 列表上的 slabs。首先对 slab 上的每个对象调用析构函数，并将内存空间返回给伙伴系统。
- 释放每个 CPU 缓存的内存空间。
- 从 `cache_cache` 列表中移除数据。

## 3.6.5 通用缓存

必须使用 `kmalloc` 和 `kfree` 函数在经典意义上分配和释放内存，而不是对象。这些是内核中用户空间 C 标准库中 `malloc` 和 `free` 函数的等效实现。

我已经多次提到，`kmalloc` 和 `kfree` 被实现为 slab 分配器的前端，并尽可能地模拟了 `malloc/free` 的语义。我们可以顺序处理它们的实现。

### kmalloc 的实现

`kmalloc` 的基础是一个数组，它将针对不同尺寸内存区域的 slab 缓存分组。数组条目是 `cache_sizes` 数据结构的实例，其定义如下：

```c
<struct def.h>

struct cache_sizes {

    size_t          cs_size;

    kmem_cache_t *cs_cache;

    kmem_cache_t *cs_dmacache;

#ifdef CONFIG_ZONE_DMA

    struct kmem_cache *cs_dmacache;

#endif

}
```

`size` 指定了该条目负责的内存区域。每个尺寸有两个 slab 缓存，一个提供适用于 DMA 的内存。

静态定义的 `malloc_size` 数组本质上使用 2 的幂次（从 $2^5=32$ 到 $2^{25}=131072$）对可用尺寸分组，具体取决于下文描述的 `KMALLOC_MAX_SIZE` 设置。

> ¹ 这不是强制的。如果一个模块想要获取在卸载模块并在下次加载时仍保留的持久内存（当然，假设在此期间系统重启了），它可以保留一个缓存，以便数据可以被重用。

> ² 在用户空间程序中使用 `printk`、`kmalloc` 和 `kfree` 是与内核编程接触过多的明显迹。

## 第3章：内存管理

```c
mm/slab.c

static struct cache_sizes malloc_sizes[] = {

#define CACHE(x) . cs_size = (x) ),

#if (PAGE_SIZE == 4096)

CACHE(32)

#endif

CACHE(64)

#if L1_CACHE_BYTES < 64

CACHE(96)

#endif

CACHE(128)

#if L1_CACHE_BYTES < 128

CACHE(192)

#endif

CACHE(256)

CACHE(512)

CACHE(1024)

CACHE(2048)

CACHE(4096)

CACHE(8192)

CACHE(16384)

CACHE(32768)

CACHE(65536)

CACHE(131072)

#if KMALLOC_MAX_SIZE >= 16384

CACHE(16384)

#endif

#if KMALLOC_MAX_SIZE >= 32768

CACHE(32768)

#endif

#if KMALLOC_MAX_SIZE >= 65536

CACHE(65536)

#endif

#if KMALLOC_MAX_SIZE >= 131072

CACHE(131072)

#endif

}
```
