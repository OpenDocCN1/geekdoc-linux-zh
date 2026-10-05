

```c
1179 psched_us_per_tick = 1000000;
1180 #ifdef PSCHED_WATCHER
1181 psched_tick(0);
1182 #endif
1183 #endif

1185 #ifdef CONFIG_RTNETLINK
1186 link_p = rtnetlink_links[PF_UNSPEC];

1188 /* rtnetlink links. It is made here to avoid
1189 exporting large number of public symbols.
1190 */

1192 if (link_p) {
1193 link_p[RTM_DEQDISC-RTM_BASE].do = tc_modify_qdisc;
1194 link_p[RTM_DELTDISC-RTM_BASE].do = tc_get_qdisc;
1195 link_p[RTM_GETQDISC-RTM_BASE].do = tc_get_qdisc;
1196 link_p[RTM_GETQDISC-RTM_BASE].dump = tc_dump_qdisc;
1197 link_p[RTM_NEWTCLASS-RTM_BASE].do = tc_ctl_tclass;
1198 link_p[RTM_DELTDCLASS-RTM_BASE].do = tc_ctl_tclass;
1199 link_p[RTM_GETTCLASS-RTM_BASE].do = tc_ctl_tclass;
1200 link_p[RTM_GETTCLASS-RTM_BASE].dump = tc_dump_tclass;
1201 }
```

# 图 9.121 调度器 API–数据包调度初始化：linux/net/sched/sched.api.

```c
#define INIT_QDIS(name) {\\
    extern struct qdisc_ops name##__qdisc_ops; \
    register_qdisc(&name##__qdisc_ops); \\
}

INIT_QDIS(pfifo);
INIT_QDIS(bfifo);
```

# 图 9.122 调度器 API–数据包调度初始化：linux/net/sched/sched.api.

```c
#ifdef CONFIG_NET_SCH_CBQ
INIT_QDIS(cbq);
#endif
#ifdef CONFIG_NET_SCH_CSZ
INIT_QDIS(csz);
#endif
#ifdef CONFIG_NET_SCH_HPFQ
INIT_QDIS(hpfq);
#endif
#ifdef CONFIG_NET_SCH_HFSC
INIT_QDIS(hfsc);
```

# 744 TCP/IP 和 Linux 协议实现

```c
1223 #endif
#ifdef CONFIG_NET_SCH_RED
1225 INIT_QDISC(red);
1226 #endif
#ifdef CONFIG_NET_SCH_GRED
1228 INIT_QDISC(gred);
1229 #endif
#ifdef CONFIG_NET_SCH_INGRESS
1231 INIT_QDISC(ingress);
1232 #endif
#ifdef CONFIG_NET_SCH_DSMARK
1234 INIT_QDISC(dmark);
1235 #endif
#ifdef CONFIG_NET_SCH_SFQ
1237 INIT_QDISC(sfq);
1238 #endif
#ifdef CONFIG_NET_SCH_TBF
1240 INIT_QDISC(tbf);
1241 #endif
#ifdef CONFIG_NET_SCH_TEQL
1243 teql_init();
1244 #endif
#ifdef CONFIG_NET_SCH_PRIO
1246 INIT_QDISC(prio);
1247 #endif
#ifdef CONFIG_NET_SCH_ATM
1249 INIT_QDISC(atm);
1250 #endif
#ifdef CONFIG_NET_SCH_CLS
1252 tc_filter_init();
1253 #endif

#ifdef CONFIG_PROC_FS
1256 create_proc_read_entry("net/psched", 0, 0, psched_read_proc, NULL);
1257 #endif
```

# 9.11.2 调度器框架

9.123 数据包调度接口-QDisc 遍历定义：linux/include/net/pkt.sched.h.

```c
20
21 struct qdisc_walker
22 {
23     int stop;
24     int skip;
25     int count;
26     int (*fn)(struct qdisc *, unsigned long cl, struct qdisc_walker *);
27 };
```

# 图 9.124 数据包调度接口–QDisc 类操作：linux/include/net/pkt-sched.h.

```c
struct Qdisc_class_ops
(
    /* Qdisc qdisc 操作 */
    int (*graft)(struct Qdisc *, unsigned long cl, struct Qdisc *, struct
               Qdisc **);
    struct Qdisc *(*leaf)(struct Qdisc *, unsigned long cl);

    /* 类操作例程 */
    unsigned long (*get)(struct Qdisc *, u32 classid);
    void (*put)(struct Qdisc *, unsigned long);
    int (*change)(struct Qdisc *, u32, u32, struct rtattr **, unsigned long);

    int (*delete)(struct Qdisc *, unsigned long);
    void (*walk)(struct Qdisc *, struct qdisc_walker *arg);

    /* 过滤器操作 */
    struct tcf_proto **(*tcf_chain)(struct Qdisc *, unsigned long);
    unsigned long (*bind)(struct Qdisc *, unsigned long, u32 classid);
    void (*unbind)(struct Qdisc *, unsigned long);

    *rtnetlink_function
    int (*dump)(struct Qdisc *, unsigned long, struct sk_buff *skb, struct
               tmsg);
# 图 9.125 调度器接口–QDisc 操作：linux/include/net/pkt-sched.h.

```c
struct qdisc_class_ops(
    struct qdisc_ops *next;
    struct qdisc_class_ops *cl_ops;
    char id[IFNAMSIZ];
    int priv_size;
    int
    int (*enqueue)(struct sk_buff *, struct qdisc);
    int (*dequeue)(struct qdisc);
    int (*requeue)(struct sk_buff *, struct qdisc);
    int (*drop)(struct qdisc *);

    int (*init)(struct qdisc *, struct rtattr *arg);
    void (*reset)(struct qdisc);
    void (*destroy)(struct qdisc);
    int (*change)(struct qdisc *, struct rtattr *arg);

    int (*dump)(struct qdisc *, struct sk_buff *arg);

# 746 TCP/IP 和 Linux 协议实现
# 图 9.126 调度器接口–QDisc 结构：linux/include/net/pkt.sched.h.

```c
struct qdisc
{
    int
    struct sk_buff *(enqueue)(struct sk_buff *, struct qdisc *dev);
    unsigned *(dequeue)(struct qdisc *dev);
    unsigned int flags;
    #define TCQ_F_BUILTIN 1
    #define TCQ_F_HTTLED 2
    #define TCQ_F_INGRESS 4
    struct qdisc_ops *ops;
    struct qdisc *next;
    u32 handle;
    atomic_t refcnt;
    struct sk_buff_head q;
    struct net_device *dev;

    struct tc_stats *stats;
    int *(reshape_fail)(struct sk_buff *skb, struct qdisc *q);

    /* 该字段已废用，但 CBQ 仍在使用，
     * 直到更好的解决方案出现 */
    struct qdisc *parent;
    char data[0];
};
# 图 9.127 调度器接口–QDisc 操作：linux/include/net/pkt.sched.h.

```c
struct qdisc_rate_table
{
    struct tc_respec rate;
    u32 data[256];
    struct qdisc_rate_table *next;
    int refcnt;
};

static inline void sch_tree_lock(struct qdisc *qdisc)
{
    write_lock(&qdisc_tree_lock);
    spin_lock_bh(qdisc->dev->queue_lock);
}

static inline void sch_tree_unlock(struct qdisc *qdisc)
{
    spin_unlock_bh(qdisc->dev->queue_lock);
    write_unlock(&qdisc_tree_lock);
}

static inline void tcf_tree_lock(struct tcf_proto *tp)
{
    write_lock(&qdisc_tree_lock);
    spin_lock_bh(tp->q->dev->unlock);
}

static inline void tcf_tree_unlock(struct tcf_proto *tp)
{
    spin_unlock_bh(tp->q->dev->queue_lock);
    write_unlock(&qdisc_tree_lock);
}

static inline unsigned long cls_set_class(struct tcf_proto *tp, unsigned long *clp, unsigned long cl)
{
    unsigned long old_cl;
    tcf_tree_lock(tp);
    old_cl = *clp;
    *clp = cl;
    tcf_tree_unlock(tp);
    return old_cl;
}

static inline unsigned long cls_set_class(unsigned long *clp, unsigned long cl)
{
    unsigned long old_cl;
    old_cl = *clp;
    *clp = cl;
    return old_cl;
}
```

# 图 9.128 调度器接口--时钟注释：linux/include/net/pkt_sched.h.

```c
/*
    定时器分辨率必须 小于 最小可调度数据包大小/带宽的 10%
    普通 IP 数据包大小为 512 字节，因此：
    0.5KB/Msec = 5ms，所以我们对 10Mbit 以太网使用 5usec 定时器。
    10nsec -> <50Kbit/sec。

结果：不是 QoS 路由器的良好选择：情况并没有那么糟糕，因为我们可以在最关键的地方通过对网络数据流进行积分来评估人工时钟。```

# 748 TCP/IP 和 Linux 协议实现

注意：我们不使用 gettimeofday。
原因是，当它与 gettimeofday 不一致时，它会返回无效的时间戳，且在 net_hb 激活时该戳不会更新。

因此，在 alpha 和带有 rtsc 的 pentium 处理器上使用 PSCHED_CLOCK_SOURCE = PSCHED_CPU。在其他架构上使用 PSCHED_JIFFIES。

```c
/*
 * 关于内部时钟的通用说明
 */
```

任何时钟源返回的时间间隔单位接近微秒。使用 PSCHED_GETTIMOFDAY 源时为微秒，否则为了最小化计算开销而选择其他。以分子/分母形式的使用/内部单位比例可以通过 /proc/net/sched 读取。

# 图 9.129 调度器 API：linux/net/sched/sch_api.c.

```c
#ifdef CONFIG_RTNETLINK
static int qdisc_notify(struct sk_buff *oskb, struct nlmsghdr *n, u32 clid,
	struct qdisc *old, struct qdisc *new);
static int tclass_notify(struct sk_buff *buff, struct nlmsghdr *n,
	struct qdisc *q, unsigned long cl, int event);
#endif
```

# 图 9.130 调度器 API–讨论：linux/net/sched/sch_api.c.

```c
/*
短期回顾。

该文件包含两个相互关联的部分：

+   1. 队列规则管理器前端。
2. 流量类管理器前端。

通常，队列规则（qdisc）是一个黑盒，它能够顺序入队数据包，并在设备准备好发送时按照隐藏算法规定的时间出队。

qdisc 被分为两类：

+   - “队列”，从外部看不到其内部结构。
- “调度器”，将所有数据包分发到“流量类”。
```

