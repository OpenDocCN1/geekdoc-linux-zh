

# TCP/IP 与 Linux 协议实现

```c
374 ip->saddr = rt->rt_src;
375 ip->daddr = rt->rt_dst;
376 skb->hh = ip;
377 /* 传输层处理 skb->foo 本体。 */
378
379 if(opt && opt->optlen) {
380 ip->ihl += opt->optlen >> 2;
381 ip_options_build(skb, NULL, sk->daddr, 0);
382
383 }
384
385 return NF_HOOK(IP_INET, NF_IP_LOCAL, NULL, NULL, rt->u.dst.dev);
386 ip_queue_xmit(2);
388
389 no_route:
390 IP_INC_STATS(IPOutNoRoutes);
391 kfree_skb(skb);
392 return -EHOSTREACH;
393 }
```

**图 6.13** IP 输出--经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
393 /*
394 构建并发送数据包，尽可能只拷贝一次
395 *
396 不关心 ip 选项... 偏移 0 的分片和其他分片的
397 选项长度可能不同。
398 *
399 注意偏移最大的分片首先发送，
400 这样 getfrag 例程可以在发送的最后一个分片中填充 TCP/UDP 校验和头部
401 字段... 实际上它也有助于
402 重组器，它们可以将大多数数据包放在分片队列的
403 头部，并且它们提前知道了总大小。这
404 最后一个特性在未来某天将显著提高 Linux 分片处理程序的性能。
405 *
406 *
407 回调函数有五个参数：一个任意指针（分片的拷贝），
408 源 IP 地址（可能取决于路由表）、
409 目的地址（char *）、要复制的偏移量以及
410 要复制的长度。
411 /*
413 static int ip_build_xmit_alloc(struct skb *sk,
414 getfrag(const void *,
415 char *,
416 unsigned int,
417 unsigned int),
418 const void *frag,
419 unsigned length,
420 struct ipcm_cookie *ipc,
421 struct rtable *rt,
422 {
423 int flag);
```

# 图 6.14 IP 输出-经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
424 unsigned int fraglen, maxfraglen, fragheaderlen;
425 int err;
426 int offset, mf;
427 int mtu;
428 u16 id = 0;
429
430 int hh_len = ((rt->u.dst.dev->hdr_header_len + 15) & ~15);
431 int nfragopt=opt=0;
432 struct ip_options *opt = ipc->opt;
433 int df = 0;
434
435 mtu = rt->u.dst.mtu;
436 if (ip_dont_fragment(sk, rt->u.dst))
437 df = htons(IP_DF);
439
440 length = sizeof(struct iphdr);
441
442 if (opt) {
443 fragheaderlen = sizeof(struct iphdr) + opt->optlen;
444 maxfraglen = ((mtu-sizeof(struct iphdr)-opt->optlen + 7) & ~7) + fragheaderlen;
445 else {
447 fragheaderlen = sizeof(struct iphdr);
448 Fraglen 是每个缓冲区的开销。现在
449 * 要发送的帧的大小。
450 */
451
452 maxfraglen = ((mtu-sizeof(struct iphdr)) & ~7) + fragheaderlen;
453 }
```

# 图 6.15 IP 输出-经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
455 if (length + fragheaderlen > 0xFFFF) {
456 ip_local_error(sk, EMSGSIZE, sk->rt_dst, mtu);
457 return -EMSGSIZE;
458 }
459
460 /*
461 通过处理剩余部分从帧的末尾开始。
462 *
463 */
464 offset = length - (length % (maxfraglen - fragheaderlen));
466
467 /*
468 为最后一个分片分配的内存量。
469 *
470
471 fraglen = length - offset + fragheaderlen;
472
473 if (length-offset==0) {

# TCP/IP 与 Linux 协议实现

```c
473 fraglen = maxfraglen;
474 offset = maxfraglen-fragheaderlen;
475 
476 /* 最后一个分片将不设置 MF。 */
478 */
479
480 mf = 0;
```

# 图 6.16 IP 输出--经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
483 /*
484 为路径 MTU 发现不分片。 */
485 */
487 if (offset > 0 && sk->proto->af_inet.pmudisc==PMTUDISC_DO) {
488 ip_local_error(sk, EMSGSIZE, rt->dst, mtu);
489 return -EMGSIZE;
490 }
491 if (flags&MSG_PROBE)
492 goto out;
```

## 6.2.2 分片

IP 输出遍历比 MTU 大的缓冲区并生成要发送的分片。

图 6.17 IP 输出--经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
494 /* 开始输出字节。 */
497
498 do {
499 char *data;
500 struct sk_buff *skb;
501
502 /* 获取留有对齐空间的内存。 */
505
506 skb = sock_alloc_send_skb(sk, fraglen+hh_len+15, 0, flags&MSG_DONTWAIT);
507 if (skb == NULL)
508 goto error;
509
510 /*
# 基础设施协议

```c
511 /* 填充控制结构 */
513 skb->priority = skb->priority;
514 skb->dst = dst_clone(rt->u.dst);
515 skb_reserve(skb, hh_len);
516 /*
517 找到从哪里开始放置字节 */
519 data = skb_put(skb, fraglen);
520 skb_iph = (struct iphdr*)data;
```

# 图 6.18 IP 输出-经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
525 /* 仅在非原始数据包上写入 IP 头部 */
528 {
529 struct iphdr *iph = (struct iphdr *)data;
530 iph->version = 4;
531 iph->ihl = 5;
532 if (opt) {
533 iph->ihl += opt->optlen>>2;
534 ip_options_build(skb, iph, rt, offset);
535 }
536 iph->tos = skb->protoinfo.af_inet_tos;
537 iph->tot_len = htons(fraglen - fragheaderlen + iph->ihl*4);
538 iph->frag_id = htons(offset>>3)|mf;
539 iph->id = id;
```

# 图 6.19 IP 输出-经典的 IP 数据包构建：linux/net/ipv4/ip_output.c。

```c
543 if (mf) {
544 if (offset || !df) {
545 /* 选择没有 DF 或已分片的
546 * 不可选择数据包 */
548 */
549 ip_select_ident(iph, rt->u.dst);
550 id = iph->id;
551 }
552 /* 任何后续分片将设置 MF。 */
554 */
555 mf = htons(IP_MF);
556 }
557 if (rt->type == RTM_MULTAST)
558 iph->tos = skb->protoinfo.af_inet_tos;
559 else
560 iph->tos = skb->protoinfo.af_inet_tos;
562 iph->protocol = skb->protocol;
563 iph->check = 0;
564 iph->saddr = rt->rt_src;
565 iph->daddr = rt->rt_dst;
566 iph->check = ipsum((unsigned char*)iph);
567 }

