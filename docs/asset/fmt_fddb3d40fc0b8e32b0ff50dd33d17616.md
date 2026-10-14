
```c
init_timer(&q->wd_timer);
q->wd_timer.data = (unsigned long)sch;
q->wd_timer.function = cbq_dog;
init_timer(&q->delay_timer);
q->delay_timer.data = (unsigned long)sch;
q->delay_timer.function = cbq_unday;
q->toplevel = TC_CBQ_MAXLEVEL;
PSCHED_GET_TIME(q->now);
q->now_rt = q->now;
cbq_link_class(&q->link);
if (tb[TC_CBQ_LSSOPT]) {
    cbq_set_lss(&q->link, RTA_DATA(tb[TC_CBQ_LSSOPT]));
  }
  cbq_addprio(q, &q->link);
  return 0;
```

# TCP/IP 和 Linux 协议实现

现在我们管理整个系统。

## 图 9.186 CBQ-剪入与裁剪类 i：`linux/net/sched/sch_cbq.c`

```c
static int cbq_graft(struct Qdisc *sch, unsigned long arg, struct Qdisc *new,
    struct Qdisc *old)
{
    struct cbq_class *cl = (struct cbq_class*)arg;
    if (cl) {
        if (new == NULL) {
            if ((new = qdisc_create_dflt(sch->dev, &pfifo_qdisc_ops)) == NULL) {
                return -ENOMEM;
            } else {
        }
    }
    #ifdef CONFIG_NET_SCH_POLICY
    if (cl->policy & TC_POLICE_CLASS)
        new->reshape_fail = cbq_reshape_fail;
    #endif
    sch_tree_lock(sch);
    *old = cl->q;
    cl->q = new;
    qdisc_reset(*old);
    sch_tree_unlock(sch);
    return 0;
    }
    return -ENOENT;
}
```

## 图 9.187 CBQ-剪入与裁剪类 ii：`linux/net/sched/sch_cbq.c`

```c
static struct Qdisc *cbq_leaf(struct Qdisc *sch, unsigned long arg)
{
    struct cbq_class *cl = (struct cbq_class*)arg;
    return cl->q;
}
static unsigned long cbq_get(struct Qdisc *sch, u32 classid)
{
    struct cbq_sched_data *q = (struct cbq_sched_data*)sch->data;
    struct cbq_class *cl = cbq_class_lookup(q, classid);
    if (cl) {
        cl->refcnt++;
        return (unsigned long)cl;
    }
    return 0;
}
```

## 图 9.188 CBQ-剪入与裁剪类 iii：`linux/net/sched/sch_cbq.c`

```c
static void cbq_destroy_filters(struct cbq_class *cl)
{
    struct tc_proto *tp;

    while (tp = cl->filter_list) {
        cl->filter_list = tp->next;
        tp_destroy(tp);
    }
}
static void cbq_destroy_class(struct cbq_class *cl)
{
    cbq_destroy_filters(cl);
    qdisc_destroy(cl);
    qdisc_put_rtab(cl->rtab);
    #ifdef CONFIG_NET_ESTIMATOR
    qdisc_kill_estimator(&cl->stats);
    #endif
    free(cl);
}
```

## 图 9.189 CBQ：`linux/net/sched/sch_cbq.c`

```c
static int
cbq_change_class(struct Qdisc *sch, u32 classid, u32 parent, struct rtattr *tca,
    unsigned long *arg)
{
    int err;
    struct cbq_sched_data *q = (struct cbq_sched_data*)sch->data;
    struct cbq_class *cl = (struct cbq_class*)arg;
    struct rtattr *tp = tca[TC_OPTIONS-1];
    struct rtattr *rttr = tca[TC_CBQ_MAX];
    struct cbq_class *parent;
    struct qdisc_rate_table *rtab = NULL;

    if (opt==NULL)
        rtattr_parse(tb, TC_CBQ_MAX, RTA_PAYLOAD(opt));
        return -EINVAL;

    if (tb[TC_CBQ_OVL_STRGY] &&
        RTA_PAYLOAD(tb[TC_CBQ_OVL_STRGY]) < sizeof(struct tc_cbq_ovl))
        return -EINVAL;

    if (tb[TC_CBQ_FOPT] &&
        RTA_PAYLOAD(tb[TC_CBQ_FOPT]) < sizeof(struct tc_cbq_fopt))
        return -EINVAL;

    #ifdef CONFIG_NET_CLS_POLICY
        if (tb[TC_CBQ_POLICE] &&
        RTA_PAYLOAD(tb[TC_CBQ_POLICE]) < sizeof(struct tc_cbq_policy))
            return -EINVAL;
    #endif

    if (cl) {
        /* Check parent */
        if (parentid) {
            if (cl->tparent && cl->tparent->classid == parentid)
                return -EINVAL;
            if (!cl->tparent || cl->tparent->classid != TC_ROOT)
                return -EINVAL;
        }
    }
    if (tb[TC_CBQ_RATE-1]) {
        rtab = qdisc_get_rtab(RTA_DATA(tb[TC_CBQ_RATE-1]), tb[TC_CBQ_RTAB-1]);
        if (rtab == NULL)
            return -EINVAL;
    }
```

## 图 9.190 CBQ：`linux/net/sched/sch_cbq.c`
