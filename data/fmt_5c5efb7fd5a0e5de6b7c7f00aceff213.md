
`tv_sub = (trecv, tvsend);`

`rtt = trecv->tv_sec * 1000.0 + trecv->tv_usec / 1000.0;`

`nhlim = -1;`

```c
for (cmsg = MSG_FIRSTHDR(msg); cmsg != NULL;
    cmsg = MSG_NEXTHDR(msg, cmsg)) {
        if (icmp6->cmsg_level == IPPROTO_IPV6
            && cmsg->cmsg_type == ICMP6_HOPLIMIT) {
            hlim = (u_int32_t *) MSG_DATA(cmsg);
            break;
        }
}
```

```c
printf("%d bytes from %s: seq=%u, hlim=",
    len, Sock_ntop_host(pr->saven, pr->salen), icmp6->icmp6_seq);
    if (hlim == -1)
        printf("??");      /* ancillary data missing */
    else
        printf("%.3f ms\n", rtt);
} else if (verbose) {
    printf("%d bytes from %s: type = %d code = %d\n",
        len, Sock_ntop_host(pr->saven, pr->salen),
        icmp6->icmp6_type, icmp6->icmp6_code);
}
#endif /* IPV6 */
```

# 如果指定了 verbose 选项则打印所有 ICMP 消息

38-4 如果用户指定了 `-v` 命令行选项，我们会打印所有收到的 ICMP 消息的类型和代码字段。

我们的 SIGALRM 信号处理器是 `sig_alarm` 函数，见图 28.13。我们在图 28.6 中看到 `rread` 函数在开始时调用一次此处理器以发送第一个数据包。该函数调用协议相关的函数发送 ICMP 请求（`send_v4` 或 `send_v6`），然后在一秒后调度 SIGALRM。

## 图 28.13 sig_alarm 函数：SIGALRM 信号处理器。

```
ping/sig_alarm.c
#include      "ping.h"
void
sig_alarm(int signo)
(
    (pr->fsend)();
    alarm(1);
);
```

```c
return;
}
```

图 28.14 显示的 `send_v4` 函数构建了一个 ICMPv4 回显请求消息并将其写入原始套接字。

### 图 28.14 send_v4 函数：构建一个 ICMPv4 回显请求消息并发送它。

`ping/send_v4.c`
```c
1 #include "ping.h"
2 void
3 send_v4 (void)
4 {
5     int               len;
6     struct icmp *icmp;
7     icmp = (struct icmp *) sendbuf;
8     icmp->icmp_type = ICMP_ECHO;
9     icmp->icmp_code = 0;
10 icmp->icmp_id = pid;
11 icmp->icmp_seq = nsent++;
12 memset(icmp->icmp_data, datalen, 0xa5, datalen); /* 用模式填充 */
13 gettimeofday((struct time *) icmp->icmp_data, NULL);
14 len = 8 + datalen;                /* 计算 ICMP 头和数据的校验和 */
15 icmp->icmp_cksum = 0; in_cksum((u_short *) icmp, len);
16 icmp->icmp_cksum = in_cksum;
17 sendto(sockfd, sendbuf, len, 0, pr->saddr, pr->salen);
18 }
```

### 构建 ICMPv4 消息

7-13 构建 ICMPv4 消息。标识符字段设置为 PID，序列号字段设置为全局变量 `nsent`，然后为下一个数据包对其进行递增。我们在 ICMP 消息的数据部分存储了 `0xa5` 模式。当前时间存储在数据部分的开头。

### 计算 ICMP 校验和

14-16 为了计算 ICMP 校验和，我们将校验和字段设置为 0 并调用 `in_cksum` 函数，将结果存储在校验和字段中。ICMPv4 校验和是从 ICMPv4 头和随后的任何数据计算得。

### 发送数据报

17 ICMP 消息在原始套接字上发送。由于我们没有设置 `IP_HDRINCL` 套接字选项，内核会在前面加上 IPv4 头。

互联网校验和是对待校验和的 16 位值的取反码和的取反码。如果长度是奇数，则为了计算校验和，会在逻辑上在数据末尾追加 1 字节。在计算校验和之前，会将校验和字段设置为 0。这用于 IPv4、ICMPv4、IGMPv4、ICMPv6、UDP 和 TCP。RFC 1071 [Braden, Borman, and Portage 1988] 包含了额外信息和一些数值示例。TCPv2 的第 8.7 节讨论了 `in_cksum` 函数中的该算法，该函数在图 28.15 所示，用于计算校验和。

### 图 28.15 in_cksum 函数：计算互联网校验和。

`libfree/in_cksum.c`
```c
1 uint16_t
2 in_cksum(uint16_t * addr, int16_t len)
3 {
4     int nleft = len;
5     uint32_t sum = 0;
6     uint16_t *w = addr;
7     uint16_t answer = 0;
8 
9     /*
10    * 我们的算法很简单，使用一个 32 位累加器 (sum)，我们向其添加
11    * 连续的 16 位字，最后将高 16 位的所有
12    * 进位位叠回低 16 位。
13    */
14    while (nleft > 1) {
15        sum += *w;
16        nleft -= 2;
17    }
18    /* 如果需要，处理一个奇字节 */
19    if (nleft == 1) {
20        *(unsigned char *) (&answer) = (unsigned char *) w;
21        sum += answer;
22    }
23 
24    /* 将从高 16 位的进位加回到低 16 位 */
25    sum = (sum >> 16) + (sum & 0xffff); /* 将高 16 位加到低 16 位 */
26    sum += (sum >> 16); /* 处理进位 */
27    answer = ~sum; /* 截断为 16 位 */
28    return (answer);
29}
```

### 互联网校验和算法

i-27 第一个循环计算所有 16 位值的和。如果长度是奇数，则将最后一个字节与和相加。我们在图 28.15 中所示的算法是简单的。由于内核执行了大量的校验和计算，内核通常具有经过优化的校验和。

该函数来自 Mike Muuss 编写的公共领域 ping。

我们 ping 程序的最终函数是 `send_v6`，如图 28.16 所示，它构建并发送 ICMPv6 请求。

### 图 28.16 send_v6 函数：构建并发送 ICMPv6 请求。

```c
1 #include "ping.h"
2 void
3 send_v6 (void)
4 {
5     int               len;
6     struct icmp *icmp6;
7 #ifdef IPV6
8     icmp6 = (struct icmp6 *) sendbuf;
9     icmp6->icmp_type = ICMPv6_ECHO_REQUEST;
10 icmp6->icmp_code = 0;
11 icmp6->icmp_id = pid;
12 icmp6->icmp_seq = nsent++; datalen; /* 用模式填充 */
13 memset((icmp6 + 1), 0xa5, (struct timeval *) (icmp6 + 1), NULL);
```
