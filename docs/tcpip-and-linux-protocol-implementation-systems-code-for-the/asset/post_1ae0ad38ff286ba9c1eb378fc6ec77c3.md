
# 384 TCP/IP and Linux Protocol Implementation

```c
133                               if (ciph->daddr == idaddr)
134                               updated = 1;
135                               }
136                            fib_res_put(res);
137                        }
138                    } else {
139                            ciph->daddr = ip->saddr;
140                               updated = 1;
141                    if (updated) {
142                               cksum = &icmp->checksum;
143                               /* Using tcpudp pivot tweaked. Why not? */
144                               check = cksum_tcpudp_magic(ciph->saddr, ciph->daddr, 0, 0, *(cksum)
145                        }
146                            *cksum = cksum_tcpudp_magic(isaddr, idaddr, 0, 0, "check");
147
148                        break;
149                }
150                default:
151                    break;
152                }
153            return NET_RX_SUCCESS;
154
155    truncated:
156        /* should return NET_RX_BAD; */
157        return -EINVAL;
158    }
```

## 6.8 Tunnels

### 6.8.1 IP in IP Tunnels

**6.251** IP in IP tunnel—opening remarks: linux/net/ipv4/ipip.c.

```c
29    / tunnel.c: an IP tunnel driver
30
31    The purpose of this driver is to provide an IP tunnel through
32    which you can tunnel network traffic transparently across subnets.
33
34    This was written by looking at Nick Holloway's dummy driver
35    Thanks for the great code!
36
37        -Sam Latinga (alouken@cs.ucdav.edu) 02/01/95
38
39    Minor tweaks:
40    Cleaned up the code and added some pre-1.3.0 tweaks.
41    dev->hard_header/hard_header_len changed to use no headers.
42    Comments/breaking tweaked.
43    Made the tunnels use dev->name tunnel: when error reporting.
44 Added tx_dropped stat
45
46 -Alan Cox (Alan.Cox@linux.org) 21 March 95
47
48 Reworked:
49    Changed to tunnel to destination gateway in addition to the
50    tunnel's multipoint address
51
52    Almost completely rewritten
53    Note: There is currently no firewall or ICMP handling done.
54
55 -Sam Lanting (slouken@cs.udavis.edu) 02/13/96
56 */

# Figure 6.252 Internet Protocol-rule for improvement: linux/net/ipv4/ipip.c

/* 
58 Things I wish had known when writing the tunnel driver:
59
60    When the tunnel_xmit() function is called, the skb contains
61    the packet to be sent (plus a great deal of extra info), and dev
62    contains the tunnel device that we are.
63
64    When we are passed a packet, we are expected to fill in the
65    source with our source IP address.
66
67    What is the proper way to allocate, copy and free a buffer?
68    After you allocate it, it is a "0" chunk of memory
69    starting at zero. If you want to add headers to the buffer
70    later, you will have to call skb_reserve(skb, amount) with
71    the amount of memory you want reserved. Then you call
72    skb_put(skb, amount) returns a pointer to the end of space you want
73    that buffer. skb->len() returns the amount of space you have left
74    allocated with skb_put(). You can write up to skb->len
75    by that buffer. If you need more, you can call skb_put(
76    again with the amount of space you need. You can use
77    find out how much space you can allocate by calling
78    skb_tailroom(skb).
79
80    Now, to add header, call skb_push(skb, header_len).
81    This creates space at the beginning of the buffer and returns
82    a pointer to this new space. If you need to strip a
83    header from the buffer, call "skb_pull(skb, header_len).
84    of the buffer (minus the main data). Remember, this headroom
85    space must be reserved before the skb_put() function is called
86
*/
89
90    This version of net/ipv4/ipip.c is a copy of net/ipv4/ip_gre.c
91
92    For comments look at net/ipv4/ip_gre.c -- AND
93  */
```

# TCP/IP and Linux Protocol Implementation

> Figure 6.253 IP in-data: linux/net/ipv4/ipip.c.

```c
#define HASH_SIZE 16
#define HASH(addr) (((addr)>>4)&0xF)
static int ipip_tunnel_init(struct net_device *dev);
static struct net_device ipip_fb_dev = {
    "tun0", 0, 0, 0, 0, 0, NULL, ipip_tunnel_init
};
static struct ip_tunnel ipip_fb_dev = {
    NULL, &ipip_fb_dev, 0, 0, 0, 0, "tun0"},
};
static struct ip_tunnel tunnels_r1[HASH_SIZE];
static struct ip_tunnel tunnels_r[HASH_SIZE];
static struct ip_tunnel tunnels_l1[HASH_SIZE];
static struct ip_tunnel tunnels_wc[1];
static struct ip_tunnel tunnels[4] = {tunnels_wc, tunnels, tunnels_r};
static rwlock_t ipip_lock = RW_UNLOCKED;
```

> Figure 6.254 IP in-lookup based on local and remote: linux/net/ipv4/ipip.c.

```c
static struct ip_tunnel ipip_tunnel_lookup(u32 remote, u32 local)
{
    unsigned h0 = HASH(remote);
    unsigned h1 = HASH(local);
    struct ip_tunnel *t;

    for (t = tunnels_r1[h0]; t; t = t->next) {
        if (local == t->parms.saddr && (t->dev->flags&IFF_UP)
            remote == t->parms.saddr && (t->dev->flags&IFF_UP)
            return t;
    }
    for (t = tunnels_r[h0]; t; t = t->next) {
        if (remote == t->parms.saddr && (t->dev->flags&IFF_UP)
            return t;
    }
    for (t = tunnels_l1[h1]; t; t = t->next) {
        if (local == t->parms.saddr && (t->dev->flags&IFF_UP)
            return t;
    }
    if ((t = tunnels_wc[0]) != NULL && (t->dev->flags&IFF_UP)
        return t;

    return NULL;
}
```

# Figure 6.255 IP in IP-tunnel bucket: linux/net/ipv4/ipip.c.

```c
static struct ip_tunnel **ipip_bucket(struct ip_tunnel *t)
{
    u32 remote = t->parms.daddr;
    u32 local = t->parms.saddr;
    unsigned h = 0;
    int prio = 0;

    if (remote) {
        prio = 2;
        h = HASH(remote);
    }
    if (local) {
        prio = 1;
        h = HASH(local);
    }
    return &tunnels[prio][h];
}
```

# Figure 6.256 IP in IP-unlink/link tunnel hash entry: linux/net/ipv4/ipip.c.

```c
static void ipip_tunnel_unlink(struct ip_tunnel *t)
{
    struct ip_tunnel **tp;
    for (tp = ipip_bucket(t); *tp; tp = &(*tp)->next) {
        if (t == *tp) {
            write_lock_bh(ipip_lock);
            *tp = t->next;
            write_unlock_bh(ipip_lock);
            break;
        }
    }
}

static void ipip_tunnel_link(struct ip_tunnel *t)
{
    struct ip_tunnel **tp = ipip_bucket(t);
    t->next = *tp;
    write_lock_bh(ipip_lock);
    *tp = t;
    write_unlock_bh(ipip_lock);
}
```

# Figure 6.257 IP in ip-tunnel: linux/net/ipv4/ipip.c.

```c
208      struct ip_tunnel *ipip_tunnel_locate(struct ip_tunnel *parms, int create)
209      {
210          u32 remote = parms->iph.daddr;
211          u32 local = parms->iph.saddr;
212          struct ip_tunnel *t, **tp, *nt;
213          struct net_device *dev = dev;
214          unsigned char h = 0;
215          int prio = 0;
216
217          if (remote) {
218              prio = 2;
219              h = HASH(remote);
220          }
221          if (local) {
222              prio = 1;
223              h = HASH(local);
224          }
225          for (tp = tunnels[prio][h]; (t = *tp) != NULL; tp = t->next) {
226              if (local == t->iph.saddr && remote == t->iph.daddr)
227                  return t;
228          }
229          if (create) {
230              return NULL;
231
232              MOD_INC_USE_COUNT;
233              dev = kmalloc(sizeof(*dev) + sizeof(*t), GFP_KERNEL);
234              if (dev == NULL) {
235                  MOD_DEC_USE_COUNT;
236                  return NULL;
237              }
238}
```

# Figure 6.258 IP in ip-locate a tunnel: linux/net/ipv4/ipip.c.

```c
239      dev->priv = (void*)(dev+1);
240      nt = (struct ip_tunnel*)dev->priv;
241      nt->dev = dev;
242      dev->init = ipip_tunnel_init;
243      dev->features |= NETIF_F_DYNALLOC;
244      memcpy(nt->parms, parms, sizeof(*parms));
245      strncpy(dev->name, name, nt->parms.name);
246      if (dev->name[0] == 0) {
247          int i;
248          for (i=0; i<100; i++) {
249              sprintf(dev->name, "tun%d", i);
250              if (dev_get_by_name(dev->name) == NULL)
251                  break;
252          }
253          if (i==100)
254              goto failed;
255      }
256      memcpy(parms->name, dev->name, IFNAMSIZ);
257  }
```
