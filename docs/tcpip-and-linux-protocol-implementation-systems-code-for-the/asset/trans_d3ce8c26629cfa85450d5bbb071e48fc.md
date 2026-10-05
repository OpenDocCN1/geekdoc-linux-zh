

# 基础设施协议 463

```c
if (sk->protocol == IPPROTO_TCP) {
    struct tcp_copopt *opt = &(sk->tp_pinfo.af_tcp);

    local_bb_disable();

    sock_prot_dec_use(sk->prot);
    sock_prot_inc_use(&tcp->prot);
    local_bb_enable();
    sk->proto = &tcp->prot;
    tp->af_specific = &ipv4_specific;
    sk->socket_ops = &inet_stream_ops;
    sk->family = PF_INET;
    tcp_sync_msrc(sk, tp->pmtu_cookie);
} else {
    local_bb_disable();
    sock_prot_dec_use(sk->prot);
    sock_prot_inc_use(&udp->prot);
    local_bb_enable();
    sk->proto = &udp->prot;
    sk->socket_ops = &inet_dgram_ops;
    sk->family = PF_INET;
}
    opt = xchg(&mp->opt, NULL);
    if (sk_kfree(sk, opt, opt->tot_len)) {
        ptok = xchg(&mp->poptions, NULL);
        if (ptok)
            kfree_skb(ptok);
    }

    sk->destruct = inet_sock_destruct;

#ifdef INET_REFCNT_DEBUG
    atomic_dec(&inet6_sock_nr);
#endif
    MOD_DEC_USE_COUNT;
    retv = 0;
    break;
}
    goto e_inval;
```

图 6.373 IPv6 socket 设置套接选项：linux/net/ipv6/ipv6_glue.c。

```c
    case IPv6_PKTINFO:
        np->rxopt.bits.rxinfo = val;
        retv = 0;
        break;

    case IPv6_HOPLIMIT:
        np->rxopt.bits.rxhlim = val;
        retv = 0;
        break;

    case IPv6_RTMDR:
      if (val < 0 || val > 2)
          goto e_inval;
      np->rxopt.bits.scrcrt = val;
      retv = 0;
      break;

  case IPv6_HOOPTS:
              np->rxopt.bits.hopopts = val;
              retv = 0;
              break;

  case IPv6_AUTHHDR:
              np->rxopt.bits.authhdr = val;
              retv = 0;
              break;

  case IPv6_DSTOPTS:
              np->rxopt.bits.dstopts = val;
              retv = 0;
              break;

  case IPv6_FLOWINFO:
              np->rxopt.bits.rxflow = val;
              retv = 0;
              break;
```

数据包选项：

**图 6.374** IPv6 socket 设置套接选项：linux/net/ipv6/ipv6_sockglue.c。

```c
  case IPv6_PKTOOPTIONS:
      {
          struct ipv6_options *opt = NULL;
          struct msghdr *msg;
          struct flow *fl1;
          int junk;

          fl1.fi6_flowlabel = 0;
          fl1.oif = ak->bound_dev_if;

          if (optlen == 0)
              goto update;

          opt = sock_kmalloc(opt, sizeof(*opt) + optlen, GFP_KERNEL);
          retv = -ENBUFS;
          if (opt == NULL)
              break;

          memset(opt, 0, sizeof(*opt));
          opt->tot_len = sizeof(*opt) + optlen;
          retv = -EFAULT;
          if (copy_from_user(opt+1, opt, optlen))
              goto done;
          msg.msg_controllen = optlen;
          msg.msg_control = (void*)(opt+1);
          retv = datagram_send_ctl(&sk, &fl, opt, &junk);
          if (retv)
              goto done;
update:
          retv = 0;
          if (sk->type == SOCK_STREAM) {
              if (opt) {
                  struct tcp_opt *opt = &sk->sk_pinfo.af_tcp;
                  if (((sk->state)&TCP_LISTENING|TCP_CLOSE)) && sk->daddr == LOOPBACK_IPV6) {
                      opt->ext_header = opt->opt_len + optlen;
                      tcp_limit(sk, opt->pmtu_cookie);
                  }
              }
              opt = xchg(&np->opt, opt);
              sk_dst_reset(sk);
          } else {
              write_lock(&sk->dst_lock);
              opt = xchg(&np->opt, opt);
              write_unlock(&sk->dst_lock);
              sk_dst_reset(sk);
          }
done:
          if (opt)
              sock_kfree(sk, opt, opt->tot_len);
          break;
}
```

多播参数：

图 6.375 IPv6 socket 设置选项：linux/net/ipv6_sockglue.c。

```c
  case IPv6_UNICAST_HOPS:
  if (val > 255 || val < -1)
      goto e_in;
  np->hop_limit = val;
  retv = 0;
  break;

  case IPv6_MULTICAST_HOPS:
  if (sk->type == SOCK_STREAM)
      goto e_in;
  if (val > 255 || val < -1)
      goto e_in;
  np->mcast_hops = val;
  retv = 0;
```

466 TCP/IP 和 Linux 协议实现

```c
      break;

  case IPv6_MULTICAST_LOOP:
      np->mc_loop = val;
      retv = 0;
      break;

  case IPv6_MULTICAST_IF:
      if (sk->type == SOCK_STREAM)
          goto e_in;
      if (sk->bound_dev_if && sk->bound_dev_if != val)
          goto e_in;

      if (dev_get_by_index(val) == NULL) {
          retv = -ENODEV;
      }
      np->cast_oif = val;
      retv = 0;
      break;
```

# 多播成员：

**图 6.376** IPv6 socket 设置套接选项：linux/net/ipv6/ipv6sockglue.c。

```c
  case IPv6_ADD_MEMBERSHIP:
  case IPv6_DROP_MEMBERSHIP:
      {
          struct ipv6_mreq mreq;

          retv = -EFAULT;
          if (copy_from_user(&mreq, optval, sizeof(struct ipv6_mreq)))
              break;

          if (opt == IPv6_ADD_MEMBERSHIP)
              retv = ipv6_sock_mc_join(sk, mreq, ipv6_mreq_finder, ipv6_mreq_multiaddr);
          else
              retv = ipv6_sock_mc_drop(sk, mreq, ipv6_mreq_finder, ipv6_mreq_multiaddr);
              break;
      }
```

# 路径参数：

**图 6.377** IPv6 socket 设置套接选项：linux/net/ipv6/ipv6sockglue.c。

```c
  case IPv6_ROUTER_ALERT:
      retv = ip6_ra_control(sk, val, NULL);
      break;
  case IPv6_MTU_DISCOVER:
    if (val < 0 || val > 2)
        goto e_inval;
    np->frag = val;
    retv = 0;
    break;
    case IPv6_MTU:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->mtu = val;
    retv = 0;
    break;
    case IPv6_RECR:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->recr = val;
    retv = 0;
    break;
    case IPv6_FLOWINFO:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->flowinfo = val;
    retv = 0;
    break;
    case IPv6_NETFILTER:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->netfilter = val;
    retv = 0;
    break;
    case IPv6_SND:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->sndinfo = val;
    retv = 0;
    break;
    case IPv6_AUTHHDR:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->authhdr = val;
    retv = 0;
    break;
```

# 基础设施协议 467

```c
    if (val < 0 || val > 2)
        goto e_inval;
    np->frag = val;
    retv = 0;
    break;
    case IPv6_MTU:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->mtu = val;
    retv = 0;
    break;
    case IPv6_RECR:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->recr = val;
    retv = 0;
    break;
    case IPv6_FLOWINFO:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->flowinfo = val;
    retv = 0;
    break;
    case IPv6_NETFILTER:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->netfilter = val;
    retv = 0;
    break;
    case IPv6_SND:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->sndinfo = val;
    retv = 0;
    break;
    case IPv6_AUTHHDR:
    if (sk->type == SOCK_STREAM)
        goto e_inval;
    np->authhdr = val;
    retv = 0;
    break;
```

# 6.9.9 IPv6 流标签

IPv6 标签是 IPv6 的一个独特特性，可以用于快速路由，正如第 9 章中讨论的区分服务或集成服务。

# 468 TCP/IP 和 Linux 协议实现

以下是标签管理的片段：

图 6.378 IPv6 流标签创建：linux/net/ipv6/flowglue.c。

```c
static struct ip6_flowlabel
fl_create(struct in6_flowlabel_req *freq, char *optval, int optlen, int *err_p)
{
    struct ip6_flowlabel *fl;
int olen;
int addr_type;
int err;

err = -ENOMEM;
fl = kmalloc(sizeof(*fl), GFP_KERNEL);
if (fl == NULL)
goto;
memset(fl, 0, sizeof(*fl));
```

图 6.379 IPv6 流标签创建：linux/net/ipv6_sockglue.c。

```c
olen = -optlen - CMSG_ALIGN(sizeof(*freq));
if (olen > 0)
    struct msghdr msgr;
    struct flowi;
    int junk;

err = -ENOMEM;
fl->opt = kmalloc(sizeof(fl->opt) + optlen, GFP_KERNEL);
if (fl->opt == NULL)
goto;
memset(fl->opt, 0, sizeof(*fl->opt));
fl->opt->tot_len = sizeof(fl->opt) + optlen;
err = -EFAULT;
if (copy_from_user(fl->opt+1, opt, optlen))
    goto;

msg.msg_controllen = olen;
msg.msg_control = (void **)(fl->opt+1);
flowi.opt = 0;

err = datagram_send_ctl(&msg, &flowi, fl->opt, &junk);
if (err)
goto;
```

