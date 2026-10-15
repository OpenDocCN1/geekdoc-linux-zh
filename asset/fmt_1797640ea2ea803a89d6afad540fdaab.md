
```c
#include "unp.h"

static void recvvfrom_alarm(int);
static int pipefd[2];

void
dg_cli(FILE *fp, int sockfd, const struct A *pservaddr, socklen_t servelen)
{
    int n, maxfdpl;
    const int on = 1;
    char sendline[MAXLINE], recvcline[MAXLINE + 1];
    fd_set rset;
    socklen_t len;
    struct sockaddr *prely_addr;
    prely_addr = Malloc(servelen);
    Setsockopt(sockfd, SOCK_SOCKET, SO_BROADCAST, &on, sizeof(on));

    Pipe(pipefd);
    maxfdpl = max(pipefd[0], pipefd[1]) + 1;
    ZERO(&rset);
    Signal(SIGALRM, recvvfrom_alarm);
    while (fgets(sendline, MAXLINE, fp) != NULL) {
        sendto(sockfd, sendline, strlen(sendline), 0, pservaddr, servelen);
        FD_SET(sockfd, &rset);
        FD_SET(pipefd[0], &rset);
        if (select(maxfdpl, NULL, &rset, NULL, NULL, 0) < 0) {
            if (errno == EINTR)
                continue;
            else
                err_sys("select error");
        }
        if (FD_ISSET(sockfd, &rset)) {
            len = Recvfrom(sockfd, recvcline, MAXLINE, 0, prely_addr, &len);
            recvcline[len] = 0; /* 终止符 */
            printf("%s: %s\n", Sock_ntop(prely_addr, len), recvcline);
        }
        if (FD_ISSET(pipefd[0], &rset)) {
            Read(pipefd[0], &n, 1); /* 定时过期 */
            break;
        }
    }
    nfree(prely_addr);
}
```

# 第 20 章

## 练习题 547

```c
47 static void
48 recvvfrom_alarm(int signo)
49 {
50     Write(pipefd[1], "", 1);   /* 向管道写入一个空字节 */
51     return;
52 }
```

图 20.10 使用管道实现信号处理程序到函数的进程间通信。

## 20.6 总结

广播发送的是一个连接子网上的所有主机都会接收到的数据报。广播的缺点是，子网上的每个主机都必须处理该数据报（对于 UDP 数据报，则要通过 UDP 层处理），即使该主机没有参与该应用程序。对于高数据率的应用（如音频或视频），这会给这些主机带来过重的处理负载。我们将在下一章看到，组播解决了这个问题，因为只有对该应用程序感兴趣的主机才会接收该数据报。

通过使用一个版本的 UDP echo 客户端（该客户端向时间服务器发送广播，并在五秒内打印收到的所有回复），我们查看了 `SIGALRM` 信号的竞态条件。由于使用 `alarm` 函数和 `SIGALRM` 信号是为读取操作设置超时的常用方法，这种细微的错误在网络应用中很常见。我们展示了一种解决问题的错误方法，以及三种正确的方法：

- 使用 `select`
- 使用 `sigsetjmp` 和 `siglongjmp`
- 使用从信号处理程序到主循环的 IPC（通常是管道）

## 练习题

20.1 使用 `dg_cli` 函数运行 UDP 客户端，该函数会广播（图 20.5）。你收到了多少个回复？回复总是以相同的顺序出现吗？你网络上的主机时钟是同步的吗？

20.2 在图 20.10 的 `select` 返回后放置一些 `printf`，查看它是否为其中一个描述符返回了错误或可读性。当定时器过期时，你的系统返回的是 `EINTR` 还是管道的可读性？

20.3 如果可用，运行如 `tcpdump` 等工具，并查找你局域网上的广播包；`tcpdump ether broadcast` 是对应的 `tcpdump` 命令。这些广播属于哪种协议？

# 第 21 章

# 组播

## 21.1 引言

如图 20.1 所示，单播地址识别单个 IP 接口，广播地址识别子网上的所有 IP 接口，而组播地址识别一组 IP 接口。单播和广播是地址频谱的两个极端（一个或全部），而组播的意图是允许对两者之间的内容进行寻。组播数据报应该只由对数据感兴趣的接口接收，即运行希望加入组播组的应用程序的主机接口。此外，广播通常局限于局域网（LAN），而组播可以在局域网或跨广域网（WAN）使用。事实上，应用程序每天都会在互联网的一个子集进行组播。

`sockets` API 中新增的组播功能简单；它们由套字选项组成：三个影响向组播地址发送 UDP 数据报的选项，以及六影响主机接收组播数据报的选项。

## 21.2 组播地址

在描述组播地址时，我们必须区分 IPv4 和 IPv6。

### IPv4 D 类地址

D 类地址范围为 `244.0.0.0` 到 `239.255.255.255`，`244.0.0.0` 到 `239.255.255.255` 范围称为 D 类。图 21.1 显示了 IPv4 到以太网的映射。

### 组播

IPv4 到以太网的映射规定在 RFC 2464 [Crawford 1998a] 中，FDDI 的相同映射在 RFC 2267 [Crawford 1998b] 中，令牌环映射在 RFC 2470 [Crawford, Norton, and Thomas 1998] 中。以太网地址第一个字节的低位两个位指定该地址为本地管理组。这里有几个 IPv4 组播地址：

- `224.0.1` 是所有主机组。子网上的所有组组能力的节点（主机、路由器等）必须加入此组。
- `224.0.2` 是所有路由器组。子网上的所有组组能力的路由器必须加入此组。

`224.0..0.0/24` 范围被称为链路本地。这些地址保留用于低级拓扑发现和维护，发往这些地址的数据报永远被路由器转发。

### IPv6 组播地址

IPv6 组播地址的高字节值为 `ff`。图 21.1 显示了 16 位 IPv6 组播地址到 6 位以太网地址的映射。组地址的低 32 位被复制到以太网地址的低 32 位中。以太网地址的高两个字节为 `ff:ff`。

IPv6 组播地址定义了两种格式，如图 21.2 所示。当 P 标志为 0 时，T 标志区分了已知组播组（值为 0）和瞬态组播组（值为 1）。P 值为 1 表示基于单播前缀分配的组播地址（定义在 RFC 3306 [Haberman and Thaler 2002]）。如果 P 标志为 1，则 T 标志也必须为 1（即基于单播的组播地址始终是瞬态的），且 `plen` 和 `prefix` 字段分别设置为单播前缀的长度和值。

### 552 多组播第 21 章

字段已被预留。IPv6 多组播地址还有一个 4 位范围字段（scope field），我们稍后讨论。RFC 3370 [Haberman 2002] 描述了 IPv6 组地址低 32 位（组 ID）的分配机制，该机制与 P 标志的设置无关。

有一些特殊的 IPv6 多组播地址：

- `ff01::1` 和 `ff02::1` 分别是接口本地（interface-local）和链路本地（link-local）范围的所有节点。所有节点（主机、路由器、打印机等）必须在所有支持多组播的接口上加入这些组。这类似于 IPv4 的 `224.0.0.1` 多组播地址。然而，由于组播是 IPv6 的不可缺的一部分（与 IPv4 不同），这是可选的。

尽管 IPv4 组被称为所有主机（all-hosts），而 IPv6 组被称为所有节点（all-nodes），但它们的作用相同。IPv6 中将该组重命名，是为了明确它不仅面向主机，还面向子网上的路由器、打印机以及任何其他 IP 设备。

- `ff01::2`、`ff02::2` 和 `ff05::2` 分别接口本地、链路本地和站点本地（site-local）范围的路由器组。子网上的所有路由器必须在所有支持多组播的接口上加入这些组。这类似于 IPv4 的 `224.0.0.2` 多组播地址。

## 多组播地址的范围
