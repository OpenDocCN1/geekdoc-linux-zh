Figure 9.100 Scheduler API–allocate and initialize new queue discipline: linux/net/
sched/sch_api.c.

```
431  skb_queue_head_init(&sch->);
432
433  if (handle == TC_H_INGRESS)
434      sch->flags |= TCQ_F_INGRESS;
435
436      sch->ops = ops;
437      sch->enqueue = ops->enqueue;
438      sch->dequeue = ops->dequeue;
439      sch->dev = dev;
440      atomic_set(&sch->refcnt, 1);
441      sch->lock = &dev->queue_lock;
442  if (handle == 0)
443      handle = qdisc_alloc(dev);
444      err = -ENOMEM;
445      if (handle == 0)
446          goto err_out;
447
448  }
449  if (handle == TC_H_INGRESS)
450      sch->handle = TC_H_MAKE(TC_H_INGRESS, 0);
451  else
452      sch->handle = handle;
453
454  if (ops->init || (ops->init(sch, tca[TCA_OPTIONS-1])) == 0) {
455      write_lock(&qdisc_tree_lock);
456      sch->next = &qdisc_list;
457      dev->qdisc_list = sch;
458      write_unlock(&qdisc_tree_lock);
459  #ifdef CONFIG_NET_ESTIMATOR
460      if (tca(TCA_RATE-1))
461          qdisc_new_estimator(&sch, tca(TCA-RATE-1));
462  #endif
463      return sch;
464}
465
466 err_out:
467  *err = err;
468  if (sch)
469      kfree(sch);
470  return NULL;
471}
```

Figure 9.101 Scheduler API–modify new queue discipline: linux/net/sched/sch_api.c.

```
473  static int qdisc_change(struct qdisc *sch, struct rtattr **tca)
474  {
475      if (tca(TCA_OPTIONS-1)) {
476          int err;
477
478          if (sch->ops->change == NULL) {
```