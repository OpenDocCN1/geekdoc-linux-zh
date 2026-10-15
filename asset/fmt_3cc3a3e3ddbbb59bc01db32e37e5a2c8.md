
```c
#include <sys/socket.h>

#include <resolv.h>

int connect(int sockfd, struct sockaddr *addr, int addr_len);
```

### 返回值

如果一切正常，返回 `0`。如果发生错误，你可以在 `errno` 中找到原因。

### 参数

- `sockfd` 新创建的套接字。你可以可选地在调用此函数前调用 `bind()` 来分配本地端口。如果不这样做，内核将分配下一个可用的端口槽位。
- `addr` 目标地址的地址和端口。
- `addr_len` `addr` 数据块的长度。

### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EBADF` | 无效的描述符。 |
| `EFAULT` | 套接字结构地址位于用户地址空间之外。这是由无效的 `addr` 结构引用导致的。 |
| `ENOTSOCK` | 描述符未与套接字关联。 |
| `EISCONN` | 套接字已连接。你不能重新连接已连接的套接字。相反，你必须关闭套接字并创建一个新套接字。 |
| `ECONNREFUSED` | 服务器拒绝连接。 |
| `ETIMEDOUT` | 尝试连接时超时。 |
| `ENETUNREACH` | 网络不可达。 |
| `EADDRINUSE` | 地址已被使用。 |
| `EINPROGRESS` | 套接字是非阻塞的，且连接无法立即完成。可以通过选择套接字的写入操作来 `select()` 或 `poll()` 以完成等待。当 `select()` 指示可写性后，使用 `getsockopt()` 读取 `SOL_SOCKET` 级别的 `SO_ERROR` 选项以确定连接是成功（`SO_ERROR` 为 `0`）还是失败（`SO_ERROR` 是先前列出的常见错误代码之一，说明失败原因）。 |

## `connect()` 错误处理

- `EALREADY`
  该套接字为非阻塞模式，且之前的连接尝试尚未完成。
- `EAFNOSUPPORT`
  传入地址的 `sa_family` 字段中未包含正确的地址族。
- `EACCES`
  用户尝试连接到一个广播地址，但未启用套接字的广播标志。

## 示例

```c
/*** 连接到 TCP 服务器 ***/

int sockfd;

struct sockaddr_in addr;

sockfd = socket(PF_INET, SOCK_STREAM, 0);

bzero(&addr, sizeof(addr));

addr.sin_family = AF_INET;

addr.sin_port = 13; /* 当前时间 */

inet_atoi("127.0.0.1", &addr.sin_addr);

if (connect(sockfd, &addr, sizeof(addr)) != 0)
    perror("connect");
```

## `socketpair()`

创建一对相互连接的套接字，其连接方式类似于管道，但使用套接字子系统。它几乎等同于 `pipe()` 系统调用，但提供了套接字 API 的附加功能。`socketpair()` 仅支持 `PF_UNIX` 或 `PF_LOCAL` 套接字。你不需要将此套接字 `bind()` 到文件系统中的文件名。

### 原型

```c
#include <sys/socket.h>

#include <resolv.h>

int socketpair(int domain, int type, int protocol,
               int sockfds[2]);
```

### 返回值

如果一切正常，则返回零 (`0`)。如果发生错误，可以在 `errno` 中查找原因。

### 参数

- `domain`
  必须是 `PF_LOCAL` 或 `PF_UNIX`。
- `type`
  `SOCK_STREAM`；这会创建一个类似 `pipe()` 的套接字。在某些 UNIX 系统中，管道是双向的。然而，Posix 1 并不要求双向性。
- `protocol`
  必须为零 (`0`)。
- `sockfds[2]`
  一个整数数组，如果调用成功，新的套接字描述符将存储在该数组中。

### 可能的错误

- `EMFILE` 此进程正在使用的描述符过多。
- `EAFNOSUPPORT` 此机器不支持指定的地址族。
- `EPROTONOSUPPORT` 此机器不支持指定的协议。
- `EOPNOSUPPORT` 指定的协议不支持创建套接字对。
- `EFAULT` `sockfds` 的地址未指定进程地址空间的有效部分。

### 示例

```c
/** 创建套接字对 ***/

int sockfd[2];

struct sockaddr_un addr;

if (socketpair(PF_LOCAL, SOCK_STREAM, 0, sockfd) != 0)
    perror("socketpair");
```

## 在通道上通信

在建立套接字和连接之后，你可以使用 API 来发送和接收消息。本节定义了所有套接字 I/O 的调用 API。

## `send()`

向已连接的通信对端、客户端或服务器发送消息。此调用类似于 `write()` 系统调用，但 `send()` 允许你为通道控制定义额外的选项。

### 原型

```c
#include <sys/socket.h>

#include <resolv.h>

int send(int sockfd, void *buffer, int msg_len,
         int options);
```

### 返回值

与 `write()` 类似，该调用返回写入的字节数。字节计数可能小于 `msg_len`。如果调用未能成功写入所有必需字节，可以使用循环进行后续写入。如果返回值为负，则调用会在 `errno` 中存储错误详情。

### 参数

- `sockfd` 套接字通道。这可以是已连接的 `SOCK_DGRAM` 或 `SOCK_STREAM` 套接字。
- `buffer` 要发送的数据。
- `msg_len` 要发送的字节数。
- `options`
  一组标志，用于启用特殊消息处理：
  - `MSG_OOB` 发送带外（紧急）消息。
  - `MSG_DONTROUTE` 绕过所有路由器发送消息。如果不成功，网络将返回错误。
  - `MSG_DONTWAIT` 不允许阻塞。类似于 `fcntl()` 选项调用，但仅适用于此调用。如果调用会阻塞，则返回 `errno` 中的 `EWOULDBLOCK`。
  - `MSG_NOSIGNAL` 如果对端断开连接，不在本地引发 `SIGPIPE` 信号。

### 可能的错误

- `EBADF` 指定了无效的描述符。
- `ENOTSOCK` 参数 `sockfd` 不是套接字。
- `EFAULT` 为 `buffer` 指定了无效的用户空间地址。
- `EMSGSIZE` 由于套接字要求消息必须原子发送，且要发送的消息大小导致无法完成此操作，因此调用无法完成。
- `EAGAIN` 套接字标记为非阻塞，且请求的操作会阻塞。
- `ENOBUFS` 系统无法分配内部内存块。当缓冲区可用时，操作可能会成功。
- `EINTR` 发生了一个信号。
- `ENOMEM` 没有可用内存。
- `EINVAL` 传入了无效参数。
- `EPIPE` 在已连接的套接字上，本地端已关闭。在这种情况下，除非设置了 `MSG_NOSIGNAL`，否则进程还将接收 `SIGPIPE`。

### 示例

```c
/* ** 向已连接的目标发送消息 (TCP, UDP) ** */

int sockfd;

int bytes, bytes_wrote=0;

/* -- 创建套接字，连接到服务器/对端 -- */

while ((bytes = send(sockfd, buffer, msg_len, 0)) > 0)
    if ((bytes_wrote += bytes) >= msg_len)
        break;

if (bytes < 0)
    perror("send");
```

```c
/*** 向已连接的目标发送紧急消息 (TCP) ***/

int sockfd;

int bytes, bytes_wrote=0;

/*--- 创建套接字，连接到服务器 ---*/

if (send(sockfd, buffer, 1, MSG_OOB) != 1)
    perror("Urgent message");
```

## `sendto()`

向特定目标发送消息，而无需建立连接。通常，你对 UDP 和原始套接字使用此系统调用。对 TCP 套接字使用此调用属于事务 TCP (T/TCP)。（然而，Linux 尚不支持 T/TCP）。

### 原型

```c
#include <sys/socket.h>

#include <resolv.h>

int sendto(int sockfd, void* msg, int len, int options,
```
