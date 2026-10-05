# 850 TCP/IP and Linux Protocol Implementation

```
234 { 
235     struct teql_sched_data *q = (void*)dev->qdisc-date;
236     struct neighbour *nm = skb->dst->neighbour;
237     struct neighbour *n = q->ncache;
238 
239     if (nm->tbl == NULL)
240         return -EINVAL;
241     if (n && k & n->tbl == nm->tbl &&
242         memcmp(n->primary_key, nm->primary_key, n->tbl->key_len) == 0) {
243             atomic_inc(&n->refcnt);
244         } else {
245             n = _neigh_lookup_errno(nm->tbl, nm->primary_key, dev);
246             if (IS_ERR(n))
247                 return PTR_ERR(n);
248             }
249             if (neigh_event_send(n, skb_res) == 0) {
250                 int err;
251                 read_lock(&n->lock);
252                 err = dev->hard_header(skb, dev, ntohs(skb->protocol), n->ha, NULL, skb->len);
253                 read_unlock(&n->lock);
254                 if (err < 0) {
255                     neigh_release(n);
256                     return -EINVAL;
257                 }
258                 teql_neigh_release(xchg(&q->ncache, nache));
259                 return 0;
260             }
261         }
262     neigh_release(n);
263     return (skb_res == NULL) ? -EAGAIN : 1;
264 }
265 static __inline_int
266 teql_resolve(struct skb_buff *skb, struct skb, struct skb_res, struct net_device *dev)
267 {
268     if (dev->hard_header == NULL ||
269         skb->dst == NULL ||
270         skb->dst->neighbour == NULL)
271         return 0;
272     return teql_resolve(skb, skb_res, dev);
273 }
```

Figure 9.304 TE net device transmit: linux/net/sched/sch_teql.c.

```
275 static int teql_master_xit(struct skb_buff *skb, struct skb, struct net_device *dev)
276 {
277     struct teql_master *master = (void*)dev->priv;
278     struct qdisc *start, *q;
279     int busy;
280     int nores;
281     int len = skb->len;
282     struct skb_buff *skb_res = NULL;
283 
284     start = master->slaves;
```