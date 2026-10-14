
在此处，取决于目标缓存中 `hh` 字段的值，可能会发生两种情况。首先，我们将看到如果没有解析到数据包的目的会发生什么，即如果 `hh` 为 `NULL`。如果 `hh` 为 `NULL`，接下来我们通过解引用 `skb` 的 `neighbor` 字段来检查邻居缓存，通过此获取邻居缓存条目的输出函数。在我们的示例中，数据包是 IP 包，`neighbour` 之前初始化为指向 ARP 协议输出函数之一（`neigh_resolve_output` 或 `neigh_count_output`）。然而，如果地址已经解析且硬件头部缓存是最新的，`output` 将指向函数 `dev_queue_xmit`。根据目标，`neighbour` 中的 `output` 字段将设置为 `neigh_ops` 中 `struct output`、`connected_output`、`hh_output` 或 `queue_xmit` 的函数之一。如果网络接口是以太网设备，在 ARP 协议初始化阶段，`ops` 被设置为 `arp_hh_ops`。`ops` 字段定义了邻居缓存条目的行为。下面的代码片段显示了 `ops` 字段。如果此邻居缓存条目对应可达节点，邻居缓存条目中的 `output` 字段被设置为指向 `ops->hh_output`。

上一个示例使用的 `neigh_ops` 结构定义在 `linux/include/neighbour.h` 中。

```c
struct neigh_ops {
    int;
    void (*destructor)(struct neighbour *);
    void (*solicit)(struct neighbour *, struct sk_buff*);
};
```

```c
void      (*error_report)(struct neighbour *, struct sk_buff);
int      (*output)(struct sk_buff*);
int      (*connected_output)(struct sk_buff*);
int      (*hh_output)(struct sk_buff*);
int      (*queue_xmit)(struct sk_buff*);
;
```

如果下一个目标已知，但其邻居的物理地址尚未确定，则 `output` 将指向 `neigh_resolve_output`。`neigh_resolve_output` 函数检查邻居缓存的条目状态以确保它是可用的。NUD 状态存储在邻居缓存的 `nud_state` 字段中。这些状态用于判断是否需要解析目标地址。NUD 状态由邻居发现协议（NDP）[RFC 2641] 使用，并列于表 6.4。

一旦地址解析，邻居缓存中的 `hh` 字段将更新指向硬件头部缓存条目，该条目包含实际的链路层目的地址。邻居缓存条目中的输出函数将更新为指向与邻居结构中 `neigh_ops` 部分相同的 `queue_xmit` 函数。这是因为之前由 ARP 初始化为指向 `dev_queue_xmit` 函数。在任何情况下，如果地址已经解析，`dev_queue_xmit` 就是调用来输出数据包的函数。如果目标不可达，数据包将被丢弃。图 6.3 显示了通过目标缓存传输数据包的序列。

![](img/c1f701734d482a86a48e8bfd231c6fdb_178_0.png)

图 6.3：目标缓存传输序列。

如果 `hh` 字段为 NULL，`IP_finish_output2` 通过 `hh` 获取链路层头部和长度。它在 `sk_buff` 头部为链路层头部留出空间并将头部拷贝到数据包前端。现在数据包已准备好传输。因此，我们调用 `hh_output` 指向的函数，在大多数情况下，它已被初始化为指向 `dev_queue_xmit` 函数。

## 6.9 用于 IPv4 地址分配、多播和配置的 In_device 结构

任何 TCP/IP 实现都具有 IP 多播和多个网络接口地址分配的可配置选项。该结构还包含大多数 IPv4 可调参数。如第 4 章所示，`net_device` 结构的大部分与协议无关。然而，IPv4 的网络接口地址必须存储在处，它们存储在 `in_device` 结构中。可以通过 `sysctl`、`setsockopt` 和 `rtnetlink` 在此结构中设置字段。地址信息在此保留而非 `net_device` 结构是为了确保地址和 Internet 配置与设备独立。

`in_device` 结构定义在文件 `linux/include/linux/netdevice.h` 中。通过文件中的 `in_dev_get` 内联函数访问。

```c
struct in_device *in_dev_get(const struct net_device *dev)
```

此处显示 `in_device` 结构。

```c
struct in_device
{
    struct net_device *dev;
    atomic_t refcnt;
    rwlock_t lock;
    int dead;
```

`dev` 是一个指向引用此 Internet 设备实例的 `net_device` 结构的指针。

这是我们将 IP 地址分配到接口的地方。由于支持多个地址，`ifa_list` 被实现为链表。`mc_list` 持有该设备的多播地址列表。这些多播地址由第 9 章 9.8 节涵盖的 IGMP 协议管理。`mr_v1_seen` 用于 IGMP 协议以指示传入的 IGMP 数据包。

```c
struct if_addr *ifa_list;
struct ip_mc_list *mc_list;
rwlock_t mc_lock;
struct ip_mc_list *mc_tomb;
unsigned long mr_v1_seen;
unsigned long mr_v2_seen;
unsigned long mr_maxdelay;
unsigned char mr_grv;
unsigned char mr_gq_running;
unsigned char mr_ifc_count;
```

下一个字段是通用查询定时器。

```c
struct timer_list mr_gq_timer;
```

该字段 `mr_ifc_timer` 是接口更改。

```c
struct timer_list mr_ifc_timer;
struct neigh_parms *arp_parms;
struct ipv4_devconf cnf;
```

`ipv4_devconf` 结构定义在文件 `linux/include/linux/device.h` 中。它位于 `in_device` 结构的 `cnf` 字段中。它包含了 IPv4 配置值，表 6.5 列出的配置项。

```c
struct ipv4_devconf {
    int accept_redirects;
    int send_redirects;
    int secure_redirects;
    int shared_media;
    int accept_source_route;
    int rp_filter;
    int proxy_arg;
    int bootp_relay;
    int log_martians;
    int forwarding;
    int mc_forwarding;
    int tag;
    int arp_filter;
    int medium_id;
    int no_xfrm;
    int no_policy;
    void *sysctl;
};
```

| Name | Value | Purpose |
| :--- | :--- | :--- |
| accept_redirects | 1 | 接受重定向。 |
| send_redirects | 2 | 发送重定向。 |
| secure_redirects | 3 | 安全重定向。 |
| shared_media | 4 | 共享媒体。 |
| accept_source_route | 5 | 接受源路由。 |
| rp_filter | 6 | 反向路径过滤。 |
| proxy_arg | 7 | 代理 ARP。 |
| bootp_relay | 8 | Bootp 中继。 |
| log_martians | 9 | 记录异常地址。 |
| forwarding | 10 | 转发。 |
| mc_forwarding | 11 | 多播转发。 |
| tag | 12 | 标签。 |
| arp_filter | 13 | ARP 过滤。 |
| medium_id | 14 | 介质 ID。 |
| no_xfrm | 15 | 无 XFRM。 |
| no_policy | 16 | 无策略。 |
| Name | Value | Purpose |
