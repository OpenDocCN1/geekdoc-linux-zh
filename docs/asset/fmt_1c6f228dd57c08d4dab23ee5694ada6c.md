
- 手册和书籍历史上一直认为，队列固定数量连接的原因是为了处理服务器进程忙于无法连续调用 `accept` 的情况。这意味着在两个队列中，完成队列的条目通常比未完成队列多。再次，网络服务器已经证明了这一点。设置大 `backlog` 的原因是未完成连接队列会随着 `SYN` 的到达而增长，等待三次握手的完成。

- 如果在客户端 `SYN` 到达时队列已满，`TCP` 会忽略到达的 `SYN`（`TCP2` 第 930–931 页）；它不会发送 `RST`。但该条件被认为是暂时的，客户端 `TCP` 将重传其 `SYN`，希望在不久后在队列中找到位置。如果服务器 `TCP` 立即响应 `RST`，客户端的 `connect` 将返回错误，强制应用程序处理这种状况，而不是让 `TCP` 的正常重传接管。此外，客户端无法区分响应 `SYN` 的表示“此端口没有服务器”的 `RST` 与表示“此处有服务器但队列已满”的 `RST`。某些实现在队列满时发送 `RST`，这种行为是错误的，除非客户端特别需要与此类服务器交互，否则最好忽略这种可能性。

- 数据在三次握手完成后、服务器调用 `accept` 之前到达，应该被放入队列，直到套接字的缓冲区。

# 图 4.10. `backlog` 取值的实际连接数。

| backlog | MacOS 10.2.6 | AIX 5.1 | Linux 2.4 | HP-UX | FreeBSD 4.8 | FreeBSD 5.1 | Solaris 2.9 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 1 | 3 | 1 | 1 | 1 | 1 |
| 1 | 2 | 4 | 2 | 2 | 2 | 2 |
| 2 | 4 | 5 | 3 | 3 | 3 | 3 |
| 3 | 5 | 6 | 4 | 4 | 4 | 4 |
| 4 | 7 | 7 | 6 | 5 | 5 | 5 |
| 5 | 8 | 9 | 7 | 6 | 6 | 6 | 6 |
| 6 | 9 | 11 | 8 | 7 | 7 | 7 | 7 |
| 7 | 11 | 13 | 9 | 8 | 9 | 9 | 9 |
| 8 | 13 | 14 | 11 | 10 | 11 | 11 | 11 |
| 9 | 14 | 16 | 12 | 11 | 13 | 13 | 13 |
| 10 | 16 | 17 | 13 | 12 | 15 | 15 | 15 |
| 11 | 17 | 19 | 14 | 13 | 17 | 17 | 17 |
| 12 | 19 | 20 | 15 | 14 | 19 | 19 | 19 |
| 13 | 20 | 22 | 16 | 15 | 21 | 21 | 21 |
| 14 | 22 | 23 | 17 | 16 | 22 | 23 | 23 |

## 4.6 `accept` 函数

`accept` 被 `TCP` 服务器调用，用于从已完成连接队列的头部返回下一个完成的连接（图 4.7）。如果已完成连接队列为空，该进程将进入睡眠（假设默认为阻塞套字）。

```c
#include <sys/socket.h>

int accept (int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

返回值：如果成功则返回非负描述符，出错时返回 `-1`

`addr` 和 `addrlen` 参数用于返回对端进程（客户端）的协议地址。`addrlen` 是一个“值-结果”参数（第 3.3 节）。在调用之前，我们通过 `*addrlen` 设置整数值，表示 `addr` 所指向的套字结构的大小；在返回时，该值包含内核存储在套字地址结构中的实际字节数。

如果 `accept` 执行成功，它的返回值是一个由内核自动创建的全新描述符。这个新描述符指向与客户端的 `TCP` 连接。在讨论 `accept` 时，我们将调用 `accept` 的第一个参数称为监听套字（由 `socket` 创建的描述符，也是调用 `bind` 和 `listen` 的第一个参数），而将 `accept` 返回的值称为已连接的套字。区分这两个套字至关重要。服务器通常只创建一个监听套字，它在服务器的生命周期内存在。对于每个被接受的客户端连接（即 `TCP` 三次握手完成），当服务器完成对该客户端的服务后，已连接的套字会被关闭。

该函数最多返回三个值：一个整数返回代码（用作错误指示）、客户端进程的协议地址（通过 `sockaddr` 指针）以及该地址的大小（通过 `addrlen` 指针）。如果我们对返回客户端的协议地址不感兴趣，则将 `sockaddr` 和 `addrlen` 都设为空指针。

图 1.9 显示了这些点。每次循环时，已连接的套字都会关闭，但监听套字在服务器运行期间一直保持开启。我们还看到 `accept` 的第二个第三第三参数是空指针，因为我们对客户端的身份并不感兴趣。

### 示例：值-结果参数

我们将通过修改图 1.9 的代码来展示如何处理 `accept` 的值-结果参数，以打印客户端的 `IP` 和端口。我们在图 4.11 中展示了这一点。

### 图 4.11 打印客户端 `IP` 地址和端口的日期服务器

`intro/daytimescsrv.c`

```c
#include <un.h> 
#include <time.h>
3 int
main(int argc, char **argv)
{
    int listenfd, confd;
    socklen_t len;
    struct sockaddr_in servaddr, cliaddr;
    char     buff[MAXLINE];
    time_t ticks;
    listenfd = Socket(AF_INET, SOCK_STREAM, 0);
    bzero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(13); /* 服务器 */
    Bind(listenfd, (SA *) &servaddr, sizeof(servaddr));
    Listen(listenfd, LISTEN_QUEUE);
    for ( ; ; ) {
        len = sizeof(cliaddr);
        confd = Accept(listenfd, (SA *) &cliaddr, &len);
        printf("%s, %d\n",
                inet_ntop(AF_INET, &cliaddr.sin_addr, buff, sizeof(buff)),
                ntoh(cliaddr.sin_port));
        ticks = time(NULL);
        sprintf(buff, buff, "%.24s\r\n", ctime(&ticks));
        Write(confd, buff, strlen(buff));
    }
}
```

### 新声明

我们定义了两个变量：`len`，它是一个值-结果变量；`cliaddr`，它将包含客户端的协议地址。

### Accept 并打印客户端地址

我们将 `len` 初始化为套字地址结构的大小，并将指向 `cliaddr` 结构的指针和指向 `len` 的指针作为 `accept` 的第二个第三三个参数。我们调用 `inet_ntop`（第 3.7 节）将套字地址结构转换为点分十 ASCII 字符串，并调用 `htons`（第 3.4 节）将 16 位端口号从网络序转换为主机序。

调用 `accept` 会让我们的服务器更具协议无关性，但此服务器已经依赖于 `IPv4`。我们将在图 11.13 中展示该服务器的协议无关版本。

如果我们在同一台主机上运行新服务器并运行客户端，连续连接两次，客户端将有如下输出：

```
solaris % timetetcpcli 127.0.0.1
Thu Sep 11 12:44:00 2003
solaris % timetetcpcli 192.168.1.20
Thu Sep 11 12:44:09 2003
```

我们首先将服务器的 `IP` 地址指定为回环地址（`127.0.0.1`），然后指定为 `192.168.1.20`。已连接的套字在每次循环时都会关闭，但监听套字在服务器运行期间一直保持开启。我们还看到 `accept` 的第二个第三个参数是空指针，因为我们对客户端的身份并不感兴趣。

```
solaris % timetetcpcli 127.0.0.1
Thu Sep 11 12:44:00 2003
```
