

# 378 TCP/IP 与 Linux 协议实现

```c
1564      int vif;
1565
1566      if (!nowait) {
1567          read_unlock(&kmrt_lock);
1568          return -EAGAIN;
1569}
1570
1571      dev = skb->dev;
1572      if (dev == NULL || (vif == ipmr_find_dev(dev)) < 0) {
1573          read_unlock(&kmrt_lock);
1574          return -ENODEV;
1575}
1576
1577      skb->nh->vif = skb_push(skb, sizeof(struct iphdr));
1578      skb->nh->ip->saddr = sizeof(struct iphdr);
1579      skb->nh->ip->daddr = rt->rt_dest;
1580      skb->nh->ip->version = 0;

1582      err = ipmr_cache_unresolved(vif, skb);
1583          read_unlock(&kmrt_lock);
1584      return err;
1585}
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_433_0.png)

```c
1589  static int ipmr_vif_info(char *buffer, char **start, off_t offset, int length)
1590  {
1591      struct vif_device *vif;
1592      int len=0;
1593      off_t pos=0;
1594      off_t begin=0;
1595      int size;
1596      int ct;

1597
1598      len += sprintf(buffer,
1599               "%Interface BytesIn PktsIn BytesOut PktsOut Flags Local Remote\n",
1600               pos=len;

1602
1603      read_lock(&kmrt_lock);
1604      for (ct=0;ct<maxif;ct++)
1605        {
1606            char *name = "none";
1607            vif=&vif_table[ct];
1608            if(VIF_EXISTS(ct))
1609              continue;
1610            if (vif->dev)
1611                name = vif->dev->name;
```

# 基础设施协议 379

```c
size = sprintf(buffer+len, "%2d-%10s %x1d %x1d %x1d %08x %08x %08x\n",
    ct, name, vif->bytes_in, vif->pkt_in, vif->bytes_out, vif->pkt_out,
    vif->flags, vif->local, vif->remote);
len+=size;
pos+=size;
if(pos<offset) {
    len=0;
    begin=pos;
    if(pos>offset+length) {
        break;
    }
}
read_unlock(&zrt_lock);
*start=buffer+(offset-begin);
len-==(offset-begin);
if (len<length) {
    len=length;
    if (len<0)
        len = 0;
}
return len;
```

图 2.244 IPMR–procs mfc reporting：linux/net/ipv4/ipmr.c。

```c
static int ipmr_mfc_info(char *buffer, char **start, off_t offset, int length)
{
    struct mfc_cache *mfc;
    int len=0;
    off_t pos=0;
    off_t begin=0;
    int size;
    int ct;

    len += sprintf(buffer,
        "Group Origin Ifn Pkts Bytes Wrong Oifs\n",
        pos=len);

    read_unlock(&zrt_lock);
    for (ct=0;ct<MFC_LINES;ct++) {
        for(mfc=mfc_array[ct]; mfc; mfc=mfc->next) {
            int n;
        }
    }
    /*
     * 接口转发映射
     */
    size = sprintf(buffer+len, "%08X %08X-%3d %x1d %x1d",
        (unsigned long)mfc->mfc_mcastgrp,
        (unsigned long)mfc->mfc_origin,
```

# 380 TCP/IP 与 Linux 协议实现

```c
1661 mfc->mfc_parent,
1662 mfc->mfc_un.res.pkt,
1663 mfc->mfc_un.res.bytes,
1664 mfc->mfc_un.res.wrong_if;
1665 for(n=mfc->mfc_un.res.minv;n<mfc->mfc_un.res.maxv;n++)
1666 {
1667 if(VIP_Exists(n) && mfc->mfc_un.res.ttl[n] < 256)
1668 size += sprintf(buffer+len, "%X2d-%3d", n, mfc->mfc_un.res.ttl[n]);
1669 size += sprintf(buffer+len, "In");
1670 len+=size;
1671 pos+=offset;
1672 if(pos<offset) {
1673 len=0;
1674 begin=pos;
1675 }
1676 if(pos>offset+length)
1677 goto done;
1678 }
1679 }

图 6.245 IPMR-procs from mfc reporting：linux/net/ipv4/ipmr.c。

```c
1683 spin_lock_bh(mfc_un_lock);
1684 for(mfc=mfc_un_queue; mfc; mfc=mfc->next)
1685 size = sprintf(buffer+len, "%08X %X-3d %8ld %8d\n",
1686 (unsigned long)mfc->mfc_castgrp,
1687 (unsigned long)mfc->mfc_origin,
1688 -1,
1689 (long)mfc->mfc_un.res.qlen,
1690 OL);
1691 len+=size;
1692 pos+=size;
1693 if(pos<offset) {
1694 len=0;
1695 begin=pos;
1696 }
1697 if(pos>offset+length)
1698 break;
1699 }
1700 spin_unlock_bh(mfc_un_lock);
1701 done:
1702 read_unlock(kmrt_lock);
1703 *start=buffer+(offset-begin);
1704 len=(offset-begin);
1705 if(len>length)
1706 len=length;
```

```c
if (len < 0) {
  len = 0;
}
return len;
}
```

## 6.5.6 IP IP 组播

图 6.246—初始组播：linux/net/ipv4/ipmr.c。

```c
#ifndef CONFIG_IPISM_V2
struct inet_protocol pim_protocol = {
  pim_rcv,            /* PIM 处理程序 */
  NULL,               /* PIM 错误控制 */
  NULL,               /* 下一个 */
  IPPROTO_PIM,       /* 协议 ID */
  0,                  /* 拷贝 */
  NULL,               /* 数据 */
  "PIM",             /* 名称 */
};
#endif

/*
 * IP 组播路由
 */
void __init_ip_mr_init(void) {
  printk(KERN_INFO "Linux IP multicast router 0.0 plus PIM-SM\n");
  m_cache = kmem_cache_create("ip_mr_cache",
                                sizeof(struct mfc_cache),
                                0, SLAB_HWCACHE_ALIGN,
                                NULL, NULL);
  init_timer(&ipmr_expire_timer);
  ipmr_expire_timer.function=ipmr_expire_process;
  register_netdevice_notifier(&ip_mr_notifier);
  #ifdef CONFIG_PROF_PIM
  proc_net_create("ip_mr_vif",ipmr_vif_info);
  proc_net_create("ip_mr_cache",0,ipmr_mfc_info);
#endif
```

## 6.6 NAT、隧道和其他技巧

这三种技术（NAT、IP 中的 IP 和 GRE）非常相似——组播支持也十分相似。第 10 章将详细介绍网络地址翻译。

## 6.7 网络地址翻译

网络地址翻译在地址不足的地方非常流行，也经常作为简单站点安全的一部分，特别是与防火墙配合使用。

图 6.247 互联网协议–简单 NAT：linux/net/ipv4/ip_nat.dumb.c。

```c
46 int
47 ip_do_nat(struct sk_buff *skb)
{
    49 struct rtable *rt = (struct rtable*)dst;
50 struct iphdr *iph = skb->nh;
51 u32 odaddr = iph->daddr;
52 u32 osaddr = iph->saddr;
53 u16 check;
54
55 IPCB(skb)->flags |= IPSBSK_TRANSLATED;
56
57
58 /* 重写 IP 头部 */
59 ip->daddr = rt->rt_dat_map;
60 ip->saddr = rt->rt_src_map;
61 ip->check = check;
62 ip->check = ipsum((unsigned char*)iph);
63 /* 如果是第一个分片，则重写头部 */
64 if ((iph->frag_off & htons(IP_OFFSET))) {
65     u16 *csum;
66
67     switch (iph->protocol) {
68     case IPPROTO_TCP:
69         csum = (struct tcphdr*)(char*)iph + iph->hl;
70         if (csum+1 > skb_tail) {
71             goto truncated;
72         }
73         if (csum == 0) {
74             check = 0xFFFF;
75         }break;
76     case IPPROTO_UDP:
77         csum = (struct udphdr*)(char*)iph + iph->hl;
78         if (csum+1 > skb_tail) {
79             goto truncated;
80         }
81         if (csum == 0) {
82             check = 0xFFFF;
83         }
84         break;
85     }
```

图 6.248 互联网协议–简单 NAT：linux/net/ipv4/ip_nat.dumb.c。

```c
86 case IPPROTO_ICMP:
87 {
88     struct icmphdr *icmph = (struct icmphdr*)(icmph + 1);
89     struct iph *ciph;
90     u32 idaddr, isaddr;
91     int updated;
92
93     if ((icmph->type != ICMP_DEST_UNREACH) &&
94         icmph->type != ICMP_TIME_EXEDED) &&
95         icmph->type != ICMP_PROB) {
96         break;
97     }
98     ciph = (struct iph*) (icmph);
99
100    if ((unsigned*)(ciph+1) > skb_tail) {
101        goto truncated;
102    }
103    isaddr = ciph->saddr;
104    idaddr = ciph->daddr;
105    updated = 0;
106
107    if (rt->rt_flags&RTCF_DNAT && ciph->saddr == odaddr) {
108        ciph->daddr = ip->daddr;
109        updated = 1;
110    }
111}
```

