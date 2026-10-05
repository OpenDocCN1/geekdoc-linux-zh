```
/*
 * Initialize sock SLAB cache.
 */
skk_init();

#ifdef SLAB_SKB
/*
 * Initialize skbuff SLAB cache
 */
ksb_init();
#endif

/*
 * Wan router layer.
 */
#ifdef CONFIG_WAN_ROUTER
wanrouter_init();
#endif
```

Then the socket VFS module itself may be installed or removed at run time, too, as needed.

# Figure 5.116 Socket glue–initializing the socket VFS module: linux/net/socket.c.

```
/*
 * Initialize the protocols module.
 */
register_filesystem(&sock_fs_type);
sock_mt = kernel_mount(&sock_fs_type);
/* The real protocol initialization is performed when
 * do_initcall is run.
 */
/*
 * The netlink device handler may be needed early.
 */
#ifdef CONFIG_RTNETLINK
rtnetlink_init();
#endif
#ifdef CONFIG_NETLINK_DEV
init_netlink();
#endif
#ifdef CONFIG_NETFILTER
netfilter_init();
#endif}
```