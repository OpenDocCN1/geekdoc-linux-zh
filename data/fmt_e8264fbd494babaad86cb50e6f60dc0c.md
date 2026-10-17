
| msqid | owner perms | 已用字节 消息数 |
| :--- | :--- | :--- |
| 0 | root | 660 5 1 |

在这里我们看到一个标识符为“0”的单个消息队列。它由用户 `root` 拥有，八进制权限为 660，即 `-rw---`。队列中有一条消息，该消息的总大小为 5 字节。`ipcs` 命令是一个非常强大的工具，可以窥探内核 IPC 对象的存储机制。学习它，使用它，并掌握它。

`ipcrm` 命令可以用于从内核中移除 IPC 对象。虽然可以通过用户代码中的系统调用移除 IPC 对象（稍后我们将看到方法），但经常会有手动移除 IPC 对象的需求，特别是在开发环境中。

```
ipcrm <msg | sem | shm> <IPC ID>
```

只需指定要删除的对象是消息队列 `msg`、信号量集 `sem` 还是共享内存段 `shm`。`IPC ID` 可以通过 `ipcs` 命令获取。你必须指定对象的类型，因为标识符在相同类型之间是唯一的（回想我们之前对此的讨论）。

消息队列可以最好地描述为内核地址空间内部的链表。消息可以按顺序发送到队列，并以几种不同的方式从队列中检索。每个消息队列（当然）都通过 IPC 标识符唯一标识。

完全理解 System IPC 等复杂主题的关键，在于非常熟悉存在于内核内部的各种内部数据结构。即使对于最原始的操作，直接访问其中一些结构也是必要的，而另一些结构则位于更低的层次。

## 消息缓冲区

我们将访问的第一个结构是 `msgbuf` 结构。这个特定的数据结构可以被视为消息数据的模板。虽然定义这种类型的结构由程序员决定，但你必须理解实际上存在一种类型为 `msgbuf` 的结构。它定义在 `linux/msg.h` 中如下：

```c
/* message buffer for msgsnd and msgrcv calls */ {
    long mtype;      /* 消息类型 */
    char mtext[1];   /* 消息文本 */
};
```

`msgbuf` 结构中有两个成员：

- `type`: 消息类型，用正数表示。这必须是一个正数！
- `mtext`: 消息数据本身。

分配给定消息类型的能力，本质上赋予了你在单个队列上进行消息复用的能力。例如，为客户端进程分配一个魔数，该数字可以作为从服务器进程发送的消息的类型。服务器本身可以使用另一个数字，客户端可以使用该数字向它发送消息。在另一种情况下，应用程序可以将错误消息标记为类型为 1，请求消息可以是类型 2 等等。可能性是无限的。

另外，不要被赋予消息数据元素 `mtext` 的几乎过于描述性的名称所误导。该字段不仅限于持有字符数组，而是任何形式的任何数据。该字段本身实际上是完全二进制的，因为该结构由应用程序程序员重新定义。考虑这种重新定义：

```c
struct my_msgbuf {
    long mtype;             /* 消息类型 */
    long request_id;       /* 请求标识符 */
    struct client info;     /* 客户端信息结构 */
};
```

在这里我们看到了消息类型，之前一样，但结构的其余部分被另外两个元素替换，其中另一个结构！这就是消息队列的魅力所在。内核不对数据进行任何翻译。然而，存在一个内部限制，即给定消息的最大大小。

在 Linux 中，它定义在 `linux/msg.h` 中如下：

```c
#define MSGMAX 4056 /* <= 4056 */ / 最大大小
```

# 编程书籍，第 125 页

为了创建一个新的消息队列或访问已存在的队列，使用了 `msgget()` 系统调用。

原型：`int msgget( key_t key, int msgfl );` 返回：成功时返回消息队列标识符

- 错误时返回 `-1`：`errno = EACCESS`（拒绝访问）
- `-EEXIST`（队列已存在，无法创建）
- `EIDRM`（队列被标记为删除）
- `ENOENT`（队列不存在）
- `ENOMEM`（内存不足以创建队列）
- `ENOSPC`（超过最大队列限制）

### 注意

`msgget()` 的第一个参数是键值（在我们的例中，由 `ftok()` 调用返回）。随后，该键值将与内核中存在的其他消息队列的现有键值进行比较。此时，打开或访问的操作将取决于 `msgfl` 参数的内容。

如果队列在内核中不存在，则创建它。

### IPC EXCL

当与 `IPC CREATE` 一起使用时，如果队列已存在。

如果单独使用 `IPC CREATE`，`msgget()` 将返回新创建的消息队列的标识符，或者返回具有相同键值的现有队列的标识符。如果 `IPC EXCL` 与 `IPC CREATE` 同时使用，则创建一个新队列；如果队列已存在，调用失败并返回 `-1`。`IPC EXCL` 本身没用，但当与 `IPC CREATE` 结合时，它可以作为确保不打开已存在队列访问的机制。

可选的八进制模式可以与掩码进行按或运算，因为每个 IPC 对象的权限在功能上与 UNIX 文件系统上的文件权限相似！

让我们为打开或创建消息队列编写一个快速的封装函数：

```c
int open_queue( key_t keyval )
```

```c
{
int qid;
if((qid = msgsget( keyval, IPC_CREAT | 0660 )) == -1) {
    return(-1);
}
return(qid);
}
```

注意使用显式权限 `0660`。这个小函数要么返回消息队列标识符 `int`，要么在错误时返回 `-1`。键值必须作为唯一参数传递给它。

一旦我们有了队列标识符，就可以开始对其进行操作了。要向队列发送消息，你使用 `msgsnd` 系统调用：

原型：`int msgsnd (int mqid, struct msgbuf *msg, int msgsz, int flg);` 返回：成功时返回 0

- 错误时返回 `-1`：`errno = EAGAIN`（队列已满，且断用了 `IPC_NOWAIT`）
- `-EACCES`（拒绝访问，无写权限）
- `EFAULT`（消息地址不可访问 -效）
- `EIDRM`（消息队列已被删除）
- `EINTR`（在等待写入时收到信号）
- `EINVAL`（无效的队列标识符、非弹出消息类型，或无效的消息大小）
- `ENOMEM`（内存不足以复制消息缓冲区）

### 注意

`msgsnd` 的第一个参数是我们的队列标识符，由之前的 `msgsget` 调用返回。第二个参数 `msgp` 是指向我们声明并加载的消息缓冲区的指针。`msgsz` 参数包含消息以字节为单位的大小，不包括消息类型的长度 `4` 字节长。`msgsflg` 参数可以设置为 `0`（忽略），或：

如果消息队列已满，则消息不会被写入队列，控制将返回给调用进程。如果未指定，调用进程将挂起（阻塞），直到消息可以写入为止。

让我们为发送消息创建另一个封装函数：

```c
int send_message(int qid, struct mymsgbuf *qbuf) {
    int result, length;
}
```

```c
/* 长度本质上是结构体的大小减去 sizeof(mtype) 的长度
length = sizeof(struct mymsgbuf) - sizeof(long);
if((result = msgsnd(qid, qbuf, length, 0)) == -1) {
    return(-1);
}
return(result);
}
```

这个小函数尝试将位于地址 `qbuf` 的消息发送到由传递的队列标识符 `qid` 指定的消息队列。这里有一个利用我们为止开发的两个封装函数的示例代码段：

```c
#include <stdio.h>
#include <stdlib.h>
#include <linux/ipc.h>
#include <linux/msg.h>
main() {
```

| 字段 | 变量 | 注释 |
| :--- | :--- | :--- |
| key_t | msgkey; | |
| struct mymsgbuf { | | |
| long | mtype; | /* 消息类型 */ |
| int | request; | /* 工作请求数 */ |
| double | salary; | /* 员工工资 */ |
| };

/* 生成我们的 IPC 键值 */ 

msgkey = ftok(".", "m");

/* 打开/创建队列 */ 

if((qid = open_queue(msg)) == -1) {

    perror("open_queue"); exit(1);

}
```

```c
/* 使用任意测试数据填充消息 */ 
msg.mtype = 1; /** 消息类型必须是正数！ */ 
msg.request = /* 工作请求 */ 
msg.salary = 1000.00; /* 员工工资 */

/** 发送消息 */
if((send_message( qid, &msg )) == -1) {
    perror("send_message");
    exit(1);
}
}
```

在创建/打开消息队列后，我们向消息缓冲区填充测试数据。现在我们有了消息，尝试 `ipcs` 命令查看队列状态。现在要从队列中检索消息，你使用 `msgrcv()` 系统调用：

原型：`int msgrcv(int msqid, struct msgbuf *msgbuf, int msgsz, long mtype);` 返回：复制到缓冲区的字节数

- 错误时返回 `-1`：`errno = EBIG`（消息长度大于 msgsz）
- `EACCES`（权限）
- `EFAULT`（指向 msgbuf 的地址无效）
- `EIDRM`（队列被删除）
- `EINTR`（被信号中断）
- `EINVAL`（msqid 无效，或 msgsz 小于 0）
- `ENOMSG`（断用了 `IPC_NOWAIT`，且队列不存在消息）

### 注意

显然，第一个参数用于指定检索过程中使用的队列（应该是由之前的 `msgget` 返回的）。第二个参数 `msgbuf` 代表存储检索到的消息的缓冲区地址。第三个参数 `msgsz` 代表消息的大小，不包括 `mtype`。再次，这很容易计算为：

```c
msgsz = sizeof(struct mymsgbuf) - sizeof(long);
```

第四个参数 `mtype` 指定要从队列检索的消息类型。内核将在队列中搜索类型匹配的消息，并将其复制到指向 `msgbuf` 参数的地址中。存在特殊情况：如果传递的 `mtype` 为零，则返回队列中最旧的消息，无论类型如何。

如果作为标志传递 `IPC_NOWAIT` 且没有可用消息，调用向调用进程返回 `ENOMSG`。否则，调用将阻塞，直到队列中出现符合 `msgrcv()` 参数的消息。成功从队列检索消息后，队列中的消息项将被删除。
`msflg` 参数中的 `MSG NOERROR` 位提供了一些额外功能。如果物理消息数据大于 `msgsz` 且断用了 `MSG NOERROR`，则消息会被截断，只返回 `msgsz` 字节。通常，`msgrcv()` 系统调用返回 `-1` `EBIG`，且消息将留在队列中以便稍后检索。这种行为可以用于创建另一个封装函数，允许我们“窥视”队列内部，查看是否有符合我们请求的消息到达：

```c
int peek_message(int qid
```

```c
int result, length;
if((result = msgrcv(qid, NULL, 0, type, IPC_NOWWAIT)) == -1)
  { 
    if(errno == E2BIG) return(TRUE);
  }
return(FALSE);
}
```

在上方，你会注意到缺少缓冲区地址和长度。在这一特定情况下，我们希望调用失败。然而，我们检查了 `E2BIG` 的返回，这表示存在一个匹配我们请求类型的消息。封装函数在成功时返回 `TRUE`，否则返回 `FALSE`。还要注意对 `IPC_NOWWAIT` 标志的使用，它防止了之前描述的阻塞行为。

通过前面介绍的封装函数，你现在拥有一种简单且相当优雅的方法在应用程序中创建和使用消息队列。现在，我们将讨论转向直接操作与给定消息队列相关的内部结构。要对消息队列执行控制操作，你需要使用 `msgctl()` 系统调用。

- 原型：`int msgctl(int msgqid, int cmd, struct msgqid_ds *buf);`
- 返回：成功时返回 0
- `-1` 错误：`errno = EACCES`（无读取权限），命令为 `IPC_STAT_EFAULT`（buf 指向的地址无效）
- `IPC_STAT`（在检索期间队列被移除）
- `EINVAL`（msgid 无效，或 msgsz 小于 0）
- `EPERM`（执行 `IPC_SET` 或 `IPC_RMID` 命令的进程对队列没有写访问权限）

备注：

常识告诉我们，直接操作内部内核数据可能会导致“深夜的乐趣”。不幸的是，程序员所承担的后果职责，只有在你喜欢破坏 IPC 子系统时才能被归类为“乐趣”。通过使用一组选择性的命令配合 `msgctl()`，你有能力操作那些较不容易引起麻烦的项目。让我们来看这些命令：

检索队列的 `msqid_ds` 结构，并将其存储在 `buf` 参数的地址中。

### IPC SET

设置队列的 `msqid_ds` 结构中 `ipc perm` 成员的值。取自 `buf` 参数的值。

### IPC RMID

从内核中移除队列。

回想我们关于消息队列内部数据结构 `msqids` 的讨论。内核为系统中存在的每个队列维护该结构的一个实例。通过使用 `IPC STAT` 命令，我们可以获取该结构的副本以供检查。让我们来看一个快速封装函数，它将检索内部结构并复制到传递的地址中：

```c
int get_queue_ds(int qid, struct msqid_ds *qbuf) {
    if (msctl(qid, IPC_STAT, qbuf) == -1) {
        return(-1);
    }
    return(0);
}
```

如果我们无法复制内部结构，则返回 `-1`。如果进展顺利，则返回 `0`。

现在我们已经有了该结构的副本，可以修改哪些属性？`ipcperm` 中唯一可修改的项目是模式 `mode`、所有者的用户 ID `uid` 和组 ID `gid`。让我们创建一个用于更改模式的封装函数。

```c
int change_queue(int qid, char *mode) {
    struct msqid_ds tmpbuf;
    if (msctl(qid, IPC_STAT, &tmpbuf) == -1) {
        return(-1);
    }
    tmpbuf.msg_perm.mode = atoi(mode);
    if (msctl(qid, IPC_SET, &tmpbuf) == -1) {
        return(-1);
    }
    return(0);
}
```

```c
int remove_queue(int qid) {
    if (msctl(qid, IPC_RMID, NULL) == -1) {
        return(-1);
    }
    return(0);
}
```

摘自《Linux 程序员指南 - 第 6 章》
(C)opy 1994-1995, Scott Burkett

一个用于调试 SysV 风格消息队列的命令行工具

```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#define MAX_SEND_SIZE 80
struct mymsgbuf { long type; char metxt[MAX_SEND_SIZE]; };
void send_message(int qid, struct mymsgbuf *qbuf, long type, char *text);
void read_message(int qid, struct mymsgbuf *qbuf, long type);
void remove_queue(int qid);
void change_queue_mode(int qid, char *mode);
void usage(void);
```

```c
int main(int argc, char *argv[]) {
    key_t key; int msgqueue_id; struct mymsgbuf *qbuf;
    if(argc == 1) usage(0);
    /* 通过调用 ftok() 生成唯一键 */ key = ftok(".", 'm');
    /* 打开队列 - 如果需要则创建 */ if((msgget(key, IPC_CREAT|0660)) == -1) { error("msgget"); exit(1); }
    switch(tolower(argv[1][0])) { 
        case 's': send_message(msgqueue_id, qbuf, atol(argv[2]), argv[3]); break; 
        case 'r': read_message(msgqueue_id, &qbuf, atol(argv[2])); break; 
