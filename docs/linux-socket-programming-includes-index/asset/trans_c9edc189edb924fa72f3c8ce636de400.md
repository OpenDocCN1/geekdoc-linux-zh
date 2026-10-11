
## connect() 错误处理
- EALREADY
该套接字为非阻塞模式，且之前的连接尝试尚未完成。
- EAFNOSUPPORT
传入地址的 sa_family 字段中未包含正确的地址族。
- EACCES
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

## socketpair()

创建一对相互连接的套接字，其连接方式类似于管道，但使用套接字子系统。它几乎等同于 `pipe()` 系统调用，但提供了套接字 API 的附加功能。`socketpair()` 仅支持 `PF_UNIX` 或 `PF_LOCAL` 套接字。你不需要将此套接字 `bind()` 到文件系统中的文件名。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>
int socketpair(int domain, int type, int protocol,
               int sockfds[2]);
```

### 返回值

如果一切正常，则返回零 (0)。如果发生错误，可以在 `errno` 中查找原因。

### 参数

- **domain**
必须是 `PF_LOCAL` 或 `PF_UNIX`。
- **type**
`SOCK_STREAM`；这会创建一个类似 `pipe()` 的套接字。在某些 UNIX 系统中，管道是双向的。然而，Posix 1 并不要求双向性。
- **protocol**
必须为零 (0)。
- **sockfds[2]**
一个整数数组，如果调用成功，新的套接字描述符将存储在该数组中。

### 可能的错误

- `EMFILE` 此进程正在使用的描述符过多。
- `EAFNOSUPPORT` 此机器不支持指定的地址族。
- `EPROTONOSUPPORT` 此机器不支持指定的协议。
- `EOPNOSUPPORT` 指定的协议不支持创建套接字对。
- `EFAULT` `socket fds` 的地址未指定进程地址空间的有效部分。

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

## send()

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

- **sockfd** 套接字通道。这可以是已连接的 `SOCK_DGRAM` 或 `SOCK_STREAM` 套接字。
- **buffer** 要发送的数据。
- **msg_len** 要发送的字节数。
- **options**
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

## sendto()

向特定目标发送消息，而无需建立连接。通常，你对 UDP 和原始套接字使用此系统调用。对 TCP 套接字使用此调用属于事务 TCP (T/TCP)。（然而，Linux 尚不支持 T/TCP）。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>
int sendto(int sockfd, void* msg, int len, int options,
           struct sockaddr *addr, int addr_len);
```

### 返回值

返回已发送的字节数，如果发生错误则返回 -1。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `sockfd` | 套接字描述符 |
| `msg` | 要发送的数据 |
| `len` | 要发送的字节数 |
| `options` | 消息控制标志（与 `send()` 相同） |
| `addr` | 目标的地址 |
| `addr_len` | 目标数据体的大小 |

### 可能的错误

（与 `send()` 相同）

### 示例

```c
/*** 向未连接的目标发送消息 (TCP, UDP) ***/
int sockfd;
struct sockaddr_in addr;
if ((sd = socket(PF_INET, SOCK_DGRAM, 0)) < 0)
    perror("socket");
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(DEST_PORT);
inet_aton(DEST_ADDR, &addr.sin_addr);
if (send(sockfd, buffer, msg_len, 0, &addr, sizeof(addr)) < 0)
    perror("sendto");
```

## sendmsg()

从几个数据块组装一个消息。此例程获取 *iovec* 结构中的数据并创建单个消息。如果 *msg_name* 指向实际的 *sockaddr*，则该例程以无连接方式发送消息。如果是 *NULL*，则例程假设套接字已连接。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>
#include <sys/uio.h>

int sendmsg(int sockfd, const struct msghdr *msg,
    unsigned int options);
```

### 返回值

此调用返回发送的总字节数，如果发生错误则返回 -1（查看 *errno* 以获取更多信息）。

### 参数

- **sockfd**
已打开的套接字描述符。
- **msg**
这是对 *msghdr* 结构的引用，其中包含目标地址、标志和消息。结构定义如下：

```c
struct iovec
{
    void *iov_base;      /* 缓冲区起始位置 */
    _kernel_size_t iov_len; /* 缓冲区长度 */
};

struct msghdr
{
    __ptr_t msg_name;    /* 目标地址 */
    socklen_t msg_namelen; /* 地址长度 */
    struct iovec *msg_iov; /* 缓冲区向量 */
    size_t msg_iovlen;  /* 向量长度 */
    __ptr_t msg_control; /* 辅助数据 */
    size_t msg_controllen; /* 辅助数据长度 */
    int msg_flags;       /* 接收到的消息标志 */
};
```

辅助数据允许程序传输特殊数据，如文件描述符。
- **options**
消息控制标志（与 *send()* 相同）。

### 可能的错误

（与 *send()* 相同）

### 示例

```c
int i, sd, len, bytes;
char buffer[MSGS][100];
struct iovec io[MSGS];
struct msghdr msg;
struct sockaddr_in addr;

sd = socket(PF_INET, SOCK_DGRAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(8080);
inet_aton("127.0.0.1", &addr.sin_addr);
bzero(&msg, sizeof(msg));
msg.msg_name = &addr;
msg.msg_namelen = sizeof(addr);
for (i = 0; i < MSGS; i++)
{
    io[i].iov_base = buffer[i];
    sprintf(buffer[i], "Buffer #%d: this is a test\n", i);
    io[i].iov_len = strlen(buffer[i]);
}
msg.msg_iov = io;
msg.msg_iovlen = MSGS;
if ((bytes = sendmsg(sd, &msg, 0)) < 0)
    perror("sendmsg");
```

## sendfile()

通过套接字传输文件的快速方式。该调用从 `in_fd` 读取数据并将其写入 `out_fd`。该调用不会更改 `in_fd` 中的文件指针，但 `out_fd` 的文件指针会发生变化。该调用从 `*offset` 开始读取 count 字节。完成后，`*offset` 指向最后一个已读取字节之后的位置。如果你需要添加头部信息，请参考 TCP(4) 中的 TCP_CORK 选项以提高性能。

### 原型

```c
#include <unistd.h>
int sendfile(int out_fd, int in_fd, off_t *offset,
             size_t count);
```

### 返回值

如果成功，该调用返回复制的总字节数。如果发生错误，该调用返回 -1 并将 errno 设置为错误代码。

