# 382 TCP/IP and Linux Protocol Implementation

# 6.7 Network Address Translation

Network address translation is popular wherever one has a shortage of addresses, and is also frequently used as part of simple site security, especially in conjunction with firewalls.

Figure 6.247 Internet Protocol–simple NAT: linux/net/ipv4/ip_nat.dumb.c.

```
46 int
47 ip_do_nat(struct sk_buff *skb)
48 {
49     struct rtable *rt = (struct rtable*)dst;
50     struct iphdr *iph = skb->nh;
51     u32 odaddr = iph->daddr;
52     u32 osaddr = iph->saddr;
53     u16 check;
54
55     IPCB(skb)->flags |= IPSBSK_TRANSLATED;
56
57
58     /* Rewrite IP header */
59 ip->daddr = rt->rt_dat_map;
60 ip->saddr = rt->rt_src_map;
61 ip->check = 0;
62 ip->check = ip_csum(unsigned char)*iph, iph->hl);
```

Figure 6.248 Internet Protocol–simple NAT: linux/net/ipv4/ip_nat.dumb.c.

```
63 / If it is the first fragment, rewrite protocol headers */
64
65 if ((iph->frag_off &htons(IP_OFFSET))) {
66     u16 *cksum;
67
68     switch (iph->protocol) {
69     case IPPROTO_TCP:
70         cksum = (u16*)((struct tcphdr*)(char*)iph) + (iph->hl<<2));-check;
71         if ((cksum+1) > skb->tail)
72             goto truncated;
73             check = csum_tcpudp_magic(iph->saddr, iph->daddr, 0, 0, (*cksum));
74             *cksum = csum_tcpudp_magic(osaddr, "odaddr", 0, 0, "check");
75             break;
76     case IPPROTO_UDP:
77         cksum = (u16*)((struct udphdr*)(char*)iph) + (iph->hl<<2));-check;
78         if ((cksum+1) > skb->tail)
79             goto truncated;
80         if ((*cksum) == 0) {
81             check = csum_tcpudp_magic(iph->saddr, iph->daddr, 0, 0, "check");
82             check = csum_tcpudp_magic(osaddr, "odaddr", 0, 0, "check");
83             *cksum = check ? 0xFFFF;
84 }
85     }
86     break;
```