
### pthread_mutex_lock()

#### 返回值

该调用成功时返回零，出错时返回非零。你可以在 `errno` 中找到确切的代码。

#### 参数

| 参数 | 描述 |
| :--- | :--- |
| `mutex` | 信号量变量 |

#### 可能的错误

| 错误代码 | 描述 |
| :--- | :--- |
| `EINVAL` | 互斥锁未正确初始化。 |
| `EADLK` | （`pthread_mutex_trylock`）调用线程已经锁定了互斥锁（仅限错误检查互斥锁）。 |
| `EBUSY` | （`pthread_mutex_lock`）由于当前已被锁定，调用线程无法获取。 |

#### 示例

```c
pthread_mutex_t mutex = fastmutex;

...

if (pthread_mutex_lock(&mutex) == 0)
{
    /**** 处理临界数据 ****/
    pthread_mutex_unlock(&mutex);
}

pthread_mutex_t mutex = fastmutex;

...

/*--等待信号量时进行其他处理--*/
while (pthread_mutex_trylock(&mutex) != 0 && errno == EBUSY)
{
    /**** 等待时处理其他事务 ****/
}

/*--获取信号量！现在处理临界区--*/
if (errno != EBUSY) // 注意：原文说 ENOERROR 不存在，可能是 EBUSY 或 0 检查
{
    /**** 处理临界数据 ****/
    pthread_mutex_unlock(&mutex);
}
```

### pthread_mutex_unlock()

解锁互斥信号量。

#### 原型

```c
#include <pthread.h>

int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

#### 返回值

该调用成功时返回零，出错时返回非零。你可以在 `errno` 中找到确切的代码。

#### 参数

| 参数 | 描述 |
| :--- | :--- |
| `mutex` | 信号量变量 |

#### 可能的错误

| 错误代码 | 描述 |
| :--- | :--- |
| `EINVAL` | 互斥锁未正确初始化。 |
| `EPERM` | 调用线程不拥有该互斥锁（仅限错误检查互斥锁）。 |

#### 示例

（参见 `pthread_mutex_lock()`）

## 信号

在处理任务时，你的程序可能会接收到信号（或异步通知）。本节描述允许你捕获和处理这些信号的系统调用。

### signal()

注册 `sig_fn` 例程以响应 `signum` 信号。默认行为是单次触发；在接收到第一个信号后，信号处理程序会恢复为默认状态。如果你想要更多地控制行为，请改用 `sigaction()`。

#### 原型

```c
#include <signal.h>

void (*signal(int signum, void (*sig_fn)(int signum)))(int signum);

- 或 -

typedef void (*TSigFn)(int signum);

TSigFn signal(int signum, TSigFn sig_fn);
```

#### 返回值

成功时返回正值。如果线程创建调用遇到任何错误，该调用返回负值并将 `errno` 设置为错误代码。

#### 参数

- `signum`：要捕获的信号号。
- `sig_fn`：调度程序调用的程序例程。

#### 可能的错误

（未设置 `errno`）

#### 示例

```c
void sig_handler(int signum)
{
    switch (signum)
    {
        case SIGFPE:
            ...
    }
}

...

if (signal(SIGFPE, sig_handler) == 0)
    perror("signal() 失败");
```

### sigaction()

与 `signal()` 类似，`sigaction()` 建立特定信号的接收者。然而，与 `signal()` 不同，此调用使你对信号通知行为拥有更多的控制权。其使用也稍微复杂一些。

#### 原型

```c
#include <signal.h>

int sigaction(int signum, const struct sigaction *sigact,
              struct sigaction *oldsigact);
```

#### 返回值

成功时为零；否则为非零。

#### 参数

- `signum`：要捕获的信号。
- `sigact`：所需的行为和信号处理程序，使用以下结构：

```c
struct sigaction
{
    void (*sa_handler)(int);
    sigset_t sa_mask;
    int sa_flags;
    void (*sa_restorer)(void);
};
```

- `sa_handler`：信号处理程序函数指针。
- `sa_mask`：在信号处理程序中处理信号期间要阻止的信号集。
- `sa_flags`：如何处理信号。你可以使用以下标志：
    - `SA_NOCLDSTOP`：如果信号是 `SIGCHLD`，忽略子进程停止或暂停的情况。
    - `SA_ONESHOT` 或 `SA_RESETHAND`：在接收到第一个信号后，将处理程序重置为默认值。
    - `SA_RESTART`：尝试重新启动被中断的系统调用。通常，被中断的系统调用返回 `EINTR` 错误。此选项尝试重新调用并避免 `EINTR` 错误。
    - `SA_NODEFER` 或 `SA_NOMASK`：允许类似信号中断处理程序。通常，如果你的处理程序正在响应诸如 `SIGCHLD` 的特定信号，内核会暂停其他 `SIGCHLD` 信号。这可能导致信号丢失。使用此选项允许你的处理程序被中断。使用此选项时请小心。
- `sa_restorer`：已废弃；请勿使用。
- `oldsigact`：旧行为的存储库。你可以在此处复制旧设置。

#### 可能的错误

- 指定了无效信号。如果尝试更改无法捕获的 `SIGKILL` 或 `SIGSTOP` 的动作，也会生成此错误。
- `sigact` 或 `old_sigact` 参数指向的内存不是进程地址空间的有效部分。
- 系统调用被中断。

#### 示例

```c
void sig_handler(int signum)
{
    switch (signum)
    {
        case SIGHCHLD:
            ...
    }
}

struct sigaction sigact;

bzero(&sigact, sizeof(sigact));

sigact.sa_handler = sig_handler;      /* 设置处理程序 */

sigact.sa_flags = SA_NOCLDSTOP | SA_RESTART; /* 设置选项 */

if (sigaction(SIGHCHLD, &sigact, 0) == 0)
    perror("sigaction() 失败");
```

### sigprocmask()

在处理信号期间，设置允许哪些信号中断当前操作。

#### 原型

```c
#include <signal.h>

int sigprocmask(int how, const sigset_t *sigset, sigset_t *oldsigset);
```
