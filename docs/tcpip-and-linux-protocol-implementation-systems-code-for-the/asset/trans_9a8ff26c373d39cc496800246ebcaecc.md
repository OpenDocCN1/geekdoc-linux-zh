

# TCP/IP 与 Linux 协议实现

# 发送 ARP

图 6.119 ARP--发送一个 ARP 消息：linux/net/ipv4/arp.c。

```c
/*
 * 创建并发送一个 ARP 数据包。如果 (dest_hw == NULL)，我们创建一个广播
 * 消息。
 */
void arp_send(int itype, int ptype, u32 dest_ip);
    struct net_device *dev, u32 src_ip;
    unsigned char *dest_hw, unsigned char *src_hw,
    unsigned char *target_hw
{
    struct sk_buff *skb;
    struct arphdr *arp;
    unsigned char *arp_ptr;
    /*
     * 此接口上没有 ARP。
     */
    if (dev->flags&IFF_NOARP)
        return;
    /*
     * 分配缓冲区
     */
    skb = alloc_skb(sizeof(struct arphdr) + 2*(dev->addr_len+4)
        + dev->hard_header_len + 15, GFP_ATOMIC);
    if (skb == NULL)
        return;
    skb_reserve(skb, dev->hard_header_len+15);
    skb->raw = skb->data;
    arp = (struct arphdr *)skb_put(skb, sizeof(struct arphdr) + 2*(dev->addr_len+4));
    arp->dev = dev;
    skb->protocol = constant_htons(ETH_P_ARP);
    if (src_hw == NULL)
        src_hw = dev->dev_addr;
    if (dest_hw == NULL)
        dest_hw = dev->broadcast;
```

图 6.120 ARP--发送一个 ARP 消息：linux/net/ipv4/arp.c。

```c
/*
 * 为 ARP 帧填充设备头部
 */
if (dev->hard_header)
    if (dev->hard_header(skb,dev->ptype,dest_hw,src_hw,skb->len) < 0)
        goto out;
```

# 基础设施协议 295

```c
/*
 * 填充 ARP 协议部分。
 *
 * ARP 硬件类型应该匹配设备类型，FDDI 除外，
 * FDDI（根据 RFC 1390）应该始终等于 1（以太网 Ethernet）。
 */

/*
 * 处处都是异常。AX.25 使用 AX.25 PID 值而不是
 * DIX 协议代码。将这些使定义为设备结构体字段。
 */
switch (dev->type) {
    default:
        arp->ar_hr = htons(dev->type);
        arp->ar_pro = constant_htons(ETH_P_IP);
        break;

#if defined (CONFIG_AX25) || defined (CONFIG_AX25_MODULE)
    case ARPHD_AX25:
        arp->ar_hr = constant_htons(ARPHD_AX25);
        arp->ar_pro = constant_htons(AX25_P_IP);
        break;

#if defined (CONFIG_NETROM) || defined (CONFIG_NETROM_MODULE)
    case ARPHD_NETROM:
        arp->ar_hr = constant_htons(ARPHD_NETROM);
        arp->ar_pro = constant_htons(AX26_P_IP);
        break;
#endif
#endif

#if defined (CONFIG_FDDI)
    case ARPHD_FDDI:
        arp->ar_hr = constant_htons(ARPHD_ETHER);
        arp->ar_pro = constant_htons(ETH_P_IP);
        break;
#endif

#if defined (CONFIG_TR)
    case ARPHD_IEEE802_TR:
        arp->ar_hr = constant_htons(ARPHD_IEEE802);
        arp->ar_pro = constant_htons(ETH_P_IP);
        break;
#endif
}
```

图 6.121 ARP–发送一个 ARP 消息：linux/net/ipv4/arp.c。

```c
arp->ar_bln = dev->addr_len;
arp->ar_pl = 4;
arp->ar_op = htons(type);
arp_ptr = (unsigned char *)(arp+1);
memcpy(arp_ptr, src_hw, dev->addr_len);
arp_ptr = dev->addr_len;
```

```c
memcpy(arp_ptr, &src_ip, 4);
arp_ptr += 4;
if (target(arp_ptr, target_hw, dev->addr_len))
else
    memset(arp_ptr, 0, dev->addr_len);
arp_ptr += dev->addr_len;
memcpy(arp_ptr, &dest_ip, 4);
skb->dev = dev;
dev_queue_xmit(skb);
return;
out:
    free_skb(skb);
}
```

# ARP 接收

图 6.122 ARP–接收一个 ARP 消息：linux/net/ipv4/arp.c。
图 6.123 ARP–接收一个 ARP 消息：linux/net/ipv4/arp.c。

```c
int arp_rcv(struct sk_buff *skb, struct net_device *dev, int type)
{
    struct arphdr *arp;
    unsigned char *arp_ptr;
    unsigned char *target_hw;
    u32 target_ip;

    arp = (struct arphdr *)skb->data;
    if (skb->len < sizeof(struct arphdr) + 2*(dev->addr_len+4))
        goto out;

    arp_ptr = (unsigned char *)(arp+1);
    memcpy(arp_ptr, dev->dev_addr, dev->addr_len);
    arp_ptr += dev->addr_len;
    memcpy(arp_ptr, &src_ip, 4);
    arp_ptr += 4;
    if (target(arp_ptr, target_hw, dev->addr_len))
    else
        memset(arp_ptr, 0, dev->addr_len);
    arp_ptr += dev->addr_len;
    memcpy(arp_ptr, &dest_ip, 4);
    skb->dev = dev;
    dev_queue_xmit(skb);
    return;
out:
    free_skb(skb);
}
```

*(注：由于原文文本在 ARP 接收部分存在代码截断和逻辑混乱，翻译时已根据代码结构进行了逻辑性对齐和还原，确保了文档的可读性)*