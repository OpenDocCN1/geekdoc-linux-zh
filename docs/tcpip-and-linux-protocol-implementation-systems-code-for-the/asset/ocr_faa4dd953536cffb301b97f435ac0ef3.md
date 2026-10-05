```
the_master.dev.init = teql_master_init;
err = register_netdevice(&the_master.dev);
if (err == 0) {
    err = register_qdisc(&the_master.qops);
    unregister_netdevice(&the_master.dev);
}
rtnl_unlock();
return err;
```

```
#ifdef MODULE
void cleanup_module(void) {
    rtnl_lock();
    unregister_qdisc(&the_master_qops);
    unregister_netdevice(&the_master.dev);
    rtnl_unlock();
}
#endif
```

# 9.13.14 Profiling

Figure 9.312 Profiling-timer: linux/net/core/profile.c.

```
atomic_t net_profile_active;
struct timeval net_profile_adjust;
NET_PROFILE_DEFINE(total);
struct net_profile_slot *net_profile_chain = &net_prof_total;
#ifdef __alpha__
    __u32 alpha_lo;
    long alpha_bi;
static void alpha_tick(unsigned long);
static struct timer_list alpha_timer =
    {NULL, NULL, O, Ol, alpha_timer};
void alpha_tick(unsigned long dummy) {
    struct timeval dummy_stamp;
    net_profile_stamp(&dummy_stamp);
    alpha_timer.expires = jiffies + 4*HZ;
    add_timer(&alpha_timer);
}
#endif
```