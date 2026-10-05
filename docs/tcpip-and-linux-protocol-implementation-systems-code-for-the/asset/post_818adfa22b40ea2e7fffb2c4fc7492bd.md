
```c
if (root_ht == NULL) {
    MDD_DEC_USE_COUNT;
    return -ENOMBUFS;
}
memset(root_ht, 0, sizeof(*root_ht));
root_ht->divisor = 0;
root_ht->handle = tp->c ? gen_new_htid(tp_c) : 0x08000000;

if (tp_c == NULL) {
    tp->c = kmalloc(sizeof(*tp_c), GFP_KERNEL);
    if (tp->c == NULL) {
        kfree(root_ht);
        MDD_DEC_USE_COUNT;
        return -ENOMBUFS;
    }
    memset(tp->c, 0, sizeof(*tp->c));
    tp->c->q = tp->q;
    tp->c->next = u32_list = tp_c;
}

tp_c->refcnt++;
root_ht->next = tp_c->hlist;
root_ht->hlist = root_ht;
root_ht->tp = tp_c;

tp->root = root_ht;
tp->data = tp_c;
return 0;
```

Figure 9.34 u32 API-destroy_key delete: linux/net/sched/cls.u32.c.

```c
static int u32_destroy_key(struct tcf_proto *tp, struct tc_u_knode *n)
{
    unsigned long cl;

    if ((cl == .cls_class_class(n->res, cl)) != 0)
        tp->q->ops->cl_ops->unbind_tq(tp->q, cl);
#ifdef CONFIG_NET_CLS_POLICY
    tcf_policies_release(n->policy);
#endif
    if (n->ht->down) {
        n->ht->down->refcnt--;
        kfree(n);
    }
    return 0;
}
static int u32_delete_key(struct tcf_proto *tp, struct tc_u_knode* key)
{
    struct tc_u_knode *kp;
    struct tc_u_knode *ht = key->ht_up;

if (ht) {
    for (kp = &ht->ht[TC_U32_HASH(key->handle)]; *kp; kp = &(kp)->next) {
        if (*kp == key) {
            tcf_tree_lock(tp);
            *kp = key->next;
            tcf_tree_unlock(tp);
            u32_destroy_key(tp, key);
            return 0;
        }
    }
    BUG_TRAP(0);
    return 0;
}
static void u32_clear_hnode(struct tcf_proto *tp, struct tc_u_hnode *ht) {
    struct tc_u_knode *n;
    unsigned h;

    for(h=0; h<ht->divisor; h++) {
        while ((n = ht->ht[h]) != NULL) {
            ht->ht[h] = n->next;
            u32_destroy_key(tp, n);
        }
    }
}
}
```

Figure 3.35 u32 API-destroy/delete classifier: linux/net/sched/cls_u32.c.

static int u32_destroy_hnode(struct tcf_proto *tp, struct tc_u_hnode *ht) {
    struct tc_u_common *tp->data;
    struct tc_u_hnode **hn;

    BUG_TRAP(ht->refcnt);
    u32_clear_hnode(tp, ht);

    for (hn = &ht->list; *hn; hn = (*hn)->next) {
        if (*hn == ht) {
            *hn = ht->next;
            kfree(ht);
            return 0;
        }
    }
    BUG_TRAP(0);
    return -ENOENT;
}
```

# 682 TCP/IP and Linux Protocol Implementation

```c
374
375 static void u32_destroy(struct tcf_proto *tp)
376 {
377     structstruct tc_u_common *tp_c = tp->data;
378     struct tc_u_hnode *root_ht = xchg(&tp->root, NULL);
379
380 BUG_TRAP(root_ht != NULL);
381
382     if (root_ht && --root_ht->refcnt == 0)
383         u32_destroy_hnode(tp, root_ht);
384
385     if (--tp->c->refcnt == 0)
386         struct tc_u_hnode *ht;
387         struct tc_u_common **tp_cp;
388
389         for (tp_cp = &u32_list, *tp_cp; tp_cp = &(tp_cp)->next) {
390             if (*tp_cp = tp_c->next)
391                 break;
392         }
393
394         for (ht = tp_c->hlist; ht = ht->next)
395             u32_clear_hnode(tp, ht);
396
397         while (ht = tp_c->hlist) != NULL) {
398             BUG_TRAP(ht->refcnt == 0);
399             kfree(ht);
400         }
401     kfree(tp_c);
402 }
407
408     MOD_DEC_USE_COUNT;
409     tp->data = NULL;
410 }
```

Figure 9.36 u32_delete(struct tcf_proto *tp, unsigned long arg)

```c
414 static int u32_delete(struct tcf_proto *tp, unsigned long arg)
415 {
416     struct tc_u_knode *ht = (struct tc_u_knode*)arg;
417
418     if (ht == NULL)
419         return 0;
420
421     if (TC_U32_KEY(ht->handle))
422         return u32_delete_key(tp, (struct tc_u_knode*)ht);
423
424     if (tp->root == ht)
425
         return -EINVAL;
426
427     if (--ht->refcnt == 0)
428
         u32_destroy_hnode(tp, ht);
429
430         return 0;
431 }
```

```c
432 static u32_new_kid(struct tc_u_hnode *ht, u32 handle)
433 {
434
     struct tc_u_knode *n;
435
     unsigned int i = 0x7FF;
436
437
     for (n=ht->ht[TC_U32_HASH(handle)]; n; n=n->next)
438
         if (i < TC_U32_NODE(n->handle))
439
             i = TC_U32_NODE(n->handle);4440
             i++;
441
442
             return (i>0xFF ? i : i);
443
 }
```

**Figure 9.37** u32 API–set parameters: linux/net/sched/cls.u32.c.

```c
446 static int u32_set_params(struct u32 *qdisc, unsigned long bone,
447
     struct tc_u_hnode *ht, struct rtattr *tb,
448
     struct tc_u_hnode *n, struct rtattr *
449
     struct rtattr *est)
450
 {
451
     if (tb[TCA_U32_LINK-1]) {
452
         u32 handle = *(u32*)RTA_DATA(tb[TCA_U32_LINK-1]);
453
         struct tc_u_hnode *ht_down = NULL;
454
455
         if (TC_U32_KEY) {
556
             return -EINVAL;
457
458
459
         if (handle) {
459
             ht_down = u32_lookup_ht(ht->tp_c, handle);
460
             if (ht_down == NULL) {
461
                 return -EINVAL;
462
             ht_down->refcnt++;
463
464
465
466
             sch_tree_lock(q);
467
             ht_down = xchg(&ht->ht_down, ht_down);
468
             sch_tree_unlock(q);
469
470
             if (ht_down) {
471
                 ht_down->refcnt--;
472
473
             if (tb[TCA_U32_CLASSID-1]) {
474
                 unsigned long cl;
475
                 n->res.class = *(u32*)RTA_DATA(tb[TCA_U32_CLASSID-1]);
476
                 sch_tree_lock(q);
477
                 cl = q->ops->cl_ops->bind_tq(q, base, n->res.class);
478
                 sch_tree_unlock(q);
479
                 if (cl)
480
                     q->ops->cl_ops->unbind_tq(q, cl);
481
 #ifdef CONFIG_NET_CLS_POLICY
             if (tb[TCA_U32_POLICE-1]) {
                 struct tcf_policy *opt = tcf_policy(tb[TCA_U32_POLICE-1]);
                 sch_tree_lock(q);
                 police = xchg(&n->police, police);
                 sch_tree_unlock(q);
                 tcf_policy_release(police);
             }
 #endif
 return 0;
 }
```

```c
static int u32_change(struct tcf_proto *proto, unsigned long base, u32 handle,
    struct rtattr *etca, unsigned long *arg)
{
    struct tc_u_common *tp_c = tp->data;
    struct tc_u_hnode *ht;
    struct tc_u_node *n;
    struct tc_u32 *els;
    struct rtattr *opt = tca[TCA_U32_OPTIONS-1];
    struct rtattr *tb[TCA_U32_MAX];
    u32 htid;
    int err;

    if (opt == NULL)
        return handle ? -EINVAL : 0;
    if (rtattr_parse(tb, TCA_U32_MAX, RTA_DATA(opt), RTA_PAYLOAD(opt) < 0)
        return -EINVAL;
    if (n = (struct tc_u_node*)arg) == NULL) {
        if (TC_U32_KEY(n->handle) == 0)
            return -EINVAL;
        return u32_set_params(tp->q, base, n->ht, n, tca[TCA_U32_RATE-1]);
    }
    if (tb[TCA_U32_DIVISOR-1]) {
        unsigned divisor = *(unsigned*)RTA_DATA(tb[TCA_U32_DIVISOR-1]);
        if (divisor > 0x100)
            return -EINVAL;
        if (TC_U32_KEY(handle))
            return -EINVAL;
        if (handle == 0) {
            handle = gen_new_ht(tp->data);
            if (handle == ENOMEM) {
                return -ENOMEM;
            }
            ht = malloc(sizeof(*ht) + divisor*sizeof(void), GFP_KERNEL);
            if (ht == NULL) {
                return -ENOBUFS;
            }
            memset(ht, 0, sizeof(*ht));
            ht->tp->c = tp_c;
            ht->refcnt = 0;
            ht->divisor = divisor;
            ht->handle = handle;
            ht->next = tp_c->hlist;
            tp_c->hlist = ht;
            *arg = (unsigned long)ht;
            return 0;
        }
    }
    if (tb[TC_U32_HASH-1]) {
        htid = (unsigned*)RTA_DATA(tb[TCA_U32_HASH-1]);
        if (TC_U32_HTID(htid) == TC_U32_ROOT) {
            ht = tp->root;
            htid = ht->handle;
        } else {
            ht = u32_lookup(ht->data, TC_U32_HTID(htid));
            if (ht == NULL)
                return -EINVAL;
        }
    } else {
        ht = tp->root;
        htid = ht->handle;
    }
    
    if (ht->divisor < TC_U32_HASH(htid)) {
        return -EINVAL;
    }
    if (handle) {
        if (TC_U32_HTID(handle) && TC_U32_HTID("handle")) {
            return -EINVAL;
        }
        handle |= TC_U32_NODE(handle);
    } else {
        handle = gen_new_kid(ht, htid);
    }
    if (tb[TCA_U32_SEL-1] == 0 ||
        RTA_PAYLOAD(tb[TCA_U32_SEL-1]) < sizeof(struct tc_u32_sel)) {
        return -EINVAL;
    }
    s = RTA_DATA(tb[TCA_U32_SEL-1]);
}
```

# 9.39 u32 API-change parameters: linux/net/sched/cls_u32.c.
