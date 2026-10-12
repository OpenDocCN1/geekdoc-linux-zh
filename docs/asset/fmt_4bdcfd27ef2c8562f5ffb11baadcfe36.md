
```
struct ipc_perm {
    key_t key;
    ushort uid;      /* 所有者 euid 和 egid */
    ushort gid;
    ushort cuid;     /* 创建者 euid 和 egid */
    ushort cgid;
    ushort mode;     /* 访问模式，见下面的标志 */
    ushort seq;      /* 槽位使用序列号 */
}
```

以上内容都非常浅易懂。与对象的 IPC key 一起存储的还有关于该对象创建者和所有者的信息（它们可能不同）。八进制访问模式也以无符号短整数的形式存储在这里。最后，槽位使用序列号存储在末尾。每当 IPC 对象通过系统调用关闭（销毁）时，该值就会增加系统中可以存在的 IPC 对象最大数量。你是否需要关注这个值呢？

在 Richard Stevens 的《UNIX 网络编程》书中（第 125 页），对这个主题以及其存在和行为的安全原因有极佳的讨论。

## 系统调用：`msgget()`

为了创建一个新的消息队列或访问现有队列，使用了 `msgget()` 系统调用。

### Linux 进程间通信 39

系统调用：`msgget();`

原型：`int msgget ( key_t key, int msgflag );`

返回值：成功时返回消息队列标识符

错误时返回 -1：

- `errno = EACCES`（权限被拒绝）
- `EEXIST`（队列已存在，无法创建）
- `EIDRM`（队列被标记为删除）
- `ENOTENT`（队列不存在）
- `ENOMEM`（内存不足以创建队列）
- `ENOSPC`（超过最大队列限制）

`msgget()` 的第一个参数是键值（通常由调用 `ftok()` 返回）。然后，该键值将与内核中其他消息队列的现有键值进行比较。此时，打开或访问操作将取决于 `msgflg` 参数的内容。

- `IPC_CREAT`—如果队列在内核中尚不存在，则创建队列。
- `IPC_EXCL`—与 `IPC_CREAT` 用时，如果队列已存在，则失败。

如果单独使用 `IPC_CREAT`，`msgget()` 返回新创建的消息队列的标识符，或者返回具有相同键值的已存在队列的标识符。如果 `IPC_EXCL` 与 `IPC_CREAT` 使用，则会创建一个新队列；或者如果队列存在，则调用失败并返回 -1。`IPC_EXCL` 本身是无用的，但结合 `IPC_CREAT` 使用时，可以作为确保不打开现有队列进行访问的机制。

可以将可选模式通过位或或合并到标志中，因为每个 IPC 对象的权限功能与 Unix 文件系统上的文件权限相似！

让我们为打开或创建消息队列编写一个快速封装函数：

```c
int open_queue( key_t keyval ) {
    int qid;
    if((qid = msgget( keyval, IPC_CREAT | 0660 )) == -1) {
        return -1;
    }
    return(qid);
}
```

注意显式权限 `0660` 的使用。这个小函数要么返回消息队列标识符 (int)，要么在错误时返回 -1。键值必须作为唯一参数传递给它。

### Linux 程序员指南：第 6 章

## 系统调用：`msgsnd()`

一旦我们有了队列标识符，就可以开始对其进行操作。要向队列投递消息，你使用 `msgsnd` 系统调用：

```
SYSTEM CALL: msgsnd();

TOTYPE: int msgsnd ( int msqid, struct msgbuf *msgsp, int msgsz, int msgflg);
返回值：成功返回 0
  - EAGAIN（队列满且断用了 IPC_NOWAIT）
- 错误时返回 1：errno
- EACCES（权限被拒绝，无写权限）
- EFAULT（msgsp 地址不可访问 -无效）
- EIDRM（消息队列已被移除）
- EINTR（等待写入时接收到信号）
- EINVAL（无效的消息队列标识符、消息类型或无效的消息缓冲区）
- ENOMEM（内存不足以拷贝消息）
```

`msgsnd` 的第一个参数是之前调用返回的队列标识符。第二个参数 `msgsp` 是指向消息缓冲区的指针。第三个参数 `msgsz` 包含消息的大小，不包括 `mtype` 的长度。`msgflg` 可以设置为 0 或 `IPC_NOWAIT`：如果队列满了，进程将阻塞直到消息到达。让我们为发送再创建一个另一个封装函数：

```c
int send_message(int msqid, struct msgbuf *msgsp, int msgsz, int msgflg) {
    int result;
    if ((result = msgsnd(msqid, msgsp, msgsz, msgflg)) == -1) {
        return -1;
    }
    return(result);
}
```

一旦我们有了队列标识符，就可以开始对其进行操作。要向队列投递消息，你使用 `msgsnd` 系统调用。这里是一个利用我们开发的函数的示例代码：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <types.h>

int main() {
    int qid;
    key_t key;
    struct msgbuf {
        long mtype;
        char mtext[100];
    } msg;
    int result;
    long length;

    key = ftok("tmp", 'a');
    if ((qid = msgget(key, IPC_CREAT | 0660)) == -1) {
        perror("msgget");
        exit(1);
    }

    msg.mtype = 1;
    sprintf(msg.mtext, "Hello!");
    length = strlen(msg.mtext);

    if ((msgsnd(qid, &msg, length, 0)) == -1) {
        perror("msgsnd");
        exit(1);
    }

    printf("Message sent.\n");
    return 0;
}
```

### Linux 程序员指南：第 6 章

在创建/打开消息队列后，我们继续查看队列的状态。现在我们有了消息标识符，开始从队列中检索消息。要这样做，使用 `msgrcv()` 系统调用：

```
SYSTEM CALL: msgrcv();

原型：int msgrcv ( int msqid, struct msgbuf *msgp, int msgsz, long mtype, int msgflg);
返回值：拷贝到消息缓冲区的字节数
错误 -1：errno
- ACCES（无读权限）
- EFAULT（msgp 指向的地址无效）
- EIDRM（检索期间队列被删除）
- EINTR（被信号中断）
- EINVAL（msgid 无效或 msgsz 小于 0）
- ENOMSG（使用了 IPC_NOWAIT 但无消息）
```

第一个参数用于指定检索过程中使用的队列（应由之前的 `msgget` 调用返回）。`msgp` 代表存储检索到的消息的消息缓冲区变量地址。第三个参数 `msgsz` 代表缓冲区的大小，不包括 `mtype` 的长度。再次，这可以简单计算为：

```c
msgsz = sizeof(struct msgbuf) - sizeof(long);
```

第四个参数 `mtype` 指定要检索的消息类型。内核将在队列中搜索匹配类型的最旧消息，并将其拷贝到 `msgp` 参数指向的位置。存在特殊情况：如果传递的 `mtype` 值为零，则返回旧的消息，无论类型如何。

如果标志中使用了 `IPC_NOWAIT` 但没有可用消息，调用向调用进程返回 `ENOMSG`。否则，调用进程将阻塞直到满足 `msgrcv()` 参数的消息到达。如果在客户端等待消息时队列被删除，则返回 `EIDRM`。如果在进程在阻塞模式下等待消息到达时捕获到信号，则返回 `EINTR`。

让我们查看从队列接收消息的快速封装函数：

```c
int receive_message(int msqid, struct msgbuf *msgp, int msgsz, long mtype, int msgfl) {
    int result;
    if ((result = msgrcv(msqid, msgp, msgsz, mtype, msgfl)) == -1) {
        return -1;
    }
    return(result);
}
```
