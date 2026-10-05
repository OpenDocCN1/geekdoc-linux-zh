# 846 TCP/IP and Linux Protocol Implementation

# 9.13.13 Link Equalization

**Figure 9.298** Traffic equalization/load balance queue-initial remarks: linux/net/sched/sch_teql.c.

```
/
# How to setup it.
--------------------
After loading this module you will find a new device teqlN
--------------------
```

After loading this module you will find a new device teqlN
and new qdisc with the same name. To join a slave to the equalizer
you should just set this qdisc on a device f.e.

```
# tc qdisc add dev eth0 teql0
# tc qdisc add dev eth1 teql0
```

That's all. Full PnP 8

Applicability:

+   1. Slave devices MUST be active devices, i.e., they must raise the tbus
signal and generate eci events if you want to equalize virtual devices
like tunnels, use a normal eci.
2. This device puts no limitations on physical slave characteristics
f.e. it will equalize 900Mbps line and 100Gbps ethernet perfectly :--
Certainly, large difference in link speeds will make the resulting
equalized link unlinkable, because of huge packet reordering.
I estimate no useful difference as "10 times".
3. If the slave requires address resolution, only protocols using
neighbour cache (IPv4/IPv6) will work over the equalized link.
Other protocols are still allowed to use the slave device directly,
which will not break load balancing, though native slave
traffic will have the highest priority. /*

**Figure 9.299** TE data: linux/net/sched/sch_teql.c.

```
struct teql_master
{
    struct qdisc_ops qops;
    struct net_device dev;
    struct qdisc *slaves;
    struct net_device_stats stats;
};
struct teql_sched_data
{
    struct qdisc *next;
    struct teql_master *ms;
    struct neighbour *ncache;
    struct sk_buff_head q;
};
```