# Infrastructure Protocols 389

```
257 if (register_net_device(dev) < 0)
258 goto failed;
259
260 dev_hold(dev);
261 ipip_tunnel_link(nt);
262 /* Do not decrement MOD_USE_COUNT here. */
263 return nt;
264
265 failed:
266
267 kfree(dev);
268 MOD_DEC_USE_COUNT;
269 return NULL;
270 }
```

6.259 IP in IP--uninitialize and destroy s tunnel: linux/net/ipv4/ipip.c.

```
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
285 } else {
286 ipip_tunnel_unlink((struct ip_tunnel*)dev->priv);
287 dev_put(dev);
288 }
289 }
```

# ICMP in IP in IP Tunnels

6.260 IP in IP–ICMP error handling: linux/net/ipv4/ipip.c.

```
291 void ipip_err(struct sk_buff *skb, unsigned char *dp, int len)
292 {
293 #ifdef I_WISH_WORLD_WERE_FECT
294
295 /* It is not :( All the routers (except for Linux) return only
296 8 bytes of packet payload. It means, that precise relaying of
297 ICMP in the real Internet is absolutely infeasible.
298 */
299 struct iphdr *iphdr = (struct iphdr)*dp;
300 int type = skb->h->icmph->type;
```