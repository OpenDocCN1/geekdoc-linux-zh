

## 示例 4.1

```c
#define AF_UNIX PF_UNIX
#define AF_FILE PF_FILE
#define AF_INET PF_INET
#define AF_AX25 PF_AX25
#define AF_IPX PF_IPX
#define AF_APPLETALK PF_APPLETALK
#define AF_NETROM PF_NETROM
#define AF_BRIDGE PF_BRIDGE
#define AF_ATMSVC PF_ATMSVC
#define AF_X25 PF_X25
#define AF_INET6 PF_INET6
#define AF_ROSE PF_ROSE
#define AF_DECnet PF_DECnet
#define AF_NETBEUI PF_NETBEUI
#define AF_SECURITY PF_SECURITY
#define PF_KEY PF_KEY
#define pseudo_AF_KEY PF_KEY
#define AF_NETLINK PF_NETLINK
#define AF_ROUTE PF_ROUTE
#define AF_PACKET PF_PACKET
#define AF_ASH PF_ASH
#define AF_ECONET PF_ECONET
#define AF_ATMSVC PF_ATMSVC
#define AF_SNA PF_SNA
#define AF_IRDA PF_IRDA
#define AF_MAX PF_MAX
```

示例 4.1 说明了另一个有趣的事实。请注意，在大多数情况下，`PF_` 系列宏是用 `AF_` 系列宏常量来定义的。前面曾提到，`AF_` 常量与 `PF_` 常量是等价的，尽管未来这种情况可能不一定总是成立。

无论如何，示例 4.1 展示了大量的协议族。然而，并非所有这些协议族都得到了支持。有些是为将来使用而定义的，另一些则处于开发阶段。在几乎所有情况下，你需要确保内核已编译支持你想要使用的协议族。

**注意**
在使用某些协议族之前，必须确保内核已编译了相应的支持。许多非主流协议通常不会包含在标准发行版的内核中。

**警告**
Linux 中的一些协议实现仍处于开发阶段，使用它们可能会导致内核崩溃。因此，你应该采取备份措施，或者在一台即使崩溃也无所谓的主机上测试新的协议选项。

## 发现套接字类型

在尝试创建非主流套接字时，了解协议族只是战斗的一部分。你现在需要了解你所选择的协议族支持的套接字类型。通常可以使用以下简单步骤来完成：

1.  切换到 Linux 内核源代码目录（你可能需要先安装它）。例如，你可能需要执行 `cd /usr/linux/src`。
2.  切换到 Linux 网络源代码子目录。例如，你要执行 `cd ../net` 以切换到该子目录。
3.  使用命令 `ls -F` 列出目录内容。这将使子目录在其名称后显示一个尾随的 `/`（斜杠）。
4.  通常，子目录的名称会指示你可能感兴趣的协议。切换到该子目录（例如，`cd ipx`）。
5.  执行 grep 命令，查找以 `SOCK_` 开头的内容。

通常，这就足以列出你想知道的套接字类型。示例 4.2 展示了遵循这些步骤的会话示例。

### 示例 4.2：列出协议族支持的套接字类型

```bash
$ cd /usr/src/linux
$ cd ../net
$ ls -F
802/
Changes
Config.in
Makefile
README
TUNABLE
appletalk/
ax25/
bridge/
core/
decnet/
ethernet/
ip/
ipx/
irda/
lppb/
netlink/
netrom/
netsyms.c
netsyms.o
network.a
packet/
protocols.o
protocols.c
rose/
sched/
sock_n_syms.o
socket.c
socket.o
sunrpc/
sysctl_net.c
sysctl_net.o
unix/
wanrouter/
x25/
$ cd ipx
$ ls -F
Config.in af_ipx.c sysctl_net_ipx.c
Makefile af_spx.c
$ grep SOCK _ .c
af_ipx.c: s->state, SOCK_INODE(s)->socket)->_i_uid);
af_ipx.c: case SOCK_DGRAM:
af_ipx.c: case SOCK_SEQPACKET:
af_spx.c: case SOCK_STREAM: /* Allow higher levels to piggyback */
af_spx.c: if(sock->type == SOCK_DGRAM)
af_spx.c: SOCK_DEBUG(sk,)
af_1px.c:            SOCK_DEBUG(sk,
af_1px.c:                "SOCK_DEBUG: %s: %s: bind failed because port %X in use.\n",
af_1px.c:                SOCK_DEBUG(sk, "IPX: bound socket 0x%04X.\n");
af_1px.c:            if(sock->type == SOCK_DGRAM )
af_1px.c:                case SOCK_SEGPACKET:
af_1px.c:            if(sock->type != SOCK_SEGPACKET)
af_1px.c:            if(sock->type != SOCK_SEGPACKET)
af_1px.c: /* route socket(PF_IPX,SOCK_SEGPACKET) calls through spx_create() */
```

从示例 4.2 中显示的 grep 输出中，你可以立即看到可能支持套接字类型 `SOCK_DGRAM` 和 `SOCK_STREAM`（为了确定，你需要查看代码逻辑）。在末尾，还出现了对 `SOCK_SEGPACKET` 的引用，这表明它可能也受到支持。

另一个有趣的点是，你知道你可能需要查阅文件 `af_ipx.c` 中的注释和说明。有时，注释对于了解什么受到支持、什么不受支持很有用。

### 接下来是什么

在本章中，你仔细研究了 `socket(2)` 函数调用。本章中包含的额外理论层次和细节是必要的，因为很多内容都取决于你在 `socket(2)` 调用中做出的选择。有了对 `socket(2)` 函数的这种实际了解，你就在让套接字发挥作用方面取得了良好进展。

下一章将主要转向 `bind(2)` 函数调用。这个函数很重要，因为它允许你为在本章中你学会了如何创建的套接字分配地址。

# 将地址绑定到套接字

前面的章节为你提供了创建套接字和形成地址的手段。本章将在此基础上进行扩展，使你能理解 `bind(2)` 如何工作以及如何正确应用它。

在本章中，你将了解

- `bind(2)` 函数调用如何为套接字分配地址
- 如何从已有地址的套接字中获取本地套接字地址
- 如何获取对端套接字地址
- `bind(2)` 如何为通信选择所使用的网络接口

第 2 章“域和地址族”详细讲述了地址。这些背景知识将使本章内容对你来说易于理解。掌握了 `bind` 函数后，你将在下一章中能够开始让套接字发挥作用。

## bind(2) 函数的用途

当你的套接字由 `socket(2)` 函数创建时，它是没有名称的。你在第 1 章“介绍套接字”中看到，当演示 `socketpair(2)` 函数时，套接字可以在没有地址的情况下使用。然而，这之所以可行，是因为这些套接字是在同一个 Linux 内核内部以这种方式创建的。对于必须连接两个不同主机的套接字，这是做不到的。

一个没有名称的套接字很难使用。没有人能向你的无名套接字发送信息，因为它就像一部没有电话号码的电话。因此，程序员必须将名称绑定到套接字，以便他人可以访问它。这就像给新电话分配一个电话号码，以便可以被呼叫。`bind(2)` 函数允许你以相同的方式为套接字分配地址。

在本章的上下文中，“名称”与 sunsite.unc.edu 之类的主机名没有任何关系。在讨论 `bind(2)` 函数时，经常使用“名称”一词，它指的是套接字的地址。毕竟，地址在某种程度上也是一种名称。然而，为了避免混淆，本章将优先使用“地址”这一术语。

## 使用 bind(2) 函数

`bind(2)` 函数的目的是为一个没有名称的套接字分配套接字地址。函数原型如下所示：

```c
#include <sys/types.h>
#include <sys/socket.h>

int bind(int sockfd, struct sockaddr *my_addr, int addrlen);
```

该函数接受以下三个输入参数：

1.  由先前 `socket(2)` 调用返回的套接字 `sockfd` 文件描述符。
2.  要分配给套接字的地址 `my_addr`。
3.  地址 `my_addr` 的字节长度（参数 `addrlen`）。

如果成功，该函数返回零值。否则，返回 -1，并且变量 `errno` 会被设置为失败的原因。

**注意**
提供给 `bind(2)` 的套接字必须当前是没有名称的（没有地址）。你不能将套接字重新绑定到一个新地址。

