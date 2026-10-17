
## 图 6.110 ARP 映射 MAC-类型/IEEE-类型：`linux/net/ipv4/arp.c`

```
184 struct neigh_table arp_tbl = =
185 {
186     NULL,
187     AF_INET,
188     sizeof(struct neighbour) + 4,
189     4,
190     arp_hash,
191     arp_constructor,
192     NULL,
193     NULL,
194     arp_redo,
195     arp_cache,
196     { NULL, arp_tbl, 0, NULL, NULL,
197         30*HZ, 1*HZ, 60*HZ, 30*HZ, 5*HZ, 3, 0, 3, 1*HZ, (8*HZ)/10, 64, 1*HZ,
198         30*HZ, 128, 512, 1024,
199 };
```

## 图 6.111 ARP 哈希函数：`linux/net/ipv4/arp.c`

```
201 int arp_nc_map(u32 addr, u8 *haddr, struct net_device *dev, int dir)
202 {
203     switch (dev->type) {
204     case ARPHRD_ETHER:

205 case ARPHRD_FDDI:
206 case ARPHRD_IEEE8082:
207   _eth_mc_map(addr, haddr);
208   return 0;
209 case ARPHRD_IEEE8082_TR:
210   _tr_mc_map(addr, haddr);
211   return 0;
212 default:
213   if (dir) {
214     memcpy(haddr, dev->broadcast, dev->addr_len);
215     return 0;
216   }
217  }
218  return -EINVAL;
219 }
```

## 图 6.112 ARP 条条目：`linux/net/ipv4/arp.c`

```
222 static u32 arp_hash(const void *pkey, const struct net_device *dev)
223 {
224   u32 hash_val;
225
226   hash_val = *(u32*)pkey;
227   hash_val ^= (hash_val>>16);
228   hash_val ^= (hash_val>>8);
229   hash_val ^= (hash_val>>3);
230   hash_val = (hash_val*dev->index)&NEIGH_HASHMASK;
231
232   return hash_val;
233 }
```

## 图 6.113 ARP 构建条目：`linux/net/ipv4/arp.c`

```
235 static int arp_constructor(struct neighbour *neighbor)
236 {
237   u32 addr = *(u32*)neighbor->primary_key;
238   struct net_device *dev = neighbor->dev;
239   struct in_dev *in_dev = in_dev_get(dev);
240
241   if (in_dev == NULL) {
242     return -EINVAL;
243   }
244   neigh->type = inet_addr_type(addr);
245   if (in_dev->parms) {
246     neigh->parms = in_dev->parms;
247   }
248
249   in_dev_put(in_dev);
250   if (dev->header == (void *)hard_header) {
251     neigh->nud->state = NUD_NOARP;
252      neighp->ops = &arp_direct_ops;
253      neighp->output = neighp->ops->queue_xmit;
254  } else {
255      /* 好设备（通过文本检查，但只有以太网测试过）
256      ARPHRD_ETHER: (ether, dev)
257      ARPHRD_FDDI: (dev)
258      ARPHRD_IEEE8082: (tr)
259      ARPHRD_METRIC: (strip)
260      ARPHRD_CNET:
261      等等。
262
263      ARP_IP 也会工作，如果作者修复了它。
264      我没有做，因为这个驱动在
265      旧范式下不起工作。
266      */
```

```
270  #if 1
271      /* 所以……这些设备是没救的。
272      我唯一能说的是
273      我们需要保留丑陋的代码来让它们开心。
274
275      它们应该被移动到一个更合理的状态，现在
276      它们使用 rebuild_header 而不是 hard_start_xmit！！！
277      此外，它们已经过时了
278      （有很多冗余克隆，没用），
279      我奇怪为什么人们认为它们能工作。
280      */
281      switch (dev->type) {
282          default:
283              break;
284              case ARPHRD_ROSE:
285          #if defined(CONFIG_AX) || (CONFIG_AX_MODULE)
286              case ARPHRD_AX:
287          #if defined(CONFIG_NET) || (CONFIG_NET_MODULE)
288              case ARPHRD_NET:
289  #endif
290              neighp->ops = &arp_broken_ops;
291              neighp->output = neighp->ops->output;
292              return 0;
293      #endif
294      ;}
295  #endif
296      if (neigh->type == RTN_MULTICAST) {
297          neigh->state = NUD_NARP;
298          arp_mc_map(addr, neigh->ha, dev, 1);
299      } else if (dev->flags& (IFF_NOARP|IFF_LOOPBACK)) {
300          neigh->state = NUD_NARP;
301          memcpy(neigh->ha, dev->addr, dev->addr_len);
302  } else if (neigh->type == RTN_BROADCAST || dev->flags&IFF_POPOINT) {
303     neigh->nud_state = NUD_ARP;
304     memcpy(neigh->ha, dev->broadcast, dev->addr_len);
305  }
306  if (dev->hard_header_cache)
307      neigh->ops = &arp_hh_ops;
308  else
309     neigh->ops = &arp_generic_ops;
310     if (neigh->nud_state&NUD_VALID) {
311         neigh->output = neigh->ops->connected_output;
312     else
313         neigh->output = neigh->ops->output;
314     }
315  return 0;
316 }
```

## 图 6.114 ARP错误报告：`linux/net/ipv4/arp.c`

```
319 static void arp_error_report(struct neighbour *neigh, struct sk_buff *skb) {

320

321     dst_link_failure(skb);

322     kfree_skb(skb);

323 }
```
