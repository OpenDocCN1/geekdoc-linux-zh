

# 图 9.151 CBQ类结构定义 iv：linux/net/sched/sch_cbq.c。

```c
psched_time_t      undertime;
long               avgdefile;
long               /* 用于 WRR 的保存赤字 */
unsigned long      penalized;
struct tc_stats    stats;
struct tc_cbq_xstats xxtats;
struct tcf_proto   *filter_list;
int                refcnt;
int                filters;
struct cbq_class   *defaults[TC_PRID_MAX+1];
};
```

# 图 9.152 CBQ–调度数据转发：linux/net/sched/sch_cbq.c。

```c
struct cbq_sched_data
{
struct cbq_class   *classes[16];      /* 所有类的哈希表 */
int                classes[TC_CBQ_MAXPRIO+1];
unsigned           quanta[TC_CBQ_MAXPRIO+1];
struct cbq_class   link;
unsigned           activemask;
struct cbq_class   *active[TC_CBQ_MAXPRIO+1]; /* 带有积压的 */
                                     /* 所有类的列表 */
#ifndef CONFIG_NET_CLS_POLICE
struct cbq_class   *rx_class;
#endif
struct cbq_class   *tx_class;
struct cbq_class   *tx_borrowed;
int                tx_len;
psched_time_t     now;               /* 缓存戳 */
psched_time_t     now_rt;            /* 缓存实时时间 */
unsigned           pmask;
struct timer_list delay_timer;
struct timer_list wd_timer;        /* 门狗定时器，当 CBQ 有积压但无法传输时启动 */
long               wd_expires;
int                ilevel;
u32               generator;
};
```

# 实际分类器

# 图 9.153 CBQ–分类器：linux/net/sched/cbq.c。

/* 分类数据包。该过程相当复杂，它允许我们透明地结合链路共享和优先级。具体来说，你可以将链路共享规则（例如基于路由的）放在 CBQ 的根节点，以便其解析为拆分节点。然后数据包根据逻辑优先级进行分类，或者在拆分节点上附加更具体的分类器。 */

```c
static struct cbq_class cbq_classifier(struct sk_buff *skb, struct qdisc *sch)
{
    struct cbq_class_data *q = (struct cbq_class_data*)sch->data;
    struct cbq_class *head = head->next_link;
    struct cbq_class **defmap = NULL;
    struct cbq_class *cl = NULL;
    u32 prio = skb->priority;
    struct tc_result *res;

    /* 步骤1. 如果 skb->priority 指向我们的类之一，则使用它。 */
    if (TC_HJ(prio) == 0 && (cl = cbq_class_lookup(q, prio)) != NULL)
        return cl;

    for (;;) {
        int result = 0;
        defmap = head->defaults;

        /* 步骤2. 应用分类器。 */
        if (head->filter_list (res = tc_classify(skb, filter_list, &res)) < 0)
            goto fallback;

        if ((cl = (void*)res->class) != NULL) {
            if (TC_HMJ(res->class))
                cl = cbq_class_lookup(q, res->class);
            else if ((cl = defmap[res->class&TC_PRIO_MAX]) != NULL)
                cl = defmap[TC_PRIO_BESTEFFORT];
        }

        if (cl == NULL || cl->level >= head->level)
            goto fallback;
    }
}
```

# 图 9.154 CBQ–分类器：linux/net/sched/cbq.c。

```c
#ifdef CONFIG_NET_CLS_POLICE
    switch (result) {
        case TC_POLICE_RECLASSIFY:
            return cbq_reclassify(skb, cl);
        case TC_POLICE_SHOT:
            return NULL;
    }
}
#endif
if (cl->level == 0)
    return cl;

/* 步骤3. 如果分类器选择了链路共享类，则应用特定代理的分类器。重复此过程直到遇到叶子节点。 */
head = cl;

fallback:
cl = head;
/* 步骤4. 未成功... */
if (TC_HMJ(prio) == 0 && !(cl = head->defaults[prio&TC_PRIO_MAX]) && !(cl = head->defaults[TC_PRIO_BESTEFFORT]))
    return head;

return cl;
```

# 图 9.155 CBQ–分类器：linux/net/sched/cbq.c。

```c
static struct cbq_class *cbq_reclassify(struct sk_buff *skb, struct cbq_class *this)
{
    struct cbq_class *cl, *new;

    for (cl = this->tparent; cl; cl = cl->tparent)
        if ((new = cl->defaults[TC_PRIO_BESTEFFORT]) != NULL && new != this)
            return new;

return NULL;
}
```

# 使用类

# 图 9.156 CBQ–激活或去激活类：linux/net/sched/sch_cbq.c。

/* 数据包刚入队空类。cbq_activate_class 将其添加到对应优先级活动列表的末尾。 */
static __inline_ void cbq_activate_class(struct cbq_class *cl)
{
    struct cbq_sched_data *q = (struct cbq_sched_data*)cl->qdisc->data;
    int prio = cl->priority;
    struct cbq_class *cl_tail;

    cl_tail = q->active[prio];
    q->active[prio] = cl;

    if (cl_tail != NULL) {
        cl->next_alive = cl_tail->next_alive;
        cl_tail->next_alive = cl;
    } else {
        cl->next_alive = cl;
        q->activemask |= (1<<prio);
    }
```

# 图 9.157 CBQ–激活或去激活类：linux/net/sched/sch_cbq.c。

/* 从活动链中取消链接。注意此过程直接在轮询调度中执行。 */
static void cbq_deactivate_class(struct cbq_class *this)
{
    struct cbq_sched_data *q = (struct cbq_sched_data*)this->qdisc->data;
    int prio = cl->priority;
    struct cbq_class *cl;
    struct cbq_class *cl_prev = q->active[prio];

    do {
        cl = cl_prev->next_alive;
        if (cl == this) {
            cl_prev->next_alive = cl->next_alive;
            cl->next_alive = NULL;

            if (cl == q->active[prio]) {
                q->active[prio] = NULL;
                q->activemask &= ~(1<<prio);
                return;
            }
            }
            cl = cl_prev->next_alive;
            return;
        }
    } while (cl_prev != q->active[prio]);
}

# 标记类

# 图 9.158 CBQ–标记顶层：linux/net/sched/sch_cbq.c。

```c
static void cbq_mark_toplevel(struct cbq_sched_data *q, struct cbq_class *cl)
{
    int tolevel = q->toplevel;
    if (toplevel && cl->level && (cl->flags&TC_F_HTTLED)) {
        psched_time_t now;
        psched_diff_t incr;

        PSCHED_GET_TIME(now);
        incr = PSCHED_DIFF_ADD(now, q->rt);
        PSCHED_DIFF_ADD(q->now, incr, now);

        do {
            if (PSCHED_LESS(cl->underflow, now)) {
                q->toplevel = cl->level;
                return;
            }
        } while ((cl->borrow) != NULL && tolevel > cl->level);
    }
}
```

# CBQ 操作

# 图 9.159 CBQ–入队：linux/net/sched/sch_cbq.c。

```c
static int cbq_enqueue(struct sk_buff *skb, struct qdisc *sch)
{
    struct cbq_sched_data *q = (struct cbq_sched_data *)sch->data;
    struct cbq_class *cl = cbq_classify(skb, sch);
    int len = skb->len;
    int ret = -NET_XEMIT_POLICE;

#ifndef CONFIG_NET_CLS_POLICE
```

# TCP/IP 和 Linux 协议实现

```c
q->rx_class = cl;
#endif
if (cl) {
    #ifdef CONFIG_NET_CLS_POLICE
      cl->q->__parent = sch;
    #endif
    if ((ret = cl->q->enqueue(skb, cl->q)) == 0) {
      sch->q.qlen++;
      sch->stats.packets++;
      sch->stats.bytes+=len;
      cbq_mark_toplevel(q, cl);
      if (cl->next_alive) {
        cbq_activate_class(cl);
        return 0;
      }
    }
    sch->stats.drops++;
    if (cl == NULL) {
      free_skb(skb);
    } else {
      cbq_mark_toplevel(q, cl);
      cl->stats.drops++;
    }
    return ret;
}
```

# 图 9.160 CBQ–重新队列：linux/net/sched/sch_cbq.c。

```c
static int cbq_requeue(struct sk_buff *skb, struct *disc, struct *sch)
{
    struct cbq_sched_data *q = (struct cbq_sched_data *)sch->data;
    struct cbq_class *cl;
    int ret;

    if ((cl = q->tx_class) == NULL) {
      free_skb(skb);
      sch->stats.drops++;
      return RET_EMIT_CN;
    }
    q->tx_class = NULL;

    cbq_mark_toplevel(q, cl);
    #ifdef CONFIG_NET_CLS_POLICE
      q->rx_class = cl;
      cl->q->__parent = sch;
    #endif
  #endif
  if ((ret = cl->q->ops->requeue(skb, cl->q)) == 0) {
    sch->q.qlen++;
    if (cl->next_alive) {
      cbq_activate_class(cl);
      return 0;
    }
  }
  sch->stats.drops++;
  if (cl == NULL) {
    free_skb(skb);
  } else {
    cbq_mark_toplevel(q, cl);
    cl->stats.drops++;
  }
  return ret;
}
```

