# Forwarding 821

Taking into account, that qave have fixed
point at Wlog, and Plog is related to max_P by
max_P = (qth_max_qth_min)/2;Plog; two lines
below have the following floating; point equivalent:

```
max_P*(qth_min/qth_max_qth_min) < rnd/count

Any Questions? --ANK (880924)
*/
if ((q->qave - q->qth_min)>>q->Wlog)+q->count < q->qR)
    goto enqueue;
    q->count = 0;
    q->qR = net_random()&q->Rmask;
    sch->stats.overlimits++;
    goto mark;

q->qR = net_random()&q->Rmask;
goto enqueue;
```
```

```
drop:
	skfree_skb(skb);
sch->stats.drop++;
return NET_XMIT_CN;
}
```

Figure 9.259 RED–requeue and dequeue: linux/net/sched/sched_red.c.

```
static int
red_dequeue(struct sk_buff *skb, struct qdisc *sch)
{
	struct red_sched_data *q = (struct red_sched_data*)sch->data;
	PSCHED_SET_PASTERPERFECT(q->qidlestart);

	__skb_queue_head(sch->q, skb);
	sch->stats.backlog += skb->len;
	return 0;
}

static sk_buff *
red_dequeue(struct qdisc *sch)
{
	struct sk_buff *skb = __skb*skb;
	struct red_sched_data *q = (struct red_sched_data*)sch->data;
	skb = __skb_dequeue(sch->q);
	if (skb) {
\tsch->stats.backlog -= skb->len;
		return skb;
}
	PSCHED_GET_TIME(q->qidlestart)
	return NULL;
}
```