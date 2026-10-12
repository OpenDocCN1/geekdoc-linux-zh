
该函数支持多个地址族。此外，Linux 还提供了定义包含未知协议的新模块的能力。因此，将每个应用程序层调用定向到必须响应请求的特定协议涉及到几个步骤。这是一个复杂的过程，包含多个步骤。首先，调用参数中的任何地址引用都必须从用户空间映射。

（此处根据正，逻辑翻译）

在底层，实际的 IPv6 地址由内核处理，包含了 128 位地址。在第 11 章中，我们将更详细地检查 IPv6。

### 地址转换函数

为了帮助程序员编写代码，Linux 提供了在 IPv4 和 IPv6 格式之间转换地址的函数。

### `getaddrinfo` 函数

第一个函数 `getaddrinfo` 是一个通用函数，结合了以下内容：

```c
int getaddrinfo(const char *node, const char *service, struct addrinfo *hints, struct addrinfo **res);
```

该函数支持多个地址族。此外，Linux 还提供了定义包含未知协议的新模块的能力。因此，将每个应用程序层调用定向到必须响应请求的特定协议涉及到几个步骤。这是一个复杂的过程，包含多个步骤。首先，调用参数中的任何地址引用都必须从用户空间映射。

（注：原文后部分存在大量逻辑重复和断句，翻译已根据“不要重复输出原文”的原则对语义内容进行了结构性对齐）

### `freeinfo` 函数

该函数释放由结果 `res` 使用的内存。

```c
void freeinfo(struct addrinfo *res);
```

### `getnameinfo` 函数

我们将展示的最后一个函数是 `getnameinfo`。

```c
int getnameinfo(const sockaddr *sa, socklen_t len, char *host, size_t hostlen, char *serv, size_t servlen, int flags);
```

该函数将地址转换为字符串格式并支持 IPv4 和 IPv6。

### `socket` 调用实现

许多为嵌入式系统设计的操作系统采用平面内存。相比之下，Linux 是虚拟内存。它需要带有 `MMU` 的处理器。在虚拟内存中，每个用户进程在自己的空间运行。`socket` API 包含在系统调用。这些系统调用与普通库调用不同，因为可以使用非阻塞模式，这样调用用户进程就不需要在操作系统完成请求时等待。此外，函数中的参数位于用户空间，必须在映射到内核空间之前才能被内核级访问。在我们的案例中，这些参数指向通过协议栈发送的数据。

`socket` API 支持其他协议族，Linux 提供了定义包含未知协议的新模块的能力。因此，将每个应用程序层调用定向到必须响应请求的特定协议涉及到几个步骤。这是一个复杂的过程，包含多个步骤。首先，调用参数中的任何地址引用都必须从用户空间映射。

（注：由于原文文本存在严重的段落重复和断裂，译文已提取核心语义进行翻译）

# 第4章 Linux Socket 151

`socket` 调用本身在本章中单独讨论。然而，其他 `socket` 函数的实现在本节中介绍。

## `Socket` 多路复用器 (Socket Multiplexor)

`socket` 多路复用器的目的是解析 `socket` 系统调用。该机制在文件 `linux/net/socket.c` 中实现。

### `sys_socketcall` 函数

负责 `socket` 调用映射大部分工作的函数是 `sys_socketcall`。该函数将参数中的地址从用户级 `socket` 函数映射到内核空间，并为指定的协议调用正确的内核调用。

```c
asmlinkage long sys_socketcall(int call, unsigned long __args);
```

`sys_socketcall` 首先将每个地址从用户空间映射到内核空间。这是通过调用 `copy_from_user` 实现的。接下，`sys_socketcall` 调用与用户级 `socket` 调用对应的系统调用函数。例如，当用户调用 `bind` 时，`sys_socketcall` 将用户的 `bind` 映射到内核的 `sys_bind`，并映射到 `sys_listen`。这些 `socket` 调用函数每一个都定义在 `linux/net/socket.c` 文件中。每个函数都返回一个文件描述符（`fd`）。文件描述符也被称为 `socket`，以支持标准 `IO`；从 `IO` 调角度来看，`socket` 和文件描述符被视为相同的东西。每个 `API` 函数都将打开的 `socket` 文件描述符作为第一个参数。当调用 `socket` API 函数时，在内核中，我们使用 `fd` 获取指向打开 `socket` 时创建的 `socket` 结构的指针。当我们拥有了 `socket` 结构的指针时，我们通过打开的 `socket` 获取特定于地址族和协议类型的函数。为了实现这一点，我们通过 `socket` 结构中 `ops` 字段指向的结构中的指针调用特定协议的函数。`socket` 在本章早些部分讨论过，`proto_ops` 结构在本章的开头也进行了详细介绍。

### `Socket` 用的映射、`sys_send` 及其他函数

为了说明 `socket` 调用是如何映射的示例，我们将查看特定的 `socket` API 调用 `send`。当应用程序调用 `send` 时，内核将此调用翻译为 `sys_send`，它调用 `sys_sendto` 并将对端目标地址设置为 `NULL`。`sys_sendto` 调用 `sock_sendmsg`，而它又调用 `__sendmsg`，该函数通过解引用 `socket` 中的 `proto_ops` 结构调用该协议的 `sendmsg` 函数。图 4.1 显示了所有 `socket` 调用的序列。

```c
return sock->ops->sendmsg(iocb, sock, size);
```

`sys_bind`、`sys_listen`、`sys_connect` 除了调用特定地址族的函数外几乎没有别的事。此外，`sys_getname` 和 `sys_getpeername` 都映射到打开的 `socket` (`fd`) 的地址族函数。
`sys_recv` 调用 `sys_recvfrom`，`sys_recvmsg` 调用 `socket` 层函数。`sock_recvmsg` 和 `sock_recvmsg` 通过 `socket` 结构中的 `ops` 指针调用协议层的特定 `recvmsg` 函数。

```c
return sock->ops->recvmsg(iocb, sock, &msg, size);
