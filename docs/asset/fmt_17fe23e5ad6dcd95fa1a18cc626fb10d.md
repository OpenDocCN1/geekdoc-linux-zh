
## TCP 分段、分片与 `skb_shared_info` 结构

如前所述，`skb_shared_info` 用于 IP 分片。它也可以用于存储 TCP 段，此时包含一个指向内存映射页的数组。TCP 提供了一种流服务，使得数据看起来是连续的字节序列，尽管数据必须被拆分成 IP 包。有关 TCP 分段的更多信息，请参阅第 7 章“通过 UDP 和 TCP 从 Socket 发数据”。当套接缓冲区被克隆时，`skb_shared_info` 会复制到新缓冲区。

共享结构的第一个字段 `dataref` 非零值表示套接缓冲区被克隆，因为每次发生克隆时它都会加 1。套接缓冲区 `cloned` 字段在克隆时也会设置为 1。共享信息结构中的下一个字段 `frag_list` 被 IP 分片重组设施使用。这就是列表上的每个分片如何共享同一个头部。每个分片的 IP 头部几乎相同。它们仅不同分片 ID 字段、分片偏移和校验和。当 IP 协议发现传入的 `skb` 是 IP 分片时，它会将包放入包含分片的特殊列表中。IP 将此列表（不复制实际数据包数据）移动到一个数据文中，该数据报由头部套接缓冲区以及一系列套接缓冲区组成，每个套接缓冲区指向一个分片。共享信息区域中的 `frag_list` 字段指向包含分片的套接缓冲区列表。虽然每个 IP 分片占用一个独立的缓冲区，但在创建时 `skb_shinfo` 结构本身会被复制到每个套接缓冲区。参见图 6.5，以获取指向 IP 分片数组的套接缓冲区插图。

`img/36e6a0d81dc7384273efb81016137b84_275_0.png`

图 6.5 带有分片的 `sk_buff`。

### 第 6 章 套接字缓冲区与 Linux 内存分配 263

## `skb_info` 结构与分段

共享信息结构中的第二个字段 `nr_frag` 不用于 IP 分片；相反，它用于 TCP 分段。当该字段包含非零值时，表示套接缓冲区包含分段。`nr_frag` 的值对应于附加到套接缓冲区的分段页数，而 `shared_info` 结构包含指向 `frags` 数组中分段页的指针。`frags` 数组放置在内存中 `nr_frag` 字段之后。该数组最多可以包含六页。数组中实际位置的数量取决于硬件架构和配置的页大小 `PAGE_SIZE`。`frags` 数组中的每个元素都指向 Linux 虚拟页表数组中的内存映射页。在第 5 章的前面部分，我们提供了更多关于 Linux slab 分配和虚拟页表的更详尽的信息。当由 TCP 创建的套接缓冲区包含一个分段链时，每个连续段的数据都在一个独立的内存映射页中，该页指向 `frags` 数组中的某个位置。这比为每个 TCP 段维护冗余的 `sk_buf` 结构要高效得多。当 TCP 处于 `ESTABLISHED` 状态时，后续段的包头几乎相同，因此包头可以在每个段之间共享。在处理过程中，不需要 Linux 为每个段拷贝完整的 IP 头部，从而节省了处理时间。

## `skb_frag_t` 结构

`frags` 数组中的每个位置由文件 `linux/include/linux/skbuff.h` 中定义的 `skb_frag_t` 结构组成。`frags` 数组的大小计算为可容纳总 64 Kb 的数据，这是 IPv4 定义的最大数据包大小。当然，数组将这 64 K 数据划分为独立的内存映射页。

```c
#define MAX_SKB_FRAGS (65536/PAGE_SIZE + 2)

typedef struct skb_frag_struct skb_frag_t;

struct skb_frag_struct {
```

`page` 是一个指向页表项的指针。下一个字段 `offset` 是从页起始位置到数据开始位置的偏移量。`size` 是页中数据的长度。

```c
struct *page;

__u16 page_offset;

__u16 size;

};
```

图 6.6 是包含 TCP 段数组的套接缓冲区插图。

`![](img/36e6a0d81dc7384273efb81016137b84_277_0.png)`

正如本章之前讨论，Linux slab 内存分配系统适用于网络协议栈，因为它效率高且不易产生碎片。套接缓冲区头部缓存也提供了性能增强，因为套接缓冲区在释放时不会返回到通用内核内存，而是被放置在单独的头部缓存中。有多个头部缓存，在多处理器实现中，每个 CPU 都有一个。缓冲区会从当前 CPU 的头部缓存中获取或返回到该缓存中。当创建一个 `sk_buff` 时，分配函数 `alloc_skb` 正如我们看到的那样分配套接字，套接缓冲区的前两个字段是 `next` 和 `prev` 指针。这样做是为了便于队列的维护。操作网络缓冲区队列的能力对于网络中使用的任何缓冲区系统都具有至关重要的意义。因此，Linux 提供了一组接口函数用于入队、出队和维护套接缓冲区列表。关于 `sk_buff` 使用的示例，我们可以查看第 5 章，该章包含了关于队列层的更详细的信息。

## 套接字缓冲区实用函数

Linux 提供了许多实用函数来分配、释放和操作套接字缓冲区 `sk_bufs`。除非使用得当，否则某些套接缓冲区不是中断安全的，通常，这些函数都有安全和不安全版本。不安全函数包括……（此处原文不完整）。在中断服务程序调用时，必须设置为 `GFP_ATOMIC`。它在 `linux/include/skbuff.h` 中定义了安全版本。如果使用不当，某些套接缓冲区不是中断安全的。在中断服务程序调用时，安全版本是……（此处原文不完整）。关于 `sk_buff` 使用的示例，我们可以查看第 5 章，该章包含了关于队列层的更详细的信息。

## 套接字缓冲区分配与释放函数

一组函数用于套接缓冲区的创建和销毁。

## `alloc_skb` 函数

`alloc_skb` 分配一个新的套接缓冲区。

```c
extern struct sk_buff *alloc_skb(unsigned int size, gfp_t priority);
```

该函数是不安全的。在中断服务程序调用时，必须设置为 `GFP_ATOMIC`。它通过调用 `kmem_cache_alloc` 从 slab 获取缓冲区。如果调用者请求奇数大小，它将根据架构将其对齐到字边界。

# 第 6 章 套接缓冲区与 Linux 内存分配

```c
extern struct sk_buff *_alloc_skb(unsigned int size, gfp_t priority, int fclone);
```

分配后，`alloc_skb` 设置了套接缓冲区中的一些字段。由于套接缓冲区是从 slab 分配的，大多数字段已经初始化。`trsize` 字段设置为缓冲区的长度加上套接缓冲区本身的长度。`head`、`data` 和 `tail` 指针都指向数据的起始位置，数据是用 `kmalloc` 分配的。`end` 指向缓冲区部分的末尾，正如之前讨论的，这就是 `sk_info` 结构所在。`len`、`cloned` 和 `datalen` 字段都设置为零。这些字段稍后会根据包大小的变化进行调整。

`users` 字段设置为一，表示这是对 `sk_buff` 的首次引用。最后，在 `sk_info` 结构中初始化了一些字段。由于此包既没有碎片列表也没有页数组，`dataref` 设置为一，`frag_list` 设置为 `NULL`。

## `dev_alloc_skb` 函数

`dev_alloc_skb` 也分配一个新的缓冲区 `sk_buff`。

```c
static inline struct sk_buff *dev_alloc_skb(unsigned int length)
```

`dev_alloc_skb` 为设备驱动开发者提供便利。以太网接口和其他网络接口设备。该函数是安全的，内部调用 `alloc_skb` 时会将 `gfp_mask` 设置为 `GFP_ATOMIC`。在调用 `alloc_skb` 实际分配 `sk_buff` 和附加数据缓冲区之前，它向长度字段增加了 16 字节为以太网 MAC 头部留空间。

## `kfree_skb` 函数

```c
static inline void kfree_skb(struct sk_buff *skb)
```
