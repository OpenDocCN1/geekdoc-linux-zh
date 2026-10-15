
```c
struct sadb_alg {
    uint8_t sadb_alg_id;             /* 来自图 19.8 的 ID */
    uint8_t sadb_alg_ivlen;           /* IV 长度，或零 */
    uint16_t sadb_alg_minbits;       /* 密钥长度 */
    uint16_t sadb_alg_maxbits;       /* 最大密钥长度 */
    uint16_t sadb_alg_reserved;      /* 预留 */
};
```

对于系统支持的每个算法，一个 `sadb_alg` 结构跟在 `sadb_supported` 扩展头之后。图 19.14 显示了注册 SA 类型 `SADB_SATYPE_ESP` 的可能回复。图 19.14 内核返回 `SADB_REGISTER` 命令的数据。图 19.15 我们的第一个示例在密钥管理套接字上注册并打印支持的算法。

## 图 19.15 在密钥管理套接字上注册的程序。

```c
void sadb_register(int type) {
    int s;
    char buf[4096];      /* XXX */
    struct sadb_msg msg;
    int ef;
    int mypid;

    s = socket(PF_KEY, SOCK_RAW, PF_KEY_V2);
    mypid = getpid();

    /* 构建并写入 SADB_REGISTER 请求 */
    bzero(&msg, sizeof(msg));
    msg.sadb_msg_version = PF_KEY_V2;
    msg.sadb_msg_type = SADB_REGISTER;
    msg.sadb_msg_stype = type;
```

- 打开 `PF_KEY` 套接字：我们打开 `PF_KEY` 套接字。
- 存储 PID：由于使用 PID 定位，我们将其存储以便以后比较。
- 创建 `SADB_REGISTER` 消息：像 `SADB_DUMP` 一样，`SADB_REGISTER` 消息不需要任何扩展。我们清空消息并填充所需的字段。
- 显示并写入套接字：我们使用 `print_sadb_msg` 函数显示正在发送的消息，并发送到套接字。
- 等待回复：我们从套接字读取消息并等待注册消息的回复。回复是针对我们的 `SADB_REGISTER` 消息的。它包含支持的算法列表，我们用 `print_sadb_msg` 函数打印。
- 示例：我们在支持 RFC 2367 中描述的若干协议的系统上运行注册程序。

```
mac % register -t ah
发送注册消息：
SADB Message Register, errno 0, stype IPSec AH, seq 0, pid 20746

返回回复：
SADB Message Register, errno 0, stype IPSec AH, seq 0, pid 20746
支持的认证算法：
HMAC-MD5 ivlen 0 bits 128-128
HMAC-SHA-1 ivlen 0 bits 160-160
Keyed MD5 ivlen 0 bits 128-128
Keyed SHA-1 ivlen 0 bits 160-160
Null ivlen 0 bits 0-2048
SHA2-256 ivlen 0 bits 256-256
SHA2-384 ivlen 0 bits 384-384
SHA2-512 ivlen 0 bits 512-512
支持的加密算法：
DES-CBC ivlen 8 bits 64-64
3DES-CBC ivlen 8 bits 192-192
Null ivlen 0 bits 0-2048
Blowfish-CBC ivlen 8 bits 40-448
CAST128-CBC ivlen 8 bits 40-128
AES ivlen 16 bits 128-256
```

当内核需要与对端通信且策略规定需要 SA 但不可用时，内核向注册了所需 SA 类型的密钥管理套接字发送 `SAD_ACQUIRE` 消息，其中包含一个描述内核建议算法和密钥长度的建议扩展。建议可以是系统支持的内容与允许此类通信的预配置策略限制的组合。建议是算法、密钥长度生命周期的列表，按优先级排序。当密钥管理守护进程接收 `SAD_ACQUIRE` 消息时，它执行选择符合内核建议组合的密钥的操作，并将其安装内核。它使用 `SAD_GETSPI` 消息请求内核从所需的范围内选择 SPI。内核对 `SAD_GETSPI` 消息的响应包括创建内核使用的 SPI，以及完成 SA 并使其进入成熟状态的 `SAD_UPDATE` 消息。动态创建的 SA 通常都关联有软生命周期和硬生命周期。当任何一个生命周期过期时，内核发送 `SAD_EXPIRE` 消息，指示是软生命周期还是硬生命周期过期。

# 19.6 总结

密钥管理套字（Key management sockets）用于向内核、密钥管理守护进程以及路由守护进程等其他安全消费者通信 SA（安全关联）。SA 可以通过密钥协商协议静态或动态地安装。动态密钥可以具有关联的生命周期；当达到软寿命（soft lifetime）时，密钥管理守护进程会收到通知。如果在达到硬寿命（hard lifetime）之前没有替换 SA，该 SA 将无法再使用。

进程与内核在密钥管理套字上交换十种消息。每种消息类型都有相关的扩展，有些是必需的，有些是可选的。进程发送的消息都会回到所有其他打开的密钥管理套字，并移除任何包含敏感数据的扩展。

## 练习

19.1 编写一个程序，打开一个 `PF_KEY` 套字并转储它接收的所有消息。

19.2 访问工作组网页 `http://www.ietf.org/html.charters/ipsec-charter.html`，了解 IETF IPsec 工作组创建的用于取代 IKE 的新协议。

# 第 20 章 广播

- 第 20.1 节 引言
- 第 20.2 节 广播地址
- 第 20.3 节 单播与广播的区别
- 第 20.4 节 `dg_cli` 函数使用广播
- 第 20.5 节 竞态条件
- 第 20.6 节 总结
- 练习

# 20.1 引言

在本章中，我们将描述广播，在下一章中，我们将描述多播。到目前为止的所有示例都处理单播：一个进程与恰一个进程通信。事实上，TCP 仅支持单播地址，尽管 UDP 和原始 IP 支持其他范式。图 20.1 显示了不同类型地址比较。

图 20.1. 不同形式的地址。

| 类型 | IPv4 | IPv6 | TCP | UDP | 标识的 IP 接口数量 | 递送到的 IP 接口 |
| --- | --- | --- | --- | --- | --- | --- |
| 单播 (Unicast) | | | | | 一个 | |
| 任任播 (Anycast) | | 尚未支持 | | 一组 | 组中的一个 |
| 多播 (Multicast) | 可选 | | | | 所有 | 组中的所有 |
| 广播 (Broadcast) | | | | | | |

IPv6 在体系地址中增加了任任播（anycasting）。IPv4 版本的任任播从未被广泛部署，其在 RFC 1546 [Partridge, Mendez, and Mullen 1993] 中描述。IPv6 任播定义在 RFC 3513 [Hinden and Deering 2003] 中。任任播允许从一组提供相同服务的系统中选择一个地址（通常是根据某些指标的“最近”的地址）。通过适当的路由配置，主机可以通过向路由协议层注入相同的地址，在 IPv4 或 IPv6 中提供任播服务。然而，RFC 3513 仅允许路由器对地址进行任播；主机可能无法提供任播服务。编写本文时，尚未定义用于使用任播地址的 API。目前正在进行完善 IPv6 任播架构的工作，未来主机可能动态地提供任播服务。

图 20.1 中的要点是：

- 多播在 IPv4 中是可选的，但在 IPv6 中是强制的。
- IPv6 不提供广播支持。任何使用广播的 IPv4 应用程序必须记录下来，以便 IPv6 使用多播代替。
- 多播和单播需要 UDP 或原始 IP 等数据报传输；它们无法与 TCP 一工作。

广播的一个用途是在假设存在服务器但不知道其 IP 地址时，在本地子网上定位服务器。这被称为资源发现。另一个用途是当多个客户端与单个服务器通信时，减少局域网上的网络流量。有许多使用广播实现此目的的应用程序示例。其中一些也使用了多播。

- ARP— 尽管这是一个位于 IPv4 之下的协议，而不是用户应用程序，但 ARP 在本地子网上广播请求，说：“IP 地址为 a.b.c.d 的系统能识别自己的身份并告诉我的硬件地址吗？” ARP 使用链路层广播，而不是 IP 层。
- DHCP— 当客户端尚不知道自己的 IP 地址、子网掩码时，它向本地子网上的服务器或中继请求并向广播地址发送请求。
