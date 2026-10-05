

# 300 TCP/IP 与 Linux 协议实现

```c
734 if (n)
735     neigh_release(n);
736     if (skb->stamp_tv_sec == 0 ||
737         skb->pkt_type == PACKET_HOST ||
738         in_dev->arp_parms->proxy_delay == 0) {
739             arp_send(ARPOP_REPLY,ETH_P_ARP,sip,dip,tip,sha,dev->addr,
740                 sha);

741     } else {
742         neigh_enqueue(arp_tbl, in_dev->arp_parms, skb);
743             in_dev_put(in_dev);
744             return 0;
745         }
746         goto out;
747     }
748 }
749 } {
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_355_0.png)

```c
751 /* 更新我们的 ARP 表 */
752 n = __neigh_lookup(arp_tbl, zip, dip, 0);

754 #ifdef CONF_IP_ACCEPT_UNSOLICATED_ARP
755 /* 默认不接受未请求的 ARP 响应。
756 某些设备可能需要启用此选项（strip 是一个候选设备）
758 */
759 if (n == NULL &&
760     arp->ar_op == __constant_htons(ARPOP_REPLY) &&
761     inet_addr_type(sip) == RTN_UNICAST)
762         n = __neigh_lookup(arp_tbl, zip, dip, -1);

764 #endif

766 if (n) {
767     int state = NUD_REACHABLE;
768     override = 0;

770 /* 如果连续收到多个不同的 ARP 回复，
771 使用第一个。当有多个代理
772 代理活跃时，这是可能的。获取第一个回复可以防止
773 ARP 抖动并选择最快的路由器。
774 */
775 if (jiffies - n->updated >= n->parms->locktime)
776     override = 1;

778 /* 广播回复和请求包
779 不断言邻居的可达性。
780 */
781 if ((arp->ar_op == __constant_htons(ARPOP_REPLY)) &&
782     skb->pkt_type == PACKET_HOST) {
```

```c
783         state = NUD_STALE;
784         neigh_update(n, sha, state, override, 1);
785         neigh_release(n);
786  }

788  out:
789      kfree_skb(skb);
790      if (in_dev)
791                 in_dev_put(in_dev);
792  out_of_mem:
793         return 0;
794 }
```

## ARP 用户接口

**图 6.129** ARP--用户接口 (proc, ioctl)—创建一个缓存条目：linux/net/ip4/arp.c。

```c
799 /*
800  * 用户级接口 (ioctl, /proc)
801 */

802  /*
803   * 设置（创建）一个 ARP 缓存条目。
804   */

806 int arp_req_set(struct arpreq *r, struct net_device *dev)
807 {
808     u32 ip = ((struct sockaddr_in *) &r->arp_pa)->sin_addr.s_addr.addr;
809     struct neighbour *neigh;
810     int err;

812     if (r->arp_flags & ATF_PUB) { ((struct sockaddr_in *) &r->arp_netmask)->sin_addr.s_addr;
813         u32 mask = mask & 0xFFFFFFFF;

815             return -EINVAL;
816         if (!dev && !(r->arp_flags & ATF_COM)) {
817             dev = dev_get_hwaddr(r->arp_ha.sa_family, r->arp_ha.sa_data);
818             if (dev)

820                 return -ENODEV;
821     }
822     if (mask) {
823             if (neigh_lookup(karp_tbl, ip, dev, 1) == NULL)
824                 return -ENOMBUFS;
825     }
826     if (dev == NULL) {
827             ipv4_devconf.proxy_arp = 1;
828             return 0;
829     }
830     if (!in_dev_get(dev)) {
```

# 302 TCP/IP 与 Linux 协议实现

```c
831      __in_dev_get(dev)->cnf.proxy_arp = 1;
832      return 0;
833  }
834      return -ENXIO;
835  }
```

图 6.130 ARP 用户接口 (proc, ioctl)—创建一个缓存条目：linux/net/ipv4/arp.c。

```c
837      if (r->arp_flags & ATF_PERM)
838          r->arp_flags |= ATF_COM;
839      if (dev == NULL) {
840          struct rtable *rt = rt;
841              if ((err = ip_route_output(rt, ip, 0, RTO_ONLINK)) != 0)
842              return err;
843          dev = rt->u.dev;
844          ip_rt_put(rt);
845          if (!dev)
846              return -EINVAL;
847      }
848      if (r->arp_ha.sa_family != dev->type)
849          return -EINVAL;

850
neigh = neigh_lookup(arp_tbl, ip, dev);
851  err = PTR_ERR(neigh);
852  if (!IS_ERR(neigh)) {
853      unsigned int state = NUD_STALE;
854      if (r->arp_flags & ATF_PERM)
855          state = NUD_PERENT;
856  err = neigh_update(neigh, (r->arp_flags & ATF_COM) ?
857          r->arp_ha.sa_data : NULL, state, 1, 0);

859
neigh_release(neigh);
861  }
862  return err;
863 }
```

图 6.131 ARP—用户接口—更改 ARP 标志：linux/net/ipv/arp.c。

```c
864  static unsigned arp_state_to_flags(struct neighbour *neigh)
865  {
866      unsigned int flags = 0;
867      if (neigh->nud_state == NUD_PERENT)
868          flags = ATF_PERM | ATF_COM;
869      else if (neigh->nud_state == NUD_VALID)
870          flags = ATF_COM;
871      return flags;
872  }
```

图 6.132 ARP—接口—获取 ARP 条目：linux/net/ipv4/arp.c。

```c
878 static int arp_req_get(struct arpreq *r, struct net_device *dev)
879  {
880     u32 ip = ((struct sockaddr_in *)&r->arp_pa)->sin_addr.s_addr;
881     struct neighbour *neigh;
882     int err = -ENXIO;

884          neigh = neigh_lookup(arp_tbl, ip, dev);
885     if (!IS_ERR(neigh)) {
886         read_lock(&neigh);
887         memcpy(r->arp_ha.sa_data, neigh->dev, dev_len);
888         r->arp_flags = arp_state_to_flags(neigh);
889         unlock_lock(&neigh);
890         r->arp_ha.sa_family = dev->type;
891         neigh_release(neigh);
892         err = 0;
893     }
894     return err;
895 }
```

图 6.133 ARP—接口—删除 ARP 条目：linux/net/4/arp.c。

```c
898 int arp_req_delete(struct arpreq *r, struct net_device *dev)
899  {
900     int err;
901     u32 ip = ((struct sockaddr_in *)&r->arp_pa)->sin_addr.s_addr;
902     struct neighbour *neigh;

904     if (r->arp_flags & ATF_PUB) {
905         u32 mask = ((struct sockaddr_in *)r->arp_netmask)->sin_addr.s_addr;
906         if (mask == 0xFFFFFFFF) {
907             neigh = neigh_delete(arp_tbl, ip, dev);
908             if (mask == 0) {
909                 if (dev == NULL) {
910                     ipv4_devconf.proxy_arp = 0;
911                     return 0;
912                 }
913                 if (in_dev_get(dev)) {
914                     __in_dev_get(dev)->cnf.proxy_arp = 0;
915                     return 0;
916                 }
917                 return -ENXIO;
918             }
919             return -EINVAL;
920         }
}
```

图 6.134 ARP—用户接口—删除一个 ARP 条目：linux/net/ipv4/arp.c。

```c
if (dev == NULL) {
    struct rtable *rt;
    if ((err = ip_route_output(rt, ip, 0, RTO_ONLINK)) != 0) {
        return err;
    }
    dev = rt->u.dev;
    ip_rt_put(rt);
    if (!dev) {
        return -EINVAL;
    }
}
err = -ENXIO;
neigh = neigh_lookup(arp_tbl, ip, dev);
if (neigh) {
    err = neigh_update(neigh, NULL, NUD_STALE, 1, 0);
}
neigh_release(neigh);
}
return err;
```

图 6.135 ARP—用户接口—ioctl 入口：linux/net/ipv4/arp.c。

```c
int ioctl(unsigned int cmd, void *arg) {
    int err;
    struct arpreq r;
    struct net_device *dev = NULL;
    switch (cmd) {
        case SIOCARP:
            case SIOCARP:
                if (!capable(CAP_NET_ADMIN)) {
                    return -EPERM;
                }
                err = copy_from_user(arg, &r, sizeof(structpreq));
                if (err)
                    return -EFAULT;
                break;
        default:
            return -EINVAL;
    }
    if (r.arp_flags != AF_INET)
        return -EFNOSPORT;
    if (r.arp_flags & (ATF_NETMASK | ATF_DONT)) {
        return -EINVAL;
    }
    if ((r.arp_flags & ATF_NETMASK)) {
        ((struct sockaddr_in *)&r.arp_netmask)->sin_addr.s_addr = htonl(0xFFFFFFFF);
    }
    rtnl_lock();
    if (r.dev[0]) {
        err = -ENODEV;
        if ((dev = dev_get_by_name(r.arp_dev)) == NULL)
            dev = dev_get_hwaddr(r.arp_ha.sa_family, r.arp_ha.sa_data);
            if (!dev)
                return -ENODEV;
        }
        if (dev) {
            if (neigh_lookup(karp_tbl, ip, dev, 1) == NULL)
                return -ENOMBUFS;
        }
        if (r.if_dev(dev) {
            ipv4_devconf.proxy_arp = 1;
            return 0;
        }
    } else if (cmd == SIOCARP) {
        err = -ENODEV;
        goto out;
    }
}
```

图 6.137 ARP—用户接口—procs 入口—写入表：linux/net/ipv4/arp.c。

```c
/*
 * 将 ARP 缓存的内容写入 PROCS 文件。
 */
#ifndef CONFIG_PROC_FS
static int arp_get_info(char *buffer, char **start, off offset, int length) { return 0; }
#else
#if defined(CONFIG_AX25) || defined(CONFIG_AX26_MODULE)
static char *ax25asc2(ax25_address *a, char *buf)
#endif
#define HBUFFERLEN 30
static int arp_get_info(char *buffer, char **start, off offset, int length)
{
```

