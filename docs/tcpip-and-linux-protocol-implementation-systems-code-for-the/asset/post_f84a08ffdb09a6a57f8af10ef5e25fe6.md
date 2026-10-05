
# 414 TCP/IP and Linux Protocol Implementation

```c
850      } 
851      if (tunnel->parms.o_flags&GRE_KEY) {
852          *ptr = tunnel->parms.o_key;
853          ptr--;
854      }
855      
856      if (tunnel->parms.o_flags&GRE_CSUM) {
857          *ptr = 0;
858          *(u16*)ptr = compute_csum(void*)(ipb+1), skb->len - sizeof(struct
859              iphdr);
860      }
861      } 
862  #ifdef CONFIG_NETFILTER
863      mf_construct_put(skb->nfctr);
864      skb->nfctr = NULL;
865      #ifdef CONFIG_NETFILTER_DEBUG
866          skb->nf_debug = 0;
867      #endif
868  #endif
870  IPTUNNEL_XMIT();
871      tunnel->recursion--;
872      return 0;
873  
874  tx_error_icmp:
875      dst_link_failure(skb);
876  
877  tx_error:
878      stats->to_tx_errors++;
879      dev_kfree_skb(skb);
880      tunnel->recursion--;
881      return 0;
882  }
```

# ICMP in GRE Tunnels

Care needs to be taken in mapping the causes of ICMP messages when they emanate within or outside a tunnel.

**Figure 6.299** tunnels--error/ICMP cases: linux/net/ipv4/ip_gre.c.

```c
316  void ipgre_err(struct sk_buff *skb, unsigned char *dp, int len)
317  {
318      #ifdef I_IF_WISH_WORD_PER_PERFECT
320      /* It is not :-( All the routers (except Linux) return only
321          8 bytes of packet payload. It means, that precise relaying of
322          ICMP in the Real Internet is absolutely infeasible.
323      */
324      Moreover, Cisco "wise men" put GRE to the third word
325      GRE header. It makes impossible maintaining soft state for keyed
326      GRE tunnels with enabled checksum. Tell them "thank you".
327      Well, I wonder, rfc1812 was written by Cisco employee,
328      what hell these idiots established by himself
329      /*
333      struct iphdr *iph = (struct iphdr *)(dp);
334      u16 *p = (u16*)(dp+(iph->ihl << 2));
335      int grehlen = skb->h.icmp->type << 4;
336      int type = skb->h.icmp->code;
337      int code = skb->h.icmp->code;
338      struct ip_tunnel *t;
340      u16 flags;
341      flags = 0;
342      if (flags&(GRE_CSUM|GRE_KEY|GRE_SEQ|GRE_ROUTING|GRE_VERSION)) {
343      if (flags&(GRE_VERSION|GRE_ROUTING)) {
344          return;
345          if (flags&GRE_KEY) {
346          grehlen += 4;
347          if (flags&GRE_CSUM) {
348          grehlen += 4;
349          }
350      }
352      /* If only 8 bytes returned, keyed message will be dropped */
353      if (len < grehlen) {
354          return;
356      switch (type) {
357      default:
358      case ICMP_PARAMETER:
359          return;
360
361      case ICMP_DEST_REACH:
362      switch (code) {
363      case ICMP_SR_FAILED:
364      case ICMP_PORT_REACH:
365          /* Impossible event. */
366          return;
367      case ICMP_FRAG_NEEDED:
368          /* Soft state pmtu is maintained by IP core. */
369          return;
370      default:
371          /* All others are translated to HOST_REACH,
372          rfc2003 contains "deep thoughts" about NET_REACH,
373          I believe they are just ether pollution.
374      */
375  break;
376  break;
377  case ICMP_TIME_EXEDED:
378  if (code != ICMP_EXC_TTL)
379  return;
380  break;
381  }
```

Figure 6.301 GRE tunnels--error/ICMP cases: linux/net/ipv4/ip_gre.c.

```c
read_lock(&ipgre_lock);
t = ipgre_tunnel_lookup(iph->daddr, iph->saddr, (flags&GRE_KEY) ? 7 * ((u32*)p) + (grehlen>>2) : 1) : 0;
if (t->parms == NULL || t->parms.daddr == 0 || MULTICAST(t->parms.daddr))
goto out;

if (t->parms.ttl == 0 && type == ICMP_TIME_EXEDED)
goto out;

if (jiffies - t->err_time < TUNNEL_ERR_TIMEOUT)
t->err_count++;
else
t->err_count = 1;
t->err_time = jiffies;
out:
read_lock;
```c
else
struct iphdr *iph = (struct iphdr*)dp;
struct iphdr *eiph;
u16 *p = (u16)(dp+(iph->ihl<<2));
int type = skb->h.icmp->type;
int code = skb->h.icmp->code;
int rel_type = 0;
int rel_code = 0;
int rel_info = 0;
u16 flags;
int grehlen = (iph->ihl<<2) + 4;
struct sk_buff *skb;
struct rtable *rt;
```c
if (p[1] != __constant_htons(ETH_P_IP))
return;
flags = p[0];
if (flags&(GRE_CSUM|GRE_KEY|GRE_SEQ|GRE_ROUTING|GRE_VERSION)) {
if (flags&(GRE_VERSION|GRE_ROUTING)) {
return;
    if (flags&GRE_CSUM)
    grehlen += 4;
    if (flags&GRE_KEY)
    grehlen += 4;
    if (flags&GRE_SEQ)
    grehlen += 4;
}
if (len < sizeof(struct iphdr))
return;
eiph = (struct iphdr)(dp + grehlen);
```c
switch (type) {
    default:
        return;
    case ICMP_PARAMETER:
        if (skb->h.icmp->type < (iph->ihl<<2))
        return;
    /* So... This guy found something encapsulated.
    Well, he is fool, but what can we do? */
        rel_type = ICMP_PARAMETER;
        rel_info = skb->h.icmp->type - grehlen;
        break;
    case ICMP_DEST_REACH:
        switch (code) {
            case ICMP_SR_FAILED:
            case ICMP_PORT_REACH:
                /* Impossible event. */
                return;
            case ICMP_FRAG_NEEDED:
                /* And it is the only thing */
                rel_info = ntohs(skb->h.icmp->mtu);
                if (len < grehlen+6)
                return;
                rel_info -= grehlen;
                /* BSD DOES NOT EXIST IN NATURE. */
                if (rel_info > ntohs(eiph->tot_len))
                return;
            default:
                /* All others are translated to HOST_REACH,
                rfc2003 contains "deep thoughts" about NET_REACH,
                I believe, it is either pollution. */
                rel_type = ICMP_DEST_REACH;
                rel_code = ICMP_HOST_REACH;
                break;
        }
    case ICMP_TIME_EXEDED:
        if (code != ICMP_EXC_TTL)
        return;
        break;
}
```

Figure 6.304 GRE tunnels--error/ICMP cases: linux/net/ipv4/ip_gre.c.

```c
/* Prepare fake skb to feed to icmp_seed */
skb2 = skb_clone(skb, GFP_ATOMIC);
if (skb2 == NULL)
return;
dst_release(skb2->dst);
skb2->dst = NULL;
skb_pull(skb2, skb->data - (u8*)eiph);
skb2->nh.data = skb2->data;
/* Try to guess incoming interface */
if (ip_route_output(art, eiph->saddr, 0, RT_TOS(eiph->tos), 0))
return;
free_skb(skb2);
skb2->dev = rt->u.dst.dev;
```

```c
/* "incoming" packet */
if (rt->rt_flags&RTCF_LOCAL) {
    ip_rt_put(rt);
    rt = NULL;
    if (ip_route_output(art, eiph->daddr, eiph->saddr, eiph->tos, 0))
    rt->u.dev->type != ARHARD_IPGRE);
    ip_rt_put(rt);
    free_skb(skb2);
    return;
} else {
    ip_rt_put(rt);
    if (ip_route_input(skb, eiph->daddr, eiph->saddr, eiph->tos, skb2->dev))
    skb2->dst->dev->type != ARHARD_IPGRE);
    free_skb(skb2);
    return;
}
}
/* to change mtu on this route */
if (type == ICMP_DEST_REACH && code == ICMP_FRAG_NEEDED) {
  if (rel_info && skb2->dst->pmtu) {
    free_skb(skb2);
    return;
  }
  skb2->dst->pmtu = rel_info;
  rel_info = btom(rel_info);
} else if (type == ICMP_TIME_EXEDED) {
  struct ip_tunnel *t = (struct tunnel*)skb2->dev;
  if (t->parms.iph) {
    rel_type = ICMP_DEST_REACH;
    rel_code = ICMP_HOST_REACH;
  } 
  icmp_send(skb2, rel_type, rel_info);
  free_skb(skb2);
}
#endif
}
```

Figure 6.306 GRE tunnels--ECN decapsulate: linux/net/ipv4/ip_gre.c.

```c
static inline void ipgre_ecn_decapsulate(struct ihdr *iph, struct sk_buff *skb) {
  #ifdef CONFIG_INET_ECN
    u8 inner = 0;
    if (skb->protocol == __constant_htons(ETH_P_IP)) {
      inner = old_iph->tos;
    else if (skb->protocol == __constant_htons(ETH_P_IPV6)) {
      inner = ip6_get_dsfield((struct ipv6hdr*)old_iph);
    }
    return INET_ECN_encapsulate(tos, inner);
  #else
    return tos;
  #endif
}
```
