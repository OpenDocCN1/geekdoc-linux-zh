# Infrastructure Protocols 359

```
571  skb->nh_iph = (struct iphdr*)skb_put(skb, ihl);
572  memccpy(skb->data,data, ihl);
573  skb->nh_iph->protocol = 0;
574                              /* Flag the kernel that this is a route add */
575  msg = (struct igmpmsg*)skb->nh_iph;
576  msg->im_vif = vifi;
577  skb->dst = dst_clone(pkt->dst);
578
579  /*
580      Add our header
581  */
582
583  igmp=(struct igmphdr*)skb_put(skb,sizeof(struct igmphdr));
584  igmp->type =
585  msg->im_msgtype = assert;
586  igmp->code = 0;
587  skb->nh_iph->tot_len=htons(skb->len);      /* Fix the length */
588  skb->b_raw = skb->raw;
589  }
590
591  if (struct_socket == NULL) {
592      free_skb(skb);
593      return -EINVAL;
594  }
595
596  /*
597      Deliver to mrouted
598  */
599  if ((ret=route_rcv_skb(mrouted_socket,skb))<0) {
600      if (net->ratelimit()) {
601          print(KERN_WARNING "mrouted: pending queue full, dropping entries.\n");
602          free_skb(skb);
603      }
604  }
605
606  return ret;
607}
```

# Multicast Forwarding and Lookup

**Figure 6.215** IPMR-- packet to send awaiting resolution: linux/net/ipv4/ipmr.c.

```
612 static int
613 ipmr_cache_unresolved(vifi_t vifi, struct sk_buff *skb)
614 {
615
616     int err;
617     struct mfc_cache *c;
618
619     spin_lock_bh(&mfc_cache->lock);
620     for (c=mfc_unres->queue; c; c=c->next) {
621         if (c->mfc_castgroup == skb->nh_iph->daddr &)
```