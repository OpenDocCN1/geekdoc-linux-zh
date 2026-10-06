

## 27.2 Socket API 的功能

以下参数被传递给 `socket()` 系统调用：

- `int family` 表示所使用的协议，因此也表示所使用的地址类型。定义了以下地址族（AF_...）的常量：
    - **AF_UNIX**: 用于本地计算机进程间通信的套接字。
    - **AF_INET**: 基于互联网协议版本 4 的 TCP/IP 协议族套接字。
    - **AF_INET6**: 基于新互联网协议第 6 版本的 TCP/IP 协议族。（参见第 23 章。）
    - **AF_IPX**: IPX 协议族。

- `int type` 表示所所需的通信关系的类型。在 TCP/IP 协议族中，我们主要区分三种类型：
    - **SOCK_STREAM**（流式套接字）指定两个套接字之间面向流的、可靠的、有序的全双工连接。
    - **SOCK_DGRAM**（数据报套接字）指定无连接的、不可靠的数据报服务，数据包可能会乱序传输。
    - **SOCK_RAW**（原始套接字）。

- `int protocol` 如果存在多个具有指定类型属性的协议，则为该套接字选择协议。在 AF_INET 地址族中，`SOCK_STREAM` 套接字类型始终选择 TCP，而 `SOCK_DGRAM` 始终使用 UDP 作为传输协议。

如果类型本身就能唯一地标识某种协议，则 `socket()` 系统调用中的 `protocol` 参数可以设置为零。

应用示例：应该建立一个 TCP 套接字。第一个参数设置为 `AF_INET`，第二个设置为 `SOCK_STREAM`。第三个参数不需要；因此将其初始化为 0。

`int close (int sockfd);`

标准的 UNIX 系统调用 `close()` 用于关闭套接字。当套接字关闭时，系统必须确保内核缓冲区中等待就绪（等待确认）的数据实际上已发送（并确认）。通常情况下，系统在执行 `close()` 系统调用后立即返回，而内核仍在尝试处理队列中等待的数据。

`close()` 函数的唯一参数是：

```c
int sockfd 是要关闭的套接字描述符。进程终止时会自动释放所有已打开的套接字。
```

应用示例：

```c
#include <sys/socket.h>
int sockfd;
/* 创建套接字。 */
/* 通信操作。 */
close(sockfd);
```

`int bind(int sockfd, struct sockaddr *mAddress, int AddrLength)`

新创建的套接字没有分配本地地址或端口号。在客户端，用户程序并不一定需要关心它们使用的本地地址，因为这些地址可以自动分配。相比之下，服务器进程必须指定它们工作的端口，因为该端口被用于标识相应的服务。这意味着服务器必须将新套接字绑定到本地地址和端口上；这种绑定是 `bind()` 系统调用完成的任务。

`bind()` 系统调用需要以下参数：

```c
int sockfd 是一个套接字描述符。
struct sockaddr *mAddress 是指向结构的指针，该结构包含套接字要绑定的地址。
int AddrLength 指定第二个参数中提供的地址结构的大小。必须指定地址结构的大小，因为不同的地址族使用不同的地址格式。
```

`bind()` 系统调用用于三种情况：

- 服务器在系统内注册自己的地址。它们通知系统在该套接字上转发什么类型的数据包，例如带有特定端口号的数据包。服务器应用程序使用全局定义的端口号，即所谓的已知端口。它们由 IANA 根据请求分配并列在 `/etc/services` 文件中。
- 客户端本身存储一个特定地址。
- 无连接的客户端必须确保系统为其创建一个独立的地址，以便通信关系的另一端在回执时有一个有效的返回地址。

应用示例：TCP 服务器注册其自己的地址（IP 地址和端口）并声明自己准备好接收任意客户端请求。常量 `INADDR_ANY` 用于 IP 地址，它告诉系统应该使用适当的本地 IP 地址。这个 32 位的值必须通过 `htons()` 转换为网络字节序（参见第 27.2.3 节）。端口号应该是大于 1024 的值，以避免与已知端口冲突。端口号大小为 2 字节（注：原文为 16 bytes 疑为笔误），因此最初通过 `htons()` 转换为网络字节序。注意，预先用零值初始化地址结构是一个好习惯。

```c
#include <sys/types.h>
#include <sys/socket.h>

#define SERVER_TCP_PORT 2001

int sockfd;
struct sockaddr_in serv_addr;

/* 初始化地址区域。 */
memset(&serv_addr, 0, sizeof(serv_addr));
serv_addr.sin_family = AF_INET;
serv_addr.sin_addr.s_addr = htons(INADDR_ANY);
serv_addr.sin_port = htons(SERVER_TCP_PORT);

/* 绑定 */
bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr));
```

`int listen(int sockfd, int backlog)`

`listen()` 系统调用允许服务器为传入的连接做好准备。套接字被切换到被动模式并准备好接受连接。此外，通知系统可以排序请求。`listen()` 适用于面向连接的套接字类型（例如 `SOCK_STREAM`）。`listen()` 取两个参数：

- `int sockfd` 是套接字描述符。
- `int backlog` 表示可以放入队列的可能连接请求的数量。超过此值的请求将被拒绝。

应用示例：服务器进程在通过 `bind()` 声明其端口后调用 `listen()` 例程：

```c
#include <sys/socket.h>

/* 创建套接字并绑定地址。 */
listen(sockfd, 5);
```

`int accept(int sockfd, struct sockaddr *Peer, int AddrLength)`

一旦面向连接的服务器进程执行了上述 `listen()` 调用，使用 `accept()` 调用等待连接。它会阻塞进程直到连接请求到达。连接请求到达时，请求客户端的地址存储在名为 `Peer` 的数据结构中。该地址的长度存储在 `AddrLength` 中。随后，系统创建一个新的套接字，与客户端连接，并将该套接字的描述符作为 `accept()` 系统调用的结果返回。发生错误则返回负值。

`accept()` 调用：

- `int sockfd` 是就绪接收套接字的描述符。
- `struct sockaddr *Peer` 是指向预留内存空间的指针，用于通信伙伴的地址。当连接请求到达时，该地址会进入此结构。
- `int *AddrLength` 指定调用预留内存空间的大小（字节）。一旦 `accept()` 返回，此参数将显示实际的地址长度。

应用示例：成功的 `accept()` 调用返回后，服务器启动一个子进程，在新进程中与客户端继续通信。父进程可以关闭新套接字或等待其他客户端连接请求。

```c
#include <sys/types.h>
#include <sys/socket.h>

int sockfd, clilen;
struct sockaddr_in cli_addr;
clilen = sizeof(cli_addr);

/* socket, bind, listen, ... */

newsockfd = accept(sockfd, (struct sockaddr *) &cli_addr, &clilen);
if (newsockfd < 0)
    printf("ERROR: Creating new socket");
```

