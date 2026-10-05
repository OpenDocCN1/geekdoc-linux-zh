```
static int
bfio_enqueue(struct sk_buff *skb, struct Qdisc *sch)
{
    struct fifo_sched_data *q = (struct fifo_sched_data *)sch->data;
    if (sch->backlog <= q->limit) {
        __skb_queue_tail(sch->sq, skb);
        sch->backlog += skb->len;
        sch->stats.bytes += skb->len;
        sch->stats.packets++;
    }
        sch->stats.drops++;
        return 0;
    }
#ifdef CONFIG_NET_CLS_POLICE
    if (sch->reshape_fail == NULL || sch->reshape_fail(skb, sch))\n#endif
 kfree(skb);
return -XMIT_DROP;
}
```