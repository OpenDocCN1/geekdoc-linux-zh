
# 图 9.179 CBQ–主出队列函数: `linux/net/sched/sch_cbq.c`

```c
static struct sk_buff *
cbq_dequeue(struct qdisc *sch)
{
    struct sk_buff *skb;
    struct cbq_sched_data *q = (struct cbq_sched_data *)sch->data;
    psched_time_t now;
    psched_tdiff_t incr;

    PSCHED_GET_TIME(now);
    incr = PSCHED_TIFF(now, q->now_rt);

    if (q->tx_class) {
        psched_tdiff_t incr2;
        /* 时间积分器。我们通过加上期望的数据传输时间
           计算 EOS 时间。
           如果真实时间更大，我们扭曲人工时钟，
           使得：
        */
        cbq_time = max(real_time, work);
        /* / */
        incr2 = L2T(L2T(q->link, q->tx_len)););
        PSCHED_TADD(q->now, incr2);
        cbq_update(q);
        if ((incr - incr2) < 0)
            incr = 0;
    }
    PSCHED_TADD(q->now, incr);
    q->now_rt = now;
}
```

# 图 9.180 CBQ-main 出队函数：`linux/net/sched/sch_cbq.c`

```c
for (;;) {
    q->wd_expires = 0;
    skb = cbq_dequeue_i(sch);
    if (skb) {
        sch->qlen--;
        sch->flags &= ~TCQ_F_THROTTLED;
        return skb;
    }

    /* 所有类都超出了限制。
       可能的情况是如果：
       1. 调度器为空。
       2. 顶层裁剪抑制了借用。
       3. 根类超限。

       重置 2d 和 3d 条件并重试。

       注意，ns 和 cbq-2.0 存在缺陷，峰值
       任意类对于祖先级共享是合适的，
       但不适用于顶层算法。

       我们的版本更好、也更慢，因为它需要
       两次遍历，但在顶层共享中这是不可避免的。
    */
    if (q->toplevel == TC_CBQ_MAXLEVEL &&
        PSCHED_IS_PASTERFECT(q->link.undertime)) {
        break;
        q->toplevel = TC_CBQ_MAXLEVEL;
        PSCHED_SET_PASTERFECT(q->link.undertime);
    }
}
```

# 图 9.181 CBQ-main 出队函数：`linux/net/sched/sch_cbq.c`

```c
/* 调度器中没有包，或者没有人想把包交给我们 :-
   唉，在最后一个类启动看门狗定时器。 */
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
}
  return NULL;
}
```

# 图 9.182 CBQ-维护函数：`linux/net/sched/sch_cbq.c`

```c
/* CBQ 类维护程序 */
static void cbq_adjust_levels(struct cbq_class *this)
{
  if (this == NULL)
    return;

  do {
    int level = 0;
    struct cbq_class *cl;

    if ((cl = this->children) != NULL)
      do {
        if (cl->level > level)
          level = cl->level;
      } while ((cl = cl->sibling) != this->children);

    this->level = level+
  } while ((this = this->tparent) != NULL);
}
```

我们初始化 CBQ 机制。

# 图 9.183 CBQ-初始化 CBQ i：`linux/net/sched/sch_cbq.c`

```c
static int cbq_init(struct cbq_class *tb, struct qdisc *qdisc, struct rtattr *opt)
{
  struct cbq_sched_data *sq = (struct cbq_sched_data*)qdisc->data;
  struct rtattr *rt = tb[TC_CBQ_MAX];
  struct tc_rspec *rc;
  if (rt_params(tb, TC_CBQ_MAX, RTA_DATA(opt), RTA_PAYLOAD(opt)) < 0 ||
      tb[TC_CBQ_RATE-1] == NULL || tb[TC_CBQ_RATE-1] == NULL ||
      RTA_PAYLOAD(tb[TC_CBQ_RATE-1]) < sizeof(struct tc_rspec))
    return -EINVAL;
  if (tb[TC_CBQ_LSOPT] && RTA_PAYLOAD(tb[TC_CBQ_LSOPT]) < sizeof(struct tc_rspec))
    return -EINVAL;
  r = RTA_DATA(tb[TC_CBQ_RATE-1]);

  MOD_INC_USE_COUNT;
  if ((rtab = qdisc_get_rtab(rb, tb[TC_CBQ_RTAB-1])) == NULL) {
    MOD_DEC_USE_COUNT;
    return -EINVAL;
  }
}
```

# 图 9.184 CBQ-初始化 CBQ ii：`linux/net/sched/sch_cbq.c`

```c
q->link.refcnt = 1;
q->link.sibling = &q->link;
q->link.classid = sch->handle;
q->link.disc = &sch;
if (!(q->link.q = qdisc_create_dflt(sch->dev, &pfifo_qdisc_ops))) {
  q->link.q = &noop_q;
  q->link.priority = TC_CBQ_MAXPRIO-1;
  q->link.priority2 = TC_CBQ_MAXPRIO-1;
  q->link.cpriority = TC_CBQ_MAXPRIO_CLASS;
  q->link.ovl_strategy = tc_cbq_ovl;
  q->link.overlimit = tc_cbq_ovl;
  q->link.alloc = psched_mtu(sch->dev);
  q->link.quantum = q->link.alloc;
  q->link.weight = q->link.rtab->rate;
  q->ewma_log = TC_CBQ_DEF_EWMA;
  q->link.avpkt = q->link.alloc/2;
  q->link.mkind = -0xFFF;
  q->link.stats.lock = &sch->dev->queue_lock;
}
```

# 图 9.185 CBQ-初始化 CBQ iii：`linux/net/sched/sch_cbq.c`
