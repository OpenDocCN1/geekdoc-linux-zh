# Protocol Implementation Framework 127

```
370 int                 (*do_ioctl)(struct net_device *dev,
371 #define HAVE_SET_CONFIG      struct ifreq *ifr, int cmd);
372 int                 (*set_config)(struct net_device *dev,
373 #define HAVE_HEADER_CACHE    struct ifmap *map);
374 int                 (*hard_header_cache)(struct neighbour *neigh,
375 int                 struct hh_cache *hh);
376 void                (*header_cache_update)(struct hh_cache *hh,
377                      struct net_device *dev,
378                      unsigned char *baddr);
379 #define HAVE_CHANGE_MTU
380 int                 (*change_mtu)(struct net_device *dev, int new_mtu);
381 #define HAVE_TX_TIMEOUT
382 void                (*tx_timeout)(struct net_device *dev);
383 int                 (*hard_header_parse)(struct sk_buff *skb,
384                      unsigned char *baddr);
385 int                 (*neigh_setup)(struct net_device *dev, int neigh_parms);
386 int                 (*accept_fastpath)(struct net_device *dev, struct dst_entry);
387 /* open/release and using marking */
388 struct module *owner;
389 /* bridge stuff */
390 struct net_bridge_port *br_port;
```

# 5.4.2 Network Reception

This is a generic receive handle/demultiplex called from receive inter-rupts from all network device drivers.

Figure 5.24 Network device Rx: linux/net/core/dev.c.

```
1028 static void netdev_wakeup(void)
1029 {
1030     unsigned long xoff;
1031
1032     spin_lock(&netdev_fc_lock);
1033     xff = netdev_fc_xoff;
1034     netdev_fc_xoff = 0;
1035     while (xff) {
1036         int i = ffs(xff);
1037         xff &= ~(1<<i);
1038         netdev_fc_slots[i].stim(netdev_fc_slots[i].dev);
1039     }
1040     spin_unlock(&netdev_fc_lock);
1041 }
```