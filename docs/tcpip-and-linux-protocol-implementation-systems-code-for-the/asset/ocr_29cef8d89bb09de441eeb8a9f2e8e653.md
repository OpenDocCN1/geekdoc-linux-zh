# Infrastructure Protocols 457

```
554   return -ETUNREACH;
555  }
556  if (fl->f16_src == NULL) {
557     err = ipv6_saddr(dst, fl->f16_dst, &saddr);
558     if (err) {
559       #if IP6_DEBUG >= 2
560         printk(KERN_DEBUG, "ip6_build_zmit: "
561             "no aviable source address\n\n562       #endif
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

Figure 6.3.5 Ipv6-output: linux/net/ipv6/ip6_output.c.

```
580  jumbolen = 0;
581  if (isk->protoinfo.af_inet.hdrincl) {
582    pktlength += sizeof(struct ipv6hdr);
583    if (opt) {
584      pktlength += opt->opt_len + opt->opt_nfl;
585
586      if (pktlength > 0xFFFF + sizeof(struct ipv6hdr)) {
587        // Jumbo dat.
588        It is assumed, that in the case of hdrincl
589        jumbo option is supplied by user.
590        /*
591        pktlength += 8;
592        jumbolen = pktlength - sizeof(struct ipv6hdr);
593      }
594    }
595  mtu = dst->pmtu;
596  if (np->frag_size < mtu) {
597    if (np->frag_size < mtu) {
598      mtu = np->frag_size;
599  else if (np->pmtudisc == IPv6_PMTUDISC_DONT) {
600    mtu = IPv6_MIN_MTU;
601  }
```