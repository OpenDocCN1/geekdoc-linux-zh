
默认是阻塞 I/O，这也是最常用的模型。我们将在后面的章节中介绍非阻塞 I/O 和信号驱动 I/O，在本章中讨论了 I/O 复用。真正的异步 I/O 由 `Posix.1` 定义，但实现很少。

最常用的 I/O 复用函数是 `select`。我们向函数传递感兴趣的描述符（用于读、写和异常）、等待的最大时间以及描述符编号（加1）。大多数调用 `select` 用于检查可读性，我们注意到处理套接字时唯一的异常是带外数据的到达（第 21 章）。由于我们在使用 `select` 批量模式运行回显客户端时，发现数据可能仍在管道中或服务器中。处理这种情况需要 `shutdown` 函数，它让我们能够在图 13.3 中利用此特性对输入操作设置时间限制。

### 练习

6.1 我们说在 C 中可以使用等号将一个描述符集合赋值另一个描述符集合。如果描述符是整数数组，应该如何操作？（提示：查看系统的 `<sys/select.h>` 或 `<sys/types.h>` 头文件。）

6.2 在第 6.3 节描述 `select` 返回“可写”的条件时，为什么我们需要套接字必须是非阻塞的，写入操作才能返回正值？

6.3 如果我们在第 19 行的 `if` 单词前面加上 `else`，图 6.9 会发生什么？

6.4 在图 6.21 的示例中，添加代码允许服务器可以使用内核当前允许的许多描述符。（提示：查看 `setlimit` 函数。）

6.5 让我们看看当 `shutdown` 的第二个参数为 `SHUT_RD` 时会发生什么。从图 5.4 中的 TCP 客户端开始，并进行以下更改：将端口号从 `SERV_PORT` 改为 19，即充电服务器（图 2.13）；将对 `str_cli` 的调用替换为对 `pause` 函数的调用。运行该程序并指定运行充电服务器的本地主机 IP 地址。使用 `tcpdump` 等工具（C.5 节）观察数据包。发生了什么？

6.6 应用程序会使用 `SHUT_RDWR` 作为参数调用 `shutdown` 而不是直接调用 `close`？

6.7 在图 6.22 中，当客户端发送 `RST` 来终止连接时会发生什么？

6.8 重写图 6.25 以调用 `sysconf` 来确定描述符的最大数量并据此分配客户端数组。

# 7 套接字选项

### 7.1 引言

有多种方法可以和设置影响套接字的选项：

- `getsockopt` 和 `setsockopt` 函数，
- `fcntl` 函数，以及
- `ioctl` 函数。

本章从介绍 `setsockopt` 和 `getsockopt` 函数开始，接着是一个打印所有选项默认值的示例，然后是对所有套接字选项的详细描述。我们将详细描述分为以下几类：通用（generic）、IPv4、IPv6 和 TCP。在第一次阅读本章时，可以跳过这些详细内容，在需要时再参考相关章节。稍后将详细讨论一些选项，例如 IPv4 和 IPv6 组播选项，我们将在 19.5 节中通过组播部分进行描述。

我们还会描述 `fcntl` 函数，因为它是 Posix 设置套接字用于非阻塞 I/O、信号驱动 I/O 以及设置套接字所有者的方法。我们将 `ioctl` 函数留到第 16 章介绍。

### 7.2 getsockopt 和 setsockopt 函数

这两个函数仅适用于套接字。

```c
#include <sys/socket.h>

int getsockopt(int sockfd, int level, int optname, void *opt, socklen_t *optlen);

 setsockopt(int sockfd, int level, int optname, const void *opt,
       socklen_t optlen);
```

`sockfd` 必须引用一个打开的套接字描述符。`level` 指定了系统中解释该选项的代码：通用套接字代码，或某些特定协议的代码（例如 IPv4、IPv6 或 TCP）。

`optval` 是一个变量，`setsockopt` 从从中获取选项的新值，或者 `getsockopt` 将选项的当前值存储到其中。

该变量的大小由最后一个参数指定，作为 `setsockopt` 的值以及作为 `getsockopt` 的输入-结果值。

图 7.1 总结了可以通过 `getsockopt` 查询或通过 `setsockopt` 设置的选项。“Datatype”（数据类型）列显示了每个选项指针必须指向的数据类型。我们使用双大括号符号表示结构体，例如 `{linger}` 意味着 `struct linger`。

有两种基本类型的选项：用于启用或禁用某些功能的二进制选项（标志，flags），以及获取并返回特定值的选项，我们可以设置或检查这些值（值，values）。标记为“Flag”（标志）的列指定了该选项是否为标志选项。在对这些标志选项调用 `getsockopt` 时，`optval` 是一个整数。如果选项被禁用，则 `optval` 中返回的值为零；如果选项已启用，则为非零。同样，`setsockopt` 需要一个非零的 `optval` 来开启选项，以及一个特定值来关闭选项。如果“Flag”列不包含 `*`，则该选项用于将指定数据类型的值传递给用户进程和系统。

本章的后续章节将提供影响套接字选项的更多细节。

### 7.3 检查选项是否被支持并获取默认值

我们编写一个程序来检查图 7.1 中定义的大多数选项是否被支持，如果是，则打印它们的默认值。图 7.2 包含了我们程序的声明。

### 检查选项是否支持并获取默认值

| level | optname | get | set | Description | Flag | Datatype |
|---|---|---|---|---|---|---|
| SOL_SOCKET | SO_BROADCAST | | * | 允许发送广播数据报 | * | int |
| | SO_DEBUG | | * | 启用调试路由表 | * | int |
| | SO_SNDROUTE | | * | 传递错误和关闭 | * | int |
| | SO_KEEPALIVE | | * | 定期测试连接是否存活 | * | int |
| | SO_LINGER | | * | 如果发送了数据则关闭时停留 | * | linger |
| | SO_SNDINLINE | | * | 内联接收带外数据 | * | int |
| | SO_RCVBUF | | * | 接收缓冲区大小 | * | int |
| | SO_SNDBUF | | * | 发送缓冲区大小 | * | int |
| | SO_RCVLOWMARK | | * | 发送低水位 | * | int |
| | SO_RCVTIMEO | | * | 接收超时 | * | timeval() |
| | SO_SNDTIMEO | | * | 允许地址重用 | * | int |
| | SO_REUSEADDR | | * | 允许地址重用 | * | int |
| | SO_REUSEPORT | | * | 获取套接字类型 | * | int |
| | SO_USEBACKACK | | * | 路由器获取其发送的内容 | * | int |
| IPPROTO_IP | IP_HDRIN | | * | 数据包含 IP 头部 | * | int |
| | IP_OPTION | | * | IP 选项 | * | (见文本) |
| | IP_RECVDSTADDR | | * | 返回目标 IP 地址 | * | int |
| | IP_RECVID | | * | 返回接口地址 | * | int |
| | IP_TTL | | * | 生存 | * | int |
| | IP_MULTICAST_IP | | * | 指定接口 | * | in_addr() |
| | IP_MULTICAST_TTL | | * | 指定 TTL | * | u_char |
| | IP_MULTICAST_LOOP | | * | 加入组播 | * | u_char |
| | IP_ADD_MEMBERSHIP | | * | 离开组播 | * | ip_mreq() |
| IPPROTO_IPV6 | ICMP6_FILTER | | * | 指定消息类型 | * | icmp_filter() |
| IPPROTO_IPV6 | IP6_ADCSUM | | * | 更改套接字地址格式 | * | int |
| | IP6_DESTOPS | | * | 原始套接字校验和偏移 | * | int |
| | IP6_HOPLIMIT | | * | 接收单播跳限制 | * | int |
| | IP6_HOPPOPT | | * | 接收下一跳限制 | * | int |
| | IP6_NEXTHDR | | * | 指定下一跳地址 | * | sockaddr() |
| | IP6_PKTINFO | | * | 接收数据包信息 | * | int |
