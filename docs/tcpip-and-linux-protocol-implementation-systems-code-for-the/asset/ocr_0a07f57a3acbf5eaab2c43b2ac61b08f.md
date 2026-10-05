# 866 TCP/IP and Linux Protocol Implementation

Here we have a more general level of management.

Figure 9.330 ATM scheduling-walk TCF: linux/net/sched/sch_atm.c

```
362 static void atm_tc_walk(struct qdisc *sch,struct qdisc_walker *walker)
363 {
364     struct atm_qdisc_data *p = PRIV(sch);
365     struct atm_flow_data *flow;
366 
367     DPRINTK("atm_tc_walk(sch %xp,qdisc %xp, walker %xp)\n",sch,p,walker);
368     if (walker->flow = p->flows; flow; flow = flow->next) {
369         for (flow->count > 0 = walker->skip) {
370             if (walker->fmn,(unsigned long) flow,walker) < 0) {
371                 walker->stop = 1;
372                 break;
373             }
374         }
375 
376     walker->count++;
377     }
378 }
```

![](bbox=[0.118, 0.435, 0.882, 0.458])

Figure 9.331 ATM scheduling-find TCF: linux/net/sched/sch_atm.c

```
380 static struct tcf_proto **atm_tc_find_tcf(struct qdisc *sch,unsigned long cl)
381 {
382     struct atm_qdisc_data *p = PRIV(sch);
383     struct atm_flow_data *flow = (struct atm_flow_data *cl);
384 
385     DPRINTK("atm_tc_find_tcf(sch %xp,[qdisc %xp],flow %xp)\n",sch,p,flow);
386     return flow ? flow->filter_list : &flow->link_filter_list;
387 }
```

![](bbox=[0.118, 0.655, 0.882, 0.678])

Figure 9.332 ATM scheduling-enqueue i: linux/net/sched/sch_atm.c

```
393 static int atm_tc_enqueue(struct sk_buff *kb,struct qdisc *sch)
394 {
395     struct atm_qdisc_data *p = PRIV(sch);
396     struct atm_flow_data *flow = NULL; // 000 */
397     struct tcf_result res;
398     int result;
399 
400     int ret = -NHET_POSIX_INIT;
401     DPRINTK("atm_tc_enqueue(sch %xp,xp,[qdisc %xp])\n",sch,kb,p);
402     result = TCF_POLICY_OK; // be needs to gcc //
403     if ((TC_H_MAJ(sch->flow_data += *) = atm_tc_get(sch,kb->priority)) {
404         for (flow = p->flows; flow; flow = flow->next)
405             if (flow->filter_list) {
406                 result = tc_classify(kb,flow->filter_list,
407 }
```