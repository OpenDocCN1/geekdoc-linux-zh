# Infrastructure Protocols 357

```
480 static struct mfc_cache *ipmr_cache_alloc_unres(void)
481 {
482     struct mfc_cache *c=kmem_cache_alloc(art_cache, GFP_ATOMIC);
483     if(c==NULL)
484         return NULL;
485     memset(c, 0, sizeof(*c));
486     skb_queue_head_init(&c->mfc_un.unres.unresolved);
487     c->mfc_un.unres.expires = jiffies + 10*HZ;
488     return c;
489 }
```

Figure 6.212 IPMR–route cache entries: linux/net/ipv4/ipmr.c.

```
/*
 *   A cache entry has gone into a resolved state from queued
 */
nstatic void ipmr_cache_resolve(struct mfc_cache *uc, struct mfc_cache *c)
{
    struct sk_buff *skb;

    /*
     *   Play the pending entries through our router
     */
    while ((skb=skb_dequeue(&uc->mfc_un.unres.unresolved))) {
n##ifdef CONFIG_RTNETLINK
        if (skb->nh.ip->version == 0) {
            int err;
            struct nlmsghdr *nlh=(struct nlmsghdr*)skb_pull(skb, sizeof(struct iphdr));
            
            if (ipmr_fill_route(skb, c, NLMS_DATA(nlh)) > 0) {
                nlh->nlms_len = skb->tail-(unsigned*)skb;
            } else {
                nlh->nlms_type = NLMS_ERROR;
                nlh->nlms_len = NLMS_LENGTH(sizeof(struct nlmsgerr));
                skb_trim(skb, nlh->nlms_len);
                (struct nlmsgerr*)HDR(nlh))->error = -EMSAGESIZE;
            }
        }
        err = netlink_unicast(rtnl, NETLINK_CB(skb)->dst_id, MSG_DONTWAIT);
}
ip_mfr_forward(skb, c, 0);
}
#endif
```