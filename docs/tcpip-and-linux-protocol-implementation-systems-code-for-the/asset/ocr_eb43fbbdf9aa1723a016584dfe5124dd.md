# Forwarding 781

```
1411
MOD_INC_USE_COUNT;
1412
if ((q->link.R_tab = q_disc_get_rtab(rb, tb[TCA_CBQ_RTAB-1])) == NULL) {
1413
    MOD_DEC_USE_COUNT;
1414
    return -EINVAL;
1415
 }
```

# Figure 9.184 CBQ-initialize CBQ ii: linux/net/sched/sch.cbq.c.

```
1417
q->link.refcnt = 1;
1418
q->link.sibling = &q->link;
1419
q->link.classid = sch-handle;
1420
q->link.disc = &sch;
1421
if (!(q->link.q = q_disc_create_dflt(sch-dev), &pfifo_disc_opts)) {
1422
    q->link.q = &noop_q;
1423
1424
q->link.priority = TC_CBQ_MAXPRIO-1;
1425
q->link.priority2 = TC_CBQ_MAXPRIO-1;
1426
q->cpriority = TC_CBQ_MAXPRIO_CLASS;
1427
q->link.ovl_strategy = tc_cbq_ovl;
1428
q->link.overlimit = cbq_ovl_classic;
1429
q->link.alloc = psched_mtu(sch-dev);
1430
q->link.quantum = &q->link.alloc;
1431
q->link.weight = q->link.R_tab->rate.rate;
1432
1433
q->ewma_log = TC_CBQ_DEF_EWMA;
1434
q->link.avpkt = q->link.alloc/2;
1435
q->link.mkindle = -0x7FFFFFFF;
1436
q->link.stats.lock = &sch-dev->queue_lock;
```

# Figure 9.185 CBQ-initialize CBQ iii: linux/net/sched/sch.cbq.c.

```
1436
init_timer(&q->wd_timer);
1439
q->wd_timer.data = (unsigned long)sch;
1440
q->wd_timer.function = cbq_watchdog;
1441
init_timer(&q->delay_timer);
1442
q->delay_timer.data = (unsigned long)sch;
1443
q->delay_timer.function = cbq_undelay;
1444
q->toplevel = TC_CBQ_MAXLEVEL;
1445
PSCHED_GET_TIME(q->now);
1446
q->now_rt = q->now;
1447
1448
cbq_link_class(&q->link);
1449
1450
if (tb[TCA_CBQ_LSSOPT-1]) {
1451
    cbq_set_lss(&q->link, RTA_DATA(tb[TCA_CBQ_LSSOPT-1]));
1452
1453
cbq_addprio(q, &q->link);
1454
    return 0;
1455
 }
```