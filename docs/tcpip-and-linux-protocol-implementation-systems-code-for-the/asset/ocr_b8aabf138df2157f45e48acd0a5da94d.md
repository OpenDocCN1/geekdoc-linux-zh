```
return 0;

if (rtatarr_parse(tb,TCA_TCINDEX_MAX,RTA_DATA(opt),RTA_PAYLOAD(opt)) < 0) {
    return -EINVAL;
}

if (tb[tb[TCA_TCINDEX_HASH-1]]) {
    hash = p->hash;
} else {
    if (RTA_PAYLOAD(tb[TCA_TCINDEX_HASH-1]) < sizeof(int)) {
        return -EINVAL;
    }
    hash = (int *) RTA_DATA(tb[TCA_TCINDEX_HASH-1]);
}
if (tb[tb[TCA_TCINDEX_MASK-1]) {
    mask = p->mask;
} else {
    if (RTA_PAYLOAD(tb[TCA_TCINDEX_MASK-1]) < sizeof(__u16)) {
        return -EINVAL;
    }
    mask = (__u16 *) RTA_DATA(tb[TCA_TCINDEX_MASK-1]);
}
if (p->perfect && hash <= mask) {
    return -EBUSY;
}
if ((p->perfect || p->hash) && hash > p->alloc_hash) {
    return -EBUSY;
}
```

Figure 9.84 TC classifier api-change classifier: linux/net/sched/cls_tcindex.c.

```
p->hash = hash;
p->mask = mask;
if (tb[TCA_TCINDEX_SHIFT-1]) {
    if (RTA_PAYLOAD(tb[TCA_TCINDEX_SHIFT-1]) < sizeof(__u16)) {
        return -EINVAL;
    }
    p->shift = (int *) RTA_DATA(tb[TCA_TCINDEX_SHIFT-1]);
}
if (tb[TCA_TCINDEX_FALL_THROUGH-1]) {
    if (RTA_PAYLOAD(tb[TCA_TCINDEX_FALL_THROUGH-1]) < sizeof(int)) {
        return -EINVAL;
    }
    p->fall_through = (*int *) RTA_DATA(tb[TCA_TCINDEX_FALL_THROUGH-1]);
}
DPRINK("class %x/%x\n\n", tb[TCA_TCINDEX_CLASSID-1],
    tb[TCA_TCINDEX_POLICE-1]);
if (tb[TCA_TCINDEX_CLASSID-1] && !tb[TCA_TCINDEX_POLICE-1]) {
    return 0;
}
if (!p->hash) {
    if (p->mask < PERFECT_HASH_THRESHOLD) {
        p->hash = p->mask+1;
    } else {
        p->hash = DEFAULT_HASH_SIZE;
    }
}
```