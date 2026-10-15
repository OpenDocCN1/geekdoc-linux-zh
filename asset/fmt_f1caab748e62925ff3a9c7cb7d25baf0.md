
IPv6 重分实现在 `linux/net/ipv6/reassembly.c` 文件中。维护一个输入分片队列。此外，队列中的每个条目关联有一个定时器。如果孤立分片在队列中停留超过合理寿命，它们将被老化并丢弃。

由于 IPv6 分片位于主头之后的可选头中，我们实际上在 `AF_INET6` 族中注册一个协议来处理分片头。该协议类似于传输协议，因为它的处理器是在 IP 头部字段遇到协议号 `IPPROTO_FRAGMENT` 时分发的。这里展示了与 `AF_INET6` 族注册分片协议处理函数的结构。

```c
static struct inet6_protocol frag_protocol = {
    .handler = ipv6_frag_rcv,
    .flags = INET6_PROTO_NOPICY,
};
```

分片协议由 `ipv6_frag_init` 初始化。

```c
void __init ipv6_frag_init(void);
```

```c
if (inet6_add_protocol(&frag_protocol, IPPROTO_FRAGMENT) < 0)
    printk(KERN_ERR "ipv6_frag_init: Could not register protocol\n");
```

分片接收处理器 `ipv6_frag_rcv` 位于同一文件中，当在 IPv6 数据包头部字段遇到 `IPPROTO_FRAGMENT` 时执行。

```c
static int ipv6_frag_rcv(struct sk_buff **skbuff, unsigned int *nhoffp)
```

在检查分片头的有效性后，我们尝试在现有队列中查找具有相同标识值的分片。

```c
if ((fq = fq_find(hdr->identification, &hdr->saddr, &hdr->daddr)) != NULL) {
    int ret = -EINOMEM;

    spin_lock(&fq->lock);
```

如果无法找到匹配的分片，我们将新的分片加入队列。

```c
ipv6_frag_queue(fq, skb, fhdr, *nhoffp);
```

然后我们调用 `ipv6_frag_reasm` 尝试将分片组合在一起。

```c
if (fq->last_in == (FIRST_IN|LAST_IN) && fq->q == fq->len)
    ret = ipv6_frag_reasm(fq, skbp, nhoffp, dev);

    spin_unlock(&fq->lock);
    fq_put(fq);
    return ret;
```

# 11.8 IPv6 输出

IPv6 中的 IP 处理与 IPv4 非常相似。一旦数据包准备好发送，目的缓存条目的 `output` 字段将指向 `ipv6_output` 函数，该函数位于 `linux/net/ipv6/ipv_output.c`。

```c
int ipv6_output(struct sk_buff *skb)
{
```

正如我们看到的，这个函数的作用仅仅是决定是否对数据包进行分片。这一确定通过检查目的缓存条目 `dst` 中的 MTU 值来完成。

```c
if ((skb)->dst_mtu(skb) || skb_shinfo(skb)->frag_list)
  return ip6_fragment(skb, ip6_output2);
else
  return ip6_output2(skb);
}
```

同一文件中的 `ip6_output2` 继续对输出数据包进行处理。

```c
int ip6_output2(struct sk_buff *skb);
```

它做的并多只是检查目标地址是否为组播地址。如果是组播地址，则对 `skb` 进行克隆并将一个副本发送到回环地址。在编写时，Linux IPv6 并不支持实际的路由。在该函数退出之前，它调用了同一文件中的 `ip6_output_finish` 来完成输出数据包的处理。

`ip6_output_finish` 完成了输出数据包的处理。

```c
static inline int ip6_output_finish(struct sk_buff *skb)
{
  struct dst_entry *dst = skb->dst;
  struct hh_cache *hh = dst->hh;
```

在此时，我们所的操作与 IPv4 输出处理非常相似。我们现在可以看到 Linux TCP/IP 中的邻居系统是如何考虑到 IPv6 设计的。如果定义了硬件缓存，我们调用 `hh_output_packets`，它会将数据包入队到接口设备。如果没有定义，我们则调用目标缓存 `dst` 中为该邻居定义的函数。

```c
if (hh) {
  int hh_alen;

  read_lock_bh(hh->hh_lock);
  hh_alen = skb->data - HH_DATA_ALIGN(hh->hh_len);
  memcpy(skb->data, hh->hh_data, hh_alen);
  read_unlock_bh(hh->hh_lock);
  skb_push(skb, hh->hh_len);
  return hh->hh_output(skb);
} else if (dst->neighbour)
  return dst->neighbour->output(skb);
free_skb(skb);
return -EINVAL;
```

## 11.9 IPv6 输入

如前所示，我们注册了一个特定函数作为 IPv6 数据包的处理器，当网络接口设备接收到类型为 `ETH_P_IPV6` 的数据包时，该处理器会被调用。由于 IPv6 头部格式更简单，此函数在许多方面比其 IPv4 等效函数更简单。IPv6 头部头部与 IPv4 不同，所有的 IPv6 选项都在独立的头部中。包处理函数 `ipv6_rcv` 定义在 `linux/net/ipv6/ipv6_input.c` 文件中，并在软中断上下文中（即数据包排队层中的“下半部”）被调用。

```c
int ipv6_rcv(struct sk_buff *skb, struct net_device *dev, struct packet_type *pt) {
struct ipv6hdr *hdr;
u32 pkt_len;
if (skb->pkt_type == PACKET_OTHERHOST) {
	goto drop;
	ip6_INC_STATS_BH(IPv6InReceives);
	if ((skb = skb_share_check(skb, GFP_ATOMIC)) == NULL) {
	ip6_INC_STATS_BH(IPv6InDiscards);
	goto out;
	}
}
```

在这里，我们使用网络接口设备的索引。一旦数据包入队，我们就不再引用实际的网络接口设备。

```c
((struct inet6_skb_param *)skb->cb)->iif = dev->ifindex;
```

我们必须检查以确保传入的数据包至少足够长以容纳 IPv6 头部。

```c
if (skb->len < sizeof(struct ipv6hdr)) {
	goto err;
}
if (!(pskb_may_pull(skb, sizeof(struct ipv6hdr))) {
	goto drop;
}
hdr = skb->nh.ipv6h;
```

我们检查以确保版本字段为 6 以表示 IPv6。

```c
if (hdr->version != 6) {
	goto err;
}
```

我们直接从数据包头部获取负载长度。如果存在可选头部，负载包含了这些头部的长度。

```c
pkt_len = ntohs(hdr->payload_len);
```

如果我们的输入数据包是一个畸形（jambogram），负载长度可能为零。

```c
if (pkt_len || hdr->nethdr != NEXTHDR_HOP) {
	if (pkt_len + sizeof(struct ipv6hdr) < skb->len) {
		goto truncated;
	}
	if (!pskb_trim(skb, pkt_len + sizeof(struct ipv6hdr))) {
		goto drop;
	}
	hdr = skb->nh.ipv6h;
}
if (skb->ip_summed == CHECKSUM_HW) {
	skb->ip_summed = CHECKSUM_NONE;
}
}
```

如果下一个头部是逐跳头部（hop-by-hop），我们调用 `ipv6_parse_hoptops` 从传入的数据包中提取跳跳选项。跳跳选项被存回套缓冲区 `skb` 中。
