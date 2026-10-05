

# 408 TCP/IP 与 Linux 协议实现

```c
569 u32 seqno = 0;
570 struct ip_tunnel *tunnel;
571 int offset = 4;
572
573 if (flags&(GRE_CSUM|GRE_KEY|GRE_ROUTING|GRE_SEQ|GRE_VERSION)) {
574   /* - 版本必须为 0。
575    - 我们不支持路由头头。
576    */
577   if (flags&(GRE_VERSION|GRE_ROUTING)) {
578     goto drop_nolock;
579   }
580 if (flags&GRE_CSUM) {
581   csum = ip_compute_csum(h, len);
582   offset += 4;
583 }
584 if (flags&GRE_KEY) {
585   key = (u32)(h + offset);
586   offset += 4;
587 }
588 if (flags&GRE_SEQ) {
589   seqno = ntohl((u32)(h + offset));
590   offset += 4;
591 }
592 }
593 
594   read_lock(&kipreg_lock);
```

图 6.290 GRE 隧道接收用例：linux/net/ipv4/ip_gre.c。

```c
595 if ((tunnel = ip_tunnel_lookup(ip->saddr, ip->daddr, key)) != NULL) {
596   skb->mac_raw = skb_pull(skb);
597   skb->nb_raw = skb_pull(skb, h + offset - skb->data);
598   memset((struct ip*)skb)->options, 0, sizeof(struct ip_options));
599   skb->ip_mem = 0;
600   skb->protocol = (u16)(h + 2);
601   skb->pkt_type = PACKET_BROADCAST;6602 #ifdef CONFIG_NET_IPRE_GRE
603   if (MULTICAST(ip->daddr)) {
604     /* 回环包，丢弃它！ */
605     if (((struct rtentry*)skb->dst)->key.iif == 0) {
606       goto drop;
607       tunnel->stat.packet++;
608       skb->pkt_type = PACKET_BROADCAST;
609     }
610   }
611 #endif
612  if ((flags&GRE_CSUM) & skb->csum)) {
613     if ((flags&GRE_CSUM) & tunnel->parms.flags&GRE_CSUM) {
614       tunnel->stat.rx_crc_errors++;
615       tunnel->stat.rx_errors++;
616       goto drop;
617     }
618  }
```

# 图 6.291 GRE 隧道接收用例：linux/net/ipv4/ip_gre.c

```c
if (tunnel->parms.i_flags&GRE_SEQ) {
    if ((flags&GRE_SEQ)) {
        if ((tunnel->i_seqno & (s32)(seqno -tunnel->i_seqno) < 0) {
            tunnel->stat.rx_fifo_errors++;
            tunnel->stat.rx_errors++;
            goto drop;
        }
        tunnel->i_seqno = seqno + 1;
    }
tunnel->stat.rx_packets++;
skb->rx_bytes += skb->len;
skb->dev += tunnel->dev;
dst_release(skb->dev);
skb->dst = NULL;
}
#ifdef CONFIG_NFCTOL
nf_connect_put(skb_nfct);
skb->nfct = NULL;
#endif
#ifdef CONFIG_NFCTOL_DEBUG
skb->nfct_debug = 0;
#endif
ipgre_ecn_decapsulate(iph, skb);
net_rx(skb);
read_unlock(&ipgre_lock);
return(0);
}
icmp_send(skb, ICMP_DEST_UNACH, ICMP_PROTO_UNACH, 0);
drop:

# 图 6.292 GRE 隧道发送封装：linux/net/ipv4/ip_gre.c

```c
/* 需要这个封装器是因为 NFHOOK 获取了地址 */
static inline int do_ip_send(struct sk_buff *skb) {
    return send(skb);
}
```

# 410 TCP/IP 与 Linux 协议实现

## GRE 隧道中的数据传输

图 6.293 GRE 隧道传输用例：linux/net/ipv4/ip_gre.c。

```c
static int ipgre_tunnel_xmit(struct sk_buff *skb, struct net_device *dev) {
  struct ip_tunnel *tunnel = (struct ip_tunnel*)dev->priv;
  struct net_device_stats *stats = &tunnel->stat;
  struct iphdr *old_iph = skb->iph;
  struct iphdr *tip;
  u8 tos;
  u16 df;                                     /* 往目标主机 */
  struct rtable *idev;                        /* 往设备 */
  struct iphdr *tip;                          /*  IP 头 */
  int max_headroom;                           /* 需要额外的头 */
  int gre_hlen;
  u32 dt;
  int mtu;

  if (tunnel->collisions) {
    tunnel->stat.collisions++;
    goto tx_error;
  }

  if (dev->hard_header) {
    gre_hlen = 0;
    tip = (struct iphdr*)skb->data;
  } else {
    gre_hlen = tunnel->hlen;
    tip = tunnel->parms->iph;
  }

  if ((dst = tip->daddr) == 0) {
    /* 隧道 */
    if (skb->dst == NULL) {
      tunnel->stat.fifo_errors++;
      goto tx_error;
    }
  }
```

图 6.294 GRE 隧道传输用例：linux/net/ipv4/ip_gre.c。

```c
if ((skb->protocol == htonsons(ETH_P_IP)) {
  rt = (struct rtable*)skb->dst;
  if ((dst = rt->gateway) == 0) {
    goto tx_error_icmp;
  }
}
#ifdef CONFIG_IPV6
else if (skb->protocol == htonsons(ETH_P_IPV6)) {
  struct in6_addr *addr6;
  int addr_type;
```

# 411 基础设施协议

```c
  if (neigh == NULL) {
    goto tx_error;
  }
  addr6 = (struct in6_addr*)&neigh->primary_key;
  addr_type = ipv6_addr_type(addr6);
  if (addr_type == IPv6_ADDR_ANY) {
    addr6 = skb->nh->ipv6->daddr;
    addr_type = ipv6_addr_type(addr6);
  }
  if ((addr_type & IPv6_ADDR_COMPAT) == 0) {
    goto tx_error_icmp;
  }
  dst = skb->s_addr[3];
}
#endif
  else {
    goto tx_error;
  }

  tos = tip->tos;
  if (tos) {
    if (skb->protocol == htonsons(ETH_P_IP)) {
      tos = old_iph->tos;
      tos &= 1;
    }
  }
  if (ip_route_output(rt, dst->saddr, RT_COS(tos), tunnel->parms.link)) {
    tunnel->stat.carrier_errors++;
    goto tx_error;
  }

  tdev = rt->u.dst.dev;
  if (tdev == dev) {
    ip_rt_put(rt);
    tunnel->stat.collisions++;
    goto tx_error;
  }
}
```

图 6.295 GRE 隧道传输用例：linux/net/ipv4/ip_frag.gre。

```c
df = tip->frag_off;
mtu = rt->u.dst.pmtu - tunnel->hlen;
if (skb->protocol == htonsons(ETH_P_IP)) {
  skb->dst->pmtu = mtu;
}
df = (old_iph->frag_off & htonsons(IP_DF));
```

# 467 TCP/IP 与 Linux 协议实现

```c
    if ((old_iph->frag_off & htonsons(IP_DF))) {
        mtu < ntohl(old_iph->to_len);
        icmp_send(skb, ICMP_DEST_UNACH, ICMP_FRAG_NEEDED, mtu);
        ip_rt_put(rt);
        goto tx_error;
    }
    #ifdef CONFIG_IPV6
    else if (skb->protocol == htonsons(ETH_P_IPV6)) {
        struct rt_info *rt6 = (struct rt_info*)skb->dst;
        if (rt6->dst->pmtu == IPv6_MIN_MTU) {
            if ((tunnel->iph.daddr & MULTICAST)) {
                rt6->flags |= RTF_MODIFIED;
                skb->dst->pmtu = mtu;
            }
        }
    }
    if (mtu > IPv6_MIN_MTU <= skb->len - tunnel->hlen + gre_hlen) {
        icmp_send(skb, ICMP_V6_PKT_TO_BIG, 0, mtu);
        ip_rt_put(rt);
        goto tx_error;
    }
#endif
```

图 6.296 GRE 隧道传输用例：linux/net/ipv4/ip.gre。

```c
    if (tunnel->err_count > 0) {
        if (jiffies - tunnel->err_time < IPTIME_TIMEOUT) {
            tunnel->err_count--;
        }
        dst_link_failure(skb);
    } else {
        tunnel->err_count = 0;
    }
    skb->b.raw = skb->nh->raw;
    max_headroom = ((dev->hard_header_len + 15) + gre_hlen);
    if (skb->headroom < max_headroom || skb_cloned(skb)) {
        struct sk_buff *new_skb = realloc(skb, max_headroom);
        if (new_skb) {
            ip_rt_put(rt);
            stats->dropped++;
            dev_kfree(skb);
            tunnel->recursion--;
            return 0;
        }
    }
```

# 413 基础设施协议

```c
if (skb->skb) {
    skb_set_owner_v(new_skb, skb);
    dev_free_skb(skb);
    skb = new_skb;
}
nskb->nh->raw = skb_push(skb, gre_blen);
memset(&IPCB(skb)->opt, 0, sizeof(IPCB(skb)->opt));
dst_release(skb);
skb->dst = &rt->dst;
```

# 图 6.297 GRE 隧道传输用例：gre.c。

```c
/*
 * 下推并安装 IPIP 头。
 */
iph = skb->nh->iph;
iph->version = 4;
iph->ihl = sizeof(struct iphdr) >> 2;
iph->frag_off = df;
iph->protocol = IPPROTO_GRE;
iph->tos = ip_gre_encapsulate(tos, old_iph, skb);
iph->daddr = rt_dst;
iph->saddr = rt_src;

if ((iph->ttl == old_iph->ttl) == 0) {
    if (skb->protocol == htonsons(ETH_P_IP))
        iph->ttl = old_iph->ttl;
}
#ifdef CONFIG_IPV6
else if (skb->protocol == htonsons(ETH_P_IPV6))
    iph->ttl = ((struct ipv6hdr*)old_iph)->hop_limit;
#endif
else
    iph->ttl = sysctl_ip_default_ttl;
}

if ((u16*)iph->i[0]) == tunnel->pars.flags;
    ((u16*)iph->i[1]) = skb->protocol;
```

# 图 6.298 GRE 隧道传输用例：gre.c。

```c
if (tunnel->pars.flags&GRE_KEY(GRE_CSUM)) {
    u32 *ptr = (u32*)(((u8*)iph) + tunnel->hlen - 4);
    if (tunnel->pars&GRE_SEQ) {
        +tunnel->o_seqno;
        *ptr = ntohl(tunnel->o_seqno);
        ptr--;
    }
}
```

