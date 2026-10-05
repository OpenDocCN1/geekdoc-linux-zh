# 684 TCP/IP and Linux Protocol Implementation

```
n->res.class = *(u32*)RTA_DATA(tb[TCA_U32_CLASSID-1]);
sch_tree_lock(q);
cl = _cls_net_class(n->res.class, q->ops->cl_ops->bind_tcf(q, base, n->res.
    classid);
sch_tree_unlock(q);
if (cl)
    q->ops->cl_ops->unbind_tcf(q, cl);
}
#ifdef CONFIG_NET_CLS_POLICE
if (tb[TCA_U32_POLICE-1]) {
    struct tcf_police *opt = tcf_police_locate(tb[TCA_U32_POLICE-1], est);
    sch_tree_lock(q);
    police = xchg(&n->police, police);
    sch_tree_unlock(q);
    tcf_police_release(police);
}
#endif
return 0;
```

Figure 9.38 u32 API–change parameters: linux/net/sched/cls.u32.c.

```
static int u32_change(struct tcf *proto, unsigned long base, u32 handle,
    struct rattr *etca,
    unsigned long *arg)
{
    struct tc_u_common *tp_c = tp->data;
    struct tc_u_node *ht;
    struct tc_u_node *n;
    struct tc_u32 *els;
    struct rattr *opt = tca[TCA_OPTIONS-1];
    struct rattr *tb[TCA_U32_MAX];
    u32 htid;
    int err;

    if (opt == NULL)
        return handle ? -EINVAL : 0;
    if (rtarttr_parse(tb, TCA_U32_MAX, RTA_DATA(opt), TCA_PAYLOAD(opt) < 0)
        return -EINVAL;
    if (n = (struct tc_u_node*)arg) == NULL) {
        if (TCA_U32_KEY->n->handle) == 0
            return -EINVAL;
        return u32_set_params(tp->q, base, n->ht, n, tca[TCA_RATE-1]);
    }
    if (tb[TCA_U32_DIVISOR-1]) {
        unsigned divisor = *(unsigned*)RTA_DATA(tb[TCA_U32_DIVISOR-1]);
        if (-divisor > 0x100
```