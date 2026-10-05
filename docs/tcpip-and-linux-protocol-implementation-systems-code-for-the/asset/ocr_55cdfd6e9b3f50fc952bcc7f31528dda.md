# Figure 6.136 ARP-user-interface--ioctl entry point: linux/net/ipv4/arp.c

```
rtnl_lock();
if (r.arp_dev[0]) {
    err = -ENODEV;
    if ((dev = dev_get_by_name(r.arp_dev)) == NULL)
        goto out;
    /* Mmmm... It is wrong... ARPHRD_NETROM=O * */
    if (r.arp_ha.sa_family)
        r.arp_ha.sa_family = dev->type;
    err = -EINVAL;
    if (r.arp_flags & AT_CONF) &&& r.arp_ha.sa_family != dev->type)
        goto out;
} else if (cmd == SIOCARP) {
    err = -ENODEV;
    goto out;
}
switch(cmd) {
case SIOCARP:
    err = arp_req_delete(kr, dev);
    break;
case SIOCARP:
    err = arp_req_set(kr, dev);
    break;
case SIOCARP:
    err = arp_req_get(kr, dev);
    if (!err && copy_to_user(arg, r, sizeof(r)))
        err = -EFAULT;
    break;
}
out:
rtnl_unlock();
return err;
}
```

# Figure 6.137 ARP-user-interface--procs entry point--write table: linux/net/ipv4/arp.c.

```
/*
 * Write the contents of the ARP cache to a PROCS file.
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