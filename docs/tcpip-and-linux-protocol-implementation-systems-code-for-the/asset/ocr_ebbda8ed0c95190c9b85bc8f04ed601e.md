# TCP/IP and Linux Protocol Implementation

```
277 static inline ip_queue_xmit2(struct sk_buff *skb)
278 {
279 struct sock *sk = skb->;
280 struct rtable *rt = (struct rtable *)skb->dst;
281 struct net_device *dev;
282 struct iphdr *iph = skb->nh->iph;
284 dev = rt->u.dst;
```

* This can happen when the transport layer has segments queued
* with a cached route, and by the time we get here things are
* re-routed to a device with a different MTU than the original
* device. Sick, it must cover it.

```
/*
291 if (skb_headroom(skb) < dev->header_len && dev->header_len)
292 struct skb_buff *skb2;
294 skb2 = skb_alloc_headroom(skb, dev->header_len + 15) & ~15);
295 kfree_skb(skb);
296 if (skb2 == NULL)
297 return -ENOMEM;
298 if (sk)
299 skb_select_owner_v(skb, sk);
300 skb = skb2;
301 iph = skb->nh->iph;
303 }
305 if (skb->len > rt->u.dst.pmtu)
306 goto fragment;
```

6.10 output-queue for sending--part 2ii: linux/net/ipv4/ip_output.c.

```
307 if (ip_dont_fragment(sk, &rt->u.dst))
308 iph->frag_off |= __constant_htons(IP_DF);
310 ip_select_ident(sk, &rt->u.dst);
312 /* Add an IP checksum. */
313 ip_send_check(iph);
315 skb->priority = sk->priority;
316 return skb->dst->output(skb);
318 fragment:
319 if (ip_dont_fragment(sk, &rt->u.dst)) {
320 /* Reject packet ONLY IF TCP might fragment
321 * it itself, if we were careful enough.
323 */
324 iph->frag_off |= __constant_htons(IP_DF);
325 NETDEBUG(printk(KERN_DEBUG "sending packet_too_big to send %s\n", ...)
326 icmp_send(skb, ICMP_DEST_UNREACH, ICMP_FRAG_NEEDED,
```