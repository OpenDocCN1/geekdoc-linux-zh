
`traceroute [-m <maxttl> -v] <hostname>;`

`host = argv[optind];`

`pid = getpid();`

`signal(SIGALRM, sig_alrm);`

`ai = Host_serv(host, NULL, ai->ai_addr);`

`h = sock_ntop(ai->ai_addr, ai->ai_addrlen);`

`printf("traceroute to %s (%s) : %d hops, %d bytes\n",`

`ai->ai_canon ? ai->ai_canon : h, max_ttl, datalen);`

`/* initialize according to protocol */`

`if (ai->ai_family == AF_INET) {`

`pr = &proto_v4;`

`#ifdef IPv6`

`} else if (ai->ai_family == AF_INET6) {`

`pr = &proto_v6;`

`if (((struct sockaddr_in6 *)ai->ai_addr)->sin6_addr))`

`err_quit("cannot traceroute IPv4-mapped IPv6 address");`

`#endif`

`} else`

`err_quit("unknown address %d", ai->ai_family);`

`pr->send = ai->ai_addr; /* contains destination address */`

`pr->recv = Calloc(1, ai->ai_addrlen);`

`pr->salast = Calloc(1, ai->ai_addrlen);`

`pr->bind = Calloc(1, ai->ai_addrlen);`

`pr->salen = ai->ai_addrlen;`

`tracerloop();`

`exit(0);`

我们检查图 28.19（第 761 页）所示的 `tracerloop` 函数。

# 创建原始 socket

9-10 我们两个 socket：一个用于读取所有返回的 ICMP 消息的原始 socket，另一个用于发送带有递增 TTL 的探测包的 socket。在创建原始 socket 后，我们将有效用户 ID 重置为真实用户 ID，因为我们不再需要超级用户权限。

# 设置 ICMPv6 接收过滤器

11-20 如果我们正在追踪到 IPv6 地址的路由，且 `-v` 命令行选项是我们预期的：“超时”（time exceeded），则安装过滤器拦截除“目的不可到达”（destination unreachable）之外的所有 ICMP 消息类型。这减少了在 socket 上收到的数据包数量。

# 创建 UDP socket 并绑定源端口

21-25 我们在用于发送的 UDP socket 上绑定源端口，使用 PID 的低 16 位，并将高位置为 1。由于在任何时刻都可能有多个 traceroute 程序副本在运行，我们需要一种方法来确定收到的 ICMP 消息是响应我们的数据报生成的，还是响应其他数据报生成的。我们使用 UDP 头部中的源端口来识别，因为返回的 ICMP 消息包含 UDP 头部。

# 信号处理程序

26 每次发送 UDP 数据报时，我们都建立 `sig_alarm` 作为信号处理程序，在发送下一个探测包之前等待三秒等待 ICMP 消息。

# 图 28.19 tracerloop 函数

`traceroute/tracerloop.c`

```c
#include "trace.h"

void
tracerloop(void)
{
    int seq, code, done;
    double rtt;
    struct rec *rec;
    struct timeval tcv;
    int recvfd = socket(pr->sa_family, SOCK_RAW, pr->protocol); // ...
    setuid(getuid()); /* we don't need special permissions */
#ifdef __linux__
    if (pr->sa_family == AF_INET6 && version == 0) {
        struct icmp_filter myfilter;
        ICMP_FILTER_SET(&myfilter);
        ICMP_FILTER_PASS(ICMP_TIME_EXCEEDED, &myfilter);
        ICMP_FILTER_BLOCK(ICMP_DST_UNREACHABLE, &myfilter);
        setsockopt(recvfd, IPPROTO_IPV6, ICMP_FILTER, &myfilter, sizeof(myfilter));
    }
#endif

    sendfd = socket(pr->sa_family, SOCK_DGRAM, 0);
    pr->sasend->sa_family = pr->sa_family;
    sport = (getpid() & 0xffff); /* our source port */
    sock_set_port(pr->sasend, pr->salen, htons(sport));
    bind(sendfd, pr->salen);
    sig_alarm(SIGALRM);
    seq = 0;
    done = 0;
    for (ttl = 1; ttl <= max_ttl && done == 0; ttl++) {
        setsockopt(sendfd, IP_level, IP_TTL, &ttl, sizeof(int));
        bzero(pr->salast, pr->salen);
        printf("%d, ", ttl);
        fflush(stdout);
        for (probe = 0; probe < nprobes; probe++) {
            rec = (struct rec *)sendbuf;
            rec->rec_seq = ++seq;
            rec->rec_ttl = ttl;
            gettimeofday(&rec->rec_tv, NULL);
            sock_set_port(pr->sasend, pr->salen, htons(dport));
            sendto(sendfd, sendbuf, 0, pr->sasend, pr->salen);
            if ((code = (*pr->recv)(seq, &tvrecv)) == -3)
                printf("** "); /* timeout, no reply */
            else {
                char str[NI_MAXHOST];
                if (getnameinfo(pr->srecv, pr->salen, str, sizeof(str), NULL, 0, 0) != 0)
                    printf(" %s", str);
                else
                    printf(" %s", sock_ntop(pr->srecv, pr->salen));
                memcpy(pr->srecv, pr->salast, pr->salen);
            }
            tv_sub(tvrecv, &rec->rec_tv);
            rtt = tvrecv.tv_sec * 1000.0 + tvrecv.tv_usec / 1000.0;
            printf("%.3f ms ", rtt);
            if (code == -1) /* port unreachable */
                done++;
            else if (code >= 0)
                printf("ICMP %s", (*pr->icmpcode)(code));
        }
    }
    fflush(stdout);
    printf("\n");
}
```
