
```cpp
/* tclient.cpp - main */
#include <stdlib.h>
#include <winsock.h>

#define WSVERS MAKWORD(2, 0)

char     *host = "localhost";      /* 如果未提供则使用的主机 */

void   errexit(const char *, ...);
void   telnet(const char *, const char *);
/*----------------------------------------------------------------------*/
/*   main - TELNET 服务的 TCP 客户端
/*----------------------------------------------------------------------*/

void
int main(int argc, char *argv[])
{
    char *service = "telnet";      /* 默认服务名称 */
    WSADATA wsendata;

    switch (argc) {
    case 1: break;
    case 3:
        service = argv[2];
        /* 透穿 */
    case 2:
        host = argv[1];
        break;
    default:
        errexit("usage: telnet [host [port]]\n");
    }
    if (WSAStartup(WSVERS, &wsendata))
        errexit("WSAStartup 失败。\n");
    telnet(host, service);
    exit(0);
}
```

用户可以提供零、一个或两个命令行参数，程序将解析这些参数。如果没有参数（`argc=1`），客户端将连接到本地主机上的服务器并使用 `telnet` 服务。如果有一个参数（`argc=2`），客户端将该参数视为执行服务器的远程主机名。最后，如果有两个参数

## 第 25.24 节 TELNET 客户端 389 的参数

，客户端将第二个参数视为远程机器上服务的名称，将第一个参数视为远程主机的名称。在解析完参数后，主程序调用 `telnet` 函数。

## 25.25 TELNET 客户端的核心

文件 `telnet.cpp` 包含了实现算法 8.1 代码：

```cpp
/* telnet.cpp - telnet */

#include <io.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <winsock.h>

#include "local.h"

extern unsigned char syncing;

#define BUFSIZE 2048 /* 读取缓冲区大小 */

SOCKET connectTCP(const char *host, const char *service);
SOCKET ttycon(void);
/* telnet - 对给定的主机和端口执行 TELNET 协议 */
void telnet(const char *host, const char *service)
{
    SOCKET sock, con; /* 远程和控制台套字描述符 */
    u_char buf[BUFSIZE];
    int cc;
    int on = 1;
    fd_set arfds, rfds;

    con = ttycon();

    sock = connectTCP(host, service);

    fsmbuild();      /* 设置 FSM */

    (void) setsockopt(sock, SOL_SOCKET, SO_OBLOCKINE, (char *)&on,
      sizeof(on));

    FD_ZERO(&rfds);
    FD_SET(sock, &rfds);      /* 套字 */
    FD_SET(con, &rfds);       /* 标准输入 */

    while (1) {
        memcpy(&rfds, &rfds, sizeof(rfds));

        if (select(FD_SETSIZE, &rfds, (struct timeval*)0, 
            fd_set*)0, 0) < 0) {
            if (GetLastError() == WSAEINTR)   /* 仅为信号 */
                continue;
            errexit("select: %d\n", GetLastError());
        }
        if (FD_ISSET(con, &rfds)) {
            unsigned long no_urg;
            if (ioctl(sock, SIOCATURMARK, &no_urg) ==
                SOCKET_ERROR)
                errexit("socket ioctl error %d\n",
                    GetLastError());
        }
        synching = &no_urg;

        cc = recv(sock, (char *)buf, sizeof(buf), 0);
        if (cc == SOCKET_ERROR)
            errexit("socket recv: %d\n",
                GetLastError());
        else if (cc == 0)
            errexit("\nconnection close.\n");
        else
            ttwrite(sock, stdout, buf, cc);

    }
    if (FD_ISSET(con, &rfds)) {
        cc = recv(con, (char *)buf, sizeof(buf), 0);
        if (cc == SOCKET_ERROR)
            errexit("*tty read: %d\n",
                GetLastError());
    } else if (cc == 0) {
        FD_CLR(con, &rfds);
        (void) shutdown(sock, 1);
    } else {
        sowrite(sock, stdout, buf, cc);
    }
}
```

> † 参见第 107 页关于算法 8.1 的描述。

## TelNet 客户端的核心

```cpp
(void) fflush(stdout);
```

`telnet` 需要两个参数，分别指定远程机器的名称及其上的服务。代码通过调用 `connectTCP` 来分配套接字并与服务器建立 TCP 连接。然后，它调用 `fsmbuild` 初始化三个有限状态机。

一旦完成初始化，客户端的主线程将进入一个无限循环。在循环的每次迭代中，它使用 `select` 从远程连接或键盘进行 I/O 操作。如果程序在 `select` 阻塞时接收到中断，则该调用将返回值 `WSAEINTR`。如果发生这种情况，客户端将继续执行循环的下一次迭代。

如果 `select` 返回正常值，则数据可能在键盘、远程连接或两者均中可用。Telnet 首先检查远程连接，查看数据是否已从服务器到达。如果是，它将调用 `recv` 提取数据并写入用户的显示器。我们将在下文中看到，telnet 实现了一个原始有限状态机，用于解释输入的数据流并处理转义和嵌入命令序列。

在 telnet 检查指向远程服务器的套接字是否有输入数据后，它会检查键盘套接字。如果数据从键盘到达，telnet 调用 `recv` 提取数据并调用 `write` 将写入套接字。套接字包含了执行本地转义处理的有限状态机代码。作为特殊情况，客户端会将键盘输入的文件结束（EOF）解释为终止连接的请求。如果接收到文件结束（例如 `recv` 返回 0），telnet 在每次迭代中都会调用 `flush` 以确保输出程序不会缓存已写入的数据。`flush` 强制操作系统立即发送所有数据，即使缓冲区未满。

## 25.26 TELNET 同步
