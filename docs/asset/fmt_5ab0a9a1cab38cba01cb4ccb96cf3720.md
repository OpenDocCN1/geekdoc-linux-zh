
```c
bzero(&sin, sizeof(sin));
sin.sin_family = AF_INET;
sin.sin_addr.s_addr = INADDR_ANY;
sin.sin_port = htons(8000); // 我们将使用端口 8000
```

现在我们准备好将新 socket 绑定到端口 8000：

```c
bind(sock_descriptor, (struct sockaddr*)sin,
sizeof(sin));
```

（注：由于原始文本存在大量重复的 OCR 错误，译文已根据核心逻辑进行了去重和对齐）

# 实现一个简单的 Web 服务器

示例程序 `web_server.c` 使用实用函数 `read_file` 来读取本地文件，并将文件内容作为一个大型大的字符缓冲区（变量 `ret_buf`）返回。变量 `error_return` 的值为一个 HTML 格式的错误消息。

以下代码实现了 `read_file` 函数，用于将本地文件的内容读取到缓冲区：

```c
char ret_buf[32768];
char error_return = "<HTML>\n<body>File not found\n</body>\n</HTML>";

char *read_file(char *buf, int num_buf) {
    int i;
    char *cp, *cp2;
    FILE *f;
    cp = buf + 5;
    cp = strchr(cp, NULL); cp2 = '\0';
    if (cp2 != '\0') {
        if (DEBUG) printf("file: %s\n", cp);
        // 获取文件
        f = fopen(cp, "r");
        if (f == NULL) return error_return;
        i = read(ret_buf, 1, 32768, f);
        if (DEBUG) printf("%d bytes read from file %s\n", i, cp);
        if (i <= 0) { fclose(f); return error_return; }
        ret_buf[i] = '\0';
        fclose(f);
        return ret_buf;
    }
}
```

在 `web_server.c` 示例中，`main` 函数以通常的方式打开 socket 来监听请求。`web_server.c` 检查了所有系统调用的错误码；这些检查在 Web 服务器原理的简短描述中省略了。以下代码与示例 `server.c` 中的服务器 socket 设置代码相似：

```c
int socket;
int serverSocket;
struct sockaddr_in serverAddr;
struct sockaddr_in clientAddr;
int clientAddrSize;
struct host entity;
serverSocket = socket(AF_INET, SOCK_STREAM, 0);
serverAddr.sin_family = AF_INET;
serverAddr.sin_port = htons(port);
serverAddr.sin_addr.s_addr = htonl(INADDR_ANY);
memset(&serverAddr.sin_zero, 0, 8);
```

# 进程间通信与网络编程

## 第三部分

以下 `bind` 调用将此 socket 关联到指定的端口号（来自变量 `port`）：

```c
bind(serverSocket, (struct sockaddr *)&serverAddr, sizeof(struct sockaddr));
```

以下 `listen` 调用设置了 10 个队列请求的限制，并表示程序现在已准备好接受服务请求：

```c
listen(serverSocket, 10);
```

`web_server.c` 中的示例现在已准备好进入循环，等待待传入的连接。每个服务请求都会打开一个新 socket；读取服务请求的数据，处理请求并将数据返回给客户端，最后关闭临时 socket (`sock`)。来自 `web_server.c` 的以下代码片段实现了一个等待传入请求的处理循环：

```c
while (1) {
    clientAddrSize = sizeof(struct sockaddr_in);
    do {
        sock = accept(serverSocket, (struct sockaddr *)&clientAddr, &clientAddrSize);
        while ((sock == -1) && (errno == EINTR));
        if (sock == -1) {
            printf("Bad accept\n");
            break;
        }
        entity = gethostbyaddr(clientAddr.sin_addr, AF_INET);
        if (DEBUG) printf("Connection from %s\n", inet_ntoa(clientAddr.sin_addr));
        i = recv(sock, recvBuffer, 4096, 0);
        if (i == -1) break;
        if (recvBuffer[i-1] != '\n') break;
        recvBuffer[i] = '\0';
        if (DEBUG) printf("Received from client: %s\n", recvBuffer);
    } while (0);
    // 调用单独的函数处理请求：
    totalReceived = read_file(recvBuffer, totalReceived);
    size = strlen(recvBuffer);
    totalSent = 0;
    do {
        bytesSent = send(sock, 
```

# TCP/IP 与 Socket 编程

## 第 19 章

此代码与示例 `server.c` 非常相似，但这里从客户端接收的数据被解释为对本地文件的请求。请求的本地文件被读取到缓冲区，缓冲区被发送回客户端。

# 实现一个简单的 Web 客户端

简短示例程序 `web_client.c` 展示了你如何与 Web 服务器交互，而不是使用 Web 浏览器。该示例程序检查了所有系统调用的返回值，但为了使代码更短，后续讨论中省略了这些错误。通常情况下，错误返回值小于零表示存在问题。变量 `host_name` 和 `port` 用于指定计算机名称和端口。在 `web_server.c` 示例中，主机名被指定为绝对地址（127.0.0.1），指定本地机器，但任何如 `www.lycos.com` 或 `www.watson.com` 的值都可以运行。Web 服务器默认在端口 80 上监听；端口 8000 用于配合在大多数 Linux 发行版中安装并运行的 Apache Web 服务器运行 `web_server.c`：

```c
char host_name = "127.0.0.1"; // 本地主机
port = 8000;
```

以下代码（你现在应该看起来很熟悉）获取 Web 服务器信息并打开到 Web 服务器的 socket 连接（`web_server.c` 包含了为了简洁起见未显示的错误检查代码）：

```c
int sd;
struct sockaddr_in pin;
struct hostent *nlp_host;
nlp_host = gethostbyname(host_name);
memset(&pin, sizeof(pin));
pin.sin_family = AF_INET;
pin.sin_addr.s_addr = htonl(INADDR_ANY);
pin.sin_addr.s_addr = (struct in_addr *)(nlp_host->h_addr)->s_addr;
pin.sin_port = htons(port);
sd = socket(AF_INET, SOCK_STREAM, 0);
connect(sd, (void *)&pin, sizeof(pin));
```

```c
// 注意：消息末尾发送回车：
sprintf(message, "GET /index.html HTTP/1.1\n");
send(sd, message, strlen(message), 0);
printf("...sent message.. wait for response...\n");
recv(sd, buf, 8192, 0); // buf 长度为 8192 
printf("%s from NLServer:%s\n", buf);
close(sd); // 我们完成了，关闭 socket 并退出
```

# 测试 Web 服务器和 Web 客户端

打开两个 xterm 窗口，并在两个窗口中切换到 `IPC/SOCKETS` 。在第一个窗口中，输入：

```bash
make
web_server
```

在第二个窗口中，输入：

```bash
web_client
```

现在你应该会在运行 `web_server` 示例程序的窗口中看到以下输出：

```
mark@colossus:~home/mark/MyDocs/LinuxBook/src/IPC/SOCKETS > web_server
Binding socket to port 8000
Accepting connections ...
```

# UDP：用户数据协议

作者：Mark Watson

## 本章内容

- 使用 UDP 发送数据的示例程序 313
- 接收 UDP 数据的示例程序 314
- 运行 UDP 示例程序 315

# 进程间通信与网络编程

## 第三部分

用户数据协议 `UDP` 是一个比 `TCP` 更底层的协议。具体而言，`UDP` 既不提供保证可靠的消息投递，也不提供失败通知。此外，`UDP` 消息无法保证按照发送的顺序送达。一种常见的观点是，对于所有应用程序，使用 `TCP` 套接字而不是 `UDP` 是更好的方法。公平地说，使用 `TCP` 有以下几个优势：

- `TCP` 套接字提供保证可靠的投递或返回错误状态。
- 如果必须传输大块数据，使用 `TCP` 并保持套接字打开比将数据拆成小块更高效（`UDP` 数据包的物理块大小限制为 8192 字节，但每个数据包用户数据的可用空间为 5200 字节）。
- 当需要检测并重发数据包时，软件实现会变得更加复杂。

我在多个项目中使用过 `UDP`（用于 DARPA 的 NMRD 监控系统、用于 PacBell 的 Sleuth 实时欺诈检测专家系统，以及用于 Angel Studios 的基于 PC 的网络悬浮船游戏）。`UDP` 可以比 `TCP` 高得多，但只有在满足以下条件时我才建议使用：

- 需要发送的数据适用于一个 `UDP` 数据包。`UDP` 数据包的长度为 8192 字节，但由于头部数据的开销，我假设一个 `UDP` 数据包可以存放 5000 字节的数据。
- 某些传输数据的丢失不会破坏系统的完整性。
- 任何丢失的数据不需要重发。

使用 `UDP` 的理想对象是运行在局域网上的计算机。在局域网上，`UDP` 数据包很少丢失。此外，如果你使用 `UDP` 数据包发送更新信息，那么如果丢失了极小比例的数据，预期网络能够正常运行是合理的。

你将在后续章节中看到，使用 `UDP` 套接字与第 19 章中使用的 `TCP` 套接字示例非常相似。如果你学习并运行了第 19 章的示例程序，你（几乎）已经知道如何使用 `UDP`。你只需要在调用 `socket` 函数时更改单个参数来选择 `UDP`。本章将使用以下两个短程序：

- `send.c`——向接收者发送 20 条文本消息
- `receive.c`——从发送者接收文本消息并打印

对于正确类型的应用程序，使用 `UDP` 是一种强大的技术。使用 `UDP` 的开销远小于 `TCP`。

## 使用 UDP 发送数据的示例程序

以下示例（位于 `src/IPC/UDP` 目录下的 `send.c`）与之前的套接字示例相似，不同在于调用 `socket` 时，我们将第二个参数使用了 `SOCK_DGRAM` 而不是 `SOCK_STREAM`。我们为家族指定了 `AF_INET`，以便我们的示例能够处理通用的互联网 IP 地址（例如，我们可以指定“markwatson.com”作为主机名；域名服务器 `DNS` 会将“markwatson.com”解析为绝对 IP 地址，如 209.238.119.186）。`sockaddr_in` 变量的填充方式与光盘中 `SOCKETS` 目录下的 `client.c` 程序完全相同。使用的 IP 地址为 `127.0.0.1`，这意味着 `send.c` 和 `receive.c` 示例程序只有在同一台机器上运行时才能工作。此限制可以通过更改 `send.c` 中设置的 IP 地址轻松消除。

```c
#include <stdio.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>

int port = 6789;

void main() {
 int socket_descriptor; int iter = 0;
 int process;
char buf[80]; // 用于发送消息
struct sockaddr_in addr;
 // 这里，我们使用 SOCK_DGRAM (用于 UDP) 而不是 SOCK_STREAM (TCP):
 socket_descriptor = socket(AF_INET, SOCK_DGRAM, 0);
 memset(&addr, 0, sizeof(struct sockaddr_in));
 addr.sin_family = AF_INET;
 addr.sin_addr.s_addr = inet_addr("127.0.0.1"); // 本地计算机
 addr.sin_port = htons(port);
 process = 1; // 用于跳出 do-while 循环的标志
 do {
 sprintf(buf,"data packet ID %d\n", iter);
 if (iter > 20) {
 sprintf(buf, "stop\n");
 process = 0;
 }
 sendto(socket_descriptor,
 buf, sizeof(buf),
 0, (struct sockaddr *)&addr,sizeof(struct sockaddr_in));

iter++;
} while (process);
}
```

`do-while` 循环使用 `UDP` 发送了 20 条消息。使用 `UDP` 的。

## 接收 UDP 数据的示例程序

该程序（`UDP` 目录下的 `receive.c`）与 `SOCKETS` 目录下的 `server.c` 相似，不同在于调用 `socket` 时我们将第二个参数使用了 `SOCK_DGRAM` 而不是 `SOCK_STREAM`。对于 `TCP` 和 `UDP`，我们都使用 `gethostby` 来解析主机名。`sockaddr_in` 变量通过调用 `recvfrom` 进行填充。

```c
#include <stdio.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>
#include <string.h>
#include <unistd.h>

int port = 6789;

void main() {
 int socket_descriptor;
 int len;
 int sin_len;
char buf[256]; // 用于接收消息
struct sockaddr_in addr;
 // 这里，我们使用 SOCK_DGRAM (用于 UDP) 而不是 SOCK_STREAM (TCP):
 socket_descriptor = socket(AF_INET, SOCK_DGRAM, 0);
 memset(&addr, 0, sizeof(struct sockaddr_in));
 addr.sin_family = AF_INET;
 addr.sin_addr.s_addr = INADDR_ANY; // 本地计算机
 addr.sin_port = htons(port);
 bind(socket_descriptor, (struct sockaddr *)&addr, sizeof(struct sockaddr_in));

 while (1) {
  len = sizeof(struct sockaddr_in);
 recvfrom(socket_descriptor,
 buf, sizeof(buf),
 0, (struct sockaddr *)&addr, &len);
 printf("Response from server:\n%s", buf);
 if (strncmp(buf, "stop", 4) == 0) break;
 }
 close(socket_descriptor);
}
```

## 运行 UDP 示例程序

要运行 `UDP` 示例程序，进入你从光盘拷贝的 `UDP` 目录，输入以下命令：

```
make
receive
```

这将构建发送和接收程序并启动接收程序。你应该看到如下输出：
