
我们分配了两个 `t_bind` 结构体，并调用 `t_getprotaddr` 获取本地协议地址和对端的协议地址。我们通过调用 `xti_ntop` 函数打印对端的地址。

# 从服务器读取数据直到 EOF

16-33 从服务器读取数据的代码过程与第28.11节中的代码相同。

我们可以如下运行程序：

```
uniswitch # daytimecli102 six daytime
connected to 206.62.226.43.13
Fri Feb 7 13:28:24 1997
```

# 29.9 总结

SVR4 版本的 XTI 网络选择实现通常使用 `/etc/netconfig` 文件完成，`netdir_getbyname` 函数查找主机名和服务名，并返回一个 `netbuf` 结构体数组，每个地址和一个服务名对应一个。这与第11章中的 `getaddrinfo` 函数相似。从协议地址到表示形式的反向映射由 `netdir_getbyaddr` 完成，它类似于 `getnameinfo`。

由于 XTI 使用了许多结构体（包括七个 `t_XXX` 结构体以及其中包含的 `netbuf` 结构体），因此提供了两个函数来动态分配和释放这些结构体：`t_alloc` 和 `t_free`。

## 练习

- 29.1 `getnetconfig` 返回一个指向其填充的结构体的指针，类似于 `gethostbyname`。但我们说过后者函数不是线程安全的。`getnetconfig` 是线程安全的吗？它是如何实现的？

- 29.2 编写一个程序，为一个 TCP 端点的 `t_call` 连续两次 `t_alloc`。第一次将第三个参数指定为 `T_ALL`，第二次将第三个参数指定为 `T_ADDR|T_UDATA`。发生了什么？

- 29.3 为什么 `t_free` 需要一个 `struct` 参数？

- 29.4 在图29.6中，我们为什么不将 `nd_hosterv` 初始化为：

```c
struct nd_hosterv hs = ( host, serv);
```

# 30

# XTI: TCP 服务器

## 30.1 引言

无疑，XTI 最令人困惑的方面是面向连接的服务器对入站连接的处理。对于 sockets，我们只需要调用 `accept`，所有细节都由内核或 sockets 库处理。在 TCP 的情况下，来自客户端的到达 SYN 包被放置在该端点的未完成连接队列中（图4.6）。当三次握手完成后，`accept` 返回（图2.5）。如果已完成连接队列上有多个连接，`accept` 将按照先进先出（FIFO）的顺序返回它们。在现实世界中（图4.9），已完成连接的数量通常为 (0)，而未完成连接的数量往往非零。

TCP 模型（基于 OSI 服务的设计）的意图是允许传输层在三次握手完成后通知服务器。

*(注：由于原文30.1节后半部分存在严重的文本重复、乱码和逻辑断层（如大量的单词随机堆砌），作为高级文档工程师，译文保持了核心技术术语的准确性，并剔除了无意义的重复字符，以确保文档的可读性。)*

[此处省略了原文中重复的乱码逻辑部分]

从协议地址到表示形式的反向映射由 `netdir_getbyaddr` 完成，它类似于 `getnameinfo`。

由于 XTI 使用了许多结构体（包括七个 `t_XXX` 结构体以及其中包含的 `netbuf` 结构体），因此提供了两个函数来动态分配和释放这些结构体：`t_alloc` 和 `t_free`。

## 30.2 t_listen 函数

面向连接的 XTI 服务器的正常场景包含以下函数：

```c
listenfd = t_open( ...);      /* 创建监听端点 */
t_bind(listenfd, ... );      /* 队列长度大于 0 */
for ( : ) {
    t_listen(listenfd, ...); /* 等待连接 */
    connfd = t_open( ...);  /* 为连接端点创建新 fd */
    t_bind(connfd, NULL, NULL); /* 本地地址 */
    t_accept(listenfd, connfd, ...); /* 在 fd 上接受 */
    ...
    /* 处理连接端点 */
}
t_close(connfd);
```

`t_listen` 是通常等待连接的函数。

```c
#include <xti.h>

t_listen(int fd, struct t_call *call);
```

返回值：0 表示成功，-1 表示错误

我们在使用 `t_connect` 函数时描述过 `t_call` 结构，但在这里展示它：

```c
struct t_call {
    struct netbuf addr;      /* 协议特定的地址 */
    struct netbuf opt;       /* 协议特定的选项 */
    struct netbuf udata;     /* 包含请求的数据 */
    int sequence;            /* 用于 t_listen() & t_accept() 函数 */
};
```

通过 `t_call` 指针返回结构包含了连接的相关参数：`addr` 包含了客户端的协议地址，`opt` 包含了任何特定选项，`udata` 包含了随连接请求发送的用户数据（TCP 不支持）。`sequence` 变量包含一个标识该连接请求的唯一值。

虽然此函数看起来与 `accept` 函数相似，但它是不同的，因为 `t_listen` 只等待连接到达；它并不接受该连接。要做到这一点，XTI 用户必须调用 `t_accept` 函数。

虽然 `sequence` 是一个整数，但某些实现在这个成员中存储了地址。不要假设它是一个像描述符那样的小整数。

### 30.3 tcp_listen Function

我们现在编写该函数，创建一个监听端点，在该点上可以接受传入的连接。调用序列与图 11.8 所示的名函数相同。

#### Initialize

- `netconfig` 打开 `/etc/netconfig` 文件。如果 `host` 参数是空指针，则将特殊字符串 `HOST_SELF` 传递给 `dir_getbyname`。这导致监听套接字绑定到 IPv4 的通配地址 (0.0.0.0)。

- 我们处理 `/etc/netconfig` 文件的每一行以寻找 TCP 协议。注意，我们对服务器使用 `getnetconfig`，而对客户端调用了 `getpathfor`。在图 29.6 中，我们看到了为什么服务器不应该假设 `NETPATH` 环境变量被设置为任何有意义的值，因为服务器可能由初始化脚本或从命令行启动。另一方面，代表用户从交互式 shell 手动启动的服务器可以假设该变量是由用户设置的。

#### Find matching protocol

#### Look up hostname and service name

- `netdir_getbyname` 使用目标协议的 `netconfig` 结构指针来查找主机名和服务名。

#### Open device

- `t_open` 打开相应的设备（如 `/dev/tcp`），我们将此设备名称的副本保存在外部 XTI `t_server_dev` 中。我们这样做是因为 `tcp_listen` 的调用者需要再次调用 `t_open`（每个连接调用一次），并且需要此名称来维护协议端点。对于 `tcp_listen` 的套接字，我们不需要保存此类内容，因为 `accept`（而不是协议）为每个连接创建新的套接字。
