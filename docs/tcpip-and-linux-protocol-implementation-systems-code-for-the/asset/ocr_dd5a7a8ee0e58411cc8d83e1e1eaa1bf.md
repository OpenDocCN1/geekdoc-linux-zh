# Infrastructure Protocols 281

```
if (sk->type == SOCK_STREAM)
    goto e_inval;
/*
    Check the arguments are allowable
*/
err = -EFAULT;
if (optlen >= sizeof(struct ip_mreq))
    if (copy_from_user(mreq, optval, sizeof(mreq)))
        break;
} else {
    memset(mreq, 0, sizeof(mreq));
    if (optlen >= sizeof(struct in_addr))\n        copy_from_user(mreq->imr_address, optval, sizeof(struct in_addr))
        break;
}
```

Figure 6.99 IP socket-setsockopt entry for IP: linux/net/ipv4/ip_socketglue.c.

```
if (!mreq->imr_ifindex)
    if (mreq->imr_address.s_addr == INADDR_ANY)
        sk->protoinfo.af_inet.mc_index = 0;
    sk->protoinfo.af_inet.mc_addr = 0;
    err = 0;
    break;
else
    dev = ip_dev_find(mreq->imr_address.s_addr);
    if (dev)
        mreq->imr_ifindex = dev->index;
        dev_put(dev);
else
    dev = _dev_get_by_index(mreq->imr_index);
    err = -EADDRNOTAVAIL;
    if (dev)
        err = -EINVAL;
        if (sk->bound_dev_if && mreq->imr_ifindex != sk->bound_dev_if)
            break;
sk->protoinfo.af_inet.mc_index = mreq->imr_ifindex;
sk->protoinfo.af_inet.mc_addr = mreq->imr_address.s_addr;
    err = 0;
    break;
```