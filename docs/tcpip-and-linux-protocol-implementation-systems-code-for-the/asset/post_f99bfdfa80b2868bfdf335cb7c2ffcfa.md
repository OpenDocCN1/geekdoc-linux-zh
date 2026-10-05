
# 402 TCP/IP and Linux Protocol Implementation

```c
870 dev_hold(dev);
871 tunnels_wc[0] = ipip_fb_tunnel;
872 return 0;
873 }
875 static struct inet_protocol ipip_protocol = {
876 ipip_rcv,         /* ipip handler */
877 ipip_err,         /* TUNNEL error control */
878                   /* next */
879 IPPROTO_IPIP,    /* protocol ID */
880 0,                /* copy */
881 NULL,             /* data */
882 "IPIP",         /* name */
883 };
```

# 6.8.2 GRE Tunnels

Figure 6.281 GRE tunnels–opening salvo: linux/net/ipv4/ip_gre.c.

Problems & solutions

- 1. The most important issue is detecting local dead loops. They would cause host lockup in transit, which would be "resolved" by stack overflow or, if queueing is enabled, with infinite looping in net_bh.

- We cannot track dead loops during route installation, it is infeasible. The most general solutions would be to keep skb->encapsulation counter (sort of local ttl), and silently drop packet when it expires. It is the best solution, but it suppresses maintaining variable in ALL skb, even if no tunneling is used.

- Current solution: t-recursion breaks dead loops. It looks like dev->flush flag, but I preferred new variable, because the semantics is different. One day, when hard_start_xmit will be multithreaded we will have to use skb->encapsulation.

Figure 6.282 GRE tunnels–opening salvo: linux/net/ipv4/ip_gre.c.

- 2. Networking protocols would not kill routers, but would really kill network. IP hop limit plays role of "t-recursion" in this case, if we copy it from packet being encapsulated to upper header. It is very good, but it introduces two problems:

- Routing protocols, with packets with ttl=i (OSPF, RIP2), do not work over tunnels.

# 403 Infrastructure Protocols

77 traceroute does not work. I planned to relay ICMP from tunnel,
78 so that this problem would be solved by traceroute output
79 even more informative. This idea appeared to be wrong:
80 only Linux complies with rfc8192 now (yes, Linux is the only true router now -), all routers (at, in neighbourhood of mine)
82 return only 8 bytes of payload. It is the end.

83 Hence, if we want UDP work or traceroute said something reasonable,
84 we should search for another solution.

85 One of them is to parse packet to detect inner encapsulation made by our node. It is difficult or even impossible, especially, taking into account fragmentation. To be short, it is not lost at all.

86 Current solution: The solution was UNEXPECTED SIMPLY we force DF flag on tunnels with preconfigured hop limit, that is ALL. Well, it does not remove the problem completely, but exponential growth of network traffic is changed to linear (where mtu are pruned) and tunnel mtu degrades to <, where looping stops.

87 Yes, it is not good if there exists a router, which does not force DF, when encapsulating packets have DF. But it is not our problem! Nobody could accuse us, we made all that we could. Even if it is injected into network, even if static route you are innocent :-)

88 3. Really, ipv4/ipip.c, ipv4/ip_gre.c and ipv6/sit.c contain practically identical code. It would be good to glue them together, but it is not evident how to make them modular. sit is integral part of IPv6, ipip and gre are naturally modular. we could extract common parts (hash table, ioctl etc) to a separate module (ip_tunnel.c/06c1ba8be5c1c4aa63e1261e2ebd_0.png).

```c
116 static int ipgre_tunnel_init(struct net_device *dev);
118 /* Fallback tunnel: no source, destination, no key, no options
120 static int ipgre_fb_tunnel_init(struct net_device *dev);
122 static struct net_device ipgre_fb_tunnel_dev = {
123 "gre0", 0x0, 0x0, 0x0, 0, 0, NULL, ipgre_tunnel_init,
124 };
126 static struct ip_tunnel ipgre_fb_tunnel = {
127 NULL, &ipgre_fb_tunnel_dev, {0}, 0, 0, 0, 0, "gre0"},
128 };
```

# 404 TCP/IP and Linux Protocol Implementation

```c
/* Tunnel hash table */
4 hash tables:
3: (remote,local)
2: (remote,*)
1: (*,local)
0: (*,*)
exact key match i.e. if a key is present in packet it will match only tunnel with the same key; if it is not present, it will match keyless tunnel.
All keyless packets, if not matched configured keyless tunnels will match fallback tunnel.
*/

#define HASH_SIZE 16
#define HASH_addr(addr) ((addr)>>4)&0xF

static struct ip_tunnel *tunnel[4][HASH_SIZE];

#define tunnels_r_1 (tunnels[3])
#define tunnels_r (tunnels[2])
#define tunnels_l (tunnels[1])
#define tunnels_wc (tunnels[0])

static rwlock_t ipgre_lock = RW_LOCK_UNLOCKED;
```

Figure 6.284 GRE tunnels-hashing function: linux/net/ipv4/ip_gre.c.

/* Given arc */

# 405 Infrastructure Protocols

```c
for (t = tunnels_l[hi]; t = t->next) {
    if (local == t->parms.iph.saddr &&
        (local == t->parms.iph.daddr && MULTICAST(local))) {
            if (t->parms.i_key == key && (t->dev->flags&IFF_UP)) {
                return t;
            }
        }
}
for (t = tunnels_wc[hi]; t = t->next) {
    if (t->parms.i_key == key && (t->dev->flags&IFF_UP)) {
        return t;
    }
}
if (ipgre_fb_tunnel->flags&IFF_UP) {
    return &ipgre_fb_tunnel;
}
return NULL;
```

Figure 6.285 GRE tunnels–hash bucket: linux/net/ipv4/ip.gre.c

```c
static struct ip_tunnel **ipgre_bucket(struct ip_tunnel *t) {
    u32 remote = t->parms.iph.daddr;
    u32 local = t->parms.iph.saddr;
    u32 key = t->parms.i_key;
    unsigned h = HASH(key);
    int prio = 0;
    if (local) {
        prio = 1;
        if (remote && MULTICAST(remote)) {
            prio = 2;
        }
        h = HASH(remote);
    }
    return tunnels[prio][h];
}
```

Figure 6.286 GRE tunnels–link/unlink entry: linux/net/ipv4/ip.gre.c

```c
static void ipgre_tunnel_link(struct ip_tunnel *t) {
    struct ip_tunnel **tp = ipgre_bucket(t);
    t->next = *tp;
    write_lock_bh(&ipgre_lock);
    *tp = t;
    write_unlock_bh(&ipgre_lock);
}
static void ipgre_tunnel_unlink(struct ip_tunnel *t) {
    struct ip_tunnel **tp;
    for (tp = ipgre_bucket(t); tp = &(tp)->next) {
        if (t == *tp) {
            write_lock_bh(&ipgre_lock);
            *tp = t->next;
            write_unlock_bh(&ipgre_lock);
            break;
        }
    }
}
```

# 406 TCP/IP and Linux Protocol Implementation

```c
static struct ip_tunnel *ipgre_tunnel_locate(struct ip_tunnel *parms, int create) {
    u32 remote = parms->ip->daddr;
    u32 local = parms->ip->daddr;
    u32 key = parms->i_key;
    struct ip_tunnel *t, *tp, *nt;
    struct net_device *dev;
    unsigned h = HASH(key);
    int prio = 0;
    if (local) {
        prio = 1;
        if (remote && MULTICAST(remote)) {
            prio = 2;
        }
        h = HASH(remote);
    }
    for (tp = &tunnels[prio][h]; *tp; tp = &(*tp)->next) {
        if (local == t->parms.ip.daddr && remote == t->parms.ip.daddr) {
            if (key == t->parms.i_key)
                return t;
            }
        }
    }
    if (!create)
        return NULL;
    }
    MOD_INC_USE_COUNT;
```

# 6.288 GRE tunnels--uninitialize and destroy entry: linux/net/ipv4/ip_gre.c

```c
if (dev == NULL) {
    MOD_DEC_USE_COUNT;
    return NULL;
}
   memset(dev, 0, sizeof(*dev) + sizeof(*tp));
   dev->priv = (void*)(dev+1);
   nt = (struct ip_tunnel*)dev->priv;
   nt->dev = dev;
   dev->init = ipgre_tunnel_init;
```

```c
dev->features |= NETIF_F_DYN;
memcpy(nt->parms, parms, sizeof(*parms));
strncpy(dev->name, nt->parms.name);
if (dev->name[0] == 0) {
    int i;
    for (i=0; i<100; i++) {
        sprint(dev->name, "gre%d", i);
        if (dev->get_by_name(dev->name) == NULL) {
            break;
        }
        if (i==100) {
            goto failed;
            memcpy(parms->name, dev->name, IFNSIZ);
        }
    }
}
if (register_device(dev) < 0) {
    goto failed;
}
dev_hold(dev);
ipgre_tunnel_link(nt);
/* Do not create MOD_USE_COUNT here. */
return nt;

failed:
kfree(dev);
MOD_DEC_USE_COUNT;
return NULL;
```

```c
static void ipgre_tunnel_destructor(struct net_device *dev) {
    if (dev != &ipgre_fb_tunnel_dev) {
        MOD_DEC_USE_COUNT;
    }
}
static void ipgre_tunnel_init(struct net_device *dev) {
    ipgre_tunnel_unlink((struct tunnel*)dev->priv);
    dev_put(dev);
}
```

# Receive Data in GRE Tunnels

Figure 6.289 GRE tunnels-receive case: linux/net/ipv4/ip_gre.c.
