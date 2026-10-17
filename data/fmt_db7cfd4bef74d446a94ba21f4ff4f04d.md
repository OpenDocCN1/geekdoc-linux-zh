
```c
/* 绑定套字 */
if (bind(s, (struct sockaddr *)sin, sizeof(sin)) == SOCKET_ERROR)
  errexit("*无法绑定到 %s 端口: %d\n", service,
  GetLastError());
if (type == SOCK_STREAM && listen(s, qlen) == SOCKET_ERROR)
  errexit("*无法监听 %s 端口: %d\n", service,
  GetLastError());
```

```c
return s;
```

### 9.3 线程结构

图 9.1 展示了用于迭代、无连接服务器的简单线程结构。

![](img/7fd1ea9db2b1f52482f69f28c8dd336d_137_0.png)

**图 9.1** 迭代、无连接服务器的线程结构。单线程服务器使用一个套接字与多个客户端通信。

单线程服务器无限执行。它使用单一的被动套接字，该套接字已绑定到其提供的服务的已知协议端口。服务器从套接字获取请求，计算响应，并使用同一个套接字向客户端发送回复。服务器使用请求中的源地址作为回复中的目的地址。

## 9.4 一个 TIME 服务器示例

通过一个示例将说明无连接服务器如何使用上述描述的套接字分配程序。回想第 7 章，客户端使用 TIME 服务从另一个系统上的服务器获取当前时间。由于 TIME 需要的计算较少，因此迭代式服务器实现运行良好。文件 `UDPTimed.cpp` 包含了迭代、无连接 TIME 服务器的代码。

124 迭代式、无连接服务器 (UDP) 第 9 章

```c
/* UDPTimed.cpp - main */
#include <time.h>
#include <winsock.h>
```

```c
SOCKET passiveUDP(const char *);
void   errexit(const char *, ...);

#define WINERPOCH     2208988800    /* Windows 纪元时间，单位为 UTC 秒 */
#define WSVERS          MAKEWORD(2, 0)
```

```c
/*
 * main - 用于 TIME 服务器的迭代式 UDP 服务器
 * 
 */
```

```c
int
main(int argc, char *argv[])
{
    struct sockaddr_in fsin;      /* 客户端的地址 */
    char    *service = "time";  /* 服务名或端口号 */
    char    buf[2048];          /* "输入"缓冲区；任何大于 1 个数据包的大小 */
    SOCKET  sock;               /* 服务器套接字 */
    time_t now;                 /* 当前时间 */
    int     alen;                /* 源地址长度 */
    WSADATA wsadata;

    switch (argc) {
    case 1:
        break;
    case 2:
        service = argv[1];
        break;
    default:
        errexit("usage: UDPTimed\n");
    }
```

```c
if (WSASStartup(WSVERS, &wsadata))
    errexit("WSASStartup failed\n");
sock = passiveUDP(service);
```

```c
while (1) {
    alen = sizeof(fsin);
    if (recvfrom(sock, buf, sizeof(buf), 0,
        (struct sockaddr *)&fsin, &alen) == SOCKET_ERROR
```

```c
    exit("recvfrom: error %d\n", GetLastError());
    (void) time(&now);
    now = htonl((u_long)now + WINERPOCH);
    (void) sendto(socket, (char *)&now, sizeof(now), 0,
                (struct sockaddr *)&fsin, sizeof(fsin));

    return 1; /* * 未到达 */
```

与任何服务器一样，`UDPtimed` 线程必须无限执行。因此，代码的主体由一个无限循环组成，该循环接受请求、计算当前时间，并将回复发送给发送请求的客户端。

代码包含几个细节。在解析参数后，`UDPtimed` 调用 `passiveUDP` 为 TIME 服务创建一个被动套接字。它进入无限循环。TIME 协议规定它可以发送任意数据包来触发回复。该数据包可以是任意长度的，并且可以包含任何值，因为服务器不解释其内容。`recvfrom` 将数据包放在缓冲区 `buf` 中，并读取下一个数据包。发送数据包的客户端端点地址在 `fsin` 结构体中。

`UDPtimed` 使用 Windows 函数获取当前时间。回想第 7 章，Windows 使用 32 位整数表示时间，从 1970 年 1 月 1 日纪元开始计算。为了执行此操作，它加上 `WINERPOCH` 常量并使用 `htonl` 转换。最后，`UDPtimed` 调用 `sendto` 将结果发送给客户端。

### 9.5 总结

对于计算量少的简单服务，迭代式实现运行良好。本章介绍了使用 UDP 进行无连接传输。

## 进一步学习

- Harrenstein [738] 规定了 TIME 协议。
- Mills [1305] 描述了网络时间协议 (NTP)；
- Mills [1361] 总结了网络中使用 NTP 的问题；
- Owicki [1985] 讨论了时钟同步。

## 练习题

- 9.1 调试 `UDPtimed` 以确定每个请求花费的时间。如果你有网络分析仪，也测量请求和回复数据包之间的时间。
- 9.2 假设服务器在请求和回复之间覆盖了客户端地址（即调用 `sendto`）。会发生什么？为什么？
- 9.3 进行实验以确定当 N 个客户端同时发送时会发生什么。改变 N（发送者数量）和 S（数据包大小）。解释为什么服务器无法响应。
- 9.4 `UDPPrime` 代码在调用 `recvfrom` 时指定的缓冲区大小为 2048。如果将其指定为 1 会发生什么？
- 9.5 计算 Windows 纪元和互联网纪元之间的差异。考虑到闰年。你计算的值与 `UDPPrime` 中的常量匹配吗？如果不匹配，请解释。（提示：阅读闰秒。）
- 9.6 作为安全检查，系统管理员要求你修改 `UDPPrime` 以记录所有访问服务器的客户端。修改代码，每当请求到达时在控制台上打印一行。解释日志如何影响服务。
- 9.7 如果你有两台通过广域网连接的机器，使用第 7 章的 `UDPtime` 客户端和本章的 `UDPPrime` 服务器查看你的网络是否丢包。

# 10

迭代式、面向连接的服务器 (TCP)

### 10.1 引言

上一章提供了一个使用 UDP 进行无连接传输的迭代服务器示例。本章展示了迭代服务器如何使用 TCP 进行面向连接的传输。示例服务器遵循算法 8.1。

## 10.2 分配被动 TCP 套接字

第 9 章提到面向连接的服务器使用 `passiveTCP` 分配流式套接字并将其绑定到所提供服务的常用端口。`passiveTCP` 有两个参数。第一个参数是字符字符串，指定服务的名称或端口号；第二个参数指定连接请求队列的长度。如果第一个参数包含名称，它必须与库函数 `getservbyname` 访问的服务数据库中的条目匹配。如果第一个参数指定端口号，它必须以文本字符串表示该数字（例如 `79`）。

> *请参见第 107 页关于算法 8.1 的描述。*

128 迭代式面向连接的服务器 (TCP) 第10章

```cpp
/* passTCP.cpp - passiveTCP */

#include <winsock.h>

SOCKET passocket(const char *, const char *, int);

/*
 * passiveTCP - 为 TCP 服务器创建一个用于的被动套接字
 */
SOCKET passiveTCP(const char *service, int qlen)
{
  return passocket(service, "top", qlen);
}
```

## 10.3 用于 DAYTIME 服务的服务器
