
## 套接字控制

在套接字打开期间，你可以将其配置为以各种方式运行。本节描述了相关的 API 调用。

### setsockopt()

更改套接字 `sd` 的行为。每个选项都有一个值（某些选项是只读或只写的）。你可以通过 `optval` 和 `optlen` 设置每个选项。完整的选项列表，请参见附录 A。

#### 原型

```c
#include <sys/types.h>
#include <sys/socket.h>
int setsockopt(int sd, int level, int optname,
               const void *optval, socklen_t optlen);
```

#### 返回值

如果一切正常，则返回零。如果发生错误，你可以在 `errno` 中找到原因。

#### 参数

| 参数 | 描述 |
| :--- | :--- |
| `sd` | 要修改的套接字 |
| `level` | 特性层级（`SOL_SOCKET`, `SOL_IP`, `SOL_TCP`, `SOL_IPV6`） |
| `optname` | 要修改的选项 |
| `optval` | 指向新值的指针 |
| `optlen` | 值的长度（以字节为单位） |

#### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EBADF` | 参数 `sd` 不是有效的描述符。 |
| `ENOTSOCK` | 参数 `sd` 是一个文件，而不是套接字。 |
| `ENOPROTOOPT` | 在指定的层级中，该选项未知。 |
| `EFAULT` | `optval` 指向的地址不在进程地址空间的有效部分中。 |

#### 示例

```c
const int TTL=128;
/*---Change the time-to-live to 128 hops---*/
if ( setsockopt(sd, SOL_IP, SO_TTL, &TTL, sizeof(TTL)) != 0 )
    perror("setsockopt() failed");
```

### getsockopt()

获取套接字配置。

#### 原型

```c
#include <sys/types.h>
#include <sys/socket.h>
int getsockopt(int sd, int level, int optname, void *optval,
               socklen_t *optlen);
```

#### 返回值

如果一切正常，则返回零。如果发生错误，你可以在 `errno` 中找到原因。

#### 参数

| 参数 | 描述 |
| :--- | :--- |
| `sd` | 要读取的套接字。 |
| `level` | 特性层级（`SOL_SOCKET`, `SOL_IP`, `SOL_TCP`, `SOL_IPV6`）。 |
| `optname` | 要修改的选项。 |
| `optval` | 值的存储位置。 |
| `optlen` | 值的长度（以字节为单位）。此字段按引用传递。 |

#### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EBADF` | 参数 `sd` 不是有效的描述符。 |
| `ENOTSOCK` | 参数 `sd` 是一个文件，而不是套接字。 |
| `ENOPROTOOPT` | 在指定的层级中，该选项未知。 |
| `EFAULT` | `optval` 或 `optlen` 指向的地址不在进程地址空间的有效部分中。 |

#### 示例

```c
int error, size=sizeof(error);
if ( getsockopt(sd, SOL_SOCKET, SO_ERROR, &error,
                &size) != 0 )
{
    perror("getsockopt() failed");
}
printf("socket error=%d\n", error);
```

## 附录 C. 内核 API 子集

### 本附录内容

- 任务
- 线程
- 锁定
- 信号
- 文件等

本附录列出了所有内核库和系统调用的手册页，这些手册页不直接与套接字相关，但通常与套接字一起使用。

### 任务

任务包括进程和线程。线程（pThreads）在下一节中定义；本节涵盖进程和低级任务（克隆）。

#### fork()

在此调用处创建一个新的进程（独立任务）。此调用创建一个子进程，与父进程一起运行。你必须小心捕获子进程并将其导向其分配的任务；否则，子进程将运行父进程所做的每一条语句（它们一起运行）。

##### 原型

```c
#include <unistd.h>
pid_t fork(void);
```

##### 返回值

| 值 | 描述 |
| :--- | :--- |
| 0 | 获得此值的任务是子进程。 |
| >0 | 获得此值的任务是父进程。 |
| <0 | 父进程未能创建新的子进程；请检查 errno。 |

##### 参数

（无）

##### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EAGAIN` | `fork()` 无法分配足够的内存来复制父进程的页表并为子进程分配任务结构。 |
| `ENOMEM` | 由于内存紧张，`fork()` 未能分配必要的内核结构。 |

##### 示例

```c
int PID;
if ( (PID = fork()) == 0 )
{  /*--- CHILD ---*/
    /**** Run the child's assignment ***/
    exit();
}
else if ( PID > 0 )
{  /*--- PARENT ---*/
    int status;
    /**** Do parent's work ****/
    wait(status); /* may be done in SIGCHLD signal handler */
}
else /*--- ERROR ---*/
    perror("fork() failed");
```

#### __clone()

这是一个用于创建任务的低级系统调用。你可以直接控制父进程和子进程之间共享的内容。这不是面向业余编程人员的；你可以创建非常不可预测的程序。（有关此调用的完整描述，请参见第 7 章“负载分担：多任务处理”。）

##### 原型

```c
#include <sched.h>
int __clone(int (*fn) (void* arg), void* stacktop, int flags, void* arg);
```

##### 返回值

`进程 ID` 如果为负值，`errno` 包含确切的错误代码。

##### 参数

| 参数 | 描述 |
| :--- | :--- |
| `fn` | 子任务的入口点。创建一个接受 `void*` 参数参数的函数（或过程）。当该例程尝试返回时，操作系统会为你终止该任务。 |
| `stacktop` | 你必须为子任务创建一个堆栈。此参数指向该堆栈的顶部（数据块的最高地址）。由于你提供了堆栈，堆栈的大小是固定的，并且不能像正常任务的堆栈那样增长。 |
| `flags` | 两种类型的信息算术或在一起：要共享的 VM 空间和终止信号。此标志支持所有信号类型，并且当任务终止时，操作系统会引发你定义的信号。可用的 VM 空间如下： |
| | - `CLONE_VM`：在任务之间共享数据空间。使用此标志共享所有静态数据、预初始化数据和分配堆。否则，复制数据空间。 |
| | - `CLONE_FS`：共享文件系统信息：当前工作目录、根文件系统和默认文件创建权限。否则，复制设置。 |
| | - `CLONE_FILES`：共享打开的文件。当一个任务更改文件指针时，其他任务会看到此更改。同样，如果任务关闭文件，其他任务将无法再访问该文件。否则，为打开的 inode 创建新的引用。 |
| | - `CLONE_SIGHAND`：共享信号表。单个任务可以选择忽略打开的信号（使用 `sigprocmask()`），而不影响同级别的任务。否则，复制表。 |
| | - `CLONE_PID`：共享进程 ID。小心使用此标志；并非所有现有工具都支持此功能。PThreads 库不使用此选项。否则，分配新的 PID。 |
| `arg` | 你可以使用此参数传递任何数据值的指针引用。当操作系统完成创建子任务后，它会使用 `arg` 参数调用例程 `fn`。如果你使用此功能，请确保将 `arg` 指向的值放在共享数据区域（`CLONE_VM`）中。 |

##### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EAGAIN` | `__clone()` 无法分配足够的内存来复制父进程的页表并为子进程分配任务结构。 |
| `ENOMEM` | 由于内存紧张，`__clone()` 未能分配必要的内核结构。 |

##### 示例

```c
#define STACKSIZE   1024
void Child(void* arg)
{
    /*---child's responsibility---*/
    exit(0);
}

int main(void)
{
    int cchild;
    char *stack=malloc(STACKSIZE);
    if ( (cchild = __clone(&Child, stack+STACKSIZE-1,
            SIGCHLD, 0)) == 0 )
    {
        /* Child code */
    }
}
```

#### exec()

运行外部程序（二进制文件或首行包含 `#! <interpreter> [arg]` 的可执行脚本）。此调用用外部程序的上下文替换当前正在运行的任务。新程序保留调用者的 PID 和打开的文件。

调用 `exec1()`、`execl()`、`execle()`、`execv()` 和 `execvp()` 都是 `execve()` 的前端。

##### 原型

```c
#include <unistd.h>
int execve(const char* path, char* const argv[], char* const envp[]);
int execl(const char* path, const char* arg, ...);
int execle(const char* file, const char* arg, ...);
int execv(const char* path, char* const argv[], char* const envp[]);
int execvp(const char* path, char* const argv[]);
```

##### 返回值

如果成功，此调用不会返回。如果失败，返回值为 −1。

##### 参数

| 参数 | 描述 |
| :--- | :--- |
| `file` | 要执行的程序。该调用使用定义的 `PATH` 在此变量中查找名称。 |
| `path` | 要执行的程序的绝对路径和文件名。 |
| `argv` | 命令行参数的字符串数组。第一个数组元素值必须是 `arg0`（或程序名称）。最后一个数组元素始终为零（`0`）。 |
| `arg` | 命令行参数。这后面跟着省略号（…），表示有多个参数。第一个 `arg` 始终是程序的名称，最后一个 `arg` 始终为零（`0`）。 |
| `envp` | 环境参数的字符串数组。每个参数形式为 `<param>`=`<value>`（例如，`TERM`=`vt100`）。最后一个数组元素始终为零（`0`）。 |

##### 可能的错误
