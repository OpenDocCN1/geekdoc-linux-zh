

# 与应用层的接口

socket 实现使用了 `proto` 结构体，它定义在 `net/ipv4/udp.c` 中，用于 UDP 访问传输协议的功能：

```c
struct proto udp_prot = {
  name: "UDP",
  close: udp_close,
  connect: udp_connect,
  disconnect: udp_disconnect,
  ioctl: udp_ioctl,
  setsockopt: ip_setsockopt,
  getsockopt: ip_getsockopt,
  sendmsg: udp_sendmsg,
  recvmsg: udp_recvmsg,
  backlog_rcv: udp_queue_rcv_skb,
  hash: udp_v4_hash,
  unhash: udp_v4_unhash,
  get_port: udp_v4_get_port,
};
```

与第 26.3.1 节所示完整的 `proto` 相比，这里缺失的元素（例如 `bind` 和 `accept`）初始化为零，这意味着对于相应的事件没有特定的传输协议处理。

Socket 状态信息存储在第 26.3.1 节提到的 `sock` 数据结构体中。UDP 的简单性意味着不需要特定协议的额外数据，因此 `tp_pinfo` 字段没有 UDP 特有的部分。

`proto` 结构体中引用的大多数函数并不复杂，因此我们在这里简要讨论它们：

- **udp_close():** 在关闭 UDP socket 期间，仅调用函数 `inet_sock_release(2)`（位于 `net/ipv4/af_inet.c`，对所有 `PF_INET` socket 都相同）来释放 socket 数据结构体。从那里，会调用 `udp_v4_unhash()`（如前所述）。
- **udp_connect():** UDP 是一种无连接协议，在应用层接口上的 `connect()` 系统调用（用于面向连接的协议以建立连接）其含义略有不同：它可以用于定义通过 socket 发送的所有 UDP 数据包的终点，这样就不每次都指定。因此，地址和目的端口存储在 `udp_connect()` 内的 `sock` 数据结构体中。这种可选定义的发生事实，通过在 `sock` 结构的 `state` 字段中输入状态标识符 `TCP_ESTABLISHED`（这是“借用”自 TCP）来注册。此外，使用 `ip_route_connect()` 构建了一个路由缓存条目并存储在 `sock` 结构中。该条目在发送数据包时使用，以避免某些开销。
- **udp_disconnect():** 状态被设置为 `TCP_CLOSE`，删除目的地址和目的端口，并释放存储的路由缓存条目。

# 用户数据报协议 (UDP)

- **udp_ioctl():** 此处可以使用 `ioctl()` 系统调用查询发送和接收队列的长度。

- **ip_setsockopt() and ip_getsockopt():** UDP 级别没有 socket 选项，这两个条目直接引用 IP 级别的通用处理例程。（参见 `setsockopt`。）
- **udp_sendmsg() and udp_recvmsg():** 这两个函数实现了 UDP 数据包的发送和接收。第 25.3 节将详细讨论它们。
- **udp_queue_rcv_skb():** 该函数将在第 25.3.2 节描述 `udp_recvmsg()` 时进行讨论。

- **udp_hash():** 在接收 UDP 数据包期间，必须决定将数据包分配给哪个 socket，以便它们能被放在 socket 的接收队列中，稍后由用户进程获取。为了方便这种 socket 的分配，所有 UDP socket 的 `sock` 结构都注册在一个哈希表中，`struct sock "udp_hash[UDP_HTABLE_SIZE]"`。端口号对 `UDP_HTABLE_SIZE` 取模用作哈希值。

在 `proto` 结构体中，哈希条目在 `udp_get_port()` 调用时，使用 `ip_route_connect()` 构建了一个路由缓存条目并存储在 `sock` 结构中。该条目在发送数据包时使用，因此不需要 `udp_hash()`。

- **udp_unhash():** 在释放 socket 时调用此函数，以移除哈希表条目。
- **udp_get_port():** 在需要分配 socket 端口时，调用 `net/ipv4/af_inet.c` 中的函数。UDP 接收 IP 包时使用的由第 14.2 节定义的 `inet_protocol` 结构如下：

```c
static struct inet_protocol protocol = {
    handler:           udp_rcv,
    err_handler:       udp_err,
    next:              IPPROTO_PREVIOUS,
    protocol:          IPPROTO_UDP,
    name:              "UDP"
};
```

`udp_rcv()` 用于接收包：第 25.3 节将详细讨论它。`udp_err()` 处理由 IP 的 ICMP 消息。

为了通过 IP 发送数据包，UDP 使用 `net/ipv4/ip_output` 中的 `ip_build_xmit()`。该函数不接受...

## 发送和接收 UDP 数据报

### UDP 数据报

```c
udp_sendmsg()
```
```c
net/ipv4/udp.c
```

当发送 UDP 数据包时，通过 socket 接口调用 `udp_sendmsg()`：其参数是具有发送 `PF_INET` socket 状态的 socket 结构体、指向指定接收者和负载的 `msg` 结构指针，以及字节字节长度。

首先，本地创建的头部结构从 `msg` 结构的 `name` 元素中获取目的地址和目的端口。如果之前通过 `udp_connect()` 为 socket 分配了默认地址，则不需要显式指定。在这种情况下，使用了来自 socket 结构的信息。源地址和源端口源自 `sock` 结构。此外，它们被存储在 `cookie` 结构中。该结构稍后将用于地址、设备标识符以及 IP 选项（如果适用）。

`msghdr` 结构 `msg_control` 元素中的任何控制消息通过调用 `ipc_msg_send()` 进行处理，结果注册在 `cookie` 结构中。控制消息可修改地址或传递 IP 选项，这些也将注册在 `cookie` 地址中。如果没有指定 IP 选项，将使用存储在 socket 结构中的 IP 选项。

必须获取路由缓存，因此在此之前处理源路由 IP 选项；第一个中间站的地址可能需要代替目的地址。

如果 socket 之前通过 `udp_connect()` 获取了路由缓存，并且在 `udp_sendmsg()` 过程中相应的目的地址没有变化，则现在检查此路由缓存。如果产生负结果，或者目的地址发生了变化，则使用 `ip_route_output()` 生成一个新的路由缓存条目（该条目存储在 socket 结构中）。

最终，数据传输通过调用 `ip_build_xmit()` 启动，该函数提供了 `udp_getfrag()` 或 `udp_getfrag_nosum()` 作为

