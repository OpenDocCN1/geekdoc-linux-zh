
```c
pthread_t *thread;
int s;
s = pthread_create(&thread, NULL, func, &arg);
if (s != 0)
    errExitEN(s, "pthread_create");
```

# 编译 Pthreads 程序

在 Linux 上，使用 Pthreads 接口的程序必须使用 `cc -pthread` 选项进行编译。该选项的作用包括：

- 定义了 `_REENTRANT` 预处理器宏。这会导致所有可重入函数（reentrant functions）的声明被暴露。
- 程序与 `libthread` 库链接（等同于 `-lpthread`）。

编译多线程程序的具体选项根据不同的实现（以及编译器）而异。其他另一些实现（例如 Tru64）也使用 `cc -pthread`；Solaris 和 HP-UX 则使用 `cc -mt`。

# 29.3 线程的创建

当程序启动时，生成的进程包含一个单一线程，称为 `initial` 或 `main` 线程。在本节中，我们将介绍如何创建额外的线程。

`pthread_create()` 函数创建一个新线程。

```c
#include <pthread.h>

int pthread_create(pthread_t *thread, const pthread_attr_t *attr,
                   void (*start)(void), void *arg);
```

成功时返回 0，错误时返回正错误数

新线程通过调用由参数 `arg` 指定的函数开始执行（即 `start(arg)`）。调用 `pthread_create()` 的线程将继续执行调用后的后续语句。（这种行为与第 28.2 节描述的用于 `clone()` 系统调用的 `glibc` 封装函数相同）。

`arg` 参数声明为 `void *`，这意味着我们可以向 `start` 函数传递任何类型的对象。通常，`arg` 指向一个全局变量或堆变量，但也可以传递 `NULL`。如果我们需要向 `start` 传递多个参数，可以将 `arg` 指定为一个包含这些参数的结构体，每个参数作为一个独立的字段。通过明智的类型转换，我们可以将 `arg` 指定为 `int`。

严格来说，C 标准并没有定义将 `int` 转换为 `void *` 及其反向转换的结果。然而，大多数编译器允许这些操作，并且它们会产生预期的结果；即 `int == ((void *))`。

`start` 的返回值类型为 `void *`，可以使用与 `arg` 参数相同的方式。我们将在描述 `pthread_join()` 函数时将看到该值是如何被使用的。

当使用转换后的整数作为启动函数的返回值时，需要小心。其原因是 `PTHREAD_CANCELED`（当线程被取消时返回的值，见第 32 节）通常是某个实现定义的整数值转换成的 `void *`。如果启动函数返回了相同的整数值，那么对于另一个正在执行 `pthread_join()` 的线程来说，将错误地显示该线程已被取消。在采用线程取消机制并选择从线程启动函数返回转换整数值的应用程序中，我们必须确保正常终止的线程返回的整数值在 Pthreads 实现中与 `PTHREAD_CANCELED` 匹配。一个可移植的应用程序需要确保正常终止的线程返回的整数值在应用程序将运行的任何实现中都不会与 `PTHREAD_CANCELED` 匹配。

该参数指向一个 `pthread_t` 类型的缓冲区，在 `pthread_create()` 返回之前，线程的唯一标识符会被拷贝到该缓冲区。该标识符可以在随后的 Pthreads 调用中引用该线程。

SUSv3 明确指出，实现不需要在新线程启动之前初始化由 `thread` 参数指向的缓冲区；也就是说，新线程可能在 `pthread_create()` 返回给调用者之前就开始运行。如果新线程需要获取自己的 ID，则它必须使用 `pthread_self()`（在第 29.5 节描述）。

`attr` 是指向 `pthread_attr_t` 对象的指针，用于指定新线程的各种属性。我们将在第 29.8 节中详细介绍这些属性。如果 `attr` 为 `NULL`，则将以各种默认属性创建线程，这也是我们在本书中大多数示例程序中所做的。

在调用 `pthread_create()` 后，程序无法保证哪个线程将下一次调度使用 CPU（在多处理器系统上，两个线程可能同时在不同的 CPU 上执行）。隐式依赖于特定调度顺序的程序可能会面临我们在第 24.4 节中描述的同类竞态条件。如果我们需要强制执行特定的顺序，则必须使用第 30 节中描述的同步技术之一。

# 29.4 线程的终止

线程的执行通过以下方式之一终止：

- 线程的启动函数执行了返回，并指定了线程的返回值。
- 线程调用 `pthread_exit()`（下文描述）。
- 线程被 `pthread_cancel()` 取消（第 32.1 节描述）。
- 任何线程调用 `exit()`，或者主线程执行了返回（在 `main()` 函数中），这会导致进程中的所有线程立即终止。

`pthread_exit()` 函数终止调用它的线程，并指定一个可以在其他调用 `pthread_join()` 的线程获取的返回值。

```c
#include <pthread.h>

void pthread_exit(void *retval);
```

调用 `pthread_exit()` 等同于在线程启动函数中执行返回，区别在于 `pthread_exit()` 可以从线程启动函数调用的任何函数中。

`retval` 参数指定线程的返回值。`retval` 所指向的值不应位于线程的栈上。(由于提供的原文文本存在重复和中断，此处已根据核心逻辑完成翻译)。

如果一个线程被分离（见第 29.7 节），那么我们必须使用 `pthread_join()` 与它连接。如果我们没有这样做，那么当线程终止时，它会产生一个同于僵尸进程的线程（第 26.2 节）。除了浪费系统资源外，即使线程不断累积，我们也无法添加额外的线程。

`pthread_join()` 为线程执行的任务与 `waitpid()` 为进程执行的任务相似。然而，它们存在一些显著的区别：

- 线程之间是平等的。进程中的任何线程都可以使用 `pthread_join()` 与该进程中的任何其他线程连接。例如，如果线程 A 创建了线程 B，线程 B 又创建了线程 C，那么线程 A 完全可以与线程 C 连接，反之亦然。这与进程之间的层级关系不同。当父进程使用 `fork()` 创建子进程时，只有该进程可以对该子进程调用 `wait()`。调用 `pthread_create()` 的线程与生成的线程线程之间没有这种关系。
- 目前没有方法可以表述“与任何线程连接”（对于进程，我们可以使用调用 `waitpid(-1,&Status,options)` 来实现）；也没有方法实现非阻塞连接（类似于 `waitpid` 标志）。但是可以使用条件变量来实现类似的功能；我们将在第 30.2.4 节中展示示例。

`pthread_join()` 只能与特定的线程 ID 连接的这一限制是刻意为之的。其思想是：程序应该只与它“已知”的线程连接。“与任何线程连接”操作的问题在于，线程之间没有层级结构，因此这种操作确实可能会连接任何线程，包括由库函数创建的线程。（我们在第 30.2.4 节中显示的条件变量技术允许与它已知的任何其他线程连接。）结果是，库将不再能够通过连接该线程来获取其状态，并且它会错误地尝试连接一个已经执行过连接的线程 ID。换句话说，“与任何线程连接”操作与模块化设计是不兼容的。

## 示例程序

列表 29-1 中的程序创建了另一个线程并与其连接：

列表 29-1：使用 Pthreads 线程的简单程序 `threads/simple_thread.c`

```c
#include <pthread.h>

#include <lpthread_hdr.h>

static void *hreadFunc(void *arg)
{
    char *s = (char *)arg;
    printf("%s", s);
    return (void *)strlen(s);
}
```

```c
int
main(int argc, char *argv[])
{
  pthread_t t1;
  void *res;
  int s;

  s = pthread_create(&t1, NULL, threadFunc, "Hello world\n");
  if (s != 0) {
    errExitEN(s, "thread_create");
  }

  printf("Message from main()\n");
  s = pthread_join(t1, &res);
  if (s != 0) {
    errExitEN(s, "thread_join");
  }
```
