
```c
d_echo(int sockfd, struct sockaddr *pcliaddr, socklen_t clilen)
{
    int n;
    char msg[MAXLINE];
    char control[MAXLINE];
    struct msghdr msg;
    struct msghdr *cmmsg;
    struct iov iov[1];
    n = 1;
    setsockopt(sockfd, IPPROTO_IPV6, IPv6_RCVHDR, &n, sizeof(n));
    bzero(msg, sizeof(msg));
    iov[0].iov_base = msg;
    msg.msg_name = pcliaddr;
    msg.msg_iov = iov;
    iov[0].iov_len = MAXLINE;
    msg.msg_control = control;
    msg.msg_control_len = sizeof(control);
    n = recvmsg(sockfd, &msg, clilen);
    for (cmmsg = CMSG_FIRSTHDR(&msg); cmmsg != NULL; cmmsg = CMSG_NEXTHDR(&msg)) {
        if (cmmsg->cmsg_level == IPPROTO_IPV6 &&
            cmmsg->cmsg_type == IPv6_RCVHDR) {
                inet6_rth_reverse(CMSG_DATA(cmmsg), CMSG_DATA(cmmsg));
            }
    }
    iov[0].iov_len = n;
    sendmsg(sockfd, &msg, 0);
}
```
图 24 `d_echo` 解析并反转 IPv6 源路由的函数。

# 查找并处理路由头

我们通过 `CMSG_FIRSTHDR` 和 `CMSG_NEXTHDR` 遍历辅助数据。尽管我们只期望一个辅助数据，但这样循环是好的。如果我们发现路由头，我们使用 `inet6_srcrt_print` 函数将其打印（图 27.15）。然后我们使用 `inet6_rth_reverse` 反转路由，以便我们可以返回数据包。在这种情况下，它在路由上原地操作，以便我们可以使用相同的辅助数据。

# Echo 数据包

我们设置要发送的数据长度并使用 `sendmsg` 返回数据包。

# 27.7 节 IPv6 粘性选项

```c
#include "unp.h"
void
inet6_srcrt_print(void *ptr)
{
    int i, segments;
    char str[INET6_ADDRRLEN];
    segments = inet6_rth_segments(ptr);
    printf("received source: ");
    for (i = 0; i < segments; i++) {
        printf("%s ", inet6_ntop(AF_INET6, inet6_rth_getaddr(ptr, i), str, sizeof(str)));
    }
    printf("\n");
}
```
图 27.15 `inet6_srcrt_print` 函数：打印接收到的 IPv6 源路由。得益于 IPv6 辅助函数，`inet6_srcrt_print` 几乎是简单的。

# 确定路由中的段

我们首先使用 `inet6_rth_segments` 确定路由中存在的段数。

# 遍历每个段

我们遍历所有段，为每个段调用 `inet6_rth_getaddr` 并使用 `inet6_ntop` 将地址转换为表示形式。我们处理 IPv6 源路由的客户端和服务器不需要知道源路由在包中的格式。API 提供的库函数隐藏了包格式的细节，同时提供了我们在 IPv4 中从头构建选项的所有活性。

我们描述了使用 `sendmsg` 和 `recvmsg` 的辅助数据来发送和接收不同的辅助数据对象：

- 1. IPv6 数据包信息：`in6_pktinfo` 结构包含目的地址和输出索引，或者源地址和到达接口索引（图 22.21）
- 2. 输出跳数或接收跳数（图 22.21）
- 3. 下一跳地址（图 22.21）
- 4. 输出或接收的流量类别（图 22.21）
- 5. 跳跳选项（图 27.10）
- 6. 目的选项（图 27.10）
- 7. 路由头（图 27.12）

我们总结了这些对象的 `cmsg_level` 和 `cmsg_type` 值，以及图 14.11 中其他辅助数据的值。

当套接字上发送的所有数据包都使用相同的值时，与其在每次调用 `sendmsg` 时发送这些选项，不如设置相应的套接字选项。套接字选项与辅助数据相同，即选项级别为 `IPPROTO_IPV6`，选项是 `IPv6_DSTOPTS`、`IPv6_HOLIMIT`、`IPv6_HOPOPS`、`IPv6_NEXT`、`IPv6_PKTINFO`、`IPv6_RTHDR` 和 `IPv6_TCLASS`，但这些粘性选项可以通过在 `sendmsg` 调用中指定辅助数据，对 UDP 套接字或原始 IPv6 套接字按数据包进行覆盖。如果在 `sendmsg` 调用中指定了任何辅助数据，则相应的粘性选项不会随数据报发送。

粘性选项的概念也可以用于 TCP，因为 TCP 套接字上的 `sendmsg` 或 `recv` 永远不会发送或接收辅助数据。TCP 应用可以设置相应的粘性套接字选项并指定本节开头提到的七种选项类型任意一种。这些对象影响在该套接字上发送的所有数据包。然而，对于最初在设置（或未设置）粘性选项时发送的数据包，重传可能会使用原始选项或新选项。

无法通过 TCP 检索选项。

# 27.8 历史上的 IPv6 API

RFC 2292 [Stevens and Thomas 1998] 定义了这里描述的 API 的早期版本，该版本在许多系统中已实现并部署。在较早的版本中，处理目的和跳跳选项的函数是 `inet6_option_space`、`inet6_option_init`、`inet6_option_append`、`inet6_option_alloc`、`inet6_option_next` 和 `inet6_option_find`。这些函数处理 `struct cmsghdr` 对象，假设所有选项都包含在辅助数据中。该 API 中的路由头函数是 `inet6_rthdr_space`、`inet6_rthdr_init`、`inet6_rthdr_add`、`inet6_rthdr_lasop`、`inet6_rthdr_reverse`、`inet6_rthdr_segments`、`inet6_rthdr_getaddr` 和 `inet6_rthdr_getflags`。这些函数也直接操作 `struct cmsghdr` 辅助数据对象。

# 第 27 章

## 27.9 总结

在定义的 10 个 IPv4 选项中，最常用的是源路由，但由于安全考量，其使用率正在下降。通过 `IP_OPTIONS` 套接字选项访问 IPv4 头部选项。

IPv6 定义了六种扩展头部。通过功能接口访问 IPv6 扩展头部，从而无需理解它们在数据包中的实际格式。这些扩展头部作为辅助数据（ancillary data）通过 `sendmsg` 写入，并作为辅助数据通过 `recvmsg` 返回。

## 练习题

* 27.1 在第 27.3 节末尾的 IPv4 源路由示例中，如果我们使用 `-G` 选项为客户端指定每个中间节点，而不是 `-g` 选项，会发生什么变化？
* 27.2 为 `IP_OPTIONS` 套接字选项指定的 `setsockopt` 缓冲区长度必须 4 字节的倍数。如果我们不按照图 27.1 所示，在缓冲区开头放置一个 `NOP`，我们该怎么办？
* 27.3 当使用 IP 记录路由选项时（TCPv1 第 7.3 节描述），`ping` 如何接收源路由的？
* 27.4 在第 27.3 节末尾清除接收到的源路由的 rlog 服务器示例代码中，为什么 `getsockopt` 和 `setsockopt` 的套接字描述符参数设为 0？
* 27.5 多年来，我们在第 27.3 节末尾显示的清除接收到的路由的代码如下：

```c
optsize = 0;
setsockopt(0, IPPROTO_IP, IP_OPTIONS, NULL, &optsize);
```
