
# 主循环；设置 TTL 跳数限制并发送探测

27-38 `tracerloop` 函数的循环是双嵌套循环。外层循环从 1 开始发送 TTL 限制并每次增加1，内部循环向目标发送三个探测（UDP 数据报）。当我们更改 TTL 时，使用 `setsockopt` 通过 `IP_TTL` 或 `IPv6_UNICAST_HOPS` socket 选项设置新值。

每次外层循环，我们都初始化由 `salast` 返回的 socket 地址结构。该结构将与接收 ICMP 消息时由 `recvfrom` 返回的 socket 地址结构进行比较，如果两个结构不同，将打印来自新 socket 的 IP 地址。使用这种技术，每个 TTL 对应第一次探测的 IP 地址（例如在运行程序时路由发生了变化），将打印新的 IP 地址。

# 设置目标端口并发送 UDP 数据报

39-40 每次发送数据包时，都会通过调用我们的 `sock_set_port` 函数更改 socket 地址结构中的目标端口。为每个探测更改端口的原因是，当到达最终目标时，三个探测包都会被发送到不同的端口，希望至少有一个端口未被占用。

# 读取 ICMP 消息

41-42 我们的一个函数 `recv_v4` 或 `recv_v6` 会调用 `recvfrom` 来读取并处理返回的 ICMP 消息。这两个函数在发生超时时返回 -3（告诉我们发送另一个探测），在接收到 ICMP “传输中超时”（time exceeded in transit）错误时返回 -2，在接收 ICMP “端口不可到达”（port unreachable）错误时返回 -1（这意味着我们已到达目标），在其他 ICMP 情况下返回非负 ICMP 代码。

# 打印回复

43-63 如前所述，如果这是给定 TTL 的第一个回复，或者发送 ICMP 消息的节点 IP 地址发生了变化，则打印主机名和 IP 地址（仅打印 IP 地址，`getnameinfo` 调用不返回主机名）。RTT 计算为从我们发送探测包到 ICMP 消息返回并打印的时间。

我们的 `recv_v4` 函数如图 28.20 所示。

# 图 28.20 函数：读取并处理 ICMPv4 消息。

```c
traceroute/recv_v4.c

1 #include          "trace.h"

2 extern int gotalarm:

/*

 * Return: -3 超时

 *      -2 ICMP 时（调用者继续）

 *      -1 ICMP 端口不可到达（调用者结束）

 *      >= 0 返回值为其他 ICMP 不可到达代码

 */

int

recv4(int seq, struct timeval *tv)

{

    int hlen1, hlen2, icmpmen, ret;

    socklen_t len;

    ssize_t n;

    struct ip *ip, *icmp;

    struct icmp *icmp;

    struct udphdr *udp;

    gotalarm = 0;

    alarm(3);

    for (; ; ) {

        if (gotalarm)

            return (-3);    /* 定时器超时 */

        len = pr->salen;

        n = recvfrom(recvd, recvbuf, sizeof(recvbuf), 0, pr->sarecv, &len);

        if (n < 0) {

            if (errno == EINTR)

                continue;

            else

                err_sys("recvfrom error");

        }

        ip = (struct ip *)recvbuf; /* IP 头部起始 */

        hlen1 = ip->ip_hl << 2; /* IP 头部长度 */

        icmp = (struct icmp *)(recvbuf + hlen1); /* ICMP 头部起始 */

        if ((icmpmen - hlen1) < 8)

            continue;    /* 数据不足，无法查看 ICMP 头部 */

        if (icmp->icmp_type == ICMP_TIMEXED &&

            icmp->icmp_code == ICMP_TIMEXED_TRANS) {

            if (icmpmen < 8 + sizeof(struct ip))

                continue;    /* 数据不足，无法查看内层 IP */

            hip = (struct ip *)(recvbuf + hlen1 + 8);

            hlen2 = hip->ip_hl << 2;

            if (icmpmen < 8 + hlen2 + 4)

                continue;    /* 数据不足，无法查看 UDP 端口 */

            udp = (struct udphdr *)(recvbuf + hlen1 + 8 + hlen2);

            if (hip->ip_p == IPPROTO_UDP &&

                udp->uh_sport == htons(sport) &&

                udp->uh_dport == htons(dport + seq)) {

                ret = -2;

                break;    /* 我们遇到了一个中间路由器 */

            }

        } else if (icmp->icmp_type == ICMP_UNREACH) {

            if (icmpmen < 8 + sizeof(struct ip))

                continue;    /* 数据不足，无法查看内层 IP * */

            hip = (struct ip *)(recvbuf + hlen1 + 8);

            hlen2 = hip->ip_hl << 2;

            if (icmpmen < 8 + hlen2 + 4)

                continue;    /* 数据不足，无法查看 UDP 端口 */

            udp = (struct udphdr *)(recvbuf + hlen1 + 8 + hlen2);

            if (hip->ip_p == IPPROTO_UDP &&

                udp->uh_sport == htons(sport) &&

                udp->uh_dport == htons(dport + seq)) {

                if (icmp->icmp_code == ICMP_UNREACH_PORT)

                    ret = -1; /* 已到达目标 */

                else

                    ret = icmp->icmp_code; /* 0, 1, 2, ... */

            }

        }

        if (verbose) {

            printf("from %s: %d, code = %d\n",

                   inet_nt_host(pr->sarecv, pr->salen),

                   icmp->icmp_type, icmp->icmp_code);

            /* 其他 ICMP 错误，再次调用 recvfrom() */

            alarm(0); /* 不要让定时器运行 */

            gettimeofday(tv, NULL); /* 获取数据包到达时间 */

            return (ret);

        }

    }

}
```
