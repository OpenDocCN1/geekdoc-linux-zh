
现在假设你想创建一个键值为 `0111` 的消息队列。你还想知道队列是否已存在，因此在这个示例中使用了 `IPC_EXCL`：

```c
// 创建一个新的消息队列
msgid = msgget(0111, IPC_CREATE | IPC_EXCL | 0666);
if (msgid == -1) {
    printf("Queue already exists...\n");
} else {
    printf("Queue created...\n");
}
```

你可能问过自己一个有趣问题：如何使用可能不唯一的 ID 来协调队列的创建？如果有人已经使用了 `0111` 会怎样？幸运的是，你必须以系统范围的方式创建键以确保唯一性。`ftok` 函数提供了使用文件系统中的文件和一个数字来创建唯一队列的方法。由于文件（及其路径）默认在文件系统中是唯一的，因此很容易创建一个唯一键。看一个使用 `ftok` 创建唯一键的示例。假设路径为 `/home/user/queues/myqueue` 的文件存在。

```c
key_t myKey;
int msgid;
// 根据定义的路径和数字创建键
myKey = ftok("/home/user/queues/myqueue", 0);
msgid = msgget(myKey, IPC_CREATE | 0666 );
```

这为该路径和数字创建了一个键；生成的相同的键。因此，它提供了一种基于文件系统中文件的生成键的有用方法。此示例中的唯一区别在于你没有提供命令，只提供了键：

```c
msgid = msgget(0111, 0);
if (msgid == -1) {
    printf("Queue doesn't exist...\n");
}
```

在这种情况下，`msgflag`（`msgget` 的第二个参数）为 0，这指示此 API 函数正在寻找已存在的消息队列。

关于消息队列的最后一点与创建消息队列时给出的默认设置有关。消息队列的配置记录在表 16.3 所示的参数中。注意，你无法在 `msgsget` 中更改这些设置。在下一节中，将查看某些可以更改的参数。

# 表 16.3 msgsget 中的消息队列配置和默认值

| 参数 | 默认值 |
|---|---|
| `msg_perm.cuid` | 调用进程的有效 ID（创建者） |
| `msg_perm.uid` | 调用进程的有效 ID（所有者） |
| `msg_perm.cgid` | 调用进程的有效组 ID（创建者） |
| `msg_perm.gid` | 调用进程的有效组 ID（所有者） |
| `msg_perm.mode` | 权限（`msgflag` 的低 9 位） |
| `msg_qnum` | 0（队列中的消息数） |
| `msg_lspid` | 0（最后发送消息的进程 ID） |
| `msg_lrpid` | 0（最后接收消息的进程 ID） |
| `msg_stime` | 0（最后发送时间） |
| `msg_rime` | 0（最后接收时间） |
| `msg_ctime` | 当前时间（最后更改时间） |
| `msg_qbytes` | 以字节为单位的队列大小（系统限制)—16 KB |

用户可以直接覆盖 `msg_perm.uid`、`msg_perm.gid`、`msg_perm.mode` 和 `msg_qbytes`。关于此主题的更多内容将在下一节。

# msgctl

`msgctl` API 函数提供了三个不同的功能。第一个是读取当前参数集的能力（通过 `IPC_STAT`）。第二个是修改部分参数的能力（通过 `IPC_SET`）。最后，提供了移除消息队列的功能（通过 `IPC_RMID`）。`msgctl` 的原型定义如下：

```c
#include <sys/msg.h>
int msgctl( int msgqid, int cmd, struct msq_ds *buf );
```

## 表格 16.4 可更新的消息队列参数

| 参数 | 描述 |
|---|---|
| `msg_perm.uid` | 消息队列的用户所有者 |
| `msg_perm.gid` | 消息队列组所有者 |
| `msg_perm.mode` | 权限（参见表 16.2） |
| `msg_qbytes` | 消息队列的大小（字节为单位） |

## 列表 16.7 在 msgctl 中设置所有可能的选项（位于光光中的中的 /source/ch16/mqrdset.c）

```c
1: #include <stdio.h>
2: #include <sys/msg.h>
3: #include <unistd.h>
4: #include <sys/types.h>
5: #include <errno.h>
6: #include "common.h"

8: int main() 
9: {
10: int msgid, ret;
11: struct msgid_ds mqid_ds;

13: /* 获取 ID 为 MY_MQ_ID 的消息队列 */
14: msgid = msgsget( MY_MQ_ID, 0 );

16: /*  msgsget 是否成功完成 */
17: if (msgid >= 0) {
18:

19: ret = msgctl(msgid, IPC_STAT, &mqid_ds);

21: mqid_ds.msg_perm.uid = getuid();
22: mqid_ds.msg_perm.gid = getgid();
23: mqid_ds.msg_perm.mode = 0644;
24: mqid_ds.msg_qbytes = 4096;

26: ret = msgctl(msgid, IPC_SET, &mqid_ds);

28: if (ret == 0) {
29:     printf("Parameters successfully changed.\n\n");
30: } else {
31:     printf("Error %d\n", errno);
32: }
33: }

35: return 0;
36: }
```

在第 14 行，你获取消息队列标识符，然后在第 19 行使用它来检索当前的参数集。在第 21 行，你使用 `getuid()` 函数将 `msg_perm.uid`（有效用户 ID）设置为当前有效用户 ID。同样，在第 22 行你使用 `getgid()` 函数设置了 `msg_perm.gid`（有效组 ID）。在第 23 行你设置了模式，在第 24 行你设置了最大队列大小（以字节为单位）。在这种情况下，你将其设置为 4 KB。现在你获取此结构体并使用 `msgctl` API 函数为当前的消息队列设置参数。这是通过 `msgctl` 中的 `IPC_SET` 命令完成的。

![](img/f7bd35eb87a62f74c6f23c07df847dff_311_0.png)

在设置 `msg_perm.mode`（权限）时，你需要知道这传统上被定义为八进制值。注意列表 16.7 的第 23 行，显示了一个前导零，表示该值是八进制的。例如，如果提供十进制值 666 而不是八进制的 0666，则权限将无效，从而导致不可期的行为。出于这个原因，使用表 16.2 所示的符号可能会很有益。

你可以使用 `msgctl` API 函数来识别某些特定的消息队列参数，例如当前消息队列中的消息数量。列表 16.8 示例了可访问参数的收集和打印。

## 列表 16.8 读取当前消息队列设置（位于光盘中的 /source/ch16/mqstats.c）
