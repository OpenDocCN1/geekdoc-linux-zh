
由于每个协议对网络地址都有自己的定义，`sockets` API 必须抽象化地址。它使用 `struct sockaddr` 作为地址的基本形式；其内容对于每个协议族定义都不同。每当将 `struct sockaddr` 传递给系统调用时，进程也会传递所传递地址的大小。

所有 `struct sockaddr` 类型都符合以下定义：

```
#include <sys/socket.h>

struct sockaddr
    unsigned short sa_family;
    char sa_data[MAXSOCKADDRDATA];
```

前两个字节（一个 `short` 的大小）指定该地址所属的地址族。Linux 应用程序常用的地址族列表在第 325 页的表 16.1 中。

## 16.2 工具函数

本节中的所有示例都使用了两个函数：`copyData()` 和 `die()`。`copyData()` 从文件描述符读取数据并写入另一个，直到没有剩余数据可读。`die()` 调用 `perror()` 并退出程序。我们将这两个函数都放在 `sockutil.c` 文件中，以保持示例程序的整洁。作为参考，这里是这些函数的实现。

```
/* sockutil.c - 简单的工具函数 */

#include <stdio.h>
#include <unistd.h>

#include "sockutil.h"

/* 通过 perror() 发送错误消息并终止程序 */
void die(char * message) {

perror(message);

    exit(1);

}

/* 将数据从文件描述符 'from' 拷贝到文件描述符 'to'
    直到没有数据可以拷贝。发生错误时退出。 */
void copyData(int from, int to) {
    char buf[1024];
    int amount;
    while ((amount = read(from, buf, sizeof(buf))) > 0) {
        if (write(to, buf, amount) != amount) {
            die("write");
            return;
        }
    }
    if (amount < 0)
        die("read");
}
```

## 16.3 基本 Socket 操作

与其他大多数资源一样，`sockets` 通过文件描述符实现。一旦 经过适当初始化，该文件描述符就可以像其他文件描述符一样用于 `read()` 和 `write()` 请求。当进程完成对 socket 操作后，应该 `close()` 以释放资源。

### 16.3.1 创建 Socket

新的 socket 通过 `socket()` 系统调用创建，该调用返回一个未化的 socket 文件描述符。socket 在创建时绑定到特定的协议，但它尚未连接到任何地方。由于尚未连接，无法对其进行读取或写入。

```
#include <sys/socket.h>
```

```
int socket(int domain, int type, int protocol);
```

就像 `open()` 一样，`socket()` 在出错时返回小于 0 的值，在成功时返回大于或等于 0 的文件描述符。

这三个参数指定要使用的协议。第一个参数指定应该使用的协议族，它通常是表 16.1 中指定的值之一。

下一个参数 `type` 是 `SOCK_STREAM` 或 `SOCK_DGRAM`，`SOCK_STREAM` 指定指定族中提供流式连接的协议，而 `SOCK_DGRAM` 指定同一族的数据报协议。

最后一个参数指定使用哪种协议，但受前两个参数的限制。通常，此参数为 0，让内核使用指定类型和族的默认协议。对于 `PF_INET` 协议族，TCP 是默认流协议，UDP 是默认数据报协议。

16.1 协议与地址族

| 地址 | 协议 | 协议描述 |
|---|---|---|
| AF_UNIX | PF_UNIX | Unix 域 |
| AF_INET | PF_INET | TCP/IP (版本 4) |
| AF_AX25 | PF_AX25 | AX.25，用于业余无线 |
| AF_IPX | PF_IPX | Novell IPX |
| AF_APPLETALK | PF_APPLETALK | AppleTalk DDS |
| AF_NETROM | PF_NETROM | NetROM，用于业余无线 |

### 16.3.2 建立连接

在创建流套接字后，它需要连接到某些地方才能发挥很大作用。建立套接字连接本质上是一个不对称的任务；连接的双方执行方式不同。

一方准备好其套接字以连接到某处，并等待有人连接它。这通常由启动并持续运行的服务器应用程序完成，等待其他进程连接它们。

相反，客户端进程创建一个套接字，告诉系统它们想要连接的地址，然后尝试建立连接。一旦服务器（一直在等待客户端）接受了连接尝试，在两个套接字之间的连接就建立了。在此发生之后，该套接字就可以用于双向通信。

## 16.3.3 将地址绑定到套接字

服务器和客户端进程都需要告诉系统为套接字使用哪个地址。将地址附加到套接字的本地端称为绑定套接字，通过 `bind()` 系统调用完成。

```c
#include <sys/socket.h>
```

```c
int bind(int sock, struct sockaddr * my_addr, int addrlen);
```

第一个参数是要绑定的套接字，其他参数指定了本地端使用的地址。

### 16.3.4 等待连接

创建套接字后，服务器进程 `bind()` 将套接字绑定到它们监听的地址。套接字绑定到地址后，进程通过调用 `listen()` 告诉系统它愿意允许其他进程向该套接字（在指定的地址）建立连接。一旦套接字绑定到地址，内核就能处理进程尝试连接该地址的请求。然而，连接不会立即建立。`listen()` 进程必须首先通过 `accept()` 系统调用接受连接尝试。向已监听的地址发起的新连接尝试被称为待处理连接（pending connections），直到连接被 `accept()` 接受。

通常，`accept()` 会阻塞直到客户端进程尝试连接它。如果套接字被标记为非阻塞，那么在没有可用客户端进程时，`accept()` 将返回错误。`select()` 系统调用也可以用于判断与套接字是否有待处理的连接。如果存在待处理连接，则该套接字在 `select()` 用中被视为可读。

以下是 `listen()` 和 `accept()` 的原型定义：

```c
#include <sys/socket.h>
int listen(int sock, int backlog);
int accept(int sock, struct sockaddr * addr, int * addrlen);
```

这两个函数都期望套接字的文件描述符作为第一个参数。`listen()` 的另一个参数 `backlog` 指定了在拒绝进一步连接尝试之前，套接字上可以有多少个待处理连接。在服务器接受连接之前，网络连接不会建立；在 `accept()` 之前，入站连接都是待处理的。通过提供一个小的待处理连接队列，内核减轻了服务器进程需要时刻准备好 `accept()` 连接的需求。历史上应用程序将最大 backlog 设置为 5，尽管有时需要更大的值。`listen()` 成功返回 0，失败返回非 0。

`accept()` 调用将一个待处理连接转换为已建立连接。已建立的连接被赋予一个新的文件描述符，`accept()` 返回。新的文件描述符从被 `listen()` 的套接字继承其属性。

`addr` 和 `addrlen` 参数指向内核填充的连接远程（客户端）端地址的数据。最初，`addrlen` 应该指向一个包含 `addr` 所向缓冲区大小的整数。`accept()` 返回一个文件描述符，如果发生错误则返回小于 0 的值，就像 `open()` 一样。

![](img/095d18a9be827fc2d1ccdd5b058befe5_355_0.png)

图 16.1 建立套接字连接

### 16.3.5 连接到服务器

像服务器一样，客户端可以在创建套接字后立即将其本地地址 `bind()`。通常，客户端并不关心本地地址是什么并跳过此步骤，允许内核为其分配任何方便的本地地址。

在 `bind()` 步骤（可以省略）之后，客户端 `connect()` 到服务器。

```c
#include <sys/socket.h>
int connect(int sock, struct sockaddr *servaddr, int addr_len);
```
