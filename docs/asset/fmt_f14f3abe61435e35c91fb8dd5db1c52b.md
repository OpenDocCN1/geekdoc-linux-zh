
**图 28.38** 获取客户端绑定到其套字的端口号。

## 向客户端指示成功

向客户端返回一个由字符 "1" 组成的字节。

## 关闭客户端的 UDP 套字

我们已经完成了对 UDP 套字的操作并将其关闭。该描述符是由我们传递的，因此是一个副本；因此，UDP 套字在客户端端仍是打开的。

## 处理错误和终止

如果发生错误，会向客户端写回字节的 "0"。当客户端终止时，我们 Unix 域连接的一端会被关闭，描述符会从 `select` 的描述符集合中移除。`client` 结构中的 `confd` 成员被设置为 -1，表示它是可用的。

## 2.7 ICMP 消息

当原始 ICMP 套字可读时，调用 `readable_conn`。该客户端在 `client` 数组中的索引是其参数。

## 2.8 ICMP 套字

`readable_conn` 在 ICMP 套字可读时被调用。这与图 28.39 所示代码与 28.40 类似。

```c
#include <icmp.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <netinet/udp.h>

int
readable_conn(int client)
{
    int unixfd, recvfd;
    char c;
    ssize_t n;
    socklen_t len;
    struct sockaddr_storage ss;

    unixfd = client(client[0]);
    recvfd = -1;

    if ((n = Read_fd(unixfd, 1, &recvfd)) == 0) {
        err_msg("client terminated, recvfd = %d", recvfd);
        client_gotodone();
    }

    if (recvfd < 0) {
        err_msg("read_fd did not return descriptor");
        client_gotodone();
    }
}
```

图 23 从客户端读取数据和可能的描述符。

一个设计决定是在应用程序和守护进程之间使用 Unix 域套字，还是使用 Unix 域套字。应用程序的 UDP 数据包可以通过任何类型的 Unix 套字传递。我们使用流式套字是为了检测客户端何时终止。当客户端终止时，它所有的描述符都会自动关闭，包括它到守护进程的 Unix 连接，这允许守护进程从 `client` 数组中移除此项。如果我们使用数据报套字，将不知道客户端何时终止。

如果客户端没有关闭连接，我们期望得到一个描述符。

我们 `readable_conn` 函数的后半部分如图 28.38 所示。

## 2.9 ICMP 报文

调用 `getsockname` 是为了让守护进程能够获取绑定到套字的端口号。由于我们不知道为套字地址结构分配多大的缓冲区，我们使用了 `sockaddr_storage` 结构，该结构足够大且对齐，可以存储系统支持的任何套字地址结构。

套字的地址族存储在 `client` 结构中，连同端口号。如果端口号为 0，我们调用 `sock_bind_wild` 函数将通配符地址和临时端口绑定到套字，但正如我们之前提到的，这在某些 SVR4 实现上不起作用。

| 行 | 代码 |
| :--- | :--- |
| 28 | `readable_conn` 在 ICMP 套字可读时被调用。 |
| 29 | 该代码与图 28.40 类似。 |
| 30 | `icmp->icmp_type == ICMP_REACH ||` |
| 31 | `icmp->icmp_type == ICMP_TIMEDOUT ||` |
| 32 | 2.8 这里的 ICMP 报文在图 28.39 所示。 |
| 33 | `icmp->icmp_type == ICMP_SOURCEQUERY)` |
| 34 | `if (icmp->len < 8 + 20)` |

我们 `readable_conn` 函数的后半部分如图 28.38 所示。

## 2.10 转换类型和代码返回 `errno` 值

```c
/* convert type and code to return errno value */
icmpd_err.icmp_errno = EHOSTUNREACH; /* default * */

if (icmp->icmp_type == ICMP_REACH) {
    if (icmp->icmp_code == ICMP_PORT)
        icmpd_err.icmp_errno = ECONNREFUSED;
    else if (icmp->icmp_code == ICMP_REACH_NEFRAG)
        icmpd_err.icmp_errno = EMSGSIZE;
}
```

## 2.11 接收到的 ICMP 报文，前半部分

```c
icmpd_err.icmp_type = icmp->icmp_type;
icmpd_err.icmp_code = icmp->icmp_code;
icmpd_err.icmp_len = sizeof(struct sockaddr_in);
memcpy(&icmpd_err.icmp_id, &icmp_id, &dest, sizeof(dest));
```

## 2.12 接收到的 ICMP 报文，后半部分

```c
dest.sin_family = AF_INET;
#ifdef HAVE_SOCKADDR_SA_LEN
dest.sin_len = sizeof(dest);
#endif
memcpy(&dest.sin_addr, &ip->ip_dst, sizeof(struct sockaddr_in));
dest.sin_port = htons(udp->uh_port);
```

图 28.40 接收到的 ICMPv4 数据报，后半部分。

## 检查消息类型，通知应用程序

我们传递给应用程序的唯一 ICMP4 消息是“目的不可到达”、“时间超时”和“源猝制”（图 28.30）。

## 检查 UDP 错误，找到客户端

`hip6` 指向在 ICMP 头部之后返回的 IP 头部。这是触发 ICMP 错误的数据报的 IP 头部。我们验证该 IP 数据报是否为 UDP 数据报，然后从 IP 头部随后的 UDP 头部中获取源 UDP 端口号。

程序将对所有具有匹配地址族和端口的客户端结构进行搜索。如果找到匹配项，将构建一个 IPv4 套接字地址结构，其中包含来自导致错误的 UDP 数据报的目的 IP 地址和端口。

## 构建 `icmpd_err` 结构

构建一个 `icmpd_err` 结构，并通过连接到该客户端的 Unix 域套连接发送给客户端。首先将 ICMP4 消息类型和代码映射为 `errno` 值，如图 28.30 所示。

```c
#include "icmpd.h"
#include <netinet/in.h>
#include <netinet/ip.h>
#include <netinet/ip_icmp.h>
#include <netinet/udp.h>

#ifdef IPv6
#include <netinet/ip6.h>
#include <netinet/icmp6.h>
#endif

int
readable_v6(void)
{
#ifdef IPv6
    int i, hlen2, icmp6len, sport;
    char buf[MAXLINE];
    char srcstr[INET6_ADDRSTRLEN], dstr[INET6_ADDRSTRLEN];
    ssize_t n;
    socklen_t len;
    struct ip6_hdr *ip6;
    struct icmp6_hdr *icmp6;
    struct udphdr *udp;
    struct sockaddr_in6 from, dest;
    struct icmpd_error icmp_err;
#endif

    len = sizeof(from);
    // 注意：原始 OCR 在函数参数 (SA *) &from, &len) 中存在错误
    n = recvfrom(fd6, buf, MAXLINE, 0, (struct sockaddr *)&from, &len);
    printf("%d type = %d, code = %d\n", icmp6->type, icmp6->icmp6_code);

    if ((struct icmp6_hdr *buf = (struct icmp6_hdr *)buf) { /* ICMP6 头部开始 */
    if ((icmplen = n) < 8)
```
