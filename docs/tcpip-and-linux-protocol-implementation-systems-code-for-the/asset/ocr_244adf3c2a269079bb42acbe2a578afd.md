546 delay == <-cl->avggidle) << (-cl->avggidle) >> -ewma_log);

547 if (cl->avggidle < cl->minidle);

548 cl->avggidle = cl->minidle;

549 PSCHED_TADU2(q->now, delay, cl->undertime);

551 if (delay > 0) {

552 sched << PSCHED_US2JIFFIE(delay) + cl->penalty);

553 cl->penalized = sched;

554 cl->cpriority = TC_CB_MAXPRIO;

555 q->pmask |= (1<<TC_CB_MAXPRIO);

556 if (del_timer(&q->delay_timer, sched) > 0) {

557 (long)q->delay_timer.expires = sched;

558 add_timer(&q->delay_timer);

559 cl->delayed = 1;

560 q->xstats.operations++;

562 return;

563 delay = 1;

565 }

566 if (q->wd_expires == 0 || q->wd_expires > delay) {

567 q->wd_expires = delay;

568 }

![](bbox=[0.139, 0.477, 0.843, 0.49])

```
/* TC_CB_OVL_LOWPRIO: penalize class by lowering its priority band */
```

```
static void cbq_ovl_lowvrio(struct cbq_class *cl)
```

```
{
```

```
struct cbq_sched_data *q = (struct cbq_sched_data*)cl->qdisc_data;
```

```
cl->penalized = jiffies + cl->penalty;
```

```
if (cl->cpriority != cl->cpriority2) {
```

```
cl->cpriority = cl->cpriority2;
```

```
q->pmask |= (1<<cl->cpriority);
```

```
cl->xstats.operations++;
```

```
}
```

```
cbq_ovl_classic(cl);
```

```
}
```

```
/* TC_CB_OVL_DROP: penalize class by dropping * */
```

```
static void cbq_ovl_drop(struct cbq_class *cl)
```

```
{
```

```
if (cl->q->ops->drop) {
```

```
if (cl->q->ops->drop(cl->q)) {
```

```
cl->qdisc->q.qlen;
```

```
cl->xstats.operations++;
```

```
cbq_ovl_classic(cl);
```

```
}
```