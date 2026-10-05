# 830 TCP/IP and Linux Protocol Implementation

```
if ((err = tbf_change(sch, opt)) != 0) {
    MOD_DEC_USE_COUNT;
}
return err;
```

Figure 9.275 TBF—destroy: linux/net/sched/sch_tbf.c.

```
static void tbf_destroy(struct qdisc *sch) {
    struct tbf_sched_data *q = (struct tbf_sched_data *)sch->data;
    del_timer(q->vd_timer);
    if (q->P_tab) {
        qdisc_put_rtab(q->P_tab);
        if (q->R_tab) {
            qdisc_put_rtab(q->R_tab);
            MOD_DEC_USE_COUNT;
        }
    }
}
```

# 9.13.8 Ingress Queuing

Figure 9.276 Ingress queuing—ingress hook: linux/net/sched/sch.ingress.c.

```
static unsigned int
ing_hook(unsigned int hook, struct sk_buff **pskb) {
    const struct net_device *dev = *device,
    const struct net_device *outdev,
    int (*okfn)(struct sk_buff *skb);
    struct qdisc *q;
    struct sk_buff *skb = *pskb;
    struct net_device *dev = skb->dev;
    int devfree_NP_ACCEPT;
\    DPRINTK("ing_hook: skb %Xs xs->len=%lu\n",
        skb ? "owned" : "unowned",
        skb->dev ? (skb->dev)->name : "no dev",
        skb->len);

/*
revisit later: Use a private since lock dev->queue_lock is also
used on the egress (might slow things for an iota)
*/
    if (dev->ingress) {
        spin_lock(&dev->queue_lock);
        if ((q = dev->qdisc_ingress) != NULL
```