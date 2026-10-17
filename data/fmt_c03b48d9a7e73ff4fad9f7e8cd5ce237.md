
```
        }

    }

    if (!MULTICAST(mfc->mfc_castgrp.s_addr))

        return -EINVAL;

    if (!ipmr_cache_alloc())

        return -ENOMEM;

    c->mfc_origin=mfc->mfc_origin.s_addr;

    c->mfc_castgrp=mfc->mfc_castgrp.s_addr;

    c->mfc_parent=mfc->mfc_parent;

    ipmr_update_thresholds(c, mfc->mfc_ttl);

    if (mrtsock)

        c->mfc_flags = MFC_STATIC;

    write_lock_bh(&mrt_lock);

    c->next = mfc_cache_array[line];

    mfc_cache_array[line] = c;

    write_unlock_bh(&mrt_lock);

}
```

**图 6.220** IPMR–用户空间调用 mfc add：linux/net/ipv4/ipmr.c。

```c
/*
 *检查是否移除了一个队列列表。如果是，
 * 需要发送帧并清理。
 */
spin_lock_bh(&mfc_unres_lock);
for (cp=mfc_unres_queue; (uc=*cp) != NULL;
    cp = &uc->next) {
    if (uc->mfc_origin == c->mfc_origin &&
        uc->mfc_castgrp == c->mfc_castgrp) {
        *cp = uc->next;
        if (atomic_dec_and_test(&cache_resolve_queue_len)) {
            del_timer(&ipmr_expire_timer);
            break;
        }
    }
}
if (uc) {
    spin_unlock_bh(&mfc_unres_lock);
    ipmr_cache_resolve(uc, c);
    kmem_cache_free(mrt_cache, uc);
}
return 0;
```

# 基础设施协议

**图 6.221** IPMR–mrouted_socket 死亡：linux/net/ipv4/ipmr.c。

```c
static void mrtsock_destruct(struct socket *sk) {
    rtnl_lock();
    if (sk == route_socket) {
        ipv4_devconf.forwarding--;
        write_lock_bh(&mrt_lock);
        route_socket=NULL;
        write_unlock_bh(&mrt_lock);
        route_tables(sk);
    }
    rtnl_unlock();
}
```

# 多播 Socket 选项

**图 6.222** IPMR–setsockopt处理器：linux/net/ipv4/ipmr.c。

*Socket 选项和虚拟接口操作。整个虚拟接口系统是一个堆，但遗憾 BSD 是那样做的。也许有一天有了正确的 MSDP/PIM 路由器我们就可以清理它。*

```c
int ip_mroute_setsockopt(struct socket *sk, int optname, char *optval, int optlen) {
    int ret;
    struct if vif;
    struct mfc mfc;
    if (optname==MRT_INIT) {
        if (route_socket && capable(CAP_NET_ADMIN))
            return -EACCES;
    }
    switch(optname) {
    case MRT_INIT:
        if (sk->type!=SOCK_RAW || sk->protocol!=IPPROTO_IGMP)
            return -EINVAL;
        if (optlen!=sizeof(int))
            return -ENOPTS;
        rtnl_lock();
        if (route_socket)
            rtnl_unlock();
            return -EADDRUSE;
        ret = ip_ra_control(sk, mrtsock_destruct);
        if (ret != 0) {
            write_lock_bh(&mrt_lock);
            route_socket=sk;
            write_unlock_bh(&mrt_lock);
        }
        ipv4_devconf.forwarding++;
        rtnl_unlock();
        return ret;
    case MRT_DONE:
        if (!route_socket)
            return -EACCES;
        return ip_ra_control(sk, NULL);
    case MRT_ADD_VIF:
    case MRT_DEL_VIF:
        if (optlen!=sizeof(vif))
            return -EINVAL;
        if (copy_from_user(&vif,optval,sizeof(vif)))
            return -EFAULT;
        if (vif.vif >= MAXVFS)
            return -ENFILE;
        rtnl_lock();
        if (optname==MRT_ADD_VIF)
            ret = vif_add(&vif, route_socket);
        } else {
            ret = vif_delete(&vif.vif);
        }
        rtnl_unlock();
        return ret;
    case MRT_ADD_MFC:
    case MRT_DEL_MFC:
        if (optlen!=sizeof(mfc)) {
            return -EINVAL;
            if (copy_from_user(&mfc,optval,sizeof(mfc))) {
                return -EFAULT;
            }
            rtnl_lock();
            if (optname==MRT_DEL_MFC)
                ret = ipmr_mfc_delete(&mfc);
            else
                ret = ipmr_mfc_add(&mfc,route_socket);
            rtnl_unlock();
            return ret;
    case MRT_ASSERT:
        {
            int v;
            if (get_user(v,int (*optval))
                return -EFAULT;
            route_do_assert=(v)?1:0;
            return 0;
        }
#ifdef CONFIG_IP_PIMSM
    case MRT_PIM:
        {
            int v;
            if (get_user(v,int (*optval))
                return -EFAULT;
            v=(v)?1:0;
            rtnl_lock();
            if (v != route_do_pim) {
```
