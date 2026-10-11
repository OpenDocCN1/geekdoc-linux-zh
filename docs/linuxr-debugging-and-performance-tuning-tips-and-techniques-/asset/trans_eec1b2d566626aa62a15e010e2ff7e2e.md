
## 9.1.5.3 退出函数

自愿终止程序的另一种方式是调用退出函数。C 标准定义了以下函数：

```c
#include <stdlib.h>              ISO C
void exit(int status);
void _Exit(int status);
int atexit(void (*function)(void));
```

这些函数的工作方式如下：

**void exit(int status)**

该函数终止程序。*status* 会被传递给系统，以便父进程恢复。在程序退出之前，`exit()` 会调用所有通过 `atexit()` 注册的函数，刷新并关闭所有打开的 `<stdio.h>` `FILE *` 流，并删除通过 `tmpfile()` 创建的任何临时文件（参见 12.3.2 节“创建和打开临时文件（最佳实践）”，第 441 页）。当进程退出时，内核会关闭任何剩余打开的文件（那些通过 `open()`、`creat()` 或文件描述符继承打开的文件），释放其地址空间，并释放其可能使用的其他资源。`exit()` 永不返回。

**void _Exit(int status)**

该函数基本上与 POSIX 的 `_exit()` 函数相同；我们将稍后讨论它。

**int atexit(void (*function)(void))**

*function* 是一个指向回调函数的指针，该函数将在程序退出时被调用。`exit()` 在关闭文件和终止之前会调用该回调函数。其想法是应用程序可以提供一个或多个清理函数，在最终关闭之前运行。提供函数被称为注册它。（`nftw()` 的回调函数在 8.4.3.2 节“nftw() 回调函数”第 263 页中描述过；这里的想法是相同的，尽管 `atexit()` 每个注册函数只调用一次。）

`atexit()` 成功时返回 0，出错时返回 -1，并相应地设置 *errno*。

以下程序没有做有用的工作，但它确实展示了 `atexit()` 的工作方式：

```c
/* ch09-atexit.c --- demonstrate atexit().
     Error checking omitted for brevity. */

/*
 * The callback functions here just answer roll call.
 * In a real application, they would do more.
 */

void callback1(void) { printf("callback1 called\n"); }
void callback2(void) { printf("callback2 called\n"); }
void callback3(void) { printf("callback3 called\n"); }

/* main --- register functions and then exit */

int main(int argc, char **argv)
{
    printf("registering callback1\n");  atexit(callback1);
    printf("registering callback2\n");  atexit(callback2);
    printf("registering callback3\n");  atexit(callback3);

    printf("exiting now\n");
    exit(0);
}
```

运行时的情况如下：

```text
$ ch09-atexit
registering callback1                 主程序运行
registering callback2
registering callback3
exiting now
                                      回调函数按相反顺序运行
callback3 called
callback2 called
callback1 called
```

如示例所示，通过 `atexit()` 注册的函数按注册的相反顺序运行：最近注册的先运行。（这也称为 *后进先出*，缩写为 LIFO。）

POSIX 定义了 `_exit()` 函数。与调用回调函数并进行 `<stdio.h>` 清理的 `exit()` 不同，`_exit()` 是“立即死亡”函数：

```c
#include <unistd.h>              POSIX

void _exit(int status);
```

*status* 与 `exit()` 一样传递给系统，但进程立即终止。内核仍然会执行常规的清理工作：关闭所有打开的文件，释放地址空间使用的内存，并释放进程使用的任何其他资源。

在实践中，ISO C 的 `_Exit()` 函数与 `_exit()` 相同。C 标准指出，`_Exit()` 是否调用通过 `atexit()` 注册的函数并关闭打开的文件是**实现定义的**。对于 glibc 系统，它不调用这些函数，行为类似于 `_exit()`。

使用 `_exit()` 的时机是在分叉的子进程中 `exec` 失败时。在这种情况下，你不希望使用常规的 `exit()`，因为那会刷新由 `FILE *` 流持有的任何缓冲数据。当父进程稍后刷新其缓冲区的副本时，缓冲数据会被写入两次；显然这不是好事。

例如，假设你想运行一个 shell 命令，并自行进行 fork 和 exec。这样的代码看起来像这样：

```c
char *shellcommand = "...";
pid_t child;

if ((child = fork()) == 0) { /* child */
    exec1("/bin/sh", "sh", "-c", shellcommand, NULL);
    _exit(errno == ENOENT ? 127 : 126);
}
/* parent continues */
```

*errno* 测试和退出值遵循 POSIX shell 使用的约定。如果请求的程序不存在（ENOENT——目录中没有该项），则退出值为 127。否则，文件存在但因其他原因无法 exec，因此退出状态为 126。在自己的程序中也遵循此约定是个好主意。

简而言之，为了充分利用 `exit()` 和 `atexit()`，你应该做以下事情：

- 定义一小套退出状态值，你的程序将使用这些值向其调用者传达信息。在代码中使用 `#define` 常量或 `enum` 来定义它们。
- 决定为使用 `atexit()` 提供回调函数是否有意义。如果有，在 `main()` 中的适当位置注册它们；例如，在解析选项之后，以及在回调函数需要清理的数据结构初始化之后。请记住，这些函数按 LIFO（后进先出）顺序调用。
- 在任何地方使用 `exit()` 在出现问题且退出是正确操作时退出程序。使用你定义的错误代码。
- 例外是 `main()`，如果你想的话可以使用 `return`。我们的风格通常是遇到问题时使用 `exit()`，在 `main()` 末尾一切顺利时使用 `return 0`。
- 如果 `exec()` 失败，在子进程中使用 `_exit()` 或 `_Exit()`。

## 9.1.6 恢复子进程的退出状态

当进程死亡时，正常的操作过程是内核释放其所有资源。内核确实会保留死进程的退出状态，以及有关其生命周期内使用的资源的信息，并且 PID 继续被视为占用。这样的死进程被称为 *僵尸*（zombie）。

父进程，无论是原始父进程还是 `init`，都可以恢复子进程的退出状态。或者，通过使用未被 POSIX 标准化的 BSD 函数，可以同时恢复退出状态和资源使用信息。状态恢复是通过等待进程死亡来完成的：这也称为回收进程（reaping the process）。

等待子进程死亡的机制与我们尚未描述的信号机制之间存在大量的相互作用。先描述哪一个有点像是先有鸡还是先有蛋的问题；我们选择先讨论子进程等待机制，第 10 章“信号”，第 347 页，提供了关于信号的完整故事。

就目前而言，理解信号是通知进程某个事件已发生的一种方式就足够了。进程可以生成发送到自身的信号，或者信号可以由其他进程或终端用户从外部发送。例如，CTRL-C 发送“中断”信号，CTRL-Z 发送作业控制“停止”信号。

默认情况下，许多信号，如中断信号，会导致接收进程死亡。其他信号，如作业控制信号，会导致其改变状态。子进程等待机制可以确定进程是否因信号而死亡，如果是，确定是哪个信号。对于进程停止也是如此，在某些系统中，对于进程继续也是如此。

### 9.1.6.1 使用 POSIX 函数：wait() 和 waitpid()

最初的 V7 系统调用是 `wait()`。较新的基于 BSD 功能的 POSIX 调用是 `waitpid()`。函数声明如下：

```c
#include <sys/types.h> 
#include <sys/wait.h>

pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);
```

`wait()` 等待任何子进程死亡；有关其死亡方式的信息在 `*status` 中返回。（我们稍后会讨论如何解释 `*status`。）返回值是死亡进程的 PID，如果发生错误则为 −1。

如果没有子进程，`wait()` 返回 −1，并将 *errno* 设置为 `ECHILD`（无子进程）。否则，它等待第一个子进程死亡或有信号传入。

`waitpid()` 函数允许你等待特定的子进程退出。它提供了相当大的灵活性，是首选使用的函数。它同样返回死亡进程的 PID，如果发生错误则为 −1。参数如下：

**pid_t pid**

该值指定等待哪个子进程，既按实际 pid 也按进程组。*pid* 值具有以下含义：

| pid | 描述 |
| :--- | :--- |
| < -1 | 等待进程组 ID 等于 pid 绝对值的任何子进程。 |
| -1 | 等待任何子进程。这是 wait() 的工作方式。 |
| 0 | 等待进程组 ID 等于父进程组 ID 的任何子进程。 |
| > 0 | 等待 PID 等于 pid 的特定进程。 |

**int \*status**

这与 `wait()` 相同。`<sys/wait.h>` 定义了各种宏来解释 `*status` 中的值，我们将很快描述。

**int options**

这应该是 0 或以下一个或多个标志的按位 OR：

