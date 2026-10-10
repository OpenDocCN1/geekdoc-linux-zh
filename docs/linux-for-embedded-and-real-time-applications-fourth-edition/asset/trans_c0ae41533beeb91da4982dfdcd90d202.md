
## 清单 9.2
/* 清理处理程序示例 */
#include <pthread.h>

typedef struct my_queue_tag {
    pthread_mutex_t  mutex;      /* 保护对队列的访问 */
    pthread_cond_t   cond;      /* 发出队列变更信号 */
    int              get, put;  /* 队列指针 */
    unsigned char    empty, full; /* 状态标志 */
    q[Q_SIZE];                  /* 队列本身 */
} my_queue_t;

my_queue_t data = {
    PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0, 1, 0};

void cleanup_handler (void *arg)
/*
   解锁与队列关联的互斥锁
*/
{
    pthread_mutex_unlock ((mutex *) arg);
}

int main (int argc, char *argv[])
{
    while (1)
    {
        pthread_cleanup_push (cleanup_handler, (void *) &data.mutex);
        pthread_mutex_lock (&data.mutex);
        if (queue is empty)
        {
            data.empty = 1;
            pthread_cond_wait (&data.cond, &data.mutex);
        }
        /* 从队列读取数据 */
        pthread_cleanup_pop (1);
        /* 对数据执行某些操作 */
    }
}

## Pthreads 实现

在 2.6 版本内核之前，最流行的线程实现是 LinuxThreads。它大约自 1996 年起就已存在，到 2.5 内核开发启动时，人们普遍认为需要一种新方法来解决 LinuxThreads 的局限性。这些局限性包括，内核将每个线程表示为一个独立的进程，或*可调度实体*，并为其分配唯一的进程 ID，尽管许多线程存在于同一个进程实体中。这导致与其他线程实现存在兼容性问题。每个进程有 8192 个线程的硬编码限制，虽然这看似很多，但有些问题确实可以从运行数千个线程中受益。

这项新开发工作的成果是原生 POSIX 线程库，即 NPTL，它现在是 2.6 和 3.x 系列内核中的标准线程实现。它同样将每个线程视为独立的可调度实体，但利用了内核中专门旨在克服 LinuxThreads 局限性的改进。`clone()` 调用被扩展以优化线程创建。每个进程的线程数量不再受限，新的完全公平调度器（CFS）可以处理数千个线程而没有过多的开销。一种新的同步机制，即快速互斥锁或“futex”，无需内核调用即可处理无竞争的情况。

在 IA-32 架构上的测试中，据报道 NPTL 能够在两秒内启动 100,000 个线程。相比之下，在没有 NPTL 的内核下运行此测试大约需要 15 分钟。

## 升级恒温器

我们现在已具备足够的背景知识，可以为恒温器添加一个线程，以监视串行端口参数的变化。我们将使用一种非常简单的协议来设置参数，该协议由一个字母后跟一个空格，再后跟一个数字组成。“s”代表设定点（setpoint），“l”代表限值（limit），“d”代表死区（deadband）。因此，要改变设定点，您只需输入，例如：

```
s 65<Enter>
```

这将设定点设置为 65 度。

将当前位于 `src/measure/` 目录中的 `thermostat.c` 复制到 `src/posix/`。创建一个名为“posix”的新 Eclipse 项目，位于 `home/samples/src/posix/` 目录中。同样，请确保它是一个 makefile 项目，并导入包含路径的项目设置。打开 `monitor.c`。首先要注意的是 `#include <pthread.h>`。此头文件声明了 Pthreads API 的原型。注意 `paramMutex` 和 `monitor` 的声明。后者将成为我们的监视线程句柄。

由于参数 `setpoint`、`limit` 和 `deadband` 被两个线程——恒温器线程和监视线程——独立访问，我们需要一个互斥锁来保证只有一个线程独占访问。实际上，这个特定应用可能并不绝对需要互斥锁，因为共享资源是简单的整数，对它们的访问应该是原子的。但它确实起到了说明问题的作用。

顺便注意，`setpoint`、`limit` 和 `deadband` 在 `thermostat.h` 中被声明为 `extern`。假设这些变量在 `thermostat.c` 中分配。如果碰巧为您的参数使用了不同的名称，您需要更改以匹配。

查看 `monitor()` 函数。它只是一个简单的循环，从 `stdin` 获取并解析字符串。注意，在 `monitor()` 更改任何参数之前，它会锁定 `paramMutex`。在 switch 语句的末尾，它解锁 `paramMutex`。在您的恒温器状态机中，也需要采用这种相同的方法。

向下滚动到 `createThread()` 函数。它将从 `thermostat.c` 中的 `main()` 调用，以初始化 `paramMutex` 并创建监视线程。如果失败，`createThread()` 返回非零值。`terminateThread()` 确保在终止 `main()` 之前正确终止监视线程。它应该从 `main()` 中的 `closeAll()` 之前调用。

## Thermostat.c 中所需的更改

为了让 `thermostat.c` 能与监视器配合工作，所做的更改惊人地少。

- 包含 `pthread.h` 和 `thermostat.h`。
- 在 `main()` 顶部调用 `createThread()`，并测试返回值，
- 在状态变量的 switch 语句之前锁定 `paramMutex`，并在 switch 语句末尾解锁它。
- 在 `running` 循环之后立即调用 `terminateThread()`。

就是这样！makefile 支持目标构建和模拟构建，如上一章所述。两种构建的驱动程序都来自 `measure/` 目录，并假设它们已被构建。构建模拟版并试用一下。

## 调试多线程程序

多线程确实给调试过程带来了一些复杂性，但幸运的是，GDB 有相应的功能来处理这些问题。在 Eclipse 中调试 `thermostat_s`（确保 `devices` 正在运行），使用主机调试配置，并在 `main()` 中调用 `createThread()` 处设置断点。当它在断点处停止时，点击“Step into”（步入）进入 `createThread()` 函数。

步过 `pthread_mutex_init()` 调用和 `CHECK_ERROR`。现在，当步过对 `pthread_create()` 的调用时，调试视图中会出现第二个线程。这是监视线程，它已经位于 `fgets()` 调用内部。

在 `monitor()` 函数中 `fgets()` 调用之后设置一个断点。现在，在 `Console`（控制台）视图中输入一行文本。它是否有效并不重要。我们此时只想让程序在断点处停止。让程序继续，当它到达断点时，请注意现在挂起在断点处的是 `Thread [2]`。`Thread [1]` 很可能挂起在 `sleep()` 函数内部。

在 `main()` 和 `monitor()` 的各个地方尝试设置断点，以验证参数是否正确更新，以及恒温器是否正确响应新值。

当您满意于程序在模拟环境下运行后，为目标板重新构建它并在那里进行调试。您需要创建一个新的 make 目标，就像我们在上一章针对 measure 项目所做的那样。您还需要删除目标版本的 `monitor.o` 和 `thermostat.o`，以便正确构建。

启动调试器时，您可能会看到控制台视图中闪过一些警告消息。这些是无害的。

调试器如常停在 `main()` 的第一行。让程序执行到 `createThread()` 的断点。步过，调试视图显示两个线程，正如我们在模拟版本中看到的那样。从此处开始，目标调试过程与模拟模式基本上相同。

有了对线程的基本理解，我们就准备好着手处理网络，即下一章的主题。

## 资源

Open Group 已免费向私人用户开放整个 Posix（现称为 Single Unix）规范。请访问：`www.unix.org/online.html`

系统将要求您注册。别担心，过程简单且免费。一旦注册，您就可以在线阅读规范，或下载完整的 `html` 文件集以供本地访问。

本章只是对 Posix 线程的简要介绍。还有更多内容值得关注。更详尽的出色处理见于：

Butenhof, David R., *Programming with POSIX Threads*, Addison-Wesley, 1997.

