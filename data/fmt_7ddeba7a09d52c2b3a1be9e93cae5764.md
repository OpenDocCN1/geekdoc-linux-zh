
```c
int clisock;
struct sockaddr_in servaddr;
clisock = socket( AF_INET, SOCK_STREAM, 0);
memset(&servaddr, 0, sizeof(servaddr));
servaddr.sin_family = AF_INET;
servaddr.sin_port = htons( 48000 );
servaddr.sin_addr.s_addr = innet_addr( "192.168.1.1" );
```

注意这两个代码段之间的相似之处。正如我们稍后看到的，区别在于服务器使用该地址绑定到自身作为一种广告。客户端则使用此信息来定义它想要连接到的对象。

# 套接字原语

在本节中，我们将查看其他一些重要的服务端套接字控制原语。

## bind

`bind` 函数为套接字提供了本地命名能力。这可以用于命名客户端或服务器套接字，但它最常用于服务器情况。`bind` 函数由以下原型提供：

```c
bind( int sock, struct sockaddr *addr, int addrLen );
```

要被命名的套接字由 `sock` 参数提供，而之前定义的地址结构由 `addr` 定义。请注意，这里的结构与我们之前讨论的结构不同。`bind` 函数可以用于多种不同的协议，当使用用 `AF_INET` 创建的套接字时，必须使用 `sockaddr_in` 结构。因此，如下例所示，我们将 `sockaddr_in` 结构强制类型转换为 `sockaddr`。

```c
err = bind( servosock, (struct sockaddr *)&servaddr, sizeof(servaddr));
```

# 套接字编程简介 161

使用我们在上一个地址节服务器示例中创建的地址结构，我们将 `servaddr` 定义的名称绑定到我们的服务器套接字 `svsock`。回想，客户端应用程序也可以调用 `bind` 来命名客户端套接字。这并不常用，因为 Sockets API 会动态地为我们分配端口。

## listen

在服务器套接字能够接受传入的客户端连接之前，它必须调用 `listen` 函数来声明其意愿。`listen` 函数由以下函数原型提供：

```c
int listen(int sock, int backlog);
```

`sock` 参数代表之前创建的服务器套接字，`backlog` 参数代表可能队列的待处理客户端连接数。在 GNU/Linux 中，`backlog` 参数（2.2 内核版本之后）表示等待应用层协议调用 `accept` 的已建立连接数。其他操作系统可能会对此进行不同的处理。

## accept

`accept` 调用是服务器用于接受传入的客户端连接所做的最后一个调用。在调用 `accept` 之前，必须创建服务器套接字，为其绑定一个名称，并调用 `listen`。`accept` 函数返回客户端连接的套接字描述符，由以下函数原型提供：

```c
int accept(int sock, struct sockaddr *addr, int *addrLen);
```

在实践中，通常会看到两种 `accept` 示例。第一种代表我们需要知道是谁连接了我们的情况。这需要创建一个不会初始化的地址结构。

```c
struct sockaddr_in cliaddr;
int cline;
cliLen = sizeof(struct sockaddr_in);
clisock = accept(servsock, (struct sockaddr*)cliaddr, &cliLen);
```

对 `accept` 的调用将阻塞直到客户端连接可用。返回后，`clisock` 的值将包含新客户端套接字的值，而 `cliaddr` 将代表客户端对端的地址（主机地址和端口号）。

另一种示例通常出现在服务器应用程序对客户端信息感兴趣的情况下。通常如下：

```c
clisock = accept(servsock, (struct sockaddr*)NULL, NULL);
```

# 162 GNU/Linux 应用程序编程

在这种情况下，地址结构和长度传递了 `NULL`。`accept` 函数将忽略这些参数。

## connect

`connect` 函数用于客户端套接字应用程序连接到服务器。客户端必须已经创建一个套接字，然后定义一个包含它们想要连接的主机和端口数的地址结构。`connect` 函数由以下函数原型提供：

```c
int connect(int sock, (struct sockaddr*)servaddr, int addrLen);
```

`sock` 参数代表我们之前用 Sockets API 创建的客户端套接字。`servaddr` 结构是我们想要连接的服务器对端（如本章“套接字地址”节节所示）。最后，我们必须传递 `servaddr` 结构的长度，以便 `connect` 知道我们正在传递一个 `sockaddr_in` 结构。以下代码展示了一个完整示例示例：

```c
int clisock;
struct sockaddr_in servaddr;
clisock = socket(AF_INET, SOCK_STREAM, 0);
memset(&servaddr, 0, sizeof(servaddr));
servaddr.sin_family = AF_INET;
servaddr.sin_port = htons(48000);
servaddr.sin_addr.s_addr = inet_addr("192.168.1.1");
connect(clisock, (struct sockaddr *)&servaddr, sizeof(servaddr));
```

## 套接字 I/O

存在多种函数可以从套接字读取数据或向套接字写入数据。两种 API 函数（`recv`, `send`）用于已连接的套接字（如流套接字），而另一对函数（`recvfrom`, `sendto`）用于未连接的套接字（如数据报套接字）。

## 连接套接字函数

# 套接字编程简介 163

`send` 和 `recv` 函数用于向对端发送消息和从对端接收消息。这些函数具有以下原型：

`send` 函数的第一个参数是要发送信息的套接字描述符。定义为 `const void *` 是因为 `msg` 指向的对象不会被 `send` 函数修改。在 `msg` 中发送的字节数由 `len` 参数包含。最后，可以使用 `flags` 参数来改变 `send` 调用的行为。通过之前创建的流发送字符串的示例所示：

```c
strcpy(buf, "Hello");
send(sock, (void *)buf, strlen(buf), 0);
```

在此示例中，我们的字符数组由 `strcpy` 函数初始化。该缓冲区随后通过 `sock` 端发送，长度由字符串长度定义。为了说明标志的使用，让我们看看 `send` 用的一个影响。当调用 `send` 时，它可能会阻塞直到 `buf` 中的所有数据都已放入套接字的发送队列中。如果没有足够的空间给此，`send` 函数将阻塞直到空间可用。如果我们想避免这种阻塞行为，而是让 `send` 调用在空间足够时直接返回，我们可以使用 `MSG_DONTWAIT` 标志，例如：

```c
send(sock, (void *)buf, strlen(buf), MSG_DONTWAIT);
```

`send` 的返回值代表错误（小于 0）或等待发送的字节数。`send` 函数的完成并不意味着数据已传输到主机，而只是队列在套接字的发送队列中等待传输。

`recv` 函数在参数列表方面镜像了 `send` 函数。不是发送 `msg` 指向的数据，`recv` 函数用从套接字读取的字节填充缓冲区。我们必须定义缓冲区的大小，以防网络协议栈覆盖缓冲区，这由 `len` 参数定义。最后，我们可以使用 `flags` 参数来改变读取调用的行为。`recv` 函数的返回值是 `msg` 缓冲区现在包含的字节数，出错时为 -1。`recv` 函数的一个示例是：

```c
#define MAX_BUFFER_SIZE 50
char buffer[MAX_BUFFER_SIZE+1];
...
numBytes = recv(sock, buffer, MAX_BUFFER_SIZE, 0);
```

在此示例完成后，`numBytes` 将包含缓冲区参数内部的字节数。

# 164 GNU/Linux 应用程序编程

我们可以使用 `MSG_PEEK` 标志来查看可读取的数据。此操作会执行一次读取，但不会消耗套接字缓冲区中的数据。这需要通过另一个 `recv` 来消耗这些可用数据。这种类型的读取示例例如所示：

```
numBytes = recvv(sock, buffer, MAX_BUFFER_SIZE, MSG_PEEK);
```

这会导致一次额外的内存拷贝（第一次用于查看数据，第二次用于实际读取并消耗数据）。在大多数情况下，这种行为是在应用程序层处理的，即通过实际读取数据来决定采取什么的操作。

## 未连接套接字函数

`sendto` 和 `recvfrom` 函数用于向对端套接字端发送消息以及从对端套接字端接收消息。这些函数具有以下原型：

```
int sendto(int sock, const void *msg, int len,
unsigned int flags,
const struct sockaddr *to, int len);
int recvfrom(int sock, void *buf, int len,
unsigned int flags,
struct sockaddr *from, int *fromlen);
```

`sendto` 函数用于未连接的套接字向由初始化地址结构体定义的目的地发送数据报。`sendto` 函数与之前讨论的 `send` 函数类似，不同之处接收者是由结构体定义的。`sendto` 函数的示例在下面的代码所示：

```
struct sockaddr_in destaddr;
int sock;
char *buf;
...
memset(&destaddr, 0, sizeof(destaddr));
destaddr.sin_family = AF_INET;
destaddr.sin_port = htons(581);
destaddr.sin_addr = inet_addr('192.168.1.1');
sendto(sock, buf, strlen(buf), 0,
(struct sockaddr *)&destaddr, sizeof(destaddr));
```

在这个示例中，我们的数据报（包含在 `buf` 中）被发送到主机 `192.168.1.1` 端口 `581` 上的应用程序。`destaddr` 结构体定义了我们数据报的接收者。

# 套接字编程简介 165

与 `send` 函数一样，它会返回等待传输的字符数量，如果发生错误则返回 -1。

`recvfrom` 函数提供了未连接套接字接收数据报的能力。`recvfrom` 函数再次类似于 `recv` 函数，需要提供一个地址结构体和长度。地址结构体用于将数据报的发送者返回给函数调用者。这些信息可以配合 `sendto` 函数，向原始发送者返回响应数据报。

`recvfrom` 函数的示例见下面的代码：

```
#define MAX_LEN 100
struct sockaddr_in fromaddr;
int sock, len, fromlen;
char buf[MAX_LEN+1];
...
fromlen = sizeof(fromaddr);
len = recvfrom(sock, buf, MAX_LEN, 0,
(struct sockaddr*)&fromaddr, &fromlen);
```

此阻塞调用在发生错误（用返回 -1 表示）或接收到数据报（返回值为 0 或更大）时返回。数据报将包含在 `buf` 中，长度为 `len`。`fromaddr` 将包含数据报发送者，具体包括源应用程序的主机地址和端口号。

# 套接字选项

套接字选项允许应用程序更改套接字及其操作套接字函数的可修改行为。例如，应用程序可以修改发送或接收套接字缓冲区的大小，或者修改 TCP 层为给定套接字使用的最大段大小。

用于设置和检索给定套接字选项的函数由以下原型提供：

```
getsockopt(int sock, int level, int optname,
           void *optval, socklen_t *optlen);
setsockopt(int sock, int level, int optname,
            void *optval, socklen_t *optlen);
```

首先，我们使用 `sock` 参数定义感兴趣的套接字。接下来，我们必须定义所应用的套接字选项级别。`level` 参数可以是 `SOL_SOCKET`（套接字层选项）、`IPPROTO_IP`（IP 层选项）和 `IPPROTO_TCP`（TCP 层选项）。级别特定选项通过 `optname` 参数应用。参数 `optval` 和 `optlen` 定义了选项的值。`optval` 用于获取或设置选项值，而 `optlen` 定义了选项的长度。使用这种稍微复杂的结构是因为结构体也可以用于定义选项。

# 166 GNU/Linux 应用程序编程

现在让我们来看一个既设置又检索选项的示例。在第一个示例中，我们将检索某个套接字发送端缓冲区的大小。

```
int sock, size, len;

getsockopt(sock, SOL_SOCKET, SO_SNDBUF,
       (void *)&size, (socklen_t *)&len);
printf("Send buffer size is %d\n", size);
```

现在我们来看一个稍微复杂的示例。在这种情况下，我们将设置 `linger`（滞留）选项。套接字 `linger` 允许我们在套接字关闭且留有数据时更改流的行为。在调用 `close` 后，任何剩余数据都将尝试在一段时间内发送。如果一段时间后数据仍无法发送，则数据将被丢弃。`close` 后数据从发送队列中移除的时间定义为滞留时间。这可以使用名为 `linger` 的特殊结构体来设置，如下例所示：

```
struct linger linger;
int sock;

linger.l_onoff = 1; /* 启用 */
linger.l_linger = 10; /* 10 秒 */
setsockopt(sock, SOL_SOCKET, SO_LINGER,
           (void *)&linger, sizeof(struct linger));
```

执行此调用后，套接字将在 `close` 调用后等待 10 秒才会中止发送。

## 其他杂杂函数

现在让我们来看 Sockets API 中的一些杂杂函数及其提供的功能。我们在本节讨论的三个函数原型见下面的代码：

```
struct host *gethostbyname(const char *name);
int getockname(int sock, struct sockaddr *name,
               socklen_t *namelen);
int getpeername(int sock, struct sockaddr *name,
               socklen_t *namelen);
```

# 套接字编程简介 167

函数 `gethostname` 提供了将主机和域名（亦称为完全限定域名或 FQDN）解析为 IP 地址的方法。例如，`microsoft.com` 可以解析为 IP 地址 `13.107.63.30`。获取主机名可以解析 FQDN。`gethostbyname` 函数的示例如下：

```
struct host *gethostbyname(const char *name);
```

`gethostname` 函数提供了将主机和域名（亦称为完全限定域名，或 FQDN）解析为 IP 地址的方法。例如，`microsoft.com` 可以解析为 IP 地址 `13.107.63.30`。获取主机名可以解析 FQDN。`gethostbyname` 函数的示例如下：

```
struct host *gethostbyname(const char *name);
```

`gethostname` 函数提供了将主机和域名（亦称为完全限定域名，或 FQDN）解析为 IP 地址的方法。例如，`microsoft.com` 可以解析为 IP 地址 `13.107.63.30`。获取主机名可以解析 FQDN。`gethostbyname` 函数的示例如下：

```
struct host *gethostbyname(const char *name);
```

`gethostname` 函数提供了将主机和域名（亦称为完全限定域名，或 FQDN）解析为 IP 地址的方法。例如，`microsoft.com` 可以解析为 IP 地址 `13.107.63.30`。获取主机名可以解析 FQDN。`gethostbyname` 函数的示例如下：

（注：此处原文存在大量重复，翻译已按逻辑结构对齐）

`gethostname` 函数提供了将主机和域名（亦称为完全限定域名，或 FQDN）解析为 IP 地址的方法。例如，`microsoft.com` 可以解析为 IP 地址 `13.107.63.30`。获取主机名可以解析 FQDN。`gethostbyname` 函数的示例如下：

（此处由于原文文本存在严重的重复和乱码问题，翻译已根据上下文提取了核心含义并对齐）
