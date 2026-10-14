
销毁由 `init` 和 `qdisc` 生命周期期间分配的资源。

---change

更改 `qdisc` 参数。

# 通用调度器

这是一个通用的调度器示例，旨在帮助澄清 API。

**图 9.134** 通用调度器–队列调度策略锁注释：`linux/net/sched/sch.generic.c`。

```c

/*

* 符合 GPL 2 许可证，或（根据您的选择）任何后续版本。

* 作者: Alexey Kuznetsov, <kuznet@ms2.inr.ac.ru>

* Jamil Hadi Salim, <hadis@nertelnetworks.com> 990601

* 入口支持

 */

```

```c

#include <asm/access.h>

#include <asm/system.h>

#include <asm/bitop.h>

#include <linux/config.h>

#include <linux/types.h>

#include <linux/kernel.h>

#include <linux/sched.h>

#include <linux/string.h>

#include <linux/mm.h>

#include <linux/socket.h>

#include <linux/sockio.h>

#include <linux/in.h>

#include <linux/errno.h>

#include <linux/interrupt.h>

#include <linux/netdevice.h>

#include <linux/skbuff.h>

#include <linux/rtnetlink.h>

#include <linux/init.h>

#include <net/sock.h>

#include <net/pkt_sched.h>

/* 主传输队列。 */

/* 主 qdisc 结构锁。 */

```
然而，对数据的修改必须额外由 `dev->queue_lock` 保护。

思路是：
- `enqueue`, `dequeue` 通过顶层设备自旋锁 `dev->queue_lock` 序列。
- 树遍历受 `read_lock(qdisc_tree_lock)` 保护。
- 树的更新仅在信号量下进行，因此此锁可能在关闭本地中断的情况下使用。

`qdisc_tree_lock` 必须在 `dev->queue_lock` **之前** 获取！

```c

/*

lock_t qdisc_tree_lock = RW_LOCK_UNLOCKED;

dev->queue_lock 序列化对设备和 qdisc 指针的访问。

dev->xmit_lock 序列化对设备的访问。

dev->queue_lock 和 dev->xmit_lock 是互斥的，如果一个被获取，另一个必须释放。 */

**图 9.135** 通用调度器：`linux/net/sched/sch_generic.c`。

```c
/* 设备触发。
此程序由定时器调用，以便我们检查 dev->tbusy 标志。

返回：0 - 队列为空。
0 - 队列不为空，已节流。
如果 dev->tbusy != 0。

注意：在本地禁用 dev->queue_lock 时调用。 */

# 图 9.136 通用调度器 i：`linux/net/sched/sch_generic.c`。

```c

int qdisc_restart(struct net_device *dev)

{

    struct qdisc *q = dev->qdisc;

    struct sk_buff *skb;

    /* 出队包 */

    if ((skb = q->dequeue(q)) != NULL) {

        if (spin_try_lock(&dev->xmit_lock)) {

            /* 记住驱动被我们获取 */

            dev->xmit_owner = processor_id();

            /* 释放队列 */

            spin_unlock(&dev->queue_lock);

            if (netif_queue_stopped(dev)) {

                dev_queue_xmit(skb, dev);

                if (dev->hard_start_xmit(skb, dev) == 0) {

                    dev->xmit_owner = -1;

                    spin_unlock(&dev->xmit_lock);

                }

            }

        }

    }

    /* 释放驱动 */

    dev->xmit_owner = -1;

    spin_unlock(&dev->xmit_lock);

    spin_lock(&dev->queue_lock);

    q = dev->qdisc;

} else {

    /* 所以，有人获取了驱动。

    /* 当 hard_start_xmit() 递归时，我们通过检查 xmit owner 并检测到丢弃了包。 */

    if (dev->xmit_owner == processor_id()) {

        dev_kfree_skb(skb);

        if (!ratelimit())

            printk(KERN_DEBUG, "Dead loop on netdevice %s, fix it!", dev->name);

        return -1;

    }

    dev->xmit_stat[processor_id]++;

# 图 9.137 通用调度器 ii：`linux/net/sched/sch_generic.c`。

```c
/* 设备踢：
这种情况发生在三种情况下：
0. 驱动锁定
1. 启用了快速路由
2. 传输开始前无法确定忙状态（例如超时）
3. 设备有 Bug（ppp） */
q->ops->requeue(skb, q);
netif_schedule(dev)
return 1;

# 图 9.138 通用调度器--定时狗定时器：`linux/net/sched/sch_generic.c`。

```c

static void dev_watchdog(unsigned long arg)

{

    struct net_device *dev = (struct net_device*)arg;

    spin_lock(&dev->xmit_lock);

    if (dev->qdisc != NULL_qdisc) {

        if (netif_dev_present(dev) &&

        netif_running(dev) &&

        netif_carrier_ok(dev)) {

            if (netif_queue_stopped(dev) > dev->watchdog_timeout) {

                if (jiffies - dev->hard_start_xmit(dev) > dev->watchdog_timeout)

                    printk(KERN_INFO "NETDEV WATCHDOG: %s: timed out\n", dev->name);

                    dev_tx_timeout(dev);

            }

        }

        if (!mod_timer(dev->watchdog_timer, jiffies + dev->watchdog_timeout))

            dev_hold(dev);

    }

    spin_unlock(&dev->xmit_lock);

    dev_put(dev);

}

static void dev_watchdog_init(struct net_device *dev)

{

    init_timer(dev->watchdog_timer);

    dev->watchdog_timer.data = (unsigned long)dev;

    dev->watchdog_timer.function = dev_watchdog;

}

void __netdev_watchdog_up(struct net_device *dev)

{

    if (dev->xmit_timeout) {

        if (dev->watchdog_timeout <= 0)
