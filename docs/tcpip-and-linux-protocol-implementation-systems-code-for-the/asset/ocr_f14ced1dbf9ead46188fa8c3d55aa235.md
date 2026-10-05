# Figure 9.17 Classifier vi: linux/net/sched/cls_api.c.

```
/* Find qdisc */
if (parent) {
    q = dev->qdisc_sleeping;
    parent = q->handle;
} else if (q = qdisc_lookup(dev, TC_H_MAX(t->tcm_parent)) == NULL) {
    return -EINVAL;
}
/* Is it classified? */
if ((cops = q->ops->cls_op) == NULL) {
    return -EINVAL;
}
/* Do we search for filter, attached to class? */
if (TC_H_MIN(parent)) {
    cl = cops->get(q, parent);
    if (cl == 0)
        return -ENOENT;
}
/* And the last stroke */\nchain = cops->tcf_chain(q, cl);
err = -EINVAL;
if (chain == NULL)
    goto errout;
```

# Figure 9.18 Classifier vi: linux/net/sched/cls_api.c.

```
/* Check the chain for existence of proto-tcf with this priority */\nfor (back = chain; (tpe->back) != NULL; back = ktp->next(next)) {
    if (tp->prio != prio) {
        if (tp->prio == prio || (tp->prio != protocol && protocol))
            goto errout;
    } else {
        tp = NULL;
        break;
    }
}
if (tp == NULL) {
    /* Proto-tcf does not exist, create new one */\n    if (tca[TCA_KIND-1] == NULL || !protocol)
        goto errout;
    err = -ENOENT;
    if (n->nlmsg_type != RTM_NEWFILTER || !(n->nlmsg_flags&NLM_F_CREATE))
        goto errout;
}
```