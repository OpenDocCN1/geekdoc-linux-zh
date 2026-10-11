
```cpp
switch (argc) {
    case 1:
        break;
    case 2:
        service = argv[1];
        break;
    default:
        errexit("usage: UDP_ptimed\n");
}
```

```cpp
if (WSASStartup(WSVERS, &wsadata))
    errexit("WSASStartup failed\n");
sock = passiveUDP(service);
```

```cpp
while (1) {
    alen = sizeof(fsin);
    if (recvfrom(sock, buf, sizeof(buf), 0,
        (struct sockaddr *) &fsin, &alen) == SOCKET_ERROR
```

# 第 9.4 节 示例 TIME 服务器

```cpp
    errexit("recvfrom: error %d\n", GetLastError());
    (void) time(&now);
    now = htoml((u_long)now + WINERPOCH);
    (void) sendto(socket, (char *)&now, sizeof(now), 0,
        (struct sockaddr *)&fsin, sizeof(fsin));

}
return 1; /* 不可到达 */
```

与任何服务器一样，`UDPTimed` 线程必须永远执行。因此，代码的主体由一个无限循环组成，该循环接收请求、计算当前时间并将回复发送给发送请求的客户端。

代码包含几个细节。在解析参数后，`UDPTimed` 调用 `passiveUDP` 为 `TIME` 服务创建一个套接字。它进入无限循环。`TIME` 协议规定，客户端可以发送任意数据报来触发回复。该数据报可以是任意长度的，并且可以包含任何值，因为服务器并不解释其内容。`recvfrom` 将入站的数据报放置在缓冲区 `buf` 中，并填充发送该数据报的客户端的端点地址。

`Timed` 使用 Windows 函数 `time` 来获取当前时间。回想第 7 章，Windows 使用 32 位整数表示时间，从 1970 年 1 月 1 日午夜（纪元）开始测量。从 Windows 获取时间后，`UPDTimed` 必须将其转换为从互联网纪元（Internet epoch）测量的值，并将结果置于网络字节序。为了执行转换，它加上了常量 `WINERPOCH`，该常量定义值为 2208988800，即互联网纪元与 Windows 纪元之间的秒差。然后它调用函数 `htol` 将结果转换为网络字节序。最后，`UPDTimed` 调用 `sendto` 将结果传回客户端。`sendto` 使用结构体 `fsin` 中的端点地址作为目标地址（即它使用了发送数据报的客户端的地址）。

## 9.5 总结

对于简单的服务（即服务器对每个请求的计算很少的服务器），迭代式实现效果良好。本章介绍了一个用于 `TIME` 服务的迭代式服务器示例，该服务器使用 `UDP` 进行无连接访问。该示例说明了过程如何隐藏套接字分配的细节，并可以使服务器代码更简单、更易理解。

## 进一步学习

Hartenstein-[RFC 738] 规定了 `TIME` 协议。Mills [RFC 1305] 描述了网络时间协议 (`NTP`)；Mills [September 1991] 总结了在实际网络中使用 `NTP` 的相关问题，Mills [RFC 1361] 讨论了使用 `NTP` 进行时钟同步。Marzullo 和 Owicki [July 1985] 也讨论了在分布式环境中如何维护时钟。

# 练习题

- 9.1 对 `UDPTimed` 进行计时，以确定它处理每个请求花费多少时间。如果你可以访问网络分析器，也测量请求包和响应包之间经过的时间。

- 9.2 假设 `UDPTimed` 在接收和发送响应之间无意中覆盖了客户端地址（即在您调用 `sendto` 之前，服务器不地分配了一个随机值）。会发生什么？为什么？

- 9.3 进行一个实验，确定当 `N` 个客户端同时向 `UDP-timed` 发送请求时会发生什么。改变 `N`（发送者数量）和 `S`（数据包大小）。解释为什么服务器未能响应所有请求。

- 9.4 `UDPTimed.cc` 中的示例代码在调用 `recvfrom` 时指定了 2048 的缓冲区大小。如果它指定的缓冲区大小为 1 会发生什么？

- 9.5 计算 Windows 时间纪元与互联网时间纪元之间的差异。记得考虑闰年。

- 9.6 作为安全检查，系统管理员要求你修改 `UDPTimed`，使其记录所有访问服务器的客户端。修改代码，每当请求到达时在控制台上打印一行。解释日志如何影响服务。

- 9.7 如果你有两台连接的机器，使用第 7 章的 `UDP` 客户端和本章的 `UPDTimed` 服务器观察互联网丢包情况。

# 迭代式、面向连接的服务器 (TCP)

## 10.1 引言

上一章提供了一个使用 `UDP` 的迭代式服务器示例。本章展示了迭代式服务器如何使用 `TCP`。遵循算法 8.1。

## 10.2 分配被动套接字

第9章提到面向连接的服务器使用 `passiveTCP` 分配套接字并将其绑定到已知端口。`passiveTCP` 取两个参数。第一个参数是字符串，指定服务的名称或数字，第二个参数指定输入队列的长度。如果第一个参数包含名称，它必须匹配由 `getservbyname` 访问的服务数据库项。如果第一个参数指定端口号，它必须以文本字符串表示该数字（例如 `"79"`）。

```cpp
/* passTCP.cpp - passiveTCP */

#include <winsock.h>

SOCKET passivesock(const char *, const char *, int);

/*
 * passiveTCP - 为 TCP 服务器创建被动套接字
 * */
SOCKET passiveTCP(const char *service, int int)
passiveTCP(const char *service, int qlen)
{
    return passivesock(service, "tcp*", qlen);
}
```

## 10.3 用于 DAYTIME 服务的

回想第 7 章，`DAYTIME` 服务允许一台机器上的用户从另一台机器获取当前的日期和时间。因为 `DAYTIME` 服务是为了人类设计的，它规定服务器在发送回复时必须将日期格式化为易读的 ASCII 文本字符串。因此，客户端可以按照收到的方式显示响应。

第 7 章展示了客户端如何使用 `TCP` 连接 `DAYTIME` 服务器并显示服务器发送的日期。由于获取和格式化日期所需的处理很少，且预计服务需求不大，`DAYTIME` 服务器不需要为了速度进行优化。

## 10.4 线程结构

如图 10.1 所示，迭代式面向连接的服务器使用单个线程。该线程无限循环，使用一个套接字处理入站请求，并使用第二个临时套接字与客户端进行通信。

### 10.4 节 线程结构

![](img/0ff5db763d2952e789585a5178acf3bc_143_0.png)

**图 10.1** 迭代、面向连接服务器的线程结构。服务器在已知端口等待连接，然后通过该连接与客户端进行通信。

使用面向连接的传输协议的服务器会对连接进行迭代：它在已知端口等待来自客户端的下一个连接到达，接受连接、处理连接、关闭连接，然后再次等待。`DAYTIME` 服务使得实现变得特别简单，因为服务器不需要从客户端接收显式请求——它利用新入入连接的出现来触发响应。由于客户端没有发送显式请求，服务器不会从该连接中接收数据。

## 10.5 示例 DAYTIME 服务器

文件 `TCPdtd.cpp` 包含一个迭代式、面向连接的 `DAYTIME` 服务器的示例代码。

```cpp
/* TCPdtdd.cpp - main, TCPdaytimed */

#include <stdlib.h>
#include <winsock.h>
#include <time.h>
```

```cpp
void   exit(const char *, ...);
void   TCPdaytimed(SOCKET);
SOCKET passiveTCP(const char *, int);
```

```cpp
#define QLEN      5
#define WSVERS  MAKEWORD(2, 0)
```

```cpp
/*-----------
* main   用于 DAYTIME 服务的迭代式 TCP 服务器
 */
```
