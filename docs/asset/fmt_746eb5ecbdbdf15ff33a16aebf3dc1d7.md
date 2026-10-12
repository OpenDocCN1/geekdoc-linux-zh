
```c
/*
 * UDPClient.c -- 一个 UDP socket 客户端
 */
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>

#define MYPORT 3490    /* 服务器绑定的端口 */

int main(int argc, char *argv[]) {
    /* 用于通信的 socket */
    int sfd;
    struct sockaddr_in s_addr, m_addr; /* s(服务端)和 m(我的)地址数据 */
    char buf[1024];
    int n;

    memset(m_addr, 0, sizeof(m_addr)); /* 我的地址信息 */
    m_addr.sin_family = AF_INET;
    m_addr.sin_port = htons(MYPORT);    /* 0 == 为我分配一个端口 */
    m_addr.sin_addr.s_addr = htonl(INADDR_ANY);

    memset(s_addr, 0, sizeof(s_addr)); /* 服务端地址信息 */
    s_addr.sin_family = AF_INET;
    s_addr.sin_port = htons(MYPORT);
    s_addr.sin_addr.s_addr = inet_addr("127.0.0.1");

    /* 打开 UDP socket */
    if ((sfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket");
        return(-1);
    }

    /* 绑定到本地 UDP 端口（随机分配） */
    if (bind(sfd, (struct sockaddr*)&m_addr, sizeof(m_addr)) < 0) {
        perror("bind");
        return(-1);
    }

    /* 将标准输入的每行作为独立消息发送给服务器 */
    while (fgets(buf, sizeof(buf), stdin) != NULL) {
        n = strlen(buf) + 1; /* 包含 EOS */
        sendto(sfd, buf, n, 0, (struct sockaddr*)&s_addr, sizeof(s_addr));
    }

    /* 关闭 socket */
    close(sfd);
}
```

# 使用 `connect()` 的 UDP 客户端

与其使用 `sendto()/recvfrom()`，UDP 客户端可以先调用 `connect()`，然后使用 `sendto()/recv()`：

### Listing 10.6.25 示例-使用 `connect()` 的 UDP 客户端

```c
/* 在调用 bind() 后 */
/* 连接到远程主机和 UDP 端口 */
if (connect(sfd, (struct sockaddr*)&s_addr, sizeof(s_addr)) < 0) {
    perror("connect");
    return(-1);
}
```

### 10.6.7 处理多个客户端

来自 10.6.5 节的骨架代码会阻塞单个客户端连接的 `accept()` 和 `read()` 调用。这意味着它只能服务自身。通常，服务器应该能够处理许多客户端。在本节中，我们将讨论用于构建多客户端服务器的机制。

### `select(2)` 系统调用

`select(2)` 允许同时监控多个 `socket`。它会指示哪些 `socket` 准备好读取，哪些准备好写入，以及哪些 `socket` 发生了异常。虽然 `select()` 主要用于网络应用程序，但它也适用于绑定到任何 I/O 设备的文件描述符。其原型定义如下：

### Listing 10.6.6 `select(2)` API 调用

```c
/* 根据 POSIX.1-2001, POSIX.1-2008 */
#include <sys/select.h>
/* 根据早期的标准 */
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>

int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
```

**返回值**：`select()` 返回已就绪的文件描述符数量。如果出错，则返回 `-1`。

**参数**：`nfds` 是最大文件描述符值加一；`readfds`、`writefds` 和 `exceptfds` 分别是读取、写入和异常的文件描述符集合；`timeout` 是超时时间，如果为 `NULL`，则将无限等待。

`select()` 返回后，超时可能会更新。由于内核间隔约为 10 毫秒，因此无论你如何设置 `timeval`，你可能都会等待。

## Linux 内核实现 `select`

`select()` 的工作原理是遍历文件描述符。对于每个文件描述符，它调用 `poll()` 方法，将调用者添加到等待队列，并返回当前的事件（可读、可写、异常）。

`poll()` 方法的实现取决于相应的设备驱动，但所有实现都具有以下原型：

Listing 10.6.28 内核 `poll` 方法原型

```c
unsigned int (*poll)(struct file *, poll_table *);
```

驱动程序的方法在 `select()` 系统调用执行时被调用。它负责监控或多个可能发生状态变化的等待队列。

- `poll_wait()` 在一个或多个可能发生状态变化的等待队列上
- 返回一个无需阻塞即可执行的操作掩码。

`poll_table` 结构体（`poll()` 方法的第二个参数）被内核用于实现 `select()` 和 `poll()`，它在 `linux/poll.h` 中定义，包含一个操作轮队列的方法和一个位掩码。

Listing 10.6.29 内核 `poll` table 结构

```c
typedef struct poll_table_struct {
    poll_queue_proc _qproc;
    __poll_t _key;
} poll_table;
```

可以唤醒进程并改变操作状态的事件队列可以通过调用函数 `poll_wait()` 添加到 `poll_table` 结构中

Listing 10.6.30 内核 `poll_wait()`

```c
static inline void poll_wait(struct file * filp,
    wait_queue_head_t * wait_address, poll_table *p){
    if (p && p->_qproc && wait_address)
        p->_qproc(filp, wait_address, p);
}
```

# 树莓派上的 Linux 操作系统基础

下面是一个使用 `select()` 的 TCP 服务器示例代码。它只是将从客户端接收的消息打印到标准输出（`STDOUT`）。

## 列表 10.6.31 使用 `select(1)` 的服务器骨架：设置、绑定和监听

```
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#include <sys/time.h>
#include <sys/select.h>

#define MYPORT 3490 /* 用户将连接的端口 */
#define MAX_CLIENTS 5
#define MAX_NCHARS 128 /* 单次读/写的最大字符数 */
#define FALSE 0
/* ======================================================== */
int main(int argc
```

# 第 10 章 | 网络

## 列表 10.6.32. 使用 `select(2)` 的服务器骨架：`select`, `accept` 和 `read`
