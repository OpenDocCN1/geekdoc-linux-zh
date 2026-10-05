# 822 TCP/IP and Linux Protocol Implementation

# Figure 9.260 RED–drop: linux/net/sched/sch_red.c.

```
static int
red_drop(struct qdisc *skb)
{
    struct sk_buff *skb;
    struct red_sched_data *q = (struct red_sched_data *)skb->data;
    skb = NULL; __skb_dequeue_tail(skb->q);
    if (skb) {
        skb->stats.backlog -= skb->len;
        skb->stats.drops++;
        q->stat.other++;
        kfree(skb);
        return 1;
    }
    PSCHED_GET_TIME(q->qidlestart);
    return 0;
}
```

# Figure 9.261 RED–reset: linux/net/sched/sch_red.c.

```
static void red_reset(struct qdisc *sch)
{
    struct red_sched_data *q = (struct red_sched_data *)skb;
    struct sk_buff *skb;

    while ((skb = skb_dequeue(sch->q)) != NULL) {
        kfree(skb);
        sch->stats.backlog = 0;
        PSCHED_GET_PASTERFECT(q->qidlestart);
        q->qave = 0;
        q->qcount = -1;
    }
```

# Figure 9.262 RED–change: linux/net/sched/sch_red.c.

```
atomic int red_change(struct qdisc *sch, struct rtattr *opt)
{
    struct red_sched_data *q = (struct red_sched_data *)opt->data;
    struct rtattr *tb = tb[TCA_RED_STAB];
    struct tc_qdisc_opt *ctl;
    if (opt = rparse(tb, TCA_RED_STAB, RTA_DATA(opt), RTA_PAYLOAD(opt)) == NULL ||n        tb[TCA_RED_PARMS-1] == 0 || tb[TCA_RED_STAB-1] == 0 ||
        RTA_PAYLOAD(tb[TCA_RED_PARMS-1]) < sizeof(ctl) ||
        RTA_PAYLOAD(tb[TCA_RED_STAB-1]) < 256)
        return -EINVAL;
    ctl = RTA_DATA(tb[TCA_RED_PARMS-1]);
    sch_tree_lock(sch); *
```