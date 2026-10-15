
`kmem_cache_t *kmem_cache_create(const char *name, size_t size, size_t offset, unsigned long flags, void (*)(void*, kmem_cache_t *, unsigned long), void (*)(void*, kmem_cache_t *, unsigned long));`

第一个参数是一个指向缓存标识符的字符串指针。通常，它是表 6.2 所示的硬编码字符串。该函数返回一个指向 `kmem_cache_t` 的指针，它被通用定义为指向 `linux/slab.c` 文件中 `kmem_cache_s` 结构体的指针。然而，每次调用 `kmem_cache_create` 通常都会重新定义 `kmem_cache_t`，将其设置为该 slab 缓存的唯一类型，该类型也是缓存名称。`unsigned long` 类型参数是标志（flags），设置为表 6.3 中的一个值之一。这些标志定义在 `linux/include/linux/slab.h` 文件中。两个参数中的第一个指向构造函数，第二个指向析构函数。这两个函数中的每一个都可以为 `NULL`，也可以指向一个针对特定缓存类型实现的函数。

# 表 6.3 `kmem_cache_create` 函数的 Slab Cache 标志

| 标志 (Flag) | 值 | 用途 |
| --- | --- | --- |
| `SLAB_DEBUG_FREE` | `0x00000100UL` | 调用 `free` 时执行调试检查。此标志似乎没有在任何地方使用。 |
| `SLAB_DEBUG_INITIAL` | `0x00000200UL` | 在对象初始化和调用构造函数时执行调试检查。 |
| `SLAB_RED_ZONE` | `0x00000400UL` | 在分配的缓冲区周围创建一个“红区”以进行溢出检查。 |
| `SLAB_POISON` | `0x00000800UL` | 请求用测试模式初始化新缓冲区，该模式为 `0xa5a5a55`。 |
| `SLAB_NO_REAP` | `0x00001000UL` | 缓存中的对象永远不应被回收（reaped）。此标志似乎没有被广泛使用。 |
| `SLAB_HWCACHE_ALIGN` | `0x00002000UL` | 指定创建缓存中的对象按硬件缓存行对齐。此标志被 TCP/IP 中几乎所有的 slab 缓存使用。 |
| `SLAB_CACHE_DMA` | `0x00004000UL` | 缓存中的对象应从 DMA 内存创建，类型为 `GFP_DMA`。此标志在 TCP/IP 中未使用。网络驱动程序使用 DMA，但数据被放置在附加套接字缓冲区的页，而不是直接放入 slab 缓存。 |
| `SLAB_MUST_HWCACHE_` | `0x00008000UL` | 强制对齐到硬件缓存行。此标志未用于 TCP/IP。 |
| `SLAB_STORE_USER` | `0x00010000UL` | 存储对象的最后一个所有者。此标志仅用于调试。 |
| `SLAB_RECLAIM_ACCOUNT` | `0x00020000UL` | 跟踪回收账户情况。 |
| `SLAB_PANIC` | `0x00040000UL` | 失败时崩溃（panic）。 |
| `SLAB_DESTROY_BY_RCU` | `0x00080000UL` | 通过 RCU 延迟销毁。 |
| `SLAB_STRUCTOR` | `0x00000001UL` | 指明对象使用构造函数。 |
| `SLAB_CTOR_ATOMIC` | `0x00000002UL` | 指明以原子方式执行。 |
| `SLAB_CTOR_VERIFY` | `0x00000004UL` | 在销毁时验证。 |

## `kmem_cache_destroy` 函数

该函数删除 slab 缓存。

```c
int kmem_cache_destroy(kmem_cache_t *);
```

该参数指向 slab 缓存。该函数将删除套接字缓冲区痕迹。

## `kmem_cache_shrink` 函数

```c
int kmem_cache_shrink(kmem_cache_t *);
```

该函数尽可能地移除缓存。

## `kmem_cache_size` 函数

```c
unsigned int kmem_cache_size(kmem_cache_t *);
```

它返回缓存的大小。

## `kmem_cache_alloc` 函数

```c
void *kmem_cache_alloc(kmem_cache_t *, gfp_t);
```

这返回指向对象的指针。第二个参数可以是表 6.4 列出的值之一。

### 表 6.4 `kmem_cache_alloc` 的标志值

| 标志 (Flag) | 含义 |
|---|---|
| `GFP_USER` | 为用户空间分配内存时使用。 |
| `GFP_KERNEL` | 用于内核内存使用。 |
| `GFP_ATOMIC` | 当调用是中断服务程序时使用。 |
| `GFP_DMA` | 表明应从 DMA 分配。 |
| `GFP_NOFS` | 当不需要文件系统调用时使用。 |
| `GFP_NOIO` | 当需要重新调度但不需要 IO 时使用。 |

## `kmem_cache_free` 函数

```c
void kmem_cache_free(kmem_cache_t *, void *);
```

第二个参数指向要释放的对象。第一个参数必须指向最初从哪个缓存分配的对象。

## LINUX 套接字缓冲区

正如之前在本章和其他章节中讨论过的，套接字缓冲区是穿越 TCP/IP 栈的数据包的容器。在本节中，我们讨论了套接字缓冲区（即 `sk_buff`）的内部架构、它们如何被分配、在释放时如何放置，以及内部 `skbuff` 队列的工作原理。套接字缓冲区可以被克隆或共享，套接字缓冲区结构包含字段来指示特定缓冲区是否被克隆或共享。Linux 提供了一个克隆套接字缓冲区的实用函数，我们将在本章后续章节与其他实用函数一起解释该函数。然而，套接字缓冲区结构的字段将在本节稍后部分显示。附加到套接字缓冲区的缓冲区或数据区域可以处于多种形式。它可以直接包含整个 TCP/IP 包，也可能只包含 TCP/IP 头部，而包的其他部分位于附加的映射页列表中。图 6.4 展示了套接字缓冲区最通的形式，以及如何使用指针字段找到附加 TCP/IP 包中的各个位置。

图 6.4 Linux 缓冲区套接字。

## 套接字缓冲区结构，`sk_buff`

在本节中，我们将检查套接字缓冲区的内部结构。缓冲区布局的概览请参考图 6.4。定义 Linux 套接字缓冲区 `sk_buff` 的结构位于文件 `linux/include/linux/sk_buff.h` 中。

```c
struct sk_buff {
    struct sk_buff      *next;
    struct sk_buff      *prev;
    struct sock         *sk;
    struct timeval      *stamp;
    struct net_device    *dev;
    struct net_device    *input_dev;
    union {
        struct tcphdr    *th;
        struct udphdr    *uh;
        struct icmphdr     *icmph;
        struct igmphdr     *igmph;
        struct iphdr       *iphdr;
        struct ipv6hdr      *ipv6h;
        unsigned char     *raw;
    } h;
    union {
        struct iphdr       *iph;
        struct ipv6hdr     *ipv6h;
    } nn;
}
```

套接字缓冲区中的以下两个字段必须在前。正如我们在书中后面看到的，有时套接字缓冲区列表会被重载为不同的类型。`next` 指向列表中的下一个缓冲区，`prev` 指向上一个缓冲区。

下一个字段指向一个套接字结构体，对于发送的数据包，它指向该数据包源的套接字。

对于接收的数据包，下一个字段 `stamp` 表示该数据包到达接口的时间。对于接收的数据包，`dev` 显示接收该数据包的设备。`dev` 指向网络接口。在涉及伪设备的情况下，`real_dev` 指向实际物理设备。

接下来的三个字段是联合（unions），展开为特定的头部类型字段。这些字段的目的是方便访问数据包中的所有头部字段。`h` 指向此缓冲区包含的数据包中的传输层头部，`nn` 指向此缓冲区包含的数据包中的网络层头部。`mac` 指向链路层头部。

这些是传输层头部，但实际上包含了任何被 IP 封装的协议。前四个头部分别对应 TCP、UDP、ICMP 和 IGMP。

`ipip` 是 IP 隧道头部，`raw` 是一个通用头部指针，`ipv6h` 是 IPv6 IP 头部。

这些是网络层头部。`iph` 是 IPv4 头部，`ipv6h` 是 IPv6 头部。
