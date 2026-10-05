
# TCP/IP and Linux Protocol Implementation

# Figure 6.152 ICMP transmit rate limiter-token bucket: linux/net/ipv4/icmp.c.

```c
388 /*
389    Check transmit rate limitation for given message.
390    The rate information is held in the destination cache now.
391    This function is generic and could be used for other purposes
392    too. It uses a Token bucket filter as suggested by Alexey Kuznetsov.

394    Note that the det_entry fields are modified by functions in
395    route.c too, but these work for packet destinations while xrlim_allow
396    works for icmp destinations. This means the rate limiting information
397    for one "ip object" is shared.

399    Note that the same det_entry fields are modified by functions in
400    route.c too, but these work for packet destinations while xrlim_allow
401    works for icmp destinations. This means the rate limiting information
402    for one "ip object" is shared - these ICMPs are twice limited:
403    by source and destination.

405    RFC 1812: 4.3.2.8 SHOULD be able to limit error message rate
406        SHO allow setting of rate limits

408    /*
409    Shared between ICMP4 and ICMP6.
410    #define XLIM_BURST_FACTOR 6
411    int xrlim_allow(struct det_entry *dest, int timeout)
412    {
413        unsigned long now;

415        now = dest->rate_tokens += dest->rate_limit;

417        dest->rate_tokens = now;
418        if (dest->rate_tokens >= XLIM_BURST_FACTOR*timeout)
419            dest->rate_tokens -= XLIM_BURST_FACTOR*timeout;
420        if (dest->rate_tokens >= timeout) {
421            dest->rate_tokens = timeout;
422            return 1;
423        }
424        return 0;
425    }
```

# Figure 6.153 ICMP transmit rate limiter xrlim_allow(struct rtable *rt, int type, int code) linux/net/ipv4/icmp.c.

```c
427 static inline icmpv4_struct(struct rtable *rt, int type, int code)
428 {
429 struct det_entry *dest = rt->u.dest;

431 if (type != NR_ICMP_TYPES || icmp_pointers[type].timeout)
    /* Redirect has its own rate limit mechanism */
    if (type == ICMP_REDIRECT)
        return 1;

    /* No rate limit on loopback */
    if (dst->dev && (dst->dev->flags&IFF_LOOPBACK))
        return 1;

    return xrlim_allow(dst, icmp_pointers[type].timeout);
}
```

**Figure 6.154** ICMP/SNMP statistics counters: linux/net/ipv4/icmp.c.

```c
/*
 * Maintain the counters used in the SNMP statistics for outgoing ICMP
 */
static void icmp_out_count(int type)
{
    if (type>=NR_ICMP_TYPES)
        return;
    (icmp_pointers[type].output)[(smp_processor_id)*2+in_softirq(*)]*sizeof(struct icmp_mib)
        /sizeof(unsigned long)]++;
    ICMP_INC_STATS(IcmpOutMsg);
}
```

**Figure 6.155** ICMP checksum: linux/net/ipv4/icmp.c.

```c
static void icmp_out_count(int type)
{
    if (type>=NR_ICMP_TYPES)
        return;
    (icmp_pointers[type].output)[(smp_processor_id)*2+in_softirq(*)]*sizeof(struct icmp_mib)
        /sizeof(unsigned long)]++;
    ICMP_INC_STATS(IcmpOutMsg);
}

/*
 * Check each fragment, and on the first include the headers and final checksum.
 */
static int icmp_glue_bits(const void *p, char *to, unsigned int offset, unsigned int fraglen)
{
    struct icmp_bwm *icmp_param = (struct icmp_bwm *p);
    struct icmpphdr *icmp;
    unsigned long csum;

if (offset) {
    icmp_param->csum=csum_partial_copy_nocheck(icmp_param->data_ptr+offset-sizeof(
        struct icmphdr),
    to, fraglen,icmp_param->csum);
    return 0;
}
/*
 First fragment includes header. Note that we've done
the other fragments first, so that we check the checksum
for the whole packet.
*/
csum = csum_partial_copy_nocheck((void *)icmp_param->icmp,
    to, sizeof(struct icmphdr),
    icmp_param->csum=csum;
csum = csum_partial_copy_nocheck(icmp_param->data_ptr,
    to, sizeof(struct icmphdr),
    fraglen-sizeof(struct icmphdr), csum);
icmp((struct icmphdr *)to;
icmp->checksum = csum_fold(csum);
return 0;
}
```

# Figure 6.156 ICMP reply: linux/net/ipv4.c

```c
void icmp_reply(struct icmp_bwm *icmp_param, struct sk_buff *skb) {
    struct sock *sk=skb->sk;
    struct icmp_pc *ipc;
    struct rtable *rt = (struct rtable*)skb->dst;
    u32 daddr;

    if (!ip_options(&icmp_param->replyopts, skb)) {
        return 0;
    }

    if (!icmp_xmit_lock()) {
        return 0;
    }

    icmp_param->icmp->checksum=0;
    icmp_param->csum=0;
    icmp_out_count(icmp_param->type);

    sk->proto=skb->nh->tos;
    daddr = rt->src;
    ipc->opt = NULL;
    if (icmp_param->replyopts) {
        ipc->opt = &icmp_param->replyopts;
        if (ipc->opt->srr)
            daddr = icmp_param->replyopts.faddr;
    }
    if (!ip_route_output(rt, daddr, rt->dst, RT_TOS(skb->nh->tos), 0)) {
        goto out;
    }
out:
if (icmpv4_allow(rt, icmp_param->type, icmp_param->code)) {
  ip_build_xmit(sk, icmp_glue_bits, icmp_param,
  icmp_param->data_len+sizeof(struct icmphdr),
  &ipc, rt, MSG_DONTWAIT);
}
ip_put(rt);
out:
  icmp_xmit_unlock(bh());
}
```

# 6.157 ICMP send: linux/net/ipv4/icmp.c

```c
void icmp_send(struct sk_buff *skb_in, int type, int code, unsigned long info)
{
  struct iphdr *iph;
  struct icmphdr *icmp;
  int root;
  struct icmp_xmit *icmp_param;
  struct rtable *rt = (struct rtable*)skb_in->dst;
  struct icmp_cookie ipc;
  u32 saddr;
  u8 tos;
  if (!rt)
    return;
/* Find the original header */
  iph = skb_in->nh->iph;
/* No replies to multicast/broadcast */
  if (skb_in->nh->type==PACKET_HOST)
    return;
/* Now check at the protocol level */
if (rt->rt_flags&(RTC_BROADCAST|RTC_MULTICAST))
  return;
/* Only reply to Fragment 0. We re-order the constant mask for efficiency. */
if (iph->frag_off&htons(IP_OFFSET))
  return;

/* Avoid recursive ICMP errors */
```

# Figure 6.158 ICMP send: linux/net/ipv4/icmp.c.

```c
/*
 * If we send an ICMP error to an ICMP message would result in.
 */
if (icmp_pointers[type].error) {
    /*
     * We are an error, check if we are replying to an ICMP error
     */
    if (iph->protocol==IPPROTO_ICMP) {
        icmp = (struct icmphdr*)((char*)iph + (iph->ihl<<2));
        /*
         * Assume any unknown ICMP type is an error. This isn't
         * specified by the RFC, but think about it.
         */
        if (icmp->type!=NR_ICMP_TYPES || icmp_pointers[icmp->type].error)
            return;
    }
}

if (icmp_xmit_lock()) {
    return;
}

/*
 * Construct source address and options.
 */
#ifdef CONFIG_IP_ROUTE_NAT
    /*
     * Restore original addresses if packet has been translated.
     */
    if (rt->rt_flags&RTC_NAT & iph(skb_in)->flags|IP_TRANSLATED) {
      iph->daddr = rt->key.dst;
      iph->saddr = rt->key.src;
    }
#endif

    saddr = iph->daddr;
    if (!(rt->rt_flags&RTC_LOCAL))
      saddr = 0;
    tos = icmp_pointers[type].error =
      ((ip->tos & IPTOS_INTERNET_MASK) | IPTOS_PREC_INTERNET_CONTROL) :
      ip->tos;
```

# Figure 6.159 ICMP send: linux/net/ipv4/icmp.c.

```c
/*
 * XXX: use more aggressive expire for routes created by
* this call (not longer than the rate limit timeout).
* It could be worthwhile to not put them into fast routing
* Otherwise an attacker can grow the routing table.
 */
if (!ip_route_output(&art, icmp_param->replyopts.faddr, saddr, RT_TOS(skb->nh->tos), 0))
  goto out;
```

# Figure 6.160 ICMP send: linux/net/ipv4/icmp.c.

```c
if (!icmpv4_allow(rt, type, code))
  goto out;

/* RFC says return as much as we can without exceeding 576 bytes. */

room = rt->dst.pmtu;
if (room > 576)
  room = 576;
```
