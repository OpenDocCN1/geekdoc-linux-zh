
## 示例

```c
int i;
struct hostent *host;
host = gethostbyname("sunsite.unc.edu");
if (host != NULL)
{
    printf("Official name: %s\n", host->h_name);
    for (i = 0; host->h_aliases[i] != 0; i++)
        printf("  alias[%d]: %s\n", i,
               host->h_aliases[i]);
    printf("Address type=%d\n", host->h_addrtype);
    for (i = 0; i < host->h_length; i++)
        printf("Addr[%d]: %s\n", i,
               inet_ntoa(host->h_addr_list[i]));
}
else
    perror("sunsite.unc.edu");
```

## getprotobyname()

此函数读取 /etc/protocol 文件以获取与 pname 匹配协议。你可以使用此调用将诸如 HTTP、FTP 和 Telnet 等名称转换为它们的默认端口号。

### 原型

```c
#include <netdb.h>
struct protent *getprotobyname(const char *pname);
```

### 返回值

如果成功，该调用返回指向 protent 的指针（在本附录后面定义）。否则，返回 NULL。

```c
struct protent {
    char        *p_name;        /* 官方协议名称 */
    char        **p_aliases;    /* 别名列表 */
    int         p_proto;        /* 协议号 */
};
```

字段 p_proto 是协议号。

### 参数

- pname: 协议名称。这可以是任何被识别的协议名称或别名。

### 可能的错误

- （未设置 errno）

### 示例

```c
#include <netdb.h>
...
int i;
struct protoent *proto = getprotobyname("http");
if (proto != NULL)
{
    printf("Official name: %s\n", proto->p_name);
    printf("Port#: %d\n", proto->p_proto);
    for (i = 0; proto->p_aliases[i] != 0; i++)
        printf("Alias[%d]: %s\n", i+1,
               proto->p_aliases[i]);
}
else
    perror("http");
```

## 套接字控制

在套接字打开期间，你可以配置它以各种方式运行。本节描述了 API 调用。

### setsockopt( )

更改套接字 sd 的行为。每个选项都有一个值（某些选项是只读或只写的）。你可以通过 optval 和 optlen 来设置每个选项。有关选项的完整列表，请参阅附录 A。

**原型**

```c
#include <sys/types.h>
#include <sys/socket.h>
int setsockopt(int sd, int level, int optname,
               const void *optval, socklen_t optlen);
```

**返回值**

如果一切正常，返回零。如果发生错误，你可以在 errno 中查找原因。

**参数**

| 参数 | 描述 |
| :-------- | :---------- |
| sd | 要修改的套接字 |
| level | 功能级别 (SOL_SOCKET, SOL_IP, SOL_TCP, SOL_IPV6) |
| optname | 要修改的选项 |
| optval | 指向新值的指针 |
| optlen | 值的字节长度 |

**可能的错误**

- EBADF: 参数 sd 不是有效的描述符。
- ENOTSOCK: 参数 sd 是一个文件，而不是套接字。
- ENOPROTOOPT: 在指定的级别下未知该选项。
- EFAULT: optval 指向的地址不在进程地址空间的有效部分中。

**示例**

```c
const int TTL=128;
/*---Change the time-to-live to 128 hops----*/
if (setsockopt(sd, SOL_IP, SO_TTL, &TTL, sizeof(TTL)) != 0)
    perror("setsockopt() failed");
```

### getsockopt()

获取套接字配置。

**原型**

```c
#include <sys/types.h>
#include <sys/socket.h>
int getsockopt(int sd, int level, int optname, void *optval,
               socklen_t *optlen);
```

**返回值**

如果一切正常，返回零。如果发生错误，你可以在 `errno` 中查找原因。

**参数**

- sd: 要读取的套接字。
- level: 功能级别 (SOL_SOCKET, SOL_IP, SOL_TCP, SOL_IPV6)。
- optname: 要修改的选项。
- optval: 存放值的空间。
- optlen: 值的字节长度。此字段通过引用传递。

**可能的错误**

- EBADF: 参数 sd 不是有效的描述符。
- ENOTSOCK: 参数 sd 是一个文件，而不是套接字。
- ENOPROTOOPT: 在指定的级别下未知该选项。
- EFAULT: optval 或 optlen 指向的地址不在进程地址空间的有效部分中。

**示例**

```c
int error, size=sizeof(error);
if (getsockopt(sd, SOL_SOCKET, SO_ERROR, &error,
    &size) != 0)
    perror("getsockopt() failed");
printf("socket error=%d\n", error);
```

## 内核 API 子集

附录

![](img/2591af4bdf00a0f382331fc9481f785e_468_0.png)

### 本附录内容

- 任务 450
- 线程 456
- 锁 460
- 信号 462
- 文件等等 465

本附录列出了内核库和系统调用的所有手册页，这些内容与套接字没有直接关系，但通常与套接字结合使用。

#### 任务

任务包括进程和线程。线程 (`pthread`s) 在下一节中定义；本节涵盖进程和底层任务（克隆）。

#### fork()

在此调用时创建一个新的进程（独立任务）。此调用创建一个子进程与父进程一起运行。你必须小心，你要捕获子进程并将其引导至其分配的任务；否则，子进程会执行父进程执行的每条语句（它们一起运行）。

**原型**

```c
#include <unistd.h>
pid_t fork(void);
```

**返回值**

- 0: 获得此值的任务是子进程。
- >0: 获得此值的任务是父进程。
- <0: 父进程未能创建新的子进程；检查 `errno`。

**参数**

（无）

**可能的错误**

- EAGAIN: `fork()` 无法分配足够的内存来复制父进程的页表并为子进程分配任务结构。
- ENOMEM: `fork()` 因内存紧张而未能分配必要的内核结构。

**示例**

```c
int PID;
if ((PID = fork()) == 0)
{ /*--- CHILD ---*/
      /**** Run the child's assignment ****/
      exit();
}
else if (PID > 0)
{ /*--- PARENT ---*/
      int status;
      /**** Do parent's work ****/
      wait(status); /* may be done in SIGCHLD signal handler */
}
else /*... ERROR ....*/
    perror("fork() failed");
```

#### clone()

这是一个用于创建任务的底层系统调用。你可以直接控制父进程和子进程之间共享的内容。这不是供业余程序员使用的；你可以创建非常不可预测的程序。（有关此调用的完整描述，请参阅第 7 章“划分负载：多任务处理”。）

**原型**

```c
#include <sched.h>
int __clone(int (*fn)(void* arg), void* stacktop, int flags, void* arg);
```

**返回值**

- 进程 ID: 如果为负值，*errno* 包含确切的错误代码。

**参数**

| 参数 | 描述 |
| :--- | :--- |
| *fn* | 子任务的归宿。创建一个接受 *void* 参数论的功能（或过程）。当例程试图返回时，操作系统会为你终止该任务。 |
| *stacktop* | 你必须为子任务创建一个堆栈。此参数指向该堆栈的顶部（数据块的最高地址）。因为你提供了堆栈，所以堆栈的大小是固定的，不能像正常任务的堆栈那样增长。 |
| *flags* | 两种类型信息按位或在一起；要共享的 VM 空间和终止信号。此标志支持所有信号类型，当任务终止时，操作系统会触发你定义的信号。<br>可用的 VM 空间如下：<br>• *CLONE_VM* 在任务之间共享数据空间。使用此标志共享所有静态数据、预初始化数据和分配堆。否则，复制数据空间。<br>• *CLONE_FS* 共享文件系统信息：当前工作目录、根文件系统和默认文件创建权限。否则，复制设置。<br>• *CLONE_FILES* 共享打开的文件。当一个任务更改文件指针时，其他任务会看到更改。同样，如果任务关闭文件，其他任务将无法再访问该文件。否则，创建对打开 inode 的新引用。 |
| | • **CLONE_SIGHAND** 共享信号表。单个任务可以选择忽略打开的信号（使用 `sigprocmask()`）而不影响同伴。否则，复制表。<br>• **CLONE_PID** 共享进程 ID。谨慎使用此标志；并非所有现有工具都支持此功能。PThreads 库不使用此选项。否则，分配新的 PID。 |
| *arg* | 你可以使用此参数传递指向任何数据值的指针引用。当操作系统完成创建子任务时，它会使用 `arg` 参数调用例程 `fn`。如果你使用此功能，请确保将 `arg` 指向的值放置在共享数据区域 (`CLONE_VM`) 中。 |

**可能的错误**

- EAGAIN: `__clone()` 无法分配足够的内存来复制父进程的页表并为子进程分配任务结构。
- ENOMEM: `__clone()` 因内存紧张而未能分配必要的内核结构。

**示例**

```c
#define STACKSIZE     1024

void Child(void* arg)
{
       /*---child's responsibility---*/
       exit(0);
}

...
int main(void)
{
       int cchild;
       char *stack=malloc(STACKSIZE);

       if ((cchild = __clone(&Child, stack+STACKSIZE-1,
                               SIGCHLD, 0)) == 0 )
```

#### exec()

运行外部程序（二进制文件或第一行带有 `#! <interpreter> [arg]` 的可执行脚本）。此调用用外部程序的上下文替换当前运行的任务。新程序保留调用者的 PID 和打开的文件。

调用 `exec1()`、`exec1p()`、`execl()`、`execv()` 和 `execvp()` 都是 `execve()` 的前端。

