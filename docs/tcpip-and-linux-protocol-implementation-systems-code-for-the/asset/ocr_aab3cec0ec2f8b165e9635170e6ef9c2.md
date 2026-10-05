# TCP/IP and Linux Protocol Implementation

> Figure 6.257 IP in ip-tunnel: linux/net/ipv4/ipip.c.

```
208      struct ip_tunnel *ipip_tunnel_locate(struct ip_tunnel *parms, int create)
209      {
210          u32 remote = parms->iph.daddr;
211          u32 local = parms->iph.saddr;
212          struct ip_tunnel *t, **tp, *nt;
213          struct net_device *dev = dev;
214          unsigned char h = 0;
215          int prio = 0;
216
217          if (remote) {
218              prio = 2;
219              h = HASH(remote);
220          }
221          if (local) {
222              prio = 1;
223              h = HASH(local);
224          }
225          for (tp = tunnels[prio][h]; (t = *tp) != NULL; tp = t->next) {
226              if (local == t->parms->iph.saddr && remote == t->parms->iph.daddr)
227                  return t;
228          }
229          if (create) {
230              return NULL;
231
232              MOD_INC_USE_COUNT;
233              dev = kmalloc(sizeof(*dev) + sizeof(*t), GFP_KERNEL);
234              if (dev == NULL) {
235                  MOD_DEC_USE_COUNT;
236                  return NULL;
237              }
}
```

> Figure 6.258 IP in ip-locate a tunnel: linux/net/ipv4/ipip.c.

```
239      dev->priv = (void*)(dev+1);
240      nt = (struct ip_tunnel*)dev->priv;
241      nt->dev = dev;
242      dev->init = ipip_tunnel_init;
243      dev->features |= NETIF_F_DYNALLOC;
244      memcpy(nt->parms, parms, sizeof(*parms));
245      strncpy(dev->name, name, nt->parms.name);
246      if (dev->name[0] == 0) {
247          int i;
248          for (i=0; i<100; i++) {
249              sprintf(dev->name, "tun%d", i);
250              if (dev_get_by_name(dev->name) == NULL)
251                  break;
252          }
253          if (i==100)
254              goto failed;
255      memcpy(parms->name, dev->name, IFNAMSIZ);
256}
```