# Forwarding 677

```
for (i = n->sel.nkeys; i>0; key++) {
    if ((u32*)(ptr+key->off+off(2&key->offmask))&key->val)&mask) {
        n = n->next;
        goto next_node;
    }
}
if (n->ht_down == NULL) {
    check_terminal:
    if (n->sel.flags&TC_U32_TERMINAL) {
        *res = n->res;
    }
#ifdef CONFIG_NET_CLS_POLICY
    if (n->policy) {
        int pol_res = tcf_policy(skb, n->policy);
        if (pol_res >= 0) return pol_res;
    } else {
        return 0;
    }
#endif
    n = n->next;
goto next_node;
}
/* PUSH */
if (depth > TC_U32_MAXDEPTH)
    goto deadloop;
```

**Figure 9.30** u32 API-classifier ii: linux/net/sched/cls_u32.c.

```
stack[depth].node = n;
stack[depth].ptr = ptr;
depth++;

ht = n->ht_down;
sel = 0;
if (ht->divisor)
    sel = ht->divisor@u32_hash_fold((u32*)(ptr+n->sel.hof), n->sel);
if ((n->sel.flags&TC_U32_VAROFFSET|TC_U32_OFFSET|TC_U32_EAT))
    goto next_ht;

if (n->sel.flags&TC_U32_EAT|TC_U32_VAROFFSET)) {
    off2 = n->sel.off + 3;
    if (n->sel.flags&TC_U32_VAROFFSET)
        off2 += ntohs(n->sel.offmask&(u16*)(ptr+n->sel.off))>>n->sel.offshift;

    off2 = "3";
}
if (n->sel.flags&TC_U32_EAT)
    ptr += off2;
    off2 = 0;
```