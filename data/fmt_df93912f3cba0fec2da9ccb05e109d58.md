
```c
sigemptyset(&blockMask);       /* 阻塞信号 *///

	if (sigprocmask(SIG_BLOCK, &blockMask, &origMask) == -1)

		perror("sigprocmask");

	sigemptyset(&sa.sa_mask);

	sa.sa_flags = SA_RESTART;

	sa.sa_handler = handler;

	if (sigaction(SYNC_SIG, &sa, NULL) == -1)

		perror("sigaction");

	switch (childPid = fork()) {

	case -1:

		perror("fork");

	case 0: /* 子进程在此处执行所需的动作... *///

		printf("%s Child started - doing some work\n", currTime("%T"), (long) getpid());

		sleep(2);

        /* 模拟执行工作花费的时间 */

		/* 并通知父进程已完成 *///

		printf("%s Child about to signal parent\n", currTime("%T"), (long) getpid());

		if (kill(getppid(), SYNC_SIG) == -1)

			errXit("kill");

        /* 新子进程可以做其他事情... *///

		exit(EXIT_SUCCESS);

	default: /* 父进程 */

        /* 父进程在此处某些工作，然后等待子进程完成所需的动作 */

		printf("%s Parent about to wait for signal\n", currTime("%T"), (long) getpid());

		sigemptyset(&emptyMask);

		if(sigsuspend(&emptyMask) == -1 && errno != EINTR)

			errXit("sigsuspend");

		printf("%s Parent got signal\n", currTime("%T"), (long) getpid());

		/* 如果需要，将信号掩码恢复到原始状态 */

		if (sigprocmask(SIG_SETMASK, &origMask, NULL) == -1)

			errXit("sigprocmask");

        /* 父进程继续做其他事情... *///

		exit(EXIT_SUCCESS);

	}

}
```

`proceexec/fork_sig.c`

# 24.6 总结

`fork()` 系统通过创建调用调用进程（父进程）的几乎完全相同的副本来创建一个新进程（子进程）。`vfork()` 系统是 `fork()` 更高效的版本，但通常会被避免，因为它具有不寻常的语义：子进程在执行 `exec()` 或终止之前会一直使用父进程的内存；在此期间，父进程的执行会被挂起。

在 `fork()` 之后，我们无法依赖父进程和子进程下一次调度使用 CPU 的顺序。那些对执行顺序做出假设的程序容易受到被称为“竞态条件”（race conditions）的错误影响。由于此类错误的发生取决于系统负载等外部因素，因此它们可能很难发现和调试。

# 进一步信息

[Bach, 1986] 和 [Goodheart & Cox, 1994] 提供了 UNIX 系统上 `fork()`、`execve()`、`wait()` 和 `exit()` 的实现细节。[Bovet & Cesati, 2005] 和 [Love, 2010] 提供了 Linux 特有的进程创建和终止的实现细节。

# 24.7 练习题

- 24-1. 程序执行完以下系列 `fork()` 调用后，会产生多少个新进程（假设没有调用失败）？

```
fork();
fork();
fork();
```

- 24-2. 写一个程序，证明在 `vfork()` 之后，子进程可以关闭文件描述符（例如描述符 0），而不影响父进程中对应的文件描述符。

- 24-3. 假设我们可以修改程序源代码，我们如何在让进程继续执行的同时，获取某一时刻进程的核心转储（core dump）？

- 24-4. 在其他 UNIX 实现上对列表 24-5 中的程序（`fork_whos_on_first.c`）进行实验，以确定这些实现如何在 `fork()` 之后调度父进程和子进程的。

- 24-5. 假设在列表 24-6 的程序中，子进程也需要等待父进程完成某些动作。程序需要哪些更改？

# 25 进程终止

本章描述了进程终止时会发生什么。我们首先描述 `exit()` 和 `_exit()` 的用法。然后讨论 `fork()`、`stdio` 缓冲区与 `exit()` 之间的交互。最后我们考虑信号的使用。

## 25.1 终止进程：_exit() 和 exit()

进程可以通过两种一般方式终止。其中一种是异常终止，由递送信号引起，如 20.1 节所述。另一种是进程可以使用 `exit()` 正常终止。

```c
#include <unistd.h>
void _exit(int status);
```

传递给 `_exit()` 的 `status` 参数定义了终止状态。与 UNIX 特有的 `_exit()` 不同，`exit()` 被定义为标准库的一部分；这意味着它在每个实现中都可用。

程序通常不会直接调用 `_exit()`，而是调用 `exit()` 库函数，在 `_exit()` 之前执行各种动作。

```c
#include <stdlib.h>
void exit(int status);
```

`exit()` 的 `status` 参数对父进程可见。虽然可以将 0 到 255 范围内的任何值传递给 `exit()`，但大于 128 的值可能会在 shell 脚本引起混淆。原因是当命令被信号终止时，shell 通过设置变量 `$?` 来指示这一事实，这与进程调用 `_exit()` 相同值的情况是无法区分的。

按照惯例，状态为 0 表示进程成功完成，非零状态表示进程执行失败。对于如何解释非零值没有固定规则；不同的应用程序遵循自己的规则。SUS3 规定了两个常量，`EXIT_SUCCESS` (0) 和 `EXIT_FAILURE` (1)，它们在大多数程序中使用。

进程终止的另一种方式是从 `main()` 函数返回，无论是显式的还是隐式的（通过运行到 `main()` 函数末尾）。执行显式 `return n` 通常等同于调用 `exit(n)`，调用 `main()` 的运行时函数使用 `main()` 的返回值来调用 `exit()`。

未指定值的返回或运行到 `main()` 函数末尾也会导致 `main()` 的调用者调用 `exit()`，但结果取决于支持的 C 标准版本和采用的编译选项：

- 在 C89 中，这些情况下的行为是未定义的；程序可能会以任意状态值终止。这是 Linux 上的 `gcc` 默认的行为，其中程序的退出状态来自栈上或特定 CPU 寄存器中的某个随机值。应该避免以这种方式终止程序。

> 在调用 `exit()` 和从 `main()` 返回之间存在不等效的情况。如果 `exit` 期间执行的任何步骤访问了 `main()` 的局部变量，那么从 `main()` 返回将导致未定义行为。例如，如果某个 `main()` 的局部变量被指定在 `setbuf()` 或 `setenv()` 调用（第 13.2 节）中可能会发生这种情况。

+ C99 标准要求主程序的末尾结束等同于调用 `exit(0)`。在 Linux 上，如果我们使用 `gcc -std=c99` 编译程序，就会得到这种行为。

## 25.2 进程终止的细节

在进程的正常和异常终止期间，会发生以下操作：

- 打开的文件描述符、目录流（第 18.8 节）、消息目录描述符（`catopen()` 和 `catgets()` 手页）以及转换描述符（`iconv_open()` 手页）将被关闭。
- 由于关闭了文件描述符，该进程持有的任何文件锁（第 55 章）将（释放。
- 任何附加的系统共享内存段将分离，并且每个段对应的 `shmn` 计数器减 1（参见第 48.8 节）。
- 对于每个 V 信号量，信号量值增加一个 `semadij` 值。（参见第 47.8 节）。
- 如果该进程是控制终端的控制进程，则向控制终端前台组中的每个进程发送 `SIGUP` 信号，并将终端与会话解离。我们在第 34.6 节中进一步讨论这一点。
- 调用进程中打开的任何 POSIX 命名信号量都将被关闭，仿佛调用了 `sem_close()` 一样。
- 调用进程中打开的任何 POSIX 消息队列都将被关闭，仿佛调用了 `mq_close()` 一样。
- 如果由于此进程退出导致进程组变成孤儿且该组中有任何停止的进程，则组中的所有进程都将收到一个 `SIGCONT` 信号，随后是一个 `SIGKILL` 信号。我们在第 34.7.4 节中进一步讨论这一点。
- 该进程使用 `mlock()` 或 `mockall()`（第 50.2 节）建立的任何内存锁都将被移除。
- 该进程使用 `mmap()` 建立的任何内存映射将被取消。

## 25.3 退出处理程序 (Exit Handlers)

有时，应用程序需要在进程终止时自动执行某些操作。考虑应用程序库的例子，如果它在进程生命周期内使用，则需要在进程退出时自动执行某些清理工作。库无法控制进程何时以及如何退出，也无法强制主程序在退出前调用库特定的清理函数，但可以保证清理操作的发生。在这种情况下，一种方法是使用退出处理程序（旧的 System V 方法使用“程序终止例程”这一术语）。

退出处理程序是程序员提供的函数，它在进程生命周期中的某一点被注册，然后在进程正常终止期间通过 `exit()` 自动调用。如果程序调用了 `exit()` 或进程被信号异常终止，则不会调用退出处理程序。

在某种程度上，当进程被信号终止时不调用退出处理程序，这一事实限制了它们的效用。我们能做的最好的办法是为可能发送给进程的信号建立处理程序，并让这些处理程序设置一个标记，导致主程序调用 `exit`（因为 `exit()` 不是第 426 页表 21-1 中的异步安全函数之一，我们我们通常不能在信号处理程序中调用它）。即便如此，这也没有处理 `SIGKILL` 的情况，因为该信号的默认操作是无法更改的。这是我们应该避免使用 `SIGKILL` 终止进程的另一个原因（如第 20.2 节所述），而应使用 `SIGTERM`，它是 `kill` 命令的默认信号。

### 注册退出处理程序

GNU C 库提供了两种注册退出处理程序的方法。第一种方法在 SUS3 中指定，是使用 `atexit()` 函数。

```
#include <stdlib.h>
atexit(void (*func)(void));
```

成功时返回 0，出错时返回非零

`atexit` 函数将 `func` 添加到一个进程终止时调用的函数列表中。函数 `func` 应该定义为不接受参数且没有返回值，因此形式如下：

```
void
func(void)
{
    /* 执行某些操作 */
}
```

注意 `atexit()` 在出错时返回非零值（不一定是 -1）。可以注册多个退出处理程序（甚至可以多次注册同一个退出处理程序）。当程序调用 `exit()` 时，这些函数按照注册顺序的反序被调用。这种顺序是有逻辑的，因为通常情况下较早注册的函数是执行基础类型清理工作的函数，这些工作可能需要在较后注册的函数之后执行。

本质上，在退出处理程序内部可以执行任何所需的操作，包括注册退出处理程序，这些程序将被放置在待调用的退出处理程序列表的头部。然而，如果其中一个退出处理程序未能返回——是因为它调用了 `exit()` 或者是因为进程被信号终止（例如，退出处理程序调用了 `raise()`）——剩余的退出处理程序将不再被调用。此外，通常由 `exit()` 执行的操作（刷新缓冲区）也不会执行。

SUS3 规定，如果退出处理程序本身调用了 `exit()`，结果是未定义的。在 Linux 上，剩余的退出处理程序会正常被调用。但在某些系统上，这会导致所有退出处理程序都被调用，从而导致无限递归（发生栈溢出）。可移植应用程序应避免在退出处理程序内部调用 `exit()`。

SUSv3 要求实现必须允许注册至少 32 个退出处理程序。通过 `syscall(SC_ATEXIT_MAX)`，程序可以确定实现定义的注册处理程序数量的上限。（然而，没有方法可以发现已经注册了多少处理程序）。通过链式，`glibc` 允许允许无限数量的处理程序。

### 示例程序

列表 25-1 展示了如何使用 `atexit()` 和 `on_exit()` 来注册处理程序。当我们运行这个程序时，会看到以下输出：

```
$ ./exit_handlers
on_exit function called: status=2, arg=20
atexit function 2 called
atexit function 1 called
on_exit function called: status=2, arg=10
```

列表 25-1: 使用退出处理程序

```c
#define BSD_SOURCE    /* 从 <stdlib.h> 获取 on_exit() 声明 */
#include <stdlib.h>
#include <tlpi.h>
static void
atexitFunc1(void)
{
    printf("atexit function 1 called\n");
}
static void
atexitFunc2(void)
{
    printf("atexit function 2 called\n");
}
static void
onexitFunc(int exitStatus, void *arg)
{
    printf("on_exit function called: status=%d, arg=%ld\n",
           exitStatus, (long) arg);
}
int
main(int argc, char *argv[])
{
    /* ... 实现细节 ... */
}
```

```c
  if (on_exit(onexitFunc, (void *) 10) != 0)
    fatal("on_exit1");
  if (atexit(atexitFunc1) != 0)
    fatal("atexit1");
  if (atexit(atexitFunc2) != 0)
    fatal("atexit2");
  if (on_exit(onexitFunc, (void *) 20) != 0)
    fatal("on_exit2");
  exit(2);
}
```

# fork()、stdio 缓冲区与 _exit() 之间的交互

列表 25-2 中程序的输出展示了一个起初令人困惑的现象。当我们标准输出重定向到终端运行该程序时，我们看到如下结果：

```
$ /fork_stdio_buf
Hello world
Ciao
```

然而，当我们将标准输出重定向到一个文件时，我们看到了以下内容：

```
$ /fork_stdio_buf > a
$ cat a
Ciao
Hello world
Hello world
```

在上述输出中，我们看到了两个奇怪的现象：`printf()` 写入的行出现了两次，且 `write()` 的输出在 `printf()` 之前。

列表 25-2：fork() 与 stdio 缓冲的交互

```c
#include <tlpi_hdr.h>
int
main(int argc, char *argv[])
{
  printf("Hello world\n");
  write(STDOUT_FILENO, "Ciao\n", 5);
  if (fork() == -1)
```
