
### 4) cache_grow/shrink

```c
/* slab 的页阶数 (2^n) */
unsigned int gpforder;

/* 强制 GFP 标志，例如 GFP_DMA */
size_t colour; /* 缓存颜色范围 */
unsigned int colour_off; /* 颜色偏移 */

struct kmem_cache *slab_cache;

unsigned int slab_size;

unsigned int dflags; /* 动态标志 */

/* 构造函数 */
void (*ctor)(struct kmem_cache, void *ptr);
```

### 5) 缓存创建/移除

```c
const char *name;

struct list_head next;
```

### 6) 统计信息

```c
...

struct kmem_list_3 *nodelists[MAX_NUMNODES];
```

这个冗长的结构根据内核源码中的注释被分为多个部分。

初始元素与内核在每次分配期间访问的 CPU 特定数据有关，在第 3-46 节中提到过。

- `array` 是一个指向数组的指针，系统中的每个每个 CPU 都有一个条目。每个条目包含一个指向下文讨论的 `array_cache` 结构实例的进一步指针。
- `batchcount` 指定从缓存的 slab 中取出并添加到每个 CPU 列表的对象数量（如果是）。它还指示了缓存增长时分配的对象数量。
- `limit` 指定了每个 CPU 列表中可以持有的对象最大数量。如果超过此值，内核会将 `batchcount` 中定义的对象数量返回给 slabs（如果内核收缩缓存，内存将从 slabs 返回到伙伴系统）。
- `buffer_size` 指定了在缓存中管理的对象的大小。

假设内核有一个指向 slab 中某个元素的指针，并想根据对象大小确定对象索引。此此最简单的方法是将指针到 slab 起位置的偏移量除以对象大小。例如，如果 slab 区域从内存位置 100 开始，每个对象包含 5 字节，对象位于内存位置 115。slab 与对象之间的偏移量为 115 - 100 = 15，因此对象索引为 15/5。遗憾的是，在旧机器上除法速度很慢。

由于乘法在机器上甚至更慢，内核只需要乘法和位移。虽然数学结果对我们的目的并不重要（它们可以在任何标准教科书中找到），但我们需要知道，与其计算 C = A/B，内核也可以采用 C = reciprocal_value(A, reciprocal_value(B)) —— 这两个函数都作为库例程提供。由于 slab 中的对象大小是固定的，内核可以将 `buffer_size` 的倒数值存储在 `reciprocal_buffer_size` 中，在稍后必须计算除法时可以使用它。

内核为每个系统处理器提供一个 `array_cache` 实例。其定义如下：

```c
struct slab_cache {
    unsigned int avail;
    unsigned int limit;
    unsigned int batchcount;
    unsigned int touched;
    spinlock_t lock;
    void *entry[];
};
```
