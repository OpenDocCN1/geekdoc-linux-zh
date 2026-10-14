
# TCP/IP 和 Linux 协议实现

```c
206             case TC_POLICE_SHOT:

207                 kfree_skb(skb);

208                 break;

209         #if 0

210             case TC_POLICE_RECLASSIFY:

211                 /* FIXME: 这里应该做什么 **/
212         #endif

213     #endif

214     case TC_POLICE_OK;
```

```c
215 skb->tc_index = TC_H_MIN(res->classid);
216 break;
217 case TC_POLICE_UNSPEC:
218     /* 穿透 */
219 default:
220     if (p->default_index)
221         skb->tc_index = p->default_index;
222         break;
223     }
224 if (
225     #ifdef CONFIG_NET_CLS_POLICE
226         result = TC_POLICE_SHOT
227 #endif
228 
229 ((ret = p->q->enqueue(skb,p->q)) != 0) {
230     sch->stats->drops++;
231     return 0;
232     }
233 sch->stats->bytes += skb->len;
234 sch->stats->packets++;
235 sch->q->qlen;
236 return ret;
237 }
```

![](img/06c11ba8be5c1c24aa633e1261e2ebd_865_0.png)

```c
240 static struct sk_buff *dsmark_dequeue(struct qdisc *qdisc)
241 {
242     struct dsmark_qdisc_data *p = PRIV(qdisc);
243     struct sk_buff *skb;
244     int index;
245 
246     printk("dsmark_dequeue(%p, [qdisc %p])\n", skb, p);
247     skb = p->ops->dequeue(p->q);
248     if (!skb) {
249         return NULL;
250     }
251 sch->q->qlen;
252 index = skb->tc_index & (p->indices-1);
253 printk("Index %d\n", index, skb->tc_index);
254     switch (skb->h->h_proto) {
255         case constant_htons(ETH_P_IP):
256             ipv4_change_dsfield(skb->nh->ipv4, p->max[index], p->value[index]);
257             break;
258         case constant_htons(ETH_P_IPV6):
259             ipv6_change_dsfield(skb->nh->ipv6, p->max[index], p->value[index]);
260             break;
261         default:
262             /*
263 * 只有在实际尝试更改时才报错
264 * 这样我们就可以通过 dsmark 发送非 IP 流量
265 * 且不需要另一个 qdisc 作为旁路。 */
266             if (p->mask[index] != 0xff || p->value[index])
267                 printk(KERN_WARNING "dsmark_dequeue: 不支持协议 %x\n", htons(skb->h->h_proto));
268             break;
269 }
270 return skb;
```

# 图 9.241 Marker-requeue: linux/net/sched/sch_dmark.c.

```c
static int dsmark_requeue(struct sk_buff *skb,struct qdisc *sch,
{
    int ret;
    struct dsmark_qdisc_data *p = PRIV(sch);
    printk("dsmark_requeue(%p, [qdisc %p])\n",skb,p);
    if ((ret = p->q->enqueue(skb,p->q)) != 0) {
        sch->stats->drops++;
        return ret;
    }
    sch->q->qlen++;
    return 0;
}
```

# 图 9.242 Marker-drop: linux/net/sched/sch_dmark.c.

```c
static int dsmark_drop(struct qdisc *sch)
{
    struct dsmark_qdisc_data *p = PRIV(sch);
    if (!p->ops->drop(p)) {
        return 0;
    }
    sch->q->qlen--;
}
```

# 图 9.243 Marker-init: linux/net/sched/dsmark.c.

```c
int dsmark_init(struct qdisc *sch, struct rattr *opt)
{
```

# 图 9.244 Marker-reset: linux/net/sched/dsmark.c.

```c
static void dsmark_reset(struct qdisc *sch)
{
    struct dsmark_qdisc_data *p = PRIV(sch);
    p->default_index = 0;
    p->filter_list = NULL;
}
```

# 图 9.245 Marker-destroy: linux/net/sched/sch_dmark.c.

```c
static void dsmark_destroy(struct qdisc *sch)
{
    struct dsmark_qdisc_data *p = PRIV(sch);
    struct tcf_proto *tp;
    while (p->filter_list) {
        tp = p->filter_list;
        p->filter_list = tp->next;
        kfree(tp);
    }
    qdisc_destroy(p->q);
    kfree(p->mask);
}
```

# 图 9.246 Marker-dump: linux/net/sched/sch_dmark.c.

```c
static int dsmark_dump(struct qdisc *sch, unsigned long cl, struct sk_buff *skb, struct tcm *tcm)
{
    struct dsmark_qdisc_data *p = PRIV(sch);
    unsigned char *b = skb->tail;
    struct rtattr *rta;
```

# 图 9.247 Marker-dump: linux/net/sched/sch_dmark.c.

```c
static int dsmark_dump(struct qdisc *sch, struct sk_buff *skb)
{
```

# 814 TCP/IP 与 Linux 协议实现

```c
411 rta = (struct rtattr *)b;
412 RTA_PUT(skb,TCA_OPTIONS_INDICES,NULL);
413 RTA_PUT(skb,TCA_DSMARK_INDICES,sizeof(u16),&p->indexes);
414 if (p->default_index)
415 RTA_PUT(skb,TCA_DSMARK_DEFAULT_INDEX,sizeof(u16));
```
