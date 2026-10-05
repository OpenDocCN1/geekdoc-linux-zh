# Routing 565

**Figure 8.23** FIB front-end entry by interface address i: linux/net/ipv4/fib-
frontend.c.

```
503  static void fib_del_ifaddr(struct in_ifaddr *ifa)
504  {
505      struct in_device *in_dev = ifa->ifa_dev;
506      struct net_device *dev = in_dev->dev;
507      struct in_ifaddr *ifa1;
508      struct in_ifaddr *prim = ifa;
509      u32 brd = ifa->ifa_address&ifa->ifa_mask;
510      u32 any = ifa->ifa_address&ifa->ifa_mask;
511      #define LOCAL_OK 1
512      #define BRD_OK 2
513      #define BRDO_OK 4
514      #define BRIG_OK 8
515      unsigned int ok = 0;
516
517
518      if ((ifa->ifa_flags&IFF_FLAG_SECONDARY) != IFF_LOOPBACK) :
519          fib_magic(RTM_DELOUTE, RTN_UNICAST, 
520              RTN_UNICAST, any, ifa->ifa_prefixen, prim);
521      else {
522          prim = ifal_ifa_byprefix(in_dev, any, ifa->ifa_mask);
523          if (prim == NULL) {
524              printk(KERN_DEBUG "fib_del_ifaddr: bug: prim == NULL\n\n525              return;
526          }
527      }
528
529      /* Deletion is more complicated than add.
530       We should take care of not to delete too much :-
531
532       Scan addresses list to be sure that addresses are really gone.
533      */
534      for (ifal = in_dev->ifa_list; ifal; ifal = ifal->ifa_next) {
535          if (ifa->ifa_local == ifa->ifa_local) {
536              ok = LOCAL_OK;
537          if (ifa->ifa_broadcast == ifa->ifa_broadcast) {
538              ok = BRD_OK;
539              if (brd == ifa->ifa_broadcast) {
540                  ok = BRD_OK;
541          if (any == ifa->ifa_broadcast) {
542              ok = BRD_OK;
543          }
544      }
```

**Figure 8.24** FIB front-end entry by interface address ii: linux/net/ipv4/fib-
frontend.c.

```
545  if (!(ok&BRD_OK)) {
546      fib_magic(RTM_DELROUTE, RTN_BROADCAST, ifa->ifa_broadcast, 32, prim);
547  if (!(ok&BRD_OK)) {
548      fib_magic(RTM_DELROUTE, RTN_BROADCAST, brd, 32, prim);
549  if (!(ok&BRD_OK)) {
550      fib_magic(RTM_DELROUTE, RTN_BROADCAST, any, 32, prim);
551  if (!(ok&LOCAL_OK)) {
```