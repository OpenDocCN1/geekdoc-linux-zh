

# 转发 851

285

286
restart:

287
nores = 0;

288
busy = 
if ((q = start) == NULL)
    goto drop;
```

# 图 9.305 TE 网络设备传输 ii: linux/net/sched/sch_teql.c.

```c
do {
    struct net_device *slave = q->dev;

    if (slave->q_sleeping == q)
        continue;
    if (netif_queue_stopped(slave) || !netif_running(slave)) {
        busy = 1;
        continue;
    }

    switch (teql_resolve(&slave, skb, res, slave)) {
        case 0:
            if (spin_trylock(&slave->xmit_lock)) {
                slave->xmit_lock_owner = smp_processor_id();
                if (netif_queue_stopped(slave)) &&
                    slave->hard_start_xmit(skb, slave) == 0) {
                    slave->xmit_lock_owner = -1;
                    spin_unlock(&slave->xmit_lock);
                    master->slaves = NEXT_SLAVE(q);
                    netif_wake_queue(dev);
                    master->stats.tx_packets++;
                    master->stats.tx_bytes += len;
                    return 0;
                }

                slave->xmit_lock_owner = -1;
                spin_unlock(&slave->xmit_lock);
            }

            if (netif_queue_stopped(dev))
                busy = 1;
            break;
        case 1:
            master->slaves = NEXT_SLAVE(q);
            return 0;

        default:
            nores = 1;
            break;
    }

    _skb_pull(skb, skb->nh.raw - skb->data);
} 
while ((q = NEXT_SLAVE(q)) != start);
```

# 852 TCP/IP 和 Linux 协议实现

图 9.306 TE 网络设备传输 iii: linux/net/sched/sch_teql.c.

```c
if (nores && skb_res == NULL) {
    skb_res = skb;
    goto restart;
}
if (busy) {
    netif_stop_queue(dev);
    return 1;
}
master->stats.tx_errors++;

drop:
    master->stats.tx.dropped++;
    dev_kfree_skb(skb);
    return 0;
}
```

图 9.307 TE 网络设备打开: linux/net/sched/sch_teql.c.

```c
static int teql_master_open(struct net_device *dev) {
    struct Qdisc *q = ; 
    struct teql_master *m = (void*)dev->priv;
    int mtu = 0xFFFF;
    unsigned flags = IFF_NOARP|IFF_MULTICAST;

    if (m->slave == NULL) {
        return -EUNATCH;
    }
    flags = FMASK;
    q = q->slave;
    do {
        struct net_device *slave = q->dev;
        if (slave == NULL) {
            return -EUNATCH;
        }

        if (slave->mtu < mtu) {
            mtu = slave->mtu;
        }
        if (slave->hard_header_len > LL_MAX_HEADER) {
            return -EINVAL;
        }
        /* 如果所有的从设备都是广播型，主设备就是广播型
           如果所有的从设备都是点对点，主设备就是点对点
           否则，主设备是多点链路 (NBMA) */
        if ((slave->flags&IFF_INTOPOINT)) {
            flags &= ~IFF_INTOPOINT;
        }
        if ((slave->flags&IFF_BROADCAST)) {
            flags &= ~IFF_BROADCAST;

# 转发 853

```c
if ((slave->flags&IFF_MULTICAST))
    flags &= ~IFF_MULTICAST;
} while ((q = NEXT_SLAVE(q)) != m->slaves)
m->dev->mtu = mtu;
m->dev->flags = (m->dev->flags&~MASK) | flags;
netif_start_queue(qm->dev);
MOD_INC_USE_COUNT;
return 0;

# 图 9.308 TE 网络设备关闭和统计: linux/net/sched/sch_teql.c.

```c
static int teql_master_close(struct net_dev *dev)
{
  netif_stop_queue(dev);
  MOD_DEC_USE_COUNT;
  return 0;
}
static struct net_dev_stats *teql_master_stats(struct net_dev *dev)
{
  struct teql_master *m = (void*)dev->priv;
  return m->stats;
}
```

# 图 9.309 TE 网络设备 mtu: linux/net/sched/sch_teql.c.

```c
static int teql_master_mtu(struct net_dev *dev, int new_mtu)
{
  struct teql_master *m = (void*)dev->priv;
  struct Qdisc *q;
  if (new_mtu < 6)
    return -EINVAL;
  q = m->slaves;
  if (q) {
    do {
      if (new_mtu > q->dev->mtu)
        return -EINVAL;
    } while ((q=NEXT_SLAVE(q)) != m->slaves);
  }
  dev->mtu = new_mtu;
  return 0;
}
```

# TCP/IP 和 Linux 协议实现

图 9.310 TE 网络设备初始化: linux/net/sched/sch_teql.c.

```c
426 static int teql_master_init(struct net_device *dev)
427 {
428 dev->open               = teql_master_open;
429 dev->hard_start_xmit = teql_master_xmit;
430 dev->stop              = teql_master_close;
431 dev->get_stats         = teql_master_stats;
432 dev->change_mtu        = teql_master_mtu;
433 dev->type             = ARPHRD;
434 dev->mtu              = 1500;
435 dev->tx_queue_len     = 100;
436 dev->flags            = IFF_NOARP;
437 dev->hard_header_len = LL_MAX_HEADER;
438 return 0;
}
441 static struct teql_master the_master = {
442 {
443 NULL,
444 NULL,
447 sizeof(struct teql_sched_data),
448 teql_enqueue,
449 teql_dequeue,
450 teql_requeue,
451 NULL,
453 teql_qdisc_init,
454 teql_reset,
455 teql_destroy,
456 NULL,
457 };
```

# 图 9.311 TE 网络设备注册: linux/net/sched/sch_teql.c.

```c
459 #ifdef MODULE
460 int init_module(void)
461 #else
462 int __init teql_init(void)
464 #endif
465 {
467 int err;
468 rnl_lock();
470 the_master.dev.priv = (void*)&the_master;
471 err = dev_alloc_name(&the_master.dev, "teql%d");
473 if (err < 0)
474 return err;
475 memcpy(the_master.qops.id, the_master.dev.name, IFNAMSIZ);
```

```c
the_master.dev.init = teql_master_init;
err = register_netdevice(&the_master.dev);
if (err == 0) {
    err = register_qdisc(&the_master.qops);
    unregister_netdevice(&the_master.dev);
}
rtnl_unlock();
return err;
```

```c
#ifdef MODULE
void cleanup_module(void) {
    rtnl_lock();
    unregister_qdisc(&the_master.qops);
    unregister_netdevice(&the_master.dev);
    rtnl_unlock();
}
#endif
```

# 9.13.14 性能分析

图 9.312 性能计时器: linux/net/core/profile.c.

```c
atomic_t net_profile_active;
struct timeval net_profile_adjust;
NET_PROFILE_DEFINE(total);
struct net_profile_slot *net_profile_chain = &net_total;
#ifdef __alpha
    __u32 alpha;
    long alpha;
static void alpha_tick(unsigned long);
static struct timer_list alpha_timer =
    {NULL, 0, alpha_timer};
void alpha_tick(unsigned long dummy) {
    struct timeval dummy_stamp;
    net_profile_stamp(&dummy_stamp);
    alpha_timer.expires = jiffies + 4HZ;
    add_timer(&alpha_timer);
}
#endif
```

# 图 9.314 性能分析接口: linux/net/core/profile.c.

```c
142 struct iphdr whitehole_iph;
143 int whitehole_count;

145 static int whitehole_xmit(struct skb_buff *skb, struct net_device *dev)
146 {
147 struct net_device_stats *stats;

149 stats = (struct net_device_stats *)dev->priv;
150 stats->tx_packets++;
151 stats->tx_bytes+=skb->len;

153 dev_kfree_skb(skb);
154 return 0;
155 }
```

```c
166 static int whitehole_open(struct net_device *dev)
167 {
168 whitehole_count = 100000;
169 whitehole_timer.expires = jiffies + 5HZ;
170 add_timer(&whitehole_timer);
171 return 0;
}

174 static int whitehole_close(struct net_device *dev)
175 {
176 del_timer(&whitehole_timer);
177 return 0;
}
```

