```
if (len < 0) {
  len = 0;
}
return len;
}
```

# ## 6.5.6 Starting IPMR Multicast

Figure 6.246—initial multicast routing: linux/net/ipv4/ipmr.c.

```
#ifndef CONFIG_IP_PIMSM_V2
struct inet_protocol pim_protocol = {
  pim_rcv,            /* PIM handler */
  NULL,               /* PIM error control */
  NULL,               /* next */
  IPPROTO_PIM,       /* protocol ID */
  0,                  /* copy */
  NULL,               /* data */
  "PIM",             /* name */
};
n#endif

/*
 * Setup for IP multicast routing
 */
void __init_ip_mr_init(void) {
  printk(KERN_INFO "Linux IP multicast router 0.06 plus PIM-SM\n");
  mrt_cache = kmem_cache_create("ip_mr_cache",
                                sizeof(struct mfc_cache),
                                0, SLAB_HWCACHE_ALIGN,
                                NULL, NULL);
  init_timer(&ipmr_expire_timer);
  ipmr_expire_timer.function=ipmr_expire_process;
  register_netdevice_notifier(&ip_mr_notifier);
  #ifdef CONFIG_PROF_PIM
  proc_net_create("ip_mr_vif",ipmr_vif_info);
  proc_net_create("ip_mr_cache",0,ipmr_mfc_info);
#endif
```

# ## 6.6 NATs, Tunnels, and Other Hacks

These three (NAT, IP in IP, and GRE) are very similar—the multicast tunnel support is quite homomorphic, too. Network address translation is covered in more detail in Chapter 10.