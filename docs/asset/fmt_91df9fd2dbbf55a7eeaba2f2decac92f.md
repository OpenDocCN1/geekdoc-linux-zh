
要创建 UNIX 域套接字，必须将 `sun_family` 设置为 `AF_UNIX`。`sun_path` 包含用作套接字的文件名称。如你所预期的那样，使用 `bind` 调用将套接字绑定到该文件，但该文件是在调用 `bind` 时创建的。如果文件已存在，`bind` 将失败，将 `errno` 设置为 `EADDRINUSE`，并向调用进程返回 -1。同样定义在 `<sys/un.h>` 中的 `SUN_LEN` 宏返回 `sockaddr_un` 结构体的大小。

`sockconn` 程序展示了客户端程序连接到服务器套接字的正确方法，因此不再重复该示例。但是，请密切注意 `sockconn` 和 `mksock` 如何将其协议的 `sockaddr_un` 结构体强制转换为通用的 `socket_addr` 结构体，以便进行 API 接口的每次调用。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_424_0.png)

## 示例

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

### 读取和写入 UNIX 域套接字

如本章开头所述，可以使用标准系统 I/O 调用从套接字读取和写入数据。程序很简单。调用 `accept` 的进程使用 `accept` 返回的文件描述符进行 I/O。调用 `connect` 的进程（通常是客户端进程）使用 `socket` 调用返回的文件描述符进行 I/O。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_425_0.png)

## 示例

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

然后，将 `mksock.c` 中的第 40–45 行替换为以下代码：

```c
/* Accept the first connection that comes in */
if ((infd = accept(sockfd, (struct sockaddr *)&srv, &socklen)) >= 0)
      puts("new connection granted");

/* Read from the socket and write to stdout */
xfer_data(infd, fileno(stdout));
```

新代码不再简单地接受每一个传入的连接，而是仅接受第一个连接，然后调用 `xfer_data` 从套接字的文件描述符 `infd` 读取传入的数据，并将其写入 `stdout`。

最后，在 `sockconn.c` 的 `exit` 语句上方添加以下代码：

```c
/* Copy stdin to the socket file descriptor */
xfer_data(fileno(stdin), sockfd);
```

这段额外的代码从 `stdin` 读取输入，并将其写入绑定到套接字的文件描述符。修改后的文件可从本书的网站下载，文件名为 `rdsock.c` 和 `wrsock.c`。

要运行这些程序，请在另一个 xterm 或虚拟控制台窗口中启动 `wrsock`，先在其中一个窗口运行 `rdsock`。每次按下回车键时，输入的行文本会显示在 `rdsock` 的窗口中。这些程序的示例输出如图 18.4 所示。

![](img/be588b36b489136ce784030a08a1d3d4_426_0.png)

图 18.4：

读取和写入 UNIX 域套接字。

在图 18.4 中，读取端/服务器端 `rdsock` 在左侧的 xterm 窗口中运行，写入端/客户端 `wrsock` 在右侧的 xterm 窗口中运行。如图所示，在按下回车键后，输入到写入端中的每一行文本都会出现在读取端。

## TCP/IP 编程

TCP/IP 是运行互联网（世界上最大的互连机器网络）的协议（实际上是协议族）。当前版本的协议是版本 4（IPv4），但向版本 6（IPv6）的过渡已经开始。当前 IPv6 提案中现有的规范已整合到 2.2.x 内核中。不过，由于新协议尚未广泛使用，本节介绍的是 IPv4。正如本章开头所述，网络编程是一个很大的话题，有很多整本书都在论述它。但是，你实际上可以使用不到 10 个函数调用来编写具备网络功能的程序。

## 网络数字

在深入网络编程本身之前，重要的是要指出 TCP/IP 协议是大端（big-endian）的；也就是说，它将多字节数字的最高有效位存储在最低的内存地址中。许多计算机同样是大端。

然而，其他计算机，例如 Intel 的 x86 处理器，是小端（little-endian）的，这意味着多字节数字的最低有效位存储在最低的内存地址中（内存中值的排列的通用术语是字节序）。这意味着当向 TCP/IP 函数提供数值时，必须将它们从主机的字节序转换为网络的字节序。

幸运的是，协议实现提供了四个专门执行此功能的函数。它们在 `<netinet/in.h>` 中声明如下：

```c
unsigned long int htonl(unsigned long int hostlong);
unsigned short int htons(unsigned short int hostshort);
unsigned long int ntohl(unsigned long int netlong);
unsigned short int ntohs(unsigned short int netshort);
```

`htonl` 将长整型整数 `hostlong` 从主机系统的字节序转换为网络字节序。类似地，`htons` 将短整型整数 `hostshort` 从主机字节序转换为网络字节序。另外两个调用 `ntohl` 和 `ntohs` 是反向过程，因此将网络字节序转换为主机系统的字节序。

## 网络地址

与 UNIX 域套接字一样，TCP/IP 网络地址存储在 `sockaddr` 结构体 `struct sockaddr_in` 中，它定义在 `<netinet/in.h>` 中，如下所示：

```c
struct sockaddr_in {
    short int sin_family;      /* AF_INET */
    uint16_t sin_port;        /* Port number */
    struct in_addr sin_addr;  /* IP address */
};
```
