
`read_unlock(sk->callback_lock);`

## 3.2.9 链路上

我们查看如果数据包是 UDP 包时的差异；例如，很大范围内，这些限于实际 UDP 协议。

## 3.3 DNS/UDP 示例

在 `udp.c` 中，感兴趣的函数是用于输出的 `udp_sendmsg()`。

### 3.3.1 UDP 输出

在 `udp.c` 中，感兴趣的函数是用于输出的 `udp_sendmsg()`。

#### 图 3.10 UDP 输出：linux/ipv4/udp.c。

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
    /* 为连接型 socket 打开路径。
       如果至少设置了一个选项，则不使用路由。
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

## 84 TCP/IP 与 Linux 协议实现

#### 图 3.11 UDP 输出：linux/ipv4/udp.c。

```c
if (ipc.opt && ipc.opt->is_strict)) {
```

# TCP/IP 与 Linux 协议实现

``` 
718      sin->sin_addr.s_addr = skb->nh->iph->saddr;
719      memset(sin->sin_zero, 0, sizeof(sin->sin_zero));
720  }
721  if (skb->protoinfo.af_inet.cmsg_flags)
722      ip_cmsg_recv(msg, skb);
723      err = copied;
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_141_0.png)

```
725  out_free:
726      skb_free_datagram(sk, skb);
727  out:
729      return err;
730  csum_copy_err:
731      UDP_INC_STATS_BH(UdpInErrors);
733  /* 清空队列. */
734  if (flags&MSG_PEEK)
736      int clear = 0;
737      spin_lock_irq(&sk->receive_queue.lock);
738      if (skb == skb_peek(sk->receive_queue)) {
739          __skb_unlink(skb, sk->receive_queue);
740          clear = 1;
741      }
742      spin_unlock_irq(&sk->receive_queue.lock);
743      if (clear)
744          free_skb(skb);
746  }
747  skb_free_datagram(sk, skb);
748  return -EAGAIN;
749 }
```

### 3.3.3 在线路上传输

16:11:35.321380 brams.cs.ucl.ac.uk.1904 > bells.cs.ucl.ac.uk.domain 60803 (43)
16:11:35.323169 bells.cs.ucl.ac.uk.domain > brams.cs.ucl.ac.uk.1904: 60803* 1/2 (172)

14:51:488399 0:20:af:eb:6e 8:20:7d:a5:36 a56 ip 85 brahms.cs.ucl.ac.uk:2167 > bells.cs.ucl.ac.uk.domain: 6517 (43)
14:51:490923 8:20:a5:36 20:af:eb1:6e ip 214: bells.cs.ucl.ac.uk.domain > brams.cs.ucl.ac.uk.2167: 6517* 1/2 (172)
14:22:05.123790 0:20:af:eb1:6e Broadcast arp 42 who-has merci.cs.ucl.ac.uk *** brams.cs.ucl.ac.uk

# 数据包的短暂生命

## 3.4 RTP/UDP（组播）示例

对于组播，高层协议是构建在 UDP 之上的，因此我们需要再次查看 `udp.c`。

发送过程与单播相同，接收端的情况必须处理一种可能：即可能有多个进程等待组播包的副本。接收尾部是否有不同，正如我们在 `udp.v4_mcast_deliver()` 中看到的。

#### 图 3.15 UDP 接收组播：linux/net/ipv4/udp.c。

```
read_lock(&udp_hash_lock);
sk = __udp_hash[ntoh(uh->dest) & (UDP_HTABLE_SIZE - 1)];
dif = skb->dev->ifindex;
skb = udp_v4_mcast_next(sk, uh->dest, uh->source, saddr, dif);
if (skb) {
    struct sock *skb = NULL;
    do {
        struct skb *skb1 = skb;
        next = udp_v4_mcast_next(sk, uh->dest, daddr, dif);
        uh->source, saddr, dif);
        if (skb1) {
            skb = skb_clone(skb, GFP_ATOMIC);
            udp_queue_rcv_sk(sk, skb1);
            skb = next;
    } while (next);
} else
free_skb(skb);
read_unlock(&udp_hash_lock);
```
