# Infrastructure Protocols 343

```
712      in_dev = inetdev_by_index(iml->multi.imr_ifindex);
713      if (in_dev) {
714          ip_mc_dec_group(in_dev, imr->imr_multiiaddr.s_addr);
715          in_dev_put(in_dev);
716      }
717      rtnl_unlock();
718      sock_kfree_s(sk, iml, sizeof(*iml));
719      return 0;
720
721  }
722  rtnl_unlock();
723  return -EADDRNOTAVAIL;
724  }
```

Figure 6.191 IGMP-socket closing: linux/net/ipv4/igmp.c.

```
730 void ip_mc_drop_socket(struct sock *sk)
731 {
732      struct ip_mc_socklist *iml;
733
734      if (sk->protoinfo.af_inet.mc_list == NULL)
735          return;
736
737      rtnl_lock();
738      while (iml->dev->protoinfo.af_inet.mc_list != NULL) {
739          struct in_device *in_dev;
740          sk->protoinfo.af_inet.mc_list = iml->next;
741
742          if ((in_dev = inetdev_by_index(iml->multi.imr_ifindex)) != NULL) {
743              ip_mc_dec_group(in_dev, iml->multi.imr_multiaddr.s_addr);
744              in_dev_put(in_dev);
745          }
746          sock_kfree_s(sk, iml, sizeof(*iml));
747      }
748
749      rtnl_unlock();
750 }
```

# Device Events that Influence Group State

Figure 6.192 IGMP-device goes down or comes up: linux/net/ipv4/igmp.c.

```
554 void ip_mc_down(struct in_device *in_dev)
555 {
556      struct ip_mc_list *iml;
557
558      ASSERT_RTNL();
559
560      for (i=in_dev->mc_list; i; i=i->next)
```