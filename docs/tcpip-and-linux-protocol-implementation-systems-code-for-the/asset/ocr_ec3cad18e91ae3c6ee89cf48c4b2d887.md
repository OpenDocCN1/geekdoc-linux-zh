# 592 TCP/IP and Linux Protocol Implementation

```
struct net_dev *dev;
memcpy(new_r->r_ifname, RTA_DATA(rta[RTA_IIF-1]), IFNAMSIZ);
new_r->r_ifname[IFNAMSIZ] = 0;
new_r->r_ifindex = -1;
dev = _dev_get_by_name(new_r->r_ifname);
if (dev)
    new_r->r_ifindex = dev->ifindex;
}
#ifdef CONFIG_CLS_ROUTE
if (rta[new_r->r_tclass], RTA_DATA(rta[RTA_FLOW-1]), 4)
memcpy(new_r->r_tclass, RTA_DATA(rta[RTA_FLOW-1]), 4);
#endif
```

Figure 8.64 FIB rules—name: linux/net/ipv4/fib_rules.c.

```
r = &fib_rules;
if (!new_r->r_preference) {
    r = fib_rules;
    if (r && (r->r_next) != NULL) {
        r = &fib_rules->r_next;
        if (new_r->r_preference)
            new_r->r_preference = r->r_preference - 1;
    }
}
while (r->rp) != NULL) {
    if (r->r_preference > new_r->r_preference)
        break;
    rp = &r->r_next;
}
new_r->r_next = r;
atomic_inc(&new_r->r_clntref);
write_lock_bh(&fib_rules->lock);
*rp = new_r;
write_unlock_bh(&fib_rules->lock);
return 0;
```

Figure 8.65 FIB rules—more uses: linux/net/ipv4/fib_rules.c.

```
u32 fib_rules_map_destination(u32 daddr, struct fib_struct *res)
{
    u32 mask = inet_make_mask(res->prefixlen);
    return (daddr&mask)|res->fi->fib_nh_gw;
}
u32 fib_rules_policy(u32 saddr, struct fib_struct *res, unsigned flags)
{
    struct fib_struct *r = res->r;
    if (r->r_action == RTW_NAT) {
```