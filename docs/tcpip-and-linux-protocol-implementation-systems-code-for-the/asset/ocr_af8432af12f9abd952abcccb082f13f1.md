# 768 TCP/IP and Linux Protocol Implementation

```
499
500  for (b = cl->borrow; b = b->borrow) {
501      delay = PSCHED_TDIFF(b->undertime, q->now);
502      if (delay < base_delay) {
503          if (delay <= 0) {
504              delay = 1;
505              base_delay = delay;
506
507      }
508  }
509  q->wd_expires = delay;
510
511}
```

Figure 9.162 CBQ-overlimit: rectify: linux/net/sched/sch_cbq.c.

```
513  /* T_TC_CBQ_OVL_RCLASSIC: penalize by offtime classes in hierarchy, when
514  they go overlimit
515  */
516  static void cbq_ovl_rclassic(struct cbq_class *cl)
517  {
518      struct cbq_shared_data *q = (struct cbq_shared_data *q)->cl->qdisc-data;
519      struct cbq_class *this = cl;
520
521      do {
522          if (cl->level > q->tolevel) {
523              cl = NULL;
524              break;
525          }
526      } while ((cl = cl->borrow) != NULL);
527
528      if (cl == NULL) {
529          cl = this;
530          cbq_ovl_classic(cl);
531  }
```

Figure 9.163 CBQ-overlimit: delay: linux/net/sched/sch_cbq.c.

```
534  /* T_TC_CBQ_OVL_DELAY: delay until it will go to underlimit */
535
536  static void cbq_ovl_delay(struct cbq_class *cl)
537  {
538      struct cbq_shared_data *q = (struct cbq_shared_data *q)->cl->qdisc-data;
539      psched_tdiff.t delay = PSCHED_TDIFF(cl->undertime, q->now);
540
541      if (!cl->deloaded) {
542          unsigned long sched = jiffies;
543
544          delay += cl->offtime;
545          if (cl->avgidle < 0)
```