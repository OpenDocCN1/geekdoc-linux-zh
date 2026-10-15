
## 5.11 选定的 AIX/Linux 系统 API 比较

#### 5.11.28.3 详细比较

**不兼容**

（注：此部分原文在输入中不完整，已根据上下文推断）

- `Q_XQUOTA`

  释放磁盘配额占用的磁盘空间。配额必须已经关闭状态。

  XFS 没有等同于 `Q_SYNC` 的命令，因为 `sync` 会将配额信息写入磁盘（除了它写入的其他文件系统元数据之外）。

#### 5.11.28.4 返回值

`quotactl()` 成功时返回 0，失败返回 -1 并设置 `ERRNO` 以指示错误。

#### 5.11.28.5 错误

- `EFAULT`. `addr` 和 `special` 无效。
- `EINVAL`. 内核编译时未启用 `QUOTA` 选项。`cmd` 无效。
- `ENOENT`. `special` 或 `addr` 指定的文件不存在。
- `ENOTBLK`. `special` 不是块设备。
- `EPERM`. 该调用需要特权，而调用者不是超级用户（super user）。
- `ESCHR`. 未为指定的用户找到磁盘配额（disc quota）。该文件系统未开启配额。
- `EUSERS`. 配额表已满。

如果 `cmd` 是 `Q_QUOTAON`，`quotactl()` 可能会将 `ERRNO` 设置为：

- `EACCES`

  `addr` 指向的配额文件存在但不是普通文件。`addr` 指向的配额文件存在但不在 `special` 指向的文件系统中。

- `EBUSY`

  尽管已经发生过 `Q_QUOTAON`，但仍尝试执行 `Q_QUOTAON`。

## 5.12 AIX 非标准编程实践

在任何平台上进行开发时，有时无法避免使用特定平台的 API。例如，开发驱动程序时必须使用特定平台的 API，而这些 API 无法在平台之间进行移植。表 5-7 列出了一些从 AIX 迁移到 Linux 时需要额外编程工作的非标准编程实践。

**TABLE 5-7 非标准编程参考**

| AIX | Linux |
| --- | --- |
| 使用对象数据管理器 (ODM) API：`odm_add_obj`, `odm_change_obj`, `odm_close_class` 等 | 使用 www.linux.org 并搜索文档“Linux Device Driver Development（Linux 设备驱动开发）”。 |
| 使用 `nlist` | 查看 `lsof` 源代码中的 `nlist_private` 示例。 |
| 直接读取 `/dev/kmem` | 使用 `/procfs` 和 `sysinfo` API 进行移植。 |
| 使用可移植流环境 (PSE) 和 System V release 4 信号：`t_accept`, `t_alloc`, `t_bind`, `t_close`, `t_connect` 等 | 使用开源 Linux Streams (LiS) (www.gcom.com/home/linux/lis/)。 |
| 使用`/proc` | 使用 `/procfs` 和 `sysinfo` API 进行移植。 |

简而言之，任何与内核直接交互的底层编程实践都被认为是不可移植的。额外的工作将涉及反向工程，以便在目标平台上实现相同的行为和功能。

## 5.13 信号

信号是事件发生的指示。通常，接收到信号的进程通过默认机制或信号处理程序（signal handler）来处理该信号。POSIX 定义了一组在 Linux 中实现的信号和信号处理函数。本节对比了 Linux 2.6 和 AIX 之间的信号支持差异。

### 5.13.1 信号动作

每个信号都有一个关联的默认动作。默认动作当信号到达该进程时，Linux 内核对该进程的操作。默认动作如下：

- 进程终止（Process Termination）。进程被终止。
- 进程转储（Process Coredump）。进程被终止并可能产生转储文件¹19
- 进程停止（Process Stopped）。进程被停止。

进程也可以安装信号处理程序，以便在信号递送给它时运行。信号处理程序将取代每个信号关联的默认动作。

信号的发生是事件的结果。以下是一些可能向进程发送信号的示例：

- 程序错误，例如除以 0 或访问无效地址
- 子进程终止
- 定时器超时
- 用户请求中断或终止进程

### 5.13.2 简单信号

Linux 支持的最简单的信号处理函数是原始的 ISO C 标准信号 `signal()` API。它允许调用进程更改特定信号的动作，即忽略或恢复默认信号动作，或者安装一个在进程接收到特定信号时调用的函数。

本节定义了 GNU/Linux 中提供的 `signal()` API 以及它们与 AIX 的区别。

> 19 在某些 Linux 系统中，默认关闭转储（coredumping）是的。要开启它，请使用 `ulimit -c` 命令。

#### 5.13.2.1 AIX 原型

```
#include <signal.h>

int sigaction(int Signal, struct sigaction *Action, struct sigaction *OAction);

int sigprocmask(int How, const sigset_t *Set, sigset *OSet);

int sigpending(sigset_t *Set);

int sigsuspend(const sigset_t *SignalMask);

int pause(int SignalMask);
```

#### 5.13.2.2 Linux 原型

```
#include <signal.h>

int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);

int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);

int sigpending(sigset_t *set);

int sigsuspend(const sigset_t *mask);

int pause(int sigmask);
```
