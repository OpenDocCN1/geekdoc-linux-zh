
```c
/* IPv6 未提到这一点，但很明显
 * 我们向路由帧发送。 */
if (skb->dev == dst->dev && skb->dst->opt->srcrt == 0) {
    struct in6_addr *target = NULL;
    struct rt6_info *rt;
    struct neighbour *n = dst->neighbour;
}
/* 入站和输出设备相同
 * 发送重定向。 */
rt = (struct rt6_info *)dst;
if ((flags & RTF_GATEWAY)) {
    target = (struct in6_addr*)&n->primary_key;
}
else
/* 通过目的限制（在 ndisc_send 内部） */
if (xlim_allow(dst, 1)) {
    ndisc_send(skb, n, target);
} else if (ipv6_addr(hdr->saddr) == (IPV6_ADDR_MULTAST|IPV6_ADDR_LOOPBACK|IPV6_ADDR_LOCAL)) {
    /* 这个检查至关重要。 */
    goto drop;
}

if (skb->len > dst->mtu) {
    /* 再次将 OUTPUT 设备作为源地址 */
    skb->dev = dev;
    icmpv6_send(skb, ICMPV6_PKT_TOO_BIG, ICMPV6_HOPLIMIT, 0, skb->dev);
    kfree_skb(skb);
    return -EMSIZE;
}

if (!err) {
    IP6_INC_STATS(IP6_OutRequests);
    err = NF_HOOK(PF_INET6, NF_OUT, skb, dst->dev, ip6_may_reroute);
}
```

# 6.9.8 IPv6 Socket Glue

Socket粘接代码与 IPv4 有不同，因为 Socket 选项也不同，正如你预期的。以下是一个片段：

## 基础设施协议 463

```c
if (sk->protocol == IPPROTO_TCP) {
    struct tcp_copopt *opt = &(sk->tp_pinfo.af_tcp);

    local_bb_disable();

    sock_prot_dec_use(sk->prot);
    sock_prot_inc_use(&tcp->prot);
    local_bb_enable();
    sk->proto = &tcp->prot;
    tp->af_specific = &ipv4_specific;
    sk->socket_ops = &inet_stream_ops;
    sk->family = PF_INET;
    tcp_sync_msrc(sk, tp->pmtu_cookie);
} else {
    local_bb_disable();
    sock_prot_dec_use(sk->prot);
    sock_prot_inc_use(&udp->prot);
    local_bb_enable();
    sk->proto = &udp->prot;
    sk->socket_ops = &inet_dgram_ops;
    sk->family = PF_INET;
}
    opt = xchg(&mp->opt, NULL);
    if (sk_kfree(sk, opt, opt->tot_len)) {
        ptok = xchg(&mp->poptions, NULL);
        if (ptok)
            kfree_skb(ptok);
    }

    sk->destruct = inet_sock_destruct;

#ifdef INET_REFCNT_DEBUG
    atomic_dec(&inet6_sock_nr);
#endif
    MOD_DEC_USE_COUNT;
    retv = 0;
    break;
}
    goto e_inval;
```

图 6.373 IPv6 socket 设置套接选项：`linux/net/ipv6/ipv6_glue.c`。

```c
    case IPv6_PKTINFO:
        np->rxopt.bits.rxinfo = val;
        retv = 0;
        break;

    case IPv6_HOPLIMIT:
        np->rxopt.bits.rxhlim = val;
        retv = 0;
        break;

    case IPv6_RTMDR:
      if (val < 0 || val > 2)
          goto e_inval;
      np->rxopt.bits.scrcrt = val;
      retv = 0;
      break;

  case IPv6_HOOPTS:
              np->rxopt.bits.hopopts = val;
              retv = 0;
              break;

  case IPv6_AUTHHDR:
              np->rxopt.bits.authhdr = val;
              retv = 0;
              break;

  case IPv6_DSTOPTS:
              np->rxopt.bits.dstopts = val;
              retv = 0;
              break;

  case IPv6_FLOWINFO:
              np->rxopt.bits.rxflow = val;
              retv = 0;
              break;
```

数据包选项：

图 6.374 IPv6 socket 设置套接选项：`linux/net/ipv6/ipv6_sockglue.c`。
