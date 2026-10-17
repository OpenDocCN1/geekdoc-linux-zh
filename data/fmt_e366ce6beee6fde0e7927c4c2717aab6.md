
每个 `addrinfo` 结构的字段描述了关联地址结构的属性。`ai_family` 字段设置为 `AF_INET` 或 `AF_INET6`，告诉我们 `socket` 地址的类型。`ai_socktype` 被设置为 `SOCK_STREAM` 或 `SOCK_DGRAM`，指示该结构是 TCP 还是 UDP 服务。`ai_protocol` 字段返回与地址族类型合适的协议值。(`ai_family`、`ai_socktype` 和 `ai_protocol` 字段提供了调用 `socket()` 时参数所需的数值)。`ai_addrlen` 字段给出由 `in_addr` 结构（IPv4）或 `in6_addr` 结构（IPv6）指向的 `socket` 地址结构的大小（字节）。`ai_canoname` 字段未使用（仅在第一个 `addrinfo` 结构中使用，且仅在 `hints_flags` 中使用了 `AI_CANONAME` 标志时，如下文所述）。

与 `getbyname()` 一，`getaddrinfo()` 可能需要向 DNS 服务器发送请求，`getnameinfo()` 也是如此，我们在 59.10.4 节中对其进行了描述。

我们在 59.11 节中演示 `getaddrinfo()` 的用法。

| result | addrinfo 结构 | 规范主机名 |
| --- | --- | --- |
| ai canonname | 套接地址结构 | |
| ai addr | | |
| ai next | | |

**图 59-33:** 由 `getaddrinfo()` 分配并返回的结构

## hints 参数

`hints` 参数指定了选择 `getaddrinfo()` 返回的套接地址结构的进一步标准。当其作为 `hints` 使用时，只有 `addrinfo` 结构中的 `ai_flags`、`ai_family`、`ai_socktype` 和 `ai_protocol` 字段可以设置。其他字段均未使用，且应根据情况初始化为 0 或 NULL。

`ai_family` 字段选择返回的套接地址结构所在的域。它可以被指定为 `AF_INET` 或 `AF_INET6`（如果实现支持，也可以是其他 `AF_*` 常量）。如果我们感兴趣获取所有类型的套接地址结构，可以将此字段指定为 `AF_UNSPEC`。

`ai_socktype` 字段指定了返回的地址结构将使用的套接类型。如果我们指定该字段为 `SOCK_DGRAM`，则会对 UDP 服务进行查询，并通过 `result` 返回相应的套接地址结构。如果我们使用 `SOCK_STREAM`，则会对 TCP 服务进行查询。如果 `ai_socktype` 被指定为 0，则任何套接类型都是接受的。

`ai_protocol` 字段为返回的地址结构选择套接协议。对于我们的目的，此字段始终指定为 0，这意味着调用者将接受任何协议。

`hints_ai_fields` 字段是一个位掩码，用于修改 `getaddrinfo()` 的行为。该字段通过以下零或多个值进行或（OR）运算形成：

### AI_ADDRCONFIG

仅当本地系统配置了至少一个 IPv4 地址（IPv4 回环地址除外）时，返回 IPv4 地址；仅当本地系统配置了至少一个 IPv6 地址（IPv6 回环地址除外）时，返回 IPv6 地址。

### AI_ALL

参见下下文对 `AI_V4MAPPED` 的描述。

### AI_CANONAME

如果 `host` 不为 NULL，则返回一个指向包含主机规范名的空终止字符串的指针。该指针存储在 `result` 返回的第一个 `addrinfo` 结构的 `ai_canoname` 字段所指向的缓冲区。

### AI_NUMERICHOST

强制将 `host` 解析为数字地址字符串。这用于在不需要的情况下防止名称解析，因为名称解析可能非常耗时。

### AI_NUMERICSERV

将 `service` 解析为数字端口号。此标志防止了任何名称解析服务的调用，如果 `service` 是数字字符串，则不需要该服务。

### AI_PASSIVE

返回适用于被动打开（即监听套接字）的套接结构。在这种情况下，`host` 应为 NULL，且 `result` 返回的套接结构中的 IP 地址部分将包含通配 IP 地址（即 `INADDR_ANY` 或 `IN6ADDR_ANY_INIT`）。如果未设置此标志，`result` 返回的地址结构将适用于 `connect()` 和 `sendto()`；如果 `host` 为 NULL，则根据域，返回的套接地址中的 IP 地址将是 `INADDR_LOOPBACK` 或 `IN6ADDR_LOOPBACK_INIT`。

### AI_V4MAPPED

如果在 `hints` 的 `ai_family` 字段中指定了 `AF_INET6`，当找不到匹配的 IPv6 地址时，应在 `result` 中返回 IPv4 映射 IPv6 地址。如果同时指定了 `AI_ALL` 和 `AI_V4MAPPED`，则在 `result` 中同时返回 IPv4 和 IPv6 地址结构，其中 IPv4 地址以 IPv4 映射 IPv6 地址的形式返回。

如上述 `AI_PASSIVE` 所注的，`host` 可以被指定为 NULL。也可以将 `service` 指定为 NULL，在这种情况下，返回的地址结构中的端口号被设置为 0（即我们只感兴趣将主机名解析为地址）。然而，不允许同时将 `host` 和 `service` 都指定为 NULL。

如果我们不需要在 `hints` 中指定上述任何选择标准，可以将其指定为 NULL，在这种情况下，`ai_socktype` 和 `ai_protocol` 假设为 0，`ai_flags` 假设为 (`AI_V4MAPPED | AI_ADDRCONFIG`)，`ai_family` 假设为 `AF_UNSPEC`。`glibc` 的实现故意偏离了 SUSv3，v3 规定如果 `hints` 为 NULL，则 `ai_flags` 假设为 0。）

## 59.10.2 释放 addinfo 列表：freeaddrinfo()

`getaddrinfo()` 函数为 `result` 所指的所有结构动态分配内存（图 59-3）。因此，调用者必须在不再需要这些结构时释放它们。提供了 `freeaddrinfo()` 函数以便方便地在一步中完成这种释放操作。

```c
#include <sys/socket.h>
#include <netdb.h>

void freeaddrinfo(struct addrinfo *result);
```

如果我们想保留一个 `addrinfo` 结构或其关联套接地址结构的副本，必须在调用 `freeaddrinfo()` 之前复制这些结构。

## 59.10.3 诊断错误：gai_strerror()

发生错误时，`getaddrinfo()` 返回表 59-1 显示的非零错误代码之一。

表 59-1：`getaddrinfo()` 和 `getnameinfo()` 的错误返回

| 错误常量 | 描述 |
| --- | --- |
| EAI_ADDRINFO | `getaddrinfo()` 和 `getnameinfo()` 的错误返回 |
| EAI_AGAIN | 名称解析临时失败（重试） |
| EAI_BADFLAGS | 指定了无效标志 |
| EAI_FAIL | 访问名称时发生不可恢复的失败 |
| EAI_FAMILY | 地址族 |
| EAI_MEMORY | 内存分配失败 |
| EAI_NODATA | 与主机无关联 |
| EAI_NONAME | 未知主机或服务，或两者都为 NULL |
| EAI_OVERFLOW | 参数溢出 |
| EAI_SERVICE | 指定的服务不支持 |
| EAI_SOCKETTYPE | 指定的套接类型不支持 |
| EAI_SYSTEM | 返回系统错误 |

给定表 59-1 中的错误代码，`gai_strerror()` 函数返回一个描述该错误的字符串。（这通常比显示的短。）

```c
#include <netdb.h>

const char *gai_strerror(int errcode);
```

可以使用 `gai_strerror()` 返回的字符串作为应用程序的一部分。

## 59.10.4 getnameinfo() 函数

`getnameinfo()` 函数是 `getaddrinfo()` 的逆过程。给定一个套接地址（无论是 IPv4 还是 IPv6），它返回包含相应主机和服务名的字符串，如果无法转换则返回数字。

```c
#include <sys/socket.h>
#include <netdb.h>

int getnameinfo(const sockaddr *addr, size_t addrlen, char *host, size_t hostlen, char *service, size_t servlen, int flags);
// 成功返回 0，错误返回非零
```
