
将 `errno` 存储在全局变量中对于共享所有全局变量的多线程是不可行的。我们将在第 26 章中讨论该问题的解决方案。

在全文中，我们将使用诸如“`connect` 函数返回 `ECONREFUSED`”之类的短语，来表示该函数返回了错误（通常返回值为 -1），并且 `errno` 被设置为指定的常量。

- [ 团队李 ]

## 1.5 简单的日期时间服务器

我们可以编写一个简单的 TCP 日期时间服务器版本，它可以与 1.2 节中的客户端工作。我们使用了上一节描述的封装函数，并在图 1.9 中展示了该服务器。

### 图 1.9 TCP daytimepsrv.

```
intro/daytimetpsrv.c

#include "unp.h"
#include <time.h>

int
main(int argc, char **argv)
{
    int listenfd, connfd;
    struct sockaddr_in servaddr;
    char buff[MAXLINE];
    time_t ticks;

    listenfd = Socket(AF_INET, SOCK_STREAM, 0);

    bzero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(13); /* daytime server */

    Bind(listenfd, (SA *) &servaddr, sizeof(servaddr));

    Listen(listenfd, LISTEN);

    for ( ;; ) {
        connfd = Accept(listenfd, (SA *) NULL, NULL);

        ticks = time(NULL);
        sprintf(buff, sizeof(buff), "%.24s\r\n", ctime(&ticks));
        Write(connfd, buff, strlen(buff));
    }

    Close(connfd);
}
```

### 创建一个 TCP socket

10 TCP socket 的创建与客户端代码相同。

### 将服务器的已知端口绑定到 socket

11-15 通过填充 Internet socket 地址结构体并调用 `bind`，将服务器的已知端口（日期时间服务的 13 端口）绑定到 socket 上。我们将 IP 地址指定为 `INADDR_ANY`，这允许服务器在任何接口上接受客户端连接，以防服务器主机有多个接口。稍后我们将看到如何限制服务器仅在单个接口上接受客户端连接。

### 将 socket 转换为监听 socket

16 通过调用 `listen`，socket 被转换为监听 socket，内核将在该 socket 上接受来自客户端的连接。这三个步骤（`socket`、`bind` 和 `listen`）是任何 TCP 服务器准备我们所说的监听描述符（在本例中为 `listenfd`）的标准步骤。

常量 `LISTENQ` 来自我们的 `unp.h` 头文件。它指定了内核为该监听描述符队列的客户端连接最大数量。我们将在 4.5 节中详细讨论队列的内容。

### 接受客户端连接，发送响应

17-2 通常情况下，服务器进程在 `accept` 调用中进入睡眠状态，等待客户端连接的到达并被接受。TCP 连接使用所谓的三次握手来建立连接。当此握手完成后，`accept` 返回，该函数的返回值是一个新的描述符（`connfd`），被称为已连接描述符。这个新描述符用于与新客户端通信。对于每个连接到我们服务器的客户端，`accept` 都会返回一个新的描述符。

书中使用的无限循环样式为：

```
for ( ; ) {
  
}
```

库函数 `time` 返回当前的时间和日期，它返回自 Unix 纪元（协调世界时 1970 年 1 月 1 日 00:00:00）以来的秒数。下一个库函数 `ctime` 将此整数值转换为可读的字符串，如下：

Mon May 26 20:58:40 2003

`snprintf` 在字符串末尾附加回车符和换行符，结果通过 `write` 写入客户端。

如果你还没有习惯使用 `snprintf` 代替旧的 `sprintf`，现在是学习的时候了。`sprintf` 的调用无法检查目标缓冲区溢出。相反，`snprintf` 要求第二个参数是目标缓冲区的大小，这就不会导致溢出。

`snprintf` 是 ANSI C 标准中较晚添加的项，即所谓的 ISO C99 版本。几乎所有的供应商都作为标准库的一部分提供它，许多免费版本也同样可用。我们在全文中使用了 `snprintf`，并建议在所有程序中使用它来代替 `sprintf` 以确保可靠性。

令人惊讶的是，竟然有如此多的黑客通过发送数据导致服务器的 `sprintf` 调用溢出，从而发生网络入侵。

### 终止连接

22 服务器通过调用 `close` 关闭其连接。注意，对于 TCP 而言，`close` 就像连接一样是一个双向握手。客户端发送一个 FIN 段表示它没有更多数据要发送了。服务器响应一个 ACK，然后发送自己的 FIN 段。客户端响应一个 ACK，连接关闭。

TCP 连接状态机如图 2.21 所示。状态有 LISTEN、SYN-SENT、SYN-RCVD、ESTABLISHED、CLOSE-WAIT、FIN-WAIT1、FIN-WAIT2、TIME-WAIT 和 LAST-ACK。

TIME-WAIT 状态对于确保最终的 ACK 被对方确认，并允许当前连接的任何延迟段被丢弃非常重要。TIME-WAIT 状态的持续时间通常为最大段生存时间（MSL）的两倍。

| 图号 | 页码 | 描述 |
| :--- | :--- | :--- |
| 5.4 | 124 | TCP/IP4，依赖协议 |
| 6.9 | 168 | TCP/IP4， 使用 select |
| 6.13 | 174 | TCP, 使用 select 并对缓冲区操作 |
| 8.7 | 224 | UDP/IP4，依赖协议 |
| 8.9 | 247 | UDP, 验证服务器地址 |
| 8.17 | 256 | UDP, 调用 connect 获取同步错误 |
| 14.2 | 384 | UDP, 使用 SIGAL 读取服务器回复时超时 |
| 14.4 | 386 | UDP, 使用 select 读取服务器回复时超时 |
| 14.5 | 387 | UDP, 使用 SO_RCTIMEO 读取服务器回复时超时 |
| 15.4 | 418 | Unix 域套接流，依赖协议 |
| 15.6 | 419 | Unix 数据报文，依赖协议 |
| 16.3 | 438 | TCP, 使用阻塞 I/O |
| 16.10 | 447 | TCP, 使用 (fork) |
| 16.21 | 462 | TCP, 建立连接并发送 RST |
| 14.15 | 404 | TCP, 使用 dev/poll 进行多路复用 |
| 14.18 | 407 | TCP, 使用 select/queue 进行多路复用 |
| 20.5 | 537 | UDP, 存在竞态条件的广播 |
| 20.7 | 540 | UDP, 通过 pselect 修复竞态条件的广播 |
| 20.9 | 544 | UDP, 广播，通过 sigset 和 siglongjmp 修复竞态条件 |
| 20.10 | 547 | UDP, 广播，通过来自 IPC 信号处理程序的 sigjmp 修复竞态条件 |
| 22.6 | 600 | UDP, 使用超时、重传和序列号实现可靠性 |
| 26.2 | 680 | TCP, 使用两个线程 |
| 27.6 | 716 | TCP/IP4, 指定源路由 |
| 27.13 | 729 | UDP/IP6, 指定路由 |

图 1.13. 文中开发的不同版本的 echo 服务器。

| 图号 | 页码 | 描述 |
| :--- | :--- | :--- |
| 5.2 | 123 | TCP/IP4，依赖协议 |
| 5.12 | 139 | TCP/IP4，依赖协议，终止子进程 |
| 6.21 | 179 | TCP/IP4，依赖协议，使用 select，一个进程处理所有客户端 |
| 6.25 | 186 | TCP/IP4，依赖协议，使用 poll，一个进程处理所有客户端 |
| 8.3 | 242 | UDP/IP4，依赖协议 |
| 8.24 | 263 | TCP 和 UDP/IP4-协议依赖，使用 select |
| 14.14 | 400 | TCP, 使用标准 I/O 库 |
| 15.3 | 417 | Unix 域套接流，依赖协议 |
