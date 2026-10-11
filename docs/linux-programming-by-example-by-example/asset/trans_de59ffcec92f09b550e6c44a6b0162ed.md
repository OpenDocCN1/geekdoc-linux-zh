

```c
if ((sockfd = socket(PF_UNIX, SOCK_STREAM, 0)) < 0)
    err_quit("socket");

/* Initialize and set up the server structure */
memset(&srv, 0, sizeof(srv));
srv.sun_family = AF_UNIX;
strncpy(srv.sun_path, argv[1], sizeof(srv.sun_path));

/* Bind the socket to an address */
if ((bind(sockfd, (struct sockaddr *) &srv, SUN_LEN(&srv))) < 0)
    err_quit("bind");

/* Wait for incoming connections */
if (listen(sockfd, 5) < 0)
    err_quit("listen");
printf("socket available: %s\n", srv.sun_path);

/* Loop forever, accepting all connections */
while (accept(sockfd, (struct sockaddr *) &srv, &socklen) >= 0)
    puts("new connection granted");

exit(EXIT_SUCCESS);
}
```

`mksock` 接受一个参数，即要创建的套接字地址。它首先调用 `socket` 创建一个面向流的（协议类型为 `SOCK_STREAM`）UNIX 域套接字（协议族为 `PF_UNIX`），并使用默认协议。在初始化 `srv` 结构体后，`mksock` 接着将套接字族设置为 `AF_UNIX`，并将套接字地址复制到 `sun_path` 成员中。然后，`bind` 调用将文件描述符 `sockfd` 与由 `srv` 描述的套接字关联起来。

请注意，`srv` 被声明为 `struct sockaddr_un`，这是 UNIX 域套接字的套接字结构体。为了消除编译器警告，将其强制转换为 `struct sockaddr *` 以匹配 `bind` 的原型。最后，`listen` 调用表示服务器正在该套接字上接受连接，而 `accept` 调用持续允许新的连接，直到 `accept` 返回错误或者程序被其他方式终止。

`helper.h` 及其实现文件 `helper.c` 是本章中所有程序使用的实用函数。它们*存在的目的*是缩短代码列表。`mksock` 和 `sockconn` 使用 `err_quit` 函数，该函数使用指定的消息调用 `perror`，然后退出。`err_quit` 定义如下：

```c
void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```

2. `sockconn` 连接到由 `mksock` 服务的套接字。

![](img/be588b36b489136ce784030a08a1d3d4_421_0.png)

### 示例

```c
/*
 * sockconn.c - Connect to a socket
 */
#include <sys/socket.h>
#include <sys/un.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(int argc, char *argv[])
{
    int sockfd;        /* File descriptor for socket */
    struct sockaddr_un cli; /* Client's socket structure */
    socklen_t socklen;      /* Size of sockaddr */

    /* Expect the socket name on the command-line */
    if (argc != 2) {
        puts("USAGE: sockconn <filename>");
        exit(EXIT_FAILURE);
    }

    /* Create a socket */
    if ((sockfd = socket(PF_UNIX, SOCK_STREAM, 0)) < 0)
        err_quit("socket");

    /* Set up the client */
    memset(&cli, 0, sizeof(cli));
    cli.sun_family = AF_UNIX;
    strncpy(cli.sun_path, argv[1], sizeof(cli.sun_path));

    /* Connect to the socket */
    socklen = SUN_LEN(&cli);
    if(connect(sockfd, (struct sockaddr *)&cli, socklen) < 0)
        err_quit("connect");
    printf("connected to socket %s\n", cli.sun_path);

    exit(EXIT_SUCCESS);
}
```

`sockconn` 的设置与 `mksock` 相同：创建一个套接字并设置套接字的一些值。实际上，也可以使用 `bind` 调用绑定本地地址，但这是可选的，因为客户端希望连接到远程服务器。通常，客户端会丢弃本地地址。`connect` 调用将客户端的文件描述符 `sockfd` 绑定到由服务器打开的套接字，该套接字作为 `sockconn` 的命令行参数传递。这两个程序的输出如图 18.3 所示。

#### 输出

![](img/be588b36b489136ce784030a08a1d3d4_422_0.png)

在图 18.3 中，左侧的 xterm 正在运行服务器程序 `mksock`，并监听名为 `lpe-sample` 的套接字。客户端程序 `sockconn` 在右侧三个较小的 xterm 中分别执行，它通过每次接受新连接时显示“new connection granted”来报告每个连接。同样，`sockconn` 通过显示套接字的地址（名称）来报告成功连接到服务器。

## UNIX 域套接字

UNIX 域套接字仅在单个机器上工作，因此它们更像命名管道而非网络协议。UNIX 域套接字绑定的地址是文件系统中的实际文件名。然而，套接字不能被打开；必须使用套接字接口进行访问。

## 创建 UNIX 域套接字

早些时候，你了解到 `socket_addr` 结构体包含网络地址。这在某种程度上是一种过度简化。实际上，那个 `socket_addr` 结构体是通用格式。所有协议族（域）都有自己特定协议的 `socket_addr` 版本。UNIX 域套接字的 `socket_addr` 结构体在 <sys/un.h> 中定义如下：

```c
struct sockaddr_un {
    unsigned short int sun_family;  /* AF_UNIX */
    char sun_path[108];     /* pathname */
};
```

要创建 UNIX 域套接字，必须将 `sun_family` 设置为 `AF_UNIX`。`sun_path` 包含用作套接字的文件名称。如你所预期的那样，使用 `bind` 调用将套接字绑定到该文件，但该文件是在调用 `bind` 时创建的。如果文件已存在，`bind` 将失败，将 `errno` 设置为 `EADDRINUSE`，并向调用进程返回 -1。同样定义在 <sys/un.h> 中的 `SUN_LEN` 宏返回 `sockaddr_un` 结构体的大小。

`sockconn` 程序展示了客户端程序连接到服务器套接字的正确方法，因此不再重复该示例。但是，请密切注意 `sockconn` 和 `mksock` 如何将其协议的 `sockaddr_un` 结构体强制转换为通用的 `socket_addr` 结构体，以便进行 API 接口的每次调用。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_424_0.png)

### 示例

本示例展示了尝试打开一个正在被使用的套接字时会发生什么。它假设你已经通过运行前两个示例程序创建了套接字文件 `lpe-sample`。

```bash
$ ls -l lpe-sample
srw-r-xr-x 1 kwall users 0 Aug 17 18:29 lpe-sample
$ ./mksock lpe-sample
bind: Address already in use
$ rm lpe-sample
$ ./mksock lpe-sample
socket available: lpe-sample
```

`bind` 调用失败，因为套接字已在被使用；但在删除套接字文件后，`bind` 调用成功，服务器开始了无限 `accept` 循环。

## 读取和写入 UNIX 域套接字

如本章开头所述，可以使用标准系统 I/O 调用从套接字读取和写入数据。程序很简单。调用 `accept` 的进程使用 `accept` 返回的文件描述符进行 I/O。调用 `connect` 的进程（通常是客户端进程）使用 `socket` 调用返回的文件描述符进行 I/O。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_425_0.png)

### 示例

本示例展示了读写 UNIX 域套接字的一种方法。简而言之，写入进程将其标准输入复制到套接字，而读取进程将从套接字读取的数据复制到其标准输出。`wrsock` 是写入进程，或客户端进程；`rdsock` 是读取进程，或服务器进程。为了保持代码相对简单且易于理解，`helper.c` 定义了一个函数 `xfer_data`，用于在两个文件描述符之间复制数据。它在本地头文件 `helper.h` 中声明。以下列表显示了 `xfer_data` 的定义：

```c
void xfer_data(int srcfd, int tgtd)
{
    char buf[1024];
    int cnt, len;

    /* Read from the input fd and write to the output fd */
    while ((cnt = read(srcfd, buf, sizeof(buf))) > 0) {
        if ((len = write(tgfd, buf, cnt)) != cnt)
            err_quit("helper.c:xfer_data:write");
    }
}
```

此函数从输入文件描述符 `srcfd` 读取任何输入，然后立即将其写入输出文件描述符 `tgtd`。如果 `read` 或 `write` 遇到错误，函数将退出。要使用此函数，请在源代码中添加行 `#include "helper.h"`。

以下两个代码片段展示了将服务器程序 `mkssock` 和客户端程序 `sockconn` 分别修改为读取器和写入器所需的修改。首先，在 `mkssock` 的顶部添加以下声明：

