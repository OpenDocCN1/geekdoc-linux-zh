Forward 723

# Figure 9.89 Scheduler API–all the disciplines: linux/net/sched/sch_api.c.

```
****************************************************
* Queuing disciplines manipulation. *
****************************************************
/* The list of all installed queuing disciplines. */
static struct qdisc_ops *qdisc_base = NULL;
```

# Figure 9.90 Scheduler API–register/unregister a discipline: linux/net/sched/sch_api.c.

```
int register_qdisc(struct qdisc_ops *qops)
{
    struct qdisc_ops *q, **qq;

    write_lock(&qdisc_mod_lock);
    for (qp = &qdisc_base; (q**qp)!=NULL; qp = &qp->next) {
        if (strcmp(qops->id, q->id) == 0) {
            write_unlock(&qdisc_mod_lock);
            return -EEXIST;
        }
    }
    
    if (qops->enqueue == NULL) {
        qops->enqueue = nop_qdisc_ops.enqueue;
    }
    if (qops->dequeue == NULL) {
        qops->dequeue = nop_qdisc_ops.dequeue;
    }
    if (qops->deque == NULL) {
        qops->deque = nop_qdisc_ops.deque;
    }

    qops->next = NULL;
    *qp = qops;
    write_unlock(&qdisc_mod_lock);
    return 0;
}

int unregister_qdisc(struct qdisc_ops *qops)
{
    struct qdisc_ops *q, **qq;
    int err = -ENOENT;

    write_lock(&qdisc_mod_lock);
    for (qp = &qdisc_base; (q**qp)!=NULL; qp = &qp->next) {
        if (q == qops) {
            break;
        }
    }
    if (q) {
        *qp = q->next;
        q->next = NULL;
        err = 0;
    }
```