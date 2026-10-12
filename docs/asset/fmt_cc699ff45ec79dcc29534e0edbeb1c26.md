
另一方面，这里是一个通过将套接字描述符转换为 `FILE*` 使用 `fprintf()` 进行典型套接字输出的片段：

```c
FILE *sp;
int sd;
sd = socket(AF_INET, SOCK_STREAM, 0);
.../** Connect to host ***/
sp = fdopen(sd, "w");          /* create FILE* from socket */
if ( sp == NULL )
    perror("FILE* conversion failed");
fprintf(sp, "%s, %s, %s\n",Name, Address, Phone);
```

请注意，在第一个示例中，程序必须循环执行 `write()` 才能发送所有字节。即使这是套接字流，你也不能保证程序一次发送所有字节。第二个实例没有这种限制，因为 `FILE*` 拥有自己的数据缓冲子系统。当你写入 `FILE*` 缓冲区时，子系统会强制你等待直到发送完所有字节。

当然，有一个专用的套接字写入调用：`send()`。与 `recv()` 调用一样，`send()` 让程序员对传输的执行有更多控制。原型声明如下

```c
#include <sys/socket.h>
#include <resolv.h>
int send(int sd, const void *msg, int len, unsigned int flags);
```

除了最后一个参数 `flags` 外，所有参数都与 `write()` 相同。`send()` 系统调用有几个选项有助于修改调用的行为：

- `MSG_OOB`：发送“带外”（Out Of Band）数据。如上所述，它允许你向对等方、客户端或服务器发送一个字节，以指示紧急状况。接收方只有一个字节专门用于 `OOB` 数据；后续的 `OOB` 消息会覆盖最后一条消息。当 `OOB` 消息到达时，操作系统会向负责的程序发出 `SIGURG`（紧急信号）。

- `MSG_DONTROUTE`：不允许路由数据包。这会导致数据包绕过路由表，强制网络尝试直接联系接收方。如果目标无法直接访问，调用将产生 `ENETUNREACH`（网络不可达）错误。只有诊断或路由程序使用此选项。

- `MSG_DONTWAIT`：不等待 `send()` 完成。此选项允许程序像在 `send()` 已完成（或委托）的情况下继续执行。如果使用了，操作系统会发出 `SIGIO` 信号，指示 `write()` 操作已完成。如果操作因 `send()` 队列已满而阻塞，调用将返回错误并将 `errno` 设置为 `EAGAIN`。

- `MSG_NOSIGNAL`：不发出 `SIGPIPE` 信号。如果另一端过早关闭，且你的程序发送另一条消息，你可能会收到 `SIGPIPE` 信号。如果你没有为此信号做好准备，你的程序将中止。

使用 `send()` 系统调用类似于使用 `recv()`。如果你想要聚合标志，请使用算术 OR 运算符：

```c
/******************************************/
/***  Do a normal write to socket pipe    ***/
/******************************************/

int bytes_sent;

bytes_sent = send(sd, buffer, MAXBUF, 0);

...

/************从套接字管道发送带外数据************/

int bytes_sent;

bytes_sent = send(sd, buffer, MAXBUF, MSG_OOB | MSG_NOSIGNAL);

...
```

第二个示例选择了 `MSG_OOB` 和 `MSG_NOSIGNAL`。请记住，这些示例与 `write()` 系统调用不同，因为它们增加了一个用于控制套接字的新参数。此外，若要使用 `write()`，套接字必须连接到服务器或主机。以下是一些你可能遇到的错误：

- `EBADF` 指定了无效的描述符。可能的原因是程序未检查 `socket()` 调用的返回值。

- `ENOTSOCK` 参数不是一个套接字。也许它混合了文件和套接字描述符。

- `EMSGSIZE` 套接字要求内核原子地发送该消息，而待发送消息的大小使得这变得不可能。广播消息不能被分片，或者程序设置了“不分片”的套接字选项。

- `EAGAIN` 套接字被标记为非阻塞，而请求的操作会阻塞。这不是一个错误，仅仅表示“尚未准备好”。请稍后再尝试发送。

- `EPIPE` 在面向连接的套接字上，本地端已关闭。在这种情况下，除非设置了 `MSG_NOSIGNAL`，否则进程还会接收到 `SIGPIPE`。（与 `write()` 系统调用中的 `EPIPE` 相同。）

你使用 `send()` 系统调用来向服务器发送提示。例如，如果你想使用服务器的网络 finger 服务，你就打开通往服务器端口（79）的通道，发送用户名，并读取响应。这个算法通常是客户端所做的事情。

执行这项任务不需要任何特殊选项。然而，你可能希望读取服务器发送给你的尽可能多的信息。有时响应可能比你缓冲区的大小还要大。下面的程序列表摘录展示了该算法的实现。你可以在随本书附带的光盘上找到完整的程序列表。

```c
/*******************************/
/*** 扩展端口测试器 - 添加访问任意端口和发送消息的功能 ***/
/*********************/
int main(int count, char *strings[])
{
    int sockfd;
    struct sockaddr_in dest;
    char buffer[MAXBUF];

    /*--- 创建套接字并分配端口号 ---*/
    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    bzero(&dest, sizeof(dest));
    dest.sin_family = AF_INET;
    dest.sin_port = htons(atoi(strings[2]));
    inet_addr(strings[1], &dest.sin_addr.s_addr);

    /*--- 连接到服务器并发送请求 ---*/
    if (connect(sockfd, &dest, sizeof(dest)) != 0 )
        PANIC("connect() failed");
    sprintf(buffer, "%s\n", strings[3]);
    send(sockfd, buffer, strlen(buffer), 0);
    /*--- 清空缓冲区并读取短回复 ---*/
    bzero(buffer, MAXBUF);
    recv(sockfd, buffer, MAXBUF-1, 0);
    printf("%s", buffer);
    close(sockfd);
    return 0;
}
```

如果你想使用此算法获取长回复，你需要将最后部分更改为以下内容：

```c
/****************************************/
/*--- 修改代码以获取较长回复 ---*/
/****************************************/
/*--- 清空缓冲区并读取短回复 ---*/
do
{
     bzero(buffer, MAXBUF);
     bytes = recv(sockfd, buffer, MAXBUF, 0);
     printf("%s", buffer);
}
while ( bytes > 0 );
close(sockfd);
```

如果服务器在向你发送数据后关闭连接，则此添加部分工作正常。否则，你的程序将无限期地等待数据。

等待信息是套接字编程中的一个特定问题。有时你可以信任服务器在发送完成后关闭连接。然而，一些服务器期望保持通道打开，直到客户端关闭它。请注意，如果你的程序等待很长时间，你可能正面临这种类型的问题。

## 不同类型的 sockaddr

网络支持几种不同类型的协议。每个协议都有特定的功能和特性。对网络来说，它们都只是数据包。数据包类型包括：

| 命名套接字 | 协议常量 | 描述 |
| :--- | :--- | :--- |
| 命名套接字 | `PF_LOCAL` | 实际上并未连接到网络。这严格用于使用文件系统处理队列。 |
| `Internet Protocol` | `PF_INET` | （已演示过。） |
| `Novell Protocol` | `PF_IPX` | 用于与 `Novell` 网络通信。 |
| `AppleTalk` | `PF_APPLETALK` | 用于与 `AppleTalk` 网络通信。 |
