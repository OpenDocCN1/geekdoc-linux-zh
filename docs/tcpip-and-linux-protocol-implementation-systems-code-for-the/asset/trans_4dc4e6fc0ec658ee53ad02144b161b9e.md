

# 路由 575

```c
if (inet_addr_type(nh->nh_gw) != RTN_UNICAST)
    return -EINVAL;
if ((dev->dev_get_by_index(nh->nh_oif)) == NULL)
    return -ENODEV;
if (!(dev->flags&IFF_UP))
    return -NETDOWN;
nh->nh_dev = dev;
atomic_inc(&dev->refcnt);
h->nh_scope = RT_SCOPE_LINK;
return 0;
```

```c
memset(&key, 0, sizeof(key));
key.dst = nh->nh_gw;
key.oif = nh->nh_oif;
key.scope = r->rtm_scope + 1;
```

### 8.39 FIB 语义——检查下一跳：linux/net/ipv4/fib_semantics.c

```c
* 这并不是必须的，但需要稍微思考 /
if (key.scope < RT_SCOPE_LINK)
    key.scope = RT_SCOPE_LINK;

if ((err = fib_lookup(&key, &res)) != 0)
    return err;
    nh->nh_scope = res.scope;
    nh->nh_oif = FIB_RES_DEV(res);
    nh->nh_dev = FIB_RES_DEV(res);
    if (nh->nh_dev)
        atomic_inc(&nh->nh_dev->refcnt);
    fib_res_put(&res);
else {
    struct device *in_dev;
    if (nh->nh_flags&(RTNH_F_PERVASIVE|RTNH_F_ONLINK))
        return -EINVAL;
    in_dev = inet_dev_get_by_index(nh->nh_oif);
    if (!in_dev)
        return -ENODEV;
    if (!(in_dev->dev->flags&IFF_UP))
        in_dev_put(in_dev);
        return -ENETEDOWN;
    nh->nh_dev = in_dev;
    atomic_inc(&nh->nh_dev->refcnt);
    nh->nh_scope = RT_SCOPE_HOST;
    in_dev_put(in_dev);
}
```

# TCP/IP 与 Linux 协议实现

# 创建新的 FIB 条目

图 8.40 FIB 语义——创建 FIB 条目 i：linux/net/ipv4/fib_semantics.c。

```c
410 struct fib_info *
411 fib_create_info(const struct rtm_msg *rtmsg, struct kern_rta,
412                    const struct nlmsghdr *nlh, int *errp)
413 {
414     int err = err;
415     struct fib_info *fi = NULL;
416     struct fib_info *ofi;
417     #ifdef CONFIG_IP_ROUTE_MULTIPATH
418         int nhs = 1;
419     else
420         const int nhs = 1;
421     #endif
422
423     /* 快速检查以捕获最异常的情况 */
424     if (fi->probes[rtmsg->rtm_type].scope > rta->rta_scope)
425         goto err_inv;
426
427
428
     #ifdef CONFIG_IP_ROUTE_MULTIPATH
429         if (rta->rta_mp)
430             nhs = fib_count_nexthops(rta->rta_mp);
431             if (nhs == 0)
432                 goto err_inv;
433         }
434     #endif
```

图 8.41 FIB 语义——创建 FIB 条目 i：linux/net/ipv4/fib_semantics.c。

```c
435 fi = kmalloc(sizeof(*fi)+nhs*sizeof(struct fib_nh), GFP_KERNEL);
436 err = -ENOMEM;
437 if (fi == NULL)
438     goto failure;
439 fib_info_cnt *cnt = NULL;
440 memset(fi, 0, sizeof(*fi)+nhs*sizeof(struct fib_nh));
441
442 fi->protocol = rta->rta_protocol;
443 fi->fib_nh = nhs;
444 fi->flags = rta->rta_flags;
445 if (rta->rta_priority)
446     fi->fib_priority = rta->rta_priority;
447 if (rta->rta_mx)
448     int attrien = RTA_PAYLOAD(rta->rta_mx);
449     struct rattr *attr = RTA_DATA(rta->rta_mx);
450
451     while (RTA_OK(attr, attrien)) {
452         unsigned flavor = attr->rta_type;
453         if (flavor)
454             if (flavor == RTA_MAX)
455                 goto err_inv;
456             fi->metrics[flavor-1] = (unsigned*)RTA_DATA(attr);
457     }
```

# 路由 575

```c
458
459   }
460
461     memcpy(fi->fib_pref, rta->rta_pref, 4);
```

图 8.42 FIB 语义--FIB 条目 ii：linux/net/ipv4/fib_semantics.c。

```c
if (rta->rta_mp) {
  #ifdef CONFIG_IP_ROUTE_MULTIPATH
    if ((err = fib_get_nexthops(fi, rta->rta_mp)) != 0) {
      goto failures;
    }
    if (rta->rta_nh && fi->fib_nh->oif != *rta->rta_oif) {
      goto err_inv;
    }
    if (rta->rta_gw && fi->fib_nh->gw, rta->rta_gw) {
      goto err_inv;
    }
  #ifdef CONFIG_NET_CLS_ROUTE
    if (rta->rta_flow && fi->fib_nh->classid, rta->rta_flow) {
      goto err_inv;
    }
  #endif
  else
    goto err_inv;
  #endif
} else {
  struct fib_nh *nh = fi->fib_nh;
  if (rta->rta_oif != *rta->rta_oif) {
    memcpy(fi->fib_nh->gw, rta->rta_gw, 4);
  }
  #ifdef CONFIG_NET_CLS_ROUTE
    if (rta->rta_flow) {
      memcpy(fi->fib_nh->classid, rta->rta_flow, 4);
    }
  #endif
  nh->nh_flags = rta->rtm_flags;
  #ifdef CONFIG_IP_ROUTE_MULTIPATH
    nh->nh_weight = 1;
  #endif
}
  #ifdef CONFIG_IP_ROUTE_NAT
  if (rta->rtm_type == RTM_NAT) {
    if (rta->rta_gw || !rta->rta_oif) {
      goto err_inv;
      memcpy(fi->fib_nh->gw, rta->rta_gw, 4);
    }
    goto link_idx;
  #endif
if (fib->props[rta->rtm_type].error) {
  if (rta->rta_gw || rta->rta_oif || rta->rta_mp) {
    goto err_inv;
  }
  goto link_idx;
}
```

# 758 TCP/IP 与 Linux 协议实现

图 8.43 FIB 语义——创建 FIB 条目 iii：linux/net/ipv4/fib_semantics.c。

```c
if (rta->rtm_scope == RT_SCOPE_HOST)
    goto err_inv;

if (rta->rtm_scope == RT_SCOPE_HOST) {
    struct fib_nh *nh = fi->fib_nh;

    /* 添加了本地地址 */
    if (nh == NULL || nh->nh_gw)
        goto err_inv;
    nh->nh_scope = RT_SCOPE_HOST;
    nh->nh_dev = dev_get_by_index(fi->fib_nh->nh_oif);
    err = -ENODEV;
    if (nh->nh_dev == NULL)
        goto failure;
} else {
    change_nexthops(fi);
    if ((err = fib_check_nh(rta, fi)) != 0)
        goto failure;
    end_nexthops(fi);
}

if (rta->rtm_type == RTN_LOCAL || rta->rta_dst == NULL)
    memcmp(fi->fib_presrc, rta->rta_dst, 4);
    if (inet_addr_type(fi->fib_presrc) != RTN_LOCAL)
        goto err_inv;
```

图 8.44 FIB 语义——创建 FIB 条目 iv：linux/net/ipv4/fib_semantics.c。

```c
link_it:
    if ((ofi = fib_find_info(fi)) != NULL) {
        fi->fib_dead = 1;
        free_fib_info(fi);
        ofi->fib_treeref++;
        return ofi;
    }

    fi->fib_treeref++;
    atomic_inc(&fi->fib_clref);
    write_lock(&fi->fib_info_lock);
    fi->fib_next = fib_info_list;
    fi->fib_prev = NULL;
    if (fib_info_list)
        fib_info_list->fib_prev = fi;
    fib_info_list = fi;
    write_unlock(&fi->fib_info_lock);
    return fi;

err_inv;
```

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

图 8.45 FIB 语义——有意义的匹配？：linux/net/ipv4/fib_semantics.c。

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

图 8.46 FIB 语义——有意义的匹配？：linux/net/ipv4/fib_semantics.c。

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

图 8.47 FIB 语义--dump：linux/net/ipv4/fib_semantics.c。

```c
/* 查找到目的地的源地址 */
u32 __fib_res_pref(struct fib_result *res)
{ return inet_select_addr(FIB_RES_DEV(res), FIB_RES_GW(res), res->scope);
}
```

图 8.48 FIB 语义--dump ii：linux/net/ipv4/fib_semantics.c。

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

图 8.49 fib 语义-dump iii：linux/net/ipv4/fib_semantics.c。

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
```

