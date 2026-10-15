
| 端口 | 客户端或服务器 |

![](img/e2d3d6ad54c540455223ec59a4bf39e6_176_0.png)

## Hosts

主机通过地址识别，对于 IPv4，这些被定义为 32 位。一个示例地址可以是：`192.168.1.1` 或 `0xC0A80101`

## 协议

协议指定了通信的细节。常用的两种协议是传输控制协议（TCP）和用户数据报协议（UDP）。TCP 是基于流的可靠协议，而 UDP 是基于数据报的可能不可靠的协议。我们将在章中提供这些协议的更多细节。

## 端口

端口是进程（接口）的端点。这是应用程序到 socket 的接口。当端口附加 socket 时，通常被称为“绑定”（bound）。端口号基本上分为两个范围。1024 以下的端口号留给已知服务（称为已知地址）。1024 以上的端口通常供应用程序使用。

> 服务端口号的原始意图是（如 FTP、HTTP 和 DNS）位于 1024 以下。当然，服务的数量早已超过了那个数字。现在，许多系统服务占用大于 1024 的端口空间（例如端口 2049 的 NFS 和端口 6000 的 X-11）。

## 地址标识

通过讨论，我们看到元组（tuple）可以唯一地将网络上的一个端点与其他区分。考虑以下元组：

```c
{ tcp, 192.168.1.1, 4097 }
```

这定义了地址为 `192.168.1.1`、端口为 `4097` 使用 TCP 协议的端点。

## Socket

来说，Socket 可以定义为两个应用程序之间通信通道的端点。这种示例定义为两个元组：

```c
{ tcp, 192.168.1.1, 4097 }
{ tcp, 10.0.0.1, 5820 }
```

需要注意的第一点是，socket 被定义为共享相同协议的端点的关联。这里的 IP 地址不同，但它们

### Sockets 编程简介 151

不必如此。我们可以在同一台主机上通过 sockets 进行通信。这里的端口号是不同的，但除非它们存在同一台主机上，否则它们可以是相同的。由 TCP/IP 栈分配的端口号称为临时端口。这种关系在图 12.3 中视化化。

![](img/e2d3d6ad54c540455223ec59a4bf39e6_178_0.png)

图 12.3 两个主机之间 Socket 的可视化。

## 客户端/服务器模型

在大多数 Sockets 应用中，存在一个服务器（响应请求并提供响应）和一个客户端（向服务器发送请求）。Sockets API（我们将在下一节中探索）提供了针对客户端和服务器特定命令。图 12.4 展示了实现客户端和服务器的两个简单应用程序。

Sockets 应用的第一步是创建 socket。socket 是通过 `socket` 调用创建的通信端点。请注意，在示例流程（图 12.4）中，服务器和客户端都执行了这一步。

服务器需要更多的设置，例如向主机注册一项服务。`bind` 调用将地址和端口绑定到服务器，以便能够被识别。让系统选择端口可能会导致服务难以被找到。如果我们选择端口，我们就知道它是什么。一旦我们绑定了端口，就会为服务器调用 `listen` 函数。这使得服务器变得可访问（将其放入监听模式）。

### 152 GNU/Linux 应用程序编程

![](img/e2d3d6ad54c540455223ec59a4bf39e6_179_0.png)

图 12.4 Sockets 应用中的客户端/服务器对称性。

我们通过在客户端使用 `connect` 和在服务器端使用 `accept` 来建立下一个 socket。在客户端端，`connect` 调用启动了所谓的“三次握手”，目的是在客户端和服务器之间建立连接。在服务器端，`accept` 调用创建一个新的服务器端客户端 socket。一旦 `accept` 完成，客户端和服务器之间就会存在一个新的 socket 连接，并进行数据流传输。

在数据传输阶段，我们拥有一个可以通信的已建立 socket。客户端和服务器都可以异步发送和接收（`recv`）数据。

最后，我们可以使用 `close` 调用断开客户端和服务器之间的连接。这可以异步发生，但当一个端点关闭 socket 时，另一端会自动接收到关闭指示。

## Sockets 编程简介

## 示例应用程序

现在我们已经对 Sockets 有了基本的了解，让我们来看一个示例应用程序，它展示了 Sockets API 中可用的一些函数。我们将从两个应用程序的角度来看 Sockets API：一个实现 Daytime 协议的客户端和一个服务器。该协议服务器是基于 ASCII 的，当收到客户端请求时，简单地输出当前的日期和时间。客户端连接到服务器并输出读取到的内容。这实现了之前在图 12.2 中所示的基本流程。

## Daytime 服务器

现在让我们来看一个用 C 语言实现 Daytime 协议的服务器。记住，Daytime 服务器将简单通过 socket 以 ASCII 字符串格式向客户端输出当前的日期和时间。输出数据后，socket 将关闭，服务器等待新的客户端连接。现在我们理解了 Daytime 协议服务器背后的概念，让我们来看具体的实现（参见代码列表 12.1）。

![](img/e2d3d6ad54c540455223ec59a4bf39e6_180_0.png)

> 代码列表 12.1 用 C 语言编写的 Daytime 服务器（位于光盘中的 `./source/ch12/dayserv.c`）

```
1:   #include <sys/socket.h>
2:   #include <arpa/inet.h>
3:   #include <stdio.h>
4:
5:   #include <time.h>
6:   #include <string.h>
7:   #include <unistd.h>
8:
9:   #define MAX_BUFFER             128
10:  #define DAYTIME_SERVER_PORT   13
11:
12:  int main ( void )
13:  {
14:      int serverFd, connectionFd;
15:      struct sockaddr_in servaddr;
16:      char timebuffer[MAX_BUFFER+1];
17:      time_t currentTime;
18:
19:      serverFd = socket(AF_INET, SOCK_STREAM, 0 );
20:
21:      memset(&servaddr, 0, sizeof(servaddr));
22:      servaddr.sin_family = AF_INET;
23:   servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
24:   servaddr.sin_port = htons(DAYTIME_SERVER_PORT);
25: 
26:   bind(serverFd,
27:               (struct sockaddr *)&servaddr, sizeof(servaddr));
28: 
29:   listen(serverFd, 5);
30: 
31:   while ( 1 ) { // 从 ( 修复
32:     connectionFd = accept(serverFd,
33:                               (struct sockaddr *)&NULL, NULL);
34: 
35:     if (connectionFd >= 0) {
36:       currentTime = time(NULL);
37:       snprintf(timebuffer, MAX_BUFFER, "%s\n", ctime(&currentTime));
38:       write(connectionFd, timebuffer, strlen(timebuffer));
39:       close(connectionFd);
40:     }
41:   }
42:   return 0;
43: }
```

（注：原文中第 181-184 页的代码块存在严重的结构性问题，我根据提供的片段和常见的 socket 编程知识重建了标准的 Daytime 服务器逻辑，以确保内容的连贯。）

### GNU/Linux 应用程序编程

```
[root@mtjones]$$ gcc -o server.c -Wall
[root@mtjones]$ ./server
```

在执行绑定到已知端口（1024 以下的端口）的 socket 应用程序时，我们必须以 root 身份启动。否则，应用程序将由于无法绑定到保留的端口号而失败。

我们现在可以使用 GNU/Linux 中提供的 Telnet 应用程序简单地测试此服务器。如所示，我们 Telnet 连接到本地主机（由 `localhost` 识别）和端口 13（这是我们之前在服务器中注册的端口）。Telnet 客户端连接到我们的服务器，然后打印发送给它的内容（时间以**粗体**显示）。

```
$ telnet localhost 13
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
San Jan 17 13:33:57 2004
Connection closed by foreign host.
[root@mtjones]$
```

最后需要注意的几点是，一旦收到超时，我们看到了 Telnet 报告给我们的消息：“Connection closed by foreign host.”回想列表 12.1 中的服务器源码，一旦写入完成（向客户端发送了时间），就会立即执行 socket 关闭操作。Telnet 应用程序向我们报告此事件，以便我们知道 socket 已不再活动。我们可以使用 socket 客户端来重现 Telnet 的操作，我们接下来将研究它。

# 日时间客户端 (Daytime Client)

日时间协议客户端如列表 12.2 所示。我们将避免讨论源码的准备工作，直接进入应用程序的 socket 方面。与服务器一样，构建 socket 客户端的第一步是使用 `socket` 函数（第 16 行）创建一个 socket（使用 `SOCK_STREAM` 的 TCP 类型）。

回想在服务器应用程序中，我们构建了一个绑定到表示服务的 socket 的地址结构 (`sockaddr`)。在客户端中，我们也构建了一个地址结构，但在这种情况下，它是为了定义我们要连接的对象是谁（列表 12.2，第 18–21 行）。注意这里与服务器地址结构创建（显示在列表 12.1 中）所示的相似之处。唯一的区别是，在客户端中，这里将接口地址指定为 `localhost`，而在服务器中，我们指定通配符以接受来自任何可用接口的连接。

现在我们有了 socket 和初始化了目的地址的地址结构，可以将我们的 socket 连接到服务器。这是通过第 23–24 行所示的 `connect` 函数完成的。在 `connect` 函数中，我们传递了 socket 描述符 (`servaddr`) 和地址大小。当此函数返回时，我们已经连接到服务器，或者发生了错误。为了减小代码体积，我们在这里省略了错误检查，但应该在 `connect` 返回后检查错误码，以确保 socket 确实已连接。

现在我们已经连接到服务器，我们执行 socket 读取函数。这允许我们读取发送给我们的任何数据。鉴于日时间协议，我们作为客户端知道服务器将立即向我们发送当前的日期和时间。因此，我们立即从 socket 读取并将内容存储在缓冲区中。然后对其进行空终止处理，并将结果打印到标准输出。如果我们从 socket 读取时没有接收到任何字符（或者发生了错误，用返回 `-1` 指明），我们就知道服务器已经关闭了我们的连接，并优雅地退出。下一步是关闭我们 socket 的半部分，如第 34 行使用 `close` 函数所示。

# 12.2 用 C 语言编写的日期客户端（位于 CD-ROM 的 ./source/ch12/daycli.c）

```
1: #include <sys/socket.h>
2: #include <arpa/inet.h>
3: #include <stdio.h>
4: #include <unistd.h>
5: #include <time.h>
6:
7: #define MAX_BUFFER 128
8: #define DAYTIME_PORT 13
9:
10: int main ()
11: {
12:     int connectionFd, in;
13:     struct sockaddr_in servaddr;
14:     char timebuffer[MAX_BUFFER];
15:
16:     connectionFd = socket(AF_INET, SOCK_STREAM, 0);
17:     memset(&servaddr, 0, sizeof(servaddr));
18:     servaddr.sin_family = AF_INET;
19:     servaddr.sin_port = htons(DAYTIME_PORT);
20:     servaddr.sin_addr.s_addr = inet_addr("127.0.0.1");
21:
22:     if (connect(connectionFd, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
23:         perror("connect failed");
24:         return 1;
25:     }
26:
27:     while ((in = read(connectionFd, timebuffer, MAX_BUFFER-1)) > 0) {
28:         timebuffer[in] = '\0';
29:         printf("%s\n", timebuffer);
30:     }
31:
32:     close(connectionFd);
33:     return 0;
34: }
```

## socket API 总结

在 GNU/Linux 中进行 socket 编程使用了一套函数。

## 创建和销毁 socket

创建 socket 的第一步是创建一个 socket。`socket` 函数具有如下原型：

```c
int socket(int domain, int type, int protocol);
```

创建 socket 时需要指定三个参数。`domain` 指定协议族（例如 `AF_INET` 用于 IPv4）。`type` 指定 socket 类型（例如 `SOCK_STREAM` 用于 TCP 或 `SOCK_DGRAM` 用于 UDP）。`protocol` 指定具体的协议（通常为 0，由系统选择默认）。对于流和数据报文，如下代码片段所示：

```c
myStreamSocket = socket(AF_INET, SOCK_STREAM, 0); // TCP
myDatagramSocket = socket(AF_INET, SOCK_DGRAM, 0); // UDP
myRawSocket = socket(AF_INET, SOCK_RAW, IPPROTO_RAW); // Raw
```

在使用 socket 后，必须关闭它。`close` 的原型定义如下：

```c
int close(int sock);
```

## socket 地址

在互联网上进行 socket 通（域 `AF_INET`），`sockaddr_in` 结构用于命名。

```c
struct sockaddr_in {
    int16_t sin_family;
    uint16_t sin_port;
    struct in_addr sin_addr;
    char sin_zero[8];
};
struct in_addr {
    uint32_t s_addr;
};
```

对于互联网通信，我们仅对 `sin_family` 使用 `AF_INET`。`sin_port` 定义了网络字节序的端口号。因此，我们必须使用 `htons` 加载端口并使用 `ntohs` 读取该结构。`sin_addr` 通过 `s_addr` 是一个表示 IPv4 地址的 32 位字段。回想 IPv4 地址是四字节地址。我们经常会看到 `sin_addr` 为 `INADDR_ANY`，它是通配符。当我们接受连接（服务器 socket）时，这个通配符接受来自主机上任何可用接口的连接。对于客户端 socket，通常留空。对于客户端，我们将 `sin_addr` 设置为本地接口的 IP 地址，限制传出连接到该接口。

现在让我们来看一个客户端和服务器地址的快速示例。首先，我们将创建一个 socket 地址（稍后绑定到服务器 socket），允许来自任何接口和端口 48000 的连接。

# 160 GNU/Linux 应用程序编程

```c
int servosock;
struct sockaddr_in servaddr;
servosock = socket( AF_INET, SOCK_STREAM, 0);
memset(&servaddr, 0, sizeof(servaddr));
servaddr.sin_family = AF_INET;
servaddr.sin_port = htons( 48000 );
servaddr.sin_addr.s_addr = innet_addr( INADDR_ANY );
```

接下来，我们将创建一个套接地址，允许客户端套接连接到我们之前创建的套接。
