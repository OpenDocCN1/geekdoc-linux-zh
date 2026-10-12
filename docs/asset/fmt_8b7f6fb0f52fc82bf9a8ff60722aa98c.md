
## `wait( )`, `waitPID( )`

等待并确认子进程的终止。这对于防止僵尸进程在进程表中滞留以及释放宝贵资源非常重要。`wait( )` 调用等待任何进程终止，而 `waitPID( )` 调用允许您指定特定的进程或组。您可以使用以下宏来获取状态的含义：

- 如果子进程正常退出，`WIFEXITED(status)` 为非零。
- `WEXITSTATUS(status)` 计算为终止的子进程返回码的低八位，该返回码可能被设置为对 `exit( )` 调用的参数，或作为主程序中 `return` 语句的参数。只有当 `WIFEXITED` 返回非零时，才能计算此宏。
- 如果子进程因未捕获的信号而退出，`WIFSIGNALED(status)` 返回 `true`。
- `WTERMSIG(status)` 返回导致子进程终止的信号编号。只有当 `WIFSIGNALED` 返回非零时，才能计算此宏。
- 如果导致返回的子进程当前已停止，`WIFSTOPPED(status)` 返回 `true`；这仅在使用 `WUNTRACED` 执行调用时才可能。
- `WSTOPSIG(status)` 返回导致子进程停止的信号编号。只有当 `WIFSTOPPED` 返回非零时，才能计算此宏。

### 原型

```c
#include <sys/types.h>
#include <sys/wait.h>

PID_t wait(int *status);
PID_t waitpid(PID_t PID, int *status, int options);
```

### 返回值

两个调用均返回终止的子进程的 `PID`。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `status` | 返回子进程的终止状态。如果不为零或 `NULL`，此参数将获取子进程的终止代码和 `exit( )` 值。 |
| `PID` | 指示要等待哪个进程：<br>- -1: 等待进程组 ID 等于 `PID` 绝对值的任何子进程。<br>- -1: 等待任何子进程；这与 `wait()` 表现的行为相同。<br>- 0: 等待进程组 ID 等于调用进程进程组 ID 的任何子进程。<br>- > 0: 等待进程 ID 等于 `PID` 值的子进程。 |
| `options` | - `WNOHANG`: 如果没有子进程退出，立即返回。<br>- `WUNTRACED`: 对已停止且状态尚未报告的子进程返回。 |

### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `ECHILD` | 如果 `PID` 中指定的进程不存在或不是调用进程的子进程。（对于自己的子进程，如果 `SIGCHLD` 的动作被设置为 `SIG_IGN`，可能会发生这种情况。） |
| `EINVAL` | 如果 `options` 参数无效。 |
| `EINTR` | 如果未设置 `WNOHANG`，并且捕获了未屏蔽的信号或 `SIGCHLD`。只需重试即可。 |

### 示例

```c
void sig_child(int signum) /* 此处理器只获取一个等待的僵尸进程 */
{
    int status;
    wait(status);

    if ( WIFEXITED(status) )
        printf("Child exited with the value of %d\n", WEXITSTATUS(status));

    if ( WIFSIGNALED(status) )
        printf("Child aborted due to signal #%d\n", WTERMSIG(status));

    if ( WIFSTOPPED(status) )
        printf("Child stopped on signal #%d\n", WSTOPSIG(signal));
}

void sig_child(int signum) /* 此处理器移除所有等待的僵尸进程 */
{
    while ( waitpid(-1, 0, WNOHANG) > 0 );
}
```

## 线程

线程是另一种类型的任务。本节定义了 `pThreads` 库中的几个库调用。

## `pthread_create()`

此调用创建一个轻量级内核进程（线程）。该线程从 `start_fn` 指向的函数开始，使用 `arg` 作为函数参数。当函数返回时，线程终止。函数应返回一个 `void*` 值，但如果它不返回，线程仍会终止，且结果被设置为 `NULL`。

### 原型

```c
#include <pthread.h>

int pthread_create(pthread_t *tchild, pthread_attr_t *attr,
void (*start_fn)(void*), void *arg);
```

### 返回值

如果成功，这是一个正值。如果线程创建调用遇到任何错误，该调用返回一个负值，并将 `errno` 设置为该错误。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `thread` | 线程句柄（通过引用传递）。如果成功，该调用将线程句柄放入此参数中。 |
| `attr` | 线程的起始属性。有关更多信息，请参阅 `pthread_attr_init`。 |
| `start_fn` | 线程启动的例程。此函数应返回一个 `void*` 值。 |
| `arg` | 传递给 `start_fn` 的参数。您应该将此参数设为非共享内存引用（除非您打算加锁）且非堆栈内存引用。 |

### 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `EAGAIN` | 系统资源不足，无法为新线程创建进程。 |
| `EAGAIN` | 已经有超过 `PTHREAD_THREADS_MAX` 个线程处于活动状态。 |

### 示例

```c
void* child(void *arg)
{
    /**** 做点什么！ ****/
    pthread_exit(arg); /* 终止并返回 arg */
}

int main()
{
    pthread_t tchild;
    if (pthread_create(&tchild, 0, child, 0) < 0 )
        perror("Can't create thread!");

    /**** 做点什么！ ****/
    if (pthread_join(tchild, 0) != 0 )
        perror("Join failed");
}
```

## `pthread_join()`

类似于 `wait()` 系统调用，此调用等待并接受子线程的返回值。

### 原型

```c
#include <pthread.h>

int pthread_join(pthread_t tchild, void **retval);
```

### 返回值

如果成功，为正值。如果线程创建调用遇到任何错误，该调用返回一个负值，并将 `errno` 设置为该错误。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `thread` | 要等待的线程句柄 |
| `retval` | 指向传回值的指针（通过引用传递） |

### 可能的错误

- `ESRCH`：无法找到与 `tchild` 指定的线程对应的线程。
- `EINVAL`：`tchild` 线程已被分离。
- 另一个线程已经在等待 `tchild` 终止。
- `EDEADLK`：`tchild` 参数指向调用线程本身。

### 示例

（参见 `pthread_create()`）

#### `pthread_exit()`

显式终止当前线程，并返回 `retval`。您也可以使用简单的 `return` 语句。

### 原型

```c
#include <pthread.h>

void pthread_exit(void *retval);
```

### 返回值

（无）

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `retval` | 要返回的 `void*` 值。请确保该值不是栈内存。 |

### 可能的错误

（无）

### 示例

（参见 `pthread_create()`）

#### `pthread_detach()`

将 `tchild` 线程从父进程中分离。通常，您需要等待或加入（`join`）每一个进程和线程。此调用允许您创建多个线程并忽略它们。这与在创建时设置线程属性相同。

### 原型

```c
#include <pthread.h>

int pthread_detach(thread_t tchild);
```
