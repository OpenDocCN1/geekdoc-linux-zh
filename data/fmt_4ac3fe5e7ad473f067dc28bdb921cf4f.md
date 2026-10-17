
```c
#include <sys/types.h>
#include <sys/socket.h>
int send(int s, const void msg, unsigned int flags);
sendto(int s, const void msg, int len, unsigned int flags,
const struct sockaddr *to, int len);
sendmsg(int s, const struct msghdr *msg, unsigned int flags);
```

## 描述

警告：这是一个 BSD man 页面。在 Linux 0.99.11 中尚未实现。

`sendto` 和 `sendmsg` 用于向另一个套字传输消息。`send` 只能在套字处于连接状态时使用，而 `sendto` 和 `sendmsg` 可以在任何时间使用。

目标地址由 `to` 提供，`len` 指定其大小。消息长度由 `len` 指定。如果消息太长，无法通过底层协议原子地传递，则返回错误 `MSGSIZE`，且消息不会传输。

`send` 不包含交付失败的指示。本地检测错误通过返回值 `-1` 来识别。

如果套字上没有可用空间存放待传输的消息，`send` 通常会阻塞，除非套字被设置为非阻塞 I/O 模式。当可以发送更多数据时可以使用 `select2()`。

`flags` 参数可能包含以下一个或多个：

```c
#define MSG_G0B 0x1 /* 带外数据 *
#define MSG_DONTROUTE 0x4 /* 绕过路由，直接接口 */
```

标志 `MSG_G0B` 用于在支持此功能的套字（例如 `SOCK_STREAM`）上发送带外数据；底层协议也必须支持带外数据。`MSG_DONTROUTE` 通常仅用于诊断或路由程序。

关于 `msghdr` 结构的描述参见 `recv2()`。

## 返回值

调用返回发送的字符数，如果发生错误则返回 `-1`。

## 错误

| 错误 | 描述 |
| :--- | :--- |
| `EBADF` | 指定了无效的描述符。 |
| `ENOTSOCK` | 参数不是套字。 |
| `EFAULT` | 为参数指定了无效的用户地址。 |
| `MSGSIZE` | 套字要求原子地发送消息，但待发送的消息大小无法实现这一点。 |
| `EWOULDBLOCK` | 套字被标记为非阻塞，且请求的操作将阻塞。 |
| `ENOBUFS` | 系统无法分配内部缓冲区。当缓冲区可用时，操作可能会成功。 |
| `ENOBUFS` | 网络接口的输出队列已满。这通常表示接口已停止，但可能是由瞬时拥堵引起的。 |

## 历史

这些函数调用出现在 BSD 4.2 中。

## 参见

```
fcntl(2), recv(2), select(2), getsockopt(2), socket(2), write(2)
```

BSD Man Page, 1991年7月24日

# setgid

setsgid—设置用于文件系统检查的组标识

## 语法概要

```c
int setsgid(uid_t fsgid);
```

## 描述

`setsgid` 设置 Linux 内核用于检查所有文件系统访问的组 ID。通常情况下，`fsgid` 的值会覆盖有效组 ID 的值。事实上，每当有效组 ID 改变时，`fsgid` 也会变为有效组 ID 的新值。

显式调用 `setsgid` 通常用于程序，例如在不改变实际和有效组 ID 的情况下更改用于访问的用户 ID。

# 第二部分：系统调用

进程组用于信号的分发，并由终端仲裁其输入请求；与终端处于同一进程组的进程为前台进程，可以读取，而其他进程在尝试读取时会被阻塞并接收信号。

这些函数用于如 `csh(1)` 等程序，用于在实现作业控制时创建进程组。`termios(4)` 中的 `TIOCGPGRP` 和 `TIOCSIGGRP` 调用用于获取/设置控制终端的进程组。

## 返回值

执行成功时，`setgid` 和 `setpgid` 返回 `0`。出错时，返回 `-1` 并适当地设置 `errno`。

`getpgid` 返回进程的进程组 ID。出错时，返回 `-1` 并适当地设置 `errno`。

`getpgid` 总是返回当前进程组。

## 错误

- `EINVAL` `pgid` 小于 `0`。
- `EPERM` 各种权限违规。
- `ESRCH` `pgid` 不匹配任何进程。

## 标准

`setgid` 和 `setpgid` 函数符合 POSIX.1.1。`setpgid` 函数源于 BSD 4.2。我没有关于 `setpgid` 来源的信息。

## 查看

`getuid(2)`, `setsid(2)`, `tcsetpgid(3)`, `termios(4)`

Linux 1.2.4, 4月15日

# setregid, setegid

setregid, setegid—设置实际组和有效组 ID

## 概要

```c
#include <unistd.h>
int setregid(gid_t rgid, gid_t egid);
int setegid(gid_t egid);
```

## 描述

`setregid` 设置当前进程的实际组 ID 和有效组 ID。非特权用户可以将实际组 ID 改为有效组 ID，反之亦然。

在 Linux 1.1.38 之前，当与 `setregid` 或 `setgid` 使用时，保存 ID 的范式是损坏的。从 1.1.38 开始，还可以从用户 ID 设置有效组 ID。

只有超级用户可以进行此类更改。

为实际组 ID 或有效组 ID 提供值 `-1` 将强制系统保持该 ID 不变。

目前（如-4.x.x），`setegid(egid)` 在功能上等同于 `setregid(-1, egid)`。

如果更改了实际组 ID 且有效组 ID 设置为不等于之前的实际组 ID 的值，则保存组 ID 将设置为新的有效组 ID。

## 返回值

执行成功时，返回 `0`。出错时，返回 `-1` 并适当地设置 `errno`。

## 错误

当前进程不是超级用户，且除了将有效组 ID 与实际组 ID 交换、将其中设置为另一个的值、或将有效组 ID 设置为保存组 ID 的值之外，指定了更改。

`EPERM`

## 历史

`setgid` 函数调用出现在 BSD 4.2 中。

## 符合

BSD 4.3

## 相关

`getgid(2)`, `setgid(2)`

Linux 1.1.38, 1994年8月2日

# setreuid, seteuid

setreuid, seteuid—设置实际和/或有效用户 ID

## 概要

```c
#include <unistd.h>
setreuid(uid_t ruid, uid_t euid);
seteuid(uid_t euid);
```

## 描述

`setreuid` 设置当前进程的实际用户 ID 和有效用户 ID。非特权用户可以将实际用户 ID 改为有效用户 ID，反之亦然。

在 Linux 1.1.37 之前，当与 `setreuid` 或 `seteuid` 使用时，保存 ID 的范式是损坏的。

从 1.1.37 开始，还可以从保存用户 ID 设置有效用户 ID。

超级用户可以进行其他更改。

为实际用户 ID 或有效用户 ID 提供值 `-1` 将强制系统保持该 ID 不变。

目前（`libc-4.x.x`），`seteuid(euid)` 在功能上等同于 `setreuid(-1, euid)`。

如果更改了实际用户 ID 或有效用户 ID 设置为不等于之前的实际用户 ID 的值，则保存用户 ID 将设置为新的有效用户 ID。

## 返回值

执行成功时，返回 `0`。出错时，返回 `-1` 并适当地设置 `errno`。

## 错误

`EPERM`

当前进程不是超级用户，且除了将有效用户 ID 与实际用户 ID 交换、将其中设置为另一个的值、或将有效组 ID 设置为保存用户 ID 的值之外，指定了更改。

## 历史

the `setgid` 函数调用出现在 BSD 4.2 中。（注：此处原文可能为笔误，应为 `setreuid`）

## 符合

BSD 4.3

# 第二部分：系统调用

## 相关

`getuid(2)`, `setuid(2)`

Linux 1.1.38, 1994年8月2日

# setsid

setsid—创建会话并设置进程组

## 概要

```c
#include <unistd.h>
pid_t setsid(void);
```

## 描述

如果调用进程不是进程组组长，`setsid()` 将创建一个新会话。调用进程是新会话的领袖、新进程的进程组组长，且没有控制终端。调用进程的进程组 ID 和会话 ID 被设置为调用进程的 PID。调用进程将是该会话中的唯一进程。

## 返回值

返回进程的会话 ID。

## 错误

出错时，返回 `-1`。

## 注意

调用进程的进程组 ID 和会话 ID 被设置为调用进程的 PID。调用进程将是该会话中的唯一进程。

## 符合

POSIX

## 相关

`setpgid(2)`, `fork(2)`

1994年8月27日

# setuid

setuid—设置实际用户 ID

## 概要
