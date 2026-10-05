# 258 TCP/IP and Linux Protocol Implementation

```
67   {
68     if (opt->ts) {
69         memset(iph+opt->ts, IPOPT_NOP, iph[opt->ts+1]);
70         opt->ts = 0;
71         opt->needsaddr = opt->needtime = 0;
72     }
73   }
```

Figure 6.65 IP options-echo: linux/net/ipv4/ip_options.c.

```
75   /*
76    * Provided (soft, skb) points to receive options,
77    * build in doct compiled option set appropriate for answering.
78    * i.e. invert SRR option, copy others,
79    * and grab room in RR/TS options.
80    *
81    * NOTE: dopt cannot point to skb.
82    */
83 
84   int ip_options_echo(struct ip_options *dopt, struct skb_buff *skb) 
85   {
86       struct ip_options *sopt;
87       unsigned char *sptr, *dptr;
88       int offsetset, offsetset;
89       int optlen;
90       u32 daddr;
91 
92       memset(dopt, 0, sizeof(struct ip_options));
93 
94       dopt->is_data = 1;
95 
96       sopt = &IPCB(skb)->opt;
97 
98       if (sopt->optlen == 0) {
99           dopt->optlen = 0;
100          return 0;
101     }
102 
103      sptr = skb->nh.raw;
104      dptr = dopt->__data;
105 
106      if (skb->dst) {
107          daddr = ((struct rtable*)skb->dst)->rt_spec_dst;
108      else
109          daddr = skb->nh.iph->daddr;
```

Figure 6.66 IP options-echo: linux/net/ipv4/ip_options.c.

```
if (sopt->rr) {
    optlen = sptr[sopt->rr+1];
    offsetset = sptr[sopt->rr+2];
```