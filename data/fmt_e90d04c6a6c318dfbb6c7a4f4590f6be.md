
如果 `SHMID` 大于 `size`，如果 `size` 大于 `SHMAX`，或者 `size` 大于段的大小，则返回此错误。

- `EEXIST`

如果指定了 `IPC_CREAT | IPC_EXCL` 且段存在，则返回此错误。

- `EIDRM`

如果段被标记为销毁或删除，则返回此错误。

- `ENOSPC`

如果所有可能的共享内存 ID 都已占用（`SHMNI`），或者分配请求大小的段将超过系统的共享内存限制（`SHMALL`），则返回此错误。

- `ENOENT`

如果 `key` 定的段不存在，且未指定 `IPC_CREAT`，则返回此错误。

- `EACCES`

如果用户没有访问该内存段的权限，则返回此错误。

- `ENOMEM`

如果无法分配内存，则返回此错误。

# shmop

## 注意

`IPC_PRIVATE` 不是一个标志，而是 `key_t` 类型。如果使用此值作为 `key`，系统将忽略 `shmid` 的低 9 位并创建一个新的内存段（成功情况下）。

以下是影响 `shmget` 的共享内存限制：

- `SHMALL` 全局共享内存页数取决于策略。
- `SHMAX` 共享内存大小（字节）；取决于实现（当前为 4MB）。
- `SHMIN` 共享内存最小大小（字节）；取决于实现（当前为 `PAGE_SIZE`）。
- `SHMNI` 全局共享内存段数；取决于实现（当前为 4096）。

实现没有每个进程最大段限制 `SHSEG`。

# Bug

使用 `IPC_PRIVATE` 不阻止其他进程对分配内存段的访问。像文件一样，没有内在方法确保内存段的独占访问。断言 `IPC_CREAT` 和 `IPC_EXCL` 仅在成功时确保创建一个新的内存段；它不会排除对段的访问。

## 参见

`ftok(3)`, `ipc(5)`, `shmctl(2)`, `shmat(2)`, `shmdt(2)` Linux 0.99, 11月28日

# shmop—共享内存操作

# 语法概要

```
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
char *shmat (int shmid, char *shaddr, int shflg);
shmdt (char *shaddr);
```

## 描述

函数 `shmat` 将 `shmid` 标识的共享内存连接到调用进程的数据段。通过 `shaddr` 指定连接的位置如下：

- 如果 `shmid` 为 0，系统尝试从 1GB 开始查找未映射的区域。
- 如果 `shaddr` 不是 0 且设置了 `SHMRDONLY`，则在等于 `shaddr` 向上对齐 `MBA` 的地址处连接。`shaddr` 必须是页对齐的地址。

如果在 `shflg` 中设置了 `SHMRDONLY`，段为只读，进程必须对段有读取权限。否则，段为读写，进程必须对段有读写权限。没有只有写的内存段的概念。

调用进程的 `brk` 值不随连接改变。段将在进程退出时自动分离。同一段可以在进程地址空间中作为读写段被连接多次。

# 第二部分：系统调用

成功的 `shmat` 调用将系统更新与共享内存段关联的 `shmid_ds` 结构成员如下：

- `shm_ctime` 设置为当前时间。
- `shm_pid` 设置为调用进程的 ID。
- `shm_natt` 加 1。

注意，如果共享内存段被标记为删除，连接也会成功。

函数 `shmdt` 从调用进程位于地址 `shaddr` 的数据段中分离共享内存段。要分离的共享内存段必须是当前连接的（进程地址空间中的），且 `shaddr` 等于连接调用返回的值。

成功的 `shmat` 调用将系统更新与共享内存段关联的 `shmid_ds` 结构成员如下：

- `shm_ctime` 设置为当前时间。
- `shm_pid` 设置为调用进程的 ID。
- `shm_natt` 减 1。如果它变为 0 且段被标记为删除，则删除该段。

进程用户空间中的占用区域被取消映射。

# 系统调用

| `fork()` | 在 `fork()` 之后，子进程继承共享内存段。 |
| `exec()` | 在 `exec()` 之后，所有连接的共享内存段均被分离（未销毁）。 |
| `exit()` | 在 `exit()` 之后，所有连接的共享内存段均被分离（未销毁）。 |

# 返回值

失败时，两个函数均返回 `-1` 并用 `errno` 指示错误；否则，`shmat` 返回连接的内存段的地址，`shmdt` 返回 `0`。

# 错误

当 `shmat` 失败时，`errno` 将设置为以下值之一：

- `EACCES`：调用进程没有请求的连接类型的权限。
- `EINVAL`：无效值（即未页对齐且未指定 `SHM_RD`）或无效的 `shaddr` 值，或 `brk` 失败。
- `ENOMEM`：无法为描述符或页表分配内存。

函数 `shmat` 仅当 `shaddr` 没有连接的共享内存时可能失败；在这种情况下，返回时 `errno` 将设置为 `EINVAL`。

## 注意

执行 `fork(2)` 系统调用时，子进程继承所有连接的共享内存段。执行 `exec(2)` 系统调用的进程连接的共享内存段将不会连接到结果进程。

以下是影响 `shmat` 系统调用的系统参数：

- `SHMLBA`：段边界地址。必须页对齐。`SHMLBA` 的值为 `PAGE_SIZE`。

实现对每个进程最大共享内存段数 (`SHMSEG`) 没有内在限制。

## 参见

`ipc(5)`, `shctl(2)`, `shget(2)`

Linux 0.99.13, 1999年11月28日

## shutdown

`shutdown`—关闭全双工连接的一部分

## 概要

```
#include <sys/socket.h>
int shutdown(int s, int how);
```

## 描述

`shutdown` 调用会导致与 `s` 关联的套字的全双工连接的所有或部分关闭。如果 `s` 为 0，将不再允许进一步接收。如果 `s` 为 1，将不再允许进一步发送。如果 `s` 为 2，将不再允许进一步的发送和接收。

## 返回值

成功时返回 `0`。出错时返回 `-1`，并恰当地设置 `errno`。

## 错误

- `EBADF` `s` 不是有效的描述符。
- `ENOTSOCK` `s` 是文件，不是套字。
- `ECONCONN` 指定的套字未连接。

## 历史

`shutdown` 函数调用出现于 BSD 4.2。

# 另参

`connect(2)`, `socket(2)`

## sigaction, sigprocmask, sigpending, sigsuspend

`sigaction`, `sigprocmask`, `sigpending`, `sigsuspend`—POSIX 信号处理函数。

## 概要

```
#include <signal.h>
int sigaction(int sig, const sigaction *act, struct sigaction *oldact);
int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);
int sigpending(const sigset_t *mask=set);
int sigsuspend(const sigset_t *mask);
```

## 描述

信号系统用于更改进程在接收到特定信号时采取的动作。

`sigaction` 指定信号，可以是 `SIGKILL` 和 `SIGSTOP` 之外的任何有效信号。

如果 `act` 不空，则从 `act` 安装信号的新动作。如果 `oldact` 不空，则将先的动作保存在 `oldact` 中。

`sigaction` 结构体定义如下：

```c
struct sigaction {
  void (*sa_handler)(int);
  sigset_t sa_mask;
  int sa_flags;
  void (**restorer)(void);
}
```

`sa_handler` 指定与信号关联的动作，默认动为 `SIG_DFL`，忽略该信号为 `SIG_IGN`，或者指向一个信号处理函数的指针。

`sa_mask` 给出一个信号掩码。此外，触发处理句的信号将被阻塞，除非使用了 `SA_NODEFER` 或 `SA_NOWASK` 标志。

`sa_flags` 指定了一组修改信号处理进程行为的标志。它由以下一个或多个标志的位或运算组成：

- `SA_NOCLDSTOP` 如果在子进程停止（即子进程接收到 `SIGSTOP`、`SIGTSTP`、`SIGTIN` 或 `SIGTOU` 之一）时不接收通知。
- `SA_ONESHOT` 或 `SA_RETHAND` 在处理器被调用后，将信号动作恢复到默认状态。（这是 `signal(2)` 系统调用的行为）。
- `SA_RESTART` 通过使某些系统调用变为可重启信号，提供了与 BSD 信号语义兼容的行为。
- `SA_NOWASK` 或 `SA_NODEFER` 不防止从信号处理器内部接收该信号。

`_restorer` 元素已过时，不应使用。

`sigprocmask` 调用用于更改当前阻塞的信号列表。调用的行为取决于 `how` 的值，如下：

| 标志 | 描述 |
| :--- | :--- |
| `SIG_BLOCK` | 阻塞信号集是当前集合与参数集的并集。 |
