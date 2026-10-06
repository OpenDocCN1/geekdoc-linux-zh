
```c
int main(int argc, char *argv[])
{
    /* 确保我们接收到了两个参数 */
    /* 使用 DNS 查找主机。gethostbyname （大多数 UNIX 版本中的它）可以正确 处理点分 IP 地址和主机名。 */
    printf("Looking up %s...\n", argv[1]);
    hostlist = gethostbyname(argv[1]);
    if (hostlist != NULL) {
        printf("Unable to resolve %s.\n", argv[1]);
        return 1;
    }
    /* 好，我们有一个地址。但是，某些站点 正在迁移到 IPv6（IP 的新版本）， 而我们还没有准备好（因为它使用了 新的地址格式）。检查这一点是个好主意。 */
    if (hostlist->h_addrtype != AF_INET) {
        printf("%s does not seem to be an IPv4 address.\n", argv[1]);
        return 1;
    }
    /* inet_ntop 将 32 位 IP 地址转换为 点分字符串表示（适用于打印）。 hostlist->h_addr_list 是可能地址的数组 （以防一个名称解析到多个 IP）。在大多数 情况下，我们只需要第一个。 */
    inet_ntop(AF_INET, hostlist->h_addr_list[0], dotted_ip, 15);
    printf("Resolved to %s.\n", argv[1], dotted_ip);
    /* 为连接创建一个套接字。 */
    sock = socket(PF_INET, SOCK_STREAM, IPPROTO_IP);
    if (sock < 0) {
        printf("Unable to create a socket: %s\n", strerror(errno));
        return 1;
    }
    /* 填充 sockaddr_in 结构体。地址 已经是网络字节序（来自 gethostbyname 调用）。我们需要使用 htons 宏 转换端口号。在执行任何其他操作之前，我们将清空 整个结构体。 */
    memset(&sa, 0, sizeof(struct sockaddr_in));
    port = atoi(argv[2]);
    sa.sin_port = htons(port);
    /* IP 地址以 char * 形式返回，适用于 各种地址。 将其拷贝到 sockaddr_in 结构体中。 */
    memcpy(&sa.sin_addr, hostlist->h_addr_list[0], hostlist->h_addr_length);
    /* 这是一个 Internet 套接字。 */
    sa.sin_family = AF_INET;
    /* 连接！ */
    printf("Trying %s on port %i...\n", dotted_ip, port);
    if (connect(sock, (struct sockaddr*)&sa, sizeof(sa)) < 0) {
        printf("Unable to connect: %s\n", strerror(errno));
        return 1;
    }
    printf("Connected! Reading data. Press Ctrl-C to quit.\n");
    /* 为 Ctrl-C (SIGINT) 安装信号处理器。 */
    /* 更多信息请参阅 signal(2) 手页。 */
    signal(SIGINT, signal_handler);
    /* 读取数据，直到遇到错误。 */
    for (;;) {
        char ch;
        int amt;
        /* 逐字节读取。 这非常低效。 */
        amt = read(sock, &ch, 1);
        /* 务必检查网络读取的错误。 它们比本地文件 访问要可靠得多。 */
        if (amt < 0) {
            printf("\nRead error: %s\n", strerror(errno));
            break;
        } else if (amt == 0) {
            /* 读取 0 字节意味着连接 已关闭。read 会等待到 可以至少返回一个字节。 */
            printf("\nConnection closed by remote system.\n");
            break;
        }
        /* 将字符写入标准输出。 */
        putchar(ch);
        fflush(stdout);
    }
    /* 关闭连接。 */
    printf("Closing socket.\n");
    close(sock);
    return 0;
}
```

让我们从顶部开始。网络程序通常包含很多额外的头文件。除了常规的 `stdio.h` 和 `stdlib.h` 之外，我们还需要（无特定要求）`unistd.h`（实用的 UNIX 函数）、`netinet/in.h`（用于 `in_addr` 和 `sockaddr_in` 类型）、`netdb.h`（用于 DNS）、`arpa/inet.h`（用于 `inet_ntop` 和其他转换函数）以及 `socket.h`（用于 socket 和相关函数）。为了让我们的生活更加复杂，这些头文件在不同的套接字实现（不同的 UNIX 类型）之间存在差异。这是一个“散弹策略”可能不是坏主意的用例——如果不确定，就把它们全部包含。（更好的主意是使用 Autoconf。）

# Linux 下的网络游戏

我们从 `main` 函数开始查找远程系统的 IP 地址。用户可以在命令行上传递 IP 地址或主机名，我们使用 `gethostbyname` 将其转换为 32 位 IP 地址。`gethostbyname` 接收一个字符串（可以是 IP 地址或主机名），并能正确处理点分 IP 地址和主机名。

`sock`—要转换为监听器的套接字。`queue`—期望的连接队列大小。这是可以尝试连接到此服务器但未被接受的客户端数量。如果你使用线程在后台处理客户端，合理的数字可能是 5 或 10。否则，你必须根据预期的客户端负载来确定此值。

# Linux 下的网络化游戏

## 287

`Function accept(sock, addr, addr_len)`

概要：从给定的套接字接收传入的连接。将有关客户端的信息（其 IP 地址和端口号）存储在 `addr` 中。如果没有待处理的连接（没有人尝试连接），`accept` 将处于等待状态（除非处于非阻塞模式，这超出了我们目前的讨论范围）。

成功时返回 0，失败返回 –1。

参数：
- `sock`—用于检查传入连接的监听型套接字。
- `addr`—指向 `sockaddr` 结构体的指针（Internet 套接字使用 `sockaddr_in`），用于接收有关连接客户端的信息。
- `addr_len`—指向整数的指针，用于接收地址结构的大小。对于 Internet 套接字，这将是 `sizeof(struct sockaddr_in)`。

现在，让我们编写一个可以与上一节中写的客户端通信的服务器。

# 代码列表 7–2 (tcpserver.c)

```c
/* Simple TCP/IP 服务器程序。 */
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <signal.h>
#include <unistd.h>
#include <netinet/in.h>
#include <netdb.h>
#include <arpa/inet.h>
#include <sys/socket.h>
char dotted_ip[15];      /* 用于将解析出的地址转换为可读格式的缓冲区。 */
```

288
第 7 章

```c
int listener;
int client;
int port;
struct sockaddr_in sa;
socklen_t sa_len;
/* 我们的监听套接字。 */
/* 当前客户端的套接字。 */
/* 我们接受连接的端口。 */
/* 连接地址。 */
/* sa 的长度。在简单情况下 这有一点多余，但套接字 不仅仅是为了 TCP/IP。 */
/* 此函数每当用户按下 Ctrl-C 时就会调用。 更多信息请参阅 signal(2) 手页。 */
void signal_handler(int sign)
{
    switch (sign) {
    case SIGINT:
        printf("\n收到中断信号。正在退出。\n");
        close(client);
        close(listener);
        exit(0);
    default:
        printf("\n收到未知信号。忽略。\n");
    }
}
int main(int argc, char *argv[])
{
    /* 确保我们收到了两个参数， 主机名和端口号。 */
    if (argc < 2) {
        printf("Simple TCP/IP uptime server.\n");
        printf("Usage: %s <port>\n", argv[0]);
        return 1;
    }
    port = atoi(argv[1]);
    /* 创建监听套接字。此套接字将队列 传入的连接。 */
    listener = socket(AF_INET, SOCK_STREAM, IPPROTO_IP);
    if (listener < 0) {
        printf("Unable to create a listener socket: %s\n", strerror(errno));
        return 1;
    }
    /* 现在将监听器绑定到本地地址。这使用了 与 connect 相同的 sockaddr_in 结构。 */
    sa_len = sizeof(sa);
    memset(&sa, 0, sa_len);
    sa.sin_family = AF_INET;
    sa.sin_port = htons(port);
    sa.sin_addr.s_addr = htonl(INADDR_ANY); /* 在 接口上监听。 */
    if (bind(listener, &sa, sa_len) < 0) {
        printf("Unable to bind to port %i: %s\n", port, strerror(errno));
    }
    /* 让网络系统知道我们在这个套接字上 接受连接。请求一个五个客户端的连接 队列。（如果我们在调用 accept 之前有超过五个客户端 尝试连接，某些 可能会被拒绝。） */
    if (listen(listener, 5) < 0) {
        printf("Unable to listen: %s\n", strerror(errno));
    }
    /* 准备绪！现在接受连接直到用户按下 Ctrl-C。 */
    signal(SIGINT, signal_handler);
    for (;;) {
        char sendbuf[1024];
        int sent, length;
        FILE *uptime;
        client = accept(listener, &sa, &sa_len);
        if (client < 0) {
            printf("Unable to accept: %s\n", strerror(errno));
            close(listener);
            return 1;
        }
        /* 我们现在有一个活跃的客户端。打印它的信息，然后通过线路发送一些内容。 */
        inet_pton(AF_INET, &sa.sin_addr, dotted_ip, 15);
        printf("Received connection from %s\n", dotted_ip);
        /* 使用 popen 获取 uptime 的输出。 */
        uptime = popen("/bin/uptime", "r");
        if (uptime == NULL) {
            printf("Unable to run uptime: %s\n", strerror(errno));
            continue;
        }
        while (fgets(sendbuf, sizeof(sendbuf), uptime)) {
            printf("%s", sendbuf);
            /* 确定要发送的数据。 */
            length = strlen(sendbuf);
            sent = write(client, sendbuf, length);
            if (sent < 0) {
                if (errno == EINTR) {
                    continue;
                } else {
                    printf("Write error: %s\n", strerror(errno));
                    break;
                }
            }
            sendbuf[sent] = '\0';
            printf("Sent: %s\n", sendbuf);
        }
        pclose(uptime);
        break;
    }
}
```

309
# Linux 下的网络化游戏

# 处理客户端

Linux 是一个多任务操作系统，有很多方法可以实现这一点，但我认为简单的方法为每个客户端创建一个线程。如果你对编写网络服务器感兴趣，建议阅读《Pocket Guide to TCP/IP Sockets》。

# 使用 UDP

UDP 是一个无连接的协议。TCP 可以比作电话对话，而 UDP 更像邮政系统。它处理的是独立寻址的数据包，而不是流的一部分。UDP 非常适合在网络上肆意发布游戏更新。它们并非都能到达，但只要足够数量就能保持游戏顺利运行。正如我们对 TCP 所的那样，我们将通过一个发送端和一个接收端演示 UDP。如下：

# 代码列表 7–3 (udpsender.c)

311
# Linux 下的网络化游戏

```c
#include <arpa/inet.h>
#include <sys/socket.h>
```
`struct hostent *hostlist;`
`char dotted_ip[15];`
- 由 `gethostbyname` 返回的主机列表。 *
- 用于将解析出的地址转换为可读格式的缓冲区。 *
- 端口号。 *
- 我们的连接套接字。 *

`int port;`
`int sock;`
`struct sockaddr_in sa;`
`int packets_sent = 0;`
/* 此函数每当用户按下 Ctrl-C 时就会调用。 更多信息请参阅 signal(2) 手页。 */

```c
void signal_handler(int signum)
{
    switch (signum) {
        case SIGINT:
            printf("\n收到中断信号。正在退出。\n");
            close(sock);
            exit(0);
        default:
            printf("\n收到未知信号。忽略。\n");
    }
}
```

```c
int main(int argc, char *argv[])
{
    /* 确保我们收到了两个参数， 主机名和端口号。 */
    if (argc < 3) {
        printf("\nSimple UDP datagram sender.\n");
        printf("Usage: %s <hostname or IP> <port>\n", argv[0]);
        return 1;
    }
    /* 使用 DNS 查找主机名。gethostbyname （在大多数 UNIX 版本中）正确地 */
    hostlist = gethostbyname(argv[1]);
    if (hostlist == NULL) {
        printf("Error looking up hostname %s: %s\n", argv[1], strerror(errno));
        continue;
    }
    sock = socket(AF_INET, SOCK_DGRAM,0);
    if (sock < 0) {
```
