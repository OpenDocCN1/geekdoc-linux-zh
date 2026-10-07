
## 停止 CD

在你开始播放轨道后，你可能由于某些原因需要停止 CD（例如为了从中读取数据）。你可以通过调用带有 `CDROMSTOP` 请求的 `ioctl(1)` 函数来停止 CD 播放。该请求不接受任何参数。

# 第 9 章

## 网络

在当今的互联网社会，除非游戏包含某种形式的多人娱乐，否则很少游戏能通过大众市场。尽管如此，仍有少量 PC 游戏在发布时并不具备与其他人类竞争或合作的能力。而另一个极端是那些设计为纯多人体验的游戏，它们在单机娱乐方面提供极少。

## 现代网络导论

如今的网络与早期已大不相同。近年来，诸如 `IPX` 等传统技术已被广泛接受的标准（如 `TCP/IP`）所取代。

即使网络的物理设计也发生了变化。旧的以太网（`Ethernet`）系统已被更可靠的 `Cat-5` 结构取代，这种结构采用了与互联网类似的格式。“星型”拓扑结构可能是目前最常用的网络类型——这有其道理。然而，我来这里不是为了教你如何搭建网络，而是为了关注软件方面。

当涉及到为任何类型的软件添加网络支持时，在编写代码之前，你需要考虑某些事情。你首先需要考虑的是你想使用哪种网络架构。有两种值得考虑的类型：点对点（`peer-to-peer`）和客户端/服务器（`client/server`）。

## 点对点网络

除非包含某种形式的多人娱乐，否则很少有游戏能通过大众市场。尽管如此，仍有少量 PC 游戏在发布时并不具备与其他人类竞争或合作的能力。而另一个极端是设计为纯多人体验的游戏，它们在单机娱乐方面提供极少。

点对点应用程序是那些不需要中心节点即可通信的程序。点对点架构在某些情况下是不适用的，但对于某些游戏，它是完美的。点对点网络允许设备之间直接通信，无需通过服务器。

点对点网络允许设备之间直接通信，无需通过服务器。点对点网络允许设备之间直接通信，无需通过服务器。这种方法减少了你需要的工作量。`client/server model` makes it easier to communicate because there is only one address to send。这种方法减少了你需要的工作量。

## 客户端/服务器网络

当今使用的主要的网络架构是客户端/服务器。这种方法利用专门的服务器来连接客户端。`client/server model` makes it easier to communicate because there is only one address to send. Instead of communicating with other clients, the client sends a message to the server, which then passes it to other clients. `client/server model` makes it easier to communicate because there is only one address to send.

## TCP/IP 栈

大多数网络使用 `TCP/IP` 栈。这种协议集合的设计是将应用程序与硬件隔离开。网络有多个层，从物理层（通过电缆传输数据）到应用层。

我们感兴趣的层是传输层（包含 `TCP`、`UDP` 和 `ICMP`）以及应用层。应用层是完全未定义的，可以用于任何内容。

> `ICMP`（互联网控制消息）是一种非常简单的协议，只能用于少数功能，且在游戏中并不真正适用。

## TCP

`TCP`（传输控制协议）是一种可靠的系统，它对数据进行错误检查。这些错误检查增加了包的大小，因此减少了你在单个包中可以发送的数据（例如，`TCP` 连接的 `MTU` 为 500）。

与 `UDP` 连接（将在下一节解释）不同，`TCP` 连接会与远程机器建立并直接发送数据。由于涉及错误检查，`TCP` 通常比 `UDP` 慢，因此不适用于紧急数据（如游戏数据），但对于需要可靠性的应用程序来说它是完美的。

## UDP

另一个选项 `UDP`（用户数据报协议）是你所要求的的最底层协议。它是一个快速、高效的系统，但不安全。所有的 `UDP` 数据包头都包含数据的目标地址（这是它唯一需要的）。然而，如果数据包在传输过程中丢失或损坏，它没办法。`UDP` 在游戏中的应用比 `TCP` 多，因为 `UDP` 具有性能优势。

## 套接字编程

套接字编程有时很容易，有时又很难，取决于你想做什么。遗憾的是，在我看来，`TCP` 选项比 `UDP` 更简单，但有一些函数适用于整个套接字领域。

### 打开套接字

`socket()` 函数为你打开初始套接字。该函数简单描述了你想要的套接字类型并返回一个套接字描述符。这些套接字描述符可以作为普通的文件描述符使用（例如由 `open()` 返回的），很好地体现了 UNIX “一切皆文件”的哲学。`socket()` 函数的原原型所示：

```c
int socket(int domain, int type, int protocol)
```

第一个参数 `domain`（域）指定了要使用的协议族。这应该是 `PF_INET` 或 `PF_INET6`（用于几年后使用的 IPv6 套接字）。有几个选项，但它们超出了本书的范围。

下一个参数 `type`（类型）是你想要使用的传输层类型。同样，尽管有多种可能，但你可能想使用 `SOCK_STREAM`（用于 TCP）或 `SOCK_DGRAM`（用于 UDP）。

最后一个参数 `protocol`（协议）是要使用的协议类型。它可以是 `IPPROTO_TCP` 或 `IPPROTO_UDP`。

`socket()` 函数在成功时返回一个有效的描述符；失败时返回 -1。

### 连接 socket

当你成功打开一个 socket 后，你必须指定具体想让它连接到哪里。你通过 `connect()` 函数来实现这一点。注意，只有在你在使用 TCP 套接字时才调用 `connect()`。`UDP` 是一种无连接协议，不需要此调用。

```c
int connect(int sockfd, struct sockaddr *serv_addr, int addrlen);
```

第一个参数 `sockfd` 是 `socket()` 返回的描述符。你将在整个过程中再次使用此值。下一个参数 `serv_addr` 是指向结构体的指针，该结构包含你要连接的地址的详细信息。虽然函数原型使用的是 `sockaddr` 类型，但在调用函数时你需要使用 `sockaddr_in` 结构并将其强制转换为正确的类型。该结构中你感兴趣的成员是 `sin_addr->saddr` 和 `sin_port`。第一个是你想要连接的机器的地址。你可以通过调用要连接主机的 `inet_aton` 函数（字符串形式）来确定此地址，随后提供一个指向 `in_addr` 结构中存储结果的指针。

`sin_port` 成员是你想要连接的端口号，必须以网络字节序指定。

> 注意
> 在指定任何类型的数字时，记住使用 `htons()` 函数，它会将主机特定的数字转换为网络字节序。

下文的示例代码演示了如何通过 TCP 连接到远程机器：

```c
#include <sys/socket.h>
#include <sys/types.h>
#define HOST "127.0.0.1"
#define PORT 80
int main(int argc, char *argv) {
    int sock;
    struct sockaddr_in *server;
    // 打开 socket
    sock = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == -1) {
        perror("Socket error:");
        return 1;
    }
    // 我们想连接到哪里？
    inet_aton(HOST, &(server)->sin_addr);
    server->sin_port = htons(PORT);
    server->sin_family = AF_INET;
    // 尝试建立连接
    if (connect(sock, server, sizeof(sockaddr_in)) == -1) {
        perror("Socket error:");
        return 1;
    }
    // 完成。
    close(sock);
    return 0;
}
```

## 发送数据

当你成功建立 socket 后，就可以向它发送数据了。有几种方法可以实现这一点，取决于 socket 的类型，从标准的文件 I/O 调用到 TCP 特有的 I/O 函数，以及介于之间的所有方法。

### 作为文件流打开 socket

我在本章早些时候提到，socket 描述符与通过 `open()` 调用创建的标准文件描述符是相同的。这种相似性允许你使用 `fdopen()` 函数来访问标准文件 I/O 函数，如 `fprintf()` 和 `fgets()`。

```c
FILE *fdopen(int filefd, char *mode);
```

该函数的作用与 `fopen()` 完全相同，只是你指定的是文件描述符（在此例中是 socket 描述符）而不是文件名。取决于你想要的访问类型，`mode` 字符串可以是任何标准的 `fopen()` 模式字符串（详情请参 `fopen` 手页）。

当你想要向 socket 发送数据时，可以使用标准文件 I/O 函数使用 `fprintf()` 向文件流写入原始文本（这对于明文协议，如 HTTP，非常有用）或使用 `write()` 写入（用于更复杂的数据类型）。

### 使用 send() 函数

如果你打开了一个 TCP 套接字，在与远程端建立连接后，可以使用 `send()` 函数。`send()` 函数接受四个参数：socket 描述符、要发送的数据、数据的长度以及一些标志。

```c
int send(int s, const void *msg, int len, unsigned int flags);
```

`flags` 参数可以由以下预定义值的组合组成：

| 名称 | 描述 |
| --- | --- |
| `MSG_OOB` | 发送带外数据。 |
| `MSG_DONTROUTE` | 忽略路由表；通常由路由器和诊断工具使用。 |
| `MSG_DONTWAIT` | 如果数据太大无法在一个数据包中发送，则不要阻塞。 |
| `MSG_NOSIGNAL` | 在发生 socket 错误时不产生 SIGPIPE 信号。 |

如果 `send()` 调用成功，它返回返回发送的字节数；出错时返回 -1。

### sendto() 函数

如果你在使用 UDP 套接字，你必须为每条消息指定目标。因此，你使用 `sendto()` 函数。

```c
int sendto(int s, const void *msg, int len, int flags, struct sockaddr *to, int addrlen);
```

第一个参数 `s` 是 socket 描述符。下一个参数 `msg` 是指向要发送数据的指针。`len` 参数是数据的长度。`flags` 参数可以是预定义值的组合。

最后两个参数 `to` 和 `addrlen` 分别指定目标地址及其大小。虽然函数原型使用的是 `sockaddr` 类型，但在调用函数时你需要使用 `sockaddr_in` 结构（如连接时那样）并将其强制转换为正确的类型。

## 接收数据

接收数据比发送稍微复杂。因为你不知道数据何时就绪，你可以使用 `select()` 函数，该函数将在后文介绍。

### recvfrom() 函数

要在 TCP 和 UDP 上接收消息，你都必须使用 `recvfrom()` 函数。注意，冗余函数 `recv()` 只是调用了带有 `NULL` 参数的 `recvfrom()`。

```c
int recvfrom(int s, void *msg, int len, int flags, struct sockaddr *from, int *from_len);
```

# select() 函数

如前节所述，`recvfrom()` 是一个阻塞函数，这意味着它会导致当前线程在继续执行之前等待。这并不是你希望应用程序在激烈的战斗序列中执行的操作。为了解决这个问题，你可以使用 `select()` 函数在调用 `recvfrom()` 之前确定是否有传入的消息。

```c
select(int n, fd_set *readfds, fd_set *writefds,
fd_set *exceptfds, struct timeval *timeout);
```

第一个参数 `n` 是三个集合中任何一个文件描述符的最大值加 1。接下来的三个参数分别是用于读取的数据、要写入的数据以及包含异常的数据的文件描述符块。最后一个参数 `timeout` 是在返回之前等待的时间。该参数应为 0（立即返回），但你也可以选择在此等待。请确保你永远不要在返回之前将此参数设置为 `NULL` 或让 `select()` 无期等待。

文件描述符块（或 `FD_SETs`）由一组宏控制。你不应该尝试编辑这些块。这些宏列举如下：

```c
FD_CLR(int fd, fd_set *fds)      // 从 fds (fd_set) 中移除 fd (描述符)
FD_ISSET(int fd, fd_set *fds)    // 检查 fd 是否在 fds 中
FD_SET(int fd, fd_set *fds)      // 将 fd 添加到 fds
FD_ZERO(fd_set *fds)             // 清空 fds
```

`select()` 函数返回包含描述符数量；如果在函数超时之前没有任何发生，则返回 0。如果返回 -1，则发生了错误。

## 另一个小型练习

在阅读下面的代码块之前，在本章不断完善的应用程序中添加一个循环，将所有传入的数据发送到 `stdout`。在需要的地方使用 `select()` 函数。

## 完整的微型浏览器

```c
#include <sys/socket.h>
#include <sys/types.h>
#include <stdio.h>
#include <string.h>
#include <malloc.h>
#define HOST "127.0.0.1"
#define PORT 80
#define BUFFERSIZE 1500
```

```c
int main(int argc, char **argv) {
    int sock;
    struct sockaddr_in *server;
    char *request = ("GET / HTTP/1.0\n\n");
    char *buffer;
    fd_set *readfd;
    // 打开 socket
    sock = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == -1) {
        perror("Socket error:");
        return 1;
    }
    // 我们想连接到哪里？
    inet_aton(HOST, &(server->sin_addr));
    server->sin_port = htons(PORT);
    server->sin_family = AF_INET;
    // 尝试建立连接
    if (connect(sock, server, sizeof(sockaddr_in)) == -1) {
        perror("Socket error:");
        return 1;
    }
}
```

```c
// 发送 HTTP 请求
send(sock, http_request, strlen(http_request), 0);
```

```c
// 为 select() 设置文件描述符
FD_ZERO(readfd);
FD_SET(sock, readfd);
```

```c
// 为接收数据分配内存
buffer = (char *)malloc(BUFFERSIZE);
```

```c
// 消息接收循环
while (1) {
  if (select(2, readfd, NULL, NULL, 0)) {
    // 有待读取的消息...
    recvfrom(sock, buffer, BUFFERSIZE, 0, NULL, NULL);
    fprintf(stdout, buffer);
  }
}
```

```c
// 我们完成了。
close(socket);
return 0;
```

## 创建服务器

服务器与客户端没有区别，不同之处服务器的初始化过程需要更多的精力。根据你所处理的服务器类型（TCP 或 UDP），在你的程序准备好提供服务之前，你必须调用一些额外的函数。

### 绑定 socket

在创建 socket 后，你不需要连接到服务器，而是必须将 socket 绑定到特定的端口。如果你使用 TCP，则通过 `bind()` 函数来实现。如果你使用 UDP，则在此时不需要任何操作。

```c
int bind(int sockfd, struct sockaddr *my_addr, int len);
```

第一个参数是那个熟悉的 socket 描述符。下一个参数 `my_addr` 是指向包含本地地址信息的结构的指针。你以与 `connect()` 建立 socket 相同的方式设置此结构，只需将 `sockaddr_in` 结构中的 `sin_addr` 成员设置为 `INADDR_ANY`。`bind()` 的最后一个参数是本地地址描述符的大小。

### 使用 listen() 函数

将 socket 绑定到端口后，你必须告诉 TCP/IP 子系统你愿意接受连接。这是通过 `listen()` 函数实现的：
