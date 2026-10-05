# Figure 6.7 IP output-multicast replication: linux/net/ipv4/ip_output.c.

```
234      * Multicasts with ttl 0 must not go beyond the host */
235
236      if (skb->skb_ip->ttl == 0) {
237          kfree_skb(skb);
238          return 0;
239      }
240  }
241  
242      if (rt->rt_flags&RTCF_CAST) {
243          struct skb_buff *newskb = skb_clone(skb, GFP_ATOMIC);
244          if (newskb) {
245              NF_HOOK(NF_INET, NF_IP_POST_ROUTING, newskb, NULL,
246                          newskb->dev, ip_dev_loopback_xmit);
247          }
248      }
249      return ip_finish_output(skb);
250  
```

# Figure 6.8 IP output–queue for sending: linux/net/ipv4/ip_output.c.

```
252  int ip_output(struct sk_buff *skb)
253  {
254      #ifdef CONFIG_IP_ROUTE_NAT
255          struct rtable *rt = (struct rtable*)skb)->dst;
256      #endif
257
258
259          IP_INC_STATS(IPOutRequests)
260      #ifdef CONFIG_IP_ROUTE_NAT
261          if (rt->rt_flags&RTCF_NAT) 
262              ip_do_nat(skb);
263      #endif
264
265      return ip_finish_output(skb);
266  } 
```

# Figure 6.9 IP output-queue for sending–part 2i: linux/net/ipv4/ip_output.c.

```
268  /* Queues a packet to be sent, and starts the transmitter if necessary.
269      * This routine also needs to put in the total length and compute the
270      * checksum. We use this in two stages, ip_builder_header() to
271      * this, but that scheme creates a mess when routes disappeared etc.
272      * So we do it all here, and the TCP send engine has been changed to
273      * match. (No more unreliable FIN disasters, etc. whee..) This will
274      * most likely other reliable transport layers above IP easier
275      * to implement under Linux.
276      */
```