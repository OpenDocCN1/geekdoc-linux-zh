
err_inv;

```c
err = -EINVAL;
failure:
  *errp = err;
if (fi) {
    fi->fib_dead = 1;
    free_fib_info(fi);
}
  return NULL;
```

# 查询 FIB 条目

图 8.45 FIB 语义——有意义的匹配？：`linux/net/ipv4/fib_semantics.c`。

```c
int
fib_semantic_match(int type, struct fib_info *fi, const struct rt_key *key, struct fib_result **res) {
  int err = fib->props[type].error;
  if (err == 0) {
    if (fi->fib_flags&RTNH_F_DEAD)
      return 1;
    *res = fi;
  }
  switch (type) {
  #ifdef CONFIG_IP_ROUTE
    case RTN_RESET:
      *res = fi;
      atomic_inc(&fi->fib_clref);
      return 0;
    case RTN_UNICAST:
    case RTN_LOCAL:
    case RTN_BROADCAST:
    case RTN_ANY:
    case RTN_MULTICAST:
      for_nexthops(fi, nh->flags&RTNH_F_DEAD) {
        continue;
        if (key->oif || key->oif == nh->oif)
          break;
      }
    }
  #endif
}
```

# 访问 FIB 统计信息

图 8.46 FIB 语义——有意义的匹配？：`linux/net/ipv4/fib_semantics.c`。

```c
#ifdef CONFIG_IP_ROUTE_MULTIPATH
if (fi->fib_nh > 1) {
  *res = fi;
  atomic_inc(&fi->fib_clref);
  return 0;
} else
if (nh < 1) {
  atomic_inc(&fi->fib_clref);
  return 0;
}
#endif
end_nexthops(fi);
*res = NULL;
return 1;
default:
*res = NULL;
printk(KERN_DEBUG "impossible\n");
return -EINVAL;
}
```

图 8.47 FIB 语义--dump：`linux/net/ipv4/fib_semantics.c`。

```c
/* 查找到目的地的源地址 */
u32 __fib_res_pref(struct fib_result *res)
{ return inet_select_addr(FIB_RES_DEV(res), FIB_RES_GW(res), res->scope);
}
```

图 8.48 FIB 语义--dump ii：`linux/net/ipv4/fib_semantics.c`。

```c
int;
fib_dump_info(struct sk_buff *skb, u32 pid, u32 seq, int event,
  u8 table_id, u8 type, u8 dst_len, u8 tos,
  struct fib_info *fi)
{
  struct rmsg *rtg;
  struct nlmsghdr *nlb;
  unsigned char *b = skb->tail;
```

```c
nhb = NLMSG_PUT(skb, pid, seq, sizeof(struct rmsg));
rtm = NLMSG_DATA(nhb);
rtm->rtm_family = AF_INET;
rtm->rtm_dest = dst_len;
rtm->rtm_src = 0;
rtm->rtm_tos = tos;
rtm->rtm_table = table_id;
rtm->rtm_type = type;
rtm->rtm_flags = fi->fib_flags;
rtm->rtm_scope = scope;
if (rtm->rtm_dst_len)
  RTM_PUT(skb, RTA_DST, 4);
rtm->rtm_protocol = fi->fib_protocol;
if (fi->fib_priority)
  RTM_PUT(skb, RTA_PRIORITY, 4, &fi->fib_priority);
#ifdef CONFIG_NET_CLS_ROUTE
  if (fi->fib_nh(0)->nh_classid)
    RTM_PUT(skb, RTA_FLOW, 4, &fi->fib_nh(0)->classid);
#endif
if (rtnetlink_put_metrics(skb, fi->fib_metrics) < 0)
  goto rtattr_failure;
if (fi->fib_presrc)
  RTM_PUT(skb, RTA_PRESRC, 4, &fi->fib_presrc);
if (fi->fib_nh->nh_oif)
  RTM_PUT(skb, RTA_GATEWAY, 4, &fi->fib_nh->nh_gw);
if (fi->fib_nh->nh_oif)
  RTM_PUT(skb, RTA_OIF, sizeof(int), &fi->fib_nh->nh_oif);
```

图 8.49 fib 语义-dump iii：`linux/net/ipv4/fib_semantics.c`。

```c
#ifdef CONFIG_IP_ROUTE_MULTIPATH
if (fi->fib_nh > 1) {
  struct rt_nexthop *nmp;
  struct rtattr *mp_head;
  if (skb_tailroom(skb) < RTA_ALIGN(0))
    goto rtattr_failure;
  mp_head = (struct rtattr*)skb_put(skb, RTA_SPACE(0));
  for (...)
    if (skb_tailroom(skb) < RTA_ALIGN(RTA_ALIGN(sizeof(*nmp)) + 4))
      goto rtattr_failure;
    nmp = (struct rt_nexthop*)skb_put(skb, RTA_ALIGN(sizeof(*nmp)));
    nmp->rtnh_flags = nh->nh_flags & 0xFF;
    nmp->rtnh_bops = nh->nh_weight-1;
    nmp->rtnh_ifindex = nh->nh_oif;
    if (nmp->rtnh_nh_go)
      RTM_PUT(skb, RTA_GATEWAY, 4, &nh->nh_gw);
    nmp->rtnh_len = skb->tail - (unsigned char*)nmp;
  }
endif_next(fi);
```

# TCP/IP 与 Linux 协议实现

```c
688      mp_head->rta_type = RTA_MULTIPATH;
689      mp_head->rta_len = skb->tail - (u8*)mp_head;
690  }
691  #endif
692  nlh->nlmsg_len = skb->tail - b;
693      return skb->len;
694
695  nlmsg_failure:
696  rtattfr_failure:
697      skb_trim(skb, b - skb->data);
698      return -1;
699  }
```

# 获取 RTNlink 请求

![](img/06c11ba8be5c1c24aa633e12618e2ebd_637_0.png)
