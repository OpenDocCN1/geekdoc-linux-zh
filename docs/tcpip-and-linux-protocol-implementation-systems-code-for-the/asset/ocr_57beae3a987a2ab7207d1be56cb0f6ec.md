# Infrastructure Protocols 395

```
536 struct ipphdr *iph;               /* Our new IP header */
537 int      max_headroom;             /* The extra header space needed */
538 u32      dst = tiph->daddr;
539 int      mtu;
540 
541 if (tunnel->recursion++) {
542     tunnel->stat.collisions++;
543     goto tx_error;
544 
545 }
546 if (skb->protocol != __constant_16__constant_htons(ETH_P_IP)) {
547     goto tx_error;
548 
549 if (toski) {
550     tos = old_iph->tos;
551 }
552 if (dst) {
553     /* NBM4 tunnel */
554     if ((rt == (struct rtable*)skb->dst) == NULL) {
555         tunnel->stat.fifo_errors++;
556         goto tx_error;
557     }
558     if ((dst = rt->rt_gateway) == 0) {
559         goto tx_error_icmp;
560     }
```

# 6.270 IP in ip-transmit code: linux/net/ipv4/ipip.c.

```
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
580 if (skb->dst & mtu mtu < skb->dst->pmtu) {
581     skb->dst->pmtu = mtu;
582 }
583 df = (old_iph->frag_off & constant_htons(IP_DF));
584 if ((old_iph->frag_off & constant_htons(IP_DF)) & mtu != ntoohs(old_iph->tot_len)) {
```