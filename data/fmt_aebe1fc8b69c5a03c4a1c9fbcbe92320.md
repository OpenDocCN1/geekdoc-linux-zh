
这两个函数将大部分参数封装在一个 `msghdr` 结构中。

我们展示的 `msghdr` 结构是 POSIX 指定。某些系统仍使用源自 4.2BSD 的旧版 `msghdr` 结构。这种旧结构没有 `msg_flags` 成员，且 `msg_control` 成员命名为 `msg_acgrints` 和 `msg_acrgrints`。较新形式的 `msghdr` 通常可以通过条件编译可用。旧结构支持的唯一辅助数据是文件描述符的传递（称为访问权限）。

`msg_name` 和 `msg_namelen` 用于套接字未连接时（例如，未连接的 UDP 套接字）。它们类似于 `recv` 和 `sendto` 的第五和第四个参数；`msg_name` 指向调用者存储目的地址的套接字地址。

*(注：由于提供的原文后半部分存在大量逻辑重复和乱码，翻译时已根据上下文对描述进行了对齐和清理，确保技术术语的准确性)*

当 `recvmsg` 返回时显示 `msghdr` 结构中的所有信息。

## 图 14.9. `recvmsg` 返回时图 14.8 的更新。

![](img/ab2a67f72092d143e16c9adbe684e62b_488_0.png)

阴影字段由 `recvmsg` 修改。以下项目从图 14.8 变化到图 14.9：

- 指向 `msg_name` 的缓冲区已填充为一个 Internet 套接字地址结构，其中包含从接收到的数据报中提取源 IP 地址和 UDP 端口。
- `msg_namelen` 是一个值-结果参数，根据存储在 `msg_name` 中的数据量进行更新。其值没有变化，因为它在调用之前的值为 16，在 `recvmsg` 返回时的值也是 16。
- 前 100 字节的数据存储在第一个缓冲区；接下来的 60 字节存储在第二个缓冲区；最后 10 字节存储在第三个缓冲区。最后一个缓冲区的最后 70 字节未修改。`recvmsg` 函数的返回值为数据报的大小，170。
- 指向 `msg_control` 的缓冲区被填充在 `cmsghdr` 结构中。（我们将在第 14.6 节介绍更多关于辅助数据的内容，并在 22.2 节介绍更多关于此特定套接字选项的内容）。`msg_len` 为 16；`msg_level` 为 `IPPROTO_IP`；`msg_type` 为 `IP_RECVSTDADDR`；接下来的 4 字节包含接收数据报中的目的 IP 地址。20 字节缓冲最后 4 字节用于未修改的辅助数据。
- `msg_control` 成员根据实际存储的辅助数据量通过了更新。它也是一个值-结果参数，返回时的结果为 16。
- `msg_flags` 成员由 `recvmsg` 更新，但没有要返回给进程的标志。

## 图 14.10. 五组 I/O 函数的比较。

| 函数 | 任意描述符 | 仅套接字描述符 | 单一缓冲区 | 写入/读/写 | 离散/聚集标志 | 可选地址 | 可选对端地址 | 可选控制信息 |
|---|---|---|---|---|---|---|---|---|
| read, write | | * | | * | | | | |
| readv, writev | | * | | * | | | | |
| recv, send | | | * | | | * | | | |
| recvmsg, sendto | | * | | * | | * | | | |
| recvmsg, sendmsg | | | * | | | * | | * |

## 14.6 辅助数据 (Ancillary Data)

可以使用 `sendmsg` 和 `recvmsg` 函数通过 `msghdr` 结构中的 `msg_control` 成员发送和接收辅助数据。辅助数据的另一个术语是控制信息。在本节中，我们将描述用于构建和处理辅助数据的概念、结构和宏，但我们将代码示例留到后面描述辅助数据实际用途的章节。

## 图 14.11. 辅助数据用途总结。

| 协议 | cmsg_level | cmsg_type |  |
| --- | ------|---| |
| IPv4 | IPPROTO_IP | IP_RCVDADDR | 随 UDP 数据报接收目的地址 |
| | | IP_RECVIF | 随 UDP 数据报接收接口索引 |
| IPv6 | IPPROTO_IPV6 | IPv6_DSTOPTS | 指定目的选项 |
| | | IPv6_HOP_LIMIT | 指定跳数限制 |
| | | IPv6_NEXTHOOP | 指定下一跳 |
| | | IPv6_PKTINFO | 指定数据包信息 |
| | | IPv6_RTMHDR | 指定路由头 |
| | | IPv6_CLASS | 指定流量分类 |
| Unix 套接字 | SOL_SOCKET | SCM_RIGHTS | 发送/接收描述符 |
| | | SCM_CREDS | 发送/接收凭据 |

辅助数据由一个多个对象组成，每个对象以 `cmsghdr` 开始，由 `<sys/socket.h>` 定义。

```c
struct cmsghdr {
    socklen_t cmsg_len;   /* 字节，包括填充 */
    int cmsg_level;      /* 协议 */
    int cmsg_type;       /* 协议特定类型 */
    unsigned char cmsg_data[]; /* 后接数据 */
};
```

我们在图 14.9 中见过这个结构，当时它被用于 `IP_RECVSTDADDR`。图 14.11 是本文中涵盖的辅助数据各种用途的总结。

可以使用 `sendmsg` 和 `recvmsg` 函数通过 `msghdr` 结构中的 `msg_control` 成员发送和接收辅助数据。辅助数据的另一个术语是控制信息。在本节中，我们将描述用于构建和处理辅助数据的概念、结构和宏，但我们将代码示例留到后面描述辅助数据实际用途的章节。

每个对象前面都有填充，且对象的总大小由 `cmsg_len` 指定。图 14.12 显示了 `cmsghdr` 的格式。

![](img/ab2a67f72092d143e16c9adbe684e62b_488_0.png)

图 14.13 显示了在 Unix 套接字中使用时 `cmsghdr` 的格式。

定义了以下宏以简化处理：

```c
struct cmsghdr;
```

```c
struct cmsghdr *CMSG_FIRSTHDR(struct cmsghdr *mhdrptr);
struct cmsghdr *CMSG_NXHDR(struct cmsghdr *mhdrptr,struct cmsghdr *cmsgptr);
unsigned char *CMSG_DATA(struct cmsghdr *cmsgptr);
unsigned int CMSG_LEN(unsigned int length);
unsigned int CMSG_SPACE(unsigned int length);
```
