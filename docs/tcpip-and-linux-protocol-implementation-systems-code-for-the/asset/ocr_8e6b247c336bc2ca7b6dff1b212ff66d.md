# Infrastructure Protocols 445

```
117 dev_queue_xmit,
118 dev_queue_xmit,
119 dev_queue_xmit,
120 dev_queue_xmit
121 };
```

Essentially, if a network supports broadcast, then this is used to propagate messages to find out who is there. An example of such a message is the neighbor advertisement. It is ARP, but uses the ICMPv6 message formats. We'll just look at this one—others are similarly constructed.

Figure 6.349 IPv6 neighbor advertisement: linux/net/ipv6/ndisc.c.

```
317 /*
318  Send a Neighbour Advertisement
319  */
320 void ndisc_send_na(struct net_device *dev, struct neighbour *neigh,
321      struct in_addr +daddr, struct in6_addr +solicited_addr,
322      int router, int solicited, int override, int inc_opt)
324 {
325     struct sock *sk = ndisc_socket->sk;
326     struct nd_msg *msg;
327     int len;
328     struct sk_buff *skb;
329     int err;
330
331     len = sizeof(struct icmp6hdr) + sizeof(struct in6_addr);
332
333     if (inc_opt) {
334         if (dev->addr_len != NDISC_OPT_SPACE(dev->addr_len))
335             len += len
336         else
337             inc_opt = 0;
338     }
339
340     skb = sock_alloc_skb(sk, MAX_HEADER + len + dev->header_len + 15,
341                               0, 0, kerr);
342
343     if (skb == NULL) {
344         ND_PRINTK("send_na: alloc skb failed\n");
345
346         return;
347     }
348
349     if (ndisc_build_ll1_hdr(skb, dev, daddr, neigh, len) == 0) {
350         xfree_skb(skb);
351         return;
352     }
353     ip6_nd_hdr(sk, sk, dev, solicited_addr, IPPROTO_ICMP6, len);
```