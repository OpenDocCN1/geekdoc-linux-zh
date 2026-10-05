# Figure 9.178 CBQ–1: linux/net/sched/sch_cbq.c.

```
968 static __inline__ * sched_buff *
969 cbq_dequeue_i(struct qdisc *sch) 
970 {
971     struct cbq_sched_data *q = (struct cbq_sched_data *)sch->data;
972     struct sk_buff *skb;
973     unsigned int activemask;
974 
975     activemask = q->activemask&0xFF;
976     while (activemask) {
977         int prio = ffs(activemask);
978         activemask &= ~(1<<prio);
979         skb = cbq_dequeue_prio(sch, prio);
980         if (skb)
981             return skb;
982     }
983     return NULL;
984 }
```

# Figure 9.179 CBQ–main dequeue function: linux/net/sched/sch_cbq.c.

```
986 static struct sk_buff *
987 cbq_dequeue(struct qdisc *sch)
988 {
989     struct sk_buff *skb;
990     struct cbq_sched_data *q = (struct cbq_sched_data *)sch->data;
991     psched_time_t now;
992     psched_tdiff_t incr;
993 
994     PSCHED_GET_TIME(now);
995     incr = PSCHED_TIFF(now, q->now_rt);
996 
997     if (q->tx_class) {
998         psched_tdiff_t incr2;
999         /* Time integrator. We calculate EOS time */
1000         by adding expected packet transmission time.
1001         If real time is greater, we warp artificial clock,
1002         so that:
1003         */
1004         cbq_time = max(real_time, work);
1005         /* / */
1006         incr2 = L2T(L2T(q->link, q->tx_len)););
1007         PSCHED_TADD(q->now, incr2);
1008         cbq_update(q);
1009         if ((incr - incr2) < 0)
1010             incr = 0;
1011     }
1012     PSCHED_TADD(q->now, incr);
1013     q->now_rt = now;
```