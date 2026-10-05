# Routing 581

```
640 nhb = NLMSG_PUT(skb, pid, seq, event, sizeof(*rtmn))
641 rtm = NLMSG_DATA(nhb);
642 rtm->rtm_family = AF_INET;
643 rtm->rtm_dest = dst_len;
644 rtm->rtm_src = 0;
645 rtm->rtm_tos = tos;
646 rtm->rtm_table = tb_id;
647 rtm->rtm_type = type;
648 rtm->rtm_flags = fi->fib_flags
649 rtm->rtm_scope = scope;
650 if (rtm->rtm_dst_len)
651 RTM_PUT(skb, RTA_DST, 4);
652 rtm->rtm_protocol = fi->fib_protocol;
653 if (fi->fib_priority)
654 RTM_PUT(skb, RTA_PRIORITY, 4, &fi->fib_priority);
655 #ifdef CONFIG_CLS_ROUTE
656 if (fi->fib_nh(0)->nh_classid)
657 RTM_PUT(skb, RTA_FLAW, 4, &fi->fib_nh(0)->classid);
658 #endif
659 if (rtnetlink_put_metrics(skb, fi->fib_metrics) < 0)
660 goto rtattr_failure;
661 if (fi->fib_presrc)
662 RTM_PUT(skb, RTA_PREFSRC, 4, &fi->fib_presrc);
663 if (fi->fib_nh->nh_oif)
664 RTM_PUT(skb, RTA_GATEWAY, 4, &fi->fib_nh->nh_gw);
665 if (fi->fib_nh->nh_oif)
666 RTM_PUT(skb, RTA_OIF, sizeof(int), &fi->fib_nh->nh_oif);
667 
668
```

Figure 8.49 fib semantics-dump iii: linux/net/ipv4/fib_semantics.c

```
669 #ifdef CONFIG_IP_ROUTE_MULTIPATH
670 if (fi->fib_nh > 1)
671 struct rtnextthop *nmp;
672 struct rtattr *mp_head;
673 if (skb_tailroom(skb) < RTA_ALIGN(0))
674 goto rtattr_failure;
675 mp_head = (struct rtattr*)skb_put(skb, RTA_SPACE(0));
676
677 for (...)
678 if (skb_tailroom(skb) < RTA_ALIGN(RTA_ALIGN(sizeof(*nmp)) + 4))
679 goto rtattr_failure;
680 nmp = (struct rtnextthop*)skb_put(skb, RTA_ALIGN(sizeof(*nmp)));
681 nmp->rtnh_flags = nh->nh_flags & 0xFF;
682 nmp->rtnh_bops = nh->nh_weight-1;
683 nmp->rtnh_ifindex = nh->nh_oif;
684 if (nmp->rtnh_nh_go)
685 RTM_PUT(skb, RTA_GATEWAY, 4, &nh->nh_gw);
686 nmp->rtnh_len = skb->tail - (unsigned char*)nmp;
687 } endif_next(fi);
```