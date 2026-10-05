# 3.2.3 IP Output Work

TCP calls IP functions to carry out output. Some of this work is structured as follows, and a relevant extract from the code is illustrated in Figure 3.4 following.

```
ip_output.c:
ip_queue_xmit()
ip_route_output()
f_HOOK()
```

ip_route_output() is an inline function defined in linux/include/net/route.h and interfaces to ip_route_output_key(), which is explained in Chapter 8. NF_HOOK() is part of the network filter support in Linux that is machine-ery to do the low-level work for firewalls and other functions, and is discussed in more detail in Chapter 10.

```
netfilter.h:
NF_HOOK(pf, hook, skb, indev, outdev, okfn)
NF_hook_slow((pf), (hook), (skb), (indev), (outdev), okfn)
ip_queue_xmit(
skb->dst_output(skb)
```

This queues, or calls okfn(), which maps to op..queue_xmit(). The skb->dst structure was filled by a local route lookup and is a link-level output

In ip_queue_xmit, header changes are as follows:

Figure 3.4 Filling in key IP bits: linux/net/ipv4/ip_output.c.

```
/ OK, we know where to send it, allocate and bind IP header. */
(struct iphdr *)skb->push(skb, sizeof(struct iphdr) + (opt ? opt->len : 0));
(* (u16 *)htons(4 << 12) | (5 << 8) | (skb->proto.af_inet.tos & 0xff));
ip->to_len = htons(skb->len);
ip->frag_offset = 0;
ip->ttl = skb->proto.af_inet.ttl;
ip->protocol = skb->protocol;
ip->saddr = rt->rt_src;
ip->daddr = rt->rt_dst;
skb->nh.ip = ip;
/* Transport layer set skb->nh.h.h.foo itself. */
```

This is covered in detail in Chapter 6.

# 3.2.4 Link-Level Output

Output at the link level can be complex (see Chapter 8). It includes specific technical details of driving devices, but also the important part is that this is