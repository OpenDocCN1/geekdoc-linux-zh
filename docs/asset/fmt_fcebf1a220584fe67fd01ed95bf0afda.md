
## ARP 请求

### 图 6.115 ARP 请求（谁有）：`linux/net/ipv4/arp.c`。

```c
static void arp_solicit(struct neighbour *neigh, struct sk_buff *skb) {

    u32 saddr;
    u8 *dst_ha = NULL;
    struct net_device *dev = neigh->dev;
    u32 target = (*u32*)neigh->primary_key;
    int probes = atomic_read(&neigh->probes);

    if (skb && int_addr_state(skb->neigh->saddr) == RTN_LOCAL) {
        saddr = skb->neigh->saddr;
    else
        saddr = inet_select_addr(dev, target, RT_SCOPE_LINK);

    if ((probes -= neigh->parms->ucast_probes) < 0) {
        if ((neigh->nud_state&NUD_VALID)) {
            print(KERN_DEBUG "在 INVALID 状态下尝试 uast 探测");
            dst_ha = neigh->ha;
            read_lock(&neigh->lock);
        } else if (probes -= neigh->parms->ucast_probes) < 0) {
            #ifdef CONFIG_ARPP
            neigh_alloc(neigh);
            #endif
            return;
        }
    arp_send(ARP_REQUEST, ETH_ARP, dev, saddr,
            dst_ha, dev->addr, NULL);

    if (dst_ha)
        read_unlock(&neigh->lock);
}
```

### 图 6.116 ARP 内置过期：`linux/net/ipv4/arp.c`。

```c
/* 过期函数 */
/* 在缓存中查找 ARP 映射。如果未找到，发送请求。
 * 这是一个丑陋的例程：它没有使用 skb->dst，
 * 即使它存在。假设 skb->dev 被虚拟设备篡改了。
 只有损坏的设备可以使用此函数，它已被计划移除。
 */
static int arp_set_predefined(int addr_hint, unsigned char *haddr, u32 paddr, struct net_device *dev)

switch (addr_hint) {
    case RTN_LOCAL:
        printk(KERN_DEBUG "ARP: 为自己的地址调用");
        memcpy(haddr, dev->addr, dev->addr_len);
        return 1;
    case RTN_MULTICAST:
        arp_mc_map(paddr, haddr, dev, 1);
        return 1;
    case RTN_BROADCAST:
        memcpy(haddr, dev->broadcast, dev->addr_len);
        return 1;
}
return 0;
int arp_find(unsigned char *haddr, struct sk_buff *skb) {
    struct net_device *dev = skb->dev;
    u32 paddr;
    struct neighbour *neigh;

    if (!skb->dst) {
        printk(KERN_DEBUG "arp_find 被调用时 dst=NULL");
        kfree_skb(skb);
        return 1;
    }
    paddr = ((struct rtable*)skb->dst)->rt_gateway;

    if (arp_preset(inet_addr_type(paddr), haddr, paddr, dev)) {
        return 0;
    }
    n = _neigh_lookup(arp_tbl, paddr, dev, 1);

    if (n) {
        n->used = jiffies;
        if (n->ud_state==NUD_VALID && neigh_event_send(n, skb) == 0) {
            read_lock(n->lock);
            memcpy(haddr, n->dev, n->addr_len);
            read_unlock(n->lock);
            neigh_release(n);
            return 0;
        }
        else
            kfree_skb(skb);
            return 1;
    }
}
/* 过期函数结束 */
```

### 图 6.118 ARP – 将地址绑定到邻居：`linux/net/ipv4/arp.c`。

```c
int arp_bind_neigh(struct dst_entry *dst)
{
struct net_device *dev = dst->dev;
struct neighbour *n = dst->neighbour;
if (dev == NULL) {
return -EINVAL;
}
u32 nexthop=((struct rtable*)dst)->rt_gateway;
if (dev->flags & (IFF_LOOPBACK|IFF_POINTPOINT)) {
nexthop = 0;
n = _neigh_lookup_errno(dev);
#ifndef CONFIG_ATM_ATM
dev->type == ARPHRD_ATM ? &clip_tbl : &arp_tbl, nexthop, dev);
#endif
```

# TCP/IP 与 Linux 协议实现

## 发送 ARP

### 图 6.119 ARP--发送一个 ARP 消息：`linux/net/ipv4/arp.c`。

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
```
