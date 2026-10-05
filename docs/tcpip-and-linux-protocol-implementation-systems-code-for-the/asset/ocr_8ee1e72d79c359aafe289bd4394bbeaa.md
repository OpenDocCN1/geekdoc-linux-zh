# 126 TCP/IP and Linux Protocol Implementation

```
321 struct Qdisc
322 unsigned long tx_queue_len; /* Max frames per queue allowed */
323
324 /* hard_start_xmit synchronizer */
325 spinlock_t      xmit_lock;
326     /* cpu id of processor entered to hard_start_xmit or -1,
327     if nobody entered there.
328     /* */
329 int                       xmit_lock_owner;
330     /* device lock * */
331 spinlock_t               queue_lock;
332     /* Number of references to this device */
333 atomic_t                 refcnt;
334     /* The flag marking this device is unregistered, but held by a user */
335 int                       deadbeef;
336
337     /* Net device features * */
338 int                       features;
339 #define NETIF_F_SG         32      /* Scatter/gather IO. */
340 #define NETIF_F_IP_CSUM    4      /* Can checksum only TCP/UDP over IPv4. */
341 #define NETIF_F_NO_CSUM             /* Does not require checksum. F.e. loopack. */
342 #define NETIF_F_HW_CSUM    4      /* Can checksum all packets. */
343 #define NETIF_F_DYNFALLOC  16      /* Self-destructible device. */
344 #define NETIF_F_HIGHDNA    32      /* Can DMA to high memory. */
345 #define NETIF_F_FRAGLIST   1       /* Scatter/gather IO. */
```

Figure 5.23 Network/OS device abstraction iv: linux/include/linux/netdevice.h

```
348 void                  (*unit)(struct net_device_dev);
349     /* Called after last user reference disappears. */
350 void                  (*destructor)(struct net_device_dev);
351
352     /* Pointers to interface service routines. */
353 int                   (*open)(struct net_device_dev);
354 int                   (*stop)(struct net_device_dev);
355 int                   (*hard_start_xmit)(struct sk_buff *skb);
356                       struct net_device *dev;
357 int                   (*hard_header)(struct sk_buff *skb);
358                       struct net_device *dev,
359                       unsigned short type,
360                       void *daddr,
361                       void *saddr,
362                       unsigned len;
363 int                   (*rebuild_header)(struct sk_buff *skb);
364 #define HAVE_MULTICAST
365 void
366     (*set_mult_list)(struct net_device_dev);
367 #define HAVE_SET_MAC_ADDR
368 int
369     (*set_mac_address)(struct net_device_dev);
370                       void *daddr);
371 #define HAVE_PRIVATE_IOCTL *
```