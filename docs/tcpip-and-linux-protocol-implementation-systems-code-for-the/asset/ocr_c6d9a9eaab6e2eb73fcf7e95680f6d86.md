# 450 TCP/IP and Linux Protocol Implementation

```
731
732      case ND_OPT_TARGET_ADDR:
733      case ND_OPT_REDIRECT_HDR: NULL)
734               ND_PRINTK("got illegal option with RA\
```

Other messages include redirects and errors.

# 6.9.5 IPv6 Input

As IPv4, IPv6 input is called on demultiplexing packet (see discussion in / Chapters 3 and 4). This ends up here:

Figure 6.356 IPv6 receive: linux/net/ipv6/ip6_input.c.

```
54  int ipv6_rc(struct sk_buff *skb, struct net_device *dev, struct packet_type *pt)
55  {
56      struct ipv6hdr *hdr;
57              u32
58              pkt_len;
59
60          if (skb->pkt_type == PACKET_OTHERMOST)
61              goto drop;
62
63              IP6_INC_STATS_BH(ip6InReceives);
64
65          if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)
66              goto out;
67
68              /* Store incoming device index. When the packet will
69              be queued, we cannot refer to skb->dev anymore.
70              */
71              (struct in6_dev_param *)skb->cb)->dev = dev->ifindex;
72              hdr = skb->nh->ipv6;
73
74              if (skb->len < sizeof(struct ipv6hdr) || hdr->version != 6)
75                  goto err;\n76
77              pkt_len = ntohs(hdr->payload_len);
```