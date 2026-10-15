
```
while (nleftread > 0) {
    while (nconn < maxconn && nleftconn > 0) {
        /* find a file to read */
        for (i = 0; i < nfiles; i++) {
            if (file[i].f_flags == 0)
                break;
            if (i == nfiles) {
                err_quit("%neftconn = %d but not found", nleftconn);
                start_connect(&file[i]);
                nconn++;
                nleftconn--;
            }
        }
    }
rs = rset;
ws = wset;
n = Select(maxfd + 1, &rs, &ws, NULL, NULL);
for (i = 0; i < nfiles; i++) {
    flags = file[i].f_flags;
    if (flags == 0 || flags & F_DONE)
        continue;
    fd = file[i].f_fd;
    if (fd & F_CONNECTING) {
        if (FD_ISSET(fd, &rs) | FD_ISSET(fd, &ws)) {
            n = strerror(error);
            if (getockopt(fd, SOL_SOCKET, SO_ERROR, &error, &n) < 0)
                err_ret("nonblocking connect failed for %s", file[i].f_name);
        } else if (error == 0) {
            /* connection established */
            printf("connection established for %s\n", file[i].f_name);
            FD_CLR(fd, &wset); /* no more writability test */
            write_get_cmd(&file[i]);
        }
    } else if (n > Read(fd, buf, sizeof(buf)) == 0) {
        printf("end-of-file on %s\n", file[i].f_name);
        Close(fd);
        file[i].f_flags = F_DONE; /* CLEAR READING */
        FD_CLR(fd, &rset);
        nleftread--;
        nconn--;
    } else {
        printf("read %d bytes from %s\n", n, file[i].f_name);
    }
}
}
```

## 第 15.6 节

### 非阻塞

```c
#include "unp.h"

int
main(int argc, char **argv) {

    int sockfd;
    struct linger link;
    struct sockaddr_in servaddr;

    if (argc != 2)
        return err_exit(EXIT_USAGE, "usage: tcpcli <IPaddress>");

    sockfd = socket(AF_INET, SOCK_STREAM, 0);

    bzero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(SERV_PORT);
    inet_pton(AF_INET, argv[1], &servaddr.sin_addr);

    connect(sockfd, (struct sockaddr *)&servaddr);

    link.l_onoff = 1; // close()时发送 RST
    link.l_linger = 0;
    setsockopt(sockfd, SOCK_SOCKET, SO_LINGER, &link, sizeof(link));

    close(sockfd);

    exit(0);
}
```

图 15.21 创建连接并发送 RST 的 TCP 客户端。

到服务器，其他实现应该返回 `EICNABORTED`，但通常返回 `EAGAIN`。考虑一种源自伯克利的实现方式。

- *在图 15.21 中，客户端建立了连接并将其中止。*
- `select` 向服务器进程返回可读，但服务器需要很短的时间来调用 `accept`。
- 在服务器从 `select` 返回到调用 `accept` 之间，收到了来自客户端的 RST。
- 已完成的连接从队列中移除，我们假设不存在其他已完成的连接。
- 服务器调用 `accept`，但由于没有已完成的连接，它会阻塞。

服务器将一直阻塞在 `accept` 调用中，直到有其他客户端建立连接。但在此期间，假设服务器如图 15.22 所示，服务器阻塞在 `accept` 调用中，不会处理任何其他读器描述符。

这个问题与第 6.8 节描述的拒绝服务攻击有些相似之处，但有了这个 bug，一旦有另一个客户端建立连接，服务器就会从阻塞的 `accept` 中跳脱出来。

## 解决此问题是

1. 如果我们使用 `select` 来告诉我们何时连接准备好被接受，则始终将监听套字设置为非阻塞，并且
2. 在随后的 `accept` 调用中忽略以下错误：`EWOULDBLOCK`（对于伯克利实现，当客户端中止连接）、`ECONNABORTED`（对于 Posix 实现，当客户端中止连接）、`EOPROTO`（对于 SVR4 实现，当客户端中止连接）以及 `EINTR`（如果在捕获信号）。

## 15.7 总结

我们在第 15.2 节中关于非阻塞读写的示例修改了 `str_cli` 客户端，使其在与服务器的 TCP 连接上使用非阻塞 I/O。`select` 通常与非阻塞 I/O 一起使用，以确定描述符何时可读或可写。这个版本的客户端是我们展示的最版本，尽管代码修改并不简单。我们随后展示了使用 `fork` 将客户端分为两个部分更为简单，我们在图 23.3 中使用线程也采用了相同的技术。

非阻塞连接允许我们在 TCP 三次握手进行期间执行其他处理，而不是阻塞在 `connect` 调用中。遗憾的是，这些也是非阻塞的，不同的实现有不同的方法来指示连接是否正常完成或遇到错误。我们使用非阻塞连接开发了一个新的客户端（类似于 Web 客户端），它同时打开多个 TCP 连接，以减少从服务器获取大量文件所需的时钟时间。这样启动多个连接可以减少时钟时间，对于 TCP 的拥塞避免来说也是“网络友好的”。

### 习题

- 15.1 在对图 15.10 的讨论中，我们提到父进程必须调用 `shut-down` 而 `close`。为什么？
- 15.2 在 15.10 中，如果服务器进程终止，子进程接收到文件结束并终止，但子进程没有通知父进程会发生什么？
- 15.3 在 15.10 中，如果父进程在子进程之前意外死亡，子进程在套接字上读取文件结束会发生什么？
- 15.4 在 15.11 中，如果我们移除以下两行

```c
if (n == 0)
    goto done;  /* 连接立即完成 */
```

会发生什么？
- 15.5 在第 15.3 节中，我们说数据可能在返回之前到达套接字。这是如何发生的？

## 16

## ioctl 操作

### 16.1 引言

`ioctl` 函数传统上一直是系统 `posit` 接口，用于所有不符合其他良好定义类别的事务。Posix 正在通过创建特定的封装函数来替换功能正被 Posix 标准化的 `ioctl`，从而消除 `ioctl`。例如，Unix 终端接口传统上是通过 `ioctl` 访问的。我们为终端创建了 12 个新函数：`tcgetattr` 获取终端属性，`tcflush` 刷新输入和输出等。类似地，Posix 正在用新函数替换 `ioctl`（第 21.3 节），替换 `SIOCATMARK` `ioctl`。尽管如此，仍有许多 `ioctl` 用于与网络编程相关的取决于实现的特性：例如，获取接口信息，访问路由表和 ARP 缓存。

本章提供了网络编程中 `ioctl` 的概述，但其中许多项取决于实现。`ioctl` 的一种用法是获取接口信息，以及访问路由表和 ARP 缓存等。我们还确定了接口是否支持广播或多播。我们在第 17 节详细介绍更多此类请求。

### 16.2 ioctl 函数
