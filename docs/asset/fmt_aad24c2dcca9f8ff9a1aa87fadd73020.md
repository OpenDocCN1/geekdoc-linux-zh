
```c
pid_t pid = fork();

if (pid == 0) {

    child();

}

printf("parent sleeping\n");

// 在所有信号阻塞的情况下睡眠。

int r = sleep(3);

// r == 0 表示我们睡眠了整个时长。

printf("woke up! r=%d\n", r);

// 恢复信号掩码，
// 这导致我们的处理程序被调用。

sigprocmask(SIG_SETMASK, &oldset, NULL);

// 等待信号处理运行。

while (!done) {

}

printf("exiting\n");

exit(0);

}
```

列表 7-5 中的程序分派了一个立即退出的子进程。这导致父进程接收到 `SIGCHLD` 信号。然而，在你分派之前，你为 `SIGCHLD` 安装了信号处理程序并阻塞了 `SIGCHLD` 信号 3 秒。从睡眠返回后，立即恢复原始信号

# 376 第 7 章 进程间的通信

handler，它会解除 `SIGCHLD` 的阻塞。随后信号处理程序执行，证明了信号已经送达：

```
$ ./sigprocmask

child exiting

parent sleeping

woke up! r=0

handled...

exiting
```

此时 `SIGCHLD` 被发送给了父进程。
由于 `SIGCHLD` 被阻塞了，因此父进程进入睡眠。
返回 0 表示我们睡眠了 3 秒；仍然没有收到信号。
信号在信号掩码恢复后才被送达。

POSIX API 包含了几个额外的函数来处理哪些信号被阻塞的信号掩码。其原型如下：

```c
int sigpending(sigset_t *set);
int sigsuspend(const sigset_t *mask);
```

`sigpending` 允许你检查已发送但未送达的信号。在列表 7-5 中，你可以在睡眠之前测试信号掩码，并看到该信号。这并没有保证，因为 `sigpending` 不会等待信号；它只是对信号进行快照并将其呈现给调用者。这种技术也被称为轮询（polling）。如果你想等待特定的信号集而不等待其他信号，那么 `sigsuspend` 函数就是你需要的。该函数会用输入掩码临时覆盖信号掩码，直到信号送达。在返回之前，它会将信号掩码恢复到原始状态。

### 7.4.4 实时信号

敏锐的读者可能会注意到由于阻塞信号引起的几个问题。例如，如果在信号被阻塞期间发送了多个信号，会发生什么？值将保留在内核中，因此信号不会丢失；当进程取消信号屏蔽时，信号会立即送达。如果同一个信号在阻塞期间发送了两次，信号通常会被丢弃。当信号取消屏蔽时，信号处理程序只调用一次。

POSIX 引入实时信号是为了让应用程序能够多次接收信号，即使信号被阻塞也是如此。当实时信号被阻塞时，内核将跟踪接收信号的次数，并在信号解锁时调用相应次数的信号处理程序。

实时信号通过一系列信号范围来标识。该范围由宏 `SIGRTMIN` 和 `SIGRTMAX` 标识。如果你指定了这两个值之间的信号号，信号将被放入队列。列表 7-6 显示了一个示例。

## 7.4 信号

列表 7-6 rt-sig.c: 阻塞与实时信号

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>
volatile int done = 0;

// 信号处理程序
void handler(int sig) {
    // signal(2) - write() 是安全的，printf() 不安全。
    const char *str = "handled...\n";
    write(1, str, strlen(str));
    done = 1;
}

void child(void) {
    int i;
    for (i = 0; i < 3; i++) {
        // 向父进程发送快速触发的信号
        kill(getppid(), SIGRTMIN);
        printf("child - BANG!\n");
    }
    exit(0);
}

int main(int argc, char *argv[]) {
    // 处理来自子进程的 SIGRTMIN
    signal(SIGRTMIN, handler);
    sigset_t newset, oldset;
    // 阻塞所有信号并保存旧信号掩码
    // 以便我们稍后恢复
    sigfillset(&newset);
    sigprocmask(SIG_BLOCK, &newset, &oldset);
    // 分叉子进程
    pid_t pid = fork();
    if (pid == 0) {
        child();
    }
    printf("*parent sleeping\n");
    // 在所有信号被阻塞的情况下睡眠
    int r = sleep(3);
```

继续

```c
// ...

// // r = 0 表示我们睡眠了整个时长。
printf("woke up! r=%d\n", r);

// 恢复旧信号掩码，
// 这会导致我们的处理程序被调用。
sigprocmask(SIG_SETMASK, &oldset, NULL);

// 等待信号处理程序运行。
while (!done) {
};

printf("exiting\n");
exit(0);
```

列表 7-6 与列表 7-5 非常相似，不同在于它使用了 `SIGRTMIN` 而不是 `SIGCHLD`，并且子进程现在退出前会向父进程发送三次该信号。使用队列信号不需要特殊的标志。信号号告诉内核对信号进行排序。运行这个示例可以看到它是如何工作的：

```
$ ./rt-sig

child - BANG!
child - BANG!
child - BANG!

parent sleeping
woke up! r=0
handled...
handled...
handled...
handled...
exiting
```

在这里你再次看到，在信号掩码恢复之前，父进程不会被信号中断。当信号掩码恢复时，处理程序会被调用三次——对应子进程每次调用 `kill` 次。

### 7.4.5 使用 sigqueue 和 sigaction 的高级信号

最后，我们提到了 `kill` 系统调用的替代方案 `sigqueue`。其原型如下所示，看起来与 `kill` 系统调用非常相似，不同之处在于它接收一个值：

```c
int sigqueue(pid_t pid, int sig, const sigval *value);
```

## 7.4 信号

`sigqueue` 系统调用允许你在发送信号的同时带上值。当信号需要向信号处理程序传递信息时，这种方法非常有用。值是通过 `union sigval` 传递的，它可以包含一个整数或指针。

`sigqueue` 的原型是：

```c
int sigqueue(pid_t pid, int sig, const sigval *value);
```

当信号送达时，值位于 `siginfo` 结构中：

```c
struct siginfo {
    int si_signo;
    int si_code;
    int si_errno;
    pid_t si_pid;
    uid_t si_uid;
    void *si_addr;
    int si_status;
    long si_band;
    sigval si_value;
};
```

为了使用 `sigqueue` 提供的值，必须带有 `SA_SIGINFO` 标志使用 `sigaction`：

```c
void handler(int sig, struct siginfo_t *info, void *unused) {
    printf("收到值: %d\n", info->si_value.sivalint);
}

struct sigaction sa;
sa.sa_handler = (void (*)(int, struct siginfo_t *, void *))handler;
sigemptyset(&sa.sa_mask);
sa.sa_flags = SA_SIGINFO;
sigaction(SIGRTMIN, &sa, NULL);
```
