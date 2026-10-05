# Figure 6.79 IP options–forwarding options–for example, route record: linux/net/ipv4:
ip.options.c.

521 void ip_forward_options(struct sk_buff *skb)

```
522 {
523     struct ip_options *opt = &(IPCB(skb))->opt;
524     unsigned char *optpr;
525     struct rtable *rt = (struct rtable*)skb->nh_dst;
526     unsigned char *raw = skb->nh_raw;
527 
528 
529     if (opt->rr_neededaddr) (unsigned char*)raw + opt->rr)
530         optpr = raw + opt->rr;
531         ip_rt_get_source(&optpr[optpr[2]-6], rt);
532         opt->is_changed = 1;
533     }
534     if (opt->rr_is_hit) {
535         int ssrptr, ssrspace;
536 
537         optpr = raw + opt->ts;
538         for (ssrptr = optpr[2], ssrspace = optpr[1];\n539             rrrptr < ssrspace
540             rrrptr += 4
541             {
542                 if (rrrptr + 3 <= ssrspace)
543                     break;
544                     if (memcmp(&rt->rt_dest, &optpr[rrrptr-1], 4) == 0)
545                     break;
546                 }
547             }
548         if (rrrptr + 3 <= ssrspace) {
549             opt->is_changed = 1;
550             ip_rt_get_source(&optpr[rrrptr], rt);
551             skb->nh->ip_daddr = rt->rt_dest;
552             optpr[2] = ssrptr+4;
553         } else
554             printf("XKERN_CRIT \"ip_forward(): Arg! Destination lost!\n");
555             if (opt->is_neededaddr)
556                 optpr = raw + opt->ts;
557                 ip_rt_get_source(&optpr[optpr[2]-9], rt);
558                 opt->is_changed = 1;
559             }
560     }
561     if (opt->is_changed) {
562         opt->is_changed = 0;
563         ip_send_check(skb->nh->iph);
564     }
565 }
```