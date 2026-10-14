
# 50 TCP/IP 和 Linux 协议实现

```c
void free_fib_info(struct fib_info *fi)
{
    if (fi->dead == 0) {
        printf("Freeing alive fib_info %p\n", fi);
        return;
    }
    change_nexthops(fi);
    if (nh->nh_dev) {
        dev_put(nh->nh_dev);
        nh->nh_dev = NULL;
    }
    end_nexthops(fi);
    fib_info->cnt--;
    kfree(fi);
}
```

```c
void free_fib_release_info(struct fib_info *fi)
{
    write_lock(&fib_info->lock);
    if (fi && --fi->fib_treeref == 0) {
        if (fi->fib_next) {
            fi->fib_next->fib_prev = fi->fib_prev;
            fi->fib_prev->fib_next = fi->fib_next;
            if (fi == fib_info_list) {
                fib_info_list = fi->fib_next;
                fi->fib_dead = 1;
                fib_info_put(fi);
            }
        }
    }
    write_unlock(&fib_info->lock);
}
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_625_0.png)

```c
extern _inline_ int nh_comp(const struct_fib *fi, const struct_fib *ofi)
{
    const struct_fib *nh *ohnh = ofi->fib_nh;
    for_each_nextthops(fi) {
        if (nh->nh_oif != onh->nh_oif ||
            nh->nh_gw != onh->nh_gw ||
            nh->nh_scope != onh->nh_scope ||
#ifdef CONFIG_ROUTE_MULTIPATH
            nh->nh_weight != onh->nh_weight ||
#endif
#ifdef CONFIG_NET_CLS_ROUTE
            nh->nh_tclassid != onh->nh_tclassid ||
#endif
            if ((nh->nh_flags & onh->nh_flags) & RTNH_F_DEAD)) {
                return -1;
            }
        nh++;
    }
    return 0;
}
```

```c
extern _inline_ struct fib_info *fib_find_info(const struct_fib *nfi)
{
    for_fib_info(fi) {
        if (fi->fib_nh != nfi->fib_nh)
            continue;
        if (fi->fib_protocol == nfi->fib_protocol &&
            fi->fib_prefsrc == nfi->fib_prefsrc &&
            fi->fib_priority == nfi->fib_priority &&
            memcmp(fi->fib_metrics, nfi->fib_metrics, sizeof(fi->fib_metrics)) == 0 &&
            (fi->fib_flags & nfi->fib_flags) & RTNH_F_DEAD) == 0 &&
            (nfi->fib_nh == 0 || nh_comp(fi, nfi) == 0)
            return fi;
    }
    endfor_fib_info(fi);
    return NULL;
}
```

## 图 8.33 FIB 语义--设置默认值：linux/net/ipv4/fib.semantics.c

```c
/* 检查网关是否已配置
仅由重定向使用。
*/
int ip_fib_check_default(u32 gw, struct net_device *dev)
{
    read_lock(&fib_info);
    for_fib_info(fi) {
        if (fi->flags & RTNH_F_DEAD)
            continue;
        for_nexthops(fi) {
            if (nh->nh_dev == dev && nh->nh_gw == gw
                if (!nh->flags&RTNH_F_DEAD))
                    read_unlock(&fib_info);
                    return 0;
        }
    }
    read_unlock(&fib_info);
    return -1;
}
#ifdef CONFIG_IP_ROUTE_MULTIPATH
static u32 fib_get_attr(struct rtattr *attr, int attrlen, int type)
{
    while (RTA_OK(attr, attrlen)) {
        if (attr->rta_type == type)
            return (u32*)RTA_DATA(attr);
        attr = RTA_NEXT(attr, attrlen);
    }
```

## 图 8.34 FIB 语义--添加下一跳并获取下一跳数：linux/net/ipv4/fib.semantics.c

```c
return 0;
static int
fib_count_nexthops(struct rtattr *rta)
{
    int nhs = 0;
    struct rtnextop *nhp = RTA_DATA(rta);
    int nhlen = RTA_PAYLOAD(rta);
    while (nhlen > (int)sizeof(struct rtnextop)) {
        if (nhlen - nhp->rtnh_len < 0)
            return 0;
        nhs++;
        nhp = RTNH_NEXT(nhp);
    }
    return nhs;
}
```

```c
static int
fib_get_nhs(struct fib_info *fi, const struct rtattr *rta, const struct rtmsg *r)
{
    struct rtnextop *nhp = RTA_DATA(rta)
    int nhlen = RTA_PAYLOAD(rta)
    change_nexthops(fi) {
        int attrlen = nhlen - sizeof(struct rtnop)
        if (attrlen < 0 || (nhlen == nhp->rtnh_len) < 0)
            return -EINVAL;
        nhp->nh_flags = (r->rtmsg_flags&0xFF) | nhp->rtnh_flags;
        nh->nh_of = nhp->rtnh_index;
        nh->nh_weight = nhp->rtnh_hops + 1;
        if (attrlen) {
            nh->nh_gw = fib_get_attr32(RTNH_DATA(nhp), attrlen, RTA_GATEWAY);
```
