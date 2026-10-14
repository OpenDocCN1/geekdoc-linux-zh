
# 基础设施协议 253

```c
FRAG_CB(next)->offset += i;

skb_pull(next, i);

qp->me -= i;

if (next->ip_summed != CHECKUM_UNNECESSARY)
    next->ip_summed = CHECKUM_NONE;
break;
} else {
```

```c
struct sk_buff *free_it = next;

/* 旧分片被新分片完全覆盖
 * 丢弃它；
*/

next = next->next;

if (prev)
    prev->next = next;
else
    qp->fragments = next;

qp->meat = free_it->len;
frag_kfree_skb(free_it);
}
}
```

图 6.59 分片–加入队列：`linux/net/ipv4/ip_fragment.c`

```c
FRAG_CB(skb)->offset = offset;
/* 将此分片插入分片链中。 */
skb->next = next;
if (prev)
    prev->next = skb;
else
    qp->fragments = skb;
if (skb->dev)
    qp->dev->ifindex = skb->dev->ifindex;
skb->meat = skb->len;
atomic_add(skb->truesize, ip_frag_mem);
if (offset == 0)
    qp->last_in |= FIRST_IN;
return;

err:
kfree_skb(skb);
}
```

# 重组

分片的逆过程是重组。这并不是严格的逆过程，因为分片可以在任何时间发生，并且在路由的许多跳数中，只要输出链路的 MTU 小于输入链路的 MTU，就会发生分片。然而，重组只在接收端完成。重组的复杂部分在于它需要一个定时器（IP 层唯一的定时器），以处理分片的丢失或乱序交付（以及丢弃永远无法完成的分片）。254 TCP/IP 与 Linux 协议实现

图 6.60 分片–将分片合并：`linux/net/ipv4/ip_fragment.c`。

```c
/ 从所有分片构建一个新的 IP 数据报。
*
FIXME: 我们在这里拷贝是因为缺乏有效的
输入位。在处理新的 skb 数据之前，我
* 不会触碰这个。
*/
static struct sk_buff *ip_frag_reasm(struct ipv4 *qp, struct net_device *dev)
{     struct skb_buff *skb;
    struct iphdr *iph;
    struct skb_buff *fp, *head = qp->fragments;
    int len;
    int ihlen;

    if (head != NULL) {
        FRAG_CB(head)->offset = 0;

    /* 为数据报分配一个新的缓冲区。 */
    ihlen = head->nh->ihl * 4;
    len = ihlen + qp->len;

    if (len > 65536)
        goto out_oversize;

    skb = dev_alloc_skb(len);
    if (!skb)
        goto out_mem;
```

图 6.61 分片–将分片合并：`linux/net/ipv4/ip_fragment.c`。

```c
/ 填充基础细节。 */
skb->mac_raw = skb->data;
skb->nh->raw = skb->data;
FRAG_CB(skb)->h = FRAG_CB(head)->h;
skb->ip_summed = head->ip_summed;
skb->cksum = 0;
/ 将原始 IP 头部拷贝到新的缓冲区。 */
memcpy(skb_put(skb, ihlen), head->nh->iph, ihlen);
/ 将所有分片的数据拷贝到新的缓冲区。 */
for (fp=head; fp = fp->next) {
    memcpy(skb_put(skb, fp->len), fp->len);
    if (skb->ip_summed != fp->ip_summed)
        skb->ip_summed = CHECUM_NONE;
```

# 基础设施协议 255

```c
else if (skb->ip_summed == CHECUM_HW)
skb->csum = csum_add(skb->csum, fp->csum);
}
skb->dst = dst_clone(head->dst);
skb->pkt_type = head->pkt_type;
skb->protocol = head->protocol;
skb->dev = dev;
```

图 6.62 分片–将分片合并：`linux/net/ipv4/ip_fragment.c`。

```c
/*
* 显然错误，在合并之前
* 每个分片的标记应该已经经过了一致性检查，
* 在 ip_glue() 调用之前可能已经进行了分片的合并。
* 如果我们不进行一致性检查，可能还会
* 取与第一个分片关联的值。
*/
nskb->security = head->security;
```

```c
/* 连接与分片相同（如果有的话）。 */
skb->nfct = head->nfct;
nf_counterrack_get(skb->nfct);
#ifdef CONFIG_NETFILTER_DEBUG
skb->nf_debug = head->nf_debug;
#endif
```

```c
/* 完成所有分片。修复新的 IP 头部。 */
ip->frag = skb->nh->ip;
ip->frag_off = 0;
ip->tot_len = htons(ip->tot_len);
IP_INC_STATS_BH(IpReasmDK);
return skb;
out_mem:
NETDEBUG(printk(KERN_ERR, "IP: queue_glue: 合并队列 %p 无内存\n",
		qp));
goto out_fail;
out_oversize:
if (net_ratelimit(KERN_INFO))
    printk(KERN_INFO, "来自 %d.%d.%d.%d 的超大 IP 包\n",
			NIPQUADAD(qp->saddr));
out_fail:
IP_INC_STATS_BH(IpReasmFails);
return NULL;
```

图 6.63 分片–处理分片的到达：`linux/net/ipv4/ip_fragment.c`。

```c
/* 处理传入的 IP 数据报分片。 */
struct sk_buff *skb = deffrag(struct sk_buff *skb)
{
    struct iphdr *iph = skb->nh->ip;
    struct ipq *qp;
    struct net_device *dev;
    IP_INC_STATS_BH(IpReasm);
    /* 从清理内存。 */
```
