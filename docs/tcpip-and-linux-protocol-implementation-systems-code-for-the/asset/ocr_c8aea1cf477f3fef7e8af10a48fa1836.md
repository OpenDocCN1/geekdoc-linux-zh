# TCP/IP and Linux Protocol Implementation

Figure 6.189 IGMP joins socket to group: linux/net/ipv4/igmp.c.

```
iml = (struct ip_mc_socklist*)sock_kmalloc(sk, sizeof(*iml), GFP_KERNEL);

err = -EADDRINUSE;
for (i=sk->protoinfo.af_inet.mc_list; i; i=i->next) {
    if (memcmp(i->imr_address.s_addr, imr) == 0) {
        /* New styles additions are reference count */\n        if (iml->imr_address.s_addr == 0) {
            count++;
            err = 0;
        }
        goto done;
    }
    count++;
}
err = -ENOMFS;
if (iml == NULL || count > sysctl_igmp_max_memberships) {
    goto done;
    memcpy(iml->multi, imr, sizeof(*iml)->af_inet.mc_list);
iml->next = sk->protoinfo.af_inet.mc_list = iml;
    iml->count = 1;
}
ip_mc_group(in_dev, addr);
iml = 0;
}

done:
fcntl_shunlock();
if (iml) {
    sock_kfree(sk, iml, sizeof(*iml));
}
return err;
```

Figure 6.190 IGMP: linux/net/ipv4/igmp.c.

```
int ip_mc_leave_group(struct sock *sk, struct ip_mreq *imr)
{
    struct ip_mc_socklist *iml, **iml;
    rtnl_lock();
    for (iml=sk->protoinfo.af_inet.mc_list; iml && iml->next!=NULL; iml=iml->next) {
        if (iml->imr_multiaddr.s_addr==imr->imr_address.s_addr &&
            iml->imr_address.s_addr==imr->imr_address.s_addr &&
            (!iml->imr_index==iml->imr_index)) {
            struct in_device *in_dev;
            if ((--iml)->count) {
                rtnl_unlock();
                return 0;
            }
        }
    }
    *iml = iml->next;
```