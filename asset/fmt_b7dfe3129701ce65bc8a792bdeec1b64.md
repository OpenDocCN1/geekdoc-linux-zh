
```c
static void fib_add_ifaddr(struct if_addr *ifa) {
{
    struct in_device *in_dev = &ifa->ifa_dev;
    struct net_device *dev = in_dev->dev;
    struct in_addr *prim = &ifa;
    u32 mask = &ifa->ifa_mask;
    u32 addr = &ifa->ifa_local;
    u32 prefix = &ifa->ifa_address&mask;

    if (ifa->flags&ifa_F_SECONDARY) {
        prim = inet_ifa_byprefix(in_dev, prefix, mask);
        if (prim == NULL) {
            printk(KERN_DEBUG "fib_add_ifaddr: bug: %p NULL\n", ifa);
            return;
        }
    }

    fib_magic(RTM_NEWROUTE, RTN_LOCAL, addr, 32, prim);
    if ((dev->flags&IFF_UP)) {
        return;
    }
/* 如果 ifa 被显式分配，则添加广播地址。 */
    if (ifa->broadcast && ifa->broadcast == 0xFFFFFFFF) {
        fib_magic(RTM_NEWROUTE, RTN_BROCAST, ifa->ifa_broadcast, 32, prim);
    }

    if (ZERONET(prefix) && (ifa->ifa_flags&ifa_F_SECONDARY)) {
        (prefix = addr | ifa->ifa_prefixlen < 32);
        fib_magic(RTM_NEWROUTE, dev->flags&IFF_LOOPBACK) ? RTN_LOCAL :
RTN_UNICAST, prefix, ifa->ifa_prefixlen);
    }
/* 当合理时，添加网络广播 / */
    if (ifa->ifa_prefixlen < 31) {
        fib_magic(RTM_NEWROUTE, RTN_BROCAST, prefix, 32, prim);
        fib_magic(RTM_NEWROUTE, RTN_BROCAST, prefix|mask, 32, prim);
    }
}
```

# 路由 565

# 图 8.23 按接口地址的 FIB 前端项：`linux/net/ipv4/fib-frontend.c`。

```c
static void fib_del_ifaddr(struct in_ifaddr *ifa)
{
    struct in_device *in_dev = ifa->ifa_dev;
    struct net_device *dev = in_dev->dev;
    struct in_ifaddr *ifa;
    struct in_ifaddr *prim = ifa;
    u32 brd = ifa->ifa_address&ifa_mask;
    u32 any = ifa->ifa_address&ifa_mask;
    #define LOCAL_OK 1
    #define BRD_OK 2
    #define BRDO_OK 4
    #define BRIG_OK 8
    unsigned int ok = 0;

    if ((ifa->ifa_flags&IFF_FLAG_SECONDARY) != IFF_LOOPBACK)
        fib_magic(RTM_DELROUTE, RTN_UNICAST,
              RTN_UNICAST, any, ifa->ifa_prefixlen, prim);
    else {
        prim = ifa_ifa_byprefix(in_dev, any, ifa->ifa_mask);
        if (prim == NULL) {
            printk(KERN_DEBUG "fib_del_ifaddr: bug: prim NULL\n");
            return;
        }
    }

    /* 删除比添加更复杂。
       我们应该扫描地址列表以确保地址已删除。 */
    for (ifa = in_dev->ifa_list; ifa; ifa = ifa->ifa_next) {
        if (ifa->ifa_local == ifa->ifa_local) {
            ok = LOCAL_OK;
            if (ifa->ifa_broadcast == ifa->ifa_broadcast) {
                ok = BRD_OK;
                if (brd == ifa->ifa_broadcast) {
                    ok = BRD_OK;
                }
                if (any == ifa->ifa_broadcast) {
                    ok = BRD_OK;
                }
            }
        }
    }

    if (!(ok&BRD_OK)) {
        fib_magic(RTM_DELROUTE, RTN_BROCAST, ifa->ifa_broadcast, 32, prim);
        if (!(ok&BRD_OK)) {
            fib_magic(RTM_DELROUTE, RTN_BROCAST, brd, 32, prim);
        }
        if (!(ok&BRD_OK)) {
            fib_magic(RTM_DELROUTE, RTN_BROCAST, any, 32, prim);
        }
        if (!(ok&LOCAL_OK)) {
            fib_magic(RTM_DELROUTE, RTN_LOCAL, ifa->ifa_local, 32, prim);

            /* 最终发现了本地地址。 */
            if (inet_addr(ifa->ifa_local) != RTN_LOCAL) {
                /* 这是最后的但不是最重要的。
                   我们必须刷新 FIB 条目。
                   首先，我们扫描 fib_info 列表查找
                   条目，然后启动 fib_flush。 */
                if (fib_sync_down(ifa->ifa_local, NULL, 0)) {
                    fib_flush();
                }
            }
        }
    }
    #undef LOCAL_OK
    #undef BRD_OK
    #undef BRDO_OK
    #undef BRIG_OK
```

# 图 8.24 按接口地址的 FIB 前端：`linux/net/ipv4/fib-frontend.c`。

# 事件处理器

# 图 8.25 FIB 前端处理器：`linux/net/ipv4/fib-frontend.c`。

```c
static void fib_disable_ip(struct net_device *dev, int force)
{
    if (fib_sync_down(0, dev, force)) {
        fib_flush();
        rt_cache_flush(0);
        arp_ifdown(dev);
    }
}
```

# 图 8.26 FIB 前端处理器：`linux/net/ipv4/fib-frontend.c`。

```c
static int fib_inet_event(struct notifier_block *this, unsigned long event, void *ptr)
{
    struct in_ifaddr *ifa = (struct in_ifaddr*)ptr;
    switch (event) {
        case NETDEV_UP:
```
