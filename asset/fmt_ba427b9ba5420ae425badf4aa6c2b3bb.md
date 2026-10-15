
9 out->tv_sec = in->tv_sec;

10 }

```
```

图 28.8 显示了 `proc_v4` 函数，它处理所有收到的 ICMPv4 消息。你可能想参考图 A.1，该图显示了 IPv4 头的部的格式。请注意，当进程在套接字上接收到 ICMPv4 消息时，内核已经验证了 IPv4 头部和 ICMPv4 头部中的字段是有效的（见 TCPv2 第 214 页和第 311 页）。

# 图 28.8 proc_v4 函数：处理 ICMPv4 消息。

`ping/proc_v4.c`

```
1 #include "ping.h"

2 void

3 proc_v4 (char *ptr

return;
```

```
/* not ICMP */

icmp = (struct icmp) (ptr + hlen); /* start of ICMP header */

if ((icmplen == len - hlen) < 8)

    /* malformed packet */

    return;
```

```
if (icmp->icmp_type == ICMP_ECHOREPLY) {

    if (icmp->icmp_id != pid)

        /* not a response to our ECHO_REQUEST */

        return;

    if (icmplen < 16)

        /* not enough data to use */

}
```

```
tvsend = (struct timeval *) icmp->icmp_data;

tv_sub = (struct tcvrec, tvsend);

ttt = tcvrec->tv_sec * 1000.0 + tcvrec->tv_usec / 1000.0;
```

```
printf("%d bytes from %s=%u, ttl=%d, rtt=%.3f ms\n",

    icmplen, Sock_Nhost(pr->sarecv), pr->salen),

    icmp->icmp_seq, ip->ip_ttl, rtt);
```

```
} else if (verbose) {

    printf("%d bytes from %s: %d, code = %d\n",

    icmplen, Sock_Nhost(pr->sarecv), pr->salen),

    icmp->icmp_type, icmp->icmp_code);

}
```

# 获取 ICMP 头部指针

**10-16** IPv4 头部长度乘以 4，得到 IPv4 头部以字节为单位的大小（记住 IPv4 头部可以包含选项）。这使我们让 `icmp` 指向 ICMP 头的开始位置。我们确保 IP 协议是 ICMP，并且有足够的回显来检查我们在回请求（echo request）中包含的时间戳。图 28.9 显示了代码使用的各种头部、指针和长度。

> 图 28.9. 处理 ICMPv4 时的头部、指针和长度

| | icmplen | | |
|---|---|---|---|
| IPv4 header | IPv4 options | ICMPv4 header | ICMP data |
| 20 bytes | 0-40 | 8 | |
| ip | icmp | | |

# 检查 ICMP echo 回显

**17-21** 如果消息是 ICMP echo 回显，我们必须检查标识符字段，以查看此回复是否是对我们进程发送的请求的响应。如果 `ping` 程序在此主机上运行多次，每个进程都会获得所有收到的 ICMP 消息的副本。

**22-27** 我们通过从消息发送的时间（包含在 ICMP 回复的可数据部分中）减去当前时间（由 `tvrec` 函数参数指向）来计算 RTT（往返时延）。RTT 从微秒转换为毫秒并打印，连同序列号字段和收到的 TTL 一起。序列号字段允许用户查看数据包是否被丢、重排序或重复，而 TTL 则提供了两个主机之间跳跳数的指示。

# 如果指定了 verbose 选项则打印所有 ICMP 消息

如果用户指定了 `-v` 命令行选项，我们会打印其他收到的 ICMP 消息的类型和代码字段。

ICMP6 消息的处理由 `proc_v6` 函数处理，见图 28.12（第 751 页）。它与 `proc_v4` 类似；但是，由于 IPv6 原始套接字不返回 IPv6 头部，因此它将跳数限制（hop limit）作为辅助数据接收。这是使用图 28.10 所示的 `init_v6` 函数设置的。`init_v6` 函数为套接字做好准备。

# 设置 ICMP 接收

如果没有指定 `-v` 命令行选项，则安装过滤器过滤掉回显以外的所有 ICMP 消息。这减少了套接字上接收的数据包数量。

# 请求 IPv6_HOPLIMIT 辅助数据

15-22 请求跳数限制 API 随时间发生了变化。我们倾向于使用新的 API：`IPv6_RECVLIMIT`。但是如果没有定义该常量，我们可以尝试旧的 API：设置 `IPv6_HOPLIMIT`。我们不检查 `setsockopt` 的返回值，因为程序即使不接收跳数限制也可以工作。

# 图 28.10 init_v6 函数：初始化 ICMP6 套接字。

```
void

init_v6()

{

#ifdef IPv6

int on = 1;

if (verbose == 0) { /* install a filter that only passes ICMP6_ECHO_REPLY */

    struct icmp_filter myfilter;

    ICMP6_FILTER_BLOCK(&myfilter);

    ICMP6_FILTER_PASS(ICMP6_ECHO_REPLY, &myfilter);

    setsockopt(sockfd, IPPROTO_IPV6, ICMP6_FILTER, &myfilter, sizeof(myfilter));} /* ignore error below; we won't receive hop limit */

#define IPv6_RECVLIMIT /* RFC 3542 */

    setsockopt(sockfd, IPPROTO_IPV6, IPv6_RECVLIMIT, &on, sizeof(on));

#else /* RFC 2292 */

    setsockopt(sockfd, IPPROTO_IPV6, IPv6_HOPLIMIT, &on, sizeof(on));

#endif

#endif
```

`proc_v6` 函数（图 28.12）处理传入的数据包。

# 获取 ICMP6 头部指针

II13 ICMP6 头部是接收操作返回的数据（注意 IPv6 头部和扩展头部如果有的话，从不作为普通数据返回，而是作为辅助数据）。图 28.11 显示了代码使用的各种头部、指针和长度。

# 图 28.11. 处理 ICMPv6 回显时的头部、指针和长度。

`img/ab2a6f7209d14e3c9adbe68_0.png`

# 检查 ICMP echo 回显

IV-37 如果 ICMP 消息类型为 echo reply，我们检查标识符字段以查看回复是否是我们的。如果是，我们计算 RTT 并连同序列号和 IPv6 跳数限制一起打印。我们从 `IPv6_HOPLIMIT` 辅助数据获取跳数限制。

# 图 28.12 proc_v6 函数：处理收到的 ICMP6 消息。

`ping/proc_v6.c`

```
1 #include "ping.h"

2 void

3 proc_v6(char *ptr, size_t len, struct msghdr *msg, struct timeval *trecv)

4 {

#ifdef IPv6

     double rtt;

     struct icmp_hdr *icmp6;

     struct timeval *tvsend;

     struct msghdr *cmsg;

10    int hlim;

11 icmp6 = (struct icmp_hdr *)ptr;

12 if (len < 8)

13     return;     /* malformed packet */
```

```
if (icmp6->icmp6_type == ICMP6_ECHO_REPLY) {

    if (icmp6->icmp6_id == pid)

        return;      /* not a response to ECHO_REQUEST */

    if (len < 6)

        return;      /* not enough data to use */

tvsend = (struct timeval *) (icmp6 + 1);
