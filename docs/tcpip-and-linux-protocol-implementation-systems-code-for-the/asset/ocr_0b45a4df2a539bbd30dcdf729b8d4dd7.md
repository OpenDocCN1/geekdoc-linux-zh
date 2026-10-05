# 406 TCP/IP and Linux Protocol Implementation

```
227
228   for (tp = ipgre_bucket(t); *tp = &(tp)->next) {
229      if (t == *tp) {
230          write_lock_bh(&ipgre_lock);
231          *tp = t->next;
232          write_unlock_bh(&ipgre_lock);
233          break;
234      }
235  }
236 }
```

# 6.287 GRE tunnels--locate hash entry: linux/net/ipv4/ip_gre.c

```
238   static struct ip_tunnel *ipgre_tunnel_locate(struct ip_tunnel_par *parms, int create)
239   {
240       u32 remote = parms->ip->daddr;
241       u32 local = parms->ip->daddr;
242       u32 key = parms->i_key;
243       struct ip_tunnel *t, *tp, *nt;
244       struct net_device *dev;
245       unsigned h h = HASH(key);
246       int prio = 0;
247
248       if (local) {
249          prio = 1;
250          if (remote && MULTICAST(remote)) {
251             prio = 2;
252             h = HASH(remote);
253          }
254          for (tp = &tunnels[prio][h]; *tp; tp = &(*tp)->next) {
255              if (local == t->parms.ip.daddr && remote == t->parms.ip.daddr) {
256                  if (key == t->parms.i_key)
257                      return t;
258              }
259          }
260      if (!create)
261          return NULL;
262  }
263  MOD_INC_USE_COUNT;
```

# 6.288 GRE tunnels--uninitialize and destroy entry: linux/net/ipv4/ip_gre.c

```
265   if (dev == NULL) {
266       MOD_DEC_USE_COUNT;
267       return NULL;
268   }
269   memset(dev, 0, sizeof(*dev) + sizeof(*tp));
270   dev->priv = (void*)(dev+1);
271   nt = (struct ip_tunnel*)dev->priv;
272   nt->dev = dev;
273   dev->init = ipgre_tunnel_init;
```