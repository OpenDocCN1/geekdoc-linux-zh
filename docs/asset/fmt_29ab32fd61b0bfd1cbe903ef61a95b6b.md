
### 图 6.163 ICMP 重定向：`linux/net/ipv4/icmp.c`。

```c
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

### 图 6.166 ICMP 回显：`linux/net/ipv4/icmp.c`。

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

## 328 TCP/IP 与 Linux 协议实现

### 图 6.169 ICMP 地址回复：`linux/net/ipv4/icmp.c`。

```c
/*
* RFC 1812 (4.3.3.9). 路由器应该监听所有回复，并在发现
* 不一致性时大声抱怨（报错）。
*/
static void icmp_address_reply(struct icmphdr *icmphdr, struct sk_buff *skb, int len)
{
    struct rtable *rt = (struct rtable*)skb->dev;
    struct net_device *dev = skb->dev;
    struct in_device *in_dev;
    struct if_addr *ifa;
    u32 mask;

    if (len < 4 || (rt->rt_flags&RTF_DIRECTSRC)) {
        return;
    }

    in_dev = in_dev->get(dev);
    if (in_dev) {
        read_lock(in_dev->lock);
        if (in_dev->ifa_list &&
            IN_DEV_LOG_MARTIANS(in_dev) &&
            IN_DEV_FORWARD(in_dev)) {
            mask = (u32*)icmphdr[1];
            for (ifa=in_dev->ifa_list; ifa; ifa=ifa->next) {
                if (mask == ifa->ifa_mask && inet_ifa_match(rt->rt_src, ifa)) {
                    break;
                }
            }
            printk(KERN_INFO "Wrong address %Xu.%Xu.%Xu.%Xu from %s/%Xu.%Xu.%Xu.%Xu\n",
                   NIPQUAD(in_dev), dev->name, NQUAD(rt->rt_src));
        }
        read_unlock(in_dev->lock);
        in_dev->put(in_dev);
    }
}
```

### 图 6.170 ICMP 丢弃：`linux/net/ipv4/icmp.c`。

```c
static void icmp_discard(struct icmphdr *icmphdr, struct sk_buff *skb, int len)
{
}
```

### 图 6.171 接收通用 ICMP 数据包：`linux/net/ipv4/icmp.c`。
