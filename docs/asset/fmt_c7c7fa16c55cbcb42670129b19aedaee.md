
#### 列表 4.6 继续

注意，在临界区结束时恢复旧的取消状态，而不是无条件地设置为 `PTHREAD_CANCEL_ENABLE` 是非常重要的。这允许你从另一个临界区安全地调用 `process_transaction` 函数——在这种情况下，你的函数将保持它被调用时的取消状态。

### 4.2.3 何时使用线程取消

通常情况下，除非在特殊情况下，否则不使用线程取消来结束线程的执行是一个好主意。在正常运行期间，更好的策略是指示线程它应该退出，然后等待线程按照自己的顺序方式退出。我们将在本书的后续部分讨论与线程通信的技术，并在第 5 章“进程间通信”。

## 4.3 线程特定数据

与进程不同，同一个程序中的所有线程共享相同的地址空间。这意味着如果一个线程修改了内存中的一个值（例如全局变量），更改对所有其他线程都是可见的。这允许多个线程在不使用进程间通信机制（在第 5 章中描述）的情况下操作相同的数据。

然而，每个线程都有自己的调用堆栈。这允许每个线程执行不同的代码，并以通常的方式调用和返回子程序。与单线程程序一样，每个线程中每个子程序的调用都有自己的一组局部变量，这些变量存储在该线程的栈上。

然而，有时希望复制某个变量，以便每个线程都有单独的拷贝。GNU/Linux 通过为每个线程提供线程特定数据区域来支持这一点。存储在该区域中的变量会为每个线程复制一份，每个线程都可以修改其变量的拷贝而不影响其他线程。由于所有线程共享相同的内存空间，因此无法使用普通的变量引用访问线程特定数据。GNU/Linux 提供了特殊函数用于从线程特定数据区域设置和检索值。

你可以创建任意数量的线程特定数据项，每个项类型为 `void*`。项通过键进行引用。要创建一个新键，从而为每个线程创建一个新数据项，请使用 `pthread_key_create`。第一个参数是指向 `pthread_key_t` 变量的指针。该值可以被每个线程用于访问其对应数据项的拷贝。`pthread_key_t` 的第二个参数是一个清理函数。当每个线程退出时，GNU/Linux 会自动调用该函数，并传递与该键对应的线程特定值。这特别棘手，因为即使线程在执行的任意点被取消，清理函数也会被调用。如果线程特定值为 `NULL`，则不会调用清理函数。如果你不需要清理函数，可以传递 `NULL` 代替函数指针。

创建键后，每个线程可以通过调用 `pthread_setspecific` 设置其与该键对应的线程特定值。第一个参数是键，第二个是要存储的 `void*` 线程特定值。要检索线程特定数据项，请调用 `pthread_getspecific` 并传递键作为参数。

例如，假设你的应用程序将任务分配给多个线程。为了审计目的，每个线程都应该有一个单独日志文件，在其中记录线程任务的进度消息。线程特定数据区域是存储文件指针的方便地方。

### 列表 4.7 (tsd.c) 使用线程特定数据实现的每个线程日志文件

```c
#include <stdlib.h>
#include <pthread.h>
#include <stdio.h>

static pthread_key_t thread_log_key;

void close_thread_log(void* thread_log) {
  fclose((FILE*)thread_log);
}

void write_to_log(const char* message) {
  FILE* thread_log = (FILE*)pthread_getspecific(thread_log_key);
  fprintf(thread_log, "%s\n", message);
}

void thread_function(void* args) {
  char thread_log_filename[20];
  FILE* thread_log;

  /* 为此线程生成日志文件名。 */
  sprintf(thread_log_filename, "thread%d.log", (int) pthread_self());

  /* 打开日志文件。 */
  thread_log = fopen(thread_log_filename, "w");

  /* 将指针存储在 thread_log_key 下的线程特定数据中。 */
  pthread_setspecific(thread_log_key, thread_log);

  write_to_log("Thread starting.");

  /* 执行一些工作... */

  return NULL;
}

int main () {
  int i;
  pthread_t threads[5];

  /* 创建键以关联线程特定数据中的日志文件指针。
     使用 close_thread_log 清理文件指针。 */
  pthread_key_create(&thread_log_key, close_thread_log);

  /* 创建线程执行工作。 */
  for (i = 0; i < 5; ++i)
    pthread_create(&threads[i], NULL, thread_function, NULL);

  /* 等待所有线程完成。 */
  for (i = 0; i < 5; ++i)
    pthread_join(threads[i], NULL);

  return 0;
}
```

观察到 `thread_function` 没有关闭日志文件。这是因为日志文件已创建，且 `close_thread_log` 被指定为该键的清理函数。每当线程退出，GNU/Linux 都会调用该函数，传递线程日志键的线程特定值。该函数负责关闭日志文件。

## 4.3 线程特定数据 (Thread-specific Data)

### 4.3.1 清理处理器 (Cleanup Handlers)

线程特定数据键的清理函数对于确保线程在退出或被取消时不泄漏资源非常有用。然而，有时在不为每个线程创建重复的新的线程特定数据项的情况下，能够指定清理函数是有用的。GNU/Linux 为此目的提供了清理处理程序。

清理处理程序就是一个在线程退出时应该被调用的函数。该处理程序接收一个 `void*` 参数，其参数值在注册处理程序时提供——这使得使用同一个处理程序函数来处理多个实例变得非常简单。

清理处理程序是一种临时措施，仅当线程退出或被取消而不是完成特定代码区域的执行时，才用于释放资源。在正常情况下，当线程没有退出也没有被取消，应该显式地释放资源并移除清理处理程序。

要注册清理处理程序，请调用 `pthread_cleanup_push`，并传递处理程序的指针及其参数值。对 `pthread_cleanup_push` 的调用必须与相应的 `pthread_cleanup_pop` 调用匹配，后者会取消注册清理处理程序。为了方便，`pthread_cleanup_pop` 接受一个 `int` 标志；如果标志非零，则会在取消注册的同时实际执行清理操作。

列表 4.8 中的程序展示了如何使用清理处理程序来确保动态分配的缓冲区被清理。

列表 4.8 (cleanup.c) 展示线程清理的程序

```c
#include <malloc.h>
#include <pthread.h>

/* 分配一个临时缓冲区。 */
void* allocate_buffer(size_t size) {
    return malloc(size);
}

/* 释放临时缓冲区。 */
void deallocate_buffer(void* buffer) {
    free(buffer);
}

void do_some_work() {
    /* 分配一个临时缓冲区。 */
    void* temp_buffer = allocate_buffer(1024);

    /* 为此缓冲区注册清理处理器，以便在线程退出或被取消时释放它。 */
    pthread_cleanup_push(deallocate_buffer, temp_buffer);

    /* 执行一些可能会调用 pthread_exit 或被取消的工作... */

    /* 取消注册清理处理程序。因为在这种情况下 pthread_cleanup_pop 的参数是非零，所以清理函数 deallocate_buffer 在这里被自动调用，不需要显式调用。在简单简单的情况下，我们可以使用标准库函数 free 作为我们的清理处理程序。 */
}
```

### 4.3.2 C++ 中的线程清理

C++ 程序员习惯于通过在析构函数中封装操作来“免费”获得清理工作。当对象超出作用范围时（无论是因为块执行完毕还是因为抛出了异常），C++ 会确保对所有具有析构函数的自动变量调用析构函数。这提供了一种方便的机制，可以确保无论以何种方式退出块，清理代码都会被调用。

然而，如果线程调用了 `pthread_exit`，C++ 并不保证会对线程栈上的所有自动变量调用析构函数。恢复此功能的一种巧妙方法是通过抛出一个特殊异常，在线程的顶层调用 `pthread_exit`。列表 4.9 中的程序演示了这一点。使用这种技术，函数通过抛出 `ThreadExitException` 而不是调用 `pthread_exit` 来表示其退出线程的意图。异常在线程顶层中被捕获，随着异常向上传递，线程栈上的所有局部变量都将被正确销。

列表 4.9 (c-exit.cpp) 使用 C++ 实现安全的线程退出

```cpp
#include <pthread.h>

class ThreadExitException {
public:
    /* 创建一个带有返回值的用于信号线程退出的异常。 */
    ThreadExitException(void* return_value) : return_value_(return_value) {}

    /* 使用构造函数中提供的返回值实际退出线程。 */
    void* DoThreadExit() {
        pthread_exit(thread_return_value_);
    }

private:
    /* 退出线程时将使用的返回值。 */
    void* thread_return_value_;
};

void do_some_work() {
    while (1) {
        /* 在这里执行一些有用的事情... */
    }

    if (should_exit_thread_immediately())
        throw ThreadExitException(NULL /* 线程的返回值 = */ NULL);
}

void* thread_function(void*) {
    try {
        do_some_work();
    } catch (ThreadExitException ex) {
        /* 某些函数指示我们应该退出线程。 */
        ex.DoThreadExit();
    }
    return NULL;
}
```

## 4.4 同步与临界区 (Synchronization and Critical Sections)

使用线程进行编程非常复杂，因为大多数线程程序都是并发程序。特别是，没有办法知道系统何时调度一个线程运行，以及它何时运行。一个线程可能会运行很长时间，或者系统可能会在线程之间快速切换。在具有多个处理器的系统上，系统可能会让多个线程在字面上同一时刻运行。

调试线程程序是困难的，因为你总是无法重现导致问题的行为。你可能运行一次程序时一切正常；但下一次运行时，它可能会崩溃。没有方法能让系统调度线程的方式与之前完全相同。

大多数涉及线程的 bug 的根本原因是线程正在访问相同的数据。正如之前提到的，这会导致竞态条件。

### 4.4.1 竞态条件 (Race Conditions)

假设两个线程恰好同时检查队列，但只有一个任务剩余。第一个线程进入队列。此时，第二个线程也检查队列，发现它为空，但实际上任务正在被处理。在这种情况下，在队列为空时，线程函数可能看起来像列表 4.10 所示。

列表 4.10 (queue.c) 从队列处理任务的线程函数

```c
#include <malloc.h>
#include <pthread.h>

struct job {
    /* 分配一个临时缓冲区。 */
    struct job* next;

    /* 处理队列。 */
};

struct job* queue = NULL;

/* 处理队列。 */
void* thread_function(void* arg) {
    /* 分配一个临时缓冲区。 */
    struct job* next_job;

    while (queue != NULL) {
        /* 获取下一个任务。 */
        next_job = queue;
        queue = queue->next;

        /* 清理。 */
        free(next_job);
    }

    return NULL;
}
```

### 4.4.2 互斥锁 (Mutexes)

任务队列问题的解决方案是允许只有一个线程访问队列。线程开始查看队列时，其他线程不应该访问它，直到第一个线程决定是否处理任务并从列表中移除任务。实现这一点需要操作系统的支持。GNU/Linux 提供了互斥锁（mutexes）。互斥锁是一种特殊的锁，允许一次只有一个线程锁定。如果一个线程锁定互斥锁，然后另一个线程尝试锁定互斥锁，第二个线程会被阻塞或挂起。只有当第一个线程解锁互斥锁时，第二个线程才会被解除——允许恢复执行。GNU/Linux 保证在尝试锁定互斥锁的线程之间不会发生竞态条件；只有一个线程会获得锁，所有所有都被阻塞。

将互斥锁想象成厕所门上的锁。先进入厕所的人锁上门。如果有人在占用期间尝试进入，那个人会发现门锁着，被迫在外面等待，直到使用者离开。

要创建互斥锁，创建一个类型为 `pthread_mutex_t` 的变量，并将指针传递给 `pthread_mutex_init`。`pthread_mutex_init` 的第二个参数是互斥锁属性对象的指针，它指定了互斥锁的属性。正如

`pthread_create`，如果属性指针为空，则假设使用默认属性。互斥锁变量应初始化一次。这段代码片段演示了互斥锁变量的声明和初始化。

```
pthread_mutex_t mutex;
pthread_mutex_init(&mutex, NULL);
```

创建默认属性互斥锁的另一种简单方法是使用特殊值 `PTHREAD_MUTEX_INITIALIZER` 对其进行初始化。不需要额外调用 `pthread_mutex_init`。这对于全局变量（在 C++ 中则为静态数据成员）特别为方便。之前的代码片段可以写成这样：

```
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
```

线程可以通过对互斥锁调用 `pthread_mutex_lock` 来尝试锁定该互斥锁。如果互斥锁处于未锁定状态，它将变为锁定状态并且函数立即返回。如果互斥锁已被另一个线程锁定，`pthread_mutex_lock` 会阻塞执行，并在当另一个线程解锁该互斥锁时才返回。可能有多个线程同时阻塞在一个锁定的互斥锁上。当互斥锁被解锁时，只有阻塞线程中的其中一个（随机选择）会被解除阻塞并允许锁定互斥锁；其他线程保持阻塞状态。

调用 `pthread_mutex_unlock` 会解锁互斥锁。此函数应始终由锁定该互斥锁的线程调用。

列表 4.11 显示了任务队列示例的另一个版本。现在队列由互斥锁保护。在访问队列（无论是读还是写）之前，每个线程都会首先锁定互斥锁。只有当完成检查队列和移除任务的整个序列后，互斥锁才会被解锁。这防止了之前描述的竞态条件。

## 列表 4.11 由互斥锁保护的任务队列函数

```c
#include <stdlib.h>
#include <pthread.h>

struct job {
    /* 链表的连接字段。 */
    struct job* next;

    /* 其他描述待执行任务的字段... */
};

/* 等待任务的链表。 */
struct job* job_queue;

/* 保护 job_queue 的互斥锁。 */
pthread_mutex_t job_queue_mutex = PTHREAD_MUTEX_INITIALIZER;

/* 处理队列中的任务直到队列为空。 */
void thread_function(void* arg) {
    while (1) {
        struct job* next_job;

        /* 锁定任务队列上的互斥锁。 */
        pthread_mutex_lock(&job_queue_mutex);

        /* 现在检查队列是否为空是安全的。 */
        if (job_queue == NULL)
            next_job = NULL;
        else {
            /* 获取下一个可用任务。 */
            next_job = job_queue;
            /* 从列表中移除此任务。 */
            job_queue = job_queue->next;
        }

        /* 解锁任务队列上的互斥锁，因为我们现在已经处理完队列。 */
        pthread_mutex_unlock(&job_queue_mutex);

        /* 队列为空吗？如果是，则结束线程。 */
        if (next_job == NULL)
            break;

        /* 执行任务。 */
    }
}
```
