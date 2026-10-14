
# 第4章 在内核中管理网络包

```c
skb_copy() net/core/skbuff.c
```

`skb_copy(skb, gfp_mask)` 创建套接缓冲区 `skb` 的副本，同时复制 `sk_buff` 结构和包数据。首先用户调用 `alloc_skb()` 获取一个新的 `sk_buff` 结构；然后设置其属性。注意，它只接受特定协议的参数（优先级、协议...）、相关的网络设备（`device`）以及路由缓存中的条目。所有处理套接缓冲区连接的指针（`next`、`prev`、`skb_list`）都被设置为空。

新套接缓冲区载荷所需的内存通过 `kmalloc()` 分配并通过 `memcpy()` 复制。随后，新数据空间的指针被设置在新的 `sk_buff` 结构中。`skb_copy()` 返回一个新的套接缓冲区（带有它自己的包数据空间），它与原始缓冲区独立存在并可以被独立处理。这意味着创建的副本的引用计数也显示为 1，这与使用 `skb_clone()` 复制包不同。

```c
skb_copy_expand() net/core/skbuff.c
```

`skb_copy_expand(skb, headroom, newtailroom, gfp_mask)` 同样创建一个新的独立的套接缓冲区副本，但是，之前的和

![skb_copy](https://example.com/skb_copy.png)

![skb_clone](https://example.com/skb_clone.png)

## 4.1 套接缓冲区

| `sk_buff` | `skb_copy` | `sk_buff` | `sk_buff` |

|---|---|---|---|

| `next` | | `next` | |

| `prev` | | `prev` | |

| ... | | ... | ... |

| `head` | | `head` | |

| `data` | | `data` | |

| `tail` | | `tail` | |

| `end` | | `end` | |

包数据存储 包数据存储 包数据存储

| IP header | IP header | IP header |

|---|---|---|

| UDP header | UDP header | UDP header |

| UDP data | UDP data | UDP data |

`dataref`: 1 `dataref`: 1 `dataref`: 1

图 4–5 克隆套接缓冲区。

### `dev_kfree` `include/linux/skbuff`

`dev_kfree-skb(skb)` 与 `kfree_skb()` 方法完全相同，并通过预处理器宏映射到 `kfree_skb()`。

### `kfree_skmem` `include/linux/skbuff`

`kfree_skmem()` 释放套接缓冲区，前提是它没有被克隆，且内核中没有实例引用它（`dataref - 1`）。测试 `skb_cloned` 是否为空，并测试 `dataref` 是否为 1。如果一切正常，`kfree()` 首先释放包内存。然后使用 `skb_head_to_pool()` 将 `sk_buff` 结构插入当前处理器的套接缓冲区缓存中供后续使用。这意味着套接缓冲区结构的内存没有释放给通用（`kfree()`），而是用于回收。

### `kfree_skb()` `include/linux/skbuff`

`kfree_skb()` 执行 `kfree_mem()` 操作，但它还会测试套接缓冲区是否在队列中（如果是，则输出错误消息）。此外，它从路由缓存中移除引用，如果存在，还会调用套接缓冲区的析构函数，由于这些额外的检查，应优先选择 `kfree_skb()`。

### 操作包数据空间

以下函数在包含文件 `<Linux/skbuff.h>` 中声明。它们大多数定义为内联函数且功能很小；尽管如此，它们非常重要且被频繁使用。

#### `skb_get()` `include/linux/skbuff.h`

该函数将 `skb_buff` 结构的用户引用计数加 1。

#### `skb_unshare()` `include/linux/skbuff.h`

`skb_unshared(skb)` 使用 `skb_cloned` 来检查套接缓冲区是否可以独占使用。如果不是，则创建并返回 `skb` 的副本，以便提供一个独占的套接缓冲区。在原始数据包中，引用计数减 1。

#### `skb_put()` `include/linux/skbuff.h`

`skb_put(skb, len)` 是一个内联函数，用于在数据包当前数据范围的末尾追加数据。虽然这种情况很少发生，因为大多数协议会在当前数据包单元之前写入其 PCI（协议控制信息），但仍有少数协议需要这种操作。具体来说，`skb_put()` 将 `point-tail` 和参数 `skb->len` 增加了 `len`。请注意，`skb_put()` 仅仅重新设置了指针；调用者负责将正确的数据拷贝到包数据空间，以便能够将新的数据包数据添加到正确的位置。在调用 `skb_put()` 之前，我们应该确认尾部空间（tailroom）足够（`skb->tail` 的旧值），否则内核将输出错误消息并调用 `skb_over_panic()`。

#### `skb_push()` `include/linux/skbuff.h`

`skb_push(skb, len)` 类似于 `skb_put()`，但在数据包开头增加了 `len` 字节的当前数据包数据空间。这意味着数据指针减少了 `len`，`skb->len` 增加了相应长度。`skb_push()` 的返回值指向新的数据空间（在这种情况下为 `skb->data`）。同样，我们应该先检查头部空间（headroom）的大小。

#### `skb_pull()` `include/linux/skbuff.h`

`skb_pull(skb, len)` 用于截断数据包开头的 `len` 字节。指针 `skb->data` 会进行调整，数据包长度（`skb->len`）也会随之减少——但首先我们会检查数据包数据空间的剩余部分是否还有字节。

#### `skb_tailroom()` `include/linux/skbuff.h`

`skb_tailroom(skb)` 返回数据空间末尾仍然空的字节。如果 `skb_put()` 在此空间请求的数据超过了 `skb_tailroom` 的的状态，将导致内核崩溃（panic）。

#### `skb_headroom()` `include/linux/skbuff.h`

`skb_headroom(skb)` 返回 (`data` - `head`)。这对应于数据包数据内存前端的可用字节数。`skb_push()` 可以恰好向数据包中插入 `skb_headroom` 字节。

#### `skb_realloc_headroom()` `include/linux/skbuff.h`

当 `skb->data` 和 `skb->head` 之间的内存空间太小时时，需要使用 `skb_realloc_headroom(skb, newheadroom)`。此函数可以创建一个头部空间对应 `newheadroom` 大小（而不是单个字节）的新套接缓冲区。旧套接缓冲区的数据部分会被拷贝到新缓冲区，`skb_buff` 结构的大部分参数取自旧缓冲区。只有 `sk` 和 `len1` 被设置为 NULL。`skb_realloc_headroom()` 通过调用函数 `skb_copy_expand()` 实现。

#### `skb_reserve()` `include/linux/skbuff.h`

`skb_reserve(skb, len)` 将当前数据空间向后移动 `len` 字节。这意味着该空间的总长度保持不变。当然，此函数仅在当前空间尚无数据且必须修正该空间初始占用情况时才有意义。

#### `skb_trim()` `include/linux/skbuff.h`

`skb_trim(skb, len)` 将当前数据包数据空间设置为 1 字节，这意味着该空间现在从数据的初始占用延伸到 `tail - data - 1len`。此函数通常用于截断末尾数据（即我们调用 `skb_trim()` 的长度值小于当前数据包的大小）。

#### `skb_cow()` `include/linux/skbuff.h`

`skb_cow(bytes, headroom)` 检查传递的套接缓冲区在数据包数据空间是否有至少 `headroom` 字节的可用空间，以及该数据包是否仍为克隆。如果这两种情况中的任一成立，则 `skb_alloc_headroom(skb, headroom)` 将创建并返回一个新的独立的数据包。如果测试都不通过，则返回该套接缓冲区。当协议需要具有足够头部空间的独立套接缓冲区时，使用 `skb_cow()`。

## 4.2 Other Functions

### `skb_cloned()` `include/linux/skbuff.h`

`skb_cloned(skb)` 指定此套接缓冲区是否被克隆以及相应的数据包空间是否为独占。引用计数 `dataref` 用于检查此项。
