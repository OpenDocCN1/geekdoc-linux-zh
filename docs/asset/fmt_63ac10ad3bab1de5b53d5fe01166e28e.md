
- 2. 在 `printarg` 的开头调用 `sleep(i)`。
- 3. 在第一个 `for` 循环中 `pthread_create` 调用之后调用 `sleep(i)`。
- 4. 在第一个 `for` 循环之后调用 `sleep(i)`。
- 5-8. 重复上述所有项，使用 `$i$` 作为循环索引而不是 `$j$`。如果线程执行超过一秒，结果将会不同。在足够快的系统上，将出现如下结果：
- 1. 练习 12.12 中的输出。
- 2. 每个线程都输出值 10，即主程序完成循环时 `$i$` 的值。
- 3. 每个线程在 `$i$` 改变之前执行，输出正确的值。
- 4. 与练习 12.12 相同。
- 5. 所有线程都输出值 0，即主程序等待第一个线程终止时 `$i$` 的值。结果可能变化。
- 6. 与 5 相同。
- 7. 与 3 相同。
- 8. 与 4 相同。

# 练习 12.14 whichexit.c

`weexit` 函数可以作为线程执行。

```c
#include <errno.h>
#include <pthread.h>
#include <stdlib.h>
#include <string.h>

void *whichexit(void *arg) {
    int n;
    int npl[1];
    int *np2;
    char sl[10];
}
```

```c
char s2[2] = "I am done";
n = 3;
p1[0] = n;
p2 = (int*)malloc(sizeof(int));
*np2 = n;
strcpy(s1, "Done");
return(NULL);
```

以下哪一个可以安全地作为 `pthread_exit` 的参数替换 `NULL`？假设没有发生错误。

- 1. `n`
- 2. `&n`
- 3. `(int *)n`
- 4. `np1`
- 5. `np2`
- 6. `s1`
- 7. `"This works"`
- 8. `strerror(EINTR)`

# 答案:

- 1. 返回值是指针而不是整数，因此这是无效的。
- 2. 整数 `n` 具有自动存储类属性，因此在函数终止后访问它是非法的。
- 3. 这是从线程返回整数的常用方法。当另一个线程调用 `pthread_join` 这里的该线程时，它会将指针强制转换为指针再转回整数。虽然这在大多数实现中可以正常工作，但应该尽量避免。C 标准 [56, Section 6.3.2.3] 规定整数可以转换为指针或整数，但结果取决于实现定义。它不保证将整数转换为指针再转回的结果仍等于原始整数。
- 4. 数组 `np1` 具有自动存储类属性，因此在函数终止后访问该数组是非法的。
- 5. 这是安全的，因为动态分配的空间在被释放之前一直可用。
- 6. 数组 `s1` 具有自动存储类属性，因此在函数终止后访问该数组是非法的。
- 7. 数组 `s2` 具有自动存储类属性，因此在函数终止后访问该数组是非法的。
- 8. 这在 C 中是有效的，因为字符串字面量具有静态存储 Duration。
- 9. 如果 `strerror` 不是线程安全的，那么这是无效的。即使在 `strerror` 是线程安全的系统上，生成的字符串也无法保证在线程终止后可用。

## 12.4 线程安全

线程的一个隐藏问题是它们可能会调用非线程安全的库函数，可能产生虚假的结果。如果多个线程可以同时执行某个函数的激活而互不干扰，则该函数是线程安全的。POSIX 规定所有所需的函数（标准 C 库中的函数）都必须以线程安全的方式实现，表 12.2 列出的特定函数除外。那些传统接口阻止其线程安全的函数必须指定带有 `_r` 后缀的替代线程安全版本。

没有线程安全的函数的重要例子是 `strerror`。虽然 `strerror` 不保证是线程安全的，但许多系统以线程安全的方式实现了该函数。遗憾的是，`strerror` 列在表 12.2 中，你不能假设多个线程调用它时它能正常工作。我们在主线程中使用 `strerror`，通常用于处理 `pthread_create` 和 `pthread_join` 的错误消息。第 13.7 节给出名为 `strerror_r` 的线程安全实现。

当线程访问相同数据时会发生另一种交互问题。程序 12.8 中的各个线程处理独立的问题，彼此不交互。在更复杂的应用程序中，线程在完成分配的任务后可能不会退出。相反，工作线程可能会请求额外的任务或共享信息。第 13 章解释了如何通过互斥锁和条件变量等同步原语来控制这种交互。

### 表 12.2. 不强制要求线程安全的 POSIX 函数。

| asctime | fcvnt | getpwnam | nl_langinfo |
| :--- | :--- | :--- | :--- |
| basename | ftw | getpuid | ptsname |
| catgets | gcvt | getservname | putc_unlocked |
| crypt | getc_unlocked | getservport | putchar_unlocked |
| ctime | getchar_unlocked | getserv | putenv |
| dbm_clearerr | getdate | getutext | pututxline |
| dbm_close | getenv | getutxid | rand |
| dbm_delete | getgrent | getutxline | readdir |
| dbm_error | getgrgid | gmtime | setenv |
| dbm_fetch | getgrnam | hcreate | setgrunt |
| dbm_firstkey | getghostbyaddr | hdestroy | setkey |
| dbm_nextkey | gethostbyname | hsearch | setpasswd |
| dbm_open | getosthent | inet_ntoa | setutxent |
| :--- | :--- | :--- | :--- |
| dbm_store | getlogin | 164a | strerror |
| dirname | getnetbyaddr | lgamma6 | strtok |
| dlerror | getnetbyname | lgammaf | ttyname |
| drand48 | getnetent | lgammal | unsetenv |
| ecvt | getopt | localeconv | wcstumbs |
| encrypt | getprotobyname | localtime | wctomb |
| endgent | getprotobynumber | lrand48 | |
| endpwent | getprotoent | mrand48 | | |
| endutxent | getpwent | nft | | |
| endutxent | getpwent | nft | | |

在传统的 UNIX 实现中，`errno` 是一个全局变量，当系统函数产生错误时会被设置。这种实现不适用于多线程。

## 12.5 用户线程与内核线程

线程的两种模型是用户线程和内核线程。如图 12.3 所示的用户线程通常运行在现有的操作系统之上。这些线程对内核是不可见的，并在它们之间竞争资源。对于内核线程，内核感知每个线程调度实体，线程在整个系统中竞争处理器资源。

## 12.4 线程安全（续接）

用户线程的开销较低，但它们也有缺点。假设线程运行时系统最终会收回控制的用户线程模型可能会被 CPU 密集型线程阻碍。CPU 密集型线程执行库调用，可能会防止线程运行时系统收回控制权以调度其他线程。

混合线程模型通过提供两个级别的控制，兼具了用户级和内核级模型的优点。图 12.5 展示了一种典型的混合方法。用户在用户级线程中编写程序，并指定与进程关联的内核可调度实体的数量。用户级线程在运行时映射到内核可调度实体，以实现并行性。用户对映射的控制程度取决于具体实现。例如，在 Solaris 线程实现中，用户级线程被称为线程，内核可调度实体被称为轻量级进程（LWP）。用户可以指定由特定的轻量级进程运行特定的线程，或者由一组线程由轻量级进程池运行。

### 图 12.5 混合模型具有两级调度，用户级线程被映射到内核实体。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_511_0.png)

POSIX 线程调度模型是一种混合模型，足够灵活，可以在标准的特定实现中同时支持用户级线程和内核级线程。该模型包含两个调度级——线程和内核实体。线程类似于用户级线程。内核实体由内核调度。线程库决定需要多少个内核实体以及如何进行映射。

POSIX 引入了线程调度范围（thread-scheduling scope）的概念，让程序员对内核实体如何映射到线程有一定的控制权。线程可以具有 `PTHREAD_SCOPE_PROCESS` 或 `PTHREAD_SCOPE_SYSTEM` 两种竞争范围。

具有 `PTHREAD_SCOPE_PROCESS` 属性的线程与其进程内的其他线程竞争处理器资源。POSIX 未规定线程如何与该进程之外的线程竞争，因此 `PTHREAD_SCOPE_PROCESS` 线程可以是类似于用户级线程，也可以通过某种更复杂的方式映射到内核实体池中。

具有 `PTHREAD_SCOPE_SYSTEM` 属性的线程在系统范围内竞争处理器资源，类似于内核级线程。POSIX 将 `PTHREAD_SCOPE_SYSTEM` 线程与内核实体之间的映射留给实现，但显而见的映射是将此类线程直接绑定到内核实体。POSIX 线程实现可以支持 `PTHREAD_SCOPE_PROCESS`、`PTHREAD_SCOPE_SYSTEM` 或两者都支持。你可以通过 `pthread_attr_getscope` 获取范围，并通过 `pthread_attr_setscope` 设置范围，前提是你的 POSIX 实现同时支持 POSIX:THR 线程扩展和 POSIX:TPS 线程执行调度扩展。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_512_0.png)

## 12.6 线程属性

POSIX 采用面向对象的方法来表示和分配属性，通过将栈大小和调度策略等属性封装在 `pthread_attr_t` 对象中。该属性对象仅在创建线程时影响线程。你首先创建一个属性对象，并将栈大小、调度策略等属性与该对象关联。然后你可以通过将线程属性对象传递给 `pthread_create` 创建多个具有相同属性的线程。通过将属性分组到对象中，POSIX 避免了带有大量参数的 `pthread_create` 调用。

### 表 12.3 POSIX 线程属性对象的可设置属性总结。

| 属性 | 函数 |
| --- | --- |
| 属性对象 | `pthread_attr_destroy`<br>`pthread_attr_init` |
| 状态 | `pthread_attr_getdetachstate`<br>`pthread_attr_setdetachstate` |
| 栈 | `pthread_attr_getguardsize`<br>`pthread_attr_setguardsize`<br>`pthread_attr_getstack`<br>`pthread_attr_setstack` |
| 调度 | `pthread_attr_getinheritsched`<br>`pthread_attr_setinheritsched`<br>`pthread_attr_getschedparam`<br>`pthread_attr_setschedparam`<br>`pthread_attr_getgetchedpolicy`<br>`pthread_attr_setschedpolicy`<br>`pthread_attr_getscope` |

`pthread_attr_init` 函数用默认值初始化线程属性对象。`pthread_attr_destroy` 函数将被销毁的属性值设置为无效。POSIX 未规定对象在销毁后的行为，但该变量可以初始化为新的线程属性。`pthread_attr_init` 和 `pthread_attr_destroy` 都接受一个单一参数，该参数是指向 `pthread_attr_t` 属性对象的指针。

### 语法概要

```
#include <pthread.h>
nint pthread_attr_destroy(pthread_attr_t *attr);
int pthread_attr_init(pthread_attr_t *attr);
```

POSIX:THR

如果成功，`pthread_attr_destroy` 和 `pthread_attr_init` 返回 0。如果失败，函数返回非零错误代码。如果没有足够的内存来创建线程属性对象，`pthread_attr_init` 会将 `errno` 设置为 `ENOMEM`。

大多数的 get/set 线程属性函数有两个参数。第一个参数是指向属性对象的指针。第二个参数是设置操作中属性的新值，或者是用于获取操作中存储该值的内存指针。`pthread_attr_getstack` 和 `pthread_attr_setstack` 则各有一个参数。

### 12.6 线程状态

`pthread_attr_getstate` 函数检查属性对象的状态，`pthread_attr_setstate` 设置属性对象的状态。线程状态的可能值为 `PTHREAD_JOINABLE`（可结合）和 `PTHREAD_DETACHED`（分离的）。`attr` 参数是指向属性对象的指针。`detachstate` 参数对应于 `pthread_attr_setstate` 设置的值以及 `pthread_attr_getstate` 获取的值。

### 语法概要

```
#include <pthread.h>
int pthread_attr_getstate(const pthread_attr_t *attr, int *detachstate);
int pthread_attr_setstate(pthread_attr_t *attr, int detachstate);
```

POSIX:THR

如果成功，函数返回 0。如果失败，它们返回负错误代码。如果 `detachstate` 无效，`pthread_attr_setstate` 会将 `errno` 设置为 `EINVAL`。

分离线程在终止时释放其资源，而可结合线程则需要通过 `pthread_join` 进行等待。默认情况下，线程是可的。你可以通过调用 `pthread_detach` 函数来分离线程。或者，你可以使用带有 `PTHREAD_CREATE_DETACHED` 属性的属性对象以分离状态创建线程。

### 示例 12.15

以下代码段创建了一个运行 `processfd` 的分离态线程。

```c
int error, fd;
pthread_attr_t tattr;
pthread_t tid;

if (error = pthread_attr_init(&tattr))
    fprintf(stderr, "创建属性对象失败: %s\n", strerror(error));
else if (error = pthread_attr_setstate(&tattr, PTHREAD_CREATE_DETACHED))
    fprintf(stderr, "设置分离状态失败: %s\n", strerror(error));
else if (error = pthread_create(&tid, tattr, processfd, fd))
    fprintf(stderr, "创建线程失败: %s\n", strerror(error));
```

### 12.6.2 线程栈

线程具有用户设置的位置，如果线程栈必须放在内存的特定区域，该属性非常有用。要定义线程栈的位置和大小，你必须首先创建一个指定栈属性的属性。然后使用此属性对象调用 `pthread_create`。

`pthread_attr_getstack` 函数检查栈参数，`pthread_attr_setstack` 设置属性对象的栈参数。每个函数的 `attr` 参数都是指向属性对象的指针。`pthread_attr_setstack` 函数将栈地址和栈大小作为额外参数。`pthread_attr_getstack` 则获取这些项的指针。

### 语法概要

```
#include <pthread.h>

int pthread_attr_getstack(const pthread_attr_t *restrict attr, void **restrict stackaddr, size_t *stacksize);
int pthread_attr_setstack(pthread_attr_t *attr, void *stackaddr, size_t stacksize);

                               POSIX:THR, TSA, TSS
```

如果成功，函数返回 0。如果失败，它们返回负错误代码。如果 `stacksize` 超出范围，`pthread_attr_setstack` 函数会将 `errno` 设置为 `EINVAL`。

POSIX 还提供了用于检查或设置栈溢出保护（guard）的函数，其中 `thread_attr_getguardsize` 函数用于检查保护参数，而 `thread_attr_setguardsize` 函数用于设置属性对象中控制栈溢出的保护参数。如果 `guardsize` 参数为 0，则栈不受保护。对于非零的 `guardsize`，实现将分配至少为 `guardsize` 大的额外内存。溢出到此额外内存会导致错误，并可能为线程产生 `SIGSEGV` 信号。

### 概要
