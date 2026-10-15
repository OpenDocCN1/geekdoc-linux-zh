
```c
#include <sys/io.h>

size_t recvmsg(int sockfd, struct msghdr *msg, int flags);

size_t sendmsg(int sockfd, struct msghdr *msg, int flags);

返回值：读取的字节数；如果正常，错误时返回 -1
```

这两个函数将所有参数封装在一个 `msghdr` 结构体中。

```c
struct msghdr {
    void *msg_name;            /* 协议地址 */
    socklen_t  msg_namelen;     /* 协议地址的大小 */
    struct iovec *msg_iov;     /* 离散/聚集数组 */
    int         msg_iovlen;     /* msg_iov 中的元素 */
    void *msg_control;          /* 辅助数据 (msghdr) */
    socklen_t  msg_controllen; /* 辅助数据的长度 */
    int         msg_flags;      /* recvmsg() 返回的标志 */
};
```

我们显示的 `msghdr` 结构是 POSIX 中的。某些较旧的 `msghdr` 起源于 4BSD。这种旧的结构没有 `msg_flags` 成员，且 `msg_control` 和 `msg_controllen` 成员被命名为 `msg_acgr` 和 `msg_acrclen`。新版本的 `msghdr` 形式通常可以通过条件编译标志可用。旧结构支持的唯一辅助数据形式是传递文件描述符（访问权限）。

`msg_name` 和 `msg_namelen` 成员在套接字未连接时使用（例如未连接的 UDP 套接字）。它们类似于 `recvfrom` 和 `sendto` 的第五、六个参数：`msg_name` 指向一个套接字结构，调用者在其中为 `sendmsg` 存储目的地的协议地址，或者 `recvmsg` 在其中存储发送者的协议地址。如果不需要指定地址（例如，TCP 套接字或已连接的 UDP 套接字），`msg_namelen` 应取空指针的值；对于 `sendmsg`，它是一个值-结果参数；对于 `recvmsg` 亦如此。

`msg_iov` 和 `msg_io_ownlen` 成员指定输入或输出缓冲区数组（`iovec` 结构体数组），类似于 `readv` 或 `write` 的第二、第三参数。`msg_control` 和 `msg_controllen` 成员指定可选辅助数据的位置和大小。`msg_control` 是 `recvmsg` 的一个值-结果参数。

通过 `recvmsg` 和 `sendmsg`，我们必须区分两个标志变量：按值传递的 `flags` 参数，以及 `msghdr` 结构体中的 `msg_flags` 成员（通过引用传递，即将结构体的地址传递给函数）。

- `msg_flags` 成员仅供 `recvmsg` 使用。当调用 `recvmsg` 时，`flags` 参数被复制到 `msg_flags` 成员中（TCPv2 第 502 页），内核使用此值来驱动其接收处理。此值根据 `recvmsg` 的结果进行更新。
- `msg_flags` 成员被 `sendmsg` 忽略，因为该函数使用 `flags` 参数来驱动其输出处理。这意味着如果我们想在 `sendmsg` 调用中设置 `MSG_DONTWAIT` 标志，我们将 `flags` 参数设置为此值；而将 `msg_flags` 成员设置为此值则没有影响。

图 14.7 总结了内核为输入输出函数解释的标志，以及 `recvmsg` 可能返回的 `msg_flags`。没有 `sendmsg msg_flags` 这一列，因为正如我们提到的，它没有被使用。

| 标志 | 检查者：send flags | sendto flags | sendmsg flags | 检查者：recv flags | recvfrom flags | recvmsg flags | 返回值： |
|---|---|---|---|---|---|---|---|
| MSG_DONTUNE | * | | | | | | |
| MSG_DONTWAIT | * | | | | | | |
| MSG_PEEK | * | | | | | | |
| MSG_WAITALL | | | | | | | * |
| MSG_EOR | * | * | | | | | |
| MSG_OOB | * | | | | | | |
| MSG_BROAST | | | | | | | |
| MSG_MCAST | | | | | | | |
| MSG_TRUNC | | | | | | | |
| MSG_CTRUNC | | | | | | | |
| MSG_NOTIFICATION | | | | | | | |

图 14.7 内核解释的输入输出函数标志以及 `recvmsg` 可能返回的 `msg_flags` 总结。

图 14.7 输入输出函数的标志总结。

阴影区域由 `recvmsg` 修改。前四个标志被检查，后两个标志被检查并返回，最后四个标志是 `recvmsg` 接收的。

`MSG_BCAST`: 这种形式在 BSD 中很常见，如果数据报是广播的则返回。`msgmsg` 接收的标志

`MSG_MCAST`: 这种形式较新，BSD 支持，如果数据报是多播的则返回。

`MSG_TRUNC`: 这种形式在数据报被截断时，内核。`recvmsg` 结构。

`MSG_CTRUNC`: 这种形式在辅助数据被截断时。`msg_flags`。

`MSG_EOR`: 这种形式在数据报结束时返回。`flags`。

`MSG_OOB`: 这种形式用于带外数据。

`MSG_NOTIFICATION`: 这种形式用于通知。

`MSG_DONTWAIT`: 这种形式用于非阻塞等待。

`MSG_PEEK`: 这种形式用于预视数据。

`MSG_WAITALL`: 这种形式用于等待所有数据。

`MSG_DONTUNE`: 这种形式用于取消对齐。

# 图 14.10 总结了五组 I/O 函数之间的差异。

| 函数 | 任意描述符 | 仅 socket 描述符 | 单个读/写缓冲区 | 离散聚集读/写 | 可选标志 | 可选对端地址 | 可选控制 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| read, write | ● | | | | | | |
| readv, writev | | ● | | | | | |
| recv, send | | | ● | | | | |
| recvfrom, sendto | | | | ● | | | |
| recvmsg, sendmsg | | | | | ● | | ● |

图 14.10 五组 I/O 函数的比较。

## 14.6 辅助数据 (Ancillary Data)

可以使用 `sendmsg` 和 `recvmsg` 函数通过 `msghdr` 结构中的 `msg_control` 和 `msg_controllen` 来发送和接收辅助数据。辅助数据的另一个术语是控制信息（control information）。在本节中，我们将描述用于构建和处理辅助数据的概念、结构和宏，但我们将把代码示例留到后面的章节，以描述辅助数据的实际用途。

图 14.11 是本文涵盖的辅助数据各种用处的总结。

| 协议 | cmsg_level | cmsg_type | 说明 |
| --- | --- | --- | --- |
| IPv4 | IPPROTO_IP | IP_RECVSTDADDR | 接收 UDP 数据报文的目的地址 |
| | | IP_RECV | 接收 UDP 数据报文的接口索引 |
| IPv6 | IPPROTO_IPV6 | IPv6_DESTOPTS | 指定目的选项 |
| | | IPv6_HOPLIMIT | 指定跳数限制 |
| | | IPv6_HOOPTS | 指定逐跳选项 |
| | | IPv6_NEXTHOP | 指定下一跳地址 |
| | | IPv6_PKTINFO | 指定数据包信息 |
| | | IPv6_RTRHDR | 指定路由头 |
| | | IPv6_TCADS | 指定流量分类 |
| Unix 域套字 | SOL_SOCKET | SCM_RIGHTS | 发送/接收描述符 |
| | | SCM_CREDS | 发送/接收用户凭据 |

图 14.11 辅助数据的用途总结。

OSI 协议也使用辅助数据用于我们在本文中未讨论的各种目的。

辅助数据由一个或多个辅助数据对象组成，每个对象以 `cmsghdr` 结构开头，由 `<sys/socket.h>` 定义。
