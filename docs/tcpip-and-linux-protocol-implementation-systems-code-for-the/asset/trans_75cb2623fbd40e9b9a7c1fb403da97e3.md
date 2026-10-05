

## 5.6.2 从全局池中分配和释放套接缓冲区

图 5.126 从池到池的套接缓冲区头部：linux/net/core/skbuff.c

```
113 static __inline__ struct skb_head *skb_head_from_pool(void)
114 {
115     struct skb_buff_list *list = skb_head_from_pool[smp_processor_id()].list;
116
117     if (skb_queue_len(list)) {
118         struct skb_buff *skb;
119         unsigned long flags;
120
121         local_irq_save(flags);
122         skb = __skb_dequeue(list);
123         local_irq_restore(flags);
124         return skb;
125     }
126     return NULL;
127 }
129 static __inline__ void skb_head_to_pool(struct skb_buff *skb)
130 {
131     struct skb_buff_list *list = __skb_head_pool[smp_processor_id()].list;
132
133     if (skb_queue_len(list) < sysctl_hot_list_len) {
134         unsigned long flags;
135
136         local_irq_save(flags);
137         __skb_queue_head(list, skb);
138         local_irq_restore(flags);
139
140         return;
141     }
142     kmem_cache_free(skb_head_cache, skb);
143 }
```

以下节自 skbuff 代码的片段详细描述了套接缓冲区的分配过程。

图 5.127 分配套接缓冲区--注释：linux/net/core/skbuff.c。

```
152 /**
153  * alloc_skb - 分配网络缓冲区
154  *  @size: 分配的大小
155  *  @gfp_mask: 分配掩码
156
157  * 分配一个新的 skb_buff。返回的缓冲区没有头部空间（headroom），且
158  * 尾部空间（tail room）大小为字节。该对象的引用计数为 1。
159  * 返回该缓冲区。如果失败，则返回 NULL。
```

# TCP/IP 与 Linux 协议实现

```
* 缓冲区只能通过使用 XGFP_ATOMIC 的 @gfp_mask 
* 在中断上下文中进行分配；
*/
```

分配套接缓冲区的代码调用了底层内核函数来实际分配正确类型的内存。

## 5.128 分配套接缓冲区：linux/net/core/skbuff.c。

```
struct sk_buff *alloc_skb(unsigned int size, int gfp_mask)
{
    struct sk_buff *skb;
    u8 *data;

    if (in_interrupt() && (gfp_mask & __GFP_WAIT)) {
        static int count = 0;
        if (++count < 5) {
            printk(KERN_ERR "alloc_skb called nonatomically\n"
                   "  from interrupt %p\n", __CALLER(size));
            BUG();
        }
    }
    gfp_mask &= __GFP_WAIT;

    /* 获取头部 */
    skb = skb_head_from_pool();
    if (skb == NULL) {
        skb = kmem_cache_alloc(skbuff_head_cache, cache, gfp_mask);
        if (skb == NULL)
            goto nodata;
    }

    /* 获取数据。大小必须与 skb_add_mtu() 匹配。*/
    size = (size + 15) & ~15;
    data = kmalloc(size + sizeof(atomic_t), gfp_mask);
    if (data == NULL)
        goto nodata;

    /* XXX: 不包含 slab 开销 */
    skb->truesize = size + sizeof(struct sk_buff);

    /* 加载数据指针。 */
    skb->head = data;
    skb->tail = data;
    skb->end = data + size;

    /* 设置其他状态 */
```

# 协议实现框架 191

```
204 skb->len = 0;
205 skb->cloned = 0;

207 atomic_set(skb->users, 1);
208 atomic_set(skb->datarefp(skb), 1);
209 return skb;

211 nodata:
212 skb_head_to_pool(skb);
213 nobead
214 return NULL;
215 }
```

图 5.129 初始化套接缓冲区：linux/net/core/skbuff.c。

```
218 /*
219 * skb 头部的 Slab 构造函数。
220 */
221 static inline void skb_headinit(void *skb, kmem_cache_t *cache,
222 unsigned long flags)
223 {
224 struct skb_buff *skb = p;
225 skb->next = NULL;
226 skb->prev = NULL;
227 skb->list = NULL;
228 skb->skb = NULL;
229 skb->stamp.tv_sec=0; /* 时间信息 */
230 skb->dev = NULL;
231 skb->dst = NULL;
232 memset(skb->cb, 0, sizeof(skb->cb)); /* 默认类型 */
233 skb->pkt_type = PACKET_HOST; /* 默认类型 */
234 skb->sum = 0;
235 skb->priority = 0;
236 skb->security = 0; /* 数据是不安全的 */
237 skb->destructor = NULL;
238
239 #ifdef CONFIG_NETFILTER
240 skb->nfmark = skb->cache = 0;
241 skb->nfct = NULL;
242 #ifdef CONFIG_NETFILTER_DEBUG
243 skb->nf_debug = 0;
244 #endif
245 #endif
246 #ifdef CONFIG_NET_SCHED
247 skb->tc_index = 0;
248 #endif
249 }
```

# TCP/IP 与 Linux 协议实现

图 5.130 释放套接缓冲区：linux/net/core/skbuff.c。

```
/*
 * 在不清理状态的情况下释放 skbuff。
 */
void kfree_skmem(struct skb_buff *skb)
{
    if (!skb->cloned || atomic_dec_and_test(skb->datarefp(skb)))
        kfree(skb->head);

    skb_head_to_pool(skb);
}
```

## 5.6.3 操作缓冲区

图 5.131 克隆套接缓冲区：linux/net/core/skbuff.c。

```
/**
 * skb_clone - 复制 skb_buff
 * @skb: 需要复制的缓冲区
 * @gfp_mask: 分配优先级
 *
 * 复制一个 skb_clone。新的缓冲区不属于任何套接字。
 * 两者共享相同的包数据但不共享结构。新的
 * 引用计数为 1。如果分配失败，则返回 NULL，否则返回新缓冲区。
 * 如果从中断中调用此函数，gfp_mask 必须为
 * GFP_ATOMIC。
 */
struct sk_buff *skb_clone(struct skb_buff *skb, int gfp_mask)
{
    struct skb_buff *n;

    n = skb_head_from_pool(skb);
    if (!n) {
        n = kmem_cache_alloc(skbuff_head_cache, gfp_mask);
        if (!n)
            return NULL;
    }

    memcpy(n, skb, sizeof(*n));
    atomic_inc(skb->datarefp(skb));
    skb->cloned = 1;

    dst_dst(n->dst);
    n->cloned = 1;
    n->next = n->prev = NULL;
    n->list = NULL;
    n->zk = NULL;
    atomic_set(&n->users, 1);
```

```
330 n->destructor = NULL;
331 #ifdef CONFIG_NETFILTER
332 nf_conntrack_get(skb->nfct);
333 #endif
334 return n;
335 }
```

以下函数复制格式但不复制内容，并增加引用计数。

图 5.132 套接缓冲区结构头部：linux/net/core/skbuff.c。

```
337 static void copy_skb_header(struct sk_buff *new, const struct sk_buff *old)
{
339 /*
340  * 数据区域之间的偏移（字节）
 */
342 unsigned long offset = new->data - old->data;
344 new->list=NULL;
345 new->sk=NULL;
346 new->dev=old->dev;
347 new->priority=old->priority;
348 new->protocol=old->protocol;
349 new->dst=dst_clone(old->dst);
350 new->h.raw=old->h.raw+offset;
351 new->nh.raw=old->nh.raw+offset;
352 new->mac.raw=old->mac.raw+offset;
353 memory(new->cb, old->cb, sizeof(old->cb));
354 new->used=old->used;
355 atomic_set(&new->users, 1);
356 new->pkt_type=old->pkt_type;
357 new->stamp=old->stamp;
358 new->destructor = NULL;
359 new->security=old->security;
360 #ifdef CONFIG_NETFILTER
361 new->ifmark=old->ifmark;
362 new->nfcache=old->nfcache;
363 new->nfct=old->nfct;
364 nf_conntrack_get(new->nfct);
365 #ifdef CONFIG_NETFILTER_DEBUG
366 new->nf_debug=old->nf_debug;
367 #endif
368 #endif
369 #ifdef CONFIG_NET_SCHED
370 new->tc_index=old->tc_index;
371 #endif
372 }
```

这里是操作套接缓冲区代码的全局数据部分。

图 5.133 复制套接缓冲区结构和数据：linux/net/core/skbuff。

```
/**
 * skb_copy_expand - 复制并扩展 skb_buff
 * @skb: 需要复制的缓冲区
 * @Gheadroom:头部新的自由空间
 * @newtailroom: 尾部新的自由空间
 * @gfp_mask: 分配优先级
 *
 * 在此的同时复制一个 skb_buff 及其数据
 */
```

