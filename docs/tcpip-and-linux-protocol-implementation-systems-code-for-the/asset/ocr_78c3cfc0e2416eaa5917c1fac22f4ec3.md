# TCP/IP and Linux Protocol Implementation

Figure 8.70 FIB rules—initialization: linux/net/ipv4/fib_rules.c.

```
384 extern __inline__ int net_fill_rule(struct sk_buff *skb,
385                             struct fib_rule *r,
386                             struct netlink_callback *cb)
387 
388 {
39     struct rmsg *rtm;
390     struct nmsghdr *nlsh;
391 unsigned char *b = skb->tail;
392 
393 nlsh = NLMSG_PUT(skb, NETLINK_CODES(cb)->skb_pid, cb->nlms_nmsg_seq, RTM_NEWRULE, sizeof
394 rtm = NLMSG_DATA(nlsh);
395 rtm->rtm_family = AF_INET;
396 rtm->rtm_dst_len = r->r_dst_len;
397 rtm->rtm_src_len = r->r_src_len;
398 rtm->rtm_tos = r->r_tos;
399 #ifdef CONFIG_ROUTE_FMWARK
400 if (r->r_fwmark) {
401     RTA_PUT(skb, RTA_PROTOINFO, 4, &r->r_fwmark);
402 }\endif
403 rtm->rtm_table = r->r_table;
404 rtm->rtm_scope = 0;
405 rtm->rtm_types = r->r_action;
406 rtm->rtm_flags = r->r_flags;
407 
408 if (r->r_dst_len)
409     RTA_PUT(skb, RTA_DST, &r->r_dst);
410 if (r->r_src_len)
411     RTA_PUT(skb, RTA_SRC, 4, &r->r_src);
412 if (r->r_ifname[0])
413     RTA_PUT(skb, RTA_IF, IFNSIZ, &r->r_ifname);
414 if (r->r_preference)
415     RTA_PUT(skb, RTA_PRIORITY, 4, &r->r_preference);
416 if (r->r_srcmp)
417     RTA_PUT(skb, RTA_GATEWAY, 4, &r->r_srcmp);
418 #ifdef CONFIG_NET_CLS_CLS
419 if (r->r_classid)
420     RTA_PUT(skb, RTA_FLOW, 4, &r->r_classid);
421 }\endif
422 nlh->nlmsg_len = skb->tail - b;
423 return skb->len;
424 
425 nlmsg_failure:
426 rtattr_failure:
427     skb_put(skb, b - skb->tail);
428     return -1;
429 }
```