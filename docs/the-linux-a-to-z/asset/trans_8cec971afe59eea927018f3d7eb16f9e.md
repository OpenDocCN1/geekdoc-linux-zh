
```c
#include <signal.h>

int sigprocmask(int fcn, sigset_t *mask, sigset_t *old);
```

掩码参数指向一个信号掩码值，该值将根据 fcn 的规范应用于进程的信号掩码。fcn 的各个值及其含义如下：

- SIG_BLOCK  mask 指定要额外阻塞的信号；
- SIG_UNBLOCK  mask 给出要解除阻塞的信号集合；
- SIG_SETMASK  mask 成为新的进程信号掩码。

SIGKILL 和 SIGSTOP 信号不能被阻塞，任何尝试这样做都将被静默忽略。

old 参数是指向信号掩码的指针，在调用后将包含之前的信号掩码值，以便在需要时可以稍后恢复。

进程可以通过调用 sigpending() 系统调用来查看是否有任何被阻塞的信号处于挂起状态：

```c
#include <signal.h>

int sigpending(sigset_t *mask);
```

mask 指向的信号掩码将被设置为指示任何挂起的信号。

## 19.3 kill 系统调用

到目前为止所考虑的大多数信号都是由进程状态自动改变、像浮点异常这样的硬件错误生成的，或者是由用户在键盘上通过中断和退出信号进行干预生成的。除此之外，如果进程具有适当的权限，它也可以故意向另一个进程发送任何信号。这是通过使用 kill() 系统调用完成的：

```c
#include <signal.h>
#include <sys/types.h>

int kill(pid_t pid, int sig);
```

sig 参数指定要发送的信号，pid 参数指定发送目标。pid 的各个值具有以下含义：

- pid > 0 这将向进程 ID 为 pid 的进程发送信号 sig。
- pid = 0 向所有与调用进程具有相同进程组 ID 的进程发送信号 sig。
- pid = -1 向系统中除 init 进程和调用进程之外的所有进程发送信号 sig。（这是 Linux 特有的。）
- pid < -1 向所有进程组 ID 与 pid 的绝对值匹配的进程组中的进程发送信号 sig（即向进程组 -pid 发送信号）。

为了使 kill() 发送信号，调用进程的有效用户 ID 必须是 root，或者必须与接收进程的真实用户 ID 或有效用户 ID 匹配。

## 19.4 pause 系统调用

有时你可能希望编写一个需要与其他程序协作才能执行其功能的程序。例如，假设两个进程通过 FIFO 文件进行通信。其中一个进程将创建 FIFO，然后它们都使用它进行通信。

显然，不创建 FIFO 文件的进程需要在另一个进程创建文件后才能继续。实现这种进程同步的一种方法是使用 pause() 系统调用：

```c
#include <unistd.h>

int pause(void);
```

此系统调用除了挂起调用它的进程的执行外什么也不做。如果进程随后接收到已为其设置了信号处理程序的信号，则在处理程序执行后，pause() 调用将返回错误值并将 errno 设置为 EINTR。此返回值和错误条件可以忽略，因为这是 pause() 返回的唯一方式。

因此，一个进程在需要等待另一个进程执行某些操作时将执行 pause() 调用。当操作已执行时，另一个进程可以向暂停的进程发送预先安排的信号，迫使 pause() 返回并允许被信号化的进程恢复执行，知道它所等待的事件现在已经发生。

## 19.5 alarm 系统调用

与信号相关的最后一个系统调用称为 alarm()。此调用的原型为：

```c
#include <unistd.h>

long alarm(long secs);
```

每个进程都有一个与其关联的闹钟计时器，可用于在预设时间过去后向自身发送 SIGALRM 信号。alarm() 调用接受一个参数（secs），即闹钟响起前经过的秒数。如果将零值传递给 alarm()，则会关闭任何当前正在运行的闹钟计时器。

alarm() 的返回值是之前的闹钟计时器值。如果当前未设置计时器，则为零；或者在调用时时钟剩余的时间。

## 练习

- 1. 编写一个 C 程序，捕获所有可以捕获的信号，并在进程接收到任何信号时显示合适的消息。
- 2. 编写一个程序，读取并显示在键盘上输入的字符。设置一个 alarm()，如果在很短的时间内没有输入字符，则打印一条消息。
- 3. 编写一个程序，向您运行的所有进程发送 SIGKILL 信号，除了当前 shell（和当前进程），基于以下 shell 脚本：

```
pidlist=`ps -aux | grep "$LOGNAME" | grep -v $$ | \
    tr -s " " | cut -f 2 -d " "`
for pid in pidlist
 do
    kill -9 $pid >/dev/null 2>/dev/null
done
```

## 答案

- 1. 这可以用单个信号处理程序完成，因为接收到的信号号作为参数传递给处理程序：

```c
void trapper(int);

main()
{
    int i;

    for (i = 0; i<32; ++i)
        signal(i, trapper);

    for (;;);
}
```

```c
void trapper(int sig)
{
    signal(sig, trapper);
    printf("Just received signal number: %d\n", sig);
}
```

- 2. 在下面的代码中，while 循环用于从键盘读取字符并在屏幕上显示它们。当没有输入字符时，循环阻塞在 read() 调用中。在循环开始之前启动一个 20 秒的闹钟。每次写入字符时，闹钟都会重置回 20 秒。当 20 秒内没有写入字符时，闹钟响起，中断 read() 并调用 trapper() 函数：

```c
#include <signal.h>
#include <unistd.h>

void trapper(int);

main()
{
    char c;

    signal(SIGALRM, trapper);
    alarm(20L);

    while (read(0, &c, 1)==1)
    {
        write(1, &c, 1);
        alarm(20L);
    }

    printf("read() interrupted...\n");
}

void trapper(int sig)
{
    printf("You stopped typing...\n");
}
```

- 3. 这个问题可以通过将 shell 脚本翻译成使用 pipe()、dup()、fork() 和 exec() 系统调用的 C 代码来轻松解决。shell 脚本中对 shell 的 PID 执行 grep -v 时，翻译成 C 代码时

你也需要对你自己的 PID 执行 grep -v，以便在程序运行时不杀死你自己的进程。你可以在程序开始时创建所有管道，以便在需要时都可用。不要忘记，在进行 I/O 重定向后，并在为每个命令调用 exec() 之前，应该关闭进程不需要的所有文件描述符（0、1 和 2 之外的所有文件描述符），否则你将无法在管道中传播文件结束。

## Tiny Shell – 案例研究

你现在已经看到了足够的系统调用，可以理解 shell 执行简单命令管道时需要发生什么。与其检查真实 shell 的代码，这里覆盖起来太复杂，不如我们来看一个 tiny shell 的代码，它只包含最基本的要素——足以演示一些原理。

tiny shell 会向你显示一个提示符，作为响应，你可以输入任何简单命令，后跟命令所需的参数。tiny shell 将执行你的命令，然后返回另一个提示符供你使用。你应该注意 tiny shell 不能处理真实 shell 接受的任何正则表达式。

除此简单场景外，tiny shell 还允许你使用熟悉的 |、<、> 和 >> 操作符进行管道和 I/O 重定向，以及使用 & 操作符在后台执行管道。

## 20.1 数据结构

为了理解 tiny shell 的操作，首先要查看的是涉及的数据结构。为了简化 tiny shell 的内部结构，其数据结构都在编译时静态分配。这意味着，例如，使用数组存储事物而不是动态分配的链表。其结果是 tiny shell 对某些事物的大小施加了固定限制，而真实 shell 无需施加此类限制。特别是，以下事物是固定的，即你需要重新编译 tiny shell 才能更改它们：shell 提示符处输入行的最大长度、用于 I/O 重定向的文件名的最大长度、每个简单命令的命令行参数的最大数量以及管道中简单命令的最大数量。

所有这些定义以及全局变量和数据结构的声明
