
`Vary`: negotiate,accept-language,accept-charset

`TCN`:

`Last-Modified`: Fri, 04 May 2001 00:00:38 GMT

`ETag`: "83617-5b0-3af1f26:3bf57446"

`Accept-Ranges`: bytes

`Content-Length`: 1456

`Connection`: close

`Content-Type`: text/html

`Content-Language`: en

```html
<!DOCTYPE html //-//W3C//DTD XHTML 1.0 Transitional//EN//
//http://www.w3.org/TR/xhtml1/DTD/xhtml-transitional.dtd>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
</html
```

`telnet` 用于在计算机 `192.168.1.20` 的 `80` 端口上建立 TCP 连接。所有输入都通过网络连接转发到与该地址相关的进程（该进程通过 IP 地址和端口号唯一标识）。一旦收到请求，就会发送响应。所请求 HTML 页面的内容将随同包含文档信息和其他内容的头部输出。Web 浏览器使用相同的进程来对用户透明地访问数据。

由于网络功能的系统性分层，希望与其他计算机通信的应用程序只需关注少数细节。计算机之间的实际链路由较低层实现，而应用程序只需生成文本字符串——无论这两台计算机是并排坐在同一个房间里，还是位于不同的大陆。

网络的层级结构体现在内核中，各个级别通过代码段实现，这些代码段通过清晰定义的接口相互通信，以交换数据或转发命令。

## 12.3 通过 Sockets 通信

从程序员的角度来看，外部设备仅仅是 Linux（以及 UNIX）下的普通文件，正如第 8 章所述，通过普通的读写操作对其进行访问。这简化了对资源的访问，因为只需要单一通用的接口。

网卡的情况要复杂一些，因为上述方案要么完全被采用，要么执行起来非常困难。网卡的工作方式与普通的块设备和字符设备完全不同，Unix “一切皆文件”的格言不再完全适用。原因之一是（在所有层中使用了许多通信协议，其中需要指定选项来建立连接——这在打开设备文件时是无法实现的。因此，`/dev` 目录下没有网卡的条目。

当然，内核提供了一个尽可能允许访问所有网络函数的接口。这个问题并不是 Linux 特有的，许多 Unix 程序员在 20 世纪 80 年就遇到过这个问题。他们采用的解决方案——特殊的套接字（sockets）作为网络实现的接口已成为行业标准。Sockets 在 POSIX 标准中定义，并在 Linux 中也实现。

Sockets 用于定义和建立网络连接，以便可以使用节点（inode）的普通手段（特别是读写操作）进行访问。在程序员看来，socket 连接的最终结果是一个文件描述符，它不仅提供了标准函数的范围，还提供了增强的功能。用于实际数据交换的接口对于所有协议和地址族都是相同的。

当创建一个 socket 时，不仅区分了地址函数和协议函数，还区分了基于流（stream）和基于数据报（datagram）的通信。对于面向连接的 socket 来说，重要的是为客户端或服务器生成一个 socket。

为了从用户的角度说明 socket 的功能，我包含了一个短示例程序，演示了几个网络编程选项。详细描述在专门的出版物中提供，例如 [Ste00]。

### 12.3.1 创建一个 Socket

Sockets 不仅可以用于具有不同传输协议的 IP 连接，还可以用于内核支持的所有其他地址和协议类型（例如 IPX、Appletalk、本地 Unix sockets、DECNet 以及 `<socket.h>` 中列出的许多类型）。因此，在生成 socket 时指定所需的连接至关重要。尽管作为过去的遗留，可以从地址和协议族中选择任何伙伴组合，但通常每个地址族只支持一种协议，并且只能区分流导向和数据导向的

> ³ 有几种 Unix 变体通过文件设备 `/dev/tcp` 来实现网络连接；从应用程序和内核的角度来看，这远不是（标准的做法）。

## 第 12 章：网络

如第 1 章所示，CPU 采用两种约定来存储数值——小端（little endian）和大端（big endian）。定义了一种端点网络字节序，遵循大端格式，以确保具有不同字节排列方式的网络能够相互通信。因此，协议头中的数值必须以这种格式指定。由于 IP 地址和端口号都只由数字组成，这一事实在定义 `sockaddr_in` 结构体的值时必须考虑在内。良好的网络应用程序在大端机器上开发时会使用这些函数，以确保它们可以移植到不同的机器上。

为了表示小端和大端类型，内核提供了几种数据类型。`__be16`、`__be32` 和 `__be64` 表示 16 位、32 位和 64 位的大端数，而带有 `__le` 的变体是

## 第 12 章：网络

小端值的类比类型。它们都定义在 `<types.h>` 中。请注意，小端和大端端值最终都会解析为相同的数据类型（即第 1 章中引入的 `u32` 等），但显式指定字节顺序允许对自动化类型检查工具的正确性进行检查。

## 13.2.2 使用套接字 (Sockets)

假设你熟悉网络编程的用户态。然而，为了简要说明套接字如何表示内核网络层的接口，我将讨论两个非常简短的示例程序：一个作为回显请求的客户端，另一个作为服务器。客户端发送一段文本并保持不变。使用 TCP/IP 协议。

### 回显客户端 (Echo Client)

回显客户端的源代码如下：

```c
#include <stdio.h>
#include <netinet/in.h>
#include <sys/types.h>
#include <string.h>
int main() {
    /* Host and port of the echo server */
    char *echo_host = "192.168.1.20";
    int echo_port = 7;
    int sockfd;
    struct sockaddr *server = 
        (struct sockaddr*)malloc(sizeof(struct sockaddr_in));
    /* Set address of family to be connected /
       server->sin_family = AF_INET;
       server->sin_port = htons(echo_port); // Note network byte order!
       ((struct sockaddr_in*)server)->sin_addr.s_addr = inet_addr(echo_host);
    /* Create a socket (Internet family, stream socket and
       default protocol) */
    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    /* Connect to server / */
    printf("Connecting to %s \n", echo_host);
    printf("Numeric: %u\n", server->sin_addr);
    connect(sockfd, (struct sockaddr*)server, sizeof(server));
    /* Send message / */
    char *msg = "Hello World";
    printf("'%s\n", msg);
    write(sockfd, msg, strlen(msg));
    /* . . . and receive result / */
    char *buf = (char*)malloc(1000); // Receive buffer for max. 1000 chars
    int bytes = read(sockfd, (void*)buf, 1000);
}
```

> 为了简化起见，省略了真实且健壮的实现中会被证明的所有错误。

```c
printf("\nbytes received: %u\n", bytes);
printf("Text: %s\n", buf);
```

```c
/* End communication (i.e. close socket) */
close(sockfd);
```

互联网守护进程（inetd, xinetd 或类似程序）通常使用内置的回显服务器。因此，源代码可以在编译后立即进行测试。

```bash
wolfgang@meitner>../echo_client
Connect to 192.168.1.20
Numeric: 335653056
```

```bash
```
