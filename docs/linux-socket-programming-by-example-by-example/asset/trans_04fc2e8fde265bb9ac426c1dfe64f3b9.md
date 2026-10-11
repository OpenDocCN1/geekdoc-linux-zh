

## 清单 11.6：续

```
0:
=
0:34786999960711639
~]
telnet> c
Connection closed.
$
```

第二个示例 `telnet` 会话显示在清单 11.7 中。请记住，这些只是示例会话。您可以自由测试 RPN 服务器的任何功能。

## 清单 11.7：与 rpnsrv2 的第二次会话

```
$ telnet localhost 9099
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
#:99
0:
genprime
0:
=
0:30392223729873609
~]
telnet> c
Connection closed.
$
```

当清单 11.6 和 11.7 中的会话正在进行时，在第三个会话中生成了一份进程列表，如清单 11.8 所示。

## 清单 11.8：访问 rpnsrv2 期间的进程列表

```
$ ps -af

    PID   PPID         C STIME TTY          TIME CMD
www     730    629     0 21:51 pts/1      00:00:00 ./rpnrsrv2 *:9099
www     731    629     0 21:53 pts/1      00:00:00 telnet localhost 9099
www     754    752     0 21:59 pts/5      00:00:00 telnet localhost 9099
www     757    665     0 21:59 pts/5      00:00:00 ps -af
$
```

清单 11.8 中的进程列表清楚地表明，当两个 `telnet` 会话（PID 731 和 754）连接到 rpnsrv2 进程时，只有一个代表服务器的进程（PID 730）。每当在 `telnet` 会话中输入一行数据时，只需在两个打开的会话中的任意一个中按下回车键，即可收到响应。这证明了一个进程服务多个连接客户端的能力。

## 示例的局限性

前面提到，此服务器示例仅使用了读取事件。即使接受演示服务器的这一局限性，如果某个不守规矩的客户端程序决定搞破坏，仍然存在一些困难的风险。

考虑如果一个客户端进程执行以下操作会发生什么：

1. 发送三个字节：`'#'`、`':'` 和 `'9'`。
2. 等待很长时间或不确定的时间。

服务器端将经历以下事件：

1. 服务器套接字的接收端会收到来自客户端的三个字节。
2. `select(2)` 调用将返回，指示客户端套接字有数据可读。
3. `fgets(3)` 函数最终将在清单 11.5 的第 90 行被调用。
4. `fgets(3)` 函数将无限期等待，因为读取所有可用数据后，没有换行符表示行尾已收到。

此时，服务器阻塞在 `fgets(3)` 调用中，现在其他客户端也将无法得到服务（它们看起来都将连接挂起）。

上述讨论表明，虽然 `select(2)` 使一个进程能够处理多个套接字，但为了避免挂起，服务器设计往往倾向于复杂化。

操作侧的写入同样复杂。虽然 `select(2)` 调用可以指示何时 `write(2)` 调用不会阻塞，但它并不指示在不阻塞的情况下可以写入多少数据。对于可能在响应中返回大量数据的服务器，这是一个严重问题。同样，必须应用特殊的缓冲技术才能成功地在健壮的服务器进程中使用 `select(2)`。

## 接下来是什么

本章涵盖了许多服务器设计概念。在章节的前半部分，你看到了 fork(2) 和独立进程如何并发处理多个客户端连接。select(2) 函数展示了它如何在一个服务器进程中服务多个客户端。

下一章将带你了解套接字选项。在那里，你将学习如何启用套接字广播、复用套接字地址、开启 TCP/IP “保持活动” 功能等等。

# 12
## 套接字选项

在福特 T 型车的全盛时期，据说你可以选择任何颜色，只要它是黑色的。这显然是在嘲笑没有选择余地的观点。幸运的是，套接字并不那么 restrictive！

前面的章节涵盖了使用套接字的基础知识。现在适合考察一些可用的可选功能。掌握本章的概念后，你将为书中其余部分涵盖的更高级的套接字主题做好准备。本章将重点讨论以下主题：

- 如何使用 getsockopt(2) 检索套接字选项值
- 如何使用 setsockopt(2) 更改套接字选项值
- 如何应用最常用的一些套接字选项

## 获取套接字选项

通常，应用程序需要确定套接字的当前选项设置。这对于子程序库函数尤其如此，这些函数对于作为参数传递给它的套接字之前发生了什么一无所知。应用程序可能还需要知道诸如系统默认值决定的最佳缓冲区大小等信息。

允许你检查套接字选项值的函数是 **getsockopt(2)** 函数。其函数原语如下所示：

```c
#include <sys/types.h>
#include <sys/socket.h>

int getsockopt(int s,
               int level,
               int optname,
               void *optval,
               socklen_t *optlen);
```

五个参数描述如下：

1. 要检查选项的套接字 *s*。
2. 要检查选项的协议 *level*。
3. 要检查的选项 *optname*。
4. 指向选项值接收缓冲区的指针 *optval*。
5. 指向输入缓冲区长度和返回选项长度值的指针 *optlen*。

此函数的返回值在成功时返回零。当发生错误时，返回 −1，外部变量 *errno* 包含错误的性质。

协议 *level* 参数指示你希望在协议堆栈的哪个位置访问选项。通常，你会使用以下其中之一：

- **SOL_SOCKET** 以访问套接字层选项
- **SOL_TCP** 以访问 TCP 层选项

本章的讨论将严格限于 **SOL_SOCKET** 层选项的使用。

*optname* 参数是一个整数值。此处使用的值首先由 *level* 参数值的选择决定。在指定的协议层内，*optname* 参数将决定你要访问哪个选项。表 12.1 展示了一些可能的层级和选项组合。

### 表 12.1：协议层级和选项名称

| 协议层级 | 选项名称 |
| :--- | :--- |
| SOL_SOCKET | SO_REUSEADDR |
| SOL_SOCKET | SO_KEEPALIVE |
| SOL_SOCKET | SO_LINGER |
| SOL_SOCKET | SO_BROADCAST |
| SOL_SOCKET | SO_OOBINLINE |
| SOL_SOCKET | SO_SNDBUF |
| SOL_SOCKET | SO_RCVBUF |
| SOL_SOCKET | SO_TYPE |
| SOL_SOCKET | SO_ERROR |
| SOL_TCP | SO_NODELAY |

表中列出的大多数选项是套接字层选项，其层级指定为 SOL_SOCKET。为了比较目的，包含了一个 TCP 层套接字选项，其层级指定为 SOL_TCP。

许多套接字选项检索到 int 数据类型。查看手册页时，除非另有说明，通常可以假设为 int 数据类型。当使用布尔值时，int 值非零时表示 TRUE，为零时表示 FALSE。

## 应用 getsockopt(2)

在本节中，你将编译并运行程序 getsndrcv.c，该程序将获取并报告套接字的发送和接收缓冲区大小。清单 12.1 中的示例说明了代码。

![](img/961a0296fe36074690a9847b79332eff_324_0.png)

```c
1: /* getsndrcv.c—Get and Report SO_SNDBUF and SO_RCVBUF Options
2:    */
3:    /* Get SO_SNDBUF & SO_RCVBUF Options:
4:    */
5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <errno.h>
9: #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12: #include <assert.h>
```

