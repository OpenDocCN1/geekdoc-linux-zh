
39-48 如果到守护进程的 Unix 域连接可读，我们尝试读取 `icmpd_structure`。如果成功，我们打印相关信息。`strerror` 是一个比它更具移植性的函数示例。ANSI C 未规定函数的错误。Solaris 手页说如果参数超出范围，函数将返回空指针。这意味着上面的代码是不正确的，因为 `strerror` 可以返回空指针。FreeBSD 实现以及其他实现通过返回如 "Unknown error." 的字符串来处理无效参数。这是合理的，意味着上面的代码没有问题。POSIX 修改了这一点，由于没有返回值来指示错误，如果参数超出范围，函数会将 `errno` 设置为 `EINVAL`。这意味着完全符合的代码必须设置 `errno`、调用 `strerror`、测试 `errno` 是否等于 `EINVAL` 并在错误时打印消息。

## UDP Echo 示例

在查看守护进程源码之前，我们展示该客户端的一些示例。我们首先看到发送到未连接互联网的 IP 地址的数据报。

```
我们假设 `icmpd` 正在运行，并期望某些路由器返回 ICMP "host unreachable" 错误，但一个都没有收到。相反，我们的应用程序超时了。我们展示此是为了重申仍然超时，并且可能会产生 "host unreachable" 的 ICMP 消息。我们的下一个示例将数据报发送到未运行的主机的标准 echo 服务器。如预期收收到 ICMP "port unreachable"。
```

```
freebsd % udpcli 192.168.42.7

hello

ICMP error: Connection refused, type = 3, code = 3
```

我们再次尝试 IPv6 并如预期收收到 ICMPv6 "port unreachable"。

```
freebsd % udpcli 3ffe:b80:1f8d:2:204:acff:7

hello

ICMP error: Connection refused, type = 1, code = 4
```

我们对长行进行了封装。

## icmpd 守护进程

我们通过图 28.33 显示的 `icmpd.h` 头文件开始对 icmpd 守护进程的描述。

### client 数组

2-17 由于守护进程可以处理任意数量的客户端，我们使用 `client` 结构数组来保存每个客户端的信息。这与第 6 节使用的数据结构类似。除了到客户端的 Unix 域连接描述符外，我们还存储了 `family` 的 UDP socket (`AF_INET` 或 `AF_INET6`) 的地址以及绑定到该 socket 的端口号。我们还声明了函数原型和这些函数共享的全局变量

## 图 28.33 icmpd 守护进程的 icmpd.h 头文件。

`icmpd/icmp.h`

```c
#include "unpicmpd.h"

struct client {
    int conffd;      /* 到客户端的 Unix 域流 socket */
    int family;      /* AF_INET or AF_INET6 */
    int lport;       /* 绑定到客户端 UDP socket 的本地端口 */
    /* 网络字节序 */
} client[FD_SETSIZE];

/* 全局变量 */
int fd4, fd6, listenfd, maxi, maxfd, nready;
fd_set reset, allset;
struct sockaddr_un cliaddr;

/* 函数原型 */
int readable_conn (int);
int readable_listen (void);
int readable_v4 (void);
int readable_v6 (void);
```

## 图 28.34 main 函数的前部分：创建 socket。

`icmpd/icmpd.c`

```c
#include "icmpd.h"

int
main(int argc, char **argv)
{
    int             sockfd;
    struct sockaddr_un sun;
    if (argc == 1)
        err_quit("usage: icmpd");
    maxi = -1;      /* client [] 的索引 */
    for (i = 0; i < FD_SETSIZE; i++)
        client[i].conffd = -1; /* - 表示可用条目 */
    FD_ZERO(&allset);
    fd4 = Socket (AF_INET, SOCK_RAW, IPPROTO_ICMP);
    FD_SET(fd4, &allset);
    maxfd = fd4;
    #ifdef IPV6
    fd6 = Socket (AF_INET6, SOCK_RAW, IPPROTO_ICMP6);
    FD_SET(fd6, &allset);
    maxfd = max (maxfd, fd6);
    #endif
    listenfd = Socket (AF_UNIX, SOCK_STREAM, 0);
    sun.sun_family = AF_LOCAL;
    strcpy (sun.sun_path, ICMPD_PATH);
    unlink (ICMPD_PATH);
    Bind (listenfd, (SA *) &sun, sizeof (sun));
    Listen (listenfd, LISTENQ);
    FD_SET(listenfd, &allset);
    maxfd = max (maxfd, listenfd);
}
```

图 28.34 显示了 `main` 函数的前半部分。

### 初始化客户端数组

9-10 通过将连接的 `socket` 成员设置为 -1 来初始化客户端数组。

### 创建 socket

12-28 创建三个套接字：一个原始 ICMP4 socket、一个原始 ICMP6 socket 以及一个 Unix 域流式套接字。我们取消链接 `unlink` 任何之前存在的 Unix 域套接字实例，将其良名路径绑定到套接字，并调用 `listen`。这是客户端连接的套接字。还为 `select` 计算了最大描述符，并为 `accept` 调用配配了一个套接字地址结构。

图 28.35 显示了 `main` 函数的后半部分，这是一个无限循环，它调用 `select` 等待守护进程的任何描述符变为可读。

# 图 28.35 `main` 函数的后半部分：处理可读描述符。

`icmpd/icmpd.c`

```
29 for ( ; ) { allset;
30 rset = Select(maxfd + 1, &rset, NULL, NULL, NULL);
31 nready = Select(listenfd, &rset)
32 if (FD_ISSET (fd, &rset))
33 if (readable_listen (listenfd) <= 0)
34 continue;
35 if (FD_ISSET (fd, &rset))
36 if (readable_v4 (fd) <= 0)
37 continue;
38 #ifdef IPV6
39 if (FD_ISSET (fd6, &rset))
40 if (readable_v6 (fd) <= 0)
41 continue;
42 #endif
43 for (i = 0; i <= maxi; i++) { /* 检查所有客户端的数据 */
44 if (sockfd = client [i] .conndfd) < 0)
45 continue;
46 if (FD_ISSET(sockfd, &rset))
47 if (readable_conn (i) <= 0)
48 break; /* 没有更多可读的描述符 */
50 }
51 exit(0);
52 )
```
