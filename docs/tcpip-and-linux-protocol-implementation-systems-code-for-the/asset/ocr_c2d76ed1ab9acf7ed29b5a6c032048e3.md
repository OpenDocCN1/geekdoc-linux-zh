# Figure 9.210 Policer iii-locate: linux/net/sched/police.c.

```
struct tcf_police *tcf_police_locate(struct rttattr *rta, struct rttattr *est)
{
    unsigned h;
    struct tcf_police *pcp;
    struct rttattr *tb[TCA_POLICE_MAX];
    struct tcf_police *parm;

    if (rttattr_parse(tb, TCA_POLICE_MAX, RTA_DATA(rta), RTA_PAYLOAD(rta)) < 0)
        return NULL;

    if (tb[TCA_POLICE_TBF-1] == NULL)
        return NULL;

    parm = RTA_DATA(tb[TCA_POLICE_TBF-1]);

    if (parm->index && (p = tcf_police_lookup(parm->index)) != NULL) {
        p->refcnt++;
        return p;
    }

    p = kmalloc(sizeof(*p), GFP_KERNEL);
    if (p == NULL)
        return NULL;
```

```
memset(p, 0, sizeof(*p));
p->refcnt = 1;
spin_lock_init(&p->lock);
p->stats.lock = &p->lock;
if (p->rate.rate > 0)
    if ((p->R_tab = qdisc_get_rtab(&p->rate, tb[TCA_POLICE_RATE-1])) == NULL)
        goto failure;
    if (p->peakrate)
        if ((p->P_tab = qdisc_get_rtab(&p->peakrate, tb[TCA_POLICE_PEAKRATE-1])) == NULL)
            goto failure;
if (tb[TCA_POLICE_RESULT-1])
    p->result = (int*)rta->RTA_DATA(tb[TCA_POLICE_RESULT]);
#ifdef CONFIG_NET_ESTIMATOR
if (tb[TCA_POLICE_AVRATE-1])
    p->avrate_rate = (u32)rta->RTA_DATA(tb[TCA_POLICE_AVRATE-1]);
#endif
p->toks = parm->burst = parm->burst;
p->mtu = parm->mtu;
if (p->mtu == 0)
    p->mtu = 0;
if (p->R_tab)
    p->mtu = 255 << (p->R_tab->rate.rate.log_log
```