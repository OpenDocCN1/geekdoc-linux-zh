
```c
unsigned short sa_family;

char sa_data[MAXSOCKADDR_DATA];
};
```

前两个字节（`short`的大小）指定地址所属的族。Linux 应用程序常用的地址族列表见 325 页的表 16.1。

## 16.2 工具函数

本节的所有示例都使用了两个函数：`copyData()` 和 `die()`。`copyData()` 从文件描述符读取数据并写入另一个，直到没有数据可读为止。`die()` 调用 `perror()` 并退出程序。我们将这两个函数放在 `sockutil.c` 文件中，以保持示例整洁。作为参考，这里这两个函数的实现。

```c
/* sockutil.c - 简单的工具函数 */
```
```c
#include <stdio.h>
#include <unistd.h>
#include "sockutil.h"
/* 通过 perror() 发布错误消息并终止程序 */
void die(char * message) (
```
```c
perror(message);
exit(1);
)
```
```c
/* 将数据从文件描述符 'from'拷贝到文件描述符 'to'
    直到没有剩余数据可拷贝。发生错误时退出。 */
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

## 16.3 基本套接字操作

和其他大多数 Linux 资源一样，套接字通过文件抽象实现。它们通过 `socket()` 系统调用创建，该调用返回一个文件描述符。一旦套接字正确初始化，该文件描述符就可以像其他文件描述符一样用于 `read()` 和 `write()` 请求。当进程完成对套接字的使用时，应该 `close()` 与其相关的资源。

### 16.3.1 创建套接字

新套接字通过 `socket()` 系统调用创建，该调用返回一个用于未初始化套接字的描述符。套接字在创建时会绑定到特定的协议，但它尚未连接到任何地方。由于尚未连接，因此还无法对其进行读或写。

表 16.1 协议与地址族
| 地址族 | 协议 | 描述 |
| :--- | :--- | :--- |
| AF_UNIX | PF_UNIX | Unix 域 |
| AF_INET | PF_INET | TCP/IP (版本 4) |
| AF_AX25 | PF_AX25 | AX.25，用于业余无线电 |
| AF_IPX | PF_IPX | Novell IPX |
| AF_APPLETALK | PF_APPLETALK | AppleTalk DDS |
| AF_NETROM | PF_NETROM | NetROM，用于业余无线电 |

```c
#include <sys/socket.h>
```
```c
int socket(int domain, int type, int protocol);
```

与 `open()` 类似，`socket()` 在出错时返回小于 0 的值，成功时返回一个大于等于 0 的文件描述符。

这三个参数指定了要使用的协议族。第一个参数指定应使用的协议族，通常是表 16.1 中指定的值之一。

下一个参数 `type` 是 `SOCK_STREAM` 或 `SOCK_DGRAM`。`SOCK_STREAM` 指定了该协议族中提供流式连接的协议，而 `SOCK_DGRAM` 指定了同一族中的数据报协议。

最后一个参数指定要使用的协议，但受前两个参数指定的约束限制。通常，该参数为 0，让内核使用指定类型和族的默认协议。对于 `PF_INET` 协议族，TCP 是默认的流式协议，UDP 是默认的数据报协议。

- 6. 还有其他一些可用值，但应用程序代码并不使用它们。

### 16.3.2 建立连接

创建流式套接字后，在使用之前需要将其连接到某些地方。建立套接字连接在本质上是非对称的；每个连接的实现方式各不同。

一方将其套接字准备好连接到某些地方，并等待有人连接。这通常由启动并持续运行、等待其他进程的服务器应用程序完成。相反，客户端进程会创建一个套接字，告诉系统它们想要连接的哪个地址，然后尝试建立连接。一旦服务器（一直在等待客户端）接受了连接，两个套接字之间就建立了连接。在此发生之后，该套接字就可以用于双向通信了。

### 16.3.3 将地址绑定到套接字

服务器和客户端进程都需要告诉系统为套接字使用哪种地址。将地址附加到套接字的本地侧称为绑定套接字（binding），并通过 `bind()` 完成。

```c
#include <sys/socket.h>
```
```c
int bind(int sock, struct sockaddr *addr, int addrlen);
```

第一个参数是正在绑定的套接字，其他参数指定了用于端点的地址。

### 16.3.4 等待连接

创建套接字后，服务器进程通过 `bind()` 将套接字绑定到它们正在监听的地址。套接字绑定到地址后，进程通过调用 `listen()` 告诉系统它愿意让其他进程连接到该套接字（指定的地址）。然而，连接不会立即建立。`listen()` 过程必须首先通过 `accept()` 接受连接尝试。已 `listen()` 的地址发出的新连接尝试被称为挂起（pending），直到服务器接受它们。通常情况下，`accept()` 会阻塞直到有客户端尝试连接它。如果通过 `fcntl()` 将套接字标记为非阻塞，则在没有可用客户端时，`accept()` 将返回一个错误。`select()` 系统调用也可用于判断与套接字是否有待处理的连接。如果有挂起的连接，则该套接字被认为已就绪。

以下是 `listen()` 和 `accept()` 的原型：

```c
#include <sys/socket.h>
```
```c
int listen(int sock, struct sockaddr *addr, int addrlen);
```

这两个函数都期望套接字的文件描述符作为第一个参数。`listen()` 的另一个参数 `backlog` 指定了在拒绝进一步连接尝试之前，套接字上可以有多少个挂起的连接。网络连接在服务器接受之前处于挂起状态。通常，`accept()` 会阻塞直到客户端尝试连接它。如果通过 `fcntl()` 将套接字标记为非阻塞，则在没有可用客户端时，`accept()` 将返回一个错误。`select()` 系统调用也可用于判断与套接字是否有待处理的连接。如果有挂起的连接，则该套接字被认为已就绪。这两个函数都期望套接字的文件描述符作为第一个参数。`listen()` 的另一个参数 `backlog` 指定了在拒绝进一步连接尝试之前，套接字上可以有多少个挂起的连接。网络连接在服务器接受之前处于挂起状态。通常，`accept()` 会阻塞直到客户端尝试连接它。如果通过 `fcntl()` 将套接字标记为非阻塞，则在没有可用客户端时，`accept()` 将返回一个错误。`select()` 系统调用也可用于判断与套接字是否有待处理的连接。如果有挂起的连接，则该套接字被认为已就绪。

### 16.3.5 连接到服务器

与服务器一样，客户端在创建套接字后可能会 `bind()` 本地地址到套接字。通常，客户端并不关心本地地址，并跳过这一步，让内核分配任何方便的地址。

在 `bind()` 步骤之后，客户端 `connect()` 到一个服务器。

```c
#include <sys/socket.h>
```
```c
int connect(int sock, struct sockaddr *servaddr, int addrlen);
```

`connect()` 的是要连接的套接字，随后是应连接的地址。

图 16.1 显示了用于建立套接字连接的常用系统调用以及发生的顺序。

## 16.4 Unix 域套接字

Unix 域套接字是通过套接字 API 最简单的族。它们实际上并不代表网络协议；它们连接到同一机器上的套接字。尽管这限制了它们的用途，但许多应用程序使用了它们，因为它们提供了灵活的 IPC 机制。它们的地址是路径，当套接字绑定到路径时，路径会在文件系统中创建。代表 Unix 域的套接字文件可以 `stat()`，但不能通过 `open()` 打开；必须使用套接字 API。

Unix 域提供了数据报和流接口。数据报接口很少使用，在此不进行讨论。此处讨论的流接口与命名管道类似。然而，Unix 域套接字与命名管道并不相同。当多个进程操作命名管道时，任何一个进程都可以读取另一个进程通过管道发送的消息。每个命名管道就像公告板。当一个进程向公告板发布消息时，任何其他具有足够权限的进程都可以从公告板获取消息。

Unix 域套接字是面向连接的；到套接字的每次连接都会产生一个新的通信通道。服务器可能处理许多并发连接，每个连接都有一个不同的文件描述符。这一属性使得 Unix 域套接字比命名管道更适用于许多 IPC 任务；这也是许多标准 Linux 服务（包括 X Window 系统和系统日志）使用它们的主要原因。

### 16.4.1 Unix 域地址

Unix 套接字的地址是文件系统中的路径。如果文件不存在，当套接字通过 `bind()` 绑定到路径时，会创建一个套接字类型的文件。如果已存在文件（即使是套接字），`bind()` 将失败并返回 `EADDRINUSE`。`bind()` 将新创建套接字文件的权限设置为 0666，并根据当前 `umask` 进行修改。

# 330 第16 章 套接字网络

要 `connect()` 到现套接字，进程必须对该套接字文件具有读写权限。

Unix 域接字地址通过 `struct sockaddr_un` 结构传递。

```c
#include <sys/socket.h>
#include <sys/un.h>
```
```c
struct sockaddr_un (
    unsigned short sun_family;      /* AF_UNIX */
    char sun_path[UNIX_PATH_MAX];   /* pathname */
);
```

在 Linux 2.0.x 内核中，`UNIX_PATH_MAX` 为 108，这在未来的 Linux 内核版本中发生变化。第一个元素 `sun_family` 必须包含 `AF_UNIX`，表示该结构包含一个 Unix 域地址。`sun_path` 存储用于连接的路径。当地址的大小在与接字相关的系统调用之间传递时，传递的长度应该是路径中的字符数加上 `sun_family` 成员的大小。`sun_path` 不需要以 `\0` 终止，尽管它通常是这样的。

## 16.4.2 等待连接

在 Unix 域套接字上监听连接的建立遵循我们之前描述的步骤：创建套接字，将地址 `bind()` 到套接字，告诉系统 `listen()` 监听连接尝试，然后 `accept()` 连接。

这是一个简单的服务器，它反复在 Unix 域套接字（当前目录下的文件 `sample-socket`）上接受连接，并从套接字读取所有数据，将其显示在标准输出上。

```c
/* userver.c - Unix 域套接字简单服务器 */
/* 等待 ./sample-socket Unix 域
   套接字上的连接。一旦建立连接，就将数据
   从套接字拷贝到 stdout，直到另一端关闭
   连接，然后等待套接字的另一个连接。 */
#include <stdio.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>
#include "sockutil.h"       /* 一些工具函数 */
int main(void) {
    struct sockaddr_un address;
    int sock, conn;
    size_t addrlen;
    if ((sock = socket(PF_UNIX, SOCK_STREAM, 0)) < 0)
        die("socket");
    /* 任何预存在的套接字（或其他文件） */
        unlink("./sample-socket");
    address.sun_family = AF_UNIX;      /* Unix 域套接字 */
    strcpy(address.sun_path, "./sample-socket");
    /* 地址的总长度包括 sun_family
       元素 */
    addrlen = sizeof(address.sun_family) +
        strlen(address.sun_path);
    if (bind(sock, (struct sockaddr *) &address, addrlen))
        die("bind");
    if (listen(sock, 5))
        die("listen");
    while ((conn = accept(sock, (struct sockaddr *) &address,
        &addrlen)) >= 0) {
        printf("--- getting data\n");
        copyData(conn, 1);
        printf("done\n");
        close(conn);
    }
    if (conn < 0)
        die("accept");
    close(sock);
    return 0;
}
```

尽管这个程序很小，但它说明了如何编写一个简单的服务器进程。该服务器是一个迭代式服务器，因为它一次只处理一个客户端。服务器也可以写成并发服务器，同时处理多个客户端。

`unlink()` 调用在绑定套接字之前执行。因为如果套接字文件已存在，`bind()` 就会失败，这允许程序运行多次而不需要手动删除套接字文件。

服务器代码将 `struct sockaddr_un` 指针在 `bind()` 和 `accept()` 中都强制转换为 `(struct sockaddr *)`。所有与套接字相关的系统调用原型都定义为接收指向 `struct sockaddr` 的指针；类型转换防止了编译器对指针类型不匹配的报错。

## 16.4.3 连接到服务器

通过 Unix 域套接字连接到服务器包括创建套接字并 `connect()` 到目标地址。一旦套接字连接，就可以像处理任何其他文件描述符一样处理它。

以下程序连接到示例服务器使用的同一个套接字，并输入拷贝到标准输出。

```c
/* uclient.c - Unix 域套接字简单客户端 */
/* 连接到 ../sample-socket Unix 域套接字，
   将其输入拷贝到标准输出，
   然后退出。 */
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>
#include "sockutil.h"       /* 一些工具函数 */
int main(void) {
    struct sockaddr_un address;
    int sock, conn;
    size_t addrlen;
    if ((sock = socket(PF_UNIX, SOCK_STREAM, 0)) < 0)
        die("socket");
    address.sun_family = AF_UNIX;      /* Unix 域套接字 */
    strcpy(address.sun_path, "./sample-socket");
    /* 地址的总长度包括 sun_family
       元素 */
    addrlen = sizeof(address.sun_family) +
        strlen(address.sun_path);
    if (connect(sock, (struct sockaddr *) &address, addrlen))
        die("connect");
    while (copyData(sock, 1) > 0) {
        printf("--- getting data\n");
    }
    close(sock);
    return 0;
}
```
