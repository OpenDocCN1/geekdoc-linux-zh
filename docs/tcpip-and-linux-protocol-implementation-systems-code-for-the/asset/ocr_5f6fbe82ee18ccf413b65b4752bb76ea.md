# TCP/IP and Linux Protocol Implementation

Figure 6.219 IPMR–user space mfc add: linux/net/ipv4/ipmr.c.

```
int ipmr_mfc_add(struct mfcctl *mfc, int mrtsock)
{
    int line;
    struct mfc_cache *uc, **c, **cp;
    line=MFC_HASH(mfc->mfc_mcastgrp.s_addr, mfc->mfc_origin.s_addr);
    for (cp=mfc_cache_array[line]; (*cp) != NULL; cp=&cp->next) {
        if (c->mfc_origin == mfc->mfc_origin.s_addr &&
            c->mfc_mcastgrp == mfc->mfc_mcastgrp.s_addr)
            break;
    }
    if (c == NULL) {
        write_lock_bh(mrts_lock);
        c->mfc_parent = mfc->mfc_parent;
        ipmr_update_thresholds(c, mfc->mfc_ttl);
        if (!mrtsock) {
            c->mfc_flags |= MFC_STATIC;
            write_unlock_bh(mrts_lock);
            return 0;
        }
    }
    if(!MULTICAST(mfc->mfc_mcastgrp.s_addr))
        return -EINVAL;
    if (!ipmr_cache_alloc())
        return -ENOMEM;
    c->mfc_origin=mfc->mfc_origin.s_addr;
    c->mfc_mcastgrp=mfc->mfc_mcastgrp.s_addr;
    c->mfc_parent=mfc->mfc_parent;
    ipmr_update_thresholds(c, mfc->mfc_ttl);
    if (mrtsock)
        c->mfc_flags = MFC_STATIC;
    write_lock_bh(mrts_lock);
    c->next = mfc_cache_array[line];
    mfc_cache_array[line] = c;
    write_unlock_bh(mrts_lock);
}
```

Figure 6.220 IPMR–user space calls mfc add: linux/net/ipv4/ipmr.c.

```
/*
 * Check to see if we removed a queued list. If so we
 * need to send on the frames and tidy.
 */
spin_lock_bh(&mfc_unres_lock);
for (cp=mfc_unres_queue; (uc=*cp) != NULL;
    cp = &uc->next)
```