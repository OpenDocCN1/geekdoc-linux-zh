
```c
#define BSD_SOURCE    /* 为了从 <netdb.h> 获取 hstrerror 声明 */
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include "tlpi_hdr.h"

int
main(int argc, char *argv[])
{
    struct hostent *h;
    char **pp;
    char str[INET6_ADDRSTRLEN];

    for (argv++; *argv != NULL; argv++) {
        h = gethostbyname(argv);
        if (h == NULL) {
            printf(stderr, "gethostbyname() failed for '%s': %s\n",
                argv, hstrerror(h_errno));
            continue;
        }
    }

    printf("Canonical name: %s\n", h->h_name);

    printf(" alias(es): %s\n", "");
    for (pp = h->h_aliases; *pp != NULL; pp++) {
        printf("%s, %s", *pp, pp);
    }
    printf("\n");
}
```

套接字：Internet域域 1233

`sockets/t_gethostbyname.c`

## 59.13.3 getservbyname() 和 getservbyport() 函数

`getservbyname()` 和 `getservbyport()` 从 `/etc/services` 文件（第59.9节）中检索记录。这些函数现在已被 `getaddrinfo()` 和 `getnameinfo()` 取代了。

```c
#include <netdb.h>

struct servent *getservbyname(const char *name, const char *proto);
struct servent *getservbyport(int port, const char *proto);
```

> 成功时返回指向（静态分配的）`servent` 结构的指针，出错时返回 `NULL`

`getservbyname()` 查找服务名匹配 `name`（或其别名之一）且协议匹配 `proto` 的记录。`proto` 参数是一个诸如 `tcp` 或 `udp` 的字符串，也可以是 `NULL`。如果将 `proto` 指定为 `NULL`，则返回任何服务名匹配 `name` 的记录。（这通常足够了，因为在 `/etc/services` 文件中，具有相同名称的 UDP 和 TCP 记录通常具有相同的端口号。）

如果找到匹配的记录，`getservbyname()` 返回一个指向后续类型静态分配结构的指针：

```c
struct servent {
    char *s_name;      /* 官方服务名 */
    char **s_aliases;  /* 别名指针（NULL 终止） */
    int port;           /* 端口号（网络字节序） */
    char *s_proto;     /* 协议 */
};
```

通常，我们调用 `getservbyname()` 仅是为了获取端口号，它返回在 `s_port` 字段中。

`getservbyport()` 执行 `getservbyname()` 的反向操作。它返回一个包含来自 `/etc/services` 信息的 `servent` 记录，其端口匹配 `port` 且协议匹配 `proto`。再次，我们可以将 `proto` 指定为 `NULL`，在这种情况下，调用将返回任何端口号匹配 1234 第59章 `port` 中指定端口的记录。（在上述提到的少数情况下，即相同端口号在 UDP 和 TCP 中映射到不同的服务名，可能不会返回预期的结果。）

`getservbyname()` 函数的用法示例位于本书源码发行的 `files/t_getservbyname.c` 中。

## 59.14 UNIX 与 Internet 域套接字

在编写在网络上通信的应用程序时，我们必须使用 Internet 域套接字。然而，当使用套接字在同一系统的应用程序之间进行通信时，我们可以在 Internet 或 UNIX 域套接字之间选择。在这种情况下，我们应该使用哪种域？为什么？

使用 Internet 域套接字编写应用程序通常是最简单的方法，因为它既可以在单主机上工作，也可以跨网络工作。然而，在某些情况下我们选择使用 UNIX 域套接字的理由：

- 在实现上，UNIX 域套接字比 Internet 域套接字快。

- 我们可以使用目录（在 Linux 上是文件）权限来控制对 UNIX 域套接字的访问，使得只有指定用户或组 ID 的应用程序连接到监听套接字或数据报套接字。这提供了一种验证客户端的简单方法。对于 Internet 域套接字，如果我们想验证客户端，我们需要做更多工作。

- 使用 UNIX 域套接字，我们可以传递打开的文件描述符和服务器凭据，如第61.13.3 节所述。

### 59.15 更多信息

有丰富的印刷和在线资源：

- *The Unix/Linux Programming Interfaces, Volume 1: Advanced Sockets in C*, Michael Stevens (2003).

- *Computer Networking: A Top-Down Approach*, James Kurose and Keith Ross (2016).

- *TCP/IP Illustrated, Volume 1: The Protocols*, W. Richard Stevens (1994).

- *Unix Communications: The Design Interface*, W. Richard Stevens (1987).

- *The Internet: A User's Guide*, Charles P. Stone (1993).

- *Computer Networks*, Andrew S. Tanenbaum (2011).

- *Applied Internet Programming: TCP/IP Skills*, Brian W. (2003).

... （此处省略重复的列表内容）

`rbuf` 指向的数据结构。该结构包含一个数据缓冲区空间、该缓冲区的大小，以及指向该缓冲区中下一个“未读”字符的指针。它还包含了在参数 `fd` 中提供的文件描述符的拷贝。第二个函数 `readLineBuf(&rbuf)` 返回与 `rbluf` 关联的缓冲区中的下一行。如果需要，此函数将从存储在 `rbuf` 中的文件描述符进一步读取另一块数据。实现这两个函数。修改列表 59-6 (`is_segment_sv_c`) 和列表 59-7 (`is_segment_cl_c`) 中的程序以使用这些函数。

- **59-2.** 修改列表 59-6 (`is_segment_sv_c`) 和列表 59-7 (`is_segment_cl_c`) 中的程序，以使用列表 59-9 (`inet_sockets.c`) 中提供的 `inetListen()` 和 `inetConnect()` 函数。

- **59-3.** 编写一个 UNIX 域套接字库，其 API 与在第 59.12 节所示的 Internet 域套接字库类似。重写列表 57-3 (`us_xfr_sv.c`, 第 1168 页) 和列表 57-4 (`us_xfr_cl.c`, 第 1169 页) 中的程序以使用该库。

- **59-4.** 编写一个存储名称-值对的网络服务器。该服务器应该允许客户端对名称进行添加、删除、修改和检索。编写一个或多个客户端程序来测试该服务器。可选地，实现某种安全机制，允许创建该名称的客户端删除该名称或修改与其关联的值。

- **59-5.** 假设我们创建了两个 Internet 域数据报套接字并绑定到特定的地址，并将第一个套接字连接到第二个套接字。如果我们创建第三个数据报套接字，并尝试通过该套接字向第一个套接字发送（`sendto()`）数据报会发生什么？编写一个程序来确定答案。

# 60

## 套接字：服务器设计

本章讨论了迭代式和并发服务器的设计基础，以及 `inetd`——这是一种旨在方便创建 Internet 服务器的特殊守护进程。

## 60.1 迭代式和并发服务器

使用套接字设计网络服务器的两种常用设计如下：

- *迭代式 (Iterative)*：服务器一次只处理一个客户端，在完全处理该客户端的请求（s）之后再处理下一个客户端。

- *并发式 (Concurrent)*：服务器被设计为同时处理多个客户端。

我们已经在第 44.8 节中看过了一个使用 FIFO 的迭代式服务器示例，并在第 46.8 节中看过了一个使用 System V 消息队列的并发服务器示例。

迭代式服务器通常只在客户端请求可以快速处理时适用，因为每个客户端必须等待之前所有的客户端都处理完毕。使用迭代式服务器的典型场景是客户端和服务器交换单个请求和响应。

当处理每个请求需要大量的处理时间，且客户端和服务器进行长时间对话并来回传递消息时，并发服务器是合适的。在本章中，我们主要关注设计并发服务器的传统（也是简单）的方法：为每个客户端创建一个新的子进程。每个服务器执行所有任务来服务单个客户端并终止。这些进程中的每一个都可以独立运行，可以同时处理多个客户端。主服务器进程（父进程）的主要任务是为每个客户端创建一个新的子进程。（此方法的变体是为每个客户端创建一个新线程）。

在接下来的节中，我们将查看使用 Internet 域套接字的迭代式和并发服务器示例。这两个服务器实现了回显服务（RFC 862），这是一种返回客户端发送的任何拷贝的原始服务。

## 60.2 一个迭代式 UDP 回显服务器

在本节和下一节中，我们将介绍用于回显服务的服务器。回显服务器运行在 UDP 和 TCP 端口 7 上。（由于这是一个保留端口，回显服务器必须以超级用户权限运行）。

UDP 服务器持续读取数据报，向发送者返回数据报的拷贝。由于服务器每次只需要处理一条消息，因此迭代式服务器设计就足够了。服务器的头文件所示列表 60-1。

### 列表 60-1：id_echo_sv.c 和 id_echo_cl.c 的头文件

```c
#include "inet_sockets.h"    /* 声明我们的套接字函数 */
#include "tlp_hdr.h" sockets/id_echo.h
```

```c
#define SERVICE "echo"           /* UDP 服务名称 */
#define BUF_SIZE 500             /* 客户端和服务器可以
读取的数据报的最大大小 */ sockets/id_echo.h
```

列表 60-2 显示了服务器的实现。请注意关于服务器实现的以下几点：

- 我们使用第 37.2 节中的 `becomeDaemon()` 函数将服务器转换为守护进程。

- 为了缩短程序，我们使用了在第 59.9 节中开发的 Internet 域套接字。

- 如果服务器无法向客户端发送回复，它将使用 `syslog()` 记录消息。

在实际应用中，我们可能会对使用 `syslog()` 写入的消息限制速率，但为了防止攻击者填充系统日志的可能性，并且由于每次调用 `syslog()` 都是昂贵的，因为（默认情况下）`syslog()` 实际上会调用 `fsync()`。

### 列表 60-2：实现回显服务的迭代式服务器

```c
#include <syslog.h>
#include "id_echo.h"
#include "become_daemon.h"

int
main(int argc, char *argv[])
{
    int sfd;
    ssize_t numRead;
    socklen_t len;
    struct sockaddr_storage claddr;
    char buf[BUF_SIZE];
    char addrStr[ADDR_LEN];

    if (becomeDaemon(0) == -1)
        errExit("becomeDaemon");

    sfd = netbind(SERVICE, SOCK_GRAM, &addrlen);
    if (sfd == -1)
        syslog(LOG_ERR, "Could not create server (%s)", strerror(errno));

    for (;;) {
        len = sizeof(struct sockaddr_storage);
        numRead = recvfrom(sfd, buf, BUF_SIZE, 0, (struct sockaddr *)claddr, &addrlen);
        if (numRead == -1)
            errExit("recvfrom");

        if (sendto(sfd, buf, numRead, 0, (struct sockaddr *)claddr, addrlen) != numRead)
            syslog(LOG_WARNING, "Error sending response to %s",
                inetAddress((struct sockaddr *)claddr), addrStr));
    }
}
```

`id_echo_sv.c`

为了测试服务器，我们使用列表 60-3 所示的客户端程序。该程序也使用了 59.12 中的 Internet 域套接字库。作为第一个命令行参数，客户端期望服务器所在的主机。客户端执行一个循环，将每个命令行参数作为单独的数据报发送，并读取并打印服务器返回的响应。

### 列表 60-3：回显服务的客户端

```c
#include <stdio.h>
#include <string.h>
#include "id_echo.h"

int
main(int argc, char *argv[])
{
    int sfd, j;
    size_t len;
    ssize_t numRead;
    char buf[BUF_SIZE];

    if (argc < 2 || strcmp(argv[1], "--help") == 0)
        usageerror("%s host msg...\n", argv[0]);

    /* 从第一个命令行参数构造服务器地址 */
    sfd = inetConnect(argv[1], SERVICE, SOCK_DGRAM);
    if (sfd == -1)
        fatal("Could not connect to server socket");

    /* 将剩余命令行参数作为单独的数据报发送 */
    for (int j = 2; j < argc; j++) {
        len = strlen(argv[j]);
        if (write(sfd, argv[j], len) != len)
            fatal("partial/failed write");
    }

    numRead = read(sfd, buf, BUF_SIZE);
    if (numRead == -1)
        errExit("read");

    printf("%ld bytes.%.*s\n", (long)numRead, (int)numRead, buf);
}

    exit(EXIT_SUCCESS);
}
```

`id_echo_cl.c`

## 60.3 并发 TCP 回显服务器

TCP 回显服务也运行在端口 7。TCP 回显服务器接受一个连接，然后持续循环，读取所有传输的数据并通过同一个套接字将其发送回客户端。服务器将继续读取，直到检测到文件结束（end-of-file），此时它将关闭其套接字（这样，如果客户端仍在从其套接字读取，则它将看到文件结束）。

由于客户端可能会向服务器发送无限量的数据（因此为客户端提供服务可能需要无限的时间），并发设计是合适的，这样就可以同时为多个客户端提供服务。服务器的实现在列表 60-4 中所示。注意关于该实现的以下几点：

- 服务器通过调用第 37.2 节所示的 `becomeDaemon()` 函数变为守护进程（daemon）。

- 为了缩短程序长度，我们使用了列表 59-9（第 1228 页）所示的 Internet 域套接字。

由于 由于服务器为每个客户端连接创建一个子进程，我们必须确保它们被收回（reaped）。我们使用 `SIGCHLD` 处理器来实现这一点。

- 服务器的主体由一个循环组成，该循环接受客户端连接，然后通过 `fork()` 创建一个子进程，该子进程调用 `handleRequest()` 函数来处理该客户端。与此同时，父进程继续执行 fork 循环以接受下一个客户端连接。

在实际应用中，我们可能会在服务器中包含一些代码，对我们可以创建的子进程数量设置上限，以防止攻击者利用该服务在系统上创建大量进程导致系统变得不可用，从而诱发“远程炸弹”。我们可以通过计算当前正在执行的子进程数量来实施此限制（该数量在成功 `fork()` 之后增加，在每个子进程被 SIGCHLD 处理器收回时减少）。如果达到了子进程数量的限制，我们可以暂时停止连接（或者，接受连接后立即关闭它们）。
