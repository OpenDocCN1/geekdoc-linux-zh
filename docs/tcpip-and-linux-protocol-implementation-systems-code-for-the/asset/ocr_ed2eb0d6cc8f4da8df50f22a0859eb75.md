# Figure 9.95 Scheduler API–allocate discipline to a unique handle: linux/net/sched/sch...

```
u32 qdisc_alloc_handle(struct net_device *dev)
(
    int i = 0x10000;
    static u32 authandle = TC_H_MAKE(0x80000000, O);

    do {
        authandle = TC_H_MAKE(0x100000, O);
        if (authandle = TC_H_MAKE(TC_H_ROOT, 0))
            authandle = TC_H_MAKE(0x80000000, U);
    } while (qdisc_lookup(dev, authandle) && --i > 0);

    return i>0 ? authandle : 0;
}
```

# Figure 9.96 Scheduler API–queue discipline to a device: linux/net/sched/sch...

```
/* Attach toplevel qdisc to device dev */
static struct qdisc *
dev_graft_qdisc(struct net_device *dev, struct qdisc qdisc)
{
    struct qdisc *oqdisc = qdisc;

    if (dev->flags & IFF_UP)
        dev_activate(dev);

    write_lock(&qdisc_tree_lock);
    spin_lock_bh(&dev->queue_lock);
    if (qdisc & qdisc->flags & QTC_CF_INGRESS)
        qdisc = dev->qdisc_ingress;
    /* Prune old scheduler */
    if (qdisc & atomic_read(&qdisc->refcnt) <= 1)
        /* delete */
        qdisc_reset(qdisc);
        dev->qdisc_ingress = NULL;
    } else { /* new */
        dev->qdisc_ingress = qdisc;
    }
} else {
    qdisc = dev->qdisc_sleeping;
    /* Prune old scheduler */
    if (qdisc & atomic_read(&qdisc->refcnt) <= 1)
        qdisc_reset(qdisc);
    }

    /* ... and graft new one */
    if (qdisc == NULL)
```