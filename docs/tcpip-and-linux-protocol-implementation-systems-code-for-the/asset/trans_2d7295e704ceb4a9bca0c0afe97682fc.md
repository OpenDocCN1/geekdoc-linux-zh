

## 288 TCP/IP 和 Linux 协议实现

图 6.108 ARP 邻居操作：linux/net/ipv4/arp.c。

```
160 static struct neigh_ops arp_direct_ops = =
161 {
162     AF_INET,
163     NULL,
164     NULL,
165     NULL,
166     dev_queue_xmit,
167     dev_queue_xmit,
168     dev_queue_xmit,
169     dev_queue_xmit,
170 };
171 struct neigh_ops arp_broken_ops = =
172 {
173     AF_INET,
174     NULL,
175     arp_solicit,
176     arp_error_report,
177     neigh_compat_output,
178     neigh_compat_output,
179     dev_queue_xmit,
180     dev_queue_xmit,
181 };
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_343_0.png)

图 6.109 ARP 表结构：linux/net/ipv4/arp.c。

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

图 6.110 ARP 映射 MAC-类型/IEEE-类型：linux/net/ipv4/arp.c。

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

## 图 6.111 ARP 哈希函数：linux/net/ipv4/arp.c。

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

## 图 6.112 ARP 条条目：linux/net/ipv4/arp.c。

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
## 图 6.113 ARP 构建条目：linux/net/ipv4/arp.c。

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
298          neigh->state = NUD_NARP;
299          arp_mc_map(addr, neigh->ha, dev, 1);
300      } else if (dev->flags& (IFF_NOARP|IFF_LOOPBACK)) {
301          neigh->state = NUD_NARP;
302          memcpy(neigh->ha, dev->addr, dev->addr_len);
303  } else if (neigh->type == RTN_BROADCAST || dev->flags&IFF_POPOINT) {
304     neigh->nud_state = NUD_ARP;
305     memcpy(neigh->ha, dev->broadcast, dev->addr_len);
306  }
307  if (dev->hard_header_cache)
308      neigh->ops = &arp_hh_ops;
309  else
310     neigh->ops = &arp_generic_ops;
311     if (neigh->nud_state&NUD_VALID) {
312         neigh->output = neigh->ops->connected_output;
313     else
314         neigh->output = neigh->ops->output;
315     }
316  return 0;
317 }

## 图 6.114 ARP错误报告：linux/net/ipv4/arp.c。

```
319 static void arp_error_report(struct neighbour *neigh, struct sk_buff *skb) {
320
321     dst_link_failure(skb);
322     kfree_skb(skb);
323 }
```

## ARP 请求

## 图 6.115 ARP 请求（谁有）：linux/net/ipv4/arp.c。

```
325 static void arp_solicit(struct neighbour *neigh, struct sk_buff *skb) {
326
327     u32 saddr;
328     u8 *dst_ha = NULL;
329     struct net_device *dev = neigh->dev;
330     u32 target = (*u32*)neigh->primary_key;
331     int probes = atomic_read(&neigh->probes);
332
333     if (skb && int_addr_state(skb->neigh->saddr) == RTN_LOCAL) {
334         saddr = skb->neigh->saddr;
335     else
336         saddr = inet_select_addr(dev, target, RT_SCOPE_LINK);
337
338     if ((probes -= neigh->parms->ucast_probes) < 0) {
339         if ((neigh->nud_state&NUD_VALID)) {
340             print(KERN_DEBUG "在 INVALID 状态下尝试 uast 探测");
341             dst_ha = neigh->ha;
342             read_lock(&neigh->lock);
343         } else if (probes -= neigh->parms->ucast_probes) < 0) {
344             #ifdef CONFIG_ARPP
345             neigh_alloc(neigh);
346 #endif
347             return;
348         }
349     arp_send(ARP_REQUEST, ETH_ARP, dev, saddr,
350             dst_ha, dev->addr, NULL);
351
352     if (dst_ha)
353         read_unlock(&neigh->lock);
354 }
```

## 图 6.116 ARP 内置过期：linux/net/ipv4/arp.c。

```
356 /* 过期函数 */
357 /* 在缓存中查找 ARP 映射。如果未找到，发送请求。
358 * 这是一个丑陋的例程：它没有使用 skb->dst，
359 * 即使它存在。假设 skb->dev 被虚拟设备篡改了。
360 只有损坏的设备可以使用此函数，它已被计划移除。
361 */
362 static int arp_set_predefined(int addr_hint, unsigned char *haddr, u32 paddr, struct net_device *dev)
363
364 switch (addr_hint) {
365     case RTN_LOCAL:
366         printk(KERN_DEBUG "ARP: 为自己的地址调用");
367         memcpy(haddr, dev->addr, dev->addr_len);
368         return 1;
369     case RTN_MULTICAST:
370         arp_mc_map(paddr, haddr, dev, 1);
371         return 1;
372     case RTN_BROADCAST:
373         memcpy(haddr, dev->broadcast, dev->addr_len);
374         return 1;
375 }
376 return 0;

377 int arp_find(unsigned char *haddr, struct sk_buff *skb) {
378     struct net_device *dev = skb->dev;
379     u32 paddr;
380     struct neighbour *neigh;
381
382     if (!skb->dst) {
383         printk(KERN_DEBUG "arp_find 被调用时 dst=NULL");
384         kfree_skb(skb);
385         return 1;
386     }
387     paddr = ((struct rtable*)skb->dst)->rt_gateway;
388
389     if (arp_preset(inet_addr_type(paddr), haddr, paddr, dev)) {
390         return 0;
391     }
392     n = _neigh_lookup(arp_tbl, paddr, dev, 1);
393
394     if (n) {
395         n->used = jiffies;
396         if (n->ud_state==NUD_VALID && neigh_event_send(n, skb) == 0) {
397             read_lock(n->lock);
398             memcpy(haddr, n->dev, n->addr_len);
399             read_unlock(n->lock);
400             neigh_release(n);
401             return 0;
402         }
403         else
404             kfree_skb(skb);
405             return 1;
406     }
407 }
408 /* 过期函数结束 */
```

## 图 6.118 ARP – 将地址绑定到邻居：linux/net/ipv4/arp.c。

```
421 int arp_bind_neigh(struct dst_entry *dst)
422 {
423 struct net_device *dev = dst->dev;
424 struct neighbour *n = dst->neighbour;
426 if (dev == NULL) {
427 return -EINVAL;
428 }
429 u32 nexthop=((struct rtable*)dst)->rt_gateway;
430 if (dev->flags & (IFF_LOOPBACK|IFF_POINTPOINT)) {
431 nexthop = 0;
432 n = _neigh_lookup_errno(dev);
433 #ifndef CONFIG_ATM_ATM
435 dev->type == ARPHRD_ATM ? &clip_tbl : &arp_tbl, nexthop, dev);
436 #endif
```
