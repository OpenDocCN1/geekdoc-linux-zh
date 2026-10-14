
为了查看如何使用 `rtnetlink`，让我们来看示例。如果运行的实用程序要在内部路由表中添加路由，它会调用 `recvmsg` 并传递 `nlmsghdr` 指针，并将 `nlmsg_type` 字段设置为 `RT_NEWROUTE`。`socket` 层会将消息汇集到 `sk_buff` 结构中并发送到 `netlink` 协议，随后将其将其到 `PF_NETLINK` `socket` 的接收队列。`rtnetlink` 中的 `netlink_rcv_skb` 函数在消息从 `socket` 出队时获取该消息。

```c
extern __inline__ int netlink_rcv_skb(struct sk_buff *sk_buff);
```

在该函数中，我们所的工作是从 `sk_buff` 的数据部分获取 `nlmsghdr` 并调用 `netlink_rcv_skb` 函数。

```c
static __inline__ int netlink_rcv_skb(struct sk_buff *sk_buff, struct nlmsghdr *nlh);
```

`netlink` 模块还为协议提供了一个初始化函数 `netlink_proto_init`。

该函数通过调用 `sock_register` 注册 `netlink` 族操作。

协议。在现代网络协议栈实现中，该框架与协议是独立的。网络框架包括一个网络层与数据链路层之间与设备无关的接口，多个协议可以同时运行。该框架还提供了一种与设备无关的网络地址到物理地址转换机制。尽管 Linux 没有显式地将其网络基础设施称为“框架”，但它本质上确实如此。虽然其他章节将讨论协议在 Linux 中是如何运行的，但在本章中，我们将检查 Linux 框架中的某些组件。

## 6.2 数据包处理胶水层 (Packet Handler Glue)

Linux 提供了一种方法，供网络和链路协议动态注册其输入函数，以便它们接收输入数据包。Linux 还提供了注册机制，让每一层的协议向其上层以及套字层（`socket layer`）注册。与其他协议栈实现方式一样，Linux 必须有一种方法让每层都能向下的层隐藏信息和实现细节。在本节中，我们将讨论连接网络接口到网络层的“胶水层”。我们将讨论协议如何从网络接口接收数据包。Linux 提供了一种调度分发机制，使得网络接口驱动程序可以根据协议将传入的数据包传递给下一层。

例如，如果数据层（第 2 层）正在处理传入的数据，则数据包必须被高效地分发给任何接收到该数据包的协议（如 `IP`、`ARP` 或 `IPv6`）处理。解复用机制基于链路层中的 2 字节数据包。表 6.1 显示了链路层协议字段中 2 字节字段定义的多数协议，这些定义在 `linux/include/linux/if_ether.h` 中。表 6.1 中的某些数字并非官方协议号。对于官方数字，请参考互联网分配编号机构（IANA）[IAPROTO3]。

表 6.1：链路层协议字段值

| 协议 | 值 | 描述 |
| :--- | :--- | :--- |
| `ETH_P_LOOP` | 0x0060 | 以太网环回数据包 |
| `ETH_P_PUP` | 0x0200 | Xerox PUP 数据包 |
| `ETH_P_PUPAT` | 0x0201 | Xerox PUP 地址传输数据包 |
| `ETH_P_IP` | 0x0800 | 网际协议 (IP) |
| `ETH_P_X25` | 0x0805 | CCITT X.25 |
| `ETH_P_ARP` | 0x0806 | 地址解析协议 (ARP) |
| `ETH_P_BPQ` | 0x08FF | G8BPQ AX.25 以太网数据包。该协议非官方。 |
| `ETH_P_IEEEPUP` | 0x0a00 | Xerox IEEE802.3 PUP 数据包 |
| `ETH_P_IEEEPUPAT` | 0x0a01 | Xerox IEEE802.3 PUP 地址传输数据包 |
| `ETH_P_DEC` | 0x6000 | DEC 分配端口 |
| `ETH_P_DNA_DL` | 0x6001 | DEC DNA 转储/加载 |
| `ETH_P_DNA_RC` | 0x6002 | DEC DNA 远程控制台 |
| `ETH_P_DNA_RT` | 0x6003 | DEC DNA 路由 |
| `ETH_P_LAT` | 0x6004 | DEC LAT |
| `ETH_P_DIAG` | 0x6005 | DEC 诊断 |
| `ETH_P_CUST` | 0x6006 | DEC 客户 |
| `ETH_P_SCA` | 0x6007 | DEC 系统通信架构 |
| `ETH_P_RARP` | 0x8035 | 反向地址解析数据包 |
| `ETH_P_ATALK` | 0x809B | AppleTalk DDP |
| `ETH_P_AARP` | 0x80F3 | AppleTalk AARP |
| `ETH_P_8021Q` | 0x8100 | 802.1 VLAN 扩展头部 |
| `ETH_P_IPX` | 0x8137 | DI 之 IPX |
| `ETH_P_IPV6` | 0x86DD | IPv6 |
| `ETH_P_PPP_DISC` | 0x8863 | PPPoE 发现消息 |
| `ETH_P_PPP_SES` | 0x8864 | PPPoE 会话消息 |
| `ETH_P_ATMMPOA` | 0x884c | ATM 之上的多协议 |
| `ETH_P_ATMFATE` | 0x8884 | 以太网上基于帧的 ATM 传输 |

Linux TCP/IP 栈的初始化是一个复杂的过程，而初始化部分之一就是协议注册。栈的内部注册实际上由三部分组成。第一部分涉及注册网络层协议（通常称为*数据包处理器*），这些协议从网络接口设备接收数据包。注册过程的第二部分涉及将传输层协议注册到网络层 IP，以便请求相应的 UDP 或 TCP 等传输层。第三部分涉及将协议注册到套字层（`socket layer`），将在第 5 章中详细讨论。第 6.7 节包含了关于协议解复用的详细信息，以及传输层协议如何告诉 IPv4 它们拥有特定类型的数据包。第 4 章详细描述了驱动程序注册过程、网络设备结构以及执行顺序。

## 6.3 TCP/IP 栈初始化

根据 OSI 网络模型，网络层详细涉及网络寻址和数据包路由的语义。然而，某些操作系统和 TCP/IP 栈将网络层定义为任何从接口驱动程序接收数据包的内容。Linux 将所有从接口驱动程序接收数据包的协议定义为数据处理器。Linux 提供的协议管理和注册设施称为 `taps`。有时在 Linux 中，我们将数据处理器称为 `taps`，这可能更准确，因为并不是所有数据处理器都会接收数据包。当数据包到达时，将根据头部的类型字段进行解复用并分发给数据处理器。

### 6.3.1 数据处理器初始化与注册

Linux 提供了两个用于注册和注销数据处理器的函数。注册由数据处理器的初始化程序调用，以便其准备接收传入的数据包。注册是基于类型的，因此数据处理器只会接收它应该接收的数据包。当数据包到达时，将根据头部的类型字段进行解复用并分发给数据处理器。这种解复用过程将在第 6.6 节描述。

数据处理器注册和注销的参数声明在 `linux/include/linux/netdevice.h` 中，定义在 `linux/net/core/dev.c`。这两个函数都接受一个指向 `packet_type` 结构的指针作为参数。

```c
struct packet_type {
    unsigned short               type;
    struct net_device         *dev;
};
```

第一个字段 `type` 与协议类型相同，对应字节序的以太网头部类型字段。表 6.1 显示了协议类型列表。该字段 `dev` 是指向我们想要接收数据包的网络接口的 `net_device` 结构指针。如果它为 `NULL`，我们将从任何网络接口接收数据包。

下一个字段指向该协议类型的协议处理函数。当协议类型字段匹配成功时，网络队列层会调用此函数。

```c
int (*func) (struct sk_buff *, struct net_device *, struct packet_type *);
void       *af_packet_priv;
```

`List` 指向数据包处理程序列表。当数据包处理程序被注册时，该字段会被填充。

```c
struct list_head  list;
```

两个函数中的第一个 `dev_add_pack` 用于注册数据包处理程序。

```c
void dev_add_pack (struct packet_type *pt);
```
