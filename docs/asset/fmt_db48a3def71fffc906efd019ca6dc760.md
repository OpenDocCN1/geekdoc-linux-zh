
创建套接字时，它属于特定的协议域，但未分配任何协议地址。套接字的协议地址也称为其地址或名称。如果没有进程引用套接字，则不需要为该套接字分配地址。例如，如果在客户端进程中创建套接字，则很可能没有其他进程会引用它。因此，将地址绑定到客户端套接字是不必要的。如果其他进程需要引用套接字，则必须为其分配地址。服务器进程创建的套接字需要将其地址绑定（即分配）给它。此地址为服务器进程提供的服务做广告，以便客户端进程可以使用服务器端套接字的地址联系服务器进程。图 20.12 显示了一个具有三个带地址的套接字的服务器进程和一个未分配地址的套接字的客户端进程。服务器进程中的套接字类型为 `PF_LOCAL`、`PF_INET` 且通信类型为 `SOCK_STREAM`，以及 `PF_INET` 且通信类型为 `SOCK_DGRAM`。客户端套接字没有地址。

您可以使用 `bind()` 系统调用为套接字分配地址。以下是 `bind()` 系统调用的简要描述。

```c
#include <sys/types.h>
#include <sys/socket.h>
int bind(int s, const struct sockaddr *addr, socklen_t addrlen);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

这里，`s` 是套接字描述符，`addr` 是要绑定到 `s` 的地址，`addrlen` 是 `addr` 的长度。为了最大限度地提高可移植性，`addr` 字段必须初始化为零。

![](img/02e070097d401d3bf7de4bf1c470b267_941_0.png)

图 20.12 带和不带地址绑定的套接字：（a）具有三个带地址的套接字的服务器进程，一个 `PF_LOCAL` 套接字，一个 `PF_INET` 且类型为 `SOCK_STREAM` 的套接字，一个 `PF_INET` 且类型为 `SOCK_DGRAM` 的套接字；以及（b）具有 `PF_INET` 且类型为 `SOCK_DGRAM` 且无地址的客户端进程。

# 表 20.16 bind() 系统调用失败的常见原因

| 失败原因 | errno 的值 |
|---|---|
| 没有足够的内核资源来完成请求 | `EAGAIN` |
| s 参数不是有效的描述符 | `EBADF` |
| s 参数表示已关闭（或已关闭）或已绑定到地址的套接字 | `EINVAL` |
| s 参数不代表套接字 | `ENOTSOCK` |
| addr 参数表示的地址已在使用中 | `EADDRINUSE` |
| addr 参数不在进程地址空间内 | `EFAULT` |

`bind()` 调用可能因各种原因而失败。一些常见的原因列在表 20.16 中。

对于 UNIX 域套接字，`bind()` 系统调用会因 `open()`、`creat()`、`mkfifo()` 和 `mkfifoat()` 系统调用失败的原因而失败，如表 18.4 和 20.7 所示。当 UNIX 域套接字不再需要时，必须使用 `unlink()` 系统调用将其从系统中删除。套接字的地址不能被与该套接字关联的进程之外的任何人读取/写入。

以下代码片段显示了如何使用 `bind()` 系统调用将地址绑定到 Internet 域套接字。

```
#define PORT 6001
...
struct sockaddr_in saddr, caddr;
...
/* Initialize socket structure */
memset(&saddr, 0, sizeof(saddr));
saddr.sin_family = AF_INET;
saddr.sin_addr.s_addr = INADDR_ANY;
saddr.sin_port = htons(PORT);

/* Bind address to socket */
if (bind(s, (struct sockaddr *)&saddr, sizeof(saddr)) == -1) {
    perror("bind failed");
    exit(1);
}
```

请注意，在 `bind()` 调用中使用地址结构变量之前，必须对其进行正确初始化。符号常量 `INADDR_ANY` 在 `/usr/include/netinet/in.h` 中定义，是一个通配符 IP 地址，与服务器进程运行的主机的任何 IP 地址匹配。因此，对于多宿主主机，即连接到多个网络并且因此具有多个 IP 地址的主机，使用通配符地址 `INADDR_ANY` 使服务器能够接受来自到达这些 IP 地址中的任何一个的客户端的连接请求。`htons(PORT)` 函数用于在将端口值赋给 `sockaddr` 地址变量的 `sin_port` 字段之前，将 `PORT` 值从主机网络字节序转换为网络字节序。只有超级用户（即 root）才能绑定到端口 < 1024。

## 练习 20.9

编写一个程序，创建一个 UNIX 域套接字，为其分配名称，并使用 UNIX 地址变量显示套接字描述符及其地址。

## 20.6.8 使服务器端套接字能够监听来自客户端的连接请求

一旦服务器端面向流的套接字被分配了地址，就需要在客户端进程可以连接到它并与其通信之前将其置于被动（监听）模式。您可以使用 `listen()` 系统调用将套接字置于被动模式。一旦在套接字上调用了 `listen()` 调用，它就开始监听来自客户端进程的传入连接请求。这样的套接字称为被动套接字。一旦套接字被置于被动模式，客户端的连接请求就可以被它接受。

以下是 `listen()` 系统调用的简要描述。

```
#include <sys/types.h>
#include <sys/socket.h>
int listen(int s, int backlog);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

这里，`s` 是套接字描述符，`backlog` 指定客户端连接请求可能等待的队列的最大长度。根据 `listen()` 调用的手册页，实际最大队列长度是程序员指定的 `backlog` 的 1.5 倍。此队列的最大长度在 `/usr/include/sys/socket.h` 文件中定义为 `SOMAXCONN`。`SOMAXCONN` 的值在 BSD 和 Solaris 上为 128。许多知名服务器在其被动套接字上使用最大队列长度。您可以使用 `netstat -aL` 命令确定系统上运行的所有服务器关联的队列长度。

`listen()` 调用可能因表 20.17 中列出的原因而失败。

# 表 20.17 listen() 失败的原因

| 失败原因 | errno 的值 |
|---|---|
| s 不是有效的描述符 | `EBADF` |
| s 不是套接字描述符 | `ENOTSOCK` |
| s 已连接或正在连接过程中 | `EINVAL` |
| s 的类型不支持 listen() 操作 | `EOPNOTSUPP` |

以下代码片段展示了 `listen()` 系统调用的典型用法。请注意，与被动套接字关联的队列长度为 5。

```
#define QLEN 5
...
/* Put socket in passive mode */
if (listen(s, QLEN) == -1) {
    perror("listen failed");
    exit(1);
}
...
```

## 20.6.9 向服务器进程发送连接请求

在面向连接的通信方式中，服务器端和客户端套接字首先被连接起来，然后两个进程才通过各自的套接字开始通信——两个进程都使用自己的套接字进行 I/O。一旦面向流的服务器端套接字被分配了地址并置于被动模式，它就准备好接收并接受客户端建立连接的请求。客户端进程可以使用 `connect()` 系统调用发送连接请求。

以下是 `connect()` 系统调用的简要说明。

```
#include <sys/types.h>
#include <sys/socket.h>
int connect(int s, const struct sockaddr *name, socklen_t namelen);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

为了最大化可移植性，`addr` 字段必须初始化为零。

当与 `SOCK_STREAM` 类型的套接字一起使用时，`connect()` 调用执行三次握手 TCP 握手以连接客户端和服务器端套接字。调用执行完成后，与每个套接字关联的底层数据结构都具有另一方的地址，并且两个套接字之间建立了完整的关联。这也意味着客户端和服务器进程之间建立了虚拟连接。这仅通过 `connect()` 和 `accept()` 系统调用的会合发生。我们将在下一节讨论 `accept()` 系统调用。一旦客户端和服务器端套接字之间建立了连接，客户端和服务器进程就可以使用 `read()` 和 `write()` 系统调用相互通信。
