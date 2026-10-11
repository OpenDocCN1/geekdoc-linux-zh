
```c
* TCPmechd.cpp - main, echo */
#include <winsock.h>
#include <string.h>

#define QLEN             5       /* 最大连接队列长度 */

#define BUFSIZE           4096
#define WSVERS            MAKEWORD(2, 0)

void      erexit(const char *, ...);
SOCKET    passiveTCP(const char *, int);
int       echo(SOCKET);

----------------------------------------------------------------*
* main - 用于 ECHO服务的并发 TCP 服务器
----------------------------------------------------------------*
void main(int argc, char *argv[]) {
	char        *service = "echo";      /* 服务名或端口号 */
	struct sockaddr_in fsin;     /* 来自客户端的地址 */
	socket      msock;
	fd_set  rfds;                   /* 读取文件描述符集 */
	fd_set  afds;                   /* 活跃文件描述符集 */
	int     alen;                    /* 源地址长度 */
	WSADATA wdata;
\unsigned int fdnx;

switch (argc) {
	case 1:
		break;
	case 2:
		service = argv[1];
		break;
```

## 第 12.5 节 单线程 ECHO 示例

default:

```c
errexit("*usage: TCPmethod [port]\n");

if (WSASartup(WSVERS, &wdata) != 0)
    errexit("*WSASartup failed\n");

msock = passiveTCP(service, QLEN);

FD_ZERO(&fds);
FD_SET(msock, &fds);

while (1) {
    memcpy(&fds, &fds, sizeof(fds));

    if (select(FD_SETSIZE, &fds, &rfds, (fd_set*)0, (struct timeval*)0) == SOCKET_ERROR)
        errexit("*select error: %d\n", GetLastError());
    
    if (FD_ISSET(msock, &fds)) {
        ssock = 0;

        len = sizeof(fsain);
        ssock = accept(msock, (struct sockaddr*)&fsain, &len);
        if (ssock == INVALID_SOCKET)
            errexit("*accept: error %d\n", GetLastError());
        FD_SET(ssock, &fds);

        for (fdndx=0; fdndx<rfds.fd_count; ++fdndx) {
            fd = rfds.fd_array[fdndx];
            if (fd != msock && FD_ISSET(fd, &fds)) {
                if (echo(fd) == 0) {
                    (void) closesocket(fd);
                    FD_CLR(fd, &fds);
                }
            }
        }
    }
}
```

```c
/*---------------------------------------
* echo - 回显一个缓冲区的数据，返回字节数
---------------------------------------
*/
int
echo(SOCKET fd) {
    char buf[BUFSIZE];
    int cc;

    cc = recv(fd, buf, sizeof(buf), 0);
    if (cc == SOCKET_ERROR) {
        errexit("echo echo recv error %d\n", GetLastError());
    }
    if (cc && send(fd, buf, cc, 0) == SOCKET_ERROR) {
        errexit("echo send error %d\n", GetLastError());
    }
    return cc;
}
```

单线程服务器的启动方式与多线程实现中的主服务器类似，通过打开一个被动套接字来监听已知端口。它使用 `FD_ZERO` 和 `FD_SET` 创建一个与它想要测试的套接字描述符对应的向量。服务器进入无限循环，在循环中调用 `select` 等待一个或多个描述符变为就绪。

如果主描述符就绪，服务器调用 `accept` 获取一个新连接。它将新连接的描述符添加到它所管理的集合中，并继续等待更多活动。如果某个从线程描述符就绪，服务器调用 `echo`，该函数又调用 `recv` 从连接中获取数据并将其发送回客户端。如果其中一个从线程描述符报告了文件结束（EOF）状态，服务器将关闭该描述符并使用宏 `FD_CLR` 将其从正在使用的描述符集合中移除。

## 12.6 总结

并发服务器的执行通常是由数据的到达驱动的，而不是由底层操作系统的定时机制驱动。在服务处理较少的情况下，单线程实现可以使用异步 I/O 来管理与多个客户端的连接，其效率与使用多线程或进程的实现相当。

单线程实现承担了主线程和从线程的职责。当主套接字就绪时，服务器接受新连接。当任何其他从套接字就绪时，服务器接收请求并发送响应。一个 ECHO 服务的单线程服务器示例说明了这些思想并展示了编程细节。

## 进一步学习

一个良好的协议规范不会限制实现方式。例如，本章描述的单线程服务器实现了由 Postel [RFC 862] 定义的 ECHO 协议。第 11 章展示了基于相同协议规范构建的多线程并发服务器的示例。

## 练习题

- 12.1 进行一个实验，证明示例 ECHO 服务器可以并发处理连接。
- 12.2 将本章讨论的实现用于 DAY-TIME 服务是否有意义？为什么或为什么不？
- 12.3 阅读 Windows 文档以查找传递给 `select` 的列表中描述符的精确表示。写出 `FD_SET` 和 `FD_CLR` 宏。
- 12.4 在具有多个处理器的计算机上比较单线程和多线程服务器实现的性能。在什么情况下，单线程版本的性能会优于（或等同）多线程版本？
- 12.5 假设有大量客户端（例如 100 个）同时访问本章中的示例服务器。解释每个客户端可能会观察到什么。
- 12.6 单线程服务器是否会在反复响应另一个客户端请求的同时，剥夺一个客户端的服务？多线程实现是否可能表现出相同的行为？请解释。

# 13

## 多协议服务器 (TCP, UDP)

## 13.1 引言

上一章描述了如何构建一个使用异步 I/O 的单线程服务器，以便在多个连接之间提供表面的并发性。本章扩展了这一概念。它展示了单线程服务器如何适应多种传输协议。它通过展示单线程服务器可以容纳多种传输协议来阐明这一思想。

### 13.2 减少服务器数量的动机

为每个协议使用独立服务器的主要优势是控制。为每个协议使用独立服务器的缺点是它们会消耗资源。当考虑到 TCP/IP 标准定义了数十种服务时，问题的规模就显而易见了。

### 13.3 多协议服务器设计

多协议服务器由单个线程组成，该线程使用异步 I/O 处理 UDP 或 TCP 的通信。服务器最初打开两个套接字：一个使用无连接传输 (`UDP`)，另一个使用面向连接的传输 (`TCP`)。随后服务器使用异步 I/O 等待一个套接字就绪。如果 `TCP` 套接字就绪，客户端请求了连接。服务器调用 `accept` 获取新连接。如果 `UDP` 套接字就绪，客户端以数据包的形式发送了请求。服务器使用 `recvfrom` 接收请求并记录发送者的地址。一旦计算出响应，服务器使用 `sendto` 将其发回客户端。

## 13.4 线程结构

图 13.1 展示了迭代多协议服务器的线程结构。

0ff5db763d2952e789585a5178acf3bc_167_0.png
