
574                              /* 标记内核这是一个路由添加条目操作 */

575  msg = (struct igmpmsg*)skb->nh_iph;

576  msg->im_vif = vifi;

577  skb->dst = dst_clone(pkt->dst);

578

579  /*

580      添加我们的头部信息

581  */

582

583  igmp=(struct igmphdr*)skb_put(skb,sizeof(struct igmphdr));

584  igmp->type =

585  msg->im_msgtype = assert;

586  igmp->code = 0;

587  skb->nh_iph->tot_len=htons(skb->len);      /* 修正长度 */

588  skb->b_raw = skb->raw;

589  }

590

591  if (struct_socket == NULL) {

592      free_skb(skb);

593      return -EINVAL;

594  }

595

596  /*

597      投递给 mrouted

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

# 多播组转发与查找

**图 6.215** IPMR-- 等解析的发送数据包：linux/net/ipv4/ipmr.c。

```c
612 static int
613 ipmr_cache_unresolved(vifi_t vifi, struct sk_buff *skb)
614 {

616     int err;
617     struct mfc_cache *c;

619     spin_lock_bh(&mfc_cache->lock);
620     for (c=mfc_unres->queue; c; c=c->next) {
621         if (c->mfc_castgroup == skb->nh_iph->daddr &)
621    c->mfc_origin == skb->nh.ip->saddr
622    break;

624  }
625  if (c == NULL) {
626      /*
627       * 如果允许，则创建一个新条目
628      */

630      if (atomic_read(&cache_resolve_queue_len)>=10 ||
631              (c=ipmr_cache_alloc_unres())==NULL) {
632              spin_unlock_bh(&mfc_unres_lock);

634              kfree_skb(skb);
635              return -ENOMBUFS;
636      }

638      /*
639       * 填充新的缓存条目
640      */
641          c->mfc_parent=-1;
642          c->mfc_origin=skb->nh.ip->saddr;
643          c->mfc_castgrp=skb->nh.ip->daddr;
> 图 6.216 IPMR-queue 等解析的发送数据包：linux/net/ipv4/ipmr.c。
```

```c
645    /*
646     * 在 mouted 处反射查询
647     */
648     if ((err = ipmr_cache_report(skb, vifi, IGMP_NOCE))<0) {
649          /* 如果 report 导致缓存条目失败 */
650          - */
651          spin_unlock_bh(&mfc_unres_lock);
652          kmem_cache_free(c);
653          kfree_skb(skb);
654          return err;
655      }
656      atomic_inc(&cache_resolve_queue_len);
657      c->next = mfc_unres_queue;
658      mfc_unres_queue = c;
659      mod_timer(&ipmr_expire_timer, c->mfc_unres.expires);
660  }
```
**图 6.217** IPMR–queue 等解析的发送数据包：linux/net/ipv4/ipmr.c。

```c
/* 查看我们是否可以追加数据包 */
if (c->mfc_unres.resolved.qlen > 3) {
    kfree_skb(skb);
    err = -ENOMBUFS;
} else {
    skb_queue_tail(&c->mfc_unres.resolved, skb);
    err = 0;
}
spin_unlock_bh(&mfc_unres_lock);
return err;
```

# 多播转发缓存的管理

**图 6.218** IPMR–用户空间调用 delete：linux/net/ipv4/ipmr.c。

```c
int ipmr_mfc_delete(struct mfctl *mfc) {
    int line;
    struct mfc_cache *c, **cp;
    line = HASH(mfc->mfc_castgrp.s_addr, mfc->mfc_origin.s_addr);
    for (cp=mfc_cache_array[line]; *cp != NULL; cp = &(*cp)->next) {
        if (c->mfc_origin == mfc->mfc_origin.s_addr &&
            c->mfc_castgrp == mfc->mfc_castgrp.s_addr) {
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

# TCP/IP 与 Linux 协议实现

**图 6.219** IPMR–用户空间 add：linux/net/ipv4/ipmr.c。

```c
int ipmr_mfc_add(struct mfctl *mfc, int mrtsock) {
    int line;
    struct mfc_cache *uc, **c, **cp;
    line = HASH(mfc->mfc_castgrp.s_addr, mfc->mfc_origin.s_addr);
    for (cp=mfc_cache_array[line]; (*cp) != NULL; cp = &cp->next) {
        if (c->mfc_origin == mfc->mfc_origin.s_addr &&
            c->mfc_castgrp == mfc->mfc_castgrp.s_addr)
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
```
