
当线程退出时，它不会释放其资源，除非它是一个分离线程（detached thread）。`pthread_detach`函数设置线程的内部选项，指定在线程退出时可以回收其存储空间。分离线程是不可汇合（joinable）的，在另一个线程调用`pthread_join`或整个进程退出之前，它们不会释放其所有资源。`pthread_join`函数导致调用者等待指定的线程退出，类似于进程层面的`waitpid`。为了防止内存泄漏，长时间运行的程序最终应对每个线程调用`pthread_detach`或`pthread_join`。

`pthread_detach`函数有一个参数`thread`，即要分离的线程的线程 ID。

### 语法

```c
#include <thread.h>

int pthread_detach(pthread_t thread);
```

> POSIX:THR

如果成功，`pthread_detach`返回 0。如果失败，`pthread_detach`返回非零错误代码。下表列出了`pthread_detach`的强制性错误。

| 错误 | 原因 |
| --- | --- |
| EINVAL | `thread`不对应的可汇合线程 |
| ESRCH | 没有找到 ID 为`thread`的线程 |

# 示例 12.5

接下来的代码段创建并分离一个线程来执行`processfd`函数。

```c
void *processfd(void *arg);

int error;
int fd;
pthread_t tid;

if (error = pthread_create(&tid, NULL, processfd, &fd))
    fprintf(stderr, "Failed to create thread: %s\n", strerror(error));
else if (error = pthread_detach(tid))
    fprintf(stderr, "Failed to detach thread: %s\n", strerror(error));
```

# 示例 12.6 detachfun.c

当`detachfun`作为线程执行时，它会将其自身分离。

```c
#include <pthread.h>
#include <stdio.h>

void *detachfun(void *arg) {
    int i = *(int *)arg;
    if (!pthread_detach(pthread_self()))
        return NULL;
    fprintf(stderr, "My argument is %d\n", i);
    return NULL;
}
```

分离线程的资源在另一个线程调用`pthread_join`并将终止线程的 ID 作为第一个参数之前，不会释放。`pthread_join`函数会挂起调用线程，直到第一个参数指定的目标线程终止。`value_ptr`参数提供了一个指向返回状态指针的位置，该状态是目标线程通过`pthread_exit`或`return`传递的。如果`value_ptr`为`NULL`，调用者将不获取目标线程的返回状态。

### 语法

```c
#include <pthread.h>

int pthread_join(pthread_t thread, void **value_ptr);
```

> POSIX:THR

如果成功，`pthread_join`返回 0。如果失败，`pthread_join`返回非零错误代码。下表列出了`pthread_join`的强制性错误。

| 错误 | 原因 |
| --- | --- |
| EINVAL | `thread`不对应的可汇合线程 |
| ESRCH | 没有找到 ID 为`thread`的线程 |

### 示例 12.7

下面的代码说明了如何获取由终止线程通过`pthread_exit`传递的值。

```c
int error;
int *exitcodep;
pthread_t tid;

if (error = pthread_join(tid, &exitcodep)) {
    fprintf(stderr, "Failed to join thread: %s\n", strerror(error));
} else {
    fprintf(stderr, "The exit code was %d\n", *exitcodep);
}
```

# 练习 12.8

如果一个线程执行它自己会发生什么？

```c
pthread_join(pthread_self());
```

### 答案：

假设该线程是可汇合的，该语句会导致死锁。某些实现会检测到死锁并强制`pthread_join`返回`EDELK`。然而，这不是主线程等待线程完成的唯一方法。

# 12.3.4 退出与取消

进程可以通过`exit`、从`main`函数返回或让一个线程调用`exit`来终止。在任何这些情况下，所有线程都会终止。如果主线程在创建线程后没有工作要做，它应该等待线程完成或调用`pthread_exit(NULL)`。

调用`exit`会导致整个进程终止；调用`pthread_exit`只导致线程终止。如果线程调用`pthread_exit`，进程将以状态0退出。

`value_ptr`值对于成功的`pthread_join`可用。然而，`pthread_exit`中的`value_ptr`必须指向退出后存在的数据，因此线程不应使用局部数据的指针。

### 语法

```c
#include <pthread.h>

void pthread_exit(void *value_ptr);
```

> POSIX:THR

POSIX 没有为`pthread_exit`定义任何错误。

线程可以通过取消机制强制其他线程返回。线程调用`pthread_cancel`请求取消另一个线程。目标的类型和可取消状态决定了结果。`pthread_cancel`的唯一参数是被取消线程的线程 ID。`pthread_cancel`函数不会导致调用者阻塞直到取消完成。相反，在发出取消请求后返回。

### 语法

```c
#include <pthread.h>

int pthread_cancel(pthread_t thread);
```

> POSIX:THR

如果成功，`pthread_cancel`返回 0。如果失败，`pthread_cancel`返回非零代码。`pthread_cancel`没有定义强制性错误。

当线程接收取消请求时发生什么取决于它的状态和类型。如果线程具有`PTHREAD_CANCEL_ENABLE`状态，它会接收取消请求。相反，如果线程具有`PTHREAD_CANCEL_DISABLE`状态，取消请求将保持挂起。默认情况下，线程具有`PTHREAD_CANCEL_ENABLE`状态。

`pthread_setcancelstate`函数更改调用线程的可取消状态。`pthread_setcancelstate`接受两个参数：`state`，指定要设置的新状态；以及`oldstate`，指向存储之前状态的整数指针。

### 概要

```c
#include <pthread.h>
```

```c
int pthread_setcancelstate(int state, int *oldstate); POSIX:THR
```

如果执行成功，`pthread_setcancelstate`返回 0。如果失败，它返回一个非零错误代码。`pthread_setcancelstate`没有定义任何强制性错误。

程序 12.3 显示了程序 12.1 中`processfd`函数的修改，该函数在调用`command`之前显式禁用了取消，以确保命令不会在执行途中被取消。原始的`processfd`在无法更改取消状态时总是返回 NULL。此函数不应返回自动局部变量的指针，因为变量在函数线程退出时会被释放。程序 12.3 使用由调用线程传递的参数来返回指针。

## 程序 12.3 processfdcancel.c

该函数监控文件描述符的输入，并调用`command`处理结果。它在调用`command`之前显式禁用了取消。

```c
#include <pthread.h>
#include "restart.h"
#define BUFSIZE 1024

void command(char *cmd, int cmdsize);

void *processfdcancel(void *arg) /* 处理带取消的命令 */ {
    char buf[BUFSIZE];
    int fd;
    ssize_t nbytes;
    int newstate, oldstate;

    fd = *((int *)(arg));
    for ( ; ; ) {
        if ((nbytes = r_read(fd, buf, BUFSIZE)) <= 0)
            break;
        if (pthread_setcancelstate(PTHREAD_CANCEL_DISABLE, &oldstate))
            return arg;
        command(buf, nbytes);
        if (pthread_setcancelstate(oldstate, &newstate))
            return arg;
    }
    return NULL;
}
```

作为一个通用规则，改变取消状态或类型的函数在返回之前应该恢复原来的值。除非遵守此规则，否则调用者无法对程序行为做出可靠假设。`processfdcancel`函数保存了旧状态并恢复它，而不是在调用`command`后仅仅启用取消。

如果线程持有资源（如锁或必须在退出前释放的文件描述符），那么取消可能会导致困难。线程使用`pthread_cleanup_push`和`pthread_cleanup_pop`维护一个清理例程栈（此处不进行讨论）。虽然被取消的线程可以在退出前取消一个函数（未讨论），但在处理程序中释放资源并不总是的。此外，执行过程中可能存在某些点，此时退出会导致资源处于不可接受的状态。取消允许`PTHREAD_CANCEL_ASYNCHRONOUS`类型的线程响应取消请求。它可以在任何时间响应取消。相比之下，`PTHREAD_CANCEL_DEFERRED`取消类型导致线程仅指定的取消点对取消请求做出响应。默认情况下，线程的类型为`PTHREAD_CANCEL_DEFERRED`。

`pthread_setcanceltype`函数根据其`type`参数更改线程的可取消性。`oldtype`参数是一个指向之前类型存储位置的指针。线程可以通过调用`pthread_testcancel`在代码的特定位置设置取消点。某些阻塞函数（如`read`）会被自动视为取消点。类型为`PTHREAD_CANCEL_DEFERRED`的线程在到达此类点时会接受挂起的取消请求。

### 概要

```c
#include <pthread.h>
int pthread_setcanceltype(int type, int *oldtype);
void pthread_testcancel(void);
```

POSIX:THR

如果执行成功，`pthread_setcanceltype`返回 0。如果失败，它返回一个非零错误代码。`pthread_setcanceltype`没有定义任何强制性错误。`pthread_testcancel`没有返回值。

## 12.3.5 向线程传递参数和返回值

线程的创建者可以在创建时使用指向`void`的指针向线程传递单个参数。为了通信多个值，创建者必须使用指向数组或结构体的指针。程序 12.4 阐述了`main`进程如何将一个包含两个打开的文件描述符的数组的指针传递给运行`copyfilealloc`的线程。

## 程序 12.4 callocymalloc.c

```c
#include <errno.h>
#include <fcntl.h>
#include <pthread.h>
#include <stdio.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#define PERMS (S_IRUSR | S_IWUSR) 
#define READ_FLAGS (O_RDONLY | O_CREAT | O_TRUNC)
#define WRITE_FLAGS (O_WRONLY | O_CREAT)

void *copyfilealloc(void *arg);

int main (int argc, char *argv[]) {
    int *bytesptr;
    int error;
    int fds[2];
    pthread_t tid;

    if (argc != 3) {
        fprintf(stderr, "Usage: %s fromfile tofile\n", argv[0]);
        return 1;
    }
    if ((fds[0] = open(argv[1], READ_FLAGS)) == -1) ||
        (fds[1] = open(argv[2], WRITE_FLAGS, PERMS)) == -1) {
        perror("open files");
        return 1;
    }
    if (pthread_create(&tid, NULL, copyfilealloc, fds) != 0) {
        perror("create thread");
        return 1;
    }
    if (pthread_join(tid, (void **)bytesptr) != 0) {
        perror("join thread");
        return 1;
    }
    return 0;
}
```
