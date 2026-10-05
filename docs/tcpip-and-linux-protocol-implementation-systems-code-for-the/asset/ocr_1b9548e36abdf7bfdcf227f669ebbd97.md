# 392 TCP/IP and Linux Protocol Implementation

```
401      rel_type = ICMP_DEST_UNREACH;
402      rel_code = ICMP_HOST_UNREACH;
403  break;
404  }
405  break;
```

Figure 2.623 IP in IP--ICMP error handling: linux/net/ipv4/ip.c

```
406  case ICMP_TIME_EXCEEDED:
407      if (code != ICMP_EX_TTL)
408          return;
409      break;
410  }
```

Figure 2.624 IP in IP--ICMP error handling: linux/net/ipv4/ip.c +/

```
412  /* Prepare skb to feed to icmp_send *//
413  skb2 = skb_clone(skb, GFP_ATOMIC);
414  if (skb2 == NULL)
415      return;
416  dst_release(skb2->dst);
417  skb2->dst = NULL;
418  skb_pull(skb, skb->data - (u8*)eiph);
419  skb2->nh->raw = skb2->data;
420
421  /* Try to guess incoming interface *//
422  if (ip_route_output(krt, eiph->saddr, 0, RT_TOS(eiph->tos)), {
423      kfree_skb(skb2);
424      return;
425  }
426  skb2->dev = rt->u.dst.dev;
427
428  /* route "incoming" packet * *//
429  if (rt->rt_flags&RTCF_LOCAL) {
430      ip_put(rt);
431      if (rt == NULL)
432          if (ip_route_output(krt, eiph->daddr, eiph->saddr, eiph->tos), 0) {
433              rt->u.dst->dev->type = ARPHRD_IPGRE;
434              ip_put(rt);
435              kfree_skb(skb2);
436          return;
437      }
438  } else {
439      ip_put(rt);
440      if (ip_route_input(skb2, eiph->daddr, eiph->saddr, eiph->tos, skb2->dev) ||
441          skb2->dst->dev->type != ARPHRD_IPGRE) {
442              kfree_skb(skb2);
443          return;
444      }
445  }
```