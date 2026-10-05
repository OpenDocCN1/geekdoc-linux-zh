

# 920 TCP/IP 与 Linux 协议实现

```
q->qave 是一个在 Wlog 带有小数点的定点数。
上述公式等于浮点数
版本：
qave = qave*(i-W) + sch->stats.backlog*W;
               --ANK (908924)
            */
}
```

图 9.257 RED-enqueue iii: linux/net/sched/sch_red.c。

```
if (q->qave < q->qth_min) {
    q->qcount = -1;
enqueue:
if (sch->stats.backlog <= q->limit) {
    skb_queue_tail(sch->q, skb);
    sch->stats.backlog += skb->len;
    sch->stats.bytes += skb->len;
    sch->stats.packets++;
    return NET_EMIT_SUCCESS;
} else {
    q->st.dropp++;
    kfree_sk(skb);
    sch->stats.drops++;
    return NET_EMIT_DROP;
}
} if (q->qave >= q->qth_max) {
    q->qcount = -1;
    sch->stats.overlimits++;
mark:
if (q->flags&FC_RED_ECN) || !red_scm_mark(skb)) {
    q->st.early++;
    goto drop;
}
q->st.marked++;
goto enqueue;
n
```

这是我们如何将随机性映射到队列位置。

图 9.258 RED-enqueue i: linux/net/sched/sch_red.c。

```
if (++q->qcount) {
    /* 下面使用的公式引起了问题。
OK. qr 是 O.Rmask 范围内的随机数。
is.s. 0..(Plog)。如果我们使用浮点
运算，它将是：(2^Plog)*rnd_num，
其中 rnd_num 小于 1。
```

# 转发 821

考虑到 qave 在 Wlog 带有小数点，且 Plog 与 max_P 关：
max_P = (qth_max_qth_min)/2;Plog; 以下两行
具有以下浮点等效于：

```
max_P*(qth_min/qth_max_qth_min) < rnd/count
```

有任何问题？--ANK (880924)
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
drop:
	skfree_skb(skb);
sch->stats.drop++;
return NET_XMIT_CN;
}
```

图 9.259 RED–requeue and dequeue: linux/net/sched/sched_red.c。

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
		sch->stats.backlog -= skb->len;
		return skb;
	}
	PSCHED_GET_TIME(q->qidlestart)
	return NULL;
}
```

# 822 TCP/IP 与 Linux 协议实现

# 图 9.260 RED–drop: linux/net/sched/sch_red.c。

```
static int
red_drop(struct qdisc *skb)
{
    struct sk_buff *skb;
    struct red_sched_data *q = (struct red_sched_data *)skb->data;
    skb = NULL; __skb_dequeue_tail(skb->q);
    if (skb) {
        skb->stats.backlog -= skb->len;
        skb->stats.drops++;
        q->stat.other++;
        kfree(skb);
        return 1;
    }
    PSCHED_GET_TIME(q->qidlestart);
    return 0;
}
```

# 图 9.261 RED–reset: linux/net/sched/sch_red.c。

```
static void red_reset(struct qdisc *sch)
{
    struct red_sched_data *q = (struct red_sched_data *)skb;
    struct sk_buff *skb;

    while ((skb = skb_dequeue(sch->q)) != NULL) {
        kfree(skb);
        sch->stats.backlog = 0;
        PSCHED_GET_PASTERFECT(q->qidlestart);
        q->qave = 0;
        q->count = -1;
    }
}
```

# 图 9.262 RED–change: linux/net/sched/sch_red.c。

```
atomic int red_change(struct qdisc *sch, struct rtattr *opt)
{
    struct red_sched_data *q = (struct red_sched_data *)opt->data;
    struct rtattr *tb = tb[TCA_RED_PARMS];
    struct tc_qdisc *ctl;
    if (parse(tb, TCA_RED_PARMS, RTA_DATA(opt), RTA_PAYLOAD(opt)) == NULL ||
        tb[TCA_RED_PARMS] == 0 || tb[TCA_RED_PARMS] == 0 ||
        RTA_PAYLOAD(tb[TCA_RED_PARMS]) < sizeof(ctl) ||
        RTA_PAYLOAD(tb[TCA_RED_PARMS]) < 256)
        return -EINVAL;
    ctl = RTA_DATA(tb[TCA_RED_PARMS]);
    sch_tree_lock(sch);

```
q->flags = ctl->flags;
q->Wlog = ctl->Wlog;
q->Plog = ctl->Plog;
q->Rmask = ctl->Plog < 32 ? (1<<ctl->Plog) - 1 : 0;
q->Scell = ctl->Scell;
q->Scell_max = (255<<q->Scell);
q->qth_min = ctl->qth_min<<ctl->Wlog;
q->qth_max = ctl->qth_max<<ctl->Wlog;
q->limit = ctl->limit;
q->count = -1;
    PSCHED_SET_PASTERFECT(q->qidlestart);
    sch_tree_unlock(sch);
return 0;
}
```

图 9.263 RED-init: linux/net/sched/sch_red.c。

```
static int red_init(struct qdisc *sch, struct rtattr *opt)
{
    int err;
    MOD_INC_USE_COUNT;
    if ((err = red_change(sch, opt)) != 0) {
        MOD_DEC_USE_COUNT;
    }
    return err;
}
```

# 913.6 GRED

GRED 是 RED 的通用版本，包含了针对不符合 TCP 的位惩罚（RED in/out）。它与 RED 在结构上相似，因此我们不进行详细讨论。

# 913.7 令牌桶 (Token Bucket)

令牌桶在前面的章节中描述过。

# 824 TCP/IP 与 Linux 协议实现

数据流满足速率 R 和深度 B 的 TBF，如果对于对于任何时间间隔 $t$，传输的比特数未超过 $B + R*(t-t_i)$。

该定义的包化版本：在 $t_i$ 服务的大小为 $s_i$ 的数据包满足 TBF，如果对于 $i<k$：
$s_i+...+s_k \le B + R*(k-t_i)$。

算法。

让 $N(t_i)$ 最初为 $B/R$，N(t)$ 随时间连续增长：
$N(t+\delta) = \min(B/R, N(t) + \delta)$

如果队列中的第一个包长度为 $S$，它只有在时间 $t^*$ 可以传输：当 $S/R \le N(t^*)$ 时，在这种情况下 $N(t_*) = N(t_*) - S/R$。

实际上，QoS 需要应用两个 TBF。其中一个控制稳定突发大小，另一个速率为 $P$（峰值速率）深度为 $M$（等于链路 MTU），在较小的时间尺度上限制突发。

很容易看出 $P=R, B=M$。如果 $P$ 为无限，则 TBF 等于单个。

当 TBF 在重塑模式工作时，延迟估计为：
$lat = \max ((L-B)/R, (L-M)/P)$

这意味着对于深度为 $B$，最大速率是
$R_{crit} = B*HZ$
例如，对于 10Mbit 以太网和 $HZ=100$，最小允许的 $B$ 是 10KB。注意峰值速率 TBF 要严格得多；当 MTU 为 1500 时
$P_{crit} = 150KB/sec$。因此，如果你需要更大的峰值速率，请使用 $HZ=1000$ :-)

# 图 9.266 令牌桶过滤器队列--linux/net/sched/sched_tbf.c。

```
struct tbf_sched_data {
    /* 参数 */
    u32 limit; /* 最大队列长度：字节 */
    u32 buffer; /* 令牌桶深度/速率：MTU/B */
    u32 mtu;
    u32 max_size;
    struct qdisc_rate_table *R_tab;
    struct qdisc_rate_table *P_tab;

    /* 变量 */ /* 当前 B 令牌数量 */
    long tokens; /* 当前 P 令牌数量 */
    long ptokens; /* 时间检查点 */
    psched_time_t t_c; /* 门狗定时器 */
    struct timer_list wd_timer; /* 门狗定时器 */
};

#define LGT(q,L) ((q)->R_tab->data(L))((q)->R_tab)->rate.cell_log))
#define LPT(q,L) ((q)->P_tab->data(L))((q)->P_tab)->rate.cell_log))
```

# 图 9.267 TBF-enqueue:linux/net/sched/sched_tbf.c。

```
static int
tbf_enqueue(struct sk_buff *skb, struct qdisc *disc)
{
    struct tbf_sched_data *q = (struct tbf_sched_data *)skb->data;

    if (skb->len > q->max_size)
        goto drop;
    skb_queue_tail((skb->sch)->q, skb);
    if ((skb->backlog += skb->len) <= q->limit)
        skb->stats.bytes += skb->len;
    skb->stats.packets++;
    return 0;
}
```

