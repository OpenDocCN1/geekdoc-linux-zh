# Getting Socket Options

Getting socket options is just the inverse of setting them:

**Figure 6.101** IP glue–getsockopt entry for IP: linux/net/ipv4/ip_sockglue.c.

```
/*
 * Get the options. Note for future reference. The GET of IP options gets the
 * _received_ones. The met sets the _sent_ones.
 */
int ip_getsockopt(struct *sk, int level, int optname, char *optval, int *optlen)
(
    int val;
    int len;
    if(level==SGL_IP)
        return -EPMOTSSUPP;
    #ifdef CONFIG_IP_MROUTE
    if(optname>=MRT_BASE && optname <MRT_BASE+10)
        return ip_mroute_getsockopt(sk,optname,optval,optlen);
    }
#endif
    if(get_user(len,optlen))
        return -EFAULT;
    lock_sock(sk);
```

**Figure 6.102** IP glue–getsockopt entry for IP: linux/net/ipv4/ip_sockglue.c.

```
switch(optname) {
    case IP_OPTIONS:
        unsigned char optbuf[sizeof(struct ip_options)+40];
        struct ip_options *opt = (struct ip_options*)optbuf;
        opt->optlen = 0;
        if (sk->protoinfo.af_inet_opt)
            memcpy(optbuf, sk->protoinfo.af_inet.opt,
                sizeof(struct ip_options)+
            opt->optlen=sk->protoinfo.af_inet.opt->optlen);
        release_sock(sk);
        if (opt->optlen == 0)
            return put_user(0, optlen);
        ip_options_undo(opt);
        len=min(len, opt->optlen);
```