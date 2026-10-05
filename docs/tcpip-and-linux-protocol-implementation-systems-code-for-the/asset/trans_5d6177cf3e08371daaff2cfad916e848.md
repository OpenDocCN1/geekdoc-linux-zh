

# 基础设施协议 457

```c
554   return -ETUNREACH;
555  }
556  if (fl->f16_src == NULL) {
557     err = ipv6_saddr(dst, fl->f16_dst, &saddr);
558     if (err) {
559       #if IP6_DEBUG >= 2
560         printk(KERN_DEBUG, "ip6_build_zmit: "
561             "no available source address\n\n");
562       #endif
563         goto out;
564     }
565     fl->f16_src = &saddr;
566   }
567   pktlength = length;
568   if (limit < 0) {
569     if (ipv6_addr_is_multicast(fl->f16_dst)) {
570       limit = np->mcast_hops;
571     else
572       limit = np->hop_limit;
573     if (limit < 0) {
574       limit = ((struct rt6_info*)dst)->rt6i_hiplimit;
575     }
576   }
```

图 6.3.5 Ipv6-output：linux/net/ipv6/ip6_output.c。

```c
580  jumbolen = 0;
581  if (isk->protoinfo.af_inet.hdrincl) {
582    pktlength += sizeof(struct ipv6hdr);
583    if (opt) {
584      pktlength += opt->opt_len + opt->opt_nfl;
585
586      if (pktlength > 0xFFFF + sizeof(struct ipv6hdr)) {
587        // Jumbo 数据。
588        // 假设在包含头部（hdrincl）的情况下，
589        // jumbo 选项是由用户提供的。
590        /*
591        pktlength += 8;
592        jumbolen = pktlength - sizeof(struct ipv6hdr);
593      }
594    }
595  mtu = dst->pmtu;
596  if (np->frag_size < mtu) {
597    if (np->frag_size < mtu) {
598      mtu = np->frag_size;
599  } else if (np->pmtudisc == IPv6_PMTUDISC_DONT) {
600    mtu = IPv6_MIN_MTU;
601  
```

# 458 TCP/IP 与 Linux 协议实现

```c
604      /* 关键算术溢出检查。
605      FIXME: gcc 会优化它吗? --ANK (980726)
606      */
607  if (pktlen < length) {
608      ipv6_local_error(sk, EMSIZE, fl, mtu);
609      err = -EMSIZE;
610      goto out;
611  }
613
613  if (flags&MSG_CONFIRM(dst)) {
614      dst_confirm(dst);
```

图 6.366 IPv6-output：linux/net/ipv6/ipv6_output.c。

```c
617  if (pktlen <= mtu) {
618      struct sk_buff *skb;
619      struct ipv6hdr *hdr;
620      struct net_device *dev = dst->dev;
621
622      err = 0;
623      if (flags&MSG_PROBE)
624          goto out;
625
626      skb = sock_alloc_skb(sk, pktlen + 15 +
627                               dev->header_len, 0);
628                               flags & MSG_DONTWAIT, &err);
629
630      if (skb == NULL) {
631          IP6_INC_STATS(IP6_Discards);
632          goto out;
633      }
634
635      skb->dst = dst_clone(dst);
636
637      skb_reserve(skb, (dev->header_len + 15) & ~15);
638
639      hdr = (struct ipv6hdr *)skb->tail;
640      skb->ipv6 = hdr;
641
642      if (!sk->protinfo->af_inet.hdrincl) {
643          ipv6_build_frag(1, sk, fl);
644          jumbolen = sizeof(struct ipv6hdr) * pktlen;
644
646
647      if (opt && jumbo) {
648          *prev_hdr = &hdr->nexthdr;
649          prev_hdr = ipv6_build_nfrag_opts(sk, prev_hdr, final_dst,
650           jumbolen);
651          if (opt && ipv6_frag_opts(sk, prev_hdr, opt)) {
652              ipv6_build_frag_opts;
653          }
654      }
655  ```

图 6.367 IPv6-output：linux/net/ipv6/ip6_output.c。

```c
654      skb_put(skb, length);
655      err = getfrag(data, &hdr->saddr,
656                            ((char *)hdr) + (pktlen - length,
657                            opt, length);
658
659      if (!err) {
660          IP6_INC_STATS(IP6_OutRequests);
661          err = NF_HOOK(PF_INET6, NF_OUT, skb, dst->dev,
662                          ip6_may_reroute);
663      } else {
664          err = -EFAULT;
665          kfree_skb(skb);
666      }
667  } if (sk->protinfo->af_inet.hdrincl || jumbolen ||
668      np->ptmsudic == IPv6_PTMSUDIC_DO) {
669          ipv6_local_error(sk, EMSGSIZE, mtu);
670          err = -EMSGSIZE;
671          goto out;
672  }
673
674  err = ip6_frag_xmit(sk, data, dst, fl, opt, final_dst, hlimit,
675                               flags, length, mtu);
676                                 
677  
678  /*
679   cleanup
680   */
681  out:
682      ip6_dst_store(sk, dst, fl->nl_u.ipv6.daddr == np->daddr : NULL);
683      if (err > 0) {
684          err = np->verr ? net_to_errno(err) : 0;
685      return err;
686  }
```

# 6.9.7 IPv6 Forward Function

图 6.368 IPv6-forward：linux/net/ipv6/ip6_output.c。

```c
720  int ip6_forward(struct sk_buff *skb)
721  {
722      struct dst_entry *dst = skb->dst;
723      struct ipv6hdr *hdr = skb->nh->ipv6;
724      struct inet6_skb_param *opt = *(struct inet6_skb_param*)skb->cb;
725
726      if (ipv6_devconf.forwarding == 0 && !opt->srcrt)
727          goto drop;
728  }
```

# 4460 TCP/IP and Linux Implementation

```c
/*
 * 我们不对 RA 数据包进行任何处理，而是将它们原封推送到用户层
 * 而没有保证应用程序能够解释它们。原因是
 * 我们不是端节点，因此如果数据包包含 AH/ESP，
 * 我们无法进行任何操作。分片也将是一个错误，RA 数据包
 * 不能被分片，因为没有保证不同的分片将沿着同一路径。--ANK
 */
if (opt->ra) {
    u8 *ptr = skb->skb_raw + opt->ra;
    if (ip6_ra_chain(skb, (ptr[2])<<8 + ptr[3])) {
        return 0;
    }
}
/*
 * 检查并递减 ttl
if (hdr->hop_limit < 1) {
    /* 强制将 OUTPUT 设备作为源地址 */
    skb->dev = dev;
    icmpv6_send(skb, ICMPV6_TIME_OUT, ICMPV6_HOPLIMIT, 0, skb->dev);
    kfree_skb(skb);
    return -ETIMEDOUT;
}
```

图 6.369 IPv6-forward：linux/net/ipv6/ip6_output.c。

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

