
### neigh_parms 结构

除了 `neigh_table` 之外，还有一个包含操作邻居表缓存项参数的结构。这些参数与 sysctl（系统控制）机制配合使用，如果 Linux 内核配置了 sysctl。因此，邻居表缓存中的项可以被添加或删除。与其他数据结构一起，邻居缓存系统的邻居参数结构 `neigh_parms` 定义在 `include/net/neighbour.c` 中。

每个邻居缓存项都有关联的 `neigh_parms`。

```c
struct neigh_parms {
    struct neighbour *next;
    int (*setup)(struct neighbour);
    struct neigh_table *tbl;
    int dead;
    atomic_t refcnt;
    struct rcu_head rcu_head;
    unsigned long used;
    unsigned long confirmed;
    unsigned long updated;
    __u8 flags;
    int gc_interval;
    int gc_thresh1;
    int gc_thresh2;
    int gc_thresh3;
    unsigned long last_flush;
    struct timer_list gc_timer;
    struct timer_list proxy_timer;
    struct sk_buff_head proxy_queue;
    int entries;
    rwlock_t lock;
    unsigned long last_rand;
    kmem_cache_t *kmem_cache;
    struct neigh_statistics stats;
};
```

到目前为止，我们还没有讨论邻居缓存项和邻居参数结构。现在我们将查看邻居缓存项本身。每个邻居表由邻居缓存项的哈希表组成。

每个邻居缓存项被 `neighbour` 结构包含。

```c
struct neighbour {
```

# 第 5 章 Linux TCP/IP 栈

`output` 指向在硬件头部解析后传输数据包的函数。它被初始化为 `neigh_blackhole`，当邻居缓存条目首次创建但尚未完全运行时，数据包将被丢弃。

```c
int (*output)(struct sk_buff *sk);
```

如果此邻居缓存条目用于 ARP 协议，则 `arp_queue` 就是等待地址解析完成的数据包队列。使用队列比强制所有数据包等待更好，因为在等待 ARP 响应时，它不会占用输出设备。`ops` 是一个用于该邻居缓存条目的特定协议的函数列表。

```c
struct sk_buff_head arp_queue;
struct timer_list timer;
struct neighbor_ops *ops;
u8 primary_key[0];
};
```

# 邻居系统初始化

邻居系统支持多次实例化；没有静态数据结构。这是因为每个协议族都应该有自己独立的邻居表。例如，IPv4。`AF_INET` 地址族包含了 ARP，即地址解析协议 [RFC 826]。ARP 在初始化时会初始化一个邻居表实例。在查看了通用邻居表初始化函数后，我们专门查看 ARP 在创建邻居表时做了什么。

## neighbor_table_init 函数

ARP 和其他解析协议调用创建邻居表的函数是 `neighbor_table_init`。该函数定义在 `linux/net/core/neighbor.c` 中。

```c
void neighbor_table_init(struct neighbor_table *tbl) {
```

现在是当前时间。邻居发现协议需要以随机间隔发送消息。为了实现这一点，`neighbor_parms` 结构中的 `reachable_time` 被设置为根据种子值 `base_reachable_time` 计算出的随机值。

```c
unsigned long now = jiffies;
unsigned long phsize;
atomic_set(&tbl->parms.refcnt, 1);

INIT_RCU_HEAD(&parms.rcu_head);
tbl->parms.reachable_time = neigh_rand_reach_time(tbl->parms->base_reachable_time);
```

我们创建了一个 slab 缓存条目，邻居表条目将从该条目中创建。

```c
if (tbl->kmem_cache == NULL)
    tbl->kmem_cache = kmem_cache_create(tbl->id,
                                        (tbl->entry_size+15)&-15,
                                        0, SLAB_HWCACHE_ALIGN,
                                        NULL, NULL);
if (!tbl->kmem_cache)
    panic("cannot create neighbour cache");

tbl->stats = alloc_percpu(struct neigh_statistics);
if (!tbl->stats)
    panic("cannot create neighbour cache statistics");

#ifndef CONFIG_PROC_FS
    tbl->pde = create_proc_entry(tbl->id, 0, proc_net_stat);
    if (!tbl->pde)
        panic("cannot create neighbour proc entry");
    tbl->pde->proc_fops = &neigh_stat_seq_fops;
    tbl->pde->data = tbl;
#endif

tbl->hash_mask = 1;
tbl->hash_buckets = neigh_hash_alloc(tbl->hash_mask + 1);
size = (PNEIGH_HASHMASK + 1) * sizeof(struct pneigh_entry *);
tbl->hash_buckets = kmalloc(phsize, GFP_KERNEL);
if (!tbl->hash_buckets)
    panic("cannot allocate neighbour cache hashes");
memset(tbl->hash_buckets, 0, phsize);

get_random_bytes(&tbl->hash_rnd, sizeof(tbl->hash_rnd));
rwlock_init(&tbl->lock);
```

接下来，初始化垃圾回收。`neigh_periodic_timer` 从一个随机值重新计算可达性。该函数为执行垃圾回收函数提供了上下文。

```c
init_timer(&tbl->gc_timer);
tbl->gc_timer.data = (unsigned long)tbl;
tbl->gc_timer.function = neigh_periodic_timer;
tbl->gc_timer.expires = now + tbl->gc_interval + tbl->parms.reachable_time;
add_timer(&tbl->gc_timer);
```

代理定时器用于代理缓存。

```c
init_timer(&tbl->proxy_timer);
tbl->proxy_timer.data = (unsigned long)tbl;
tbl->proxy_timer.function = neigh_proxy_process;
skb_queue_head_init(&tbl->proxy_queue);

tbl->last_flush = now;
tbl->last_rand = now + tbl->parms.reachable_time*2;
write_lock(&neigh_lock);
```

此邻居表实例被放置在邻居的链表中。

```c
tbl->next = neighbor_tables;
neigh_tables = tbl;
unlock(&neigh_lock);
```
