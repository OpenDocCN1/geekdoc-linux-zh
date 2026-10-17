
```c
if (arp->ar_op != htons(ARPOP_REPLY) ||

nskb->pkt_type != PACKET_HOST)
```

`state = NUD_STALE;`

```
最后，我们调用 update 来更新邻居缓存条目。Neigh_release 减少了邻居缓存条目中的引用计数，因为我们不再对该条目进行操作。
```

`neigh_update(n, sha, state, override, l);`

`neigh_release(n);`

```
}
```

```
out:
if (in_dev)
  in_dev_put(in_dev);
  kfree_skb(skb);
  return 0;
}
```

# 9.11 网际控制消息协议 (ICMP)

ICMP 协议处理 IPv4 的许多控制功能。该协议通常被认为是 IP 的一部分，ICMP 消息载在 IP 包内部。有许多不同类型的 ICMP 包，每种类型都需要不同的操作。Linux ICMP 使用一个数组根据输入数据包类型来分发控制函数。该数组 `icmp_control` 定义在 `linux/net/ipv4/icmp.c` 文件中。

```
struct icmp_control {
```

许多 ICMP 包需要对数据包进行递增。该结构包含一个指向输出时递增的统计计数器的偏移量，以及一个类似的输入偏移量。

```
int output_off;
int input_off;
```

`Handler` 指向一个处理此特定消息类型的函数。下一个字段 `error` 在此特定消息为错误消息时，其值被设置为 1。

```
void (*handler)(struct sk_buff *skb);
short error;
```

表 9.8 列出了在 `linux/include/linux/icmp.h` 文件中定义的 ICMP 消息类型。

| 消息 | 值 处理器 | 输出计数器 | 输入计数器 |
| :--- | :--- | :--- | :--- |
| ICMP_ECHOREPLY | A00 | icmp_discard | IcmpEchoReps | IcmpInEchoReps |
| ICMP_DEST_REACH | A03 | icmp_unreach | IcmpOutreaches | IcmpInDestreaches |
| ICMP_SOURCE_QUENCH | A04 | icmp_unreach | IcmpOutQuenches | IcmpInQuenches |
| ICMP_REDIRECT | A05 | icmp_redirect | IcmpOutRedirects | IcmpInRedirects |
| ICMP_ECHO | A08 | icmp_echo | IcmpOutEchos | IcmpInEchos |
| ICMP_TIME_EXEDED | 11 | icmp_unreach | IcmpOutTimecds | IcmpInTimecds |
| ICMP_PARAMETER | 12 | icmp_unreach | IcmpOutParmbs | IcmpInParmbs |
| ICMP_TIMESTAMP | 13 | icmp_timestamp | IcmpOutTimestamps | IcmpInTimestamps |
| ICMP_TIMESTAMPLY | 14 | icmp_discard | IcmpOutTimestampReps | IcmpInTimamps |
| ICMP_INFO_REQUEST | 15 | icmp_discard | dummy | dummy |
| ICMP_INFO_REPLY | 16 | icmp_discard | dummy | dummy |
| ICMP_ADDRESS | 17 | icmp_address | IcmpOutMasks | IcmpInMasks |
| ICMP_ADDRESSREPLY | 18 | icmp_address_reply | IcmpOutAddrReps | IcmpInAddrReps |

# 9.1.1 ICMP 包处理

当 `AF_INET` 族初始化时，`linux/ipv4/af_inet.c` 中的函数调用 `inet_add` 将 ICMP 添加到 IP 后接收 IPv4 包的协议列表中。在 `linux/net/ipv4/icmp.c` 中定义的 `icmp_rcv` 处理器函数的主要目的是分发表 9.8 所示的所有 ICMP 消息类型。在剥离 IPv4 头后接收所有 ICMP 包。

```
int icmp_rcv(struct sk_buff *skb)
```

`icmp` 指向传入数据包中的 ICMP 头。`Rt` 是路由缓存条目。

```
struct icmphdr *icmp;
struct rtable *rt = (struct rtable *)skb->dst;
ICMP_INC_STATS_BH(IcmpInMsgs);
```

在这里，我们进行一些基础的有效性检查。首先，检查校验和是否正确。

```
switch (skb->checksum) {
  case CHECKSUM_HW:
    if ((u16)csum_fold(skb))
      break;
    if (net_ratimit())
      printk(KERNEL_DEBUG "icmp4 hw sum\n");
  case CHECKSUM_NONE:
    if ((u16)csum_fold(skb, 0, skb->len, 0))
      goto error;
```

现在，我们检查包长度至少与 ICMP 头一样。

```
if (!pskb_pull(skb, sizeof(struct icmphdr))
    goto error;
```

如果数据包是 ICMP，我们将将其设置为包中的 ICMP 头。

```
icmp = skb->data;
```

现在，我们检查是否收到了非 ICMP 包类型。如果是，则静默丢弃它 [RFC 122]。

```
if (icmp->type > NR_ICMP_TYPES)
    goto error;
if (rt->rt_flags & (RTF_BROADCAST | RTF_MULTICAST)) {
```

发送到广播的 ICMP echo 可能会被静默忽略 [RFC 122]。Linux 提供了一个 `sysctl` 变量来产生这种行为。

```
if (icmp->type == ICMP_ECHO &&
    sysctl_icmp_echo_broadcasts) {
    goto error;
if (icmp->type != ICMP_ECHO &&
    icmp->type != ICMP_TIMESTAMP &&
    icmp->type != ICMP_ADDRESS &&
    icmp->type != ICMP_ADDRESSREPLY) {
    goto error;
}
```

现在，我们准备好根据 ICMP 消息类型分发表 9.8 列出的控制函数之一。

```
ICMP_INC_STATS_BH(icmp_pointers[icmp->type].input_off);
icmp_pointers[icmp->type].handler(skb);
```

最后，我们完成了。

```
drop:
    kfree_skb(skb);
    return 0;
error:
    ICMP_INC_STATS_BH(IcmpInErrors);
    goto drop;
}
```

我们检查的下一个函数是 `icmp_unreach`，它处理各种类型的不可达包。

```
static void icmp_unreach(struct sk_buff *skb)
```

```
if (icmp->type == ICMP_DEST_REACH) {
```

我们解码 ICMP 头中的字段以查看这是哪种类型的不可达包。少数代码需要特殊处理。

```
switch (icmp->code & 15) {
case ICMP_NET_UNREACH:
case ICMP_HOST_UNREACH:
case ICMP_PROT_UNREACH:
case ICMP_PORT_UNREACH:
    break;
case ICMP_FRAG_NEEDED:
```

如果我们收到分片需要，调用 `ip_rt_needed` 来处理分片请求。这种 ICMP 类型用于 MTU 发现。如果我们收到 `ICMP_FRAG_NEEDED` 包，意味着我们需要通过 IP 分片减小包的大小。

```
if (ipv4_config.pmtu_disc) {
```

如果我们没有配置 MTU 发现，我们会在错误中接收此类包类型。
