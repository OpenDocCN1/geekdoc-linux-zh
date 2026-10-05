# Figure 8.33 FIB semantics--set defaults: linux/net/ipv4/fib.semantics.c.

```
/* Check, that the gateway is already configured.
Used only by redirect accept.
*/
int ip_fib_check_default(u32 gw, struct net_device *dev)
{
    read_lock(&fib_info_lock);
    for_fib_info(fi) {
        if (fi->flags & RTNH_F_DEAD)
            continue;
        for_nexthops(fi) {
            if (nh->nh_dev == dev && nh->nh_gw == gw
                if (!nh->flags&RTNH_F_DEAD))
                    read_unlock(&fib_info_lock);
                    return 0;
        }
    }
    read_unlock(&fib_info_lock);
    return -1;
}

#ifdef CONFIG_IP_ROUTE_MULTIPATH
static u32 fib_get_attr(struct rtattr *attr, int attrlen, int type)
{
    while (RTA_OK(attr, attrlen)) {
        if (attr->rta_type == type)
            return (u32*)RTA_DATA(attr);
        attr = RTA_NEXT(attr, attrlen);
    }
```

# Figure 8.34 FIB semantics--add up next hops and get nhs: linux/net/ipv4/fib.semantics.c.

```
return 0;
static int
fib_count_nexthops(struct rtattr *rta)
{
    int nhs = 0;
    struct rtnextop *nhp = RTA_DATA(rta);
    int nhlen = RTA_PAYLOAD(rta);
    while (nhlen > (int)sizeof(struct rtnextop)) {
        if (nhlen - nhp->rtnh_len < 0)
            return 0;
        nhs++;
        nhp = RTNH_NEXT(nhp);
    }
    return nhs;
```