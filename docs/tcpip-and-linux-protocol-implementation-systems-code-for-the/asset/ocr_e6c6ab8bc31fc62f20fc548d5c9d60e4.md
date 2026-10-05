# TCP/IP and Linux Protocol Implementation

```
688      mp_head->rta_type = RTA_MULTIPATH;
689      mp_head->rta_len = skb->tail - (u8*)mp_head;
690  }
691  #endif
692  nlh->nlmsg_len = skb->tail - b;
693      return skb->len;
694
695  nlmsg_failure:
696  rtattfr_failure:
697      skb_trim(skb, b - skb->data);
698      return -1;
699  }
```

# Taking an RTNlink Request

![](bbox=[0.118, 0.386, 0.814, 0.401])

```
705  int
706  fib_convert_rtentry(int cmd, struct nlmshdr *nl, struct nl *attr, struct rtmsg *rtm,
707      struct kern_rta *rta, struct rtentry *r)
708  {
709      int plen;
710         u32 *ptr;
711      memset(rtm, 0, sizeof(*rtm));
712      memset(rta, 0, sizeof(*rta));
713
714      if (r->rt_dst->family != AF_INET)
715          return -EAFNOSUPPORT;
716
717      /* Check mask for validity:
718          a) it must be contiguous.
719          b) destination must have all host bits clear.
720          c) if application forgot to set correct family (AF_INET),
721              reject unless it is absolutely clear i.e.
722              both family and mask are zero.
723*/
724      plen = 32;
725      ptr = ((struct sockaddr_in*)r->rt_dst)->sin_addr.s_addr;
726      if ((r->rt_flags & RTF_ROUTE)) {
727          u32 mask = ((struct sockaddr_in*)r->rt_genmask))->sin_addr.s_addr;
728          if (r->rt_genmask.sa_family != AF_INET) {
729              if (mask | r->rt_genmask.sa_family) {
730                  return -EAFNOSUPPORT;
731              }
732          }
733          if (bad_mask(mask, ptr)) {
734              return -EINVAL;
735          }\plen = inet_mask_len(mask);
736      }
737}
738  nl->nlmsg.flags |= NLM_F_REQUEST;
```