
线程的概念已经存在一段时间，但直到 POSIX 1003.1 规范出现，它们还没有被广泛采用。Linux 在 1996 年左右通过一个通常被称为 LinuxThreads 的库获得了线程支持。两个主要项目是新一代 POSIX 线程 (NGPT) 和原生 POSIX 线程 (NPTL)。这两个项目都必须对 Linux 内核进行修改以支持线程。2002 年，NGPT 团队宣布他们不想分裂社区，并将停止为 NGPT 添加新功能，但将继续开发 NPTL。因此，看来 NPTL 将成为线程的新标准。关于 NPTL 的一些有趣的背景信息可以在 Ulrich Drepper 和 Ian Molnar 撰写的名为《The Thread Library for Linux》的论文中找到，本书期间可以通过 `http://www.redhat.com/partners/pdf/POSIX_Linux_Threading.pdf` 找到。

本章中的大部分代码应该适用于任何线程，因为它是基于 POSIX 标准的。然而，你将看到一些差异，特别是如果你没有在使用示例中使用的 NPTL。使用旧的 Linux Threads 库时，你通常会看到多个进程，通常比你的线程数多一个；使用 NPTL，你应该只看到一个程序，尽管它内部有许多线程。

## 线程的优点和缺点

在某些情况下，创建新线程比创建新进程具有一些明显的优势（尽管 Linux 在创建新进程方面比其他操作系统特别高效）。

以下是线程用途的一些示例：

有时，让程序看起来同时在做两件事非常有用。经典的例子是在仍在编辑文本的同时对文档进行实时字数统计。一个线程可以管理用户的输入并执行编辑。另一个线程（可以看到文档内容）则持续更新字数变量。这个线程（甚至是第三个线程）可以使用此共享变量来向用户告知最新信息。另一个例子是多线程数据库服务器，一个进程为多个客户端提供服务，通过处理某些请求的同时阻塞其他请求并等待磁盘活动，提高整体数据吞吐量。

## POSIX 线程

对于数据库服务器而言，在不同的进程中高效地实现这种多任务处理是非常困难的，因为锁和数据一致性的要求会导致不同进程之间紧密耦合。与多个进程相比，使用多线程更容易实现这一点。

- 一个混合了输入、计算和输出的应用可以通过将这三者作为三个线程运行来提高性能。当输入或输出线程正在等待连接时，其他线程可以继续运行。因此，任何应用程序最终一次只能做一件事，而线程允许应用程序在等待连接等事项时执行一些有用操作。处理多个网络连接的服务器应用程序也天然适合多线程程序。
- 总的来说，在线程之间切换需要操作系统完成的工作比在进程之间切换少得多。因此，多个线程对资源的需求远小于多个进程，而且在单处理器系统上运行逻辑上需要许多执行线程的程序更具实用性。也就是说，编写多线程程序的设计非常重要，不应掉以轻心。

线程也有缺点：

- 编写多线程程序需要非常仔细的设计。在多线程程序中由于无意共享变量而引入细微时序故障的风险是巨大的。Alan Cox（为本书序言的 Linux 大师）曾评论道，线程也被称为“如何同时射自己的脚”。
- 调试多线程程序比调试单线程程序要困难得多，因为线程之间的交互非常难以控制。
- 将一个大型计算分为两部分并作为不同线程的程序，在单处理器机器上并不一定运行得更快，因为有许多 CPU 周期可用；如果没有其他程序在尝试执行，且你有多个处理器或超线程 CPU，那么多线程方法可能会带来收益。

## 第一个线程程序

有一系列与线程相关的库调用，大多数名称都以 `pthread_` 开头。要使用这些库调用，我们必须定义 `REENTANT` 宏，包含 `thread.h` 文件，并使用 `-pthread` 链接线程库。

在设计原始 UNIX 和 POSIX 库函数时，假设任何进程都只有一个执行线程。一个明显的错误是将 `errno` 变量用于调用失败后检索错误信息。在多线程程序中，默认情况下所有线程共享一个 `errno` 变量。在另一个线程能够检索之前的错误之前，该变量很容易被一个线程的调用更新。类似的问题也存在于函数中，例如 `puts`，它通常使用单个全局变量进行缓冲。

我们需要被称为“重入函数”（re-entrant routines）的例程。重入代码可以被不同的线程以某种方式多次调用或嵌套调用，并且能够正常运行。因此，重入代码部分必须使用局部变量，使得对代码的每次调用都能获得其独特的数据拷贝。

## 第 12 章

在多线程程序中，我们通过在程序中任何 `#include` 行之前定义 `REENTANT` 宏来告诉编译器我们需要此功能。这为我们做了三件事，而且执行得非常优雅，以至于我们通常不需要知道其中某件事的作用：

- 某些函数获得了重入安全等价版本的原型。这些通常是相同的函数名，但添加了 `_r`，例如将 `gethostbyname` 变为 `gethostbyname_r`。
- 某些通常以宏形式实现的 `stdio.h` 函数变成了真正的重入安全函数。
- 变量 `errno`（源自 `errno_`）被改为了一个函数，该函数可以以线程安全的方式确定 `errno` 值。

包含 `pthread.h` 文件为我们提供了代码中需要的其他定义和原型，比如用于标准输入输出例程的 `stdio.h`。我们必须确保包含适当线程头文件，并链接实现 `pthread` 函数的相应库。我们将在本节之后的“尝试运行”部分详细查看编译程序的方法。

`pthread_create` 创建一个新线程，就像 `fork` 创建新进程一样。

```
#include <pthread.h>

int pthread_create(pthread_t *thread, pthread_attr_t *attr, void
    *(*start_routine)(void *), void *arg);
```

这看起来可能很吓人，但实际上非常易用。第一个参数是指向 `pthread_t` 的指针。当创建线程时，一个标识符会被写入指针指向的位置，使我们能够引用该线程。下一个参数设置线程属性。你通常不需要任何特殊属性，可以简单地将 `NULL` 作为此参数。在章的后后部分，我们将展示如何使用这些属性。最后两个参数告诉函数何时开始执行，以及要传递给该函数的参数。

```
void *(*start_routine)(void *)
```

上一行仅表示我们必须传递一个以 `void` 为参数的函数地址，该函数将返回一个指向 `void` 的指针。因此，我们可以传递任何类型的单参数，并返回任何类型的指针。使用 `fork` 会导致执行在相同位置继续但带有不同的返回码，而新线程则提供了一个新线程应该开始执行的函数指针。

返回 0 表示成功，如果发生任何错误则返回错误号。手册页包含了本章使用的此函数和其他函数的错误条件详细信息。

`pthread_create` 像大多数 `pthread` 函数一样，属于不符合使用 -1 表示错误惯例的 UNIX 函数。除非你非常有把握，否则在检查错误代码之前双重检查手册总是安全的。

## POSIX 线程

当一个线程终结时，它会调用 `pthread_exit` 函数，就像进程终止时调用 `exit` 一样。该函数终止调用线程，并返回一个对象的指针。永远不要用它返回局部变量的指针，因为变量会在线程结束时消失，导致严重的错误。`pthread_exit` 定义如下：

```
#include <pthread.h>
void pthread_exit(void *ret);
```

`pthread_join` 是进程使用 `wait` 来收集子进程的线程等效函数。该函数定义如下：

```
#include <pthread.h>
int pthread_join(pthread_t thread, void **thread_return);
```

第一个参数是要等待的线程，即 `pthread_create` 填充的标识符。第二个参数是一个指针，指向线程的返回值。和 `pthread_create` 一样，该函数成功时返回零，失败时返回错误代码。

## 尝试运行——简单的线程程序

此程序创建一个单线程，展示它与原始线程共享变量，并让新线程向原始线程返回结果。多线程程序没有比这更简单的了！这里是 `thread1.c`：

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <pthread.h>

void *thread_function(void *arg);

char message[] = "Hello World";

int main() {
    pthread_t a_thread;
    void *thread_result;
    int res;

    res = pthread_create(&a_thread, NULL, thread_function, (void *)message);
    if (res != 0) {
        perror("Thread creation failed");
        exit(EXIT_FAILURE);
    }
    printf("Waiting for thread to finish...\n");
    res = pthread_join(a_thread, &thread_result);
    if (res != 0) {
        perror("Thread join failed");
        exit(EXIT_FAILURE);
    }
    printf("Thread joined, it returned %s\n", (char *)thread_result);
}
```

## 第 12 章

```c
printf("Message is now %s\n", message);
exit(EXIT_SUCCESS);
}
void *thread_function(void *arg) {
    printf("thread_function is running. Argument was %s\n", (char*)arg);
    sleep(3);
    strcpy(message, "Bye!");
    pthread_exit("Thank you for the CPU time");
}
```

要编译此程序，我们首先需要确保在某些系统上开启了 `REENTRANT`，我们可能还需要定义 `POSIX_SOURCE`，但通常这是必需的。

- 现在我们必须确保链接了相应的线程。取决于你的系统，NPTL 可能不是默认选项，或者在较旧系统上，根据内核版本，甚至不存在或不可用。正式地说，本章中的大多数代码都独立于特定的某个线程库。在作者的系统中，检查标准的 `/usr/include/pthread.h` 文件显示其名称为 Linuxthreads，版权日期为 1996 年，这是一个非常老老的库。为了获取新的 NPTL，我们需要安装额外的 RPM 包，它会在 `/usr/include/nptl` 下提供额外的文件并在 `/usr/lib/nptl` 下提供额外的库。
- 在识别并安装了适当的文件后，我们现在可以这样编译并链接我们的程序：

```bash
$ cc -DREENTRANT /usr/include/nptl thread.c -o thread -L/usr/lib/nptl -lpthread
```

如果你同时安装了这两套文件和库，可能可能考虑删除旧的，以确保使用的是正确的一组。如果 NPTL 是你系统上的默认选项，你显然不需要 `-I` 和 `-L` 选项。本章中的代码尽可能贴近标准，希望你能够在任何对线程支持良好的 Linux 系统上运行它。

当你运行这个程序时，你应该会看到：

```bash
$ ./thread1
Waiting for thread to finish...
thread_function is running. Argument was Hello World
Thread joined, it returned Thank you for the CPU time
Message is now Bye!
```

花一点时间理解这个程序是值得的，因为我们将它作为本章大部分示例的基础。

## 工作原理

我们为创建线程时将调用的函数声明一个原型。

```c
void *thread_function(void *arg);
```

按照 `pthread_create` 的要求，它接受一个 `void` 指针作为唯一参数，并返回一个 `void` 指针。我们稍后来看该函数的定义（以及实现）。

## POSIX 线程

在 `main` 函数中，我们声明了一些变量并调用 `pthread_create` 来启动我们的新线程。

```c
pthread_t a_thread;
void *thread_result;
```

```c
res = pthread_create(&a_thread, NULL, thread_function, (void *)message);
```

我们传递了一个 `pthread_t` 对象的地址，之后我们可以引用该线程。我们不希望修改默认线程属性，因此将 `NULL` 作为第二个参数。最后两个参数是要调调用的函数以及传递给它的参数。

如果调用成功，现在将有两个线程在运行。原始线程（main）继续执行 `pthread_create` 之后的代码，而新线程在我们富有想象力的命名 `thread_function` 中开始执行。

原始线程检查新线程已启动，并调用 `pthread_join`。

```c
res = pthread_join(a_thread, &thread_result);
```

这里我们传递了正在等待合并的线程标识符和一个指向结果的指针。该函数将一直等待直到另一个线程返回结果。它打印线程的返回值和变量的内容，然后退出。

新线程开始执行，`thread_function` 打印它的参数，睡眠一段时间，更新全局变量，然后退出并向主线程返回一个字符串。新线程写入同一个数组 `message`，原始线程也可以访问该数组。如果我们调用的是 `fork` 而不是 `pthread_create`，情况就不是如此了。

## 同时执行

接下来我们将编写一个程序来检查两个线程的执行是否是同时发生的（当然，仍然是在单处理器系统上），因为 CPU 正在线程之间明巧妙地切换。我们还没有遇到任何高效完成此任务的线程同步函数，这将是一个非常低效的程序，即两个线程之间的“轮询”。再次，我们将利用进程中局部函数变量外所有内容在不同线程间共享的这一特性。

> **尝试一下——两个线程的同步执行**

在本节中创建的程序 `thread2.c` 是通过稍微修改 `thread1.c` 创建的。我们添加了一个额外的作用域变量来测试哪个线程正在运行：

```c
run_now = 1;
```

当 `main` 函数执行时，我们将 `run_now` 设置为 1，当我们的新线程执行时，将其设置为 2。

在 `main` 函数中，创建新线程之后，我们添加了以下代码：

```c
int print_count1 = 0;
while(print_count++ < 20) {
    if (run_now == 1) {
        printf("1");
        run_now = 2;
    }
    else {
        sleep(1);
    }
}
```

`run_now` 为 1，我们打印 "1"，`run_now = 2`。（在线程函数中，逻辑类似）。

```c
int print_count2 = 0;
while(print_count++ < 20) {
    if (run_now == 2) {
        printf("2");
        run_now = 1;
    }
    else {
        sleep(1);
    }
}
```

`run_now` 为 2，我们打印 "2"，`run_now = 1`。这就是轮询机制。

## 第12 章

下一对函数用于控制信号量的值，声明如下：

```
#include <semaphore.h>

int sem_wait(sem_t *sem);

int sem_post(sem_t *sem);
```

这两个函数都接受一个指向通过 `sem_init` 初始化的信号量对象的指针。

`sem_post` 函数以原子的方式将信号量的值加 1。这里的“原子性”意味着，如果两个线程同时尝试将同一个信号量的值加 1，它们不会互相干扰；而如果两个程序同时读取值、被另一个线程增加了该值、然后又同时写入值，就会发生这种情况。信号量的值将准确地增加 2，因为有两个线程尝试修改它。

`sem_wait` 函数以原子的方式将信号量的值减 1，但它总是会等待，直到信号量的计数非零为止。因此，如果你在一个初始值为 2 的信号量上调用 `sem_wait`，该线程将继续执行，但值会减为 1。如果在一个值为 0 的信号量上调用 `sem_wait`，该函数将等待直到它变为非零。如果两个线程在 `sem_wait` 中等待同一个信号量变为非零，而第三个进程将其增加了 1，那么两个等待进程中只有一个可以减少信号量的值，另一个将继续等待。

这种在单个函数中实现原子的“测试并设置”（test and set）能力使得信号量如此宝贵。另一个信号量函数 `sem_trywait` 是它是 `sem_wait` 的非阻塞伙伴。我们在这里不讨论它，但你可以在手册页中找到更多细节。

最后一个信号量函数是 `sem_destroy`。该函数在我们完成对信号量的使用后对其进行清理。它的声明如下：

```
#include <semaphore.h>

int sem_destroy(sem_t *sem);
```

同样，它接受一个指向信号量的指针并清理它可能拥有的任何资源。如果你尝试销毁一个线程正在等待的信号量，将得到错误。

与 Linux 类似，这些函数在成功时返回 0。

## 尝试一下——线程信号量

这段代码 `thread3.c` 同样基于 `thread1.c`。由于发生了很多变化，我们将以完整的形式展示它。
