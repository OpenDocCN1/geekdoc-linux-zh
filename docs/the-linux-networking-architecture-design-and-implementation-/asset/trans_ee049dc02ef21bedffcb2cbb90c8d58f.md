

# 第 25 章 用户数据报协议 (UDP)

这是一个获取数据的函数，取决于数据包头部的校验和是否包含有效负载。这里使用的参数还包括 `udpfetchhdr` 和 `ipcm` 结构、路由缓存项、来自 `msghdr` 结构的标志，以及 UDP 数据包的总长度。

接后的讨论仅考虑 `udp_getfrag()`，因为 `udp_getfrag_nosum()` 相同的功能，但在跳过校验和计算时更为简单。

```
udp_getfrag() net/ipv4/udpc
```

对于它生成的每个 IP 分片，`ip_build_xmit` 会调用回调函数 `udp_getfrag()` 来获取所需的有效负载。由 `udp_sendmsg()` 填充的 `udphdr` 结构指针是传递的参数之一，此外还有目标地址和所需的数据量。

实际的大部分工作由定义 `net/core/uvec.c` 中的函数 `csum_fromend()` 完成。该函数不仅直接从用户地址位置拷贝 `uvec` 结构引用的数据，还计算了校验和。校验和计算的结果存储在每一步 `udphdr` 结构的 `weck` 元素中。下一步使用该结果作为起始值，以便校验和覆盖整个数据。

第一个分片必须最后创建，因为它包含了带有校验和的 UDP 头部。留给 `ip_build_xmit()` 来确保正确的顺序：`udp_getfrag()` 通过偏移量零来识别第一个分片。它将校验和计算扩展到数据包头部和 IP 伪头部，并最终通过插入校验和完成数据包头部，最后将其拷贝到数据包开头。

# 接收 UDP 数据报

```
udp_recv() net/ipv4/udpc
```

一旦 IP 接收到 UDP 数据包，它就会将其以 `sk_buf` 指针的形式传递给 `udp_recv()` 进行进一步处理。在检查了数据包长度并对伪头部计算了校验和后（如果数据包头部不包含校验和，或者校验和是由接口硬件计算的，这会被注册在 `sk_buff` 中），`udp_recv()` 直接将多播和广播数据包转发到 `udp_mcast_deliver()`，该操作会在后续被延迟执行。

最重要的任务是将数据包分配给套接字，以便它可以被放入该套接字的队列中，直到被用户获取。此任务由 `udp_recv()` 用的函数 `udp_v4_lookup()`（或 `udp_v4_lookup_longway()`）处理。该函数查找 `udp_hash` 表，并从链接列表中匹配数据包的套接字中，选择地址、目的端口和输入接口信息最具体的套接字。

> 如果套接字结构中的 `no_check` 标志为空，则会计算校验和，默认情况下如此。此标志可以通过 `SOL_SOCKET` 级别的套接字选项 `SO_NO_CHECK` 设置。

# 25.3 发送和接收 UDP 数据报 521

当找到套接字后，会调用 `udp_queue_rcv_skb()`，继而调用 `sk_queue_rcv_skb()`，后者将数据包插入该套接字的队列中。前提是校验和计算可以成功完成。对于校验和错误的数据包不会生成 ICMP 消息。

```
udp_mcast_deliver()                               net/ipv4.udpc
```

类似于 `udp_v4_lookup()`，`udp_mcast_deliver()` 会搜索匹配的接收者。然而，它并不是选择最匹配的单个套接字，而是所有与目的端口（如果包含此信息）、地址和输入接口匹配数据包的套接字。所有这些套接字都会接收数据包的副本。副本使用 `skb_clone()` 创建，并像 `udp_queue_rcv_skb()` 一样进行交付。

```
udp_recvsmsg()                               net/ipv4.udpc
```

如果用户处理其中一个接收数据包的系统调用，它所映射的套接字接口会调用函数 `udp_recvsmsg()`。这从作为参数传递的套接字的接收队列中移除 `sk_buff` 结构，将其解释为 UDP 数据包，并将包含的有效负载（如果有必要也包括数据包头部信息）以接收者传递的 `msghdr` 结构的形式返回。如果队列当前为空，根据规范，进程必须处于等待状态，或者通过适当的 fetch 终止调用。

从接收队列队列中获取 `sk_buff` 结构、等待其到达以及拷贝数据的过程不仅是 UDP 所需要的，在其他几个地方也是必须的。因此，`net/core/datagram.c` 文件包含了这些用途的通用函数，并被 `udp_recvsmsg()` 使用：

- `skb_rcv_datagram()` 用于获取 `sk_buff`。这是通过 `skb_dequeue()`（如果提供的标志显示应该读取但不移除，则使用 `skb_peek()`）完成的。如果可用 `sk_buff`，则返回它；否则，如果允许阻塞，套接字注册中实现的 `wait_for_packet()` 函数会将进程注册为套接字的等待进程，并调用 `schedule()` 临时获取控制权。

- `skb_copy_datagram_ioc()`（或 `skb_copy_and_datagram_iovec()`）由 `udp_recvsmsg()` 调用，将有效负载拷贝到数据包的 `msghdr` 结构的 `skb_iov` 元素中，以便在过程中计算并验证校验和。

- `skb_free_datagram()` 在 `udp_recvsmsg()` 拷贝地址信息后释放 `sk_buff` 结构，例如当 IP 选项被接管到控制消息时（通过调用函数 `ip_cmsg_recv()`）。

# 第 26 章

## 套接字的概念

### 26.1 引言

套接字的抽象被引入（基于 BSD 版本的 UNIX，该接口首次在此使用；也称为 BSD 套接字），旨在方便网络应用程序的编程。应用程序可以使用此统一接口在网络上发送或接收数据。该接口对于所有协议看起来都是相似的，通过匹配三个参数（族、类型和协议）来选择所需的协议套接字。第 27 章完整概述了所有可用的协议族（family）。它还讨论了应用程序如何使用套接字接口。相比之下，本章概述了 Linux 内核中套接字的实现情况。

图 26–1 概述了套接字支持如何集成到 Linux 内核的协议实现中。BSD 套接字接口为上层应用程序提供了一个统一接口；不同的协议族通过特定协议的套接字进行区分。最重要的协议族之一 `PF_INET`（协议族）将在接下来的章节中描述。此外，近期的 Linux 版本中的 `PF_PACKET` 套接字提供了一种直接访问设备发送数据的优雅方法。数据包套接字的使用在第 9 章介绍。26.3 节详细介绍了数据包套接字。相比之下，Netlink 套接字不是用于网络传输，而是用于配置架构的不同部分。要配置的部分如图 26–1 所示。

## 26.2 BSD SOCKETS

Linux 内核仅提供一个套接字系统调用，应用程序的所有套接字调用都映射到此调用。函数 `as long sys_socket_call(int call, unsigned long *args)` 定义在 `net/socket.c` 中。此外，编号在 `include/asm/unistd.h` 中分配（`#define __NR_socketcall 102`），并添加到 `arch/i86/kernel/entry.S` 中的系统调用表中。要处理的套接字函数可以在 `call` 参数中指定。允许的参数定义在 `include/linux/net.h` 中：`SYS_SOCKET`、`SYS_BIND`、`SYS_CONNECT`、`SYS_LISTEN`、`SYS_ACCEPT`、`SYS_GETSOCKET`、`SYS_GETPEERNAME`、`SYS_PAIR`、`SYS_SEND`、`SYS_RECV`、`SYS_SENDTO`、`SYS_RECVFROM`、`SYS_SHUTDOWN`、`SYS_SETSOCKOPT`、`SYS_GETSOCKETOPT`、`SYS_SENDMSG`、`SYS_RECVMSG`。在用户空间的库内部，带有特定参数的 `sys_socketcall()` 被映射到独立函数（例如 `sys_socketcall(SYS_SOCKET,...)` 变为调用 `socket(...)`）。

```
sys_socketcall() // net/socket.c
```

在 `sys_socketcall()` 函数中使用 `switch` 命令选择要调用的函数，并使用 `copy_from_user()` 命令将函数的参数拷贝到向量 `unsigned long a[6]`：

```
if (copy_from_user(a, args, nargs[call]))
    return -EFAULT;

a0=a[0];
a1=a[1];

switch(call)
{
    case SYS_SOCKET:
        err = sys_socket(a0,a1,a[2]);
        break;
```

