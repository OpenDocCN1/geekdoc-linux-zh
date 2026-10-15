
要定义线程，你回回溯 Linux 进程以理解它们的组成。进程和线程都有控制流并可以并发运行，但在某些非常独特的方式上有所不同。例如，线程共享数据，而进程没有显式共享。当进程被 `fork` 时（回想第 13 章“套接字编程”），会创建一个新进程，它有自己的全局变量和栈（见图 15.1）。当创建线程时，唯一创建的新元素是线程唯一的栈（见图 15.2）。代码和全局数据在线程间是通用的。这是一种优势，但线程的共享性质也可能带来问题。本章将调查这个问题。

# 进程 A 地址空间 | 进程 B 地址空间

![](img/0b91ab9198b0fdfd5649d5d19571459e_275_0.png)

图 15.1 创建新进程。

## 第 15 章 POSIX 线程 (Pthreads) 编程 255

一个 GNU/Linux 进程可以创建并管理多个线程。每个线程通过一个线程标识符标识，该标识对于系统中的每个线程都是唯一的。每个线程都有它自己的栈（如图 15.2 所示）以及唯一的上下文（程序计数器、保存的寄存器等）。但由于数据空间是线程间共享的，它们共享的不仅仅是用户数据。例如，打开的文件或套接字的文件描述符也是共享的。因此，当多线程应用程序使用 `socket` 或文件时，必须对资源的访问进行保护，以防止多次并发访问。本章将介绍实现目标的方法。

### 进程 A 地址空间

![](img/0b91ab9198b0fdfd5649d5d19571459e_276_0.png)

图 15.2 创建新线程。

虽然在某些方面，编写多线程应用程序可能比传统的基于进程的应用程序更容易，但你确实遇到需要理解的问题。线程的共享数据属性可能是设计上最困难的，但它同时也非常强大，能够带来性能更高、更简单的应用程序。关键是在开发线程应用程序时强烈考虑共享数据。另一个重要的考虑是，严肃的多线程应用程序开发需要利用 2.6 内核而不是 2.4 内核（由于采用了新的 NPTL 线程实现）。

### 线程函数基础

目前讨论的 API 遵循一种相当统一的模型：发生错误时返回 `-1`，实际错误值存储在 `errno` 进程变量中。线程 API 在成功时返回 `0`，返回正值以表示错误。

### pthreads API

虽然 `pthreads` API 功能完备，但它非常容易理解和使用。本节将探索 `pthreads` API，从线程创建的基础知识介绍到可用的特殊通信和同步方法。

所有多线程程序必须使 `pthread` 函数原型和符号可用。这通过包含 `pthread` 标准头文件来实现，如下所示：

```
#include <pthread.h>
```

> 随后的示例代码为了简洁起见而编写，在某些情况下没有检查返回值。为了避免调试时出现意外，强烈建议你检查所有系统调用的返回值，永远不要假设某个函数执行成功了。

![](img/0b91ab9198b0fdfd5649d5d19571459e_277_0.png)

### 线程基础

所有多线程应用程序必须创建线程并最终销毁它们。通过 `pthreads` API 的两个函数实现：

```
int pthread_create( pthread_t *thread,
                pthread_attr_t *attr,
                void *(*start_routine)(void, void, void *arg);
int pthread_exit(void *retval);
```

`pthread_create` 函数允许创建新线程，而 `pthread_exit` 允许线程自终止。你还有一个函数允许一个线程终止另一个线程，但将在稍后讨论。

要创建一个新线程，你调用 `pthread_create` 并将 `pthread_t` 对象与一个函数（`start_routine`）关联。该函数代表在线程内执行的顶层代码。你可以选择通过 `pthread_attr_t` 提供一组属性（通过 `pthread_attr_init`）。最后，第四个参数（`arg`）是一个可选参数，在创建线程时传递给线程。

## 第 15 章 POSIX 线程 (Pthreads) 编程 257

现在是时候看线程创建的一个短示例了（参见列表 15.1）。在主函数中，你首先在第 10 行创建一个 `pthread_t` 对象。该对象代表你的新线程。你在第 12 行调用 `pthread_create`，并提供 `pthread_t` 对象（由 `pthread_create` 函数填充）以及包含包含线程代码的函数（参数 3，`myThread`）。返回 `0` 表示线程创建成功。

### 列表 15.1 使用 pthread_create 创建线程（位于光盘的 `/source/ch15/ptccreate.c`）

```
1: #include <pthread.h>
2: #include <stdlib.h>
3: #include <stdio.h>
4: #include <string.h>
5: #include <errno.h>
6: 
7: int main()
8: {
9: int ret;
10: pthread_t mythread;
11:
12: ret = pthread_create(&mythread, NULL, myThread, NULL);
13:
14: if (ret != 0) {
15: printf("Can't create thread (%s)\n", strerror(errno));
16: exit(-1);
17: }
18:
19: return 0;
20: }
```

`pthread_create` 函数在成功时返回零；否则返回非零值。现在是时候看看线程函数本身了，它也演示了 `pthread_exit` 函数（参见列表 15.2）。线程简单地向标准输出发送一条消息，表示它运行过，然后在第 6 行通过 `pthread_exit` 终止。

### 列表 15.2 使用 pthread_exit 终止线程（位于光盘的 `/source/ch15/pttexit.c`）

```
1: void *myThread(void *arg)
2: {
3: printf("Thread ran!\n");
4:
5: /* Terminate the
6: pthread_exit(
```

### GNU/Linux 应用程序

### 线程管理

在深入研究线程同步和协调之前，是时候看一些杂用的函数。第一个是 `pthread_self`，线程可以使用它来检索自己的标识符。第二个是 `pthread_cancel`，可以作为第一个参数用于终止线程。

```
pthread_self( void );
```

考虑列表 15.3 中的线程函数，它展示了 `pthread_t` 句柄。在第 5 行，你调用 `pthread_self` 获取句柄并在第 7 行将其标准输出。

### 列表 15.3 使用 pthread_self 获取 pthread_t 句柄（位于光盘的 `/source/ch15/pthreadcreate.c`）

```
1: void *myThread(void *arg)
2: {
3: pthread_t pt;
4:
```

## 第 15 章 POSIX 线程 (Pthreads) 编程 259

```
5:    pt = pthread_self();
6:
7:    printf("Thread %x ran!\n", (int)pt);
8:
9:    pthread_exit(NULL);
10:   }
```

大多数应用程序都需要某些初始化，但在线程应用程序中，这项工作可能困难。`pthread_once` 函数允许开发者创建一个在多线程应用程序中只调用一次的初始化程序（即使多个线程尝试调用它）。`pthread_once` 函数需要两个对象：一个 `pthread_once_t` 对象（已通过 `pthread_once_init` 初始化）和一个初始化函数。考虑列表 15.4 中的部分示例。第一个调用 `pthread_once` 的线程会调用初始化函数（`initialize_app`），后续对 `pthread_once` 的调用将不再调用 `initialize_app`。

### 列表 15.4 使用 pthread_once 提供单次初始化函数

```
1:    #include <pthread.h>
2:
3:    pthread_once_t my_init_mutex = pthread_once_init;
4:
5:    void initialize_app(void )
6:    {
7:        /* Single-time init here */
8:    }
9:
10:   void *myThread(void *arg)
11:   {
12:       ...
13:
14:       pthread_once(&my_init_mutex, initialize_app);
15:
16:       ...
17:   }
```
