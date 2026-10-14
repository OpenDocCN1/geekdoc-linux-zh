
```c
418         int nhs = 1;
419     else
420         const int nhs = 1;
421     #endif
422
423     /* 快速检查以捕获最异常的情况 */
424     if (fi->probes[rtmsg->rtm_type].scope > rta->rta_scope)
425         goto err_inv;
426
428     #ifdef CONFIG_IP_ROUTE_MULTIPATH
429         if (rta->rta_mp)
430             nhs = fib_count_nexthops(rta->rta_mp);
431             if (nhs == 0)
432                 goto err_inv;
433         }
434     #endif
```

图 8.41 FIB 语义——创建 FIB 条目 i：`linux/net/ipv4/fib_semantics.c`。

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
```

# 路由 575

```c
458
459   }
460
461     memcpy(fi->fib_pref, rta->rta_pref, 4);
```

图 8.42 FIB 语义--FIB 条目 ii：`linux/net/ipv4/fib_semantics.c`。

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

图 8.43 FIB 语义——创建 FIB 条目 iii：`linux/net/ipv4/fib_semantics.c`。

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

图 8.44 FIB 语义——创建 FIB 条目 iv：`linux/net/ipv4/fib_semantics.c`。

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
```
