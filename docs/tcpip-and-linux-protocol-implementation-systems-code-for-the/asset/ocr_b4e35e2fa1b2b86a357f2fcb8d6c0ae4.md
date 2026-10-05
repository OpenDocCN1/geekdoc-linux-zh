```
577      return -EINVAL;
578  if (q->handle == 0)
579      return -ENOENT;
580  if ((err = qdisc_graft(dev, p, clid, &q)) != 0)
581      return err;
582  if (q)
583      qdisc_notify_bh(skb, n, clid, NULL);
584      spin_lock_bb(&dev->queue_lock);
585      qdisc_destroy(q);
586      spin_unlock_bb(&dev->queue_lock);
587    }
588  } else {
590    qdisc_notify(skb, n, clid, q);
591    return 0;
592  }
```

# Changing Scheduler Discipline Parameters

Figure 9.105 Scheduler API-change queue discipline entry: linux/net/sched/... api.c.

```
598  static int tc_modify_qdisc(struct sk_buff *skb, struct nlmsghdr *en, void *arg)
599  {
600      struct tcmmsg *tcm = NLMSG_DATA(n);
601      struct rtattr *tca = arg;
602      struct net_device *dev;
603      u32 clid = tcm->tcm_parent;
604      struct qdisc *q = NULL;
605      struct qdisc *p = NULL;
606      int err;
607
608      if (dev && _dev_get_by_index(tcm->ifindex) == NULL)
609          return -ENODEV;
610
611      if (clid) {
612          if (clid != TC_H_ROOT) {
613              if (clid != TC_H_INGRESS) {
614                  if ((p = qdisc_lookup(dev, TC_H_MAJ(clid))) == NULL)
615                      return -ENOENT;
616              q = qdisc_leaf(p, clid);
617          } else { /*ingress */
618              q = dev->qdisc_ingress;
619          }
620      }
621  } else {
622          q = dev->qdisc_sleeping;
623      }
624
625      /* = It may be default qdisc, ignore it +/\n626      if (q && q->handle == 0)
627          q = NULL;
```