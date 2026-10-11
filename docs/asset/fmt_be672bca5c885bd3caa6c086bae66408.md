
### 10.1
在本地系统上运行 `DAYTIME` 服务器需要特殊权限吗？运行 `DAYTIME` 客户端需要特殊权限吗？请解释原因。

### 10.2
利用连接的存在触发服务器响应的主要优势是什么？主要的缺点又是什么？

某些 `DAYTIME` 服务器通过回车符（`CR`）和换行符（`LF`）两个字符的组合来结束行。修改示例服务器，在行末尾发送 `CR-LF` 而不是仅发送 `LF`。标准是如何规定行应该如何结束的？

`TCP` 软件通常为服务器忙期间到达的额外连接请求分配一个固定大小的队列，并允许服务器在 `listen` 期间更改队列大小。你的本地 `TCP` 软件提供的队列有多大？服务器通过 `listen` 可以将队列做得多大？

修改 `TCPd.cpp` 中的示例服务器代码，使其在写入响应后不再显式关闭连接。它运行正常吗？为什么？

比较一个在发送响应后显式关闭每个连接的面向连接的服务器，和一个允许客户端在关闭连接前任意长时间保持连接的服务器。这两种方法的优缺点分别是？

假设 `TCP` 使用 4 分钟的连接超时时间（即在连接关闭后保留 4 分钟的信息）。如果 `DAYTIME` 服务器运行在一个具有 100 个 `TCP` 连接信息槽位的系统上，该服务器在不耗尽槽位的情况下处理请求的最大速率是多少？

## 11
## 并发面向连接的服务器 (TCP)

### 11.1 引言

上一章说明了迭代服务器如何使用面向连接的传输协议。本章提供了一个使用面向连接传输协议的并发服务器示例。示例服务器遵循算法 8.4+，这是程序员在构建并发 `TCP` 服务器时最常用的设计。服务器依赖操作系统对并发处理的支持，在计算响应时实现并发。系统管理员安排主服务器在系统启动时自动启动。主服务器永久运行，等待来自客户端的新连接请求。主服务器为每个新连接创建一个新的从线程来处理，并允许每个从线程处理其与客户端的所有通信。

后续章节将考虑并发服务器的替代实现方案，并展示如何扩展这里介绍的基本思想。

### 11.2 并发 ECHO

考虑第 7 章中描述的 `ECHO` 服务器。客户端与服务器建立连接，然后跨连接重复发送数据，并接收服务器返回的“回声”（`echo`）。`ECHO` 服务器对每个客户端做出响应。它接受连接，从连接中接收数据，然后发送相同的数据。

> *请参见第 112 页关于算法 8.4 的描述。*

为了允许客户端发送任意数量的数据，服务器在发送响应之前不会接收整个输入。相反，它在接收和发送之间交替。当新连接到达时，服务器进入循环。在循环的每次迭代中，服务器首先从连接接收数据，然后将数据发回。服务器继续迭代直到遇到文件结束（`EOF`）条件，此时它关闭连接。

### 11.3 迭代实现与并发实现

`ECHO` 服务器的迭代实现性能可能很差，因为它要求给定的客户端在它处理所有之前的连接请求时等待。如果客户端选择发送大量数据（例如许多兆字节），迭代服务器将延迟所有其他客户端，直到它能够满足该请求。

`ECHO` 服务器的并发实现避免了长时间等待，因为它同时与许多客户端进行通信以推进。因此，从客户端的角度来看，并发服务器比迭代服务器提供了更好的观测响应时间。

### 11.4 线程结构

图 11.1 展示了并发面向连接服务器的线程结构。如图所示，主服务器不直接与客户端通信。相反，它只是在已知端口等待。因此，与第 10 章中的迭代服务器一样，主服务器接受每个连接并创建一个从线程来处理。

![Figure 11.1](img/7fd1ea9b2b1f2482f692c8dd336)

**图 11.1** 连接连接服务器的线程结构。任何时候，服务器由一个主线程和多个从线程组成。

### 11.5 示例服务器

文件 `TCPechod.cpp` 包含并发线程为多个客户端提供服务的 `ECHO` 服务器代码。

```cpp
/* TCPechod.cpp - main, TCPechod */
```

```cpp
#include <stdio.h>
#include <winsock.h>
#include <process.h>
```

```cpp
#define QLEN               5       /* 最大队列长度 */
#define STKSIZE          16536
#define BUFFERSIZE        4096
#define WSVERS           MAKEKEWORD(2, 0)
```

```cpp
SOCKET msock, ssock;          /* 主从服务器套接字 */
```

```cpp
int    TCPechod(SOCKET);
void   errexit(const char *, ...);
SOCKET passiveTCP(const char *, int);
```

```cpp
/*------------------------------------------------------
* main - 用于 ECHO 服务器的并发 TCP 服务器
*
*/
```

```cpp
int
main(int argc, char *argv[]) {
    char        *service = "echo";      /* 服务名或端口号 */
    struct      sockaddr_in fsin;     /* 客户端地址 */
    int         alen;                   /* 客户端地址长度 */
    WSADATA wsadata;

    switch (argc) {
        case 1:
            break;
        case 2:
            service = argv[1];
            break;
        default:
            errexit("usage: TCPechod [port]\n");
    }

    if (WSAsartup(WSVERS, &wsadata) != 0)
        errexit("WSAsartup failed\n");
    msock = passiveTCP(service, QLEN);

    while (1) {
```

## 第 11.5 节 一个并发 ECHO 服务器 139

```c
alen = sizeof(fsin);
ssock = accept(msock, (struct sockaddr*) &fsin, &alen);
if (ssock == INVALID_SOCKET)
    erreit("*accept: error resource number\n", GetLastError());
    if (_beginthread(void (*)(void *), TCPechod, STKSIZE, void **) < 0) {
    erreit("*_beginthread: %s\n", strerror(errno));
}

return 1;
/* not reached */
```

/*- TCPechod - 回显数据直到文件结束

   * */

```c
int
TCPechod(SOCKET fd)
{
    char buf[BUFSIZE];
    int cc;

    cc = recv(fd, buf, sizeof(buf), 0);
    while (cc != SOCKET_ERROR && cc > 0) {
        if (send(fd, buf, cc, 0) == SOCKET_ERROR) {
            fprintf(stderr, "echo send error: %d\n",
                GetLastError());
            break;
        }
        cc = recv(fd, buf, sizeof(buf), 0);
    }
    if (cc == SOCKET_ERROR) {
        fprintf(stderr, "echo recv error: %d\n", GetLastError());
        closesocket(fd);
        return 0;
    }
```

示例显示，控制并发的调用仅占了代码的一小部分。主线程在 `main` 中开始执行。在检查完参数后，主线程调用 `passiveTCP` 为已知协议端口创建一个被动套接字。然后它进入一个无限循环。

140 并发、面向连接的服务器 (TCP) 第 11 章

在循环的每次迭代中，主线程调用 `accept` 等待来自客户端的连接请求。与迭代服务器一样，该调用会阻塞直到请求到达。在底层 `TCP` 协议栈接收到连接请求后，系统为新连接创建一个套接字，`accept` 调用返回该套接字描述符。
