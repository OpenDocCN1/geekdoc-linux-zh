
# Infrastructure Protocols 359

```c
571  skb->nh_iph = (struct iphdr*)skb_put(skb, ihl);
572  memcc(skb->data,data, ihl);
573  skb->nh_iph->protocol = 0;
574                              /* Flag the kernel that this is a route add */
575  msg = (struct igmpmsg*)skb->nh_iph;
576  msg->im_vif = vifi;
577  skb->dst = dst_clone(pkt->dst);
578
579  /*
580      Add our header
581  */
582
583  igmp=(struct igmphdr*)skb_put(skb,sizeof(struct igmphdr));
584  igmp->type =
585  msg->im_msgtype = assert;
586  igmp->code = 0;
587  skb->nh_iph->tot_len=htons(skb->len);      /* Fix the length */
588  skb->b_raw = skb->raw;
589  }
590
591  if (struct_socket == NULL) {
592      free_skb(skb);
593      return -EINVAL;
594  }
595
596  /*
597      Deliver to mrouted
598  */
599  if ((ret=route_rcv_skb(mrouted_socket,skb))<0) {
600      if (net->ratelimit()) {
601          print(KERN_WARNING "mrouted: pending queue full, dropping entries.\n");
602          free_skb(skb);
603      }
604  }
605
606  return ret;
607}
```

# Multicast Forwarding and Lookup

**Figure 6.215** IPMR-- packet to send awaiting resolution: linux/net/ipv4/ipmr.c.

```c
612 static int
613 ipmr_cache_unresolved(vifi_t vifi, struct sk_buff *skb)
614 {
615
616     int err;
617     struct mfc_cache *c;
618
619     spin_lock_bh(&mfc_cache->lock);
620     for (c=mfc_unres->queue; c; c=c->next) {
621         if (c->mfc_castgroup == skb->nh_iph->daddr &)
621    c->mfc_origin == skb->nh.ip->saddr
622    break;
623
624  }
625  if (c == NULL) {
626      /*
627       * Create a new entry if allowable
628      */
629
630      if (atomic_read(&cache_resolve_queue_len)>=10 ||
631              (c=ipmr_cache_alloc_unres())==NULL) {
632              spin_unlock_bh(&mfc_unres_lock);
633
634              kfree_skb(skb);
635              return -ENOMBUFS;
636      }
637
638      /*
639       * Fill in the new cache entry
640      */
641          c->mfc_parent=-1;
642          c->mfc_origin=skb->nh.ip->saddr;
643          c->mfc_mcastgrp=skb->nh.ip->daddr;
```

> Figure 6.216 IPMR-queue packet to send awaiting resolution: linux/net/ipv4/ipmr.c.

```c
645    /*
646     * Reflect first query at mouted.
647     */
648     if ((err = ipmr_cache_report(skb, vifi, IGMP_NOCACHE))<0) {
649          /* If the report failed threw the cache entry
650          out - Brad Paker
651          */
652          spin_unlock_bh(&mfc_unres_lock);
653
654          kmem_cache_free(mrt_cache, c);
655          kfree_skb(skb);
656          return err;
657      }
658
659      atomic_inc(&cache_resolve_queue_len);
660          c->next = mfc_unres_queue;
661          mfc_unres_queue = c;
662
663          mod_timer(&ipmr_expire_timer, c->mfc_un.unres.expires);
664  }
```

**Figure 6.217** IPMR–queue a packet to send awaiting resolution: linux/net/ipv4/ipmr.c.

```c
/*
 * See if we can append the packet
 */
if (c->mfc_unres.resolved.qlen > 3) {
    kfree_skb(skb);
    err = -ENOMBUFS;
} else {
    skb_queue_tail(&c->mfc_unres.resolved, skb);
    err = 0;
}

spin_unlock_bh(&mfc_un_lock);
return err;
```

# User Management of Multicast Forwarding Cache

**Figure 6.218** IPMR–user space calls MFC delete: linux/net/ipv4/ipmr.c.

```c
int ipmr_mfc_delete(struct mfctl *mfc) {
    int line;
    struct mfc_cache *c, **cp;

    line = HASH(mfc->mfc_castgrp.s_addr, mfc->mfc_origin.s_addr);
    for (cp=mfc_cache_array[line]; *cp != NULL; cp = &(*cp)->next) {
        if (c->mfc_origin == mfc->mfc_origin.s_addr &&
            c->mfc_mcastgrp == mfc->mfc_castgrp.s_addr) {
            write_lock_bh(&mrt_lock);
            *cp = c->next;
            write_unlock_bh(&mrt_lock);
        }
    }

    kmem_cache_free(mrt_cache, c);
    return 0;
}
return -ENOENT;
```

# TCP/IP and Linux Protocol Implementation

**Figure 6.219** IPMR–user space mfc add: linux/net/ipv4/ipmr.c.

```c
int ipmr_mfc_add(struct mfctl *mfc, int mrtsock) {
    int line;
    struct mfc_cache *uc, **c, **cp;
    line = HASH(mfc->mfc_castgrp.s_addr, mfc->mfc_origin.s_addr);
    for (cp=mfc_cache_array[line]; (*cp) != NULL; cp = &cp->next) {
        if (c->mfc_origin == mfc->mfc_origin.s_addr &&
            c->mfc_mcastgrp == mfc->mfc_castgrp.s_addr)
            break;
    }
    if (c == NULL) {
        write_lock_bh(&mrt_lock);
        c->mfc_parent = mfc->mfc_parent;
        ipmr_update_thresholds(c, mfc->mfc_ttl);
        if (!mrtsock) {
            c->mfc_flags |= MFC_STATIC;
            write_unlock_bh(&mrt_lock);
            return 0;
        }
    }
    if (!MULTICAST(mfc->mfc_castgrp.s_addr))
        return -EINVAL;
    if (!ipmr_cache_alloc())
        return -ENOMEM;
    c->mfc_origin=mfc->mfc_origin.s_addr;
    c->mfc_mcastgrp=mfc->mfc_castgrp.s_addr;
    c->mfc_parent=mfc->mfc_parent;
    ipmr_update_thresholds(c, mfc->mfc_ttl);
    if (mrtsock)
        c->mfc_flags = MFC_STATIC;
    write_lock_bh(&mrt_lock);
    c->next = mfc_cache_array[line];
    mfc_cache_array[line] = c;
    write_unlock_bh(&mrt_lock);
}
```

**Figure 6.220** IPMR–user space calls mfc add: linux/net/ipv4/ipmr.c.

```c
/*
 * Check to see if we removed a queued list. If so we
 * need to send on the frames and tidy.
 */
spin_lock_bh(&mfc_unres_lock);
for (cp=mfc_unres_queue; (uc=*cp) != NULL;
    cp = &uc->next) {
    if (uc->mfc_origin == c->mfc_origin &&
        uc->mfc_mcastgrp == c->mfc_mcastgrp) {
        *cp = uc->next;
        if (atomic_dec_and_test(&cache_resolve_queue_len)) {
            del_timer(&ipmr_expire_timer);
            break;
        }
    }
}

if (uc) {
    spin_unlock_bh(&mfc_unres_lock);
    ipmr_cache_resolve(uc, c);
    kmem_cache_free(mrt_cache, uc);
}
return 0;
```

# Infrastructure Protocols

**Figure 6.221** IPMR–mrouted_socket dies: linux/net/ipv4/ipmr.c.

```c
static void mrtsock_destruct(struct socket *sk) {
    rtnl_lock();
    if (sk == mroute_socket) {
        ipv4_devconf.mc_forwarding--;
        write_lock_bh(&mrt_lock);
        mroute_socket=NULL;
        write_unlock_bh(&mrt_lock);
        mroute_tables(sk);
    }
    rtnl_unlock();
}
```

# Multicast Socket Options

**Figure 6.222** IPMR–setsockopt entry handler: linux/net/ipv4/ipmr.c.

* Socket options and virtual interface manipulation. The whole virtual interface system is a complete heap, but unfortunately that's how BSD happens. Maybe one day with a proper MSDP/PIM router we can clean this up.

```c
int ip_mroute_setsockopt(struct socket *sk, int optname, char *optval, int optlen) {
    int ret;
    struct if vif;
    struct mfc mfc;

    if (optname==MRT_INIT) {
        if (mroute_socket && capable(CAP_NET_ADMIN))
            return -EACCES;
    }
    switch(optname) {
    case MRT_INIT:
        if (sk->type!=SOCK_RAW || sk->protocol!=IPPROTO_IGMP)
            return -EINVAL;
        if (optlen!=sizeof(int))
            return -ENOPTS;
        rtnl_lock();
        if (mroute_socket)
            rtnl_unlock();
            return -EADDRUSE;
        ret = ip_ra_control(sk, mrtsock_destruct);
        if (ret != 0) {
            write_lock_bh(&mrt_lock);
            mroute_socket=sk;
            write_unlock_bh(&mrt_lock);
        }
        ipv4_devconf.mc_forwarding++;
        rtnl_unlock();
        return ret;
    case MRT_DONE:
        if (!mroute_socket)
            return -EACCES;
        return ip_ra_control(sk, NULL);
    case MRT_ADD_VIF:
    case MRT_DEL_VIF:
        if (optlen!=sizeof(vif))
            return -EINVAL;
        if (copy_from_user(&vif,optval,sizeof(vif)))
            return -EFAULT;
        if (vif.vif >= MAXVFS)
            return -ENFILE;
        rtnl_lock();
        if (optname==MRT_ADD_VIF)
            ret = vif_add(&vif, mroute_socket);
        } else {
            ret = vif_delete(&vif.vif);
        }
        rtnl_unlock();
        return ret;
    case MRT_ADD_MFC:
    case MRT_DEL_MFC:
        if (optlen!=sizeof(mfc)) {
            return -EINVAL;
            if (copy_from_user(&mfc,optval,sizeof(mfc))) {
                return -EFAULT;
            }
            rtnl_lock();
            if (optname==MRT_DEL_MFC)
                ret = ipmr_mfc_delete(&mfc);
            else
                ret = ipmr_mfc_add(&mfc,mroute_socket);
            rtnl_unlock();
            return ret;
    case MRT_ASSERT:
        {
            int v;
            if (get_user(v,int (*optval))
                return -EFAULT;
            mroute_do_assert=(v)?1:0;
            return 0;
        }
#ifdef CONFIG_IP_PIMSM
    case MRT_PIM:
        {
            int v;
            if (get_user(v,int (*optval))
                return -EFAULT;
            v=(v)?1:0;
            rtnl_lock();
            if (v != rmoute_do_pim) {
                rmoute_do_pim = v;
                rmoute_do_assert = v;
            }
#endif
#ifdef CONFIG_IP_PIMSM_V2
            if (rmoute_do_pim)
                inet_add_protocol(&pim_protocol);
```
