# TCP/IP and Linux Protocol Implementation

```
473 fraglen = maxfraglen;
474 offset = maxfraglen-fragheaderlen;
475 
476 }
477 /*
478 * The last fragment will not have MF (more fragments) set.
479 */
480
481 mf = 0;
```

Figure 6.16 IP output--classic building of IP packet: linux/net/ipv4/ip_output.c.

```
483 /*
484 * Don't fragment packets for path mtu discovery.
485 */
486
487 if (offset > 0 && sk->proto->af_inet.pmudisc==PMTUDISC_DO) {
488 ip_local_error(sk, EMSGSIZE, rt->dst, sk->dport, mtu);
489 return -EMGSSIZE;
490 }
491 if (flags&MSG_PROBE)
492 goto out;
```

# 6.2.2 Fragmentation

Here is IP output loops over a buffer that is bigger than the MTU size, and generates fragments to send.

Figure 6.17 IP output--classic building of IP packet: linux/net/ipv4/ip_output.c.

```
494 /*
495 * Begin outputting the bytes.
496 */
497
498 do {
499 char *data;
500 struct sk_buff *skb;
501
502 /*
503 * Get the memory we require with some space left for alignment.
504 */
505
506 skb = sock_alloc_send_skb(sk, fraglen+hb_len+15, 0, flags&MSG_DONTWAIT, &err);
507 if (skb == NULL)
508 goto error;
509
510 /*
```