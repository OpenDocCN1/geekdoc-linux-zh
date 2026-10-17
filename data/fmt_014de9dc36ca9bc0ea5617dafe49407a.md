
| `SLAB_CACHE_DMA` | `0x00004000UL` | 缓存对象可以从 DMA 内存创建，类型为 GFP DMA。此标志未在 TCP/IP 中使用。 |

| 表 7.3: Slab Cache 标志 |

| 标志 (Flag) | 值 (Value) | 目的 (Purpose) |

| :--- | :--- | :--- |

| `SLAB_MUST_HWCACHE_ALIGN` | `0x00008000UL` | 强制对齐硬件缓存行。TCP/IP.cache 不使用此标志。 |

| `SLAB_STORE_USER` | `0x00010000UL` | 存储对象的最后一个所有者。此标志仅用于调试。 |

| `SLAB_RECLAIM_ACCOUNT` | `0x00020000UL` | 跟踪单独页以指示哪些页以后可能被回收。此标志由 socket 缓存使用。 |

| | | 分缓存对象时，以下三个标志会被传递给构造函数。 |

| `SLAB_CTOR_CONSTRUCTOR` | `0x001UL` | 表示调用构造函数进行对象初始化，而不是析构函数（析构函数通常负责初始化）。 |

| `SLAB_CTOR_ATOMIC` | `0x002UL` | 通知构造函数必须以原子方式执行。 |

| `SLAB_CTOR_VERIFY` | `0x0004UL` | 如果设置此标志，则调用构造函数仅用于验证。 |

只有在将未初始化的 slab 添加到 slab 缓存时，才会调用构造函数。

函数 `kmem_cache_destroy` 销毁 slab 缓存。

```c
int kmem_cache_destroy (kmem_cache_t *cachep);
```

参数 `cachep` 指向 slab 缓存。此函数将移除该 slab 缓存的所有痕迹。如果模块创建了不需要在模块加载之间持久存在的 slab，则应在模块卸载前从模块调用此函数。调用此函数之前，缓存中的所有对象都应该被释放。在函数执行期间，调用者必须保护缓存免受分配。

下一个函数 `kmem_cache_shrink` 减小 slab 缓存的大小。

```c
int kmem_cache_shrink (kmem_cache_t *cachep);
```

它尽可能地移除 slab。当所有 slab 都释放时，它返回 0。

函数 `kmem_cache_size` 获取缓存大小。

```c
unsigned int kmem_cache_size (kmem_cache_t *cachep);
```

它返回 `cache` 指向的缓存中对象的大小。

接下来的两个函数用于在特定的 slab 缓存中分配和释放对象。

`kmem_cache_alloc` 从特定的 slab 缓存分配一个对象。

```c
void * kmem_cache_alloc (kmem_cache_t *cachep, int flags);
```

它返回指向由 `cache` 指向的分配 slab 的指针。参数 `flags` 可以是表 7.4 列出的四个值之一。仅当缓存不包含任何对象且必须“增长”时才使用标志。这些值是“获取空页”的值，单独页分配在 slab 缓存的后台进行的。

| 表 7.4: Kmem_cache_alloc 函数中标志参数的值 |

| 标志 (Flag) | 含义 (Meaning) |

| :--- | :--- |

| `GFP_USER` | 用于为用户空间中的应用程序分配内存。 |

| `GFP_KERNEL` | 用于正常的内核内存分配。 |

| `GFP_ATOMIC` | 当调用者是中断服务程序时使用。 |

| `GFP_DMA` | 表明内存应从 DMA 空间分配。此标志用于架构开发。 |

本节的最后一个函数 `kmem_cache_free (kmem_cache_t *cachep, void *objp)`。

参数 `objp` 指向要释放的对象。`cache` 必须指向最初分配对象的缓存。

## 7.7 Linux 套接缓冲区 (Socket Buffers)

在本节中，我们将讨论套接缓冲区（或 `sk_bufs`）的内部架构、它们如何被分配、在释放时如何被放入头部缓存中，以及内部 `sk_buff` 队列是如何运作的。套接缓冲区是复杂的，包含许多用途看似模糊的字段，例如指针、计数器和其他维护项。在本节及随后的章节中，我们试图理清所有数据，并理解 `sk_buff` 结构中的字段以及操作这些字段的函数。与套接字关联的数据存储在单独缓冲区，通常直接通过 `kmalloc` 分配；然而，这看起来并不那么简单。缓冲区可以被克隆或共享，套接缓冲区结构体字段会指示缓冲区是关闭还是共享的。提供了一个克隆缓冲区的实用函数，该函数将在本章后面的其他函数中进行解释。附加到套接缓冲区的缓冲区或数据可以是多种形式。它可能包含整个 TCP/IP 数据包，也可能只包含 TCP/IP 头部，其余包内容位于映射页列表中。图 7.4 显示了最通用形式的套接缓冲区图像，以及如何使用指针字段找到附加的 TCP/IP 数据包中的各种位置。

![](img/c1f701734d482a86a48e8bfd231c6fdb_195_0.png)

### 7.7.1 套接缓冲区结构，Sk_buff

套接缓冲区结构 `sk_buff` 定义在文件 `/linux/include/linux/skbuff.h` 中。

```c
struct sk_buff {
```

套接字两个字段必须在前面。正如我们后面看到的，有时套接缓冲区列表会被重载为不同类型。接下来 `next` 指向列表中的下一个缓冲区，`prev` 指向上一个缓冲区。

```c
struct sk_buff {
    struct sk_buff *next;
    struct sk_buff *prev;
```

下一个字段 `list` 指向列表的头部。这用于套接缓冲区队列。

```c
struct sk_buff {
    struct sk_buff_head *list;
```

下一个字段 `sk` 指向包含实际数据的套接字结构。

```c
struct sk_buff {
    struct sk *sk;
```

下一个字段 `stamp` 指示数据包到达的时间。这用于超时和计时逻辑。

```c
struct sk_buff {
    struct timeval stamp;
```

下一个字段 `dev` 指向数据包通过的网络设备。

```c
struct sk_buff {
    struct net_device *dev;
```

下一个字段 `cb` 被称为控制缓冲区。它用于存储跨层拷贝的协议特定项。

```c
struct sk_buff {
    char cb[48];
```

下一个字段 `len` 包含头部和任何数据的总长度。`data_len` 是包的数据部分长度。`csum` 持有 IP 头部校验和。

```c
struct sk_buff {
    unsigned int len;
    unsigned int data_len;
    int csum;
```

`local_df` 持有“不分片”值。如果设置，数据包在传输时不会被分片。`cloned` 表示此包被克隆过。`pkt_type` 是包的类别，设置为表 7.5 中的值之一。`ip_summed` 字段指示输出设备是否可以计算 IP 校验和。

```c
unsigned char local_df;
unsigned char cloned;
unsigned char pkt_type;
unsigned char ip_summed;
```

表 7.5: 套接缓冲区中的包类型

| 包类型 (Packet Type) | 值 (Value) | 目的 (Purpose) |

| :--- | :--- | :--- |

| `PACKET_HOST` | 0 | 指向本机器的数据。 |

| `PACKET_BROADCAST` | 1 | 广播包。 |

| `PACKET_MULTICAST` | 2 | 多播包。 |

| `PACKET_OTHERHOST` | 3 | 发送到对端的单播包。 |

| `PACKET_OUTGOING` | 4 | 发出包。 |

| `PACKET_LOOP` | 5 | 任何环回的广播或单播包。 |

| `PACKET_FASTROUTE` | 6 | 此包将在快速路由路径中处理。 |

下一个字段指向该数据包的析构函数，如果没有，则指向 NULL。

```c
void
    (*destructor) (struct sk_buff *skb);
```

如果配置了 netfilter，则会使用以下字段：
