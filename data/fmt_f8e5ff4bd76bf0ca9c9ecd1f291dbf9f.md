
> 图 10.7 将 IPv4 套接字转换为 IPv6

对 `setsockopt` 的调用将套接字的地址格式从 IPv4 更改为 IPv6，`getpeername` 返回一个 IPv4 映射的 IPv6 地址，假设该套接字是 IPv4 套接字。如果此程序使用 IPv6 套接字输入，则对 `setsockopt` 的调用将不起作用，因为地址格式已经是 IPv6。当接受传入 IPv4 连接的程序由他人提供时，可以使用 `getsockopt` 的场景（即我们没有源代码来修改程序以使用 IPv6，或者最好与协议无关），但我们执行的程序处理 IPv6 连接。如果为 `IPV6_ADDR` 调用 `getsockopt`，返回的值是 `AF_INET` 或 `AF_INET6`，取决于套接字的地址格式。

## 10.6 源代码的可移植性

大多数现有网络应用程序都使用 IPv4，`sockaddr_in` 结构在调用 `socket AF_INET` 时作为第一个参数被分配并填充的。我们从图 1.5 到图 1.6 的转换中看到，这些 IPv4 应用不需要费太大精力就可以转换为 IPv6。我们展示的许多更改可以使用某些编辑脚本自动完成。而更依赖 IPv6 的程序（例如多组播、IP 选项或原始套字等功能）则需要更多工作来转换。

如果我们将一个应用程序转换为 IPv6 并以源代码的形式分发，就不需要担心接收者的系统是否支持 IPv6。处理这种情况的典型方法是在整个代码中使用 `#ifdef`，尽可能使用 IPv6（因为我们已经看到 IPv6 客户端仍然可以与 IPv4 服务器通信，反之亦然）。这种方法的问题是代码会迅速充斥大量的 `#ifdef`，变得更加难以维护。

更好的方法是将转换为 IPv6 作为一个让程序实现协议无关的机会。第一步是移除对下一章描述的 `gethostnameby`、`getaddrinfo` 和 `getname` 函数的调用。这允许我们将套接字视为对象，通过指针和大小进行引用，这正是基础套接字函数所做的：`bind`、`connect`、`recvfrom` 等。我们在第 3.8 节中的 `sock_XXX` 函数可以帮助操作这些内容，且独立于 IPv4 或 IPv6。显然，这些函数包含了处理 IPv4 和 IPv6 的 `#ifdef`，但将所有协议依赖隐藏在几个库函数中使得我们的代码更加简单。我们在第 19.6 节开发了一系列大多数 XXX 函数，可以使 IPv4 或 IPv6 应用程序更容易。

另一个需要考虑的点是，如果在同时支持 IPv4 和 IPv6 的系统上使用源码，发布每个可执行文件或对象文件（而不只是源码），并在不支持 IPv6 的系统上运行程序会发生什么？本地域名服务器可能会支持 AAAA 记录，并为应用程序尝试连接的对端返回 A 和 AAAA 记录。如果我们的应用程序支持 IPv6，并调用 `socket` 创建 IPv6 套接字，如果主机不支持 IPv6，它将失败。我们在下一章描述的函数处理了这个问题：通过忽略来自 `socket` 的错误并尝试域名服务器返回的列表中的地址。假设对端有记录，且域名服务器返回了 A 记录，则 IPv4 套接字的创建将成功。这种功能属于库函数，而不是每个应用程序的源码。

## 10.7 总结

双栈主机上的 IPv6 服务器可以同时为 IPv4 客户端和 IPv6 客户端提供服务。IPv4 客户端仍然向服务器发送 IPv4 数据报文，但服务器的协议栈会将客户端的地址转换为 IPv4 映射的 IPv6 地址，因为 IPv6 服务器处理的是 IPv6 地址结构。

同样，双栈主机上的 IPv6 客户端可以与 IPv4 服务器通信。客户端的解析器将为服务器的所有 A 记录返回 IPv4 映射的 IPv6 地址，在双栈环境下，为这些地址中的每一个地址调用 `connect`，并结合对端使用的 IPv4 SYN 段（例如 FTP）以及使用 `IN6_IS_ADDR_VAPPED` 宏，可以判断对端是否正在使用 IPv4。`IPv6_ADDRVFORM` 套接字选项可以被期望某种类型套接字（通常是 IPv6 套接字）的程序使用。

### 练习题

- 1. 在运行 IPv4 和 IPv6 的双栈主机上启动一个 IPv6 FTP 客户端。连接到 IPv4 FTP 服务器，发出 `debug` 命令，然后执行 `dir` 命令。对 IPv4 服务器执行相同的操作，并比较因 `dir` 命令而产生的 `PORT` 命令。
- 2. 编写一个需要一个命令行参数的程序，该参数为 IPv4 点进制地址。创建一个 IPv4 TCP 套接字，并将该地址与某个端口（例如 8888）绑定到套接字。调用 `listen` 然后暂停。编写一个类似的程序，接受 IPv6 十进制字符串作为参数，并创建一个 IPv6 TCP 套接字。`SO_REUSEADDR` 套接字选项会有区别吗？如果你先启动 IPv6 程序，然后再尝试启动 IPv4 程序会怎样？

![](img/aeda3be9ee318bedd42850d461da0f28_279_0.png)

## 11 高级主机名与地址转换

### 11.1 引言

第 9 章描述的两个函数 `gethostbyname` 和 `gethostbyaddr` 是依赖协议的。使用前者时，我们必须知道将结果移动到套接字地址结构的哪个成员（例如 IPv4 的 `sin_addr` 成员或 IPv6 的 `sin6_addr` 成员），当调用后者时，我们必须知道哪个成员包含二进制地址。本章从新的 Posix.1 `getaddrinfo` 函数开始，它为我们的应用程序提供了协议无关性。我们在章后面介绍了它的补充函数 `getnameinfo`。

我们使用这些函数开发自己的函数，来处理 TCP 和 UDP 客户端和服务器的典型场景。在本文其余部分，我们将不再直接调用 `getaddrinfo`。

`gethostbyname` 和 `gethostbyaddr` 函数也是非重入函数的示例。我们展示了原因并描述了一些替换函数。我们在本章结束处展示了 `getaddrinfo` 的完整实现、它的工作方式、返回值以及与 IPv6 的交互。

### 11.2 getaddrinfo 函数

`getaddrinfo` 函数隐藏了库中所有的协议依赖。它定义在 Posix.1 中。

该定义源于 Marshall Rose 向 X/Open 提出的名为 `getconninfo` 的早期提案。

```c
#include <netdb.h>

int getaddrinfo(const char *hostname, const char *service,
                const struct addrinfo *hints, struct addrinfo **result);
```
返回值：成功返回 0，错误返回非零（见图 11.3）

该函数通过 `result` 指针返回指向 `addrinfo` 结构列表的指针，定义在 `<netdb.h>`。

```c
struct addrinfo {
    int ai_flags;
    int ai_family;
    int ai_socktype;
    int ai_protocol;
    size_t ai_addrlen;
    char *ai_hostname;
    struct sockaddr *ai_addr;
    struct addrinfo *ai_next;
};
```
