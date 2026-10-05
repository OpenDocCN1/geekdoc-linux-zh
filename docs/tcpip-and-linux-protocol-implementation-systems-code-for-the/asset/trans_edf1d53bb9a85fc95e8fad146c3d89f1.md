

## 32 TCP/IP 和 Linux 协议实现

```c
669   room = sizeof(struct iphdr) + icmp_param.replyopts.optlen;
670   room = sizeof(struct icphdr);
671
672 icmp_param.data_len=skb_in->tail-(u8*)iph);
673   if (icmp_param.data_len > room)
674     icmp_param.data_len = room;
675
676   ip_build_zmit(struct socket)->sk, icmp_glue_bits, &icmp_param,
677     icmp_param.data_len+sizeof(struct icphdr);
678     &ipc, rt, MSG_DONTWAIT);
680 ende:
681   ip_rt_put(rt);
682 out:
683   icmp_zmit_unlock();
684 }
```

## 正确处理不可达消息：

图 6.161 ICMP 不可达：linux/net/ipv4/icmp.

```c
687 /*
688  * 处理 ICMP_DEST_UNREACH, ICMP_TIME_EXCEED 和 ICMP_QUENCH。
689 */
691 static icmp_unreach(struct icphdr *icmp, struct sk_buff *skb, int len)
692 {
693   struct iphdr *iph;
694   int hash;
695   struct inet_protocol *iprotrot;
696   unsigned char *dp;
697   struct sock *raw_sk;
698
699   /*
700    头部不完整？
701    * 仅检查 IP 头部，应该对上层中更长的
702    *头部进行额外的检查。
703 */
705 if (len<sizeof(struct iphdr)) {
706   ICMP_INC_STATS_BH(IcmpInErrors);
707   return;
708 }
709
710 iph = (struct iphdr *)(icmp + 1);7711 dp = (unsigned char*)iph;
```

### 图 6.162 ICMP 不可达：linux/net/ipv4/icmp.c。

```c
if (icmp->type==ICMP_DEST_UNREACH) {
    switch (icmp->code & 15) {
        case ICMP_NET_UNREACH:
            break;
        case ICMP_HOST_UNREACH:
            break;
        case ICMP_PROTO_UNREACH:
            break;
        case ICMP_PORT_UNREACH:
            break;
        case ICMP_FRAG_NEEDED:
            if (ipv4_config.no_pmtu_disc) {
                if (net_ratelimit()) {
                    printk(KERN_INFO "ICMP: Xu.Xu.Xu.Xu: fragmentation\nneeded and DF set.\n",
                           NIPQUAD(iph->addr));
                }
            } else {
                unsigned short new_mtu;
                new_mtu = ip_rt_frag_needed(iph, ntohs(icmp->frag_mtu));
                if (new_mtu) {
                    return;
                }
                icmp->frag_mtu = htons(new_mtu);
            }
            break;
        case ICMP_SR_FAILED:
            if (net_ratelimit()) {
                printk(KERN_INFO "ICMP: Xu.Xu.Xu.Xu: Source Route Failed.\n\t\t\t\t                       NIPQUAD(iph->addr));
            }
            break;
        default:
            break;
    }
    if (icmp->code>NR_ICMP_UNREACH) {
        return;
    }
}
```

### 图 6.163 ICMP 不可达：linux/net/ipv4/icmp.c。

/*
* 向我们的底层层抛出
* RFC 1122: 3.2.2 必须从传递的头部中提取协议 ID。
* RFC 1122: 3.2.2 将 ICMP 不可达消息传递给传输层。
* RFC 1122: 3.2.2 将 ICMP 超时消息传递给传输层。
* 某些路由器发送错误的响应帧。如果你看到此消息，检查你的网络掩码是否匹配两端，让另一端修复。

```c
761 if (sysctl_icmp_bogus_error) {
762     if (ip_addr(iph->daddr) == RT_BROADCAST) {
763         if (net_ratelimit()) {
764             printk(KERN_WARNING "%u.%u.%u sent an invalid ICMP error to broadcast", NIPQUAD(iph->saddr));
765             return;
766     }
767 }
```

```c
/* 将 ICMP 消息传递到原始套接。有用吗？
查看 raw.c 和 net/raw.h, RAW_HTABLE_SIZE=INET_PROTS-1。 */
772 hash = iph->INET_PROTS - 1;
773 read_lock(&raw_v4_lock);
774 if ((raw_sk = raw_v4_htable[hash]) != NULL) {
775     while ((raw_sk = raw_v4_lookup(raw_sk, iph->protocol, iph->saddr, skb->dev->ifindex)) != NULL) {
776         raw_err(raw_sk, skb);
777         raw_sk = raw_sk->next;
778     }
779 }
780 read_unlock(&raw_v4_lock);
```

ICMP 不可达：linux/net/ipv4/icmp.c。

/* 在在我们执行时它不会改变。调用者已获得 BR_NETPROTO_LOCK 所以我们安全。 */
796 ipprot = (struct inet_protocol *)inet_protos[hash];
797 while (ipprot != NULL) {
798     struct inet_protocol *nextip;
799     nextip = (struct inet_protocol *)ipprot->nextip;
800     /* 将其传递给需要它的人。 */
801     if (iph->protocol == ipprot->protocol && ipprot->err_handler) {
802         ipprot->err_handler(skb, dp, len);
803     ipprot = nextip;
804 }

      struct iphdr *iph;
      unsigned long ip;

      if (len < sizeof(struct iphdr)) {
          ICMP_INC_STATS_BH(IcmpInErrors);
          return;
      }

      /* 获取导致重定向的数据包拷贝头部
      iph = (struct iphdr *) (iph + 1);
      ip = iph->daddr;

      switch(icmp->code & 7) {
          case ICMP_REDDIR_NET:
          case ICMP_REDDIR_NET:
              /* 根据 RFC 建议，现在作为主机重定向处理。 */
              case ICMP_REDDIR_HOST:
              case ICMP_REDDIR_HOST:
                  ip_rt_redirect(skb->nh.iph->saddr, ip, icmp->un->gateway, iph->saddr, iph->tos, skb->dev);
                  break;
          break;
  }
```

### 图 6.163 ICMP 重定向：linux/net/ipv4/icmp.c。

### 图 6.166 ICMP 回显：linux/net/ipv4/icmp.c。

```c
/*
 * 处理 ICMP_ECHO ("ping") 请求。
 * RFC 1122: 3.2.2.6 必须有一个回答 ICMP 回显请求的回显服务器。
 * RFC 1122: 3.2.2.6 ICMP_ECHO 请求中接收的数据必须包含在回复中。
 * RFC 1812: 4.3.3.6 应该有一个静默忽略回显请求的配置选项，必须有默认值。
 * 等完成并工作后，另查看 SRT 对选项的处理。
 */
```
static void icmp_echo(struct icmphdr *icmpph, struct sk_buff *skb, int len)
{
	if(syscall(icmp_echo,ignore_all)) {
	struct icmp_bzm icmp_param;
	struct timeval tv;
	__u32 times[3];

	/*
	do_gettimeday(&tv);
	times[1] = htonl(tv.tv_sec % 86400) * 1000 + tv.tv_usec / 1000;
	times[2] = htonl(times[1]); */
	icmp_param.iphh=&icmpph;
	icmp_param.type=ICMP_ECHPLY;
	icmp_param.code=0;
	icmp_param.data_ptr=&data;
	icmp_param.data_len=12;
	icmp_reply(&icmp_param, skb);
}
}
```

