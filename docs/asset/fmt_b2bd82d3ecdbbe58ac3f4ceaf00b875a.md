
`struct net_device *dev, int create);`

`int pneigh_delete(struct neigh_table *tbl, const void *pkey, struct net_device *dev);`

```
## pneigh_enqueue 函数

该代理函数将 `skb` 放入代理队列并设置代理计时器。

```

`void pneigh_enqueue(struct neigh_table *tbl, struct neigh_parms *p, struct sk_buff *skb);`

如果我们希望数据等待代理 ARP 请求的响应，则调用 `pneigh_enqueue`。

## 使用缓存传输数据包

在接下来的章节中，我们将查看各种协议的数据包输出程序如何利用目的缓存和邻居缓存。

## 使用目的缓存发送数据包

在接下来的章节中，我们将查看如何使用目的缓存和目的缓存来传输数据包。我们展示了协议的输出函数如何使用邻居结构和目的缓存，在输出数据包准备传输时快速找到输出网络接口、硬件头部（hard-header）和输出传输函数。我们将从数据包准备好传输时，网络层协议的传输函数检查目的缓存的时间点开始。目的缓存条目通过套接缓冲区（socket buffer）访问。为了理解目的缓存的工作原理，最好的方法是检查一个特定场景，我们将使用 IP 协议的输出路由作为示例。IP 输出代码大部分可以在 `linux/net/ipv4/ip_output.c` 中找到。

在大多数情况下，最后的处理步骤是通过物理接口发送数据包。IP 输出通过检查 `skb` 中的 `dst` 字段来确定应对数据包的操作，以检查数据包是否知道要去哪里。这实际上是检查是否已为此特定包定义了目的硬件地址。

当 IP 协议准备发送数据包时，它通过检查 `skb` 中的 `dst` 字段来检查数据包是否有已知的目的。接下来，`ip_finish_output2` 通过检查目的缓存中的 `hh` 字段来检查目的是否定义了实际的硬件地址。`hh` 字段为 `NULL` 或指向包含包完整 MAC 头的硬件头部缓存。

## IP 输出以及使用邻居缓存和硬件头部缓存发送数据包

此时，根据目的缓存中的值，会发生两种情况之一。首先，我们将看到如果没有到数据包目的地的解析路由会发生什么。如果是这样，`hh` 将是 `NULL`。如果 `hh` 为 `NULL`，我们通过解引用 `skb` 的 `neighbour` 字段来检查邻居缓存，并通过此指针，我们获得该邻居缓存条目的输出函数。在我们的示例中，数据包是一个 IP 包，`neighbour` 之前已初始化为 ARP 协议输出函数之一（`resolve_output` 或 `neighbor_compat_output`）。然而，如果目的地址已经解析且硬件头部缓存是最新的，`output` 将指向函数 `dev_queue_xmit`。根据目的的不同，`neighbor` 中的 `output` 字段将设置为 `neigh_ops` 结构中的指针之一：`output`、`connected_output`、`hh_output` 或 `queue_xmit`。例如，对于该邻居条目，neighbor 中的 `output` 字段被设置为 `hh_output`。

## neigh_ops 结构

上一个示例中使用的 `neigh_ops` 结构定义在 `include/net/neighbour.h` 中

```c
struct neigh_ops {
    void (*destructor)(struct neighbour *);
    void (*solicit)(struct neighbour *, struct sk_buff *);
    void (*error_report)(struct neighbour *, struct sk_buff *);
    int (*output)(struct neighbour *, struct sk_buff *);
    int (*connected_output)(struct neighbour *, struct sk_buff *);
    int (*hh_output)(struct neighbour *, struct sk_buff *);
    int (*queue_xmit)(struct neighbour *, struct sk_buff *);
};
```

如果邻居条目尚未确定，`output` 将指向 `neigh_resolve_output`。邻居缓存中的 NUD 状态用于查看是否需要解析目的地址。这些状态被邻居发现协议（NDP）使用，并列在表 5.4 中。

## 表 5.4 邻居条目 NUD 状态

| 状态 | 值 | 描述 |
| :--- | :--- | :--- |
| `NUD_INCOMPLETE` | `0x01` | 当前正在进行地址解析。 |
| `NUD_REACHABLE` | `0x02` | 表示邻居可达。 |
| `NUD_STALE` | `0x04` | 自确认可达性以来已超过了经过时间。 |
| `NUD_DELAY` | `0x08` | 自确认可达性以来已超过了经过时间。 |
| `NUD_PROBE` | `0x10` | 已发送请求，我们正在等待响应。 |
| `NUD_FAILED` | `0x20` | 表示可达性状态检测失败。 |
| `NUD_NOARP` | `0x40` | 表示不使用 ARP 的伪状态。 |
| `NUD_PERMANENT` | `0x80` | 表示不进行垃圾回收的伪状态。 |
| `NUD_NONE` | `0x00` | 未定义状态。 |

当地址解析后，邻居缓存中的 `nud` 字段将更新指向头部缓存条目，该条目包含实际层目的地址。邻居缓存条目中的 `output` 函数将指向与 `neighbour` 结构中 `neigh_ops` 部分 `queue_xmit` 字段相同的函数。这是因为 `neigh_ops` 之前由 ARP 初始化指向 `dev_queue_xmit` 函数。在任何情况下，如果地址已经解析，`dev_queue_xmit` 就是调用输出数据包的函数。如果目的不可达，数据包将被丢弃。图 5.3 显示了通过目的缓存传输数据包的序列。

如果 `hn` 字段不为 `NULL`，`ip_finish_output` 通过 `hn` 获取链路层头部及其长度。它在 `sk_buff` 头部为链路层头部留出空间并将头部拷贝到包前端。现在数据包已准备好传输。因此，我们调用 `hn_output` 指向的函数，在大多数情况下，它已初始化指向 `dev_queue_xmit` 函数。

# 地址分配、多播及配置的结构与函数

任何 TCP/IP 实现都必须具有用于 IP 多播和多个网络接口地址分配的可配置选项。Linux 也不例外，它通过使用 `in_dev` 结构来实现这一点。该结构还包含了大多数 IPv4 可调参数。如第 4 章所示，`net_dev` 结构的大部分与协议无关的。然而，IPv4 的网络接口地址必须存储在某处，它们存储在 `in_device` 结构中。该结构中的字段可以通过 `sysctl` 或 `setsockopt` 和 `rtlink` 设置。地址信息存储在这里而不是 `net_device` 结构中，是因为地址和 Internet 配置信息必须与设备保持独立。

## in_dev_get 函数

`in_dev` 结构定义在 `linux/include/linux/inetdev.h` 文件中。通过 `in_dev_get` 或该文件中相关函数之一进行访问。

```c
static __inline struct net_device *
in_dev_get(const struct net_device *dev)
{
    struct in_device *in_dev;
    rcu_read_lock();
    in_dev = __in_dev_get_rcu(dev);
    if (in_dev)
        atomic_inc(&in_dev->refcnt);
    rcu_read_unlock();
    return in_dev;
}
```

## in_dev_device 结构

`in_device` 结构包含许多用于管理每个网络接口驱动实例（或实际上每个接口）的多个地址的字段。

```c
struct in_device
{
```

`dev` 是指向引用此 Internet 实例的 `net_device` 结构的指针。

```c
struct net_device *dev;
atomic_t refcnt;
int dead;
```
