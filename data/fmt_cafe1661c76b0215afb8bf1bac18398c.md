
我印象 Cisco 可以实现类似的功能，

但这个功能在 IOS 中显然缺失了（@）。

1033 设置 10.66.66/24 和 fec0:6666:6666::0 作为虚拟网络

1034 使用 224.66.66.66。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1035

1036 `ping -t 255 224.66.66.66`

1037 mbone 没有响应。

1038

1040 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1041 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1042 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1043 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1044 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1045 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1046 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

1047 `ip tunnel add mode 224.66.66.66`。如果你有 mbone 的访问权限，可以跟我玩玩 :-

...（省略重复内容）...

312 GRE tunnels--broadcast support: `linux/net/ipv4/ip_gre.c` `linux/net/ipv4/ip_gre.c`。

...（省略重复内容）...

1078 <你的真实地址>

...（省略重复内容）...

`ipheader(struct net_device *dev)`

## 426 TCP/IP 和 Linux 协议实现

```c
struct rtable *rt;

if (!ip_route_output(&rt, ip->daddr, ip->saddr, RT_TOS(ip->tos), tunnel->parms.
link)) {
 tdev = rt->u.dst;
 ip_rt_put(rt);
}

dev->flags |= IFF_POINTTOPOINT;
#ifdef CONFIG_IPRE_BROADCAST
if (MULTICAST(ip->daddr)) {
 if (ip->saddr) {
 return -EINVAL;
dev->flags |= IFF_BROADCAST;
 dev->hard_header = ipre_header;
 dev->open = ipre_open;
 dev->stop = ipre_close;
}
}
#endif
if (tdev && tunnel->parms.link) {
 tdev = _dev_get_by_index(tunnel->parms.link);
}
if (tdev) {
 hlen = dev->hard_header_len;
 mtu = dev->mtu;
}
dev->ifflink = tunnel->parms.link;
/* 预计算 GRE 选项长度 */
if (tunnel->parms.o_flags&(GRE_CSUM|GRE_KEY|GRE_SEQ)) {
 if (tunnel->parms.o_flags&GRE_CSUM)
 addend += 4;
 if (tunnel->parms.o_flags&GRE_KEY)
 addend += 4;
 if (tunnel->parms.o_flags&GRE_SEQ)
 addend += 4;
}
dev->hard_header_len = hlen + addend;
dev->mtu = addend;
tunnel->hlen = addend;
return 0;
}
```

图 6.317 GRE隧道——隧道初始化：`linux/net/ipv4/ip_gre.c`。

图 6.318 GRE隧道——模块初始化：`linux/net/ipv4/ip_gre.c`。

```c
#ifdef MODULE
static int ipre_fb_tunnel_open(struct net_device *dev)
{
    MOD_INC_USE_COUNT;
****
```

## 基础设施协议 427

```c
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
1237      tunnels[0]   =ipgre_fb_tunnel;
1238      return 0;
1239  }
```

图 6.319 GRE隧道协议设置：`linux/net/ipv4/ipgre.c`。

```c
1242  static struct inet_protocol ipgre_protocol = {
1243      ipgre_rcv,      /* GRE处理器 */
1244      ipgre_err,      /* 隧道控制 */
1245      0,             /* 下一个 */
1246      IPPROTO_GRE,    /* 协议 ID */
1247      0,             /* 拷贝 */
1248      NULL,           /* 数据 */
1249      "GRE",          /* 名字 */
1250  };
1251  /*
1252  * 现在是模块代码和内核接口。
1253  */
1254
1255  #ifdef MODULE
1256      int init_module(void)
1257  #else
1258      int __init_ipgre_init(void)
```

##428 TCP/IP 和 Linux 协议实现

```c
1262     printk(KERN_INFO "GRE over IPv4 驱动\n");
1263 
1264     ipgre_fb_tunnel_dev.priv = (void*)&ipgre_tunnel;
1265   #ifdef MODULE
1266     register_netdev(&ipgre_fb_tunnel_dev);
1267   #else
1268     rtnl_lock();
1269     register_netdev(&ipgre_fb_tunnel_dev);
1270     rtnl_unlock();
1271   #endif
1272 
1273     inet_add_protocol(&ipgre_protocol);
1274     return 0;
1275 }
1276 #ifdef MODULE
```
