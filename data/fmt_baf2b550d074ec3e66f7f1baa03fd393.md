
图 2.40。ARP 请求的嗅探输出。

## 2.18 总结

TCP 是一种面向连接的流协议。它通过 ACK 机制确保发送的每个字节都在另一端接收。

TCP 为小数据包实现了 Nagle 算法。
延迟确认方案通过在 ACK 段中捎带数据来减轻网络负载。

TCP 滑动窗口协议用于批量数据传输。它在任何时间点通过考虑宣告窗口和拥塞窗口来决定数据传输速率。

TCP 扩展（如 SACK、时间戳、mss 和窗口缩放）提供了增强性能的可靠性。

TCP 拥塞控制算法使用两个 TCP 状态变量来控制数据传输速率：发送拥塞窗口 `cwnd` 和慢启动阈值 `ssthresh`。

IP 是一种无状态协议，携带了大部分互联网流量。
IP 数据报通过每次跳过一个路由器在互联网中进行路由。

每个路由器都维护一个路由表，保存关于给定目的地的下一跳路由的所有信息。

`netstat` 命令用于显示内核路由表。
`traceoute` 是一个强大的工具，用于跟踪数据包到达目的地所经过的路径。

互联网使用 ICMP 消息报告错误。

ARP/RARP 设计用于从协议地址解析硬件地址，反之亦然。

# 套接字的内核实现

Linux 支持支持符合 OSI 模型的不同通信协议。BSD socket 是不同协议族的一个接口。兼容 BSD 的 socket 在用户进程和内核中的网络协议栈之间提供了统一的 socket 接口。BSD socket 是 Linux 支持的不同类型 socket 族的框架。BSD socket 的概念与 VFS（虚拟文件系统）层非常相似，VFS 只是一个为用户提供不同文件系统/管道/设备/socket 通用接口的框架，而无需内核内部是如何组织的。Linux 支持这些不同的协议族。例如，协议模块使用通用的 socket 接口进行分组。对于 `PF_INET`、`PF_IPX`、`PF_PACKET` 等协议族以及 `SOCK_STREAM` 和 `SOCK_DGRAM` 等 socket 类型，如图 3.1 所示。

BSD socket 框架规定了标准，每个协议族都需要遵循这些标准。这些标准无非是一组函数，如 `create`, `bind`, `listen`, `accept`, `connect`, `write`, `ioctl`, `setsockopt`, `getsockopt` 等，这些是特定于协议的数据结构。

TCP/IP Architecture, Design, and Implementation in Linux. By S. Seth and M. VenkatesCopyright 2008 the IEEE Computer Society

## 套接字的内核实现

使用文件描述符通过 VFS 层在内核中访问。

用户空间

内核

VFS

Socket 层

![](img/b3f231108facab5be0138b2cfd3f681a_128_0)

| AF_MAX | AF_FILE | PF_INET | PF_UNIX | AF_LOCAL | AF_AX5 | PF_IPX | AF_APPALK | AF_NET | AF_BRIDGE | AF_ATVC | AF_25 | AF_INET | AF_ROCENT | AF_NETLINK | AF_ROUTE | AF_IRDA | AF_BLETOOTH | AF_ECONET |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | : |
| SOCK_STREAM (IPPROTO_TCP) | SOCK_DGRAM (IPPROTO_UDP) | SOCK_RAW (IPPROTO_IP) | |

![](img/b3f231108facab5be0138b2cfd3f681a_128_1)

图 3.1。套接字架构。

在内核中 socket。讨论将主要基于 `PF_INET`（特定于 ipv4）协议族。解释了与 `PF_INET` 相关的各种重要函数和数据结构。

### 3.1 SOCKET 层

BSD socket 与 `sock` 结构关联，该结构包含特定于协议族的字段。`sock` 数据结构中的字段指向协议-

## VFS 与 SOCKET

[PAGE 129]

## SOCKET 的内核实现

该进程的 `task_struct` 对象的 `files` 字段是指向任意 `files_struct` 的指针。`file` 对象的 `f_d` 字段是指向 `dentry` 对象的指针。`dentry` 的 `d_inode` 字段是指向与文件相关的 `inode` 对象的指针。`inode` 是任何文件类型的通用结构。socket 也被视为特殊字段，通过 `inode` 对象的 `i_sock` 字段进行标识。`u` 是 VFS 子系统支持的所有文件类型的联合体。可以通过联合体 `u` 中的 `socket_i` 字段访问 socket 对象。

从这里开始，你可以很容易地访问到一个 socket 对象。socket 有一个指向协议特定信息的指针，一旦 socket 拥有一个由 `prot` 字段指向的协议特定操作集合的指针。

`socket_create()` 找到特定于协议族的 `create()` 函数并调用它初始化与 BSD socket 关联的结构体。`net_families[]` 是一个类型为 `net_proto_family` 的数组，通过协议族进行索引。该结构包含两个主要字段：

```
int family

int (*create)(struct *sock, int protocol)
```

`family` 字段包含协议族，`create` 是一个指向特定于协议的 socket 创建函数的函数指针。`net_family[]` 包含已注册协议族的 `net_proto_family` 数据。`socket_register()` 函数获取如 c 3.1 所示的协议族完成的 `net_proto_family` 注册。INET 族 `family_inet_` 已经注册。

从现在起，一切都将与协议族非常相关。因此，我将使用 `PF_INET` socket 类型在提到它之前处处解释 socket 层。因此，`sock_create()` 找到 `PF_INET` 协议族的入口。

```
net/socket.c

1620 int sock_register(struct net_proto_family *ops)

1621 {

1622     int err;

1623

1624     if (ops->family == NPROTO) {

1625         prink(KERN_CRIT, "protocol %d > NPROTO(%d\n", ops->family, NPROTO);

1626         return -ENOBUSY;

1627     }

1628     net_family_write_lock();

1629     err = -EEXIST;

1630     if (!families[ops->family]) {

1631         net_families[ops->family]=ops;

1632         err = 0;

1633     }

1634     net_family_write_unlock();

1635     return err;

1636 }
```
