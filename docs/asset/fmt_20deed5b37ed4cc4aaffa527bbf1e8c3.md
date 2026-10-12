
# 第 4 章 Linux Sockets

`type` 参数可以设置为 `SOCK_DGRAM` 或 `SOCK_STREAM`，但这并不重要，因为协议由 `netlink_family` 决定，该参数设置为表 4.6 中的值之一。`send` 和 `recv` socket 调用通常与 `netlink` 使用。通过这些套字发送的消息具有特定的格式。详情见 `netlink(7)`。使用 `netlink` 套字的复杂性比我们描述的要多。在本章后面的部分，我们将详细讨论 `netlink` 的内部结构，同时查看 `netlink` 机制如何与 `TCP/IP` 中的协议接口。

### 路由套字 (Routing Sockets)

路由套字由 `AF_ROUTE` 指定。在 Linux 中，路由套字与 `netlink` 套字相同。

#### 表 4.6 `Netlink_family` 参数值

| 名称 | 数值 | 用途 |
|---|---|---|
| `NETLINK_ROUTE` | 0 | 路由或设备钩 |
| `NETLINK_USER` | 1 | |
| `NETLINK_USERSOCK` | 2 | 为未来的用户模式协议预留 |
| `NETLINK_FIREWALL` | 3 | 防火墙访问钩 |
| `NETLINK_INET_DIAG` | 4 | `AF_INET` 套字监控 |
| `NETLINK_NFLOG` | 5 | `Netfilter` 和 `iptables` 用户日志 |
| `NETLINK_XFRM` | 6 | `IPsec` 协议使用 |
| `NETLINK_SELINUX` | 7 | `Secure Linux` 事件监控 |
| `NETLINK_ISC` | 8 | `iSCSI` 实现 |
| `NETLINK_AUDIT` | 9 | 审计 |
| `NETLINK_FIB_LOOKUP` | 10 | 转发信息库 (BIB) 中的查找 |
| `NETLINK_CONNECTOR` | 11 | |
| `NETLINK_NETFILTER` | 12 | `netlink` 的 `netfilter` 子系统 |
| `NETLINK_IP6_FW` | 13 | `IPv6` 转发 |
| `NETLINK_DN_MSG` | 14 | `DECnet` 路由消息 |
| `NETLINK_KOBJECT_UEVENT` | 15 | 将内核消息传递到用户空间 |
| `NETLINK_GENERIC` | 16 | |

### `rtnetlink`

`rtnetlink` 通过附加带有某些额外属性的 `netlink` 类型消息来扩展 `netlink` 套字。`rtnetlink` 套字最常用于应用程序层对路由表的访问。

关于 `rtnetlink` 和其他特种套字类型的更多信息可以在主页面中找到。更多信息请参考 Linux 手页的 `netlink(7)`、`rtnetlink(7)`、`packet(7)` 和 `raw(7)`。

### 安全与 Linux 权限 (CAPABILITIES)

Linux 权限（capabilities）类似于其他系统上的访问控制列表（ACL）。如果没有安全机制，上一节中讨论的特殊套字可能被程序员用来访问底层的内核结构，包括 `TCP/IP` 堆栈的内部结构。在错误的人手中，这组函数可能成为安全违规的工具。我们希望防止未经授权的用户进行拒绝服务（DoS）和其他攻击。通过删除路由或重定向套字很容易破坏系统。权限是 Linux 中防止未经访问这些强大功能的机制，并在较新版本的内核中用于细粒度的访问。传统的 `Unix` 系统只有两种访问级别：`root` 或用户。用户获得 `root` 权限后，可以做任何事情。最近，Linux 权限符合 `POSIX.1` 草案权限。它将完整的 `root` 权限划分为子集。我们不会详细讨论 Linux 权限的所有功能，因为它们与 `TCP/IP` 无关，但我们将展示如何使用 Linux 权限来控制套字的访问。更多信息请参阅 Linux 手页 `capabilities(7)`。

权限很重要，因为它存储了套字层在允许访问原始或 `netlink` 套字之前检查的用户权限。为了执行这些操作，Linux 提供了一个内部函数 `capable`，定义在 `linux/include/linux/capability.h` 中，用于检查当前执行的用户进程的权限。

```c
extern int capable(int cap);
```

从 2.4 版本开始，Linux 在 `linux/include/capability.h` 文件中提供了一组数据结构和宏来存储和操作权限。如果内核中配置了安全功能 `CONFIG_SECURITY`，`capable` 函数将指向已加载权限模块的操作，该模块是内核的插件。

Linux 2.6 安全框架。如果不是，能力函数将调用一个虚拟函数 `dummy_capable`，该函数返回当前进程的有效权限，即正在发起用户级 socket 调用的进程。

```c
static int dummy_capable(struct task_struct *tsk, int cap)
{
    if (cap_raised (tsk->cap_effective, cap))
        return 0;
    return -EPERM;
}
```

在 Linux 中，全局变量 `current` 始终指向当前执行的进程。内核权限存储在一个 32 位的整数 `kernel_cap_t` 中。`current` 存储了以下类型的权限。

```c
kernel_cap_t cap_effective, cap_inheritable, cap_permitted;
```

在 socket 层代码中，我们实际上只检查 `cap_effective` 权限，因为我们对正在发起 socket 调用的当前应用程序进程的权限感兴趣。请参文件 `linux/include/linux/capability.h` 获取所有 `POSIX` 权限列表及其相关的数值值。

### 关于 Socket API 和 IPv6 的说明

第 11 章涵盖了 `IPv6` 协议、其实现方式以及它与 `IPv4` 实现的比较。然而，在本节中，我们将提到 `IPv6` 使用的地址族，以及为了适应该协议族对 2.6 内核 socket API 进行的一些更改。`IPv6` 引入了一个新的地址族 `AF_INET6`，该与与其他地址族一起定义在 `linux/include/socket.h` 中。

### `IPv6` Sock 地址类型，`sockaddr_in_6`

为了支持 `IPv6` 建模，Linux 为 `IPv6` 提供了一个独立的 socket 地址类型 `sockaddr_in6`，定义在文件 `linux/include/linux/in6.h` 中。

```c
struct sockaddr_in6 {
    unsigned short int sin6_family;
    __u16 sin6_port;
    __u32 sin6_flowinfo;
    struct in6_addr sin6_addr;
    __u32 sin6_scope_id;
}
```

前两个字段看起来与 `sockaddr_in` 结构非常相似。后续字段 `sin6_family` 被设置为 `AF_INET6` 或 10。

该字段 `sin6_port` 是 `UDP` 或 `TCP` 的端口号。下一个字段 `sin6_flowinfo` 是 `IPv6` 流信息。有关 `IPv6` 流的更多信息，请参见第 11 章。

下一个字段 `sin6_addr` 是定义为联合（union）的实际 `IPv6` 地址。最后一个字段是作用域 ID，它定义了地址的范围。我们将在第 11 章中详细讨论该结构以及 `IPv6` 地址范围。

`IPv6` socket 与 `IPv4` 兼容。socket API 定义数据可以在不修改的情况下通过 `IPv6` 发送。在底层，实际的 `IPv6` 地址由内核处理，包含了 128 位地址。在第 11 章中，我们将更详细地检查 `IPv6`。

### 地址转换函数

为了帮助程序员编写代码，Linux 提供了在 `IPv4` 和 `IPv6` 格式之间转换地址的函数。

### `getaddrinfo` 函数

第一个函数 `getaddrinfo` 是一个通用函数，结合了以下内容：

```c
int getaddrinfo(const char *node, const char *service, struct addrinfo *hints, struct addrinfo **res);
```
