

# 图 6.176 IGMP 配置多播接口：linux/net/ipv4/igmp.c。

```c
128 static void ip_ma_put(struct ip_mc_list *im)
129 {
130 if (atomic_dec_and_test(im->refcnt)) {
131     in_dev_put(im->interface);
132     kfree(im);
133 }
134 }
```

## 管理状态的 IGMP 定器

# 图 6.177 IGMP 定器管理：linux/net/ipv4/igmp.c。

```c
142 static __inline_ void igmp_stop_timer(struct ip_mc_list *im)
143 {
144     spin_lock_bh(im->lock);
145     if (del_timer(im->timer)) {
146         atomic_dec(im->refcnt);
147         im->tm_running=0;
148         im->unsolicit_count=0;
149     spin_unlock_bh(im->lock);
150     }
151 }
152 
153     /* 必须在锁定 im->lock 的情况下调用 */
154 void igmp_start_timer(struct ip_mc_list *im, int max_delay)
155 {
156     int tv=rand() % max_delay;
157 
158     im->tm_running=1;
159     if (!mod_timer(im->timer, jiffies+tv+2)) {
160         atomic_dec(im->refcnt);
161     }
162 }
163 void igmp_mod_timer(struct ip_mc_list *im, int max_delay)
164 {
165     spin_lock_bh(im->lock);
166     im->unsolicit_count=0;
167     if (del_timer(im->timer)) {
168         if ((long)(im->timer->expires-jiffies) < max_delay) {
169             add_timer(im->timer);
170             im->tm_running=1;
171             spin_unlock_bh(im->lock);
172             return;
173         }
174         atomic_dec(im->refcnt);
175     }
176     igmp_start_timer(im, max_delay);
177     spin_unlock_bh(im->lock);
178 }
```

# 图 6.178 IGMP 定器超时：linux/net/ipv4/igmp.c。

```c
257 static void igmp_timer_expired(unsigned long data)
258 {
259     struct ip_mc_list *im=(struct mc_list*)data;
260     struct in_device *in_dev = im->interface;
261
262     int err;
263
264     spin_lock(&im->tm_lock);
265     im->tm_running=0;
266
267     if (IGMP_V1_SEEN(in_dev), im->multiaddr, IGMP_HOST_MEMBERSHIP_REPORT)
268         err = igmp_send_report(in_dev, im->multiaddr, IGMP_HOST_NEW_MEMBERSHIP_REPORT)
269     else
270         err = igmp_send_report(in_dev, im->multiaddr, IGMP_HOST_NEW_MEMBERSHIP_REPORT)
271
272     /* 失败了，稍后重试。 */
273     if (err) {
274         if (in_dev->dead)
275             igmp_start_timer(im, IGMP_Unsolicited_Report_Interval);
276             goto out;
277
278     }
279     if (im->unsolicit_count)
280         im->unsolicit_count--;
281         igmp_start_timer(im, IGMP_Unsolicited_Report_Interval);
282 }
283 out:
284     im->reporter = 1;
285     spin_unlock(&im->lock);
286     ip_ma_put(im);
287 }
```

## IGMP 传输

# 图 6.179 IGMP发送报告：linux/net/ipv4/igmp.c。

```c
185 #define IGMP_SIZE(sizeof(struct igmphdr)+sizeof(struct iphdr)) hook
186
187     /* 不要只处理 NO_BOOK skb->dst->output，以防 netfilter hook 
188      更改了路由; */
189 static inline int
190 output_may_reroute(struct skb *skb)
191 {
192     return skb->dst->output(skb);
193 }
194 static int igmp_send_report(struct net_device *dev, u32 group, int type)
195 {
196     struct sk_buff *skb;
197     struct iphdr *iph;
198     struct igmphdr *ih;
199     struct rtable *rt;
200     u32 dst;
201
202     /* 根据 IGMPv2 规范，LEAVE 消息
203     发送到所有路由器组。 */
204     */
205     dst = group;
206     if (type == IGMP_HOST_LEAVE_MESSAGE)
207     dst = IGMP_ALL_ROUTER;
208     if (ip_route_output(rt, dst, 0, dev->index))
209         return -1;
210     if (rt->t_src == 0) {
211         ip_rt_put(rt);
212         return -1;
213     }
214     skb=alloc_skb(IGMP_SIZE+dev->hard_header_len+15, GFP_ATOMIC);
215     if (skb == NULL) {
216         ip_rt_put(rt);
217         return -1;
218     }
# 图 6.180 IGMP发送报告：linux/net/ipv4/igmp.c。

```c
219     skb->dst = &rt->u.dst;
220     skb_reserve(skb, dev->hard_header_len+15);
221     iph = (struct iphdr*)skb_put(skb, sizeof(struct iphdr));
222     iph->version = 4;
223     iph->ihl = (sizeof(struct iphdr)>>2);
224     iph->tos = 0;
225     iph->frag_off = htons(IP_DF);
226     iph->ttl = 1;
227     iph->daddr = dst;
228     iph->addr = &rt->rt_src;
229     iph->protocol = IPPROTO_IGMP;
230     iph->tot_len = htons(IGMP_SIZE);
231     ip_select_id(iph, &rt->u.dst);
232     iph->check[0] = htons(RA);
233     iph->check[1] = 4;
234     iph->check[2] = 0;
235     iph->check[3] = 0;
236     ip_send_check(iph);
237     ih = (struct igmphdr*)skb_put(skb, sizeof(struct igmphdr));
238     ih->type = type;
239     ih->codes = 0;
240     ih->csum = 0;
241     ih->group = group;
242     ih->csum_compute((void *)ih, sizeof(struct igmphdr));
243     return NETHOOK(PF_INET, NF_IP_LOCAL_OUT, NULL, skb->dev,
244             output_maybe_reroute);
245 }
```

## IGMP 接收

# 图 6.181 IGMP接收：linux/net/ipv4/igmp.c。

```c
248 static void igmp_heard_report(struct in_device *dev, u32 group)
249 {
250     struct ip_mc_list *im;
251
252     /* 定器仅为非本地组设置 */
253     if (group == IGMP_ALL_HOSTS)
254         return;
255
256     read_lock(&in_dev->lock);
257     for (im=in_dev->mc_list; im!=NULL; im=im->next) {
258         if (im->multiaddr == group)
259             igmp_stop_timer(im);
260             break;
261     }
262     read_unlock(&in_dev->lock);
263 }
```

# 图 6.182 IGMP收到查询：linux/net/ipv4/igmp.c。

```c
267 static void igmp_heard_query(struct in_device *dev, unsigned char max_resp_time,
268         u32 group)
269 {
270     struct ip_mc_list *im;
271     int;
272
273     max_delay = max_resp_time*(HZ/IGMP_TIMER_SCALE);
274
275     if (max_resp_time == 0)
276         /* 遗憾，这里出现了旧路由器。 */
277             max_delay = IGMP_Query_Response_Interval;
278             in_dev->mr_seen = jiffies + IGMP_Router_Present_Timeout;
279             group = 0;
280 }
281
282      * 启动我们所有成员记录中的定器，
283      * 查询适用于查询到达的接口，
284      * 排除属于 
285      * “本地”组 (224.0.0.X) 的记录。
286      * 对于已经在运行的定器，检查它们是否需要
287      * 重置。
288      * 使用 igmp_code
289      * 字段
290      */
291     read_lock(&in_dev->lock);
292     for (im=in_dev->mc_list; im!=NULL; im=im->next) {
293         if (im->multiaddr != group)
294             continue;
295         if (group == IGMP_ALL_HOSTS)
296             continue;
297         igmp_mod_timer(im, max_delay);
298     }
299     read_unlock(&in_dev->lock);
300 }
```

img/06c1ba8be5c246339e218.png

```c
344 int igmp_rcv(struct sk_buff *skb, unsigned short len)
345 {
346     struct igmphdr *ih;
347     struct in_device *in_dev = skb_dev(skb);
348
349     if (in_dev == NULL) {
350         free_skb(skb);
351         return 0;
352     }
353
354     if (len < sizeof(struct igmphdr)) {
355         free_skb(skb);
356         return 0;
357     }
358
359     switch (ih->type) {
360         case IGMP_QUERY:
361             break;
362
363         case IGMP_HOST_MEMBERSHIP_REPORT:
364         case IGMP_HOST_NEW_MEMBERSHIP_REPORT:
365             break;
366
367         case IGMP_HOST_LEAVE_MESSAGE:
368             break;
369
370         default:
371             /* 未处理 */
372             break;
373     }
374     return 0;
375 }
```

## 6.5.2 管理组/接口

## 6.184 IGMP 接口添加和删除：linux/net/ipv4/igmp.c。

```c
398 static void ip_mc_filter_add(struct in_device *in_dev, u32 addr)
399 {
400     char *buf[MAX_ADDR_LEN];
401     struct net_device *dev = in_dev->dev;
402
403     /* 在这里检查 IFF_MULTICAST 是错误的、错误的、错误的。
404      当 IFF_MULTICAST 发生变化时，将会导致多播泄漏。
405      此检查应该在 dev->multicast_list 
406      例程中进行。某种操作如：
407      if (dev->flags&IFF_MULTICAST) {  do it; }
408      */
409
410     if (arp_mc_map(addr, buf, dev, 0) == 0)
411         dev_mc_add(dev,buf,dev->addr_len,0);
412 }
413
414 /*
415  从设备中移除过滤器
416  */
417
418 static void ip_mc_filter_del(struct in_device *in_dev, u32 addr)
419 {
420     char *buf[MAX_ADDR_LEN];
421     struct net_device *dev = in_dev->dev;
422
423     if (arp_mc_map(addr, buf, dev, 0) == 0)
424         dev_mc_delete(dev,buf,dev->addr_len,0);
425 }
```

