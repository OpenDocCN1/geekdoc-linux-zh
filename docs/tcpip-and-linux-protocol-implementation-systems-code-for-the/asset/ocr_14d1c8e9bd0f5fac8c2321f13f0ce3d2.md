# Infrastructure Protocols 315

```
333 /*
334 *
335 * The ICMP socket. is the most convenient way to flow control
336 * our ICMP output as well as maintain a clean interface throughout
337 * all layers. All Socketless ICMP Pends will be gone.
338 */
339
340 struct inode icmp_inode;
341 struct socket *icmp_socket=&icmp_inode.u.socket_i;
342
343 /* ICMPv4 socket is only a bit non-reentrant (unlike ICMPv6,
344 * which is strongly non-reentrant). A bit later it will be made
345 reentrant and the lock may be removed.
346 */
347 static int icmp_xmit_holder = -i;
```

Figure 6.151 ICMP-transmit locks: linux/net/ipv4/icmp.c.

```
350 static int icmp_xmit_lock_bb(void)
351 {
352     if (spin_trylock(&icmp_socket->sk->lock)) {
353         if (icmp_xmit_holder == smp_processor_id())\n354             return -EAGAIN;
355         spin_lock(&icmp_socket->sk->lock);
356     }
357     icmp_xmit_holder = smp_processor_id();
358     return 0;
359 }
360
361 static inline_ int icmp_xmit_lock_bb(void)
362 {
363     int ret;
364     local_bb_disable();
365     ret = icmp_xmit_lock_bb();
366     if (ret)
367         local_bb_enable();
368     return ret;
369 }
370
371 static void icmp_xmit_unlock_bb(void)
372 {
373     icmp_xmit_holder = -1;
374     spin_unlock(&icmp_socket->sk->lock);
375 }
376
377 static inline_ void icmp_xmit_unlock(void)
378 {
379     icmp_xmit_unlock_bb();
380     local_bb_enable();
381 }
```