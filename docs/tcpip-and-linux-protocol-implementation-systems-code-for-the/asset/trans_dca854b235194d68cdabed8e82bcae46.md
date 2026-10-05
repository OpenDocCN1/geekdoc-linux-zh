

# 384 TCP/IP 与 Linux 协议实现

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
143                               /* 使用调整过的 tcpudp pivot。为什么不呢？ */
144                               check = cksum_tcpudp_magic(ciph->saddr, ciph->daddr, 0, 0, *(cksum)
145                        }
146                            *cksum = cksum_tcpudp_magic(isaddr, idaddr, 0, 0, "check");

148                        break;
149                }
150                default:
151                    break;
152                }
153            return NET_RX_SUCCESS;

155    truncated:
156        /* 应该返回 NET_RX_BAD; */
157        return -EINVAL;
158    }
```

## 6.8 隧道

### 6.8.1 IP in IP 隧道

**6.251** IP in IP 隧道——序言：linux/net/ipv4/ipip.c。

```c
29    / tunnel.c: 一个 IP 隧道驱动程序
30
31    该驱动程序的目的是提供一个 IP 隧道，
32    通过该隧道，你可以透明地跨子网传输网络流量。
33
34    此程序参考了 Nick Holloway 的虚拟驱动程序而编写
35    感谢这些极佳的代码！
36
37        -Sam Latinga (alouken@cs.ucdav.edu) 02/01/95
38
39    微调：
40    清理了代码并添加了一些针对 1.3.0 之前的调整。
41    dev->hard_header/hard_header_len 更改为不使用头部。
42    调整了注释/破坏性更改。
43    使隧道在错误报告时使用 dev->name tunnel。
44 添加了 tx_dropped 统计量
45

46 -Alan Cox (Alan.Cox@linux.org) 95年3月21日
47
48 重构：
49    更改为除了隧道的多点地址外，还隧道到
50    目标网关
51
52    几乎完全重写
53    注意：目前尚未进行防火墙或 ICMP 处理。
54
55 -Sam Lanting (slouken@cs.udavis.edu) 96年1月13日
56 */

# 图 6.252 互联网协议改进规则：linux/net/ipv4/ipip.c

/* 
58 我希望在编写隧道驱动程序时知道的事宜：
59
60    当调用 tunnel_xmit() 函数时，skb 包含了
61    要发送的数据包（以及大量额外信息），dev 
62    包含了我们正在使用的隧道设备。
63
64    当我们接收到一个数据包时，我们预期在源地址
65    填入我们的源 IP 地址。
66
67    分配、拷贝和释放缓冲区的正确方法是什么？
68    在你分配后，它是一个从零开始的“0”内存块。
69    如果你稍后想向缓冲区添加头部，
70    你必须调用 skb_reserve(skb, amount) 预留
71    所需的内存。然后调用
72    skb_put(skb, amount) 返回缓冲区
73    结束空间的指针。
74    skb->len 返回通过 skb_put() 分配
75    剩余的空间。如果你需要更多空间，可以再次
76    调用 skb_put 你需的空间。
77    你可以通过 skb_tailroom(skb) 
78    发现可以分配多少空间。
79
80    现在，为了添加头部，调用 skb_push(skb, header_len)。
81    这会在缓冲区开头创建空间并返回
82    该新空间的指针。如果你需要剥离
83    缓冲区的头部（减去主数据），调用
84    skb_pull(skb, header_len)。
85    记住，在调用 skb_put() 之前
86    必须预留空间
87*/
88
89    这个版本的 net/ipv4/ipip.c 是
90    net/ipv4/gre.c 的拷贝
91    注释请参见 net/ipv4/gre.c -- 以及
92  */

# TCP/IP 与 Linux 协议实现

# 图 6.253 IP in-data：linux/net/ipv4/ipip.c。

```c
#define HASH_SIZE 16
#define HASH(addr) (((addr)>>4)
static int ipip_tunnel_init(struct net_device *dev);
static struct net_device ipip_fb_dev = {
    "tun0", 0, 0, 0, 0, NULL, ipip_tunnel_init
};
static struct ip_tunnel ipip_fb_dev = {
    NULL, &ipip_fb_dev, 0, 0, 0, "tun0"},
};
static struct ip_tunnel tunnels_r1[HASH_SIZE];
static struct ip_tunnel tunnels_r[HASH_SIZE];
static struct ip_tunnel tunnels_l1[HASH_SIZE];
static struct ip_tunnel tunnels_wc[1];
static struct ip_tunnel tunnels[4] = {tunnels_wc, tunnels_r};
static rwlock_t ipip_lock = RW_LOCKED;
```

# 图 6.254 基于本地和远程的 IP 查找：linux/net/ipv4/ipip.c。

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

# 图 6.255 IP in IP-隧道桶：linux/net/ipv4/ipip.c。

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

# 图 6.256 IP in IP-unlink/link 隧道哈希项：linux/net/ipv4/ipip.c。

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

# 图 6.257 IP in-tunnel：linux/net/ipv4/ipip.c。

```c
208      struct ip_tunnel *ipip_tunnel_locate(struct ip_tunnel *parms, int create)
209      {
210          u32 remote = parms->daddr;
211          u32 local = parms->saddr;
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
226              if (local == t->parms.saddr && remote == t->parms.daddr)
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
238      }
```

# 图 6.258 IP in ip-locate 隧道：linux/net/ipv4/ipip.c。

```c
239      dev->priv = (void*)(dev+1);
240      nt = (struct ip_tunnel*)dev->priv;
241      nt->dev = dev;
242      dev->init = ipip_tunnel_init;
243      dev->features |= NETIF_F_DYNALLOC;
244      memcpy(nt->parms, parms, sizeof(*parms));
245      strncpy(dev->name, parms->name, IFNAMSIZ);
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
258}
```

