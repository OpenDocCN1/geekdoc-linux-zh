
该函数执行的第一件事是检查输出数据包是否已经存在路由。我们通过检查`sk_buff`中的`dst`字段来实现，该字段指向路由缓存项（route cache entry）。如果没有路由，我们将根据`skb`中的信息（如目的地址、端口和 ToS 值）构建一个流信息结构。然后，我们调用`ip_route_output_flow`来解析路由。一旦获取了路由，我们就构造 IP 报头部，计算 IP 校验和，并调用路由缓存项中`output`字段指向的函数，该字段通常根据路由指向`ip_forward`或`ip_output`。

## 9.14 IP 中的接收包

当数据包到达 IP 时，必须做出几个基本决策。首先，IP 必须决定该数据包是有效的 IP 数据包还是将其丢弃。下一个决策是将数据包转发到接口之外还是发送到内部目的地。如果是发送到另一个接口，IP 必须弄清楚将数据包发送到哪里，是发送到最终目的地还是网关。最后，对于保留的数据包，IP 必须决定下一个由哪个高层协议接收该数据包。第一个决策是基于数据包的基本完整性。第二个决策在第 9.3 节中讨论了 IP 路由机制以及如何根据路由表查找进行转发。在本节中，我们从 IP 数据包进入 IP 接收包处理程序时开始，并跟踪它的处理过程。图 9.1 显示了 IP 接收包处理程序收到的数据包的处理序列。

![](img/c1f701734d482a86a48e8bfd231c6fdb_353_0.png)

图 9.1：接收包序列。

第 6 章第 6.6 节涵盖了如何从输入包队列中移除数据包，以及`NET_RX_SOFTIRQ`任务let如何检查链路类型字段以决定为特定类型调用何种数据包处理程序。对于 IP 协议，数据包类型为`0x0800`。

### 9.14.1 IP 输入函数`ip_rcv`

正如第 9.2 节所述，IP 在其初始化阶段注册了数据包处理函数`ip_rcv`。`ip_rcv`是 IP 协议的主要输入函数，它接收一个封装在`sk_buff`中的传入数据包、指向网络接口`dev`的指针以及一个指向数据包类型的指针。

```
int ip_rcv(struct sk_buff *skb, struct net_device *dev,
    struct packet_type *pt)
{
    首先，我们获取指向 IP 数据包头部的指针 iph；
    struct iphdr *iph;
```

套接缓冲区`skb`的`pkt_type`字段指示数据包的类别。稍后，我们检查此字段以查看数据包是否不是发送给此主机。由于我们目前正在为该主机执行接收例程，如果数据包不是发送给我们的，我们就将其丢弃。这是一个冗余检查。除非是以混杂模式接收到数据包，否则如果它不是为了供我们消费的，它就不会被发送到 IP 接收例程。数据包类型字段的值在第 7 章中。

```
if (skb->pkt_type . PACKET_OTHERHOST)
    goto drop;
IP_INC_STATS_BH(IPInReceives);
if (skb == skb_share_check(skb
```

这是一个检查数据包大小是否至少与 IP 头部大的检查，如果不是，将其丢弃。

```
if (!pskb_may_pull(skb, sizeof(struct iphdr)))
    goto inhdr_error;

iph = skb->nhip;
```

现在我们检查头部校验和，以确认 IP 版本是否为四以及头部长度是否至少为 20 字节。如果不是，我们静默丢弃该数据包 [RFC 1122]。我们检查数据包是否足够容纳头部和任何选项。

```
if (iph->ihl < 5 || iph->version != 4)
    goto inhdr_error;
if (!pskb_may_pull(skb, iph->ihl*4))
    goto inhdr_error;
```

我们获取头部的指针并计算 IP 头部校验和。

```
iph = skb->nhip;
if (ip_fast_csum((u8 *)iph, iph->ihl) != 0)
    goto inhdr_error;
{
    __u32 len = ntohs(iph->tot_len);
    if (skb->len < len || len < (iph->ihl<<2))
        goto inhdr_error;
```

由于网络接口将填充持有数据包的缓冲区末尾，`pskb_trim`将消除填充，使得`skb`的长度等于 IP 头部中的包长度字段。

```
if (skb->len > len) {
    pskb_trim(skb, len);
    if (skb->ip_summed == CHECKSUM_HW)
        skb->ip_summed = CHECKSUM_NONE;
}
```

`ip_rcv_finish`继续输入处理，描述在下一节中。

```
return NF_HOOK(PF_INET, IP_ROUTING, skb, dev),
    ip_rcv_finish());
```

```
inhdr_error:
    IP_INC_STATS_BH(IPInHdrErrors);
drop:
    kfree_skb(skb);
out:
    return NET_RX_OK;
```

### 9.14.2 继续 IP 输入处理`ip_rcv_finish`

`ip_rcv_finish`继续下一节描述的输入处理。定义在`net/ipv4/ip_input.c`中。`ip_rcv_finish`是由`ip_rcv`调用的，用于处理源路由选项。当数据包到达此处时，`ip_rcv_finish`会检查数据包的源路由选项。在目的主机处接收数据包进入 IP 接收例程时，如果数据包不是为了我们消费的，我们需要将其丢弃。这是一个冗余检查。如果是为了源路由的，`ip_rcv_finish`会从数据包中提取 IP 选项。

```
static int ip_rcv_finish(struct sk_buff *skb, struct net_device *dev)
{
    struct iphdr *iph;
    struct ip_options *opt;
    u32 idx;
```

`ip_rcv_finish`检查数据包的源路由选项。如果输入设备未配置源路由，我们认为输入数据包是“火星包”并将其丢弃。否则，我们处理源路由选项。`ip_options_rcv_srr`如果失败将返回选项和错误，数据包将被丢弃。否则，我们像处理普通数据包一样继续。

`dst`字段的值在之前调用`ip_route_input`时已经确定。对于目标为 UDP、TCP 或 IGMP 等任何 IP 族协议的入站数据包，`dst`字段中的输入操作将指向函数`ip_local_deliver`。

```
return dst_input(skb);

inhdr_error:
    IP_INC_STATS_BH(IPInHdrErrors);
drop:
    kfree_skb(skb);
    return NET_RX_DROP;
```

### 9.14.3 将输入数据包交付上层协议

在`ip_rcv_finish`完成入站数据包的处理后如果包用于本地消费且该主机内有一个本地目的地，则数据包将传递给`ip_local_deliver`函数。该函数将决定下一个由哪个高层协议接收数据包。`ip_local_deliver`被传递给`skb`中的输入数据包。

```
int ip_local_deliver(struct sk_buff *skb)
```

会调用`ip_defrag`来重组 IP 分片。重组后的 IP 数据包将通过`skb`返回。

```
if (skb->nh.ip->frag_off & htons(IP_MF|IP_OFFSET)) {
    skb = ip_defrag(skb);
    if (!skb)
        return 0;
}
```

一旦 IP 数据包完成，我们就准备好将数据包交付给上层协议。

```
return NF_HOOK(PF_INET, NF_IP_LOCAL_IN, skb, skb->dev, NULL,
    ip_local_deliver_finish());
```

`ip_local_deliver_finish`函数将输入数据包交付给所有后续接收该包的协议。它决定数据包是发送到单个高层协议还是多个协议。在几种条件下，它可以将数据包分发到多个协议。对于任何混杂模式接收数据包的协议，它必须接收输入数据包的一个副本（实际上是克隆）。如果有一个或多个原始套接字（raw sockets），每个原始套接字将接收输入数据包的克隆。
