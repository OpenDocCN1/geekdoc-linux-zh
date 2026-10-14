
559         goto tx_error_icmp;

560     }
```

## 6.270 ip-transmit 代码中的 IP：`linux/net/ipv4/ipip.c`

```c
562 if (ip_route_output(rt, dst, tiph->saddr, RT_TOS(tos), tunnel->parms.link)) {
563     tunnel->stat.carrier_errors++;
564     goto tx_error_icmp;
565 }
566 tdev = rt->u0.dst.dev;
567 
568 if (tdev == dev) {
569     ip_rt_put(rt);
570     tunnel->stat.collisions++;
571     goto tx_error;
572 }
573 
574 mtu = rt->u2.dst.pmtu - sizeof(struct ipphdr);
575 if (mtu < 68) {
576     tunnel->stat.collisions++;
577     ip_rt_put(rt);
578     goto tx_error;
579 }
580 if (skb->dst & mtu && mtu < skb->dst->pmtu) {
581     skb->dst->pmtu = mtu;
582 }
583 df = (old_iph->frag_off & constant_htons(IP_DF));
584 if ((old_iph->frag_off & constant_htons(IP_DF)) & mtu != ntoohs(old_iph->tot_len)) {
```

# TCP/IP 与 Linux 协议实现

```c
586 icmp_send(skb, ICMP_DEST_UNREACH, ICMP_NEEDED, hhtonl(mtu));
587 ip_rt_put(rt);
588 goto error_tx;
589 
591 if (tunnel->err_count > 0) {
592 if (jiffies - tunnel->err_time < IPTUNTUNE_ERR_TIMED) {
593 tunnel->err_count--;
594 dst_link_failure(skb);
595 else
596 tunnel->err_count = 0;
597 
598 skb->h.raw = skb->nh.raw;
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_451_0.png)

```c
/*
 * 好的，现在我们看看是否可以原样将其装入缓冲区。
 */
max_header = ((struct dev_hard_len)+15) + sizeof(struct iphdr);
if (skb->headroom(skb) > max_header || skb_cloned(skb) || skb_shared(skb)) {
    struct skb_buff *new_skb = skb_realloc_head(skb, max_header);
    if (new_skb) {
        ip_rt_put(rt);
        skb->to_dropped++;
        dev_free_skb(skb);
        tunnel->recursion--;
        return 0;
    }
    if (skb->sk)
        dev_set_owner(new_skb, skb->skb);
    skb = new_skb;
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_451_1.png)

```c
/*
 * 下推并安装 IPI 头部。
 */
iph = skb->nh.iph;
iph->version = 4;
iph->ihl = sizeof(struct iphdr)>>2;
```

```c
633 iph->frag_off          = df;
634 iph->protocol          = PROTO_IPIP;
635 iph->tos               = INET_GCN_encapsulate(tos, old_iph->tos);
636 iph->daddr              = rt->rt_dst;
637 iph->saddr              = rt->rt_src;
638 
639 if ((iph->ttl == tiph->ttl) == 0) {
640     iph->ttl               = old_iph->ttl;
641 
642 #ifdef CONFIG_NETFILTER
643     nf_conrack_put(skb->nfct);
644     skb->nfct = NULL;
645 #ifdef CONFIG_NETFILTER_DEBUG
646     skb->nf_debug = 0;
647 #endif
648 #endif
649 
650 ip_xmit();
651 tunnel->recursion--;
652 return 0;
653 
654 tx_error_icmp(skb);
655 dst_link_failure(skb);
656 tx_error:
657 tunnel->stat.errors++;
658 dev_free_skb(skb);
659 tunnel->recursion--;
660 return 0;
661 }
```

# IP 隧道管理

```c
663 static int
664 ipip_tunnel_ioctl(struct net_device *dev, struct ifreq *ifr, int cmd)
665 {
666     int err = 0;
667     struct ipip_tunnel_parms *p;
668     struct ipip_tunnel *t;
669 
670     mod_inc_use_count();
671 
672     switch (cmd) {
673     case SIOCGETTUNNEL:
674         t = NULL;
675         if (dev == &ipip_tunnel_dev) {
676             if (copy_from_user(p, ifr.ifr_data, sizeof(p))) {
677                 err = -EFAULT;
678                 break;
679             }
680         }
681         t = ipip_tunnel_locate(&p, 0);
```

```c
681         ) NULL;
682         if (t == (struct ip_tunnel*)dev->priv)
683             memcpy(p, &t->parms, sizeof(p));
684 
685         if (copy_to_user(ifr.ifr_data, &p, sizeof(p))) {
686             err = -EFAULT;
687             break;
688         }
689 	case SIOCADTUNNEL:
690 	case SIOCCHTUNNEL:
691 		err = -EPERM;
692 		if (!capable(CAP_NET_ADMIN))
693             goto done;
694 
695             err = -EFAULT;
696 		if (copy_from_user(&p
```
