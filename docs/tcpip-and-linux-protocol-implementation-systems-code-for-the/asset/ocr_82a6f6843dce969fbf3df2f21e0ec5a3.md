# 574 TCP/IP and Linux Protocol Implementation

313

Attempt to reconcile all of these (alas, self-contradictory) conditions
results in pretty ugly and hairy code with obscure logic.

316

I chose to generalized it instead, so that the size
code does not increase practically, but it becomes
much more general.

319

Every prefix is assigned a "scope value: "host" is local address,
link" is direct route,
[... "site" "interior" ...]
and "universe" is true gateway route with global meaning.

324

Every prefix refers to a set of "nexthop" (gw, oif),
where gw must have narrower scope. This recursion stops
when gw has LOCAL scope or if "nexthop" is declared ONLINK,
which means gw is forced to be on link.

329

Code is still hairy, but now it is apparently logically
consistent and very flexible. F.e. as by-product it allows
to coexists in peace independent exterior and interior
routing processes.

334

Normally it looks as following.

```
{universe prefix) -> (gw, oif) [scope link]
|
|-> (link prefix) -> (gw, oif) [scope local]
|
|-> [local prefix] (terminal node)
*/
```

# Checking for Next Hop

Figure 8.38 FIB semantics--check next hop: linux/net/ipv4/fib_semantics.c.

```
static int fib_check_nh(const struct rtmg *rtmsg, struct fib_info *fi, struct fib_nh *nh)
{
	int err;

	if (nh->gw) {
	struct rt_key key;
	struct fib_result res;
	#ifdef CONFIG_IP_ROUTE_PERVASIVE
		if (nh->flags&RTNH_F_PERVASIVE) {
		eturn 0;
	}
	#endif
		struct net_device *dev;

	tif (r->scope >= RT_SCOPE_LINK) {
		eturn -EINVAL;
	}
}
}
```