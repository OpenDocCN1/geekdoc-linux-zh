
```c
static int
btbf_requeue(struct skb_buff *skb, struct Qdisc* sch)
{
  __skb_dequeue_head(&sch->q, skb);
  sch->stats.backlog += skb->len;
  return 0;
}

static int
btbf_drop(struct Qdisc* sch)
{
  struct skb_buff *skb;
  skb = __skb_dequeue_tail(&sch->q);
  if (skb) {
    sch->stats.backlog -= skb->len;
    sch->stats.drops++;
    kfree_skb(skb);
    return 1;
  }
}
```

图 9.269 TBF—看门狗：`linux/net/sched/sch_tbf.c`。

```c
static void tbf_watchdog(unsigned long arg)
{
  struct Qdisc *sch = (struct Qdisc*)*arg;

  sch->flags &= ~TCQ_F_THROTTLED;
  netif_schedule(sch->dev);
}
```

# 图 9.270 TBF-出队列：`linux/net/sched/sch_tbf.c`。

```c
static struct sk_buff *
tbf_dequeue(struct qdisc *q)
{
    struct tbf_sched_data *data = (struct tbf_sched_data *)q->sch->data;
    struct sk_buff *skb;

    skb = __skb_dequeue(q->sch->q);

    if (skb) {
        psched_time_t now;
        long toks;
        long ptoks = 0;

        PSCHED_GET_TIME(now);

        toks = PSCHED_TDIFF_SAFE(now, q->t_c, buffer, 0);

        if (q->P_tab) {
            ptoks = toks + q->ptoks;
            if (toks > (long)q->mtu) {
                toks = q->mtu;
            }
            ptoks -= L2T(q, skb->len);
        }
        toks += q->ptoks;
        if (toks > (long)q->buffer) {
            toks = q->buffer;
        }
        toks -= L2T(q, skb->len);
    }
}
```

# 图 9.271 TBF-出队列：`linux/net/sched/sch_tbf.c`。

```c
if ((toks-ptoks) > 0) {
    q->t_c = now;
    q->tokens = toks;
    q->ptoks = ptoks;
    sch->stats.backlog -= skb->len;
    sch->flags |= TCQ_F_THROTTLED;
    return skb;
}

if (neif_queue_stopped(sch->dev)) {
    long delay = PSCHED_US2JIFFIE(max(-toks, -ptoks));

    if (delay == 0) {
        delay = 1;
    }
    mod_timer(q->wd_timer, jiffies+delay);
}

/* 也许队列中有一个更短的数据包，
   现在可以发送。这听起来很好，
   但是，这在原理上是错误的。
   在这种情况下，我们绝对不能重排数据包。
```

# 828 TCP/IP 与 Linux 协议实现

实际上，如果将流拆分为独立的

子流，这将是一个非常好的解决方案。

这是所有 FQ 算法的核心思想

（参考 CSZ, HPQ, HFSC）

```c
_skb_queue_head(&sch->q, skb);

sch->flags |= TCQ_F_THROTTLED;
sch->stats.overlimits++;
}
return NULL;
}
```

# 图 9.272 tbf-重置：`linux/net/sched/sch_tbf.c`。

```c
static void
btbf_reset(struct disc *sch)
{
  struct tbf_sched_data *q = (struct tbf_sched_data *)sch->data;
  skb_queue_purge(&sch->q);
  sch->stats.backlog = 0;
  PSCHED_GET_TIME(q->t,c);
  q->tokens = q->buffer;
  q->tokens = q->mtu;
  sch->flags &= TCQ_F_THROTTLED;
  del_timer(&q->timer);
}
```

# 图 9.273 tbf-修改：`linux/net/sched/sch_tbf.c`。

```c
static int tbf_change(struct disc *sch, struct rtattr *opt)
{
  int err = EINVAL;
  struct tbf_sched_data *q = (struct tbf_sched_data *)sch->data;
  struct rtattr *rtab[TCA_TBF_PTAB];
  struct tc_tbf *opt;
  struct disc_rate_table *table = NULL;
  struct disc_rate_table *ptab = NULL;
  int max_size;
  if (rtattr_parse(tb, TCA_TBF_PTAB, RTA_DATA(opt)) ||
      tb[TCA_TBF_PTAB-1] == NULL ||
      RTA_payload(tb[TCA_TBF_PTAB-1]) < sizeof(*opt))
    goto done;
  qopt = RTA_DATA(tb[TCA_TBF_PTAB-1]);
  rtab = disc_get_rtab(&qopt->rate, tb[TCA_TBF_PTAB-1]);
  if (!err)
    return NULL;
  goto done;
}
```
