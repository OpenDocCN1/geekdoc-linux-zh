
在应用程序出于任何目的使用操作系统的任何网络函数之前，必须调用 `socket`。`socket` 返回一个标识符，也称为套接字。该标识符本质上是一个文件描述符，其用法与 `open` 调用返回的文件描述符相同。换句话说，可以通过指定套接字来完成 `read` 和 `write` 调用。

`socket` 用的第一个参数 `domain` 指定了通过此调用返回的套接字访问哪种协议族。它应该被设置为 Linux 中使用的协议族之一（如表 5.1 所示），通常是 `AF_INET`。在 Linux 以及本书的任何地方，我们交替使用*协议族*和*地址族*。BSD 派的实现区分了这二者，但 Linux 没有区分。为了与 BSD 兼容，协议族用以 `PF_` 开头的名字定义，地址族的名字以 `AF_` 开头。

套接字 API 提供地址和端口，重要的是，TCP/IP 与其他网络协议一样，始终认为通过套接字 API 传递的端口和 Internet 地址处于网络序。网络序等于字节序或摩托罗拉字节序。Linux 与兼容 Unix 的操作系统不同，提供了一set转换函数，用于在不同长度的整数之间转换主机字节序和网络序。有关这些函数的列表，请参见 Linux man 页面 `byteorder(3)`。

下一个套接字 API 调用 `bind` 是由想要在套接字上注册本地地址的应用程序调用的。本地地址通常由端口号组成，被称为套接字的名称。

（此处重复修正）：`bind` 通常用于应用程序服务器与套接字建立端点或端口和地址组合。本地地址通常由端口号组成，被称为套接字的名称。发送 UDP 数据包或数据报的应用程序不需要调用 `bind`。如果它们想知道数据来自哪里，就应该调用 `bind`。`listen` API 函数由 `SOCK_STREAM` 或 TCP 调用，以告知套接字层已准备好在套接字 `s` 上接收连接请求。端口号和本地 IP 地址以 `sockaddr` 结构的形式指定在 `myaddr` 中。

`accept` 只有当应用程序准备好接受连接请求时才调用。它为被接受的连接返回一个新的套接字。请求连接的对端地址是放在 `addr` 指向的 `sockaddr` 结构中。在调用 `accept` 之前，`addr` 应该指向一个包含 `struct sockaddr` 大小的变量。函数返回后，`addrlen` 指向 `addr` 中新地址的长度。

```c
int accept(int s, struct sockaddr *addr, socklen_t *addrlen);
```

socket 调用 `connect` 主要用于客户端应用程序通过 TCP 协议与服务器建立面向连接或 `SOCK_STREAM` 类型的连接。

```c
int connect(int s, const struct sockaddr *serv_addr, socklen_t addrlen);
```

`servaddr` 指定了调用者想要连接的服务器地址和端口，`addrlen` 是 `struct sockaddr` 的长度。当与 TCP 使用时，它实际上会导致 TCP 启动对端之间的连接。也可以与 `SOCK_DGRAM` 使用，在这种情况下它并不会实际导致连接；相反它指定了对端地址信息，以便通过 socket `s` 使用 `send`。

socket 调用 `socketpair` 不用于 TCP/IP，因此此处不进行讨论。它用于 `AF_UNIX` 域，进行系统内的进程间通信。稍后我们在讨论 socket 层的内部结构时，将会看到 socket 的部分复杂性是因为大多数基于 `AF_UNIX` 的 socket 用于进程间通信。

接下来三个调用——`send`、`sendto` 和 `accept`——分别从 `s` 向对端 socket 传输数据。`send` 用于之前已调用过已连接的 socket（无论是服务器还是客户端）。`sendto` 用于任何 `SOCK_DGRAM` socket，因为它包含了 `send` 的参数以及 `to` 参数，后者指定了目的地址。

```c
int send(int s, const void *msg, size_t len, int flags);

int sendto(int s, const void *msg, size_t len, int flags,
const struct sockaddr *to, socklen_t tolen);

sendmsg(int s, struct msghdr *msg, int flags);
```

通常情况下，这些调用将一直阻塞，直到有足够的空间接收指定长度的数据包。`flags` 参数可以包含以下任何一个值：见表 5.3 所示的所有 socket 及其值。

> 表 5.3: Socket API 函数的 Flags 值

| Flag | Value | Purpose |
|---|---|---|
| MSG_OOB | 1 | 请求带带带数据。 |
| MSG_PEEK | 2 | 返回接收队列头部的数据但不将其移除。 |
| MSG_DONTROUTE | 4 | 不对此消息路由。通常在 ping 工具中发送 ICMP 包时使用。 |
| MSG_TRYHARD | 4 | TCP/IP 不使用。`MSG_DONTROUTE` 的同义词。 |

| 表 5.3: Socket API 函数的 Flags 值 |
| Flag | Value | Purpose |
| --- | --- | --- |
| MSG_CTRUNC | 8 | 用于 SOL_IP 内部控制消息。 |
| MSG_PROBE | 0x10 | 用于 MTU 发现。 |
| MSG_TRUNC | 0x20 | 截断消息。 |
| MSG_DONTTAIT | 0x40 | 如果调用者想要非阻塞 IO 则设置。 |
| MSG_EOR | 0x80 | 记录结束。 |
| MSG_WAITALL | 0x100 | 在返回前等待请求数据的的完整长度。 |
| MSG_FIN | 0x200 | TCP FIN |
| MSG_SYN | 0x800 | TCP SYN |
| MSG_CONFIRM | 0x800 | 在传输数据包之前确认路径的有效性。 |
| MSG_RST | 0x1000 | TCP RST |
| MSG_ERRQUEUE | 0x2000 | 请求从错误队列读取消息。 |
| MSG_NOSIGNAL | 0x4000 | 当确定连接断开时不生成 SIGPIPE 信号。 |
| MSG_MORE | 0x8000 | 设置指示发送者将发送更多数据。 |

`msg_name` 包含 socket 的“名称”。这是此消息的 IP 地址和端口号。`msg_namelen` 是 `msg_name` 指向的地址的长度。

```c
void *msg_name;

socklen_t msg_namelen;
```

`msg_iov` 是要发送或接收的缓冲区数组。它通常被称为“离散/聚集数组”（scatter gather array），但它不用于 DMA 操作。`msg_jovlen` 是 `msg_iov` 指向的数组中的缓冲区数量。

```c
struct iovec *msg_iov;

size_t msg_jovlen;
```

以下字段用于 Posix 1003.1g 辅助数据对象信息。辅助数据由一系列 `cmsghdr` 和 `msg_data` 对组成。`msg_control` 用于支持 `cmsg` API 函数，将控制信息传递给底层协议。更多信息请参见 man page `cmsg(3)`。

```c
void *msg_control;

socklen_t msg_control;
```

`msg_flags` 包含接收消息的标志位。

```c
int msg_flags; /* flags on received message */
```
