# Forwarding 681

if (ht) {

```
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
```

static void u32_clear_hnode(struct tcf_proto *tp, struct tc_u_hnode *ht) {

```
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

Figure 3.35 u32 API--destroy/delete classifier: linux/net/sched/cls_u32.c.

static int u32_destroy_hnode(struct tcf_proto *tp, struct tc_u_hnode *ht) {

```
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
```