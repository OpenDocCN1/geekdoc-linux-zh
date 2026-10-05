# Figure 2.625 IP in IP–ICMP error handling: linux/net/ipv4/ipip.c.

```
/* change mtu on this route / */
if (type == ICMP_DEST_UNREACH && code == ICMP_FRAG_NEEDED)
    if (rel_info, skb(skb2)->dst->pmtu)
        kfree_skb(skb2);
    return;
    skb2->dst->pmtu = rel_info;
    rel_info = htonl(rel_info);
} else if (type == ICMP_TIME_EXCEEDED)
    struct ip_tunnel *t = (struct ip_tunnel*)dev->priv;
    if (t->parms.iph->ttl)
        rel_type = ICMP_DEST_UNREACH;
        rel_code = ICMP_HOST_UNREACH;
icmp_send(skb2, rel_type, rel_code, rel_info);
kfree_skb(skb2);
return;
```

# Figure 2.626 IP in IP–ECN decapsulate(struct iphdr *iph, struct sk_buff *skb)

```
static inline void ipip_ecn_decapsulate(struct iphdr *iph, struct sk_buff *skb)
    if (INET_ECN_is_ce & (skb->nh->tos))
        INET_ECN_is_not_ce(skb->nh->tos);
    IP_ECN_set_ce(iph);
```

# Data in IP Tunnels

# Figure 2.627 IP in IP–receive code: linux/net/ipv4/ipip.c.

```
int ipip_rcv(struct sk_buff *skb, unsigned short len)
    struct iphdr *iph;
    struct ip_tunnel *tunnel;
    iph = skb->nh;
    skb->nh->len = skb->nh->raw;
    skb->nh->raw = skb_pull(skb, skb->raw - skb->data);
    memset(&((struct ip*)iph)->opt), 0, sizeof(struct ip_options));
    skb->protocol = __constant_htons(ETH_P_IP);
    skb->ip_summed = 0;
    skb->pkt_type = *PACKET_HOST;
```