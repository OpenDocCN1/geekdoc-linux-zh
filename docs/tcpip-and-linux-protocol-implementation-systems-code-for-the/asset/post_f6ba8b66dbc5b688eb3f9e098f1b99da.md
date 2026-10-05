
# TCP/IP and Linux Protocol Implementation

```c
1062  softnet_data[cpu].cng_level = NET_RX_DROP;
1063  #endif
1064  else if (avg_blog > lo_cong) {
1065      softnet_data[cpu].cng_level = NET_RX_MOD;
1066  #ifdef RAND_LIE
1067      rd = net_random();
1068      rq = rd % netdev_max_backlog;
1069          if (rq < avg_blog) /* unlucky backlog *//
1070              softnet_data[cpu].cng_level = NET_RX_HIGH;
1071  #endif
1072  else if (avg_blog > no_cong) {
1073      softnet_data[cpu].cng_level = NET_RX_LOW;
1074  else /* no no_cong *//
1075      softnet_data[cpu].cng_level = NET_RX_SUCCESS;
1076  softnet_data[cpu].avg_blog = avg_blog;
1077  }
```

Network devices interrupts up calling the function netif_rx() via the net_devices structure in linux/net/core/dev.

# Figure 3.7 Network device driver Rx iii: linux/net/core/dev.c.

```c
1135  enqueue:
1136      dev_bound(skb->dev);
1137      __skb_queue_tail(&queue->input_pkt_queue, skb);
1138      __skb_queue_raise_softirq(this->cpu, NET_RX_SOFTIRQ);
1139          local_irq_restore(flags);
1140  #ifdef OFFLINE_SAMPLE_SAMPLE
1141      get_sample_stats(this->cpu);
1142  #endif
1143      return softnet_data[cpu].cng_level;
1144
1145  }
1146  if (queue->throttle) {
1147      queue->throttle = 0;
1148  #ifdef CONFIG_NET_HW_FLOWCONTROL
1149      if (atomic_dec_and_test(&netdev_dropping))
1150          netdev_wakeup();
1151  #endif
1152  }
1153      goto enqueue;
1154  }
1156  if (queue->throttle == 0) {
1157      queue->throttle = 1;
1158      netdev_rx_stat[this->cpu].throttled++;
1159  #ifdef CONFIG_NET_HW_FLOWCONTROL
1160      atomic_inc(&netdev_dropping);
1161  #endif
1162  }
```

1164 drop:

```c
netdev_rx_stat[this->cpu].dropped++;
local_irq_restore(flags);
```

```c
kfree_skb(skb);
return NET_RX_DROP;
```
}

# Figure 3.8 Network device driver RX iv: linux/net/core/dev.c.

/* Deliver skb to an old protocol, which is not threaded well
or which do not understand shared skbs.
 */ 
static int dev_to_old_ones(struct packet_type *pt, struct sk_buff *skb, int, last last 
{
```c
static spinlock_t net_sk_bb_lock = SPIN_LOCK_UNLOCKED;
int ret = NET_RX_DROP;
```

```c
if (last) {
    skb = skb_clone(skb, GFP_ATOMIC);
    if (skb == NULL)
        return ret;
}
```

/* The assumption (correct one) is that old protocols
did not depend on BH different of NET_BH and TIMER_BH.
/*
/* Emulate NET_BH with special spinlock */
```c
spin_lock(net_bh_lock);
```

/* Disable timers and wait for all timers completion */
```c
tasklet_disable(bh_task_vec+TIMER_BH);
```

```c
ret = pt->func(skb, skb->dev, pt);
```

```c
tasklet_enable(bh_task_vec+TIMER_BH);
```

Then the software interrupt reschedules the rest, which eventually results in a call to net_rx_action.

Next, net_rx_action(), which dequeues the packet, calls a packet handler based on the packet type (via a table)—if it is IP, this calls ip_rcv() in ip_input.c, which checks various things.

## 3.2.6 IP Work

IP input has to decipher the packet, so the first thing to do is figure out if it is really for me, e.g., as it is IP version 4.

In ip_input, ip_recv() checks, then calls, NH_HOOK (to run filters), which may call, or queue directly, ip_recv_finish(), which calls ip_route_input() in route.c, which fills in the internal route.

This includes a function (forward or local delivery), and calls ip_local_deliver() in ip_input again, and this calls ipprot->handler.

This pointer was previously filled in (via the inet_protocol structure) in protocol.c, which matches the protocol to the protocol handler function—in this case, TCP–tcp_v4_recv().

This is investigated in more detail in Chapter 6.

## 3.2.7 TCP Input

The IPv4 case, the relevant input is coded off tcp_ipv4.c, which looks up if we have a connection, then tries to queue in process context, or else calls tcp_v4_do_recv(), which actually processes the TCP header (prediction, and so on) and calls tcp_event_data_recv(), does any acknowledgment needed, and calls the last function queues the socket.

## 3.2.8 Socket Input

In core/sock.c, we see that the main effect is triggered because sk->ready = sock_def_readable()...

# Figure 3.9 Socket receive-up code: struct sock *sk, int len linux/net/core/sock.c.

```c
void sock_def_readable(struct sock *sk, int len)
{
  read_lock(sk->callback_lock);
  if (sk->sleep & wake_active(sk))
    wake_up_interruptible(sk->sleep);
  sk_wake_async(sk, U_IN);
  read_unlock(sk->callback_lock);
}
```

## 3.2.9 On the Wire

We look at the difference if the packet were a UDP packet; for example, part a large extent, these are restricted to the actual UDP protocol.

## 3.3 DNS/UDP Example

In udp.c, the main function of interest is udp_sendmsg() for output.

## 3.3.1 UDP Output

In udp.c, the main function of interest is udp_sendmsg() for output.

# Figure 3.10 UDP output: linux/ipv4/udp.c.

```c
if (msg->msg_name) {
    struct sockaddr_in *usin = (struct sockaddr_in*)msg->msg_name;
    if (msg->msg_len > sizeof(*usin))
        return -EINVAL;
    if (usin->sin_family != AF_INET) {
        if (usin->sin_family != AF_SPEC)
            return -EINVAL;
    }
    ufh.daddr = usin->sin_addr.s_addr;
    ufh.dest = usin->sin_port;
    if (ufh.dest == 0)
        return -EINVAL;
} else {
    if (sk->state != TCP_ESTABLISHED)
        return -EMCONN;
    ufh.daddr = sk->daddr;
    ufh.dest = dport;
    /* Open path for connected socket.
       Route not be used, if at least one option is set.
    */
    connected = 1;
    ipc.addr = sk->daddr;
    ufh.source = sk->sport;
    ipc.opt = NULL;
    ipc.opt->sk = sk->bound_dev;
    if (err = ip_cmsg(msg, &ipc)) {
        if (err)
            return err;
        if (ipc.opt) {
            free = 1;
            connected = 0;
        }
    }
    if (ipc.opt) {
        ipc.opt->sk = sk->protoinfo.af_inet.addr;
    }
    ufh.saddr = sk->protoinfo.af_inet.mc_addr;
    ipc.addr = daddr = ufh.daddr;
```

## 84 TCP/IP and Linux Protocol Implementation

# Figure 3.11 UDP out: linux/ipv4/udp.c.

```c
if (ipc.opt && ipc.opt->is_strict)) {
    if (daddr)
        return -EINVAL;
    daddr = ipc.opt->faddr;
    connected = 0;
}
tos = RT_TOS(sk->protoinfo.af_inet.tos);
if (sk->localroute(msg->msg_flags&MSG_ROUTE) ||
    (ipc.opt && ipc.opt->is_route)) {
    tos = RT_UNLINK;
    connected = 0;
}
if (MULTICAST(daddr)) {
    if (!ipc.oif)
        ipc.oif = sk->protoinfo.af_inet.mc_index;
    if (daddr)
        ufh.saddr = sk->protoinfo.af_inet.mc_addr;
        connected = 0;
}
if (connected)
    rt = (struct rtable*)sk_dst(sk, 0);
if (rt == NULL) {
    err = ip_route_output(&art, daddr, ufh.saddr, ipc->oif);
    if (err)
        goto out;
}
err = -EACCES;
if (rt->rt_flags&RTFC_BROADCAST && !sk->broadcast)
    goto out;
if (connected)
    sk_dst_set(sk, dst_clone(rt->dst));
```

# Figure 3.12 UDP out: linux/ipv4/udp.c.

```c
if (msg->msg_flags&MSG_CONFIRM)
    goto do_confirm;
back_from_confirm:
ufh.saddr = rt->rt_src;
if (!ipc.addr)
    ufh.daddr = ipc.addr = rt->rt_dst;
ufh.ub_len = htons(len);
ufh.uh_check = 0;
ufh.iov = msg->msg_iov;
ufh.wcheck = 0;

    /* RFC1122: OK. Provides the checksuming facility (MUST) as per */
```

```c
/* 4.1.3.4. It's configurable by the application setsockopt() */
/* (MAY) and it defaults to on (MUST). */
```

```c
err = ip_build_xmit(
    (skb)->no_check == UDP_CSUM_NOIT ?
    udp_getfrag_nosum :
    udp_getfrag(),
    ufh, ulen, ipc, rt, msg->msg_flags);
```

## 3.3.2 UDP Input

UDP is small enough that it is all in one C file. For receive, the function of interest is udp_recvmsg().

# Figure 3.13 UDP input: linux/net/ipv4/udp.c.

```c
skb = skb_recv_datagram(sk, flags, noblock, &err);
if (!skb) {
    goto out;

    copied = skb->len - sizeof(struct udphdr);
    if (copied > len) {
        copied = len;
        msg->msg_flags |= MSG_TRUNC;
    }
\if (skb)->ip_sum==CHECKSUM_UNNECESSARY) {
    err = skb_copy_datagram_iov(skb, sizeof(struct udphdr), msg->msg_iov,
        copied);
} else if (msg->msg_flags&MSG_TRUNC) {
    if (skb)->checksum_complete(skb)) {
        goto csum_copy_err;
    }
    err = skb_copy_datagram_iov(skb, sizeof(struct udphdr), msg->msg_iov,
        copied);
} else {
    err = copy_and_checksum_tolovec(msg->msg_iov, skb, sizeof(struct udphdr));
}

if (err) {
    goto csum_copy_err;
}

if (err) {
    goto out_free;
}

nsock_recv_timestamp(msg, skb);
/* Copy the address. */
if (sin) {
    sin->sin_family = AF_INET;
    sin->sin_port = skb->uh->hs_source;
}
```
