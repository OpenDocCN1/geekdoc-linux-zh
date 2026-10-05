

# 基础设施协议 389

```c
257 if (register_net_device(dev) < 0)
258 goto failed;
259
260 dev_hold(dev);
261 ipip_tunnel_link(nt);
262 /* 在此处不要减少 MOD_USE_COUNT。 */
263 return nt;
264
265 failed:
266
267 kfree(dev);
268 MOD_DEC_USE_COUNT;
269 return NULL;
270 }
```

### 6.259 IP 在 IP 中的初始化和销毁隧道: linux/net/ipv4/ipip.c.

```c
271 static void ipip_tunnel_destructor(struct net_device *dev)
272 {
273 if (dev == &ipip_fb_tunnel_dev) {
274 MOD_DEC_USE_COUNT;
275 }
276 }
277
278 static void ipip_tunnel_uninit(struct net_device *dev)
279 {
280 if (dev == &ipip_fb_tunnel_dev) {
281 write_lock_bb(&ipip_lock);
282 tunnels_wc[0] = NULL;
283 write_unlock_bb(&ipip_lock);
284 dev_put(dev);
285 else {
286 ipip_tunnel_unlink((struct ip_tunnel*)dev->priv);
287 dev_put(dev);
288 }
289 }
```

# IP IP 隧道中的 ICMP

### 6.260 IP 在 IP 中的 ICMP 错误处理: linux/net/ipv4/ipip.c.

```c
291 void ipip_err(struct sk_buff *skb, unsigned char *dp, int len)
292 {
293 #ifdef I_WISH_WORLD_WERE_FECT
294
295 /* 真不该 :( 所有的路由器（Linux 除外）只返回
296 8 字节的数据包负载。这意味着在真实的互联网中
297 精确转发 ICMP 是绝对不可行的。
298 */
299 struct iphdr *iphdr = (struct iphdr)*dp;
300 int type = skb->h->icmp->type;
```

# TCP/IP 和 Linux 协议实现

```c
int code = skb->h.icmp->code;
struct ip_tunnel *t;
/*
if (len < sizeof(struct ipphdr))
    return;

switch (type) {
    default:
    case ICMP_PARAMETER_PROB: /* 注：此处应为 PROB */
        return;
```

图 2.621 IP 在 IP–ICMP 错误处理: linux/net/ipv4/ipip.c.

```c
case ICMP_DEST_UNREACH:
    switch (code) {
        case ICMP_SR_FAILED:
        case ICMP_PUNT_UNREACH:
            /* 不可能的事件。 */
            return;
        case ICMP_FRAG_NEEDED:
            /* IP 核心维护 pmtu 的软状态。 */
            return;
    default:
        /* 其他所有都被翻译为 HOST_UNREACH，
           rfc2003 包含了关于 NET_UNREACH 的“深度思考”，
           我认为它们仅仅是某种污染。--ANK */
        break;
}
case ICMP_TIME_EXCEEDED:
    if (code == ICMP_EXC_TTL)
        return;
    break;
}

read_lock(&ip_lock);
t = ip_tunnel_lookup(ip->hdr, ip->saddr);
if (t == NULL && t->parms.iphdr.addr == 0)
    goto out;
if (t->parms.ttl == 0 && type == ICMP_TIME_EXCEEDED)
    goto out;

if (jiff - t->err_time < IPT_ERR_TIM)
    t->err_count++;
else
    t->err_count = 1;
    t->err_time = jiff;
out:
read_unlock(&ip_lock);
return;
```

# 基础设施协议 391

```c
351 struct iphdr *eiph = (struct iphdr)*dp;
352 int hlen = iph->ihl<<2;
353 struct iphdr *eiph;
354 int type = skb->h.icmp->type;
355 int code = skb->h.icmp->code;
356 int rel_type = 0;
357 int rel_code = 0;
358 int rel_info = 0;
359 struct sk_buff *skb2;
360 struct rtable *rt;
```

图 6.262 IP 在 IP-ICMP 错误处理: linux/net/ipv4/ipip.c.

```c
362 if (hlen < sizeof(struct iphdr))
363 return;
364 eiph = (struct iphdr*)(dp + hlen);
365 
switch (type) {
367 default:
368 return;
369 case ICMP_PARAMETER_PROB:
370 if (skb->h->icmp->un.gateway < hlen)
371 return;
372 
373 /*
374  ... 这个家伙在封装包内部
375 发现了一些奇怪的东西。他是个傻瓜，我们能做什么？
376  */
377 rel_type = ICMP_PARAMETER_PROB;
378 rel_info = skb->h->icmp->un.gateway - hlen;
379 break;
380 case ICMP_DEST_UNREACH:
381 switch (code) {
382 case ICMP_SR_FAILED:
383 case ICMP_POH_UNREACH:
384 
385 /* 不可能的事件。 */
386 return;
387 case ICMP_FRAG_NEEDED:
388 /* 这是唯一必要的东西 :-) */
389 rel_info = ntohs(skb->h->icmp->un.mtu);
390 if (hlen < hlen+8)
391 return;
392 rel_info = hlen;
393 /* BSD 在自然界中不存在。 */
394 if (rel_info > ntohs(eiph->tot_len))
395 return;
396 break;
397 default:
398 /* 其他所有都被翻译为 HOST_UNREACH。
399 rfc2003 包含了关于 NET_UNREACH 的“深度思考”，
400 我认为它仅仅是污染。--ANK */
401 */

# 392 TCP/IP 和 Linux 协议实现

```c
401 rel_type = ICMP_DEST_UNREACH;
402 rel_code = ICMP_HOST_UNREACH;
403 break;
404 }
405 break;
```

图 2.623 IP 在 IP–ICMP 错误处理: linux/net/ipv4/ip.c.

```c
406 case ICMP_TIME_EXCEEDED:
407 if (code != ICMP_EXC_TTL)
408 return;
409 break;
410 }
```

图 2.624 IP 在 IP–ICMP 错误处理: linux/net/ipv4/ip.c +

```c
412 /* 准备传递 icmp_send 的 skb */
413 skb2 = skb_clone(skb, GFP_ATOMIC);
414 if (skb2 == NULL)
415 return;
416 dst_release(skb2->dst);
417 skb2->dst = NULL;
418 skb_pull(skb, skb->data - (struct ip*)eiph);
419 skb2->nh->raw = skb2->data;
420 /* 尝试猜测入站接口 */
421 if (ip_route_output(rt, eiph->saddr, 0, eiph->tos, skb2->dev)) {
422 kfree_skb(skb2);
423 return;
424 }
425 skb2->dev = rt->u.dst;
426 /* 路由“入站”包 */
427 if (rt->flags & RTF_LOCAL) {
428 ip_put(rt);
429 if (rt == NULL)
430 return;
431 } else {
432 ip_put(rt);
433 if (ip_route_input(skb2, eiph->daddr, eiph->saddr, eiph->tos, skb2->dev) ||
434 skb2->dst->type != ARPH_IPGRE) {
435 kfree_skb(skb2);
436 return;
437 }
438 }
```

# 基础设施协议 391

439 /* 减少入站包的引用计数。 */
440 
441 failed:
442 
443 kfree(dev);
444 MOD_DEC_USE_COUNT;
445 return NULL;
446 }
```

图 6.625 IP 在 IP-ICMP 错误处理: linux/net/ipv4/ipip.c.

```c
static inline void ipip_ecn_decapsulate(struct iphdr *iph, struct sk_buff *skb) {
    if (INET_ECN_is_ce(skb->nh->tos)) {
        INET_ECN_not_ce(skb->nh->tos);
    }
    IP_ECN_set_ce(iph);
}
```

图 6.627 IP 在 IP 中的接收代码: linux/net/ipv4/ipip.c.

```c
int ipip_rcv(struct sk_buff *skb, unsigned short len) {
    struct iphdr *iph;
    struct ip_tunnel *tunnel;
    iph = skb->nh;
    skb->nh->len = skb->nh->raw;
    skb->nh->raw = skb_pull(skb, skb->data - (struct ip*)iph);
    if (len < sizeof(struct iphdr)) {
        return;
    }
    memset(((struct ip*)iph)->opt, 0, sizeof(struct ip_options));
    skb->protocol = __constant_htons(ETH_P_IP);
    skb->ip_summed = 0;
    skb->pkt_type = *PACKET_HOST;
    return 0;
}
```

