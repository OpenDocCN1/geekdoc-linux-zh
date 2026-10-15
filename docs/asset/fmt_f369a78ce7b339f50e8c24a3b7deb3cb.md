
```c
#include "unp.h"

int
multicast_set_loop(int sockfd, int onoff)
{
    switch (sockfd_to_family(sockfd)) {
        case AF_INET:
            unsigned char flag;
            flag = onoff;
            return (setsockopt(sockfd, IPPROTO_IP, IP_MULTAST_LOOP,
                           &flag, sizeof(flag)));
    }
#ifdef IPV6
    unsigned int flag;
            flag = onoff;
            return (setsockopt(sockfd, IPPROTO_IPV6, IPv6_MULTICAST_LOOP,
                           &flag, sizeof(flag)));
    }
#endif
    default:
        errno = EAFNOSPORT;
        return (-1);
    }
}
```

## 21.8 使用组播

我们通过移除 `setsockopt` 的调用修改了图 20.5 中的 `udpcli`。如果输出接口、TTL 和回环选项可以接受，大多数组播选项都需要设置以发送组播报文。我们运行一个修改后的 UDP echo 服务器加入组，然后运行我们的程序并指定主机组为目标地址。

```
macosx % udpcli 224.0.1
hi there
from 172.24.37.78: macOS X
from 172.24.37.94: FreeBSD
```

我们从子网上的两个系统都收到了响应。它们都在运行组播服务器。每个回复都是单播的，因为请求的源地址（每个服务器作为回复的目标地址）是一个单播地址。

## IP 分片与组播

我们在第 20.4 节末尾提到，由于策略决定，大多数系统不允许广播报文进行分片。在组播中使用分片是可以的，因为我们可以使用相同的 2000 字节行的文件轻松进行验证。

```
macosx % udpcli 224.0.1
from 172.24.37.78: xxxxxxxxxx
from 172.24.37.94: xxxxxxxxxx
```

## 21.9 接收 IP 组播公告

IP 组播基础设施是互联网中启用了域间组播的部分。IP 组播基础设施于 1992 年作为“MBone”作为一种覆盖网络诞生，并在 1999 年转向作为互联网基础设施的一部分进行部署。它在企业内部被广泛部署，但域间组播基础设施部分并不常见。

要在 IP 组播上接收多媒体会议，站点需要知道会议的组播地址以及会议流的 UDP 端口（例如音频和视频）。会话公告协议或 SAP（RFC 2974 [Handley, Perkins, and Welcher]）描述了如何实现这一点（这些公告组播到 IP 组播基础设施的报文头和频率），会话描述协议或 SDP（RFC 2327 [Handley and Jacobson 1999]）描述了这些公告的内容（如何指定组播地址和 UDP 端口号）。希望在 IP 组播基础设施上发布会议的站点定期向一个已组播组和 UDP 端口发送包含会议描述的组播数据包。IP 组播基础设施上的站点运行一个名为 `sadr` 的程序来接收这些公告。这个程序做了很多工作：它不仅接收会话公告，还提供了一个交互式用户界面显示信息并允许用户发送公告。在本节中，我们将开发一个只接收这些会话公告的简单程序，以展示简单组播接收器的示例。

## 图 21.14 显示了我们接收 SAP/SDP 公告的主程序。

### 已知名称和已知端口

分配给 SAP 公告的组播地址是 224.2.127.254，其名称为 `sap.mcast.net`。所有已知组播地址（见 http://www.iana.org/assignments/multicast-addresses）都出现在 DNS 的 `mcast.net` 下。已知 UDP 端口是 9875。

```c
socklen_t salen;

struct sockaddr *sa;

if (argc == 1)
    sockfd = Udp_client(SAP_NAME, SAP_PORT, (void **) &sa, &salen);
else if (argc == 4)
    sockfd = Udp_client(argv[1], argv[2], (void **) &sa, &salen);
else
    err_quit("usage: mysdr <icast-addr> <port> <interface-name>");
```

```c
setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));

Bind(sockfd, sa, salen);

Mcast_join(sockfd, sa, salen, (argc == 4) ? argv[3] : NULL, 0);
```

```c
loop(sockfd, salen); /* receive and print */
```

```c
exit(0);
```

### 创建 UDP 套接字

12-17 我们使用 `udp_client` 函数查找名称和端口，它会填充相应的套接字地址结构。如果没有指定命令行参数，我们使用默认值；否则，我们将从命令行参数中获取组播地址、端口和接口名称。

### 绑定端口

18-19 我们设置 `SO_REUSEADDR` 套接字选项以允许该程序的多个实例在主机上运行，并将组播地址绑定到套接字上，以防止套接字接收发送到该端口的任何其他 UDP 数据报。绑定此组播地址不是必须的，但它可以由内核对我们不感兴趣的数据包进行过滤。

### 加入组播组

20 我们调用 `mcast_join` 函数加入该组。如果通过命令行参数指定了接口名称，则会将其传递给该函数；否则，我们让内核选择加入该组的接口。

21 我们调用图 21.15 所示的 `loop` 函数来读取并打印所有公告。

## 图 21.15 接收并打印 SAP/SDP 公的循环。

`mysdr/loop.c`

```c
#include "mysdr.h"

void
loop(int sockfd, socklen_t salen)
{
    socklen_t len;
    ssize_t n;
```

```c
char *p;
struct sockaddr *sa;
struct sap_packet {
    uint32_t sap_header;
    uint32_t sap_src;
    char sap_data[BUFFERSIZE];
};
```

```c
sa = Malloc(salen);

for ( : ; {
    len = salen;
    n = Recvfrom(sockfd, &buf, sizeof(buf) - 1, 0, sa, &len);
    if ((char *)&buf)[n] == 0) /* null terminate */
    buf.sap_header = ntohl(buf.sap_header);

    printf("% %s 0x%04x\n", Sock_nop(sa, len), buf.sap_header & SAP_HASH_MASK);
    if ((buf.sap_header & SAP_VERSION_MASK) >> SAP_VERSION_SHIFT) > 1) {
        err_msg("... version field not 1 (0x%08x)", buf.sap_header);
        continue;
    }
    if (buf.sap_header & SAP_IPV6) {
        err_msg("... IPv6");
        continue;
    }
    if (buf.sap_header & (SAP_DELETE | SAP_COMPRESSED)) {
        err_msg("... can't parse packet type (0x%08x)", buf.sap_header);
        buf.sap_header;
        continue;
    }
    p = buf.sap_data + (buf.sap_header & SAP_AUTHLEN_MASK);
    if (strcmp(p, "application/sdp") == 0) {
        p += 16;
        printf("%s\n", p);
    }
}
```

### 数据格式
