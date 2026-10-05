# Infrastructure Protocols 427

```
1209      return 0;
1210  }
1211
1212  static int ipgre_fb_tunnel_close(struct net_device *dev)
1213  {
1214      MOD_DEC_USE_COUNT;
1215      return 0;
1216      }
1217  #endif
1218
1219  int __init_ipgre_fb_tunnel_init(struct net_device *dev)
1220  {
1221      struct ip_tunnel *tunnel = (struct ip_tunnel*)dev->priv;
1222      struct ipphr *iphdr;
1223
1224      ipgre_tunnel_init_gen(dev);
1225  #ifdef MODULE
1226      dev->open       = ipgre_fb_tunnel_open;
1227      dev->stop       = ipgre_fb_tunnel_close;
1228  #endif
1229
1230      struct iphdr = #ipgre_fb_tunnel.parms.iphdr;
1231      iphdr->version  = 4;
1232      iphdr->protocol = IPPROTO_GRE;
1233      iphdr->hl        = 6;
1234      tunnel->hlen    = sizeof(struct iphdr) + 4;
1235
1236      dev_hold(dev);
1237      tunnels_vc[0]   = #ipgre_fb_tunnel;
1238      return 0;
1239  }
```

**Figure 6.319 GRE tunnels-protocol setup: linux/net/ipv4/ipgre.c.**

```
1242  static struct inet_protocol ipgre_protocol = {
1243      ipgre_rcv,      /* GRE handler      */
1244      ipgre_err,      /* TUNNEL error control  */
1245      0,             /* next             */
1246      IPPROTO_GRE,    /* protocol ID      */
1247      0,             /* copy             */
1248      NULL,           /* data             */
1249      "GRE",          /* name             */
1250  };
1251
1252  /*
1253   * And now the modules code and kernel interface.
1254  */
1255
1256  #ifdef MODULE
1257      int init_module(void)
1258  #else
1259      int __init_ipgre_init(void)
1260  #endif
```