# Figure 9.188 CBQ–grafting and pruning classes iii: linux/net/sched/sch_cbq.c.

```
static void cbq_destroy_filters(struct cbq_class *cl)
{
    struct tcf_proto *tp;

    while (tp = cl->filter_list) != NULL) {
        cl->filter_list = tp->next;
        tp->ops->destroy(tp);
    }
}
}

static void cbq_destroy_class(struct cbq_class *cl)
{
    cbq_destroy_filters(cl);
    qdisc_destroy(cl->oq);
    qdisc_put_rtab(cl->R_tab);
#ifdef CONFIG_NET_ESTIMATOR
    qdisc_kill_estimator(&cl->stats);
#endif
    free(cl);
}
```

# Figure 9.189 CBQ: linux/net/sched/sch_cbq.c.

```
static int
cbq_change_class(struct qdisc *sch,, u32 classid, u32 parent, struct rtattr *tca,
    unsigned signed long *arg)
{
    int err;
    struct cbq_sched_data *q = (struct cbq_sched_data*)sch->data;
    struct cbq_class *cl = (struct cbq_class*)arg;
    struct rtattr *tp = tca[TCA_OPTIONS-1];
    struct rtattr *rttr = tca[TCA_CBQ_MAX];
    struct cbq_class *parent;
    struct qdisc_rate_table *rtab = NULL;

    if (opt==NULL)
        rtattr_parse(tb, TCA_CBQ_MAX, RTA_PAYLOAD(opt));
        return -EINVAL;

    if (tb[TCA_CBQ_OVL_STRATEGY-1] &&
        RTA_PAYLOAD(tb[TCA_CBQ_OVL_STRATEGY-1]) < sizeof(struct tc_cbq_ovl))
        return -EINVAL;

    if (tb[TCA_CBQ_FOPT-1] &&
        RTA_PAYLOAD(tb[TCA_CBQ_FOPT-1]) < sizeof(struct tc_cbq_fopt))
        return -EINVAL;
```