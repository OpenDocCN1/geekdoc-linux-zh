# Figure 9.180 CBQ-main dequeue function: linux/net/sched/sch_cbq.c.

```
for (;;) {
    q->wd_expires = 0;
    skb = cbq_dequeue_i(sch);
    if (skb) {
        sch->qlen--;
        sch->flags &= ~TCQ_F_THROTTLED;
        return skb;
    }

    /* All the classes are overlimit.
       It is possible, if:
       1. Scheduler is empty.
       2. Toplevel cutoff off inhibited borrowing.
       3. Root class is overlimit.

       Reset 2d and 3d conditions and retry.

       Note, that ns and cbq-2.0 are buggy, peaking
       an arbitrary class is appropriate for ancestor-only
       sharing, but not for toplevel algorithms.

       Our version is better, slower, because it requires
       two passes, but it is unavoidable with top-level sharing.
    */
    if (q->toplevel == TC_CBQ_MAXLEVEL &&
        PSCHED_IS_PASTERFECT(q->link.undertime)) {
        break;
        q->toplevel = TC_CBQ_MAXLEVEL;
        PSCHED_SET_PASTERFECT(q->link.undertime);
    }
```

# Figure 9.181 CBQ-main dequeue function: linux/net/sched/sch_cbq.c.

```
/* No packets in scheduler or nobody wants to give them to us :-
   Sigh-, start watchdog timer in the last class. */
if (sch->qlen) {
    sch->stats.overlimits++;
    if (q->wd_expires && !netif_queue_stopped(sch->dev)) {
        long delay = PSCHED_US2JIFFIES(q->wd_expires);
        del_timer(&q->wd_timer);
        if (delay < 0) {
            delay = 0;
        }
        q->wd_expires = jiffies + delay;
        add_timer(&q->wd_timer);
        sch->flags |= TCQ_F_THROTTLED;
    }
```