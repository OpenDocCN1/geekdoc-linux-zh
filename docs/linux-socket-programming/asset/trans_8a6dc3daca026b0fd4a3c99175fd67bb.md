

```c
perror("Bind AF_INET");
```

使用清单 6.2 中的代码段绑定到命名套接字（AF_UNIX 或 AF_LOCAL）。

## 示例 6.2. 在 LOCAL 服务器中使用 bind()

```c
/**************************************************
/***  LOCAL Socket Example: Fill the sockaddr_un struct  ***/
/***  variable addr
/*****

#include <linux/un.h>
struct sockaddr_un addr;      /* create a local named socket */
bzero(&addr, sizeof(addr));   /* start with a clean slate */
addr.sun_family = AF_LOCAL;    /* select a named socket */
strcpy(addr.sun_path, "/tmp/mysocket");  /* select name */
if ( bind(sd, &addr, sizeof(addr)) != 0 )        /* bind name */
        perror("Bind AF_LOCAL");
```

使用此特定代码段，你可以查看 /tmp 目录并看到套接字文件。系统消息记录器 syslogd 使用 LOCAL 套接字获取其信息：系统进程打开到记录器套接字的连接并向其发送消息。

以下是调用时可能出现的典型错误：

- `EBADF` 套接字描述符无效。如果 `socket()` 系统调用失败且你未检查返回值，可能会发生这种情况。

- `EACCES` 请求的端口号仅允许 root 访问。请记住，如果你使用 0–1023 之间的端口，运行程序时必须是 root。更多信息，请参见第 2 章中关于主机端口号的部分。

- `EINVAL` 端口已被使用。你可能有另一个程序拥有此端口。此外，如果你在服务器死机后立即重新运行服务器，也可能会遇到此错误。操作系统释放已分配端口（最多 5 分钟！）需要一些时间。

在所有情况下，`bind()` 系统调用都尝试为你的服务器套接字分配一个特定的名称或端口（使用 /etc/services 文件作为可用端口或标准端口的参考）。客户端使用此端口建立连接并开始发送和接收数据。

## 创建套接字监听队列

套接字接口为你的程序提供了与其他网络上的程序连接的方式。连接是排他的：一旦某个程序连接，其他程序就无法连接。绕过此限制的一种方法是创建一个等待队列。

你使用 `listen()` 系统调用来启用套接字等待队列。回顾本章前面的示例，如果公司只有一部电话，它一次无法处理超过一个呼叫；因此，不太可能不会遇到忙音。解决方案是添加呼叫等待。

`listen()` 系统调用类似于呼叫等待队列。当服务器调用 `listen()` 时，它指定队列插槽的数量。此调用还将套接字转换为仅监听套接字。此转换很重要，以便你稍后使用 `accept()` 系统调用。

```c
#include <sys/socket.h>
#include <resolve.h>
int listen(int sd, int numslots);
```

同样，`sd` 参数表示由 `socket( )` 调用创建的套接字描述符。`numslots` 参数分配待处理连接插槽的数量。清单 6.3 中的代码段显示了一种典型用法。

## 示例 6.3. Listen( ) 示例

```c
/* ******************************************************/
/*   Listen-Conversion Example: Convert the socket to a   */
/*   listening socket for client connections.               */
/* ******************************************************/
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0);
/* ** Bind port ***/
if ( listen(sd, 20) != 0 )    /* convert to listening socket */
    perror("Listen");        /* ...with 20 pending slots */
```

通常，服务器将队列深度设置为 5 到 20 个待处理连接。在正常的生产（多任务）环境中，队列深度超过 20 通常是一种浪费。如果没有多任务，你可能需要将其增加到接近你设置的超时值（例如，60 秒设为 60）。

以下是 `listen( )` 系统调用通常返回的错误：

- `EBADF` 套接字描述符无效（参见 `bind( )` 系统调用的说明）。
- `EOPNOTSUPP` 套接字协议不支持 listen 调用。例如，TCP（`SOCK_STREAM`）支持监听队列，但 UDP（`SOCK_DGRAM`）不支持。

将套接字转换为监听套接字后的下一步是等待并接受连接，如下一节所述。

## 接受客户端连接

到目前为止，程序已创建套接字、绑定了端口号并设置了连接队列。现在，它可以接受连接了。`accept( )` 系统调用使套接字描述符成为所有连接的分派器。这里事情变得有点奇怪，并且最初的规则被打破。当你将套接字转换为监听套接字时，它不再是数据的双向通道。你的程序实际上甚至不能读取数据；监听套接字只允许你接受连接。`accept( )` 系统调用等待（或 *阻塞*）直到连接到达。

当客户端建立连接时，监听套接字使用相同的端口为该客户端创建一个新的双向通道。`accept( )` 系统调用隐式为程序创建一个新的套接字描述符。实际上，每个新连接都在客户端和服务器之间创建一条新的专用线路。从此，你通过新通道与客户端交互。

此外，你可以确定谁在连接到你的服务器，因为调用的一些参数获取了客户端的连接信息。*第 4 章* 介绍了一个类似的系统调用 `recvfrom( )`，它获取数据和返回地址。这些地址信息对于跟踪连接到你的服务器的计算机非常有用。

```c
#include <sys/socket.h>
#include <resolve.h>
int accept(int sd, sockaddr *addr, int *addr_size);
```

一如既往，`sd` 参数是套接字描述符。与 `recvfrom()` 系统调用一样，最后两个参数为调用提供了写入客户端地址和端口号的位置。与 `recvfrom()` 系统调用不同，`accept()` 的最后两个参数是 *可选的*。如果你不想获取调用者的地址和端口号，只需将这些参数设置为零。

确保 `addr` 参数的大小足够大，以接受其预期的地址。不用担心缓冲区溢出导致的损坏；调用不会超过 `addr_size` 字节。在大多数情况下，客户端连接的大小与协议相同（例如，`sockaddr_in` 对应 `AF_INET` 或 `sockaddr_ipx` 对应 `AF_IPX`）。该调用通过引用传递 `addr_size`，以便你的程序可以确定实际使用的字节数（参见 **清单 6.4**）。

## 示例 6.4. Accept() 示例

```c
/*************************************************************/
/*** Accept Example: Wait for and accept a client        ***/
/*** connection.                                         ***/
/*************************************************************/
int sd;
struct sockaddr_in addr;

/*** Create socket, bind it & convert it to a listener **/
for (;;)                                /* repeat this indefinitely */
{
    int clientsd;                       /* the new socket descriptor */
    int size = sizeof(addr);            /* reassign the size of addr */

    clientsd = accept(sd, &addr, &size); /*await connection */
    if ( clientsd > 0 )                 /* no error occurred */
    {
        /**** Interact with client ****/
        close(clientsd);                /* clean up and disconnect */
    }
    else                                /* accept error */
        perror("Accept");
}
...
```

## 与客户端通信

请注意，清单关闭了 `clientsd`。`clientsd` 套接字描述符与 `sd`（主套接字描述符）不同。关闭 `clientsd` 很重要，因为每个连接都会生成一个新的描述符。未能关闭每个连接最终可能导致文件描述符插槽耗尽。

### 注意

### 重用 `addr` 变量

你可以重用 `bind()` 系统调用中的 `addr` 局部变量。在完成服务器端口的 `bind()` 之后，服务器不再需要该信息。此时可以安全地使用该变量用于其他目的。

请记住，大多数参数都是网络字节序。你可以使用 **第 2 章** 中描述的转换工具从 `addr` 中获取地址和端口号（参见 **清单 6.5**）。

