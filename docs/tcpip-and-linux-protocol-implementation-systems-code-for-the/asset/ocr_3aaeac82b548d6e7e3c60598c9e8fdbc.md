# Protocol Implementation Framework 191

```
204 skb->len = 0;
205 skb->cloned = 0;
206
207 atomic_set(skb->users, 1);
208 atomic_set(skb->datarefp(skb), 1);
209 return skb;

211 nodata:
212 skb_head_to_pool(skb);
213 nobead
214 return NULL;
215 }
```

Figure 5.129 Initialize socket buffer: linux/net/core/skbuff.c.

```
218 /*
219 * Slab constructor for a skb head.
220 */
221 static inline void skb_headinit(void *skb, kmem_cache_t *cache,
222 unsigned long flags)
223 {
224 struct skb_buff *skb = p;
226 skb->next = NULL;
227 skb->prev = NULL;
228 skb->list = NULL;
229 skb->skb = NULL;
230 skb->stamp.tv_sec=0; /* No idea about time */
231 skb->dev = NULL;
232 skb->dst = NULL;
233 memset(skb->cb, 0, sizeof(skb->cb)); /* Default type */
234 skb->pkt_type = PACKET_HOST; /* Default type */
235 skb->ip_sum = 0;
236 skb->priority = 0;
237 skb->security = 0; /* By default packets are insecure */
238 skb->destructor = NULL;
239
240 #ifdef CONFIG_NETFILTER
241 skb->nfmark = skb->nfcache = 0;
242 skb->nfct = NULL;
243 #ifdef CONFIG_NETFILTER_DEBUG
244 skb->nf_debug = 0;
245 #endif
246 #endif
247 #ifdef CONFIG_NET_SCHED
248 skb->tc_index = 0;
249 #endif
250 }
```