
## 5.8 我们的客户端运行在一个小端 Intel 系统上，其中值为 1 的 32 位整数的存储方式如图 E.2 所示。

### 图 E.2. 小端格式下 32 位整数 1 的表示。

![](img/ab2a67f72092d143e16c9adbe684e62b_1085_0.png)

4 个字节按照 `A`, `A+1`, `A+2` 和 `A+3` 的顺序通过套字发送，它们以大端格式存储，如图 E.3 所示。

### 图 E.3. 图 E.2 中 32 位整数在大端格式下的表示。

![](img/ab2a67f72092d143e16c9adbe684e62b_1085_1.png)

这个 `0x01000000` 的值被解释为 16,777,216。同样，客户端发送的整数 2 在服务器端会被解释为 `0x02000000`，或 33,554,432。这两个整数之和为 50,331,648，或 `0x03000000`。当大端格式值被发送到客户端时，它在客户端上被解释为整数 3。

-22 的 32 位整数在小端系统上的表示如图 E.4 所示（假设负数采用补码表示）。

### 图 E.4. 小端格式下 32 位整数 -22 的表示。

![](img/ab2a67f72092d143e16c9adbe684e62b_1085_2.png)

这在大端服务器上被解释为 `0xffffeffff`，或 -321,537。同样，-77 的小端表示是 `0xffffffb3`，但它在大端服务器上被表示为二进制结果 `0xb3ffff`，或 -1,275,417。服务器上的加法运算得到二进制结果 `0xe9ffffff`，或 -627,954。这个大端值通过套字发送，在客户端被解释为小端值 `0xfeffff9e`，或 -16,777,314。

## 5.9 这种技术是正确的（将二进制值转换为网络字节序），但不能使用 `htonl` 和 `ntohl` 函数。尽管 `long` 函数在逻辑上看起来是“长”的，但这些函数操作的是 32 位整数（第 3.4 节）。在 64 位系统上，`long` 可能会占用 64 位，这些函数将无法正常工作。人们可以定义新函数 `hton64` 和 `ntohl64` 来解决这个问题，但这在使用 32 位表示 `long` 的系统上将无效。

## 5.10 在第一种场景下，服务器在图 5.20 的 `read` 调用处阻塞，因为客户端没有发送数据。

# 第 6 章

## 6.1 整数数组位于结构体中。

## 6.2 `select` 告诉我们套字是可写的。

## 6.4 并不是 POSIX.1 的一部分，但是是 Unix 98 的。

## 6.5 服务器应用程序持续向客户端发送数据，客户端 TCP 会予以确认并丢弃。

## 6.6 使用 `shutdown` 关闭 `SHUT_WR` 或 `SHUT_RDWR` 总是发送 `FIN`，而 `close` 仅在套字引用计数为 1 时才发送 `FIN`。

## 6.7 `read` 返回错误，我们的 `Read` 封装函数终止了服务器。服务器必须比这更健壮。注意我们在图 6.26 中处理了这种情况，尽管代码仍然不完善。考虑如果客户端与服务器的某个响应之间的连接丢失会发生什么，最终返回可能是 `TIMEDOUT`。

通常情况下，服务器不应因此类错误终止。它应该记录错误、关闭套字并继续服务其他客户端。意识到在这样一个进程处理所有客户端的服务器中，通过终止来处理此类错误是不可接受的。但如果服务器是处理单个客户端的子进程，那么一个子进程终止不会影响父进程（我们假设它处理所有新连接并产生子进程），也不会影响服务其他客户端的其他子进程。

# 第 7 章

## 7.2 图 E.5 显示了本练习题的一种解决方案。我们删除了对服务器返回的数据字符串的打印，因为不需要该值。

### 图 E.5 建立连接前后的套接字接收缓冲区大小和 MSS 打印。

`socket/rcvbuf.c`

```c
#include "unp.h"
#include <netinet/tcp.h>    /* 用于 TCP_MAXSEG */

int
main(int argc, char **argv) {
    int sockfd, rcvbuf, mss;
    socklen_t len;
    struct sockaddr_in servaddr;

    if (argc != 2)
        err_usage("usage: rcvbuf <IPAddress>\n\n", argv[0]);

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    len = sizeof(rcvbuf);
    getsockopt(sockfd, SOL_SOCKET, SO_RCVBUF, &rcvbuf, &len);
    len = sizeof(mss);
    getsockopt(sockfd, IPPROTO_TCP, TCP_MAXSEG, &mss, &len);
    printf("after defaults: SO_RCVBUF = %d, MSS = %d\n", rcvbuf, mss);

    zero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(13);    /* 日光服务器 */
    inet_pton(AF_INET, argv[1], &servaddr.sin_addr);

    connect(sockfd, (struct sockaddr *)&servaddr, sizeof(servaddr));

    len = sizeof(rcvbuf);
    getsockopt(sockfd, SOL_SOCKET, SO_RCVBUF, &rcvbuf, &len);
    len = sizeof(mss);
    getsockopt(sockfd, IPPROTO_TCP, TCP_MAXSEG, &mss, &len);
    printf("after connect: SO_RCVBUF = %d, MSS = %d\n", rcvbuf, mss);

    exit(0);
}
```

首先，程序没有所谓的“正确”输出。输出结果随系统而异。某些系统（特别是 Solaris 2.5.1 及早期版本）对套接字缓冲区大小始终返回 0，这导致我们无法观察连接过程中该值发生了什么变化。

关于 MSS，连接前打印的值是默认值（通常为 536 或 512），连接后打印的值取决于对端可能提供的 MSS。例如，在本地以以太网路上，连接后的值为 1,460。在连接到远程网络上的服务器后，MSS 可能与默认值相似，除非你的系统支持 MTU 发现。如果可能，在程序运行时使用类似 `tcpdump`（第 C.5 节）的工具，查看对端发送的 SYN 段中实际的 MSS 选项。

关于套接字接收缓冲区大小，许多实现在连接建立后会将该值缩小为 MSS 的倍数。另一种检查连接后套接字接收缓冲区大小的方法是使用类似 `tcpdump` 的工具监控数据包，并查看 TCP 的通窗口（advertised window）。

## 7.3 分配一个名为 `ling` 的 `linger` 结构体并按如下方式初始化：

```c
str_cli(stdin, sockfd);
ling_l_onoff = 1;
ling_l_linger = 0;
setsockopt(sockfd, SOL_SOCKET, SO_LINGER, &ling, sizeof(ling));
exit(0);
```

这应该导致客户端 TCP 使用 `RST` 终止连接，而不是正常的四段式挥手。服务器子进程的 `readline` 调用返回 `ECONNRESET` 错误，消息打印如下：

```
readline error: Connection reset by peer
```
