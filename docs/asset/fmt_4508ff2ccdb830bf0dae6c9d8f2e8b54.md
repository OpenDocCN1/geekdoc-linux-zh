
## SO_REUSEADDR

当任何服务器想要绑定到同一机器上某些应用程序正在使用的端口时，此选项允许我们在某些条件下使用相同的端口。此选项使用了 socket 对象的 `reuse` 字段。当应用程序想要绑定到特定端口时，内核通过 bind 路径调用 `tcp_v4_get_port()`。我们遍历绑定列表；如果发现端口被占用且设置了 `sk->reuse`，直接使用该端口。否则，如果 `sk->reuse` 的值设置为 1（第 252 行，c1.9），它在获取端口之前必须通过额外的检查。

## SO_KEEALIVE

此选项为 TCP 连接启用了心跳机制。应用程序可能运行数月，一方知道另一端。可能会发生一方掉线，在这种情况下另一端永远不知道。半连接将不必要地开启，从而占用资源。此选项会向另一端发送消息一段时间。作为回报，如果没有收到确认，连接将在经过若干重试后关闭。当启用此选项时，调用 `tcp_set_keepalive()` 设置 TCP 的存活定时器，并将 `sk->keepalive` 设置为 1。`tcp_set_keepalive()` 在存活定时器未设置时重置它；这是通过调用 `tcp_keepalive_timer()` 实现的（见 c10, 568）。

## SO_LINGER

linger 选项允许 TCP socket 在应用程序关闭 socket 时提供足够的时间发送队列中的数据。我们通过此选项提供一个超时值，以便内核在关闭 socket 之前挂起。在此期间，TCP 有足够的时间将所有数据刷新给接收者。如果没有提供超时时间，内核将等待所有数据被刷出。

此选项将 `sk->linger` 设置为 1，并将 `sk->lingertime` 设置为用户应用程序提供的超时值。当应用程序通过 `close()` 系统调用关闭 INET socket 时，会调用 `inet_release()`。如果设置了 linger 选项，将采取 linger 超时。

### 引言 (INTRODUCTION)

```c
net/ipv4/tcp_timer.c
562 void tcp_set_keepalive(struct sock *sk, int val)
563 |
564   if ((1<<sk->state)&(TCPF_CLOSE|TCPF_LISTEN))
565       return;
566 
567   if (val && !sk->keepalive)
568       tcp_keepalive_timer(sk, alive_time_reset(&sk->pinfo.af_tcp));
569   else if (!sk)
570       tcp_delete_keepalive_timer(sk);
571 |
```

### c1.10. `tcp_set_keepalive()`

```c
net/ipv4/af_inet.c
444 int inet_release(struct socket *sock)
445 |
446   struct sock *sk = sock->sk;
447 
448   if (sk) {
449       long timeout;
461       timeout = 0;
462       if (sk->linger && !(current->flags & PF_EXITING))
463           timeout = sk->lingerime;
464       sock->sk = NULL;
465       sk->prot->close(sk, timeout);
466   }
467   return(0);
468 |
```

### c1.11. `inet_release()`

来自 `sk->lingerime`（c1.11, 463）。最后，带有 linger 超时值调用协议特定的关闭程序（第 465 行，见 c1.11）。在 `tcp_close()` 中，我们检查作为路由参数的超时时间。如果内核通过第 1978 行调用 `add_wait_queue()` 将进程推睡眠（见 cs1.12）。当我们收到超时时，所有数据都已刷新。一旦我们执行了超时，socket 被关闭。

# TCP/IP 编程的应用程序接口

`net/ipv4/tcp.c`

```
1900 void tcp_close(struct sock *sk, long timeout)
1901 {
1902     struct sk_buff *skb;
      ...
1976     if (timeout) {
1977         struct task_struct *tsk = current;
1978         DECLARE_WAITQUEUE(sk,current);
1979      ...
1980         add_wait_queue(sk->sleep, &wait);
2064 )
```

cs 1.12. `tcp_close()`.

`net/ipv4/tcp.c`

```
680 static inline int tcp_memory_free(struct sock *sk)
681 {
682     return sk->wmem_queued < sk->sndbuf;
683 }
```

cs 1.13. `tcp_memory_free()`.

段被确认后，它们留在发送缓冲区中并计算发送缓冲区的消耗。

当应用程序数据写入 TCP 套字时，调用 `tcp_memory_free()` 以检查发送缓冲区是否有足够的空间存放应用程序数据。如果返回 TRUE，我们可以将新数据放入套字字的发送缓冲区，否则（见代码 13）。

**`SO_RCVBUF`.** 该选项与 `SO_SNDBUF` 相同，不同在于它设置了接收缓冲区 `sk->rcvbuf` 的上限。在 `tcp_data_queue()` 中，我们检查分配给接收区的内存是否超过套字字的限制（见代码 14）。如果是，我们通过调用 `tcp_prune_queue()` 尝试挤压接收区的内存。

**`SO_DIRECTROUTE`.** 该选项通常用于 RAW 套接字或 UDP 套接字，并将 `sk->localroute` 设置为 1。启用此选项，当目标直接连接网络时，数据将进行路由。

**`SO_RCTIMEO`.** 该选项为套接字设置超时时间，指定进程在等待传入事件时阻塞的最大时间，例如：

- 监听套接字的 Accept 等待连接。
- 连接套接字的 Read 接收数据。

引言

`net/ipv4/tcp.c`

cs 1.14. `tcp_data_queue()`.

`include/net/sock.h`

```
1238 static inline long sock_rcvtimeout(struct sock *sk, int nonblock)
1239 {
1240     return nonblock ? 0 : sk->rcvtime;
1241 }
```

cs 1.15. `sock_rcvtimeout()`.

`include/net/sock.h`

cs 1.16. `tcp_recvmsg()`.

`sock_rcvtimeout()` 为阻塞套接字返回超时值（见代码 15）。当请求的数据不可用时，`tcp_recvmsg()` 在第 1488 行（见代码 16）调用 `sock_rcvtimeout()` 获取套字字的超时值。随后在第 1639 行调用 `tcp_data_wait()`，让进程进入睡眠状态，直到发生超时或先接收到数据。

**`SO_SNDTIMEO`.** 该选项与 `SO_RCVTIMEO` 类似，区别在于为套字字的接收事件设置超时。它设置了 `sk->sndtimeout` 的值。

## SHUTDOWN

`include/net/sock.h`

```
1243 static inline long sock_sndtime(struct sock *sk, int nonblock)
1244 {
1245     return nonblock ? 0 : sk->sndtime;
1246 }
```

```
cs 1.17, sock_sndtime()...

ipv4/tcp.c

```

```
1009 int tcp_sendmsg(struct sock *sk, struct msghdr *msg, int size)

1010 {

...

1025     timeout = sock_sndtime(sk, flags&MSG_DONTWAIT);

1067     skb = tcp_alloc_skb(sk, select(sk), 0, allocation);

1068     if (sk == NULL)

1069         goto wait_for_memory;

1176 wait_for_memory:

1180     if ((err = wait_memory_free(sk, &timeout)) != 0)

1181         goto do_error;
```
