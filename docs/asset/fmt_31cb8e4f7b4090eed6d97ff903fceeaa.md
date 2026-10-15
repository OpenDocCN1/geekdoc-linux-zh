
`struct ip_mreq` {

    `struct in_addr`          `imr_multiaddr`;      /* IPv4 D 类组播地址 */

    `struct in_addr`          `imr_interface`;      /* 本地接口的 IPv4 地址 */

};

`struct ipv6_mreq` {

    `struct in6_addr`          `ipv6_multiaddr`;      /* IPv6 组播地址 */

    `unsigned int`             `ipv6_interface`;      /* 接口索引，或 0 */

};

`struct group_req` {

    `unsigned int`             `gr_interface`;       /* 接口索引，或 0 */

    `struct sockaddr_storage` gr_group;       /* IPv4 或 IPv6 组播地址 */

}

如果本地索引限制为 IPv4 通配符（`INADDR_ANY`）或 IPv6 的索引0，则内核将选择单个接口。

如果一个或多个进程属于该组，则我们称该主机属于给定接口上的给定组播组。

给定的套接字允许多次加入，但每次加入必须针对不同的组播地址，或者针对相同的组播地址但于之前加入该地址的不同接口。这可以用于多宿主机，例如，创建一个套接字，并为每个接口对给定的组播组执行加入。

回想图 21.3，IPv6 组播地址包含一个作为地址部分的显式作用域字段。如所述，作用域不同的 IPv6 组播地址代表不同的组。如果 NTP 实现想要无论作用域如何都接收所有 NTP 数据包，它必须加入 `ff01::10`（接口本地）、`ff02::10`（链路本地）、`ff05::10`（站点本地）、`ff08::10`（组织本地）和 `ff0e::10`（全局）。所有加入操作可以在单个套接字上完成，并且应该设置 `IPv6_PKTO` 选项（第 22.8 节）以返回数据报的返回地址。

IP 协议无关套接字选项（`MCAST_JOIN_GROUP`）与 IPv6 选项相同，它们都使用 `in6_addr` 的 `sockaddr_storage` 将地址传递给内核。`sockaddr_storage`（图 3.5）足以存储系统支持的任何类型的地址。

大多数实现对每个套接字允许的加入次数有限制。该限制规定为 `IP_MAX_MEMBERSHIP`（Berkeley 衍生实现为 20），但某些实现限制了此值或将其提高最大。

当未指定要加入的接口时，Berkeley 衍生内核会在普通 IP 路由表中查找组播地址，并使用生成的接口（TCPv2 第 357 页）。某些系统在初始化时会为所有组播地址安装路由（即 IPv4 目的为 224.0.0.0/8 的路由）以处理这种场景。

对 IPv6 组播和协议无关选项进行了更改，使用接口索引来指定与 IPv4 使用的本地单播地址接口，以便允许在无编号接口和隧道上加入。

原始的 IPv6 组播 API 定义使用 `IPv6_ADD_MEMBERSHIP` 而不是 `IPv6_JOIN_GROUP`。API 其他部分相同。我们的 `mcast_join` 函数稍后处理此差异。

# IPV6_DROP_MEMBERSHIP, IPV6_LEAVE_GROUP, MCAST_LEAVE_GROUP

在指定的本地接口上离开源组播组。我们为用于加入组的相同结构也用于此套接字选项。如果未指定接口（即 IPv4 值为 `INADDR_ANY` 或 IPv6 索引为 0），则离开第一个匹配的组播组。

如果进程加入了一个组但没有显式离开该组，当套接字关闭（显式关闭或进程终止）时，成员关系将自动删除。如果主机上的多个套接字加入同一组，在这种情况下，在最后一个套接字离开之前，处理器将一直是该组的成员。

原始的 IPv6 组播 API 定义使用 `IPv6_DROP_MEMBERSHIP` 而不是 `IPv6_LEAVE_GROUP`。API 其他部分相同。我们的 `mcast_leave` 函数稍后处理此差异。

# IP_BLOCK_SOURCE, MCAST_BLOCK_SOURCE

阻塞从本地接口上现有的任何组成员关系中接收来自此源的流量。如果所有加入的套接字都阻塞了该源，系统可以通知路由器该流量是不需要的，可能会影响网络中的组播路由。它可以用于忽略来自恶意发送者的流量，例如。我们通过 IPv4 的其一个单播地址或协议无关 API 的接口索引来指定本地接口。在阻塞或取消阻塞源时会创建两个结构：

```
struct ip_mreq_source {

    struct in_addr imr_multiaddr;      /* IPv4 D 类组播地址 */

    struct in_addr imr_sourceaddr;    /* IPv4 源地址 */

    struct in_addr imr_interface;     /* 本地接口的 IPv4 索引 */

};
```

```
struct group_source_req {

    unsigned int gsr_interface;      /* 接口索引，或 0 */

    struct sockaddr_storage gsr_group;   /* IPv4 或 IPv6 组播地址 */

    struct sockaddr_storage gsr_source;  /* IPv4 或 IPv6 源地址 */

};
```

如果本地接口指定为 IPv4 的通配地址（`INADDR_ANY`）或 IPv6 的索引0，则由内核选择本地接口。

![img/ab27f092d143e6b7843e67512846270.png](https://example.com/img/ab27f092d143e6b7843e67512846270.png)

在指定的本地接口上离开源组播组。我们用于加入组的相同结构也用于此套接字选项。如果未指定接口（即 IPv4 值为 `INADDR_ANY` 或 IPv6 索引为 0），则离开第一个匹配的组播组。

如果进程加入了一个组但没有显式离开该组，当套接字关闭（显式关闭或进程终止）时，成员关系将自动删除。如果主机上的多个套接字加入同一组，在这种情况下，直到最后一个套接字离开，处理器一直是该组的成员。

原始的 IPv6 组播 API 定义使用 `IPv6_DROP_MEMBERSHIP` 而不是 `IPv6_LEAVE_GROUP`。API 其他部分相同。我们的 `mcast_leave` 函数稍后处理此差异。

# IP_BLOCK_SOURCE, MCAST_BLOCK_SOURCE

阻塞从本地接口上现有的任何组成员中接收来自此源的流量。如果所有加入的套接字都阻塞了该源，系统可以通知路由器该流量是不需要的，可能会影响网络中的组播。它可以用于忽略来自恶意发送者的流量，例如。我们通过 IPv4 的其单播地址或协议无关 API 的接口索引来指定本地接口。在阻塞或取消阻塞源时创建两个结构：

```
struct ip_mreq_source {

    struct in_addr imr_multiaddr;      /* IPv4 D 类组播地址 */

    struct in_addr imr_sourceaddr;    /* IPv4 源地址 */

    struct in_addr imr_interface;     /* 本地接口的 IPv4 索引 */

};
```

```
struct group_source_req {

    unsigned int gsr_interface;      /* 接口索引，或 0 */

    struct sockaddr_storage gsr_group;   /* IPv4 或 IPv6 组播地址 */

    struct sockaddr_storage gsr_source;  /* IPv4 或 IPv6 源地址 */

};
```

如果本地接口指定为 IPv4 的通配地址（`INADDR_ANY`）或 IPv6 的索引0，则由内核选择本地接口。

![img/ab27f092d143e6b7843e67512846270.png](https://example.com/img/ab27f092d143e6b7843e67512846270.png)

（已指定的接口上通过 `IP_ADD_MEMBERSHIP`、`IPv6_JOIN_GROUP` 或 `MCAST_JOIN_GROUP` 加入）。

```
IP_UNBLOCK_SOURCE,MCAST_UNBLOCK_SOURCE
```

取消预先阻塞的源。参数必须与此套接字上的 `IP_BLOCK_SOURCE` 或 `MCAST_BLOCK_SOURCE` 相同。

如果本地接口指定为 IPv4 的通配地址（`INADDR_ANY`）或协议无关 API 的索引0，则取消对第一个源的阻塞。

```
IP_ADD_SOURCE_MEMBERSHIP,MCAST_JOIN_SOURCE_GROUP
```
