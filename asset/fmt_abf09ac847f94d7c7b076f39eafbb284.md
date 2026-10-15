
图 6.235 IPMR-处理待转发的多播数据包：`linux/net/ipv4/ipmr.c`。

```c
1298  /*
1299      用于转发的多播数据包到达此处
1300  */
1301  int ipmr_r_input(struct sk_buff *skb)
1303  {
1304      struct mfc_cache *cache;
1305      int local = ((struct rtable*)skb->dst)->rt_flags&RTCTF_LOCAL;
1308      /* 数据包在转发后被回环，不应再次
1309          转发，但仍可以在本地进行交付。
1310      */
1311      if (IPCB(skb)->flags&IPSKB_FORWARDED)
1312          goto dont_forward;
```

# 基础设施协议 373

```c
if (!local) {
    if (IPCB(skb)->opt.router_alert) {
        if (ip_call_chain(skb)) {
            return 0;
        }
    } else if (skb->nh->protocol == PROTO_IGMP) {
        /* IGMP1 和损坏的 IGMPv2 实现在
           Cisco IOS < 11.2(8) 中不会向指向可路由
           组的 IGMP 数据包中放置路由器告警
           选项。这非常糟糕，因为这意味着
           我们无法转发任何 IGMP 消息。
        */
        read_lock(&mrt_lock);
        if (mroute(mroute_socket, skb)) {
            read_unlock(&mrt_lock);
            return 0;
        }
        read_unlock(&mrt_lock);
    }
}
```

**图 6.236** IPMR—处理待转发的多播数据包：`linux/net/ipv4/ipmr.c`

```c
read_lock(&mrt_lock);
cache = ipmr_cache_find(skb->nh->ip->saddr, skb->nh->ip->daddr);

/*
    没有可用的缓存项
*/
if (cache==NULL) {
    int vif;
    if (local) {
        struct skb *skb2 = skb_clone(skb, GFP_ATOMIC);
        ip_local_deliver(skb);
        if (skb2 == NULL) {
            read_unlock(&mrt_lock);
            return -ENOFS;
        }
        skb = skb2;
    }
    vif = ipmr_cache_find(skb->dev);
    if (vif > 0) {
        int err = ipmr_cache_un(vif, skb);
        read_unlock(&mrt_lock);
        return err;
    }
    read_unlock(&mrt_lock);
    kfree_skb(skb);
    return -ENODEV;
}
```

# 374 TCP/IP 与 Linux 协议实现

```c
1365 ip_forward(skb, cache, local);
1366 read_unlock(rt_lock);
1368 if (local)
1369 return ip_local_deliver(skb);
1371 return 0;
1374 dont_forward:
1375 if (local)
1376 return ip_local_deliver(skb);
1377 kfree_skb(skb);
1378 return 0;
1379 }
```

### 6.5.5 PIM 特性

图 6.237 IPMR–PIM vi处理器：`linux/net/ipv4/ipmr.c`。

```c
1381 #ifdef CONFIG_IP_PIM_VI
1382 /*
1383 * 处理 PIM_VI 的 IGMP 消息 */
1386 int pim_rcv_vi(struct sk_buff *skb, unsigned short len)
{
1389 struct igmp *pim = (struct igmp *)skb->h_raw;
1390 struct iphdr *encap;
1391 struct net_device *reg_dev = NULL;
1392 if (iproute_do_pim ||
1393 len < sizeof(encap) ||
1394 pim->group != PIM_VI_VERSION || pim->code != PIM_REGISTER)
1395 kfree_skb(skb);
1396 return -EINVAL;
1398 }
1399 encap = (struct iphdr*)(skb->h_raw + sizeof(igmp));
1400 /* 检查：
1401 a. 数据包确实指向多播组
1402 b. 数据包不是 NULL_REGISTER
1403 c. 数据包未被截断 */
1406 if (MULTICAST(encap->daddr) == 0 ||
1407 ntoohs(encap->tot_len) + sizeof(*pim) < len)
1409 kfree_skb(skb);
1410 return -EINVAL;
1411 }
```

# 图 6.238 IPMR–PIM v1 处理器：`linux/net/ipv4/ipmr.c`。

```c
read_lock(rt_num_lock);

if (reg_vif_num >= 0)
    reg_dev = vif_table[reg_vif_num].dev;

if (reg_dev)
    dev_hold(reg_dev);

unlock_lock(rt_num_lock);

if (reg_dev == NULL) {
    kfree_skb(skb);
    return -EINVAL;
}

skb->mac_raw = skb->h_raw;
skb_pull(skb, (unsigned char*)encap - skb->data);
skb->nh_ip = (struct iphdr*)skb->data;
skb->dev = reg_dev;
memset(&skb->options, 0, sizeof(struct ip_options));
skb->protocol = cpu_htons(ETH_P_IP);
skb->ip_summed = 0;
skb->pkt_type = PACKET_HOST;
dst_release(skb->dst);
skb->dst = NULL;
((struct net_device_stats*)reg_dev->priv)->rx_bytes += skb->len;
((struct net_device_stats*)reg_dev->priv)->rx_packets+=1;
#ifdef CONFIG_NETFFILTER
nf_conrack_put(skb->nfct);
skb->nfct = NULL;
#endif
netif_rx(skb);
dev_put(reg_dev);
return 0;
```

# 图 6.239 IPMR–PIM v2 处理器：`linux/net/ipv4/ipmr.c`。

```c
#ifdef CONFIG_IP_PIM_V2
int pim_rcv(struct skb_buff *skb, unsigned short len)
{
    struct pimrehdr *pim = (struct pimrehdr*)skb->h_raw;
    struct iphdr *encap;
    struct net_device *reg_dev = NULL;
    if (len < sizeof(pim) + sizeof(encap) ||
        (pim->type != (PIM_VERSION_4) ||
        (pim->flags & PIM_NULL_REGISTER) ||
```
