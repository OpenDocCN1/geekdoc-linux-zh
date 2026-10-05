
Figure 8.81 Fast accessing of the FIB through hashing--select default entry: linux/net/ipv4/fib_hash.c

```c
if (order<0 || fi==NULL) {
    fn_hash_last_dflt = -1;
    goto out;
}

if ((fib_detect_death(fi, order, &last_resort, &last_idx)) {
    if (res->fi) {
        fib_info_put(res->fi);
    }
    res->fi = fi;
    atomic_inc(&fi->fib_clntref);
    fn_hash_last_dflt = order;
    goto out;
}

if (last_idx >= 0) {
    if (res->fi) {
        fib_info_put(res->fi);
    }
    res->fi = last_resort;
    atomic_inc(&last_resort->fib_clntref);
}
fn_hash_last_dflt = last_idx;
out:
    read_unlock(&fib_scan_hash_lock);
}
```

## Adding a FIB Entry

Now look at the case of adding (updating) entries.

Figure 8.82 Fast accessing of the FIB through hashing--insert entry i: linux/net/ipv4/fib_hash.c.

```c
#define FIB_SCAN(f, fp) \
for ( : ; (fp = *(fp)) != NULL; fp = &(fp)->fn_next)

#define FIB_SCAN_KEY(f, fp, key) \
for ( : ; (fp = *(fp)) != NULL && fn_key_eq(fp)->fn_key, key); fp = &(fp)->fn_next)

#ifndef CONFIG_ROUTE_TOS
#define FIB_SCAN_TOS(f, fp, key, tos) FIB_SCAN_KEY(f, fp, key) \
#else
#define FIB_SCAN_TOS(f, fp, key, tos) \
for ( : ; (fp = *(fp)) != NULL && fn_key_eq(fp)->fn_key, key) && (fp)->fn_tos == (tos); fp = &(fp)->fn_next)
    (fp)->fn_tos = (tos);
#endif
```

## TCP/IP and Linux Protocol Implementation

```c
427
#ifdef CONFIG_RTNETLINK
static void rmsg_fib(struct fib_node*, int, int, int,
    struct nmsgghdr *n,
    struct netlink_ekb_parms *);
else
#define rmsg_fib(a, b, c, d, e, f)
#endif
static int
fn_hash_insert(struct fib_table *tb, struct rmsg *r, struct kern_rta rta,
    struct nmslghdr *n, struct netlink_ekb_parms *req)
(
    struct fib_table *table = (struct fn_hash*)tb->tb_data;
    struct fib_node *new_f, *fp, **del_fp;
    struct fn_zone *fz;
    struct fib_info *info = fi;

    int z = r->rtm_dst_len;
    int type = r->rtm_type;
#ifdef CONFIG_IP_ROUTE_TOS
u8 tos = r->rtm_tos;
#endif
    fn_key_t key,
    int err;
```

Figure 8.83 Fast access of the FIB through hashing-insert ii: linux/net/ipv4/hash.c

```c
454
printf("%b(d)", insert);
455
(*u32*)rta->rtm_dst = 0, z = rta->rtm_oif ? *rta->rtm_oif : -1,
456
rta->prefrc ? (*u32*)rta->rtm_prefrc : 0);
457
if (z > 3)
458
    return -EINVAL;
459
fz = table->zones[z];
460
if (fz && (fz = fn_new_zone(table, z)))
461
    return -ENBUFS;
462
fz_key_0(key);
463
if (rta->rta_rtm_dst) {
464
    u32 dst;
465
    memcpy(&dst, rta->rtm_dst, 4);
466
    if (dst & ~FZ_MAX(fz))
467
    return -EINVAL;
468
    key = fz_key(dst, fz);
469
}
470
if ((fi = fib_create_info(r, rta, n, err)) == NULL)
471
    return err;
475
ifdef CONFIG_IP_ROUTE_LARGE_TABLES
```

## Routing 607

```c
476 if (fz->fz_next > (fz->fz_divisor<)) &&
477 fz->fz_divisor < FZ_MAX_DIVISOR &&
478 (ze==32 || (iz) > fz->fz_divisor))
479 fn_rehash_zone(fz);
480 #endif
482
fp = fz_chain_p(key, fz);

483
485 /*
486 * Scan list to find the first route with the same destination
487 */
488 FIB_SCAN(fp, fp) {
489 if (fn_key_leq(key,fp)->fn_key)
490 break;
491 }

493
#ifdef CONFIG_IP_ROUTE_TOS
494 /*
495 * Find route with the same destination and tos.
496 */
497 FIB_SCAN_KEY(fp, fp, tos) {
498 if (fp)->to <= tos)
499 break;
500 }
501 #endif
```

Figure 8.24 Fast accessing of the FIB through hashing--insert entry iii: linux/net/ipv4/fib.hash.c.

```c
503 del_fp = NULL;
504 if (f && (f)->fn_state&FN_S_ZOMBIE) &&
506 #ifdef CONFIG_IP_ROUTE_TOS
507 f->fn_tos == tos &&
508 #endif
509 fn_key_eq(f->fn_key, key) {
510 del_fp = fp;
511 fp = &fp->fn_next;
512 f = *fp;
513 goto create;
514 }

516 FIB_SCAN_TOS(f, fp, key, tos) {
517 if (fi->fib_priority <= FIB_INFO(f)->fib_priority)
518 break;
519 }
```

## Figure 8.85 Fast accessing of the FIB through hashing--insert entry iv: linux/net/ipv4/
fib_hash.c.

```c
// Now f=fp points to the first node with the same
keys [prefix,priority], if such key already
   exists or to the node, before which we will insert new one.
*/
   if (f &&
     #ifdef CONFIG_IP_ROUTE_TS
       f->fn_tos = tos &&
#endif
       fib_key_eq(f->fn_key, key) &&
       fi->fib_priority = FIB_INFO(f)->fib_priority) {
           struct fib_node *ins_fp;
           err = -EXIST;
           if (n->nlmsg_flags&NLM_F_EXCL)
               goto out;

   if (n->nlmsg_flags&NLM_F_REPLACE) {
       del_fp = fp;
       fp = &f->fn_next;
       f = *fp;
       goto replace;
   }
   ins_fp = fp;
   err = -EXIST;
   FIB_SCAN_TOS(f, fp, key, tos) {
       if (fi->fib_priority != FIB_INFO(f)->fib_priority)
           break;
       if (f->fn_type == type && f->fn_scope == r->rtm_scope
           && FIB_INFO(f) == fi)
           goto out;
   }
   if (!(n->nlmsg_flags&NLM_F_APPEND)) {
       fp = ins_fp;
       f = *fp;
   }
```

Figure 8.86 Fast accessing of the FIB through hashing--insert entry v: linux/net/ipv4/
fib_hash.c.

```c
create:
   err = -ENOENT;
   if (!(n->nlmsg_flags&NLM_F_CREATE))
       goto out;
replace:
```

## Routing 609

```c
err = -ENOMEM;
new_f = kmem_cache_alloc(fn_hash, SLAB_KERNEL);
if new_f == NULL
goto out;
memset(new_f, 0, sizeof(struct fib_node));
new_f->fn_key = key;
#ifdef CONFIG_IP_ROUTE_TOS
new_f->fn_tos = tos;
#endif
new_f->fn_type = type;
new_f->fn_scope = r->rtm_scope;
FIB_INFO(new_f) = fi;
/*
 * Insert new entry to the list. */
new_f->fn_next = f;
write_lock_bh(&fib_hash_lock);
*fp = new_f;
write_unlock_bh(&fib_hash_lock);
fz->nent++;
```

Figure 8.7 Fast accessing of the FIB through hashing--insert entry vi: linux/net/ipv4/fib_hash.c.

```c
if (del_fp) {
    f = del_fp;
    /* Unlink node */
    write_lock_bh(&fib_hash_lock);
    f = f->fn_next;
    del_fp = unlock_bh(&fib_hash_lock);
    if (!(f->fn_state&FN_S_ZOMBIE))
        rtmsg_fib(RTM_DELROUTE, f, z, tb->tb_id, n, req);
    if (f->fn_state&FN_S_ACCESSED)
        rt_cache_flush(-1);
        free_node(f);
        fz->nent--;
} else {
    rt_cache_flush(-1);
}
rtmsg_fib(RTM_NEWROUTE, new_f, z, tb->tb_id, n, req);
return 0;
out:
fib_release_info(fi);
return err;
```

## TCP/IP and Linux Protocol Implementation

## Deleting a FIB Entry

Figure 8.88 Fast accessing of the FIB through hashing--delete entry: linux/net/ipv4/fib_hash.c.

```c
617
static int
fn_hash_delete(struct fib_table *tb, struct rmag *r, struct rta *rta,
            struct nlmsghdr *n, struct netlink_skparms *req)
{
    struct fn_hash *table = (struct fn_hash*)tb->tb_data;
    struct fib_node *fp = *del_fp, fp;
    int z = r->rtm_dest_len;
    struct fn_zone *fz;

    fn_key_t key;
    if (!matched)
        #if (CONFIG_IP_ROUTE_TOS)
            u8 tos = r->rtm_tos;
        #endif

    dprint("%d).delete: %d %08x/%d\n", tb->ib_id, r->rtm_type, rta->rta_dst ?
            *(u32*)rta_dst, 0, rta->rta_ois ? *rta->rta_ois : -1);
    if (z > 0)
        return -EINVAL;
    if ((fz = fn_hash_zones[z]) == NULL)
        return -ESRCH;

    fn_key_0(key);
    if (rta->rta_dst) {
        u32 dst;
        memcpy(&dst, rta->rtm_dst, 4);
        if (dst & FZ_MASK(fz))
            return -EINVAL;
            key = fn_key(dst, fz);
    }

    fp = fz_chain_p(fp, fz);

    FIB_SCAN(f, fp) {
        if (fn_key_eq(f->fn_key, key))
            break;
        if (fn_key_leg(key, f->fn_key)
            return -ESRCH;
    }
}
```

Figure 8.89 Fast accessing of the FIB through hashing--delete entry: linux/net/ipv4/fib_hash.c.

```c
658
#ifdef CONFIG_IP_ROUTE_TOS
    FIB_SCAN_KEY(f, fp, key) {
660         if (f->fn_tos == tos &&
661             break;
662     }
```

## Routing 611

```c
#endif
matched = 0;
del_fp = NULL, tos;
FIB_SCAN_TOS(f, fp, key, tos) {
    struct fib_info *fi = FIB_INFO(f);
    if (fi->fib_priority != FIB_INFO(f)->fib_priority)
        break;
    if (f->fn_state&FN_S_ZOMBIE) {
        return -ESRCH;
    }
    matched++;
}
if (del_fp == NULL &&
    (r->rtm_type == 0 || f->fn_type == r->rtm_type) &&
    (r->rtm_scope == RT_SCOPE_NOWHERE || f->fn_scope == r->rtm_scope) &&
    (r->rtm_protocol == r->rtm_protocol) &&
    fib_nh_match(r, rta, fi) == 0) {
}
del_fp = fp;
```

Figure 8.90 Fast accessing of the FIB through hashing--insert entry iii: linux/net/ipv4/fib_hash.c.

```c
if (del_fp) {
    f = del_fp;
    /* Unlink node */
    write_lock_bh(&fib_hash_lock);
    f = f->fn_next;
    del_fp = unlock_bh(&fib_hash_lock);
    if (!(f->fn_state&FN_S_ZOMBIE))
        rtmsg_fib(RTM_DELROUTE, f, z, tb->tb_id, n, req);
    if (f->fn_state&FN_S_ACCESSED)
        rt_cache_flush(-1);
        free_node(f);
        fz->nent--;
} else {
    rt_cache_flush(-1);
}
rtmsg_fib(RTM_NEWROUTE, new_f, z, tb->tb_id, n, req);
return 0;
out:
fib_release_info(fi);
return err;
}
```
