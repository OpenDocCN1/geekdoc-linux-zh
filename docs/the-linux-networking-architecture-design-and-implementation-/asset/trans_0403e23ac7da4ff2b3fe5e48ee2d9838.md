
# 528 第 26 章 套字的概念

在 TCP 中，`tcp_func` 结构（定义在 `net/ipv4/tcp_ipv4.c` 的 `include/net/tcp.h` 中）包含了 TCP 特有的函数，并通过入口 `tp_pinfo_af_tcp_specific` 供套字结构使用。

TCP 的发送函数（`tcp_transmit_skb()`——参见第 24 章）访问从 IP 层（网络层）可用的发送函数 `ip_build_xmit`（见第 14 章）。然而，这种方法并不统一（例如，UDP 没有实现 `init()`，而是直接访问 `ip_build_xmit()`）。

## 26.2 PF_PACKET 套字

PF_PACKET 套字是一种允许应用程序访问网络设备的套字类型。基本思想是让应用程序在 PF_PACKET 套字上发送数据包类型（例如类型为 `ETH_P_PPP` 的连接管理数据包）。这意味着所有此类入数据包都直接交付到指定的网络设备；反之，通过此套字发送的所有包都直接发送到指定的网络设备。因此，内核内部不发生协议处理，你可以在用户空间实现网络协议。在接口处，应用程序将族设置为 `PF_PACKET`。此外，选择了 `PF_INET`，并且必须指定类型 `SOCK_PACKET`。

对于 `PF_INET` 套字，当 PF_PACKET 支持启动时会导出 `create()` 函数（在此情况下为 `net/packet/af_packet.c` 中的）。该函数将 PF_PACKET 套字的函数与 BSD 套字注册。此外，`register_netdev_notifier()` 和 `packet_notifier()` 函数用于为所有与 PF_PACKET 套字注册的数据包调用 `dev_add_pack()` 函数（`net/core/dev.c`）。这意味着在指定的网络设备中为所有所需数据包类型的入数据包安装了处理器。该处理器将数据包转发到 `packet_rcv()` 函数进行处理，如第 5 章所述。

在接下来，我们将简要介绍发送和接收函数。

```
packet_sendmsg()                               net/packet/af_packet.c
```

套字结构指针和要发送的消息被传递给此函数。接下来，必须选择用于此传输的网络设备。这可以通过套字指定的源地址来实现，除非设备已由于 `bind()` 操作被添加到套字结构的 `tp_pinfo.af_packet->index` 字段中；因此，消息被拷贝到 `skb` 并通过 `dev_queue_xmit()` 函数直接发送到网络设备，而不使用 PF_PACKET 套字底下的协议。

```
packet_rcv()                                       net/packet/af_packet.c
```

当接收注册的数据包类型时，网络设备提供一个包含接收数据的 `sk_buff` 指针给 `packet_rcv()` 函数。下一步填充 `sk_buffer` 结构的其他字段。随后，函数 `_skb_queue_tail()` 将 `sk_buff` 插入关联套字的接收队列中。接下来，等待套字的进程必须被通知。这是通过套字结构的指针 `data_ready()` 实现的，它在结构初始化时绑定到函数 `sock_def_readable()`。

```
sock_def_readable()                               net/core/sock.c
```

此函数通知进程已接收数据。为了目的，必须区分两种情况：如果应用程序在套字处处于阻塞等待，则使用 `wake_up_interruptible()` 将相关进程添加到可执行进程列表中。在非阻塞等待的情况下，描述符字段探测并转换相关进程。这是通过函数 `sk_wake_async()`（`include/net/sock.h`）实现的，它访问之前提到的 BSD 套字的 `fasync_list`。

## 26.3 PF_NETLINK 套字

PF_NETLINK 套字用于在内核部分和用户空间之间交换数据。指定的协议族为 `PF_NETLINK`，类型为 `SOCK_RAW` 或 `SOCK_DGRAM`。协议可以从多个选项中选择（参见 `include/net/netlink.h`）：
