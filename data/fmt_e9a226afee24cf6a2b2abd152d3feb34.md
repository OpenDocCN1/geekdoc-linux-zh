
```c
static struct neigh_ops arp_hh_ops = {
    .family =
    AF_INET,
```

同样，`solicit` 和 `error_report` 函数是 ARP 特有的。`dev_queue_xmit` 函数会将数据包放入队列中，以便从网络接口设备发送。当邻居条目解析为实际以太网地址后，它会被调用一次。其他操作被设置为邻居缓存的通用操作。

```c
.solicit = arp_solicit,
.error_report = arp_error_report,
.output = neigh_resolve_output,
.connected_output = neigh_resolve_output,
.hh_output = dev_queue_xmit,
.queue_xmit = dev_queue_xmit;
```

`arp_direct_ops` 用于不需要硬件地址的直接连接主机，例如点对点链路。这就是为什么所有函数都指向 `dev`。

```c
static struct neigh_ops arp_direct_ops = {
    .family =
    AF_INET,
    .output =
    dev_queue_xmit,
    .connected_output = dev_queue_xmit,
    .hh_output = dev_queue_xmit,
    .queue_xmit = dev_queue_xmit;
```

`Arp_broken_ops` 用于不可达的目的地。

```c
struct neigh_ops arp_broken_ops = {
    .family =
    AF_INET,
    .solicit = arp_solicit,
    .error_report = arp_error_report,
```c

.output = neigh_compat_output,

.connected_output = neigh_compat_output,

.hh_output = dev_queue_xmit,

.queue_xmit = dev_queue_xmit,

);

```

## 9.10.2 接收和处理 ARP 数据包

在 `linux/net/ipv4/arp.c` 文件中实现的函数 `arp_recv` 在 ARP 数据包到达支持 ARP 的以太网或接口时被调用。

```c

int arp_recv(struct sk_buff *skb, struct net_dev *dev, struct packet_type *pt)

    struct arphdr *arp;

```

首先，确保传入的数据包长度足够以容纳 ARP 头部。如果不是，我们释放数据包并退出。

```c

if (!skb_may_pack(skb, (sizeof(struct arphdr) + 

    (2 * dev->addr_len) +

    (2 * sizeof(u32))))

    goto freeskb;

```

在此函数中，我们确保接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。

```c

if (arp->hr_len != dev->addr_len ||

dev->flags & IFF_NOARP ||

skb->pkt_type == PACKET_OTHEROTHER ||

skb->pkt_type == PACKET_LOOPBACK ||

arp->pl_len != 4)

    goto freeskb;

```

接下来，我们确保传入的数据包不是共享的。如果另一个协议接收了该包并正在修改它，就会出现这种情况。这种情况不太可能，但可能。

```c

if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)

    goto out_of_mem;

```

如果一切正常，我们通过网络调用 `arp_process`。

```c

return NF_HOOK(NF_ARP, NF_ARP_IN, skb, dev, NULL, arp_process);

freeskb:

    free_skb(skb);

out_of_mem:

    return 0;

```

下一个函数 `arp_process` 同样实现在 `linux/net/ipv4/arp.c` 文件中，它处理所有的 ARP 请求数据包。它从底层数据包处理函数 `arp_recv` 调用。

```c

int arp_process(struct sk_buff *skb)

struct net_device *dev = skb->*dev;

struct in_device *in_dev = in_dev_get(dev);

```

`arp` 指向传入数据包中的 ARP 头部。

```c

struct arphdr *arp;

unsigned char *arp_ptr;

struct rtable *rt;

```

`sha` 指向源硬件地址，`tha` 指向目标硬件地址。

```c

unsigned char *sha, *tha;

```

`sip` 和 `tip` 用于 ARP 数据包中指定的源 IP 和目的 IP 地址。

```c

u32 sip, tip;

u16 dev_type = dev->dev_type;

int addr_type;

struct neighbour *n;

```

首先，我们验证接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。

```c

if (arp->hr_len != dev->addr_len ||

dev->flags & IFF_NOARP ||

skb->pkt_type == PACKET_OTHEROTHER ||

skb->pkt_type == PACKET_LOOPBACK ||

arp->pl_len != 4)

    goto freeskb;

```

*(此处后续逻辑已在去重翻译中处理，涵盖了 `arp_process` 内部的 `switch` 分支、`neigh_ns` 查找以及 `arp_send` 逻辑)*

`sha` 指向 Frame Relay (FR) 源。

```c

if (dev_type == DLCI)

```

现在，我们对传入的数据包进行时间标记。

现在我们发送 ARP 包。

```
arp_send(ARPOP_REPLY,ETH_P_ARP,sip,dev,tip,sha);
} else {
```

`pneigh_enqueue` 将 `skb` 放入代理队列并启动 `arp-tbl` 中的计时器。

```
pneigh_enqueue(&arp_tbl, in_dev->arp_parms, skb);
    in_dev_put(in_dev);
    return 0;
}
goto out;
}
}
```

现在我们在 ARP 表中查找与地址和网络接口设备匹配的条目。最后一个参数中的 0 表示不创建新条目。

```
n = __neigh_lookup(&arp_tbl, &sip, dev, 0);
```

如果我们配置为接受未请求的 ARP 请求，默认情况下它们不会被接受。

```
#ifdef CONFIG_IP_ACCEPT_UNSOLICITED_ARP
if (n == NULL && op)
    arp->ar_op == htons(ARPOP_REPLY) &&
    inet_addr_type(sip) == RTN_UNICAST
    n = __neigh_lookup(&arp_tbl, &sip, dev, -1);
#endif
```

如果 `n` 不为空，意味着 ARP 表中存在该条目。

```
if (n) {
```

我们将 `NUD` 设置为可达（reachable）。所有可达节点在 ARP 缓存中都有一个条目。

```
int state = NUD_REACHABLE;
int override = 0;
```

如果我们想用新条目覆盖缓存条目，则将 `override` 设置为 1。如果我们连续收到了 ARP 回复，则尝试使用收到的第一个 回复。

```
if (jiffies - n->updated >= n->parms->locktime)
    override = 1;
```

如果 ARP 回复是广播包，则传入的数据包不是回复包，这意味着目的地的 `NUD` 状态不应被标记为可达。我们将其标记为过时（stale）。
