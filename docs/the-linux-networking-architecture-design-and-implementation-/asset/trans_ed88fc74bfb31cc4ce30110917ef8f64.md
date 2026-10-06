
## 14.2 实现互联网协议

IP 数据报到达后会被存储在分片缓存中，直到所有分片的等待时间（IP_FRAG_TIME）过期或 IP 数据报的所有分片都已到达。

```
ip_find()
```

ip_find(iph) 在分片缓存中查找带有 `iph` 数据包包头的 IP 数据报的 ipq 条目。为此，使用 `ipqhashfn()` 根据数据包包头字段中的发送者地址、目的地址、协议 ID 和分片 IP 来计算该条目的哈希值。基于这些参数，可以区分不同的数据报，并将入站的分片分配给每个数据报。多个具有相同哈希值的 ipq 结构冲突通过双向链表进行线性解决（见图 14–7）。如果 `ip_find()` 无法为 IP 分片找到匹配的条目，则在分片缓存创建一个新的 ipq 条目（ip_frag_create()）。

```
ip_frag_queue()
```

ip_frag_queue(qp, skb) 将新到达的分片按顺序放入分片队列（由 ipq 结构表示）中。该函数检查数据报是否完整，完整则意味着新分片是重复的。如果不是如此，则根据 IP 包包头中的分片偏移（Fragment Offset）参数计算该分片在原始 IP 数据报中的位置（偏移和长度）。随后，使用 MF 标志来检查这是否是数据报的最后一个分片（设置 LAST_IN）。

随后，在接收到的分片列表（qp->fragments）中搜索正确的位置，并将套接缓冲区（socket buffer）放置在该位置。数据报 ipq 结构中的 `meat` 参数增加与所添加分片对应的长度。如前所述，`length` 参数指定了接收到的分片 IP 数据报的字节数。

```
ip_frag_reasm()
```

此函数由 ip_defrag() 调用；它重组数据包的所有分片（qp->len == qp->meat），并将其重组为单一的 IP 数据报。首先，创建一个具有 `qp->len` 预留空间的新套接缓冲区，并初始化 IP 数据报头。将每个分片的 IP 载荷拷贝到新套接缓冲区的头部。

```
ip_defrag()
```

ip_defrag(skb) 方法在 ip_local_deliver() 中为每个分片被调用。如第 14.2.1 节所述，要交付到本地机器的数据包会走这条互联网协议路径（即分片 IP 数据报在目标机器上进行重组）。

这里首先检查分片缓存中是否有足够的缓冲区空间来存放新分片。如果不是，则 ip_evictor() 将移除条目，直到达到低阈值 `sysctl_ipfrag_low_thresh`。随后，ip_find() 在分片缓存中查找相关条目。如前所述，一旦 IP 数据报的第一个分片到达，就会创建一个新的 ipq 结构。

最后，ip_queue() 将新分片添加到已存在的分片列表中。当 IP 数据报的所有分片都已到达（可以通过 `pq->len == pq->next->reassembly` 检查）时，ip_frag_reasm() 返回。

## 14.2 IP 实例的数据

IP 实例（在路由器中）的主要任务是转发 IP 包。为此，必须为该 IP 实例配置若干网络设备。这些供互联网协议使用的网络设备（INET 设备）主要由存储 `net/ipv4/dev.c` 文件中的函数管理。在后续讨论中，我们将这些网络设备称为 IP 网络设备。

本节旨在要介绍 IP 网络设备管理的结构。这一点代表了互联网协议多个函数之间的绑定成员。例如，下文介绍结构可用于管理 IP 实例的 IP 地址和网络设备，以及激活的多播组或不同的 IP 配置参数（是否允许包转发？是否接受重定向包？等）。

`in_device` 数据结构代表了网络设备管理的起点：

```
struct in_device include/linux/inetdevice.h
```

为每个配置了互联网协议的网络设备创建一个 `in_device` 结构。该结构管理此 IP 网络设备的配置数据。图 14-8 显示，IP 网络设备的 `net_device` 结构各有一个 `ip_ptr_param`，指向相关的 `in_device` 结构。IP 网络设备没有显式列表，通过 `dev_base` 访问列表。

`net/ipv4/dev.c` 文件包含了管理 IP 网络设备的函数，包括初始化 IP 网络设备的 `inetdev_init()`。

`in_device` 结构的结构和元素如下：

```
struct in_device {
    struct net_device               *dev;
    atomic_t refcnt;
    rwlock_t lock;
    int flags;
    struct in_ifaddr              /* ifaddr_list; /* IP ifaddr 链 */
    struct ip_mc_list *mc_list; /* IP 多播过滤链 */
    unsigned long neigh_v1 seen;
    struct neigh *arp_parms;
    struct ipv4_dev conf;
};
```

![](img/5a25b942ec3329b8799f2b564)
图 14-8 管理 IP 设备及其参数的结构结构。

- `dev` 指向配置了互联网协议的网络设备的 `net_device` 结构。
- `refcnt` 存储对该结构的引用计数，即网络设备使用的实例数量。`refcnt` 本质上通过 `dev_get()` 和 `dev_put()` 函数进行更改。
- `lock` 用于防止由于对设备结构进行并行操作导致的错误。
- `dead` 显示 IP 设备是否仍然有效。
- `ifa_list` 指向 `in_ifaddr` 结构列表，存储该网络设备的 IP 地址。除了 IP 地址 (`ifa_address`) 外，`in_ifaddr` 结构还存储了其他参数（例如子网掩码 (`ifa_mask`)、广播地址 (`ifa_broadcast`)）。`in_ifaddr` 结构的内容如下：

```
struct in_ifaddr {
    struct in_ifaddr *ifa_next;
    struct in_device  *ifa_dev;
    u32               ifa_local;
    u32               ifa_address;
    u32               ifa_mask;
    u32               ifa_broadcast;
    u32               ifa_anycast;
    unsigned char ifa_scope;
    unsigned char ifa_flags;
    unsigned char ifa_preflen;
    char ifa_label[IFNAMSIZ];
};
```

- `mc_list` 是 `ip_mc_list` 结构列表。列表中的每个元素存储了 IP 实例当前订阅的 IP 多播组的信息，并通过当前网络设备接收。
- `mr_v1_seen` 由 IGMP 使用（见第 17.3 节）。
- `arp_parms` 指向 `neigh_parms` 类型的结构，存储了 ARP 协议最重要的参数。（见第 15 章。）
- `cnf` 指向 `ipv4_devconf` 结构，存储了 IP 实例的重要设置。`ipv4_devconf` 描述见下文。

```struct
struct ipv4_devconf include/linux/inetdev.h
```

`ipv4_devconf` 数据结构可用于激活或停用 IP 网络设备上 IP 实例的各种属性。为此，`/proc/sys/net/ipv4/conf` 包含每个 IP 网络设备的子目录，可以在其中设置下文提到的属性。这些属性将简要描述。附录 B 讨论了互联网协议的所有 proc 条目。
