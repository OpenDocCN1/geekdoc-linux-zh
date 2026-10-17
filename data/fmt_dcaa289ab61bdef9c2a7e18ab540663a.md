
## 图 6.133 ARP—接口—删除 ARP 条目：`linux/net/4/arp.c`

```c
895 }

```

```c
898 int arp_req_delete(struct arpreq *r, struct net_device *dev)
899  {
900     int err;
901     u32 ip = ((struct sockaddr_in *)&r->arp_pa)->sin_addr.s_addr;
902     struct neighbour *neigh;
903     if (r->arp_flags & ATF_PUB) {
904         u32 mask = ((struct sockaddr_in *)r->arp_netmask)->sin_addr.s_addr;
905         if (mask == 0xFFFFFFFF) {
906             neigh = neigh_delete(arp_tbl, ip, dev);
907             if (mask == 0) {
908                 if (dev == NULL) {
909                     ipv4_devconf.proxy_arp = 0;
910                     return 0;
911                 }
912                 if (in_dev_get(dev)) {
913                     __in_dev_get(dev)->cnf.proxy_arp = 0;
914                     return 0;
915                 }
916                 return -ENXIO;
917             }
918             return -EINVAL;
919         }
}
```

## 图 6.134 ARP—用户接口—删除一个 ARP 条目：`linux/net/ipv4/arp.c`

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

## 图 6.135 ARP—用户接口—ioctl 入口：`linux/net/ipv4/arp.c`

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

## 图 6.137 ARP—用户接口—procs 入口—写入表：`linux/net/ipv4/arp.c`

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

# TCP/IP 与 Linux 协议实现

```c
1022  int len=0;
1023  off_t pos=0;
1024  int size;
1025  char hbuffer[HBUFFERLEN];
1026  int i,j,k;
1027  const hexbuf[] = "0123456789ABCDEF";

1029  size = sprintf(buffer,"IP address HW type Flags HW address Mask Device="%s");

1031  pos+=size;
1032  len+=size;

1034  for(i=0; i<NEIGH_HASHMASK; i++) {
1035    struct neighbour *n;
1036    read_lock_bh(&arp_tbl[i]);
1037    for (n=arp_tbl[i].hsb_buckets[j]; n; n=n->next) {
1038      struct net_dev *dev = n->dev;
1039      int intype = dev->type;

1041      /* 不要将用户的 "arp -a" 与魔术项混淆 */
1042      if ((n->nud_state&NUD_NOARP))
1043        continue;
1044  }

1046  read_lock(kn->lock);
```
