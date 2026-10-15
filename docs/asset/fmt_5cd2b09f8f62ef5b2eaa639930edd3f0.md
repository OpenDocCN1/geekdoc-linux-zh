
```c
ssize_t
readline(int fd, void *vptr, size_t maxlen)
{
    size_t n, rc;
    char c, *ptr;

    ptr = vptr;
    for (n = 1; n < maxlen; n++) {
        if ((rc = read(fd, &c, 1)) == 1) {
            *ptr++ = c;
            if (c == '\n')
                break;
        } else if (c == 0) {
            if (n == 1)
                return (0); /* EOF，未读到数据 */
        } else {
            break; /* EOF，读取了部分数据 */
        }
    } else {
        if (errno == EINTR)
            goto error;
        return (-1); /* 错误，errno 由 read() 设置 */
    }
    *ptr = 0; /* 像 fgets() 一样空空终止 */
    return (n);
}
error:
```

图 3.17 `readline` 的更好的版本。

### 3.10 `isfdtype` 函数

有时我们需要测试描述符是否为特定类型 `socket`。在历史上，这是通过调用 `fstat` 并测试返回的 `st_mode` 值实现的（我们在 3.8 节讨论过）。许多实现 `fstat` 不支持套接字。

```c
#include <sys/stat.h>

int isfdtype(int fd, int ftype); /* 返回：如果是 socket 返回1，不是则返回0，错误返回-1 */
```

图 3.18 显示使用 `fstat` 的 `isfdtype`。

### 套接字简介

```c
#include "unp.h"

#ifndef EINTR
#error EINTR 未定义
#endif

int
isfdtype(int fd, int ftype)
{
    struct stat buf;

    if (fstat(fd, &buf) < 0)
        return (-1);

    if (buf.st_mode & ftype)
        return (1);
    else
        return (0);
}
```

### 3.11 总结

套接字结构是每个网络不可或的一部分。有时我们填充它们并传递它们的指针。套接字结构是自定义的，因为它们总是以一个标识地址的字段（`family`）开始。支持变长地址结构的现代实现还包含一个长度字段。

将 IP 地址在表示格式（我们写的 ASCII 字符）和数值格式（进入套接字结构的数据）之间转换的两个函数是 `inet_pton` 和 `inet_ntop`。我们在后续章节中使用这两个函数，但它们依赖于协议。更好的技术是将套接字结构视为不透明对象，只需结构指针和其大小，我们开发了一套帮助程序协议独立的 `sock` 函数。

TCP 套接字为应用程序提供字节流；没有记录标记。`read` 的返回值可能少于我们请求的值，但这并不表示错误。为了帮助读取和写入字节流，我们开发了三个函数 `readn`、`writn` 和 `readline`，我们在全文中使用了它们。

### 练习题

-3.1 为什么套接字结构的长度等值结果参数必须通过引用传递？

-3.2 为什么 `read` 和 `write` 函数不将 `void*` 指针拷贝到 `char*` 指针？

-3.3 `inet_aton` 和 `inet_addr` 函数传统上对接受的点点表示法 IPv4 地址字符串非常宽容；允许一到四个由小数点分隔的数字，并允许以 0 开头的十六进制数，或以 0 开头的八进制数（通过 `telnet` 显示了这种行为）。`inet_pton` 对 IPv4 地址要严格得多：编写一个名为 `inet_pton` 的新函数来处理这些情况：如果地址族是 `AF_INET` 且 `inet_pton` 返回，调用 `inet_aton` 并检查是否成功。同样，如果地址族是 `AF_INET6` 且 `inet_pton` 返回 0，调用 `inet_aton` 如果成功，则返回 IPv4 映射的 IPv6 地址。

## 4. 基础 TCP 套接

### 4.1 介绍

本章描述了编写一个完整的 TCP 客户端和服务器所需的的基础套接函数。我们首先描述将用到的所有基础套接函数，然后在下一章中开发客户端和服务器。我们将在整个文中一直使用这个客户端和服务器，并对其进行多次增强（图 1.12 和图 1.13）。

我们还描述了并发服务器，这是一种常用的 Unix 技术，用于在大量客户端同时连接到同一个服务器时提供并发支持。每个客户端连接都会导致服务器为该客户端派生（`fork`）一个新进程。在本章中，我们只考虑使用 `fork` 的“每个客户端一个进程”模型，但在第 23 章描述线程时，我们会考虑另一种“每个客户端一个线程”的模型。

图 4.1 显示了 TCP 客户端和服务器之间发生典型场景的时间线。首先启动服务器，然后在此某个时刻启动一个客户端并连接到服务器。我们假设客户端向服务器发送请求，服务器处理请求，并向客户端发送回复。这一过程一直持续，直到客户端关闭其连接端，这会向服务器发送一个文件结束（EOF）通知。服务器随后关闭其连接端，并终止或等待新的客户端连接。

### 4.2 `socket` 函数

为了执行网络 I/O，进程必须完成的第一件事是调用 `socket` 函数，指定所需的通信协议类型（使用 IPv4 的 TCP、使用 IPv6 的 UDP、Unix 域流协议等）。

### TCP 服务器

![](img/aeda3be9ee318bedd42850d461da0f28_98_0.png)

图 4.1 用于基础 TCP 客户端-服务器的套接字函数。

```c
#include <sys/socket.h>

int socket(int family, int type, int protocol):

    返回：成功则返回非负描述符，出错时返回 -1
```

`family` 指定协议族，是图 4.2 所示常量之一。套接字类型是图 4.3 所示的常量之一。通常情况下，`socket()` 函数的 `protocol` 参数设置为 0，原始套接字（`raw sockets`）除外。我们将在第 25 章讨论这些内容。

并不是所有的套接字族和类型组合都是有效的。图 4.4 显示了有效的组合，以及由该组合选择的实际协议。标记为“Yes”的框是有效的，但没有许多缩写。空白框表示不支持。

| family | 描述 |

|--- | :--- |

| `AF_INET` | IPv4 协议 |

| `AF_INET6` | IPv6 协议 |

| `AF_LOCAL` | Unix 域协议（第 14 章） |

| `AF_ROUTE` | 路由套接字（第 17 章） |

| `AF_KEY` | 密钥套接字 |

图 4.2 用于 `socket` 的协议族常量。

| type | 描述 |

|--- | :--- |

| `SOCK_STREAM` | 流套接字 |

| `SOCK_DGRAM` | 数据报套接字 |

| `SOCK_RAW` | 原始套接字 |

图 4.3 `socket` 函数的套接字类型。

| `AF_INET` | `AF_INET6` | `AF_LOCAL` | `AF_ROUTE` | `AF_KEY` |

| --- | --- | --- | --- | --- |

| `SOCK_STREAM` | TCP | TCP | | |

| `SOCK_DGRAM` | UDP | UDP | Yes | |

| `SOCK_RAW` | IPv4 | IPv6 | Yes | Yes |

图 4.4 `socket` 函数的族和类型组合。

你可能在 `socket` 的第一个参数中遇到相应的 `AF_xxx`。我们将在本节末尾详细介绍这一点。

我们注到，你可能会遇到 `AF_UNIX`（历史上的 Unix 名称）而不是 `AF_LOCAL`（Posix 命名），我们将在第 14 章中详细介绍这一点。

`family` 和 `type` 参数还有其他值。例如，4BSD 同时支持 `AF_NS`（Xerox NS 协议，通常称为 XNS）和 `AF_IS150`（OSI 协议）。但今天很少有人使用这两种协议中的任何一种。同样，`SOCK_SEQPACKET`（顺序包套接字）类型也由 Xerox NS 协议和 OSI 协议实现。但 TCP 是字节流，只支持 `SOCK_STREAM` 套接字。

Linux 支持一种新的套接字类型 `SOCK_PACKET`，它提供了对数据链路的访问，类似于图 2.1 中的 BPF 和 DLPI。我们将在第 26 章中详细介绍这一点。
