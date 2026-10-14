
```c
192 int ip_mc_output(struct skb_buff *skb)
193 {
194      struct sock *sk = skb->sk;
195      struct rtable *rt = (struct rtable*)skb->dst;
196      struct net_device *dev = rt->u.dev;

198
      /*
199       * 如果指定的接口处于启用并运行状态，则发送数据包。
200       */
201      IP_INC_STATS(IPOutRequests);
202      #ifdef CONFIG_IP_ROUTE_NAT
203      if (rt->flags & RTCF_NAT)
204          ip_do_nat(skb);
205
206      #endif

208      skb->dev = dev;
209      skb->protocol = __constant_htons(ETH_P_IP);

211
      /*
212       * 多播包将对其他本地用户进行环回
213       */
214      if ((rt->flags & RTCF_MULTICAST) && (IPCB(skb)->flags & IPSKB_FORWARDED)) || (info.inet.mc_loop)) {
215      #ifdef CONFIG_IP_MROUTE
216          /* 小优化优化：不对非本地帧进行环回，
217           这些帧在转发后返回；它们无论如何
218           会被 ip_mr_input 丢弃。
219          注意，本地帧被环回是为了传递给
220          本地接收者。
221
222          目前，此检查在 ip_mr_input 中是重复的。
223          */
224      if ((rt->flags & RTCF_NAT) || (IPCB(skb)->flags & IPSKB_FORWARDED)) {
225      #endif
226      {
227          struct sk_buff *newskb = skb_clone(skb, GFP_ATOMIC);
228          if (newskb) {
229              NF_HOOK(PF_INET, INET_IP_POST_ROUTING, newskb, NULL,
230              newskb->dev = dev;
231              ip_dev_loopback_xmit;
232          }
233      }
234  }
```

## 图 6.7 IP 输出-多播复制：`linux/net/ipv4/ip_output.c`。

```c
234      * ttl 为 0 的多播包不能超出主机 */

236      if (skb->skb_ip->ttl == 0) {
237          kfree_skb(skb);
238          return 0;
239      }
240  }

242      if (rt->rt_flags&RTCF_CAST) {
243          struct skb_buff *newskb = skb_clone(skb, GFP_ATOMIC);
244          if (newskb) {
245              NF_HOOK(NF_INET, NF_IP_POST_ROUTING, newskb, NULL,
246                          newskb->dev, ip_dev_loopback_xmit);
247          }
248      }
249      return ip_finish_output(skb);
250  }
```

## 图 6.8 IP 输出-发送队列：`linux/net/ipv4/ip_output.c`。

```c
252  int ip_output(struct sk_buff *skb)
253  {
254      #ifdef CONFIG_IP_ROUTE_NAT
255          struct rtable *rt = (struct rtable*)skb->dst;
256      #endif

258
259          IP_INC_STATS(IPOutRequests);
260      #ifdef CONFIG_IP_ROUTE_NAT
261          if (rt->rt_flags&RTCF_NAT)
262              ip_do_nat(skb);
263      #endif
264
265      return ip_finish_output(skb);
266  }
```

## 图 6.9 IP 输出-发送队列-部分 2：`linux/net/ipv4/ip_output.c`。

```c
268  /* 将数据包放入队列发送，必要时启动传输器。 */
269      * 此例程还需要计算总长度和
270      * 校验和。我们在两个阶段中使用
271      * header() 来处理，但这种方案在
272      * 路由时会产生混乱，
273      * 所以我们在这里处理，并且传输层
274      * 可能会是不可靠的（产生更多灾难）。这
275      * 在 Linux 下实现。
276      */
```

> 注：原文中268-276行内容存在乱码或重复，已根据上下文逻辑进行翻译

# TCP/IP 和 Linux 协议实现

```c
277  static inline ip_queue_xmit(struct sk_buff *skb)
278  {
279      struct sock *sk = skb->sk;
280      struct rtable *rt = (struct rtable*)skb->dst;
281      struct net_device *dev = rt->u.dev;
282      struct iphdr *iph = skb->iph;
283      dev = rt->u.dev;
284  /* 当传输层由于缓存路由而
285  * 路由到一个 MTU 不同的设备时，
286  * 必须处理它。 */
287  */
288  if (skb_headroom(skb) < dev->header_len && dev->header_len) {
289      struct skb_buff *skb2;
290      skb2 = skb_alloc_headroom(skb, dev->header_len + 15);
291          kfree_skb(skb);
292          if (skb2 == NULL)
293              return -OMEM;
294          if (skb2)
295              ip_select_owner(skb);
296              skb = skb2;
297      iph = skb2;
298  }
```

## 6.10 输出-发送队列-部分 2：`linux/net/ipv4/ip_output.c`。

```c
299  /* 如果路由失败，传输层将直到路由
300  * 出现时进行重传。 */
301  }
302  if (ip_output(rt, daddr, skb->saddr,
303  RT_TOS(skb->proto.af_inet.tos) | RTO_CONN | skb->localroute,
304  /* 路由时设置 DF 标志。 */
305  )
306  /* 
307  设置 标志 */
308      printk(KERN_DEBUG "sending packet too big to %s\n",
309  icmp_send(skb, ICMP_DEST_REACH, ICMP_FRAG_NEEDED,
310  htonl(rt->dst.mtu));
311      kfree_skb(skb);
312      return -EMSIZE;
313  }
314  ip_select_ident(skb, rt->dst);
315  return ip_fragment(skb);
316  }
```

## 6.11 发送队列包-部分 1：`linux/net/ipv4/ip_output.c`。
