
```c
rth->u.output = ip_forward;
atomic_set(&rth->u.flags, 1);
rth->u.flags = DST_HOST;
if (dev->conf.policy)
    rth->u.dst.flags |= DST_NOPOLICY;
rth->fl14_dst = daddr;
rth->rt_dst = daddr;
rth->fl14_tos = tos;
#ifdef CONFIG_IP_ROUTE
rth->fl14_fmark = skb->fmark;
#endif
rth->fl14_src = saddr;
rth->rt_src = saddr;
#ifdef CONFIG_IP_ROUTE_NAT
rth->rt_dst_map = fl14_dst;
rth->rt_src_map = fl14_src;
#endif
#ifdef CONFIG_CLS_ROUTE
rth->u.dst.tclassid = itag;
#endif
```

目的设备是回环设备。输入接口设置为接收我们正尝试路由的数据包的网络接口。`dst_entry` 最重要的字段是函数指针，它设置为 `ip_local`。该函数将接收使用此条目的所有数据包。此外，如果路由标志为 `RTCF_LOCAL`，则识别出传入的数据包是本地消费的。

```c
rth->rt_iif = dev->index;
rth->u.dst.dev = &loopback_dev;
dev_hold(rth->u.dst.dev) = daddr;
rth->spec_dst = spec_dst;
rth->u.dst.input = ip_local;
rth->rt_flags = flags | RTCF_LOCAL;
```

如果没有 `no_route`，则 FIB 中的路由类型不可达，指示错误并丢失本地标签。

```c
if (res.type == RTN_REACHABLE) {
rth->u.dst.input = ip_error;
rth->dst.error = -err;
rth->rt_flags &= ~RTCF_LOCAL;
}
rth->rt_type = res.type;
goto intern;
```

如果 FIB 搜索我们尝试路由的目的不可达，则到达此标签 `no_route`。

```c
no_route:
rt_cache_stat[smp_processor_id()].in_no_route++;
spec_dst = inet_select_addr(dev, 0, RT_SCOPE_UNIVERSE);
res.type = RTN_REACHABLE;
goto local_input;
```

如果我们之前的 FIB 搜索显示目的地址是非法地址（Martian），我们记录相应的错误但不缓存。

```c
martian_destination:
rt_cache_stat[smp_processor_id()].in_martian_dst++;
#ifdef CONFIG_IP_ROUTE_VERBOSE
if (IN_DEV_LOG_MARTIANS(in_dev) && !net_ratelimit())
 printk(KERN_WARNING, "Martian destination %u.%u.%u from %u.%u.%u, dev %s\n",
 NIPQUAD(daddr), NIPQUAD(saddr), dev->name);
#endif
```

```c
#endif
e_invalid:
err = -EINVAL;
goto done;
```

```c
e_nobufs:
  err = -ENOBUFS;
goto done;
```

如果 FIB 搜索显示源地址是非法地址，我们也增加统计信息。RFC 1812 第 5.3 节提供了根据数据包接口验证源地址的可达性提示。这就是代码尝试记录 MAC 层头部信息。

```c
martian_source:
  RT_CACHE_STAT_INC(in_martian_src);
  #ifdef CONFIG_IP_ROUTE_VERBOSE
    if (IN_DEV_LOG_MARTIANS(in_dev) && net_ratelimit()) {
```

如果源地址是非法的，我们打印 MAC 地址。这就是源地址虚假的唯一指示。

```c
printk(KERN_WARNING "martian source %u.%u.%u from \n"
      NIPQUAD(daddr), UIPQUAD(saddr), dev->name);
if (dev->hard_header_len) {
  int i;
  unsigned char *p = skb->mac_raw;
  printk(KERN_WARNING "ill hard header: %s");
  for (i = 0; i < dev->hard_header_len; i++, p++) {
    printk("%02x",*p);
    if (i < (dev->hard_header_len - 1))
      printk(":");
  }
  printk("\n");
}
}
#endif
goto e_invalid;
```

# 9 路由输出包

在本节中，我们将讨论 IP 在传输之前如何为包选择路由。如果目的主机直接连接到发送主机，目的地址可以通过 ARP 或其他解析协议转换为链路地址，并可以在上面发送包。这似乎是一个相当简单的过程。然而，如果目的不可达，情况就不简单。如果发送主机上有多个设备，IP 协议必须选择一个输出接口。

在 UDP 发送数据报之前，它请求目的地的路由。然而，TCP 在发送数据包时已经建立了路由。无论传输 TCP 还是 UDP 包，定义在 `linux/route.h` 文件中的 `ip_route_connect` 都是解析输出包的主函数。

```c
static inline int ip_route_connect(struct rtable **rp,
	u32 daddr, u32 saddr,
	u32 tos, int oif, u8 protocol,
	u16 sort, u16 port, struct sock *sk)
```

与输入路由函数一样，早些检查的 `flow` 结构使用在路由缓存中执行许多路由的信息初始化。如果路由无法在缓存中匹配，它也用于 FIB 搜索。

```c
struct flowi fl = { .dif = oif,
	.nl_u = {.ip4_u = { .daddr = dst,
		.saddr = src,
		.tos = tos },
		.proto = protocol,
	.uli_u = {.ports = {
		.sport = sport,
		.dport = dport } } };
```

```c
int err;
if (!dst || !src) {
```

我们调用快速路径函数之一。之后，我们尝试更新缺失的源和目的地址。

```c
err = __ip_route_output_key(rp, &fl);
if (err) {
	return err;
	fl.fl4_dst = (*rp)->rt_dst;
	fl.fl4_src = (*rp)->rt_src;
	ip_route_output(*rp);
	*rp = NULL;
}
```

如果源地址和目的地址都已定义，我们传递 `sk` 中 `sock` 的指针。

```c
return ip_route_output_flow(rp, &fl, sk, 0);
```

如果协议值设置为 NAT 或其他非零数字，`ip_route_output_flow` 函数可以自动转换路由。

```c
int ip_route_output_flow(struct rtable **rp, struct flowi *flp, struct sock
*sk, int flags)
```

```c
int err;
```

我们在这里调用快速路由解析函数。

```c
if ((err == __ip_route_output_key(rp, flp)) != 0)
    return err;
```

如果我们找到了路由，且流（flow）中的信息不为零，我们尝试转换路由。

```c
return flp->proto ? xfrm_lookup(struct dst_entry**)rp, flp, sk, flags) : 0;
```

`ip_route_output_key` 是执行快速路径输出路由的函数。首先，它尝试在路由缓存（route cache）中查找匹配的路由。如果在缓存中找不到，它将尝试通过搜索 FIB（转发信息基础）来查找。如果找到精确匹配，该函数返回零；否则返回非零值。如果搜索成功，会将指向路由缓存条目的指针放在参数 `rp` 中。
