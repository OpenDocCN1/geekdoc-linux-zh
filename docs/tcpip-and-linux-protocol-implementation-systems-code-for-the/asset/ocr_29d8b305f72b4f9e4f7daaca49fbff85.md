# Figure 6.80 IP options-receive SSR and process: linux/net/ipv4/ip.options.c.

```
struct ip_options *opt = &(IPCB(skb)->opt);
int arrspace, srtptr;
u32 nexthop;
struct iphdr *iph = skb->nh->iph;
unsigned char *optr = skb->nh.raw+opt->sr;
struct rtable *rt = (struct rtable+)*skb->dst;
struct rtable *rt2;
int err;

if (!opt->srr)
    return 0;

if (skb->pkt_type == PACKET_HOST)
    return -EINVAL;
if (rt->rt_type == RTN_UNICAST)
    if (opt->is_stricteroute)
        return 0;
    icmp_send(skb, ICMP_PARAMETER_PROB, 0, htonl((16<<24));
    return -EINVAL;

if (rt->rt_type != RTN_LOCAL)
    return -EINVAL;
```

# Figure 6.81 IP options-receive SSR and process: linux/net/ipv4/ip.options.c.

```
for (rrptr=optptr[2], rrspace = optptr[1]; rrptr <= rrspace; rrptr += 4) {
    if (rrptr > 3 > rrspace) {
        icmp_send(skb, ICMP_PARAMETER_PROB, 0, htonl((opt->srr+2)<<24));
        return -EINVAL;
    }
    memcpy(nexthop, optptr[rrptr], 4);
    rt = (struct rtable*)skb->dst;
    skb->dst = NULL;
    err = ip_route_input(skb, nexthop, &addr, iph->tos, skb->dev);
    rt2 = (struct rtable*)skb->dst;
    if (err || rt->rt_type != RTN_UNICAST && rt2->rt_type == RTN_LOCAL) {
        ip_rt_put(rt);
        skb->dst = &rt->dst;
        return -EINVAL;
    }
    ip_rt_put(rt);
    if (rt->rt_type != RTN_LOCAL)
        break;
    /* Super(8) loopback forward */
    memcpy(&iph->addr, optptr[rrptr], 4);
    opt->is_changed = 1;
}
if (rrptr <= rrspace) {
```