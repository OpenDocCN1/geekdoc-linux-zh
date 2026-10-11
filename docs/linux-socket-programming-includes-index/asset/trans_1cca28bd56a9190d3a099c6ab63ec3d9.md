

## IPv6 多播标志字段

表 A.14 展示了 IPv6 多播地址中当前定义的标志字段。

**表 A.14** IPv6 多播标志字段描述

| 位 # | 描述 |
| :--- | :--- |
| 0 | 临时性 |
| | 0= 知名地址 |
| | 1= 临时地址 |
| 1 | （保留） |
| 2 | （保留） |
| 3 | （保留） |

# 附录 B

## 本附录内容

- 连接到网络 422
- 在通道上通信 428
- 终止连接 437
- 网络数据转换 438
- 网络寻址工具 442
- 套接字控制 446

本附录汇总了所有网络库和系统调用。

# 连接到网络

Sockets API 提供工具帮助你创建套接字并连接到其他主机。本节描述了与套接字创建和连接相关的 API。

## socket()

socket() 创建一个双向通道，通常用于连接网络。你可以使用此通道配合网络特定的系统调用或通用文件 I/O 进行操作。

### 原型

```c
#include <resolv.h>
#include <sys/socket.h>
#include <sys/types.h>

int socket(int domain, int type, int protocol);
```

### 返回值

如果成功，该调用返回一个有效的套接字描述符。否则，结果小于零。请检查 `errno` 以获取更多关于错误的信息。

### 参数

- **domain** 选择套接字的网络协议（参见附录 A，“数据表”）。
- **type** 选择网络层（参见附录 A）。
- **protocol** 通常为 0（参见附录 A）。

### 可能的错误

- **EPROTONOSUPPORT** 该协议类型或指定协议在此域中不受支持。
- **ENFILE** 内核内存不足以分配新的套接字结构。
- **EMFILE** 进程文件表溢出。
- **EACCES 和 ENOBUFS** 拒绝创建指定类型或协议的套接字。
- **ENOMEM** 可用内存不足。在释放足够的资源之前无法创建套接字。
- **EINVAL** 未知协议或协议族不可用。

### 示例

```c
/** 创建一个 TCP 套接字 **/
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0);

/** 创建一个 ICMP 套接字 **/
int sd;
sd = socket(PF_INET, SOCK_RAW, htons(IPPROTO_ICMP));
```

## bind()

bind() 将端口或名称绑定到套接字。如果你希望为传入连接使用一致的端口，必须将套接字绑定到某个端口。在大多数情况下，如果你未显式调用，内核会自动为套接字调用 bind()。内核生成的端口分配在每次执行时可能不同。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>

int bind(int sockfd, struct sockaddr* addr, int addrlen);
```

### 返回值

如果一切正常，返回 0。如果发生错误，你可以在 `errno` 中找到原因。

### 参数

- **sockfd** - 要绑定的套接字描述符。
- **addr** - 端口分配或名称。
- **addrlen** - `addr` 的长度，因为 `addr` 可以是不同大小的。

### 可能的错误

- **EBADF** - sockfd 不是有效的描述符。
- **EINVAL** - 套接字已绑定到某个地址。未来可能会改变；详情请参见 `.../linux/unix/socket.c`。
- **EACCES** - 该地址受保护，且用户不是超级用户。
- **ENOTSOCK** - 参数是文件的描述符，而非套接字。

### 示例

```c
/*** 将端口 #9999 绑定到任何互联网地址的套接字 ***/
int sockfd;
struct sockaddr_in addr;
sockfd = socket(PF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(9999); /* 或你想要的任何端口 */
/* 绑定任何网络接口 */
addr.sin_addr.s_addr = INADDR_ANY;
/* -或- 绑定特定接口，使用以下内容： */
/* inet_aton("128.1.1.1", &addr.sin_addr); */
if ( bind(sockfd, &addr, sizeof(addr)) != 0 )
    perror("bind");
```

![](img/2591af4bdf00a0f382331fc9481f785e_442_0.png)

## listen()

listen() 将套接字转换为监听套接字。此选项仅适用于 SOCK_STREAM 协议。该调用创建了一个传入连接队列。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>

int listen(int sockfd, int queue_len);
```

### 返回值

如果一切正常，返回 0。如果发生错误，你可以在 `errno` 中找到原因。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| sockfd | 已绑定到端口的 SOCK_STREAM 套接字 |
| queue_len | 待处理连接的最大数量 |

### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| EBADF | 参数 sockfd 不是有效的描述符。 |
| ENOTSOCK | 参数 sockfd 不是套接字。 |
| EOPNOTSUPP | 套接字类型不支持 listen() 操作。如果你提供任何非 SOCK_STREAM 类型的套接字，都会得到此错误。 |

### 示例

```c
/*** 将套接字转换为具有 10 个槽位的监听套接字 *** */
int sockfd;
sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*** 使用 bind() 设置地址 ---**/
listen(sockfd, 10); /* 创建一个包含 10 个待处理连接的队列 */
```

## accept()

等待连接。当连接到达时，为该特定连接返回一个新的套接字描述符（独立于 sockfd）。此调用仅适用于 SOCK_STREAM 套接字。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>

int accept(int sockfd, struct sockaddr *addr, int *addr_len);
```

### 返回值

| 条件 | 结果 |
| :--- | :--- |
| 如果 >= 0 | 一个新的套接字描述符。 |
| 如果 < 0 | 错误；`errno` 中有详细信息。 |

### 参数

- **sockfd** 已绑定并处于监听状态的套接字描述符。
- **addr** 如果非零，该调用会将地址定义放置在此区域中。虽然它应该匹配 `sockfd` 的协议族（AF_INET），但不要假设如此。
- **addr_len** 通过引用传递长度，以便该调用可以准确告知你使用了 `addr` 数据块的多少部分。这意味着你需要在每次调用时重置该值。

### 可能的错误

- **EBADF** 套接字描述符无效。
- **ENOTSOCK** 描述符引用的是一个文件，而非套接字。
- **EOPNOTSUPP** 引用的套接字类型不是 SOCK_STREAM。
- **EFAULT** `addr` 参数不在用户地址空间的可写部分。
- **EAGAIN** 套接字被标记为非阻塞，且当前没有预存在的连接可供接受。
- **EPERM** 防火墙规则禁止连接。
- **ENOBUFS, ENOMEM** 空闲内存不足。

### 示例

```c
/*** 接受连接，忽略来源 ***/
int sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*---使用 bind() 将地址绑定到套接字---*/
/*---使用 listen() 将其转换为监听套接字---*/
for (;;) {
    int client;
    client = accept(sockfd, 0, 0);
    /*---与客户机交互---*/
    close(client);
}

/*** 接受连接，并在日志中捕获来源 ***/
int sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*---使用 bind() 将地址绑定到套接字---*/
/*---使用 listen() 将其转换为监听套接字---*/
for (;;) {
    struct sockaddr_in addr;
    int client, addr_len = sizeof(addr);
    client = accept(sockfd, &addr, &addr_len);
    printf("Connected: %s:\n", inet_ntoa(addr.sin_addr),
           ntohs(addr.sin_port));
    /*---与客户机交互---*/
    close(client);
}
```

## connect()

连接到对等端或服务器。你可以使用此函数用于 SOCK_DGRAM 或 SOCK_STREAM 协议。对于 UDP，它仅记住你连接的端口。这允许你使用 send() 和 recv()。对于 TCP (SOCK_STREAM)，此调用启动流通信的三次握手。

### 原型

```c
#include <sys/socket.h>
#include <resolv.h>

int connect(int sockfd, struct sockaddr *addr, int addr_len);
```

### 返回值

如果一切正常，返回 0。如果发生错误，你可以在 `errno` 中找到原因。

### 参数

- **sockfd** 新创建的套接字。你可以可选地在调用此函数前调用 bind() 来分配本地端口。如果不这样做，内核将分配下一个可用的端口槽位。
- **addr** 目标地址的地址和端口。
- **addr_len** addr 数据块的长度。

### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| EBADF | 无效的描述符。 |
| EFAULT | 套接字结构地址位于用户地址空间之外。这是由无效的 addr 结构引用导致的。 |
| ENOTSOCK | 描述符未与套接字关联。 |
| EISCONN | 套接字已连接。你不能重新连接已连接的套接字。相反，你必须关闭套接字并创建一个新套接字。 |
| ECONNREFUSED | 服务器拒绝连接。 |
| ETIMEDOUT | 尝试连接时超时。 |
| ENETUNREACH | 网络不可达。 |
| EADDRINUSE | 地址已被使用。 |
| EINPROGRESS | 套接字是非阻塞的，且连接无法立即完成。可以通过选择套接字的写入操作来 select() 或 poll() 以完成等待。当 select() 指示可写性后，使用 getsockopt() 读取 SOL_SOCKET 级别的 SO_ERROR 选项以确定连接是成功（SO_ERROR 为 0）还是失败（SO_ERROR 是先前列出的常见错误代码之一，说明失败原因）。 |

