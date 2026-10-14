
`cmd` 指定要在队列上执行的操作。它可以是以下内容之一：

- `IPC_RMID`
  - 立即移除消息对象及其关联的 `msqid_ds` 数据结构。队列中剩余的所有消息将丢失，任何阻塞的读取或写入进程将立即立即唤醒，且 `msg()` 或 `msgrcv()` 将因错误 `EIDRM` 失败。此操作会忽略 `msgctl()` 的第三个参数。
- `IPC_STAT`
  - 将与此消息队列关联的 `msqid_ds` 数据结构的副本存放在 `buf` 指向的缓冲区中。我们在第 46.4 节中描述了 `msqid_ds` 结构。
- `IPC_SET`
  - 使用 `buf` 指向缓冲区缓冲区提供的值，更新与此消息队列关联的 `msqid_ds` 数据结构的选定字段。

关于这些操作的更多细节、调用进程所需的权限和许可，见第 45.3 节。我们在第 46.6 节中描述了 `cmd` 的其他值。

列表 46-4 展示了如何使用 `msgctl()` 删除消息队列。

### 列表 46-4：删除 System V 消息队列

```c
#include <sys/types.h>
#include <sys/msg.h>
#include "tlipc_hdr.h"

int
main(int argc, char *argv[])
{
    int j;
    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usageErr("%s [msid...]\n", argv[0]);

    for (j = 1; j < argc; j++) {
        if (msgctl(getint(argv[j]), IPC_RMID, NULL) == -1)
            errit("msgctl %s", argv[j]);
    }

    exit(EXIT_SUCCESS);
}
```

`svmsgg/svmsg_rm.c`

## 46.4 消息队列关联数据结构

每个消息队列都有一个如下的关联 `msqid_ds` 数据结构：

```c
struct msqid_ds {
    struct ipc_perm msg_perm;      /* 所有权和权限 */
    time_t msg_stime;               /* 上次 msgsnd() 的时间 */
    time_t msg_rime;                /* 上次 msgrcv() 的时间 */
    time_t msg_ctime;               /* 最后修改的时间 */
    unsigned long msg_qnum;         /* 队列中的消息数 */
    unsigned long msg_qbytes;       /* 队列的最大字节数 */
    pid_t pid_lspid;               /* 上次 msgsnd() 的 PID */
    pid_t pid_lprid;               /* 上次 msgrcv() 的 PID */
};
```

在 `msqid_ds` 名称中使用 `msq` 缩写是为了困扰程序员。这是唯一使用这种拼写的消息队列接口。

`msg_qnum` 和 `msglen` 数据类型——用于消息队列 `msg_qnum` 和 `msg_qbytes` 字段——是 SVs3 指定无符号整数类型。

`msqid_ds` 结构的字段由各种消息队列系统隐含更新，某些字段可以使用 `msgctl(IPC_SET)` 操作显式更新。详情如下：

**`msg_perm`**

当创建消息队列时，此子结构的字段将按照第 45.3 节所述进行初始化。`uid`、`gid` 和 `mode` 子字段通过 `IPC_SET` 更新。

**`msg_stime`**

创建队列时，此字段被设置为 0；之后每次成功的 `msgsnd()` 都会将其设置为当前时间。此字段以及 `msqid_ds` 结构中的其他时间戳字段类型为 `time_t`；它们存储自 Unix 纪（Epoch）以来的秒数。

**`msg_rtime`**

创建消息队列时，此字段设置为 0，然后在每次成功的 `msgrcv()` 时被设置为当前时间。

**`msg_ctime`**

在创建消息队列以及每当成功执行 `IPC_SET` 操作时，此字段被设置为当前时间。

**`msg_cbytes`**

创建消息队列时，此字段设置为 0，随后在成功的 `msgsnd()` 和 `msgrcv()` 期间调整，以反映队列中所有消息 `mtext` 字段包含的字节总数。

**`msg_qnum`**

创建消息队列时，此字段被设置为 0。它随每次成功的 `msgsnd()` 递增，随每次成功的 `msgrcv()` 递减，反映队列中的消息总数。

**`msg_qbytes`**

此值定义了消息队列中所有消息 `mtext` 字段字节数的上限。它在创建队列时被初始化为 `MSGQNB` 的值。特权进程（`CAP_SYS_RESOURCE`）可以使用 `IPC_SET` 操作将 `msg_qbytes` 调整为 0 到 `INT_MAX`（32 位平台上为 2,147,483,647）范围内的任何值。非特权进程无法调整 `msg_qbytes`。特权用户可以修改 `/proc/sys/kernel/msgnb` 文件中的值，以更改后续创建队列的初始 `msg_qbytes`。我们在 46.5 节中介绍更多关于消息队列限制。

**`msg_lspid`**

创建队列时，此字段设置为 0，然后在每次成功的 `msgsnd()` 时设置为调用进程的 PID。

**`msg_lprid`**

创建队列时，此字段设置为 0，然后在每次成功的 `msgrcv()` 时设置为调用进程的 PID。

除了 `msg_cbytes` 之外，上述所有字段都由 SUSv3 规定。然而，大多数 UNIX 实现提供了等价的 `cbytes` 字段。列表 46-5 中的程序演示了使用 `IPC_STAT` 和 `IPC_SET` 操作修改消息队列的 `msg_qbytes` 设置。

### 列表 46-5：更改 System V 消息队列的 `msg_qbytes` 设置

```c
#include <sys/types.h>
#include <sys/msg.h>
#include <sys/ipc.h>

int
main(int argc, char *argv[])
{
    struct msqid_ds ds;
    int msqid;

    if (argc != 3 || strcmp(argv[1], "--help") == 0)
        usageErr("%s msqid max-bytes\n", argv[0]);

    /* 从内核获取关联数据结构 */
    msqid = getint(argv[1], 0, "msqid");
    if (msgctl(msqid, IPC_STAT, &ds) == -1)
        errExit("msgctl");

    ds.msg_qbytes = getint(argv[2], 0, "max-bytes");

    /* 更新内核中的关联数据结构 */
    if (msgctl(msqid, IPC_SET, &ds) == -1)
        errExit("msgctl");

    exit(EXIT_SUCCESS);
}
```

## 46.5 消息队列限制

大多数 UNIX 实现对消息队列的操作都有各种限制。这里描述 Linux 下的限制，并说明与其他 UNIX 实现的若干差异。以下限制在 Linux 上强制执行。受影响的系统调用以及达到限制时产生的错误列在括号中。

- `MSGID`
  - 这是可创建的消息队列标识符（换言之，消息队列）数量的系统级限制。(`msgsget`, `ENOSPC`)
- `MSGMAX`
  - 这是单条消息中可以写入的最大字节数的系统级限制。(`msgsnd`, `EINVAL`)
- `MSGNB`
  - 这是消息队列中一次可以容纳的最大字节数。此限制是一个系统级参数，用于初始化与此消息队列关联的 `msqid_ds` 结构的 `msg_qbytes` 字段。随后，可以按照 46.4 节所述按队列修改 `msg_qbytes` 值。如果达到了队列的 `msg_qbytes` 限制，`msgsnd()` 将阻塞，或者如果设置了 `IPC_NOWAIT` 则返回错误 `EAGAIN`。某些 UNIX 实现还定义了以下限制：
- `MSGQL`
  - 这是系统中所有消息队列中可以放置的消息数量的系统级限制。
- `MSGPOOL`
  - 这是系统中所有消息队列数据池池的系统级限制。
