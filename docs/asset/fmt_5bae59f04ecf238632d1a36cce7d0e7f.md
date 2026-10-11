
由于 `CreateProcess` 是从文件中检索新程序，上述设计允许系统管理员直接替换文件，而无需重新编译多服务服务器、终止服务器进程或重启它即可实现功能更新。从概念上讲，使用 `CreateProcess` 将处理每个服务的程序与建立连接的主服务器分离来。

在多服务服务器中，Windows 的 `CreateProcess` 调用使得处理单个服务的代码与管理客户端初始请求的代码分离成为可能。

## 14.8 多服务、多协议设计

虽然将多服务服务器认为是无连接的或面向连接的似乎很自然，但多协议设计也是可行的。正如第 13 节所述，多协议设计允许单个服务器线程同时管理同一服务的 UDP 套接字和 TCP 套接字。在多服务服务器的情况下，服务器可以为其提供的部分或全部服务管理许多 UDP 和 TCP 套接字。

许多网络专家使用“超级服务器”（super server）来指代多服务、多协议服务器。原则上讲，超级服务器的工作方式与传统的多服务服务器相似。最初，服务器为其提供的每个服务打开一个或两个主套接字。给定服务的主套接字对应无连接传输（UDP）或面向连接的传输（TCP）。服务器选择等待任何套接字就绪。如果 UDP 套接字就绪，服务器调用一个过程从套接字中读取下一个（数据报），计算响应并发送回复。如果 TCP 套接字就绪，服务器调用一个过程从套接字接受下一个连接并进行处理。服务器可以直接处理连接（通过迭代方式），也可以通过创建一个新线程（或新进程）来处理连接，从而实现并发。

## 14.9 多服务服务器示例

`super.cpp` 中的多服务服务器扩展了第 12 节中的单线程服务器实现。在初始化数据结构并为其每个服务打开套接字后，主程序进入无限循环。循环的每次迭代都会调用 `select` 等待套接字就绪。当一个或多个请求到达时，`select` 调用返回。

`event` 数组中的每个元素包含一个 `service` 类型的结构体，指定了服务与套接字描述符之间的映射。当 `select` 返回时，服务器遍历 `event` 并使用宏 `FD_JSSET` 测试记录在 `sv_sock` 字段中的描述符是否就绪。如果找到就绪的描述符，服务器将调用一个函数来处理该请求。

`sv_func` 字段包含处理服务的函数地址。在 `event` 中找到与就绪描述符对应的条目后，程序调用所选的函数。对于 UDP 套接字，服务器通过 `doTCP` 直接调用服务处理程序。

TCP 套接字需要额外的过程，因为 TCP 套接字在面向连接的服务器中对应于主套接字。当此类套接字就绪时，意味着连接请求已到达套接字。服务器需要创建一个新线程来管理该连接。因此，`doTCP` 过程调用 `accept` 来接受新连接。然后它调用 `_beginthread` 创建一个从线程来调用服务处理函数（`sv_func`）。当服务函数返回时，从线程终止。

```cpp
/* superd.cpp - main, dotTCP */

#include <process.h>
#include <winsock.h>

#define UDP_SERV 0
#define TCP_SERV 1

struct service {
    char    *sv_name;
    char    *sv_useTCP;
    SOCKET sv_sock;
    void    (*sv_func) (SOCKET);
};

void TCP(SOCKET), TCPchargend(SOCKET), TCPdaytimed(SOCKET),
     TCPptimed(SOCKET);

SOCKET passiveTCP(const char *, int);
SOCKET passiveUDP(const char *);
void   errexit(const char *, ...);
void   doTCP(struct service *);

struct service svent[] = {
    { "echo*", TCP_SERV, INVALID_SOCKET, TCPPechod },
    { "chargen*", TCP_SERV, INVALID_SOCKET, TCPchcharg },
    { "daytime*", TCP_SERV, INVALID_SOCKET, TCPdaytimed },
    { "time*", TCP_SERV, INVALID_SOCKET, TCPptimed },
    { 0, 0, 0, 0 }
};

#define WSERVERS   MAKEWORD(2, 0)
#define QLEN         5
#define LINELEN      128

extern u_short portbase; /* * from passivesock() * */
```

### Sec. 14.9 一个多服务服务器示例

```cpp
/* main - 超级服务器主程序
 */
void
main(int argc, char *argv[]) {
    struct service *psv; /* 服务表指针 */
    fd_set afds;         /* 可读描述符 */
    struct timeval wsdata;
    u_short portbase;

    switch (argc) {
    case 1:
        break;
    case 2:
        portbase = (u_short) atoi(argv[1]);
        break;
    default:
        errexit("*usage: superd [portbase]\n");
    }

    if (!WSAStartup(WSERVERS, &wsdata))
        errexit("*Startup failed");

    FD_ZERO(&fds);
    for (i=0; i<QLEN; ++i) {
        if (svent[i].sv_useTCP)
            svent[i].sv_sock = passiveTCP(svent[i].sv_name, portbase);
        else
            svent[i].sv_sock = passiveUDP(svent[i].sv_name);
        if (svent[i].sv_sock != INVALID_SOCKET)
            FD_SET(svent[i].sv_sock, &fds);
    }

    while (1) {
        if (select(QLEN, &fds, NULL, NULL, &wsdata) == -1)
            errexit("select error: %d\n", GetLastError());

        for (i=0; i<QLEN; ++i) {
            if (FD_ISSET(svent[i].sv_sock, &fds)) {
                if (svent[i].sv_useTCP)
                    _beginthread(NULL, NULL, (void __ccall *)doTCP, (void *)svent[i]);
                else
                    _beginthread(NULL, NULL, (void __ccall *)svent[i].sv_func, (void *)svent[i]);
            }
        }
    }
}
```
