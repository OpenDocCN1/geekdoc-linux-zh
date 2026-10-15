
```c
13: int nlen = strlen(varname);      /* 工具字符指针 */

14:                                     /* 变量名的长度 */

15: if (Ivar)

16: return;                          /* 变量已取消设置 */

17:

18: /*

19: * 删除变量：

20: */

21: var = var - nlen - 1;            /* 指向条目起始 */

22:

23: for (cp=var+strlen(var)+1; *cp; cp += z) {

24: z = strlen(cp) + 1;             /* 下一个值的长度 */

25: memmove(var,cp,z);               /* 向上移动 */

26:

27:

28: *var = 0;                         /* 两个空字节标记 vars 的结束 */

29:

30: return;                          /* 成功 */

31: }

```

变量名在第 11 行进行搜索。如果没有找到，函数在第 16 行返回。否则，第 23–26 行的 `for` 循环移动字符串以替换原来被删除变量占据的区域。第 28 行添加第二个空字节以标记变量列表的新结束位置。

## 总结

`globvar` 工具为 Shell 程序提供了一种简单的方法，通过共享内存相互共享动态信息。你已经看到如何使用信号量提供并发保护。你还观察到共享内存中的信号量 IPC ID 等静态项可以安全地无锁访问。作为一个练习，你可能想通过添加 `-k IPC key` 选项进一步增强该工具。这将消除在无关进程之间通信 IPC ID 值的需要。

你已经完成了 IPC 通信集的概览，其中包含了消息队列、信号量和共享内存。下一章将探讨 UNIX 内核映射内存的能力。

# 第 26 章 内存映射文件

内存映射文件允许文件映射到进程的地址空间。这使得程序可以像访问内存中的数组一样访问文件数据，这比使用标准的读写系统调用可能更高效。

接下来的章节将讨论如何在 UNIX 环境中创建和管理这些映射。

# 高级 UNIX 编程

`prot` 参数指示该内存区域所需的内存保护类型。除了 `PROT_NONE`（它必须单独指定）外，`prot` 参数通过以下宏的按位或（OR）组合指定：

| 标志 | 描述 |
| :--- | :--- |
| `PROT_NONE` | 区域不提供任何访问（此标志与其他标志互斥使用）。 |
| `PROT_READ` | 区域授予读取权限。 |
| `PROT_WRITE` | 区域授予写入权限。 |
| `PROT_EXEC` | 内存映射区域内可以执行程序指令。 |

参数标志指定了 `mmap(2)` 函数调用的若干可选功能。可移植的标志位是：

| 标志 | 描述 |
| :--- | :--- |
| `MAP_FIXED` | 映射到参数 `addr` 中指定的地址，如果无法满足该地址则返回错误。通常当 `addr` 不为空空时，如果请求的地址不可接受，将替换为另一个对齐映射的地址。 |
| `MAP_PRIVATE` | 对映射文件的修改将保持私有。未修改的页面由映射相同文件的所有进程共享。当其中一个内存页被修改时，会创建一个原始页的私有副本，该副本仅由当前进程引用。 |
| `MAP_SHARED` | 对映射文件的修改最终将写回文件。所有进程共享这些更改。 |

通常，`fd` 参数必须是一个打开的文件描述符（`MAP_ANON` 除外）。它代表要映射到内存的普通文件或字符特殊文件。但一旦 `mmap(2)` 返回，你可以关闭文件描述符，因为内核维持着该文件的引用。

`offset` 参数通常指定为 0。当使用其他偏移量时，它必须是函数 `getpagesize(3)` 返回的页大小的倍数。否则将返回错误 `EINVAL`。

当 `mmap(2)` 成功时，将返回至少 1 字节映射的起始地址。否则，返回值 `MAP_FAILED`，并将代码存入 `errno`。

FreeBSD 的 `mmap(2)` 支持额外的功能，通过以下标志位选择：

| 标志 | 描述 |
| :--- | :--- |
| `MAP_ANON` | 创建与任何文件关联的映射内存。文件描述符参数必须包含值 -1，且 `offset` 参数被忽略。 |
| `MAP_INHERIT` | 允许进程在执行 `execve(2)` 系统调用后保留内存映射。 |
| `MAP_HASSEMAPHORE` | 通知 UNIX 内核内存映射区域可能存在信号量。这允许内核对互斥锁（mutexes）采取特殊的预防措施。 |
| `MAP_STACK` | 请求创建一个向下增长的栈区域，其大小至少为 `pagelen` 字节。栈顶为返回的指针加上 `pagelen` 字节。此标志意味着 `MAP_ANON`，并强制 `fd` 参数为 -1，且 `offset` 为 0。`prot` 参数必须至少包含 `PROT_READ` 和 `PROT_WRITE`。 |

`MAP_ANON` 标志值并非所有 UNIX 平台都直接支持。Linux 和 IBM AIX 4.3 使用宏名称 `MAP_ANONYMOUS` 代替之。

> 对于没有此 `mmap(2)` 功能的平台，请使用 `MAP_PRIVATE` 标志映射设备 `/dev/zero` 来实现等同 `MAP_ANON` 的操作。

`MAP_INHERIT` 标志允许你在 `execve(2)` 系统调用成功完成后保留内存映射。这是在同一个进程内从一个可执行程序传递数据到另一个程序的巧妙方法，但缺点是其他 UNIX 平台不支持此功能。

`MAP_HASSEMAPHORE` 标志允许程序员向内核提示内存映射中存在互斥锁标志。这允许内核更改对映射的处理方式，从而影响更改同步的方式并可能影响页面的交换状态。这是一项 BSD UNIX 特性。

`MAP_STACK` 位允许你创建栈区域，其内存页随着栈的向下增长而分配。许多平台（包括 HPUX 1.1 和 UnixWare 7）并不支持此选项。

在某些硬件平台上，指定 `PROT_EXEC` 保护也会授予 `PROT_READ`。这是由于平台硬件的限制导致的。

表 26.1 显示了各种 UNIX 平台支持的标志值的交叉引用表。

## 表 26.1 支持的 mmap(2) 功能交叉引用表

| mmap(2) 标志 | FreeBSD | SGI IRI 6.5 | HPUX 11 | UnixWare 7 | Solaris 8 | IBM AIX 4.3 | Linux |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `MAP_SHARED` | X | X | X | X | X | X | X |
| `MAP_PRIVATE` | X | X | X | X | X | X | X |
| `MAP_FIXED` | X | X | X | | | X | X |
| `MAP_ANON` | X | | | | | X | X |
| `MAP_ANONYMOUS` | | | | | | X | |
| `MAP_HASSEMAPHORE` | X | | | | | | | |
| `MAP_INHERIT` | X | | | | | | | |
| `MAP_STACK` | X | | | | | | | |
| `MAP_GROWSDOWN` | | | | | | | X |
| `MAP_AUTOGROW` | | X | | | | | | |
| `MAP_NORESERVE` | | | | | X | | | |
| `MAP_AUTORESV` | | X | | | | | | |
| `MAP_LOCKED` | | | | | | | X | |
| `MAP_ADDR32` | | | X | | | | | |
| `MAP_LOCAL` | | X | | | | | | |
| `MAP_FILE` | | | | | | X | | |
| `MAP_VARIABLE` | | | | | | X | | |

列表 26.2 显示了一个使用内存映射文件根据语言选择系统错误消息的程序。

# 第 26 章 • 内存映射文件 545

```c
116: * 调用语言文件的内存映射：

117:  /*

118:  load_messages();

119:  */

120: /*

121:   * 报告消息：

122:  */

123:  for (x=1; x<MAX_MSGS; ++x) {

124:    printf("error=%d (%s): %s\n",

125:           univ_maclist[x],univ_errlist[x]);

126:  }

127:  return 0;

128: }
```

`main()` 程序通过调用 `load_messages()` 来选择并加载第 118 行中的错误消息。`load_messages()` 函数最初尝试通过第 61 行的 `getenv(3)` 查找环境变量 `MSG_LANG`。该变量会影响错误消息使用的语言，并默认为英语（见第 77 行）。

此演示程序仅使用了前 12 条系统错误消息，该限制由第 13 行的宏 `MAX_MSGS` 确立。该宏还定义了数组 `univ_errlist[]` 的长度以及宏名称 `univ_maclist[]`。第 69–72 行初始化了 `univ_errlist[]` 和 `univ_maclist[]` 数组的默认值。如果没有发生内存映射，则将使用这些默认值。

要映射的消息文件路径在第 77 行形成。文件大小通过第 79–81 行的 `stat(2)` 调用确定。如果无法 `stat(2)` 文件，函数将提前返回，导致错误消息使用默认值（第 80 行）。

第 86 行以只读模式打开消息文件。第 92 行通过 `mmap(2)` 对文件进行映射。由于没有提供具体地址，内核将选择一个合适的地址并分配给变量 `mmap_msgs`。映射区域的长度指定为 `msgs_len+1` 字节。请求额外的字节是为了让程序可以使用空字节终止，从而简化代码。

对该区域的访问将同时允许读取和写入。使用 `MAP_PRIVATE` 标志是为了确保程序所做的任何更改与文件以及映射该文件的其他进程保持分离。允许写入权限的原因在解释 `parse_messages()` 函数时会变得清晰。

第 100 行关闭了消息文件，因为不再需要打开它。在成功调用 `mmap(2)` 后，Unix 内核维护了对文件的自己的引用，因此你的应用程序可以关闭文件。

现在查看第 25–52 行的 `parse_messages()` 函数。第 27 行将 `(void *)` 指针 `ms` 赋给字符指针 `mp`。这指向我们映射文件的开头。第 31 行在文件末尾放置一个空字节以简化此例程的工作。注意，原始的 `mmap(2)` 调用允许了这个额外字节的存在。

# 高级 UNIX 编程

在查看代码如何解析之前，先看一个英语示例消息文件：

```
$ cat errors.english
EPERM 1 Operation not permitted
ENOENT 2 No such file or directory
ESRCH 3 No such process
EINTR 4 Interrupted system call
EIO 5 Input/output error
ENX 6 Device not configured
EZBIG 7 Argument list too long
ENOGEC 8 Exec format error
EBADF 9 Bad file descriptor
ECHILD 10 No child processes
EDEADLK 11 Resource deadlock avoided $
```

消息文件中的每一行都分为一个宏字段、一个 `errno` 值和消息文本本身。此演示仅涵盖了前 12 个代码。

在第 35 行第一次调用 `strtok(3)` 时，参数 `mp` 不为空。这启动了解析过程，但请注意，随后的迭代在此处会提供空指针（见第 33 行的 `for` 循环）。第 35–47 行解析输入行的三个字段。第 49–50 行存储了指向这些消息的指针引用。

此应用程序的 `PRO_WRITE` 保护是必要的，因为 `strtok(3)` 会修改它正在解析的内存。记住，它会在找到的标记末尾放置一个空字节。然而，为了防止这些更改写回消息文件，`MAP_PRIVATE` 标志将更改保留在进程内存中。

一种改进方法是使用一个应用程序创建一个不需要解析的消息文件。然后第二个应用程序只需以只读权限将生成的镜像映射到其内存中即可。这留给你们作为一项练习。

编译列表 26.2 中的程序并在不设置任何语言设置的情况下调用它，会导致其显示默认值：

```
$ make messages
cc -c Wall messages.c
c -o messages messages.o
$ ./messages
errno=1 (EPERM) : Operation not permitted
errno=2 (ENOENT) : No such file or directory
errno=3 (ESRCH) : No such process
errno=4 (EINTR) : Interrupted system call
errno=5 (EIO) : Input/output error
errno=6 (ENXIO) : Device not configured
errno=7 (EZBIG) : Argument list too long
errno=8 (ENOGEC) : Exec format error
errno=9 (EBADF) : Bad file descriptor
errno=10 (ECHILD) : No child processes
errno=11 (EDEADLK) : Resource deadlock avoided $
```

# 列表 26.3 mprotect.c—修改 messages.c 使消息文本变为只读

```
$ diff -c messages.c mprotect.c
*** messages.c Sun Jul 9 18:11:00 2000
+++ mprotect.c Sun Jul 9 18:59:19 2000
n****
*** 1,4 ****
! /* messages.c */
#include <stdio.h>
#include <unistd.h>
-- 1,4 --
! /* mprotect.c */
#include <stdio.h>
#include <unistd.h>
********************
*** 103,108 ****
103,114 --
* 现在解析消息：
*/
parse_messages();
/*
* 现在将消息文本设为只读
*/
if (mprotect(msgs, msgs_len+1,PROT_READ))
    fprintf(stderr,"%s: mprotect (PROT_READ)\n",strerror(errno));
```

`mprotect(2)` 紧随列表 26.3 中的 `parse_messages()` 函数调用。在此时，使用只读状态是理想的，因为这可以防止错误代码修改消息文本。如果尝试更改错误消息文本，将引发 SIGBUS 信号。

# 向内核提供内存使用建议

为了获得最大性能，你可能会发现让应用程序通知 UNIX 内核关于内存区域的状态或其使用模式是有益的。系统调用 `madvise(2)` 可以实现这一目标：

```
#include <sys/types.h>
#include <sys/mman.h>
int madvise(void *addr, size_t len, int behavior);
```
