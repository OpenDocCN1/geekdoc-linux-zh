
```c
/***************************************************************/
/** IPv6 Packet definition ***/
/***************************************************************/
union IPv6_Address
{
    unsigned char u8[16];
    unsigned short int u16[8];
    unsigned long int u32[4];
    unsigned long long int u64[2];
};
struct IPv6_Header
{
    unsigned int version:4;         /* The IP version (6) */
    unsigned int priority:4;
    unsigned int flow_label:24;
    unsigned int payload_len:16;    /* bytes following header */
    unsigned int next_header:8;     /* protocol (6 for TCP) */
    unsigned int hop_limit:8;       /* same as TTL */
    union IPv6_Address source;
    union IPv6_Address dest;
};
```

只有三个字段需要更多解释。`priority` 字段是一个实验性字段，它设置数据包的优先级。如果网络变得拥塞，路由器可能会保留或丢弃较低优先级的数据包。默认情况下，所有数据包都是 `priority` 零。

`flow_label` 字段也是实验性的，并与 `priority` 协同工作。流是由源到目的地通过一系列路由器移动的数据包序列。`flow_label` 帮助路由器确定任何特殊处理。一个消息只有一个 `flow_label`；一旦选定，流值对于流中的所有数据包都不会改变。你可以在绑定套接字地址时，使用 `sockaddr_in6` 中的可选 `sin6_flowinfo` 字段来设置 `priority` 和 `flow_label`。

最后一个字段，`payload_len`，可以为零，以表示巨大的数据包。一个一吉比特（甚至 100Mbit）网络发送小数据包（小于 100KB）是带宽的浪费。将此字段设置为零，并在头部和载荷之间包含一条额外的记录。以下定义按网络字节序显示：

```c
/* ************************************************** */
/** Jumbo (extra large) packet option definition    ***/
/* ************************************************** */
struct Jumbo_Payload
{
    unsigned char option;   /* equals 194 */
    unsigned char length;   /* equals 4 (bytes) */
    unsigned long bytes;    /* payload length */
};
```

使用此选项，你可以发送最大为 4GB 的数据包。对于一小段时间来说，这还不错。

## 将 ICMPv6 套接字转换为 IPv6

ICMPv6 头部的物理布局 [RFC2463] 与 ICMPv4 相同，但 `type` 和 `code` 字段发生了相当大的变化。例如，回显请求和回显应答有了新的编号（分别为 128 和 129）。一些代码不再受支持。关于代码的完整列表，请参见附录 A“数据表”。

## 新的多播协议

另一项架构变更涉及 IPv6 管理多播的方式。它必须在三个方面发挥作用：硬件、寻址和路由。

正如第 17 章“通过多播、广播和 Mbone 共享消息”所述，多播必须与硬件协同工作，指示硬件接收并非其自身以太网或 MAC 地址的数据包。这些地址取决于所请求的多播地址——IPv6 取地址的最后四个字节，并创建具有 `33:33` 前缀的 MAC 地址。例如，如果请求的多播地址是 `FF02::725:6832:D012`，则生成的 MAC 地址将是 `33:33:68:32:D0:12`（忽略 725）。

IPv6 的多播寻址与 IPv4 略有不同。第一个字节 `FF` 指示这是一个多播地址，但下一个字节包含关于多播组类型和路由细节的附加信息，每个信息宽 4 位。

第一个子字段有四个位标志，每个代表一个特征。最低有效位（第 0 位）为零 (0) 表示已知的多播地址。为一 (1) 表示瞬时地址。其他三个位目前保留。

另一个子字段同样有四位，指示地址的范围（本地或全局地址）。数字越高，范围越广。另一方面，IPv4 仅使用 TTL 来确定范围（较小的数字会在到达全局地址之前过期）。此外，如第 17 章所述，IPv4 已分配特定的地址块用于本地、站点或全局范围。表 19.2 定义了不同的范围。

| 范围 | 范围值 | 描述 |
| :---- | :---- | :---------- |
| 1 | 节点 | 同一主机上的本地（类似于 `127.0.0.1`）。 |
| 2 | 链路 | 消息保持在路由器的组内。路由器从不允许这些消息通过。 |
| 5 | 站点 | 由网络管理员定义，消息保持在站点的本地范围内。 |
| 8 | 组织 | 由网络管理员定义，消息保持在组织的本地范围内。 |
| 14 | 全局 | 所有路由器允许消息通过全局网络（直到它们过期）。 |

最后，路由规则（如第 17 章所述）保持不变。IPv6 使用 IPv4 的可选 IGMP 将加入或退出多播组的请求传递出去。由于两者都使用 MAC 地址获取多播消息，IPv6 无需定义超出 IPv4 实现之外的内容。

加入 IPv6 多播组的程序几乎与 IPv4 相同，但你需要使用不同的结构来选择地址：

```c
/* ********************************** */
/** IPv6 multicast structure definition **** */
/* ********************************** */
struct ipv6_mreq
{
    struct in6_addr ipv6mr_multiaddr; /* IPv6 multicast addr */
    unsigned int ipv6mr_interface; /* interface number */
};
```

第一个字段 `ipv6mr_multiaddr` 是广播消息地址。你在此字段中放置 IPv6 地址（例如，`FF02::10`）。下一个字段是接口号：0 表示所有接口，1 表示第一个接口（`eth0`），依此类推。

要启用 IPv6 多播，请使用以下代码片段：

```c
/***** */
/** Join a IPv6 multicast group **** */
/***** */
const char *GroupID = "FF02::4590:3A0";
struct ipv6_mreq mreq;
if ( inet_pton(GroupID, &mreq.ipv6mr_multiaddr) == 0 )
    panic("address (%s) bad", GroupID);
mreq.ipv6mr_interface = 0; /* any interface */
if ( setsockopt(sd, SOL_IPV6, IPV6_ADD_MEMBERSHIP, &mreq, sizeof(mreq)) != 0 )
    panic("Join multicast failed");
if ( setsockopt(sd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on)) != 0 )
    panic("Can't reuse address/ports");
```

可以看出，代码与 IPv4 多播代码非常相似。

## 摘要：将代码移向未来

IPv6 解决了目前 IPv4 寻址结构中的局限性。通过扩展寻址范围几个数量级，IPv6 看起来是互联网明确的未来。仍处于初创阶段，寻址分配已采用标准网络，如 IPX。它已在欧洲和远东网络中获得支持。

随着扩展地址的出现，物理外观发生了变化，并包含了一些简写表示法以便于表示和编程。只要遵循本文中的指南和示例，将程序从 IPv4 移植到 IPv6 是直接的。`socket()` 系统调用真正帮助网络编程适应不同的网络。

IPv6 网络包含 IPv4 网络，因此所有 IPv4 地址仍然有效。大多数支持 IPv6 的操作系统很可能使用双栈来支持和转换这两个网络。双栈中的寻址方案和转换允许某些隐式协作——支持所需的重编程很少。
