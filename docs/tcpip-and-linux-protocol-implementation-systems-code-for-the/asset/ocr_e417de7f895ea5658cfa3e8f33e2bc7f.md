# 132 TCP/IP and Linux Protocol Implementation

Figure 5.30 Ethernet driver 2--init d: linux/drivers/net/3c501.c.

```
364 lp=dev->priv;
365 spin_lock_init(&lp->lock);
366
367 /*
368      *
369      The ELI-specific entries in the device structure.
370  */
371
372 dev->=open = &el_open;
373 dev->=hard_start_xmit = &el_start_xmit;
374 dev->=tx_timeout = &el_timeout;
375 dev->=watchdog_time = HZ;
376 dev->=stop = &el_close;
377 dev->=get_stats = &el_get_stats;
378 dev->=set_multicast_list = &set_multicast_list;
379
380 /*
381      *
382      Setup the generic properties
383  */
384
385 ether_setup(dev);
386
387 return 0;
388 }
```

# 3c501 Start Transmission

DMA network devices have quite a lot of autonomy (i.e., they can get on with quite a lot of work in parallel with the processor(s)). Sometimes, though, they can be quite slow about some phases, so it is common practice to separate out the work, and as few (and short) critical regions as possible.

Figure 5.31 Ethernet driver 2--txstart a: linux/drivers/net/3c501.c.

```
451 /*
452  * el_start_xmit;
453  * @dev: The packet that is queued to be sent
454  * @dev: The 3c501 card we want to throw it down
455  */
456  * Attempt to send a packet to a 3c501 card. There are some interesting
457  * catches here because the 3c501 is an extremely old and therefore
```