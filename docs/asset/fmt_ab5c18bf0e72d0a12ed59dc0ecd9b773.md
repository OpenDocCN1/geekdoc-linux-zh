
## 表 4.2 套接字类型的值

| 名称 | 值 | 目的 |
|---|---|---|
| `SOCK_STREAM` | 1 | 流套接字。用于面向连接或 `TCP` 套接字。 |
| `SOCK_DGRAM` | 2 | 数据报套接字。用于无连接或 `UDP` 套接字。 |
| `SOCK_RAW` | 3 | 原始套接字。为应用层直接访问网络层协议。 |
| `SOCK_RDM` | 4 | 可靠传输消息 (`RDM`) 套接字。 |
| `SOCK_SEQPACKET` | 5 | 顺序包套接字。 |
| `SOCK_PACKET` | 10 | 用于在网络设备级别直接访问数据包的套接字。 |

`prot` 字段指向协议块结构。该结构在创建套接字时使用。该结构用于为任何支持套接字接口的协议构建接口。下一个字段 `ops` 指向该协议特定的一组操作函数集。`proto_ops` 结构在本章前面已经讨论过。它与套接字结构中的 `ops` 字段具有相同的定义。

```c
struct proto *prot;
struct proto_ops *ops;
```

`Capability`（能力）用于确定应用层程序是否有权限执行套接字操作。对于某些原始套接字的套接字操作，需要适当的权限。这是为了防止安全攻击，因为原始套接字操作可以访问 `TCP/IP` 的内部操作。请查看本章后面关于 `Linux` `capabilities` 的章节获取更多信息。

```c
int capability;
```

下一个字段 `no_check` 告诉网络接口驱动程序不要执行校验和。最后，最后一个字段 `flags` 被定义为同一文件中定义的两个值之一。

```c
#define INET_PROTOS_REUSE 0x01
#define INET_PROTOS_PERMANENT 0x02
#define INET_PROTOS_ICSK 0x04
```

如果 `flags` 设置为 `INET_PROTOS_PERMANENT`，则协议是永久的，无法被注销。在这种情况下，注销函数会打印错误消息并返回。例如，`UDP` 和 `TCP` 的 `flags` 被设置为 `INET_PROTOS_PERMANENT`，而对于原始套接字，`SOCK_RAW` 标志值设置为 `INET_PROTOS_REUSE`。标志 `INET_PROTOS_ICSK` 表示这是一个面向连接的协议，即 `TCP`。

```c
unsigned char flags;
```

## IPv4 中成员协议的注册与初始化

在本节中，我们将讨论单独的 `AF_INET` 成员协议（如 `UDP` 和 `TCP`）如何与套接字层注册，第 6 章包含了对 `IPv4` 初始化步骤的完整讨论。在这里，我们只查看套接字层的注册。在上一节中，我们区分了永久性协议和其他协议。现在我们将查看永久性调用是如何在协议切换器中注册的。

### `inet_init` 函数

`IPv4` 中的永久协议通过定义在 `linux/net/ipv4/af_inet.c` 文件中的 `inet_init` 函数进行注册。我们在这里仅包含了一个代码段，因为我们主要关心协议切换器的注册。

```c
static int __init inet_init(void)
{}
```

该函数中的代码实际上在协议被放入数组后对其进行注册。

```c
for (r = &inetwsw[0]; r < &inetwsw[SOCK_MAX]; ++r)
   INIT_LIST_HEAD(r);
for (q = inetwsw_array; q < &inetwsw_array[INETWS_ARRAY_LEN]; ++q)
   inet_register_protos(q);
```

在前面的代码中，我们可以看到 `inet_init` 为数组 `inetwsw_array` 中的每个协议调用了 `inet_register_protos`。数组中的协议是 `UDP`、`TCP` 和原始（`raw`）接字。

### `protosw` 结构的初始化

每个协议的值在编译时初始化到 `protosw` 结构中，如图所示。此初始化在 `linux/net/ipv4/af_inet.c` 文件中完成。

```c
static struct protosw inetwsw_array[] =
{
```

第一个协议是 `TCP`，因此类型为 `SOCK_STREAM`，`flags` 被设置为永久和 `INET_PROTOS_ICSK`，以表示这是一个面向连接的协议。

```c
.type = SOCK_STREAM,
.protocol = IPPROTO_TCP,
.prot = &tcp_prot,
.ops = &inet_stream_ops,
.capability = -1,
.no_check = 0,
.flags = INET_PROTOS_PERMANENT | INET_PROTOS_ICSK,
},
```

第二个协议是 `UDP`，因此类型为 `SOCK_DGRAM`，`flags` 也被设置为永久。

```c
.type = SOCK_DGRAM,
.protocol = IPPROTO_UDP,
.prot = &udp_prot,
.ops = &inet_stream_ops,
.capability = -1,
.no_check = 0,
.flags = INET_PROTOS_PERMANENT,
},
```

第三个协议是原始（`raw`）接字，因此类型为 `SOCK_RAW`，`flags` 被设置为 `INET_PROTOS_REUSE`。

```c
.type = SOCK_RAW,
.protocol = IPPROTO_RAW,
.prot = &raw_prot,
.ops = &inet_stream_ops,
.capability = -1,
.no_check = 0,
.flags = INET_PROTOS_REUSE,
},
```
