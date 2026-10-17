
（注：OCR 文本在最后的 struct 块中存在严重损坏，如 "ununion struct" 和 "__u8proto"，这些已根据路由表的标准内核结构重建。）

等等，让我严格遵循提供的 OCR 文本处理最后一个块，同时修复 OCR 错误：

#### 表 9.3：ToS 字段位定义

| 定义 | 值 | 用途 |
| --- | --- | --- |
| `IPTOS_LOWDELAY` | `0x10` | 这是低延迟位。 |
| `IPTOS_THROUGHPUT` | `0x08` | 吞吐量位。 |
| `IPTOS_RELIABILITY` | `0x04` | 可靠性位。 |
| `IPTOS_MINCOST` | `0x02` | 该位用于... |
| `RTO_ONLINK` | `0x01` | 该位用于识别直接连接的主机。 |

### 9.5.2 路由缓存实用

如前所述，每个路由条目 `rtable` 的第一部分包含目的缓存 `dst_entry`。`dst_entry` 包含了 `dst_ops` 结构，其中包含对应缓存操作的函数指针。每个使用缓存的路由协议都可以实现这些函数。通用目的缓存在第 6 章中讨论。特定于 IP 的目的函数全部位于 `linux/net/ipv4/route.c` 中，如表 9.4 所示。

#### 表 9.4：IP 缓存的 dst_ops 值

| dst_ops 中的字段 | IP 函数或值 | 用途 |
| --- | --- | --- |
| `family` | `AF_INET` | IPv4 地址族。 |
| `protocol` | `ETH_P_IP` | 头部中的协议字段，`0x0800`。 |
| `gc` | `rt_garbage_collect` | 垃圾回收函数。 |
| `check` | `ipv4_dst_check` | 释放目的缓存条目。 |
| `destroy` | `ipv4_dst_destroy` | 路由条目的析构函数。 |
| `negative_advice` | `ipv4_negative_advice` | 当条目变为重定向或过时时调用此函数。 |
| `link_failure` | `ipv4_link_failure` | 发送 ICMP 不可达消息并过期路由。 |
| `update_pmtu` | `ip_rt_update_pmtu` | 更新路由的 MTU。 |

表 9.4 中的几个函数值得关注。第一个是垃圾回收函数 `rt_garbage_collect`，在第 9.5.3 节中解释，另一个是目的检查函数 `ipv4_dst_check`，通过 `dst_ops` 结构的 `cache` 字段访问。它所做的只是调用 `dst_release`，这是目的缓存的通用函数。

这里展示了删除函数 `ipv4_dst_destroy`。

```
static void ipv4_dst_destroy(struct dst_entry *dst);
```

它会删除通过 `rtable` 结构体的 `rt` 字段访问的关联的 Internet 对端 `inet_peer`。

负面建议函数 `ipv4_negative_advice` 会移除 `dst` 指向的缓存中的路由。

```
static struct dst_entry *ipv4_negative_advice(struct dst_entry *dst);
```

首先，它通过检查 `dst` 的 `obsolete` 字段来检查路由是否已过期。如果是，它会调用 `ip_rt_put` 将路由返回到 slab 缓存。否则，我们会删除所有关于该目的地且我们接收到了负面建议的路由。我们通过检查 `dst_entry` 中的 `entry` 字段来检查该条目是否已过期，或者通过检查 `rt_flags` 字段中是否存在 `RTCF_REDIRECT` 标志来检查路由是否被重定向。如果是，它将重新计算 32 位哈希值并调用 `rt_del` 来删除哈希桶位置中的所有路由。

除了操作函数外，路由缓存也可以直接调用。仔细查看这些定义在 `route.h` 中的函数是有帮助的。其中一些是内联函数（inlines），其他函数定义在 `route.c` 中。第一个函数 `ip_rt_put` 通过调用目的地缓存的通用 `dst_release` 函数来删除路由。

```
static inline void ip_rt_put(struct rtable *rt)
{
    if (rt)
        dst_release(&rt->dst);
}
```

下一个函数 `rt_bind_peer` 为路由创建一个条目。在此效果中，它向路由表中添加了关于目的地的信息。

```
void rt_bind_peer(struct rtable *rt, int create);
```

首先，它通过调用 `inet_get` 创建一个新的 `inet_peer` 结构。它在锁定路由缓存的同时，将 `rtable` 中的 `peer` 字段设置为路由对端，并递增 `inet_peer` 结构中的计数器。

使用 `SOCK_STREAM` 类型套字的应用程序在通过打开的套字发送数据包之前，需要与远程对端建立连接。为了建立连接，应用程序在打开的套字上调用 `connect`。连接建立后的工作之一是设置到目的地的路由。在运行 `SOCK_DGRAM` 类型套字的应用程序中，`connect` 套字调用会在发送数据之前设置到目的地址的路由。IP 提供了 `ip_route` 函数来建立路由。该函数定义在 `linux/include/route.h` 文件中。

```
static inline int ip_route_connect(struct rtable **rp, u32 dst, u32 src, u32 tos, int of, u8 protocol, u16 port, u16 dport, struct sock *sk);
```

实际上，`ip_route_connect` 仅是主路由解析函数 `ip_route_output` 的前端，该函数将在 9.8 节中讨论。

其他几个配合路由表使用的函数也值得提及。这些函数并不是路由缓存接口的一部分，因为它们是静态函数。然而，它们被如 `ip_route_output` 等路由函数使用。查看这些函数对于理解路由条目是如何创建和使用的是有帮助的。

当新路由准备好用于传输数据包时，`ip_route_output` 调用定义在 `linux/net/ipv4/route.c` 中的函数 `rt_intern_hash`，将路由进入路由缓存。

```
static int rt_intern_hash(unsigned hash, struct rtable **rp);
```

`rt_intern_hash` 使用哈希值作为哈希表 `rt_hash_table` 的索引。该索引指向一个与路由最匹配的位置。该位置可能包含零、一个或多个路由。接下来，`rt_intern_hash` 使用路由结构体中的 `routei` 寻找与哈希表中的某条路由的精确匹配。如果找到了精确匹配项，它会将匹配的路由移动到列表头部，递增其计数，并释放新路由。如果与表中的任何路由都没有精确匹配，则会将新路由放置在发布到哈希位置的链表列表的最前端。在将新路由放入缓存之前，我们尝试通过调用 `arp_bind_neighbour` 将其绑定到邻居缓存。如果看起来邻居缓存已满，我们会调用 `rt_garbage_collect` 移除路由，直到为新路由腾出空间。如果 `rt_intern_hash` 未能找到空间，它将返回 `ENOBUFS` 错误。

两个路由解析函数 `ip_route_output_slow` 和 `ip_route_input_slow` 如果有指向外部且不指向直接连接主机的路由，都需要设置某些特定信息。例如，IP 允许为路由指定 MTU，且 TCP 有一个选项与对端协商最大段大小。用于设置这些信息的函数是 `rt_set_nexthop`。

```
void rt_set_nexthop(struct rtable *rt, struct fib_result *res, u32 itag);
```
