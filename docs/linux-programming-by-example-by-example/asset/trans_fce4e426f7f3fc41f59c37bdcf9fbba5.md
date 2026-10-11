

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

# TCP/IP 编程

TCP/IP 是运行互联网（世界上最大的互连机器网络）的协议（实际上是协议族）。当前版本的协议是版本 4（IPv4），但向版本 6（IPv6）的过渡已经开始。当前 IPv6 提案中现有的规范已整合到 2.2.x 内核中。不过，由于新协议尚未广泛使用，本节介绍的是 IPv4。正如本章开头所述，网络编程是一个很大的话题，有很多整本书都在论述它。但是，你实际上可以使用不到 10 个函数调用来编写具备网络功能的程序。

# 网络数字

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

# 网络地址

与 UNIX 域套接字一样，TCP/IP 网络地址存储在 `sockaddr` 结构体 `struct sockaddr_in` 中，它定义在 `<netinet/in.h>` 中，如下所示：

```c
struct sockaddr_in {
    short int sin_family;      /* AF_INET */
    uint16_t sin_port;        /* Port number */
    struct in_addr sin_addr;  /* IP address */
};
```

你还需要包含 `<sys/socket.h>` 以获取完整的套接字定义。对于 TCP/IP（至少是版本 4），`sin_family` 必须是 `AF_INET`。`sin_port` 是要连接的端口号，`sin_addr` 是 IP 地址。`sin_port` 和 `sin_addr` 都必须是网络字节序。然而，`sin_addr` 是一个二进制结构，因此要将其转换为标准的点分十进制形式，请使用 `inet_ntoa` 函数；反之，要将点分十进制地址转换为 `sin_addr` 的二进制格式，请使用 `inet_aton`。这些调用在 `<arpa/inet.h>` 中的原型如下：

```c
char *inet_ntoa(struct in_addr addr);
int inet_aton(const char *daddr, struct in_addr *ipaddr);
```

`inet_ntoa` 将存储在 `addr` 中的二进制 IP 地址转换并返回为字符串（返回的字符串是一个静态分配的缓冲区，会被后续调用 `inet_ntoa` 覆盖）。`inet_aton` 将存储在 `daddr` 中的点分十进制地址转换为正确的二进制格式，然后存储在 `ipaddr` 中。如果地址是有效地址，`inet_aton` 返回非零，否则返回零。

> **注意**
>
> 几个 TCP/IP API 函数在失败时返回零，在成功时返回非零。这种行为与你之前看到的几乎所有库和系统调用的行为完全相反。

> **提示**
>
> 你偶尔会遇到一个名为 `inet_addr` 的函数。它执行与 `inet_aton` 相同的功能。它的原型是 `unsigned long int inet_addr(const char *daddr)`。它是一个过时的调用，因为它不识别 `255.255.255.255` 为有效的 IP 地址。如果你遇到使用此函数的代码，请做件好事，将其更改为使用 `inet_aton`。

TCP/IP 网络地址是 32 位数字，通常表示为 *点分十进制* 形式，例如 www.xxx.yyy.zzz。由于它们是 32 位数字，潜在的唯一网络地址有 4,294,967,295 个（从 0 开始计数）。然而，由于每个唯一地址可能需要或需要同时运行多个 TCP/IP 应用程序，因此每个地址还有多达 65,535 个用于连接的端口。

*端口* 是 16 位数字，代表特定系统上的连接或端点（端口 0-1024 保留给以 root 权限运行的进程使用）。因此，一个系统上的唯一连接点由主机的 IP 地址和端口号的组合定义。两个系统之间完整且唯一的网络连接由两个这样的连接点定义。图 18.5 直观地说明了这一点。

![](img/be588b36b489136ce784030a08a1d3d4_430_0.png)

如图所示，HOST1 和 HOST2 之间有四个完整连接：HOST1:PORT1 到 HOST2:PORT2，HOST1:PORT2 到 HOST2:PORT3，HOST2:PORT1 到 HOST1:PORT3，以及 HOST2:PORT4 到 HOST1:PORT4。

在查看示例程序之前，你必须了解最后一个函数 *setsockopt*。关闭套接字后，其地址（IP 和端口号的组合）在一段时间内不可用。若要重用此地址，必须设置套接字的选项以允许重用。它在 `sys/socket.h` 中声明如下：

```c
int setsockopt(int sockfd, int level, int optname,
               const void *optval, socklen_t optlen);
```

*setsockopt* 将存储在 *optname* 中的选项设置为 *optval*，适用于在文件描述符 *sockfd* 上打开的套接字。对于套接字，*level* 必须是 *SOL_SOCKET*。

将 *optname* 设置为 *SO_REUSEADDR*，将 *optval* 设置为 *1*。也就是说，*setsockopt* 调用应类似于以下形式：

```c
int i = 1;
setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &i, sizeof(i));
```

# 示例

![](img/be588b36b489136ce784030a08a1d3d4_431_0.png)

# 示例

1.  下面的示例 *mynet* 创建一个 *TCP/IP* 套接字，然后等待并接受所有连接。它使用端口号 *50000*，该端口不太可能被其他程序使用。

```c
/*
 * mynet.c - Bind to and wait on a TCP/IP socket
 */
#include <sys/socket.h>
#include <netinet/in.h>

#include <arpa/inet.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(void)
{
    int sockfd;
    struct sockaddr_in srv; /* Server's socket structure */
    socklen_t socklen;
    int i = 1;               /* For setsockopt */

    /* Create the socket */
    if ((sockfd = socket(PF_INET, SOCK_STREAM, 0)) < 0)
        err_quit ("socket");

    /* Want to reuse the local address */
    setsockopt (sockfd, SOL_SOCKET, SO_REUSEADDR, &i, sizeof (i));

    /* Initialize and set up the server structure */
    memset (&srv, 0, sizeof (srv));
    srv.sin_family = AF_INET;
    srv.sin_port = htons (50000); /* Don't forget network byte order */
```

