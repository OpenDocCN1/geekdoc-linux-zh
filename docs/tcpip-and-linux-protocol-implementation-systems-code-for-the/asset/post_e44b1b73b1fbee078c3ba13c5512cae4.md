
## Classifier Statistics

**Figure 9.24** Classifier--dump output: linux/net/sched/cls_api.c.

```c
struct tcf_dump_args
{
    struct tcf_walker *w;
    struct tcf_buff *skb;
    struct netlink_callback *cb;
};

static int tcf_node_dump(struct tcf_proto *tp, unsigned long n, struct tcf_walker *arg)
{
    struct tcf_dump_args *a = (void*)arg;
    return tcf_fill_node(a->skb, tp, NETLINK_CB(a->cb)->pid,
                         a->nlh->nlmsg_seq, NLMMSG_F_MULTI, RTM_NEWFILTER);
}
```

**Figure 9.25** Classifier--dump output: linux/net/sched/cls_api.c.

```c
static int tcm_dump_filter(struct sk_buff *skb, struct netlink_callback *cb)
{
    int t;
    int s_t;
    struct net_device *dev;
    struct qdisc *qdisc;
    struct tcf_proto *tp, **chain;
    struct nlmsg *tcm = (struct nlmsg*)NLMSG_DATA(cb->nlh);
    unsigned long cl = 0;
    struct qdisc_class_ops *ops;
    struct tcf_dump_args *arg;

    if (cb->nlmsg_len < NLMMSG_LENGTH(sizeof(*tcm)))
        return skb->len;
    if ((dev == dev_get_by_index(tcm->tcm_index)) == NULL)
        return skb->len;

    read_lock(&qdisc,tree_lock);
    if ((tcm->tcm_parent))
        q = dev->qdisc_sleeping;
    else
        q = qdisc_lookup(dev, TC_H_MAX(tcm->tcm_parent));
    if (q == NULL) {
        read_unlock(&qdisc,tree_lock);
        dev_put(dev);
        return skb->len;
    }
    if ((ops = q->ops->cl_cl) == NULL)
        goto error;
    if (TC_H_MIN(tcm->tcm_parent))
        cl = ops->get(q, tcm->tcm_parent);
    if (cl == 0)
```

**Figure 9.26** Classifier--dump output: linux/net/sched/cls_api.c.

```c
383 goto errout;
384 }
385 chain = ops->tcf_chain(q, cl);
386 if (chain == NULL)
387 goto errout;
388 
389 s_t = cb->args[0];
391 for (tp=chain, t=0; tp=tp->next, t++) {
392 if (t < s_t) continue;
393 if (TC_H_MAX(t->tcm_info) &&
394 TC_H_MAX(t->tcm_info) != tp->prio)
395 continue;
396 if if (TC_H_MIN(t->tcm_info) &&
397 TC_H_MIN(t->tcm_info) != tp->protocol)
398 continue;
399 if (t > s_t) {
400 memset(&cb->args[i], 0, sizeof(cb->args)[cb->args]));
401 if (cb->args[i] == 0) {
402 if (tc_fill_node(sk, tp, 0, NETLINK_CB(cb->skb).pid) <= 0) {
403 break;
404 }
405 }
406 if (cb->nlh->nlmsg_seq, NLM_MULTIPLE, RTM_NEWFILTER) <= 0)
407 cb->args[i] = 1;
408 }
409 if (tp->ops->walk == NULL)
410 continue;
411 arg->v.fn = tcf_node_dump;
412 arg->skb = skb;
```

**Figure 9.27** Classifier--initialization: linux/net/sched/cls_api.c.

```c
436 int init_tc_filter(void);
437 {
438 #ifdef CONFIG_RTLINK
439 struct rtnetlink_link *elem_p = rtnetlink_links[PF_UNSPEC];
440 
441 /* Setup rtnetlink links. It is made here to avoid
442 exporting large number of public symbols. */
443 
444 if (link_p) {
445 link_p[RTM_NEWFILTER-RTM_BASE] = tc_ctl_filter;
446 link_p[RTM_DELFILTER-RTM_BASE] = tc_ctl_filter;
447 link_p[RTM_GETFILTER-RTM_BASE] = tc_ctl_filter;
448 link_p[RTM_GETSTATS-RTM_BASE] = tcf_dump;
449 }
450 #endif
```

```c
452 #define INIT_TC_FILTER(name) {
453     extern struct tcf_proto_ops name##_ops;
454     register_tcf_proto_ops(&name##_ops);
455 }
456 
457 #ifdef CONFIG_NET_CLS_U32
458     INIT_TC_FILTER(u32)
459 #endif
460 #ifdef CONFIG_NET_CLS_ROUTE
461     INIT_TC_FILTER(route4)
462 #endif
463 #ifdef CONFIG_NET_CLS_FW
464     INIT_TC_FILTER(fw)
465 #endif
466 #ifdef CONFIG_NET_CLS_RSVP
467     INIT_TC_FILTER(rsvp)
468 #endif
469 #ifdef CONFIG_NET_CLS_TCINDEX
470     INIT_TC_FILTER(tcindex)
471 #endif
472 #ifdef CONFIG_NET_CLS_RSVP6
473     INIT_TC_FILTER(rsvp6)
474 #endif
475     return 0;
476 }
```

## Universal Classifiers

The u32 classifier is such a common thing that it has its own form.

**Figure 9.18** Universal 32-bit classifier API–global data: linux/net/sched/cls_u32.c.

```c
56 struct tc_u_node
57 {
58     struct tc_u_node *next;
59     unsigned int handle;
60     struct tc_u_hnode *ht_up;
61 #ifdef CONFIG_NET_CLS_POLICE
62     struct tcf_police *police;
63 #endif
64     struct tcf_result res;
65     struct tc_u_node *ht_down;
66     struct u32_sel sel;
67 };
68 
69 struct tc_u_hnode
70 {
71     struct tc_u_node *next;
72     unsigned int handle;
73     struct tc_u_common *tp_c;
74     int refcnt;
75     unsigned int divisor;
76     unsigned int hgenerator;
77     struct tc_u_node *ht[1];
78 };
```

```c
80 struct tc_u_common
81 {
82     struct tc_u_common *next;
83     struct tc_u_hnode *hlist;
84     struct qdisc *q;
85     int refcnt;
86     unsigned int hgenerator;
87 };
88 
89 static struct tc_u_common *u32_list;
90 static __inline__ unsigned u32_hash_fold(u32 key, struct u32_sel *sel)
91 {
92     unsigned int h = key & sel->hmask;
93     h = h>>16;
94     h = h>>8;
95     return h;
96 }
```

**Figure 9.29** u32 API-the classifier: linux/net/sched/cls_u32.c.

```c
101 struct {
102
103     struct tc_u_node *knode;
104     u8 *ptr;
105 } stack[TC_U32_MAXDEPTH];
106 
107 struct tc_u_hnode *ht = (struct tc_u_hnode*)tp->root;
108 u8 *ptr = skb->nh->raw;
109 struct tc_u_node *n;
110 int sdepth = 0;
111 int off2 = 0;
112 int sel = 0;
113 int i;
114 
115 if (defined(__i386__)) && !defined(__mc68)) {
116     if ((unsigned long)ptr & 3)
117         return -1;
118 }
119 
120 next_ht:
121 n = ht[sel];
122 
123 next_node;
124 if (n) {
125     struct tc_u32_key *key = n->sel.keys;
126 
127     for (i = n->sel.keys; i>0; i++) {
128         if ((u32*)(ptr+key->off+off2) & key->mask) {
129             n = n->next;
130             goto next_node;
131         }
132 }
133 if (n->ht_down == NULL) {
134 check_terminal:
135     if (n->sel.flags & TC_U32_TERMINAL) {
136         *res = n->res;
137     #ifdef CONFIG_NET_CLS_POLICY
138         if (n->policy) {
139             int pol_res = tcf_policy(skb, n->policy);
140             if (pol_res >= 0) return pol_res;
141         } else {
142             return 0;
143     }
114 #endif
145     n = n->next;
146     goto next_node;
147 }
148 /* PUSH */
149 if (depth > TC_U32_MAXDEPTH)
150     goto deadloop;
151 
152 stack[depth].node = n;
153 stack[depth].ptr = ptr;
154 depth++;
155 ht = n->ht_down;
156 sel = 0;
157 if (ht->divisor) {
158     sel = u32_hash_fold((u32*)(ptr+n->sel.off), n->sel);
159     off2 = n->sel.shift;
160 }
161 if (n->sel.flags & TC_U32_VAR_OFFSET) {
162     ptr += off2;
163     off2 = 0;
164 }
165 if (ptr < skb->tail)
166     goto next_ht;
167 
168 /* POP * */
169 if (sdepth--) {
170     n = stack[sdepth].knode;
171     ht = n->ht_up;
172     ptr = stack[sdepth].ptr;
173     goto check_terminal;
174 }
175 return -1;
176 
177 deadloop:
178 if (!net_ratelimit())
179     printf("cls_u32: dead loop\n");
180 return -1;
```

There are lookup functions and other functions functions.

**Figure 9.31** u32 API--lookup functions: linux/net/sched/cls.u32.c.

```c
static __inline__ struct tc_u_hnode *
u32_lookup_ht(struct tc_u_common *tp_c, u32 handle)
{
    struct tc_u_hnode *ht;

    for (ht = tp_c->blist; ht; ht = ht->next)
        if (ht->handle == handle)
            break;

    return ht;
}

static __inline__ struct tc_u_knode *u32_lookup_key(struct tc_u_hnode *ht, u32 handle)
{
    unsigned sel;
    struct tc_u_knode *n;

    sel = TC_U32_HASH(handle);
    if (sel > ht->divisor)
        return 0;

    for (n = ht[sel]; n; n = n->next)
        if (n->handle == handle)
            return n;

    return NULL;
}
```

**Figure 9.32** u32 API–miscellaneous support: linux/net/sched/cls_u32.c.

```c
static unsigned long u32_get(struct tcf_proto *tp, u32 handle)
{
    struct tc_u_hnode *ht;
    struct tc_u_common *tp_c = tp->data;
    if (TC_U32_HTID(handle) == TC_U32_ROOT)
        ht = tp->root;
    else
        ht = u32_lookup_ht(tp_c, TC_U32_HTID(handle));
    if (!ht)
        return 0;
    if (TC_U32_KEY(handle) == 0)
        return (unsigned long)ht;
    return (unsigned long)u32_lookup_key(ht, handle);
}

static void u32_put(struct tcf_proto *tp, unsigned long f)
{
    int i = 0x800;
    // logic truncated based on OCR
}
```

## Starting Up the Classifier System

**Figure 9.33** u32 API–initialization: linux/net/sched/cls_u32.c.

```c
static int u32_init(struct tcf_proto *tp)
{
    struct tc_u_hnode *ht;
    struct tc_u_common *tp_c;
    MOD_INDEX_USE_COUNT;
    for (tp_c = u32_list; tp_c; tp_c = tp_c->next)
        if (tp_c->q == tp->q)
            break;
    ht = kmalloc(sizeof(*root_ht), GFP_KERNEL);
}
```
