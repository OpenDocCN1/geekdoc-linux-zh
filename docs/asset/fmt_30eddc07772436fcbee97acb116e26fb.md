
同样，`sd` 参数指示从 `socket()` 调用创建的套接字描述符。`numslots` 参数分配挂起连接槽位的数量。列表 6.3 中的代码段显示了一个典型用法。

#### 列表 6.3 Listen() 示例

```c
/***** 转换示例：将套接字转换为 ****/
/***** 用于客户端连接的监听套接字。 ****/

int sd;
sd = socket (PF_INET, SOCK_STREAM, 0);
/*** 绑定端口 *** */
if (listen (sd, 20) != 0) /* 转换为监听套接字 */
    perror("Listen"); /* ...带有 20 个挂起槽位 */
```

通常，服务器将队列深度设置在 5 到 20 个挂起连接之间。在正常生产（多任务）环境中，队列深度超过 20 通常是浪费的。如果没有多任务，你可能需要将这个数字增加到接近你设置的超时值（例如，对于 60 秒，则设为 60）。

以下是 `listen()` 系统调用通常返回的错误：

- `EBADF` 套接字描述符无效（参见 `bind()` 系统调用的描述）。

- `EPROTOSUPP` 套接字协议不支持监听调用。例如，`TCP` (`SOCK_STREAM`) 支持监听队列，但 `UDP` (`SOCK_DGRAM`) 不支持。

将套接字转换为监听套接字后的下一步是等待并接受连接，如下一节所述。

### 接受客户端连接

到目前为止，程序已创建套接字、绑定端口号并建立连接队列。现在，它可以接受连接。`accept()` 系统调用使套接字描述符成为所有连接的调度器。事情在这里变得有点奇怪，最初的规则被打破。当你将套接字转换为监听套接字时，它不再是一个双向数据通道。你的程序实际上甚至不能读取数据；监听套接字只允许你接受连接。`accept()` 系统调用等待（或阻塞）直到连接到达。

当客户端建立连接时，监听套接字使用该端口为该客户端创建一个新的双向通道。`accept()` 系统调用隐式为程序创建一个新的套接字描述符。实际上，每个新连接都在客户端和服务器之间创建一条新的专用线路。从这一点开始，你通过新通道与客户端交互。

此外，你可以确定谁正在连接你的服务器，因为该调用的几个参数获取了客户端的连接信息。第 4 章介绍了一个类似的系统调用 `recvfrom()`，它获取数据和返回地址。这些地址信息对于跟踪连接到你的服务器的计算机非常有用。

```c
#include <sys/socket.h>
#include <resolv.h>
int accept(int sd, sockaddr *addr, int *addr_size);
```

一如既往，`sd` 参数是套接字描述符。与 `recvfrom()` 系统调用一样，最后两个参数为调用提供了写入客户端地址和端口号的位置。与 `recvfrom()` 系统调用不同，`accept()` 的最后两个参数是可选的。如果你不想获取调用者的地址和端口号，只需将这些参数设置为零。

务必使 `addr` 参数的大小足够大，以接受其预期的地址。不要担心因缓冲区溢出导致的损坏；`accept` 不会超过 `addr_size` 字节。在大多数情况下，客户端连接的大小与协议相同（例如，`sockaddr_in` 的 `AF_INET` 或 `sockaddr_ipx` 的 `AF_IPX`）。该调用通过引用传递 `addr_size`，以便你的程序可以确定实际使用的字节数（参见列表 6.4）。

## 6 服务器入门

### 列表 6.4：Accept() 示例

```c
/************************************************/
/*** Accept Example: Wait for and accept a client     **/
/**  connection.                          **/ 
/************************************************/
int sd; 
struct sockaddr_in addr; 
/*** Create socket, bind it & convert it to a listener ***/
for(;;)   /* repeat this indefinitely */ 
{  int clientsd;        /* the new socket descriptor */ 
   int size = sizeof(addr); /* reassign the size of addr */ 

   clientsd = accept(sd, &addr, &size); /*await connection */
   if ( clientsd > 0 )      /* no error occurred */ 
   { 
      /*** Interact with client ****/ 
      close(clientsd);      /* clean up and disconnect */ 
   }
   else                   /* accept error */ 
      perror("Accept"); 
}
...
```

### 与客户端通信

请注意，列表关闭了 `clientsd`。`clientsd` 套接字描述符不同于 `sd`，即主套接字描述符。关闭 `clientsd` 很重要，因为每个连接都会生成一个新的描述符。如果不关闭每个连接，最终可能导致文件描述符插槽耗尽。

### 重用 addr 变量

你可以重用 `bind()` 系统调用中的 `addr` 局部变量。在完成服务器端口的 `bind()` 之后，服务器不再需要该信息。此时可以安全地将该变量用于其他用途。

请记住，大多数参数都采用网络字节序。你可以使用第 2 章中描述的转换工具（见列表 6.5）从 `addr` 中获取地址和端口号。

### 列表 6.5：带有连接日志记录的 Accept()

```c
/***** ****** *******************************************/
/*** Accept Example (revised): Add client-connection ***/
/*** logging. Compare with Listing 6.4 ***/
/***** ****** *******************************************/
/***** (Inside the loop) *****/
... 
client = accept(sd, &addr, &asize);
if ( client > 0 )
{
    if ( addr.sin_family == AF_INET )
        printf("Connection[%s]: %s:%d\n", /* log connection */
            ctime(time(0)), /* time-stamp connection */
            ntoa(addr.sin_addr), ntohs(addr.sin_port));
    /*---interact with client---*/
... 
```

如果 `accept()` 系统调用发生错误，它会向你的服务器返回一个负值。否则，它将返回一个新的套接字描述符。以下是一些常见的错误：

- `EBADF`：套接字描述符无效（请参见第 4 章中关于 `bind()` 的描述）。

- `EPROTONSUPP`：该调用要求套接字必须是 `SOCK_STREAM` 类型。

- `EAGAIN`：套接字被设置为非阻塞模式，且监听队列中没有待处理的连接。如果套接字被设置为非阻塞，则对 `accept()` 的调用在队列中无人等待时不会阻塞任务。

回声服务器简单地将其接收到的内容原样发送回来，直到收到 `bye` 消息为止（见列表 6.6）。

### 列表 6.6：回声服务器示例
