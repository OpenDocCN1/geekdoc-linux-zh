# 774 TCP/IP and Linux Protocol Implementation

```
789  idle = (1/W - i)*(-true,avgidle)
790  or
791  idle = (1 - W*)(-cl->avgidle);
792  */
793  idle = (-avgidle) - ((-avgidle) >> ewma_log);
794
795  /*
796  That is not all.
797  To maintain the rate allocated to the class,
798  we add to uptime virtual clock,
799  necessary to complete transmitted packet.
800  (len/phys_bandwidth has been already passed
801  to the moment of cbq_update)
802  */
803  idle -= L2T(aq->link, len);
804  idle += L2T(cl, len);
805
806  PSCHED_AUDIT_TDIFF(idle);
807
808  PSCHED_TADD2(q->now, idle, cl->undertime);
```

Figure 9.172 CBQ—update each level's occupancy: linux/net/sched/sch_cbq.c.

```
810 } else {
811   /* Underlimit */
812
813   PSCHED_SET_PASTERFECT(cl->undertime);
814   if (avgidle > cl->maxidle)
815     cl->avgidle = cl->maxidle;
816   else
817     cl->avgidle = avgidle;
818
819   }\n820   cl->last = q->now;
821
822  cbq_update_toplevel(q, this, q->tx_borrowed);
823 }
```

If a level is underlimit, we may need to lend capacity.

Figure 9.173 CBQ—underlimit actions: linux/net/sched/sch_cbq.c.

```
825 static __inline_ struct cbq_class *
826   cbq_under_limit(struct cbq_class *cl)
827 {
828   struct cbq_sched_data *q = (struct cbq_sched_data*)cl->qdisc->data;
829   struct cbq_class *this_cl = cl;

```