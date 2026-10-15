
### struct tc_u_node

```c
struct tc_u_node
{
    struct tc_u_node *next;
    unsigned int handle;
    struct tc_u_hnode *ht_up;
#ifdef CONFIG_NET_CLS_POLICE
    struct tcf_police *police;
#endif
    struct tcf_result res;
    struct tc_u_node *ht_down;
    struct u32_sel sel;
};
```

### struct tc_u_hnode

```c
struct tc_u_hnode
{
    struct tc_u_node *next;
    unsigned int handle;
    struct tc_u_common *tp_c;
    int refcnt;
    unsigned int divisor;
    unsigned int hgenerator;
    struct tc_u_node *ht[1];
};
```

### struct tc_u_common

```c
struct tc_u_common
{
    struct tc_u_common *next;
    struct tc_u_hnode *hlist;
    struct qdisc *q;
    int refcnt;
    unsigned int hgenerator;
};
```

```c
static struct tc_u_common *u32_list;
static __inline__ unsigned u32_hash_fold(u32 key, struct u32_sel *sel)
{
    unsigned int h = key & sel->hmask;
    h = h>>16;
    h = h>>8;
    return h;
}
```

**图 9.29** u32 API 分分类器：`linux/net/sched/cls_u32.c`。

```c
struct {
    struct tc_u_node *knode;
    u8 *ptr;
} stack[TC_U32_MAXDEPTH];

struct tc_u_hnode *ht = (struct tc_u_hnode*)tp->root;
u8 *ptr = skb->nh->raw;
struct tc_u_node *n;
int sdepth = 0;
int off2 = 0;
int sel = 0;
int i;

if (defined(__i386__)) && !defined(__mc68)) {
    if ((unsigned long)ptr & 3)
        return -1;
}

next_ht:
n = ht[sel];

next_node;
if (n) {
    struct tc_u32_key *key = n->sel.keys;

    for (i = n->sel.keys; i>0; i++) {
        if ((u32*)(ptr+key->off+off2) & key->mask) {
            n = n->next;
            goto next_node;
        }
    }
if (n->ht_down == NULL) {
check_terminal:
    if (n->sel.flags & TC_U32_TERMINAL) {
        *res = n->res;
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
```

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

图 9.34 u32 API-destroy_key delete: `linux/net/sched/cls.u32.c`.
