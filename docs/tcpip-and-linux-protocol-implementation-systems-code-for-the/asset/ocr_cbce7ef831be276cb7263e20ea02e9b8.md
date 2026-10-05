# Figure 6.357 IPv6 receive: linux/net/ipv6/ipv6_input.c.

```
/* pkt_len may be zero Jumbo payload option is present */
if (pkt_len || hdr->nextdr == NEXTHDR_HDR_OP) {
    if (pkt_len + sizeof(struct ipv6hdr) > skb->len)
        goto truncated;
    skb_trim(skb, pkt_len + sizeof(struct ipv6hdr));
}
}

if (hdr->nextdr == NEXTHDR_HDR_OP) {
    skb->raw = (u8*)(hdr+1);
    if (ipv6_parse_hopops(skb, &khdr->nextdr)) {
        IP6_INC_STATS_BH(IP6InHErrors);
        return 0;
    }
}
return NF_HOOK(PF_INET6, NF_IP6_PRE_ROUTING, skb, NULL, ip6_rcv_finish);
truncated:
IP6_INC_STATS_BH(IP6InTruncatedPkts);
IP6_INC_STATS_BH(IP6InHErrors);
free_skb(skb);
return 0;
```

This ends up calling ip6_rcv_finish via the Network Filter Hook again, which then returns the packet to the appropriate demultiplexing (e.g., forwarding, or local reception to a transport protocol) via the normal pattern:

# Figure 6.358 IPv6 receive finish: linux/net/ipv6/ipv6_buff.c.

```
static inline int ip6_rcv_finish(struct skb *skb) {
    if (skb->dst == NULL)
        ip6_route_input(skb);
    return skb->dst->input(skb);
}
```

# 6.9.6 IPv6 Output

Output is pretty straightforward. As usual we have to go via the Network Filter Hook.