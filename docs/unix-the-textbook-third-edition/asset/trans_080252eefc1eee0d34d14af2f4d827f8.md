

线程中访问共享数据的代码段被称为临界区。因此，访问共享数据的多个临界区必须互斥地执行，一个接一个地执行。换句话说，当有对多个临界区执行的同时请求时，这些临界区的执行必须被序列化。如何实现这种互斥被称为临界区问题。文献中提供了几种解决该问题的方案。然而，对该主题的进一步讨论超出了本书的范围。如果你有兴趣了解更多关于该主题的内容，你可以阅读一本关于操作系统原理或操作系统概念的教科书。

## EXERCISE 19.3

浏览网络并写下除我们在第 19.2.5 节中讨论过的之外，可用于用户级线程的三种线程库的名称。

## EXERCISE 19.4

Bakery Algorithm 是 N 进程临界区问题的优雅解决方案。浏览网络或查阅一本关于操作系统原理和概念的书籍，了解该算法的作者姓名。作者是谁？

## 19.3 PROCESS MANAGEMENT CONCEPTS

进程管理包含多项内容，从进程创建到终止以及中间的一切，包括挂起一个进程，让一个进程等待某个事件例如子进程的终止，向一个进程发送信号（软件中断），处理信号，在一个进程中设置闹钟，以及在 PPFDT 中复制文件描述符。表 19.1 显示了一些用于进程管理的系统调用。

TABLE 19.1 The UNIX System Calls for Process Management

|  |  |
|---|---|
| fork() | 创建调用进程的克隆（即子进程） |
| execve() | 覆盖调用进程的主内存映像 |
| wait() | 挂起调用进程并等待子进程终止 |
| waitpid() | 等待具有给定 PID 的进程终止 |
| exit() | 终止调用进程并将状态返回给该进程的父进程 |
| getpid() | 获取调用进程的 PID |
| getppid() | 获取调用进程的父进程的 PPID |
| getuid() | 获取调用进程所有者的 UID |
| getgid() | 获取调用进程所有者的 GID |
| signal() | 通过忽略它、采取默认（内核定义）操作或采取为相关信号指定的程序员定义操作来处理信号 |
| kill() | 向一个进程发送特定类型的信号；通常用于终止一个进程 |
| alarm() | 为给定秒数设置闹钟信号 |
| dup(), dup2() | 在 PPFDT 中复制文件描述符 |

## EXERCISE 19.5

浏览 execve() 系统调用的手册页并列出此调用的所有变体名称，包括系统调用和库调用。

## EXERCISE 19.6

浏览 wait() 系统调用的手册页并列出此调用的所有变体名称，包括系统调用和库调用。

### 19.3.1 Getting the Process ID and the Parent Process ID

你可以使用 getpid() 和 getppid() 调用来显示进程的 ID（PID）及其父进程的 ID（PPID）。以下是这些调用的简要描述。

```
#include <sys/types.h>
#include <unistd.h>
pid_t getpid();
Success: The ID of the process (PID)
Failure: -1 and kernel variable errno set to indicate the type of error
```

```
#include <sys/types.h>
#include <unistd.h>
pid_t getppid();
Success: The ID of the parent process (PPID)
Failure: -1 and kernel variable errno set to indicate the type of error
```

以下会话中的 pids.c 程序展示了这些调用的使用。编译和运行此程序会显示进程的 PID（26438）及其父进程的 PID（16733）。请注意，进程的父进程是登录 shell（-csh），其 PID 为 16733，如 ps 命令的输出所示。

```
% cat pids.c
void main(void)
{
    printf("Child's PID = %d\n", getpid());
    printf("Parent's PID = %d\n", getppid());
}
% gcc48 -w pids.c -o pids
% ./pids
Child's PID = 26438
Parent's PID = 16733
% ps
PID TT  STAT  TIME COMMAND
16733 1  Ss  0:02.23 -csh (csh)
26830 1  R+  0:00.01 ps
%
