```
/*
fib_disable_ip(ifa->ifa->dev, 1);
} else {
    fib_del_ifaddr(ifa);
    rt_cache_flush(-1);
    break;
}
return NOTIFY_DONE;
*/
```

# Figure 8.27 FIB front end event handler: linux/ipv4/fib_frontend.c.

```
static int fib_netdev_event(struct notifier_block *this, unsigned long event, void *ptr)
{
    struct net_dev *dev = ptr;
    struct in_dev *in_dev = __in_dev_get(dev);
    if (!in_dev)
        return NOTIFY_DONE;
    switch (event) {
        case NETDEV_UP:
            for_ifa(in_dev) {
                fib_add_ifaddr(ifa);
                endfor_ifa(in_dev);
            }
            #ifdef CONFIG_IP_ROUTE_MULTIPATH
                fib_sync_up(dev);
            #endif
            rt_cache_flush(-1);
            break;
        case NETDEV_DOWN:
            fib_disable_ip(dev, 0);
            break;
        case NETDEV_UNREGISTERED:
            fib_disable_ip(dev, 1);
            break;
        case NETDEV_CHANGEMU:
        case NETDEV_CHANGE:
            rt_cache_flush(0);
            break;
    }
    return NOTIFY_DONE;
}
```