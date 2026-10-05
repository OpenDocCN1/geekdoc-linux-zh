
# Figure 9.289 SFQ--data structures: linux/net/sched/sch_sfq.c.

```c
#define SFQ_DEPTH             128
#define SFQ_HASH_DIVISOR    1024

/* This type should contain at least SFQ_DEPTH*2 values */
    typedef unsigned char sfq_index;

    struct sfq_head
    {
        sfq_index      next;
        sfq_index      prev;
    };

struct sfq_sched_data
{
    /* Parameters */
        int             perturb_period;
        unsigned        quantum;        /* Allotment per round: MUST BE >= MTU */
    
    /* Variables */
    struct timer_list_timer {
        int             perturbation;
        sfq_index       tail;           /* Index of current slot in round */
        sfq_index       max_depth;      /* Maximal depth */
    };
    sfq_index       ht[SFQ_HASH_DIVISOR];  /* Hash table */
    sfq_index       next[SFQ_DEPTH];    /* Active slots link */
    short           allot[SFQ_DEPTH];   /* Current allotment per slot */
    unsigned short hash[SFQ_DEPTH];    /* Hash value indexed by slots */
    struct sk_buff_head qs[SFQ_DEPTH];  /* Slot queue */
    struct sfq_head_dep dep[SFQ_DEPTH*2]; /* Linked list of slots, indexed by depth */
};
```

# TCP/IP and Linux Protocol Implementation

Figure 2.290 SFQ-queue hash functions: linux/net/sched/sch_sfq.c.

```c
static __inline__unsigned sfq_fold_hash(struct sfq_sched_data *q, u32 h, u32 hi)
{
    int port = q->perturbation;

    /* We have any rotation primitives? If not, WHY? */
    h = (hi < pert) ? (hi) > (0 - pert);
    h = h>>10;
    return h & 0x3FF;
}

#ifdef IPPROTO_ESP
#define IPPROTO_ESP 50
#endif

static unsigned sfq_hash(struct sfq_sched_data *q, struct sk_buff *skb)
{
    u32 h, h2;
    switch (skb->protocol) {
        case htons(ETH_P_IP):
        {
            struct ip_hdr *iph = skb->iph;
            h = iph->saddr;
            h2 = iph->saddr ^ iph->protocol;
            if ((iph->frag_off & IP_OFFSET) &&
                iph->protocol == IPPROTO_TCP ||
                iph->protocol == IPPROTO_UDP ||
                iph->protocol == IPPROTO_ESP)
                h2 = *((u32*)iph + iph->ihl);
            break;
        }
        case htons(ETH_P_IPV6):
        {
            struct ipv6_hdr *iph = skb->ipv6;
            h = iph->saddr[3];
            h2 = iph->saddr[3] ^ iph->next;
            if (iph->next == IPPROTO_TCP ||
                iph->next == IPPROTO_UDP ||
                iph->next == IPPROTO_ESP)
                h2 = *((u32*)iph[1]);
            break;
        }
        default:
            h = (u32)(unsigned long)skb->protocol;
            h2 = (u32)(unsigned long)skb->sk;
    }
    return sfq_hash(q, h, h2);
}
```

# Figure 9.291 SFQ-queue decrement/increment functions: linux/net/sched/sch_sfq.c.

```c
extern __inline_ void sfq_link(struct sfq_sched_data *q, sfq_index x)
{
    sfq_index p, n;
    int d = q->qs[x].qlen + SFQ_DEPTH;

    p = d;
    n = q->dep[d].next;
    q->dep[x].next = n;
    q->dep[x].prev = p;
    q->dep[p].next = q->dep[n].prev = x;
}

extern __inline_ void sfq_dec(struct sfq_sched_data *q, sfq_index x)
{
    sfq_index p, n;
    n = q->dep[x].next;
    p = q->dep[x].prev;
    q->dep[p].next = n;
    q->dep[n].prev = p;

    if (n == p && q->max_depth == q->qs[x].qlen + 1) {
        q->max_depth--;
        sfq_link(q, x);
    }
}

extern __inline_ void sfq_inc(struct sfq_sched_data *q, sfq_index x)
{
    sfq_index p, n;
    int d;

    n = q->dep[x].next;
    p = q->dep[x].prev;
    q->dep[p].next = n;
    q->dep[n].prev = p;
    d = q->qs[x].qlen;
    if (q->max_depth < d) {
        q->max_depth = d;
    }
    sfq_link(q, x);
}
```

# Figure 9.292 SFQ--dequeue function: linux/net/sched/sch_sfq.c.

```c
static int sfq_drop(struct qdisc *q)
{
    struct sfq_sched_data *sfq = (struct sfq_sched_data *)q->data;
    struct sfq_index d = q->max_depth;
    struct sk_buff *skb;

    /* Queue is full! Find the longest slot and
        drop a packet from it */

    if (d > 1) {
        sfq_index x = q->dep[d+SFQ_DEPTH].next;
        skb = q->qs[x].prev;
        skb_unlink(skb, &q->qs[x]);
        kfree_skb(skb);
        sfq_dec(q, d);
        sch->q_len--;
        sch->stats.drops++;
        return 1;
    }

    if (d == 1) {
        /* It is difficult to believe, BUT ALL SLOTS HAVE LENGTH 1. */
        d = q->next(q)->tail;
        q->next(tail) = q->next[d];
        q->allot[d] += q->quantum;
        skb = q->qs[d].prev;
        skb_unlink(skb, &q->qs[d]);
        kfree_skb(skb);
        sfq_dec(q, d);
        sch->q_len--;
        q->ht[d] = SFQ_DEPTH;
        sch->stats.drops++;
        return 1;
    }
    return 0;
}
```

# Figure 9.293 SFQ--enqueue function: linux/net/sched/sch_sfq.c.

```c
static int
sfq_enqueue(struct sk_buff *skb, struct qdisc *q)
{
    struct sfq_sched_data *sfq = (struct sfq_sched_data *)q->data;
    unsigned hash = sfq_hash(q, skb);
    sfq_index x;

    x = q->ht[hash];
    if (x == SFQ_DEPTH) {
        q->ht[hash] = x = q->dep[SFQ_DEPTH].next;
        q->hash[x] = hash;
    }
    skb_queue_tail(q->qs[x], skb);
    sfq_inc(q, x);
    if (q->qs[x].qlen == 1) { /* The flow is new */
        if (q->tail == SFQ_DEPTH) { /* It is the first flow */
            q->tail = x;
            q->next[x] = x;
            q->allot[x] = q->quantum;
        } else {
            q->next[x] = q->next[q->tail];
            q->next[q->tail] = x;
            q->tail = x;
        }
    }
    if (sch->stats.bytes < SFQ_DEPTH-1) {
        sch->stats.bytes += skb->len;
        sch->stats.packets++;
        return 0;
    }
    sfq_drop(sch);
    return NET_XMIT_CN;
}
```

# 2.194 SFQ-requeue function: linux/net/sched/sch_sfq.c.

```c
static int
sfq_requeue(struct sk_buff *skb, struct qdisc *sch)
{
    struct sfq_sched_data *q = (struct sfq_sched_data *)sch->data;
    unsigned hash = sfq_hash(q, skb);
    sfq_index x;

    x = q->ht[hash];
    if (x == SFQ_DEPTH) {
        q->ht[hash] = x = q->dep[SFQ_DEPTH].next;
        q->hash[x] = hash;
    }
    skb_queue_tail(q->qs[x], skb);
    sfq_inc(q, x);
    if (q->qs[x].qlen == 1) { /* The flow is new */
        if (q->tail == SFQ_DEPTH) { /* It is the first flow */
            q->tail = x;
            q->next[x] = x;
            q->allot[x] = q->quantum;
        } else {
            q->next[x] = q->next[q->tail];
            q->next[q->tail] = x;
            q->tail = x;
        }
    }
    if (++sch->stats.bytes < SFQ_DEPTH-1) {
        sch->stats.bytes += skb->len;
        sch->stats.packets++;
        return 0;
    }
    sfq_drop(sch);
    return NET_XMIT_CN;
}
```

# 844 TCP/IP and Linux Protocol Implementation

# Fig. 2.95 SFQ-dequeue function: linux/net/sched/sch_sfq.c.

```c
static struct sk_buff *
sfq_dequeue(struct qdisc *sch)
{
    struct sfq_sched_data *q = (struct sfq_sched_data *)sch->data;
    struct sk_buff *skb;
    sfq_index a, old_a;

    /* No active slots */
    if (q->tail == SFQ_DEPTH) {
        return NULL;
    }
    a = old_a = q->next(q->tail];
}
```
