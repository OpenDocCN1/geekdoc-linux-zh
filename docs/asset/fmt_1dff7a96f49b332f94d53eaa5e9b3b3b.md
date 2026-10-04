
# 18.10.1 signal_c：捕获 SIGALRM 信号

`program_c`（图 18.11）使用 `alarm` 调用设置一个五秒后超时的定时器。程序提示输入文件名，如果用户在五秒内输入，则显示该文件名。如果用户正在响应，会产生 `SIGALRM`，它会调用信号处理程序将默认处置设置为 `foo`。

我们在 `main` 之前声明了 `alrm_handler` 函数的原型，并将其分配给 `act` 结构中类型为信号的 `sa_handler` 成员。对 `signal` 的调用为 `SIGALRM` 安装了此函数。

用户提示输入文件名，随后定时器立即启动。如果在超时时间内输入了文件名，则显示该文件名。产生 `SIGALRM`，导致 `alrm_handler` 的执行。我们分别带上不带文件名运行程序：

```
$ /a
Enter filename: signal.log
Filename: signal.log
$ /a
Enterter filename:
Signal 14 received, default filename: foo
$ kill -1 | grep 14
13) SIGPIPE 14) SIGALRM 15) SIGTERM 16) SIGUSR1
```

# 第 18 章：系统编程 II—进程控制

## 图 18.11 signal.c

```c
/* 程序：signal.c -- 等待 5 秒等待用户输入，然后
   产生一个指定了处理程序的 SIGALRM */

#include <stdio.h>
#include <unistd.h>
#include <signal.h>
#define BUFSIZE 100
#include "quit.h"

void alrm_handler(int signo);   /* 原型声明 */

char buf[BUFSIZE] = "foo\0";   /* 全局变量 */
int main(void) {
   int n;
   struct sigaction act;
   act.sa_handler = alrm_handler;   /* 指定处理程序 */
   if (sigaction(SIGALRM, &act, NULL) == -1) /* 安装处理程序 */
      quit("alarm", 1);

   fprintf(stderr, "Enter filename: %s"); /* 设置闹器；将递送 */
   alarm(5);
   n = read(STDIN_FILENO, buf, BUFSIZE); /* 5秒内 */
   if (n > 0)                           /* 如果用户输入 */
      fprintf(stderr, "Filename: %s\n", buf);
   exit(0);
}

void alrm_handler(int signo) {
   fprintf(stderr, "\nsignal %d received, default filename: %s\n", signo, buf);
   exit(1);
}
```

# 18.10.2 捕获终端信号

让我们开发另一个程序 `signal2.c`（图 18.12），它对 `SIGINT` 和 `SIGTSTP` 使用信号处理程序。这些信号来自键盘。我们还将忽略 `SIGQUIT`。使用 `sigaction` 将不同信号的处置设置为忽略。`Ctrl-Z` 产生 `SIGTSTP`，但我们捕获它并显示消息而不停止进程。我们也捕获 `Ctrl-C` (`SIGINT`)，当按下两次键时终止进程。`for` 循环让 `pause` 系统调用循环运行。`pause` 挂起执行直到接收到任何信号，此时它返回 `EINTR` 错误。现在让我们按顺序三个序列运行此程序：

## 图 18.12 signal2.c

```c
/* 程序：signal2.c -- 处理从终端产生的
   SIGINT 和 SIGTSTP，需要两次 Ctrl-C 终止 */

#include <stdio.h>
#include <signal.h>
#include "quit.h"

void tstp_handler(int signo);
void int_handler(int signo);
int count = 0;

/* Ctrl-Z 的处理程序 */
/* Ctrl-C 的处理程序 */

int main (void) {
   struct sigaction act1, act2, act3;
   act1.sa_handler = tstp_handler;
   act2.sa_handler = int_handler;
   act3.sa_handler = SIG_IGN;
   sigaction(SIGTSTP, &act1, NULL);
   sigaction(SIGINT, &act2, NULL);
   sigaction(SIGQUIT, &act3, NULL);

   fprintf(stderr, "Press Ctrl-C first, then Ctrl-C\n");
   for (;;)
      pause();
   exit(0);
}

/* 这两个信号的处置 */
/* 设置为处理程序 */
/* 忽略处置 */

void tstp_handler(int signo) {
   fprintf(stderr, "Can't stop this program\n");
}

void int_handler(int signo) {
   if (++count == 1)
      fprintf(stderr, "Press again\n");
   else
      quit("Quitting", 1);
}

/* 接收到信号时返回 */
/* 终止程序 */
```

```
$ ./a.out

Press Ctrl-Z first, then, Ctrl-C

Ctrl-Z

Can't stop this program

Ctrl-C

Press again

Ctrl-C

Quitting: Interrupted system call
```

信号忽略
From tstp_handler
From int_handler
From int_handler

在这里可以看到三个信号处理程序都在工作。到为止，我们处理了大部分从键盘生成的特定信号；在 18.11 节中，我们将使用 `kill` 生成任何信号。

当进程使用 `&` 在后台执行时，`SIGINT` 的处置被设置为 `SIG_IGN`，这就是为什么 `Ctrl-C` 无法终止后台进程。当进程使用 `nohup` 运行时，`SIGHUP` 的处置也被设置为 `SIG_IGN`；当连接中断时，进程不会终止。

# 18.11 killprocess.c：使用 fork-exec-wait 和 SIGCHLD

在看下一个程序之前，我们有一个新系统要讨论——`kill`。与其对应的命令，`kill` 系统调用向一个或多个进程发送信号：

```c
int kill(pid_t pid, int sig);
```

通常，我们通过 `pid = fork()` 获取子进程的 PID，然后使用 `kill(pid, SIGTERM)` 用 `SIGTERM` 杀死子进程。

为了巩固，让我们演示 `fork-exec-wait` 和信号处理机制的使用。程序 `killprocess.c`（图 18.3）运行用户输入的命令，如果命令在五秒内完成，则打印状态。如果没有完成，父进程使用 `kill` 发送 `SIGTERM` 来杀死子进程。

这次使用单个信号处理函数同时处理 `SIGCHLD` 和 `SIGALRM`。父进程 `fork` 出子进程，然后使用 `execvp` 运行用户指定的程序作为一个或多个参数。注意，这次父进程在 `fork` 之后没有等待子进程死亡。它从 `alarm(5)` 开始，该在接收到任何信号时返回。这里有两个信号之一可以唤醒父进程——`SIGCHLD` 或 `SIGALRM`。信号处理函数考虑了子进程可能执行或不执行。如果执行，将发出 `SIGCHLD`，`death_handler` 调用 `waitpid` 获取子进程的退出状态。否则，`death_handler` 等待 `SIGALRM` 然后用 `SIGTERM` 杀死进程。

## 图 18.13 killprocess.c

```c
/* 程序: killprocess.c -- 使用 fork 和 exec 运行用户定义的程序，
如果它在 5 秒内未完成，则将其杀死。 */

#include <stdio.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <signal.h>
#include <stdlib.h>

pid_t pid;

int main(int argc, char **argv) {
    int i;
    void death_handler(int signo); /* 这次是一个常用的信号处理函数 */
    struct sigaction act;
    act.sa_handler = death_handler;
    sigaction(SIGCHLD, &act, NULL); /* 这些信号的处理方式 */
    sigaction(SIGALRM, &act, NULL); /* 设置进入信号处理函数 */
    switch (pid = fork()) {
        case -1: fprintf(stderr, "Fork error\n");
        case 0: execvp(argv[1], &argv[1]); /* 执行命令 */
            perror("exec");
            break;
        default: alarm(5); /* 在 5 秒后发送 SIGALRM */
            pause(); /* 当接收到 SIGCHLD 信号时返回 */
            fprintf(stderr, "Parent dies\n");
    }
    exit(0);
}

void death_handler(int signo) { /* 这个通用处理器捕获 */
    int status;
    /* 正常终止的退出状态 */
    /* 但如果 */
    /* 命令未在 5 秒内完成 */ 则发送 SIGTERM 信号 */
    switch (signo) {
        case SIGCHLD: waitpid(-1, &status, 0); /* 等同于 wait() */
            fprintf(stderr, "Child dies; exit status: %d\n",
                WEXITSTATUS(status));
            break;
        case SIGALRM: if (kill(pid, SIGTERM) == 0)
            fprintf(stderr, "5 seconds over, child killed\n");
    }
}
```

## 第 18 章：系统编程——进程控制

# 599

```
进程死亡；退出状态: 0
父进程死亡
```

```
$ /a.out find /home -name a.out -print
/home/sumit/personal/project8/a.out
/home/sumit/personal/books_code/glass_ables/12/a.out
/home/sumit/personal/books_code/stevens_c/ch08/a.out
... 5 秒 ...
```

```
5 秒时间到，子进程被杀死
父进程死亡
```

`kill` 可以向当前进程发送信号。你仍然需要使用 `getpid` 在此处指定 PID，但 `raise` 库函数会为你完成这项工作。事实上，`raise(SIGTERM)` 等同于 `kill(getpid(), SIGTERM)`。

## 18.12 使用无命名管道的进程间通信 (IPC)

UNIX 为两个进程之间的通信有一套非常复杂的方案。在本节中，我们将讨论 shell 中可用的管道机制。

为了理解管道如何允许一个进程将其标准输出发送到另一个进程的标准输入，请想象使用磁盘文件执行类似的操作。一个进程可以向文件写入，另一个进程可以从文件中读取。这意味着随着数据从写入者流向读取者，文件的大小会不断增长。此外，如果读取者比写入者快，该系统将无法工作，它经常会追上写入者并读取到 EOF。没有流控制机制可以让一个进程阻塞直到另一个进程完成工作。操作系统理论家对这种现象有一个专门的名字——生产者-消费者问题。

管道解决了这两个问题。它是一个半双工通信通道，这意味着数据只向一个方向流动。它是一种可以使用 `read` 和 `write` 使用的文件类型，但它是通过 `pipe` 调用创建的：

```c
int pipe(int fds[2]);
```

`pipe` 接收一个两个整数的数组作为唯一参数，并填充填充两个文件描述符。写入 `fds[1]` 的任何内容都可以从 `fds[0]` 读取；0 和 1 的意义在管道中同样保留。对 `fds[1]` 调用 `write` 会填充一个固定大小的缓冲区（约 4-KB），而对 `fds[0]` 调用 `read` 会清空缓冲区，以便下一次写入可以填充它。

如果在读取期间缓冲区为空，操作将阻塞，直到缓冲区写入了数据。同样，对尚未读取的缓冲区进行写入也会阻塞。数据按照先入先出（FIFO）的原则读取，正如你所预期的，管道的文件类型是 FIFO，可以通过 `S_ISFIFO` 宏进行检查。

虽然管道最常两个进程共享，但一个简单的示例展示了它在单个进程中的用法：

```c
int n, fd[2]; char buf[100];
```

# 你的 UNIX/Linux：终极指南

```c
pipe(fd);
write(fd[1], "abcdefgh", 8 );
n = read(fd[0], buf, 8);
write(STDOUT_FILENO, buf, n);
```

- `fd[2]` 填充了两个描述符
- 向一个文件描述符写入并从另一个读回
- 打印从管道读取的内容

`pipe` 生成了两个文件描述符，`fd[0]` 和 `fd[1]`。我们简单地从 `fd[1]` 写入 `abcdefgh` 并从 `fd[0]` 读回；0 和 1 的意义在管道中同样保留。

## 18.12 与 fork 使用管道

为了理解管道如何工作，让我们首先检查 `pipe` 调用后描述符的状态。`pipe` 生成了两个文件描述符，`fd[0]` 和 `fd[1]`。我们简单地从 `fd[1]` 写入 `abcdefgh` 并从 `fd[0]` 读回；0 和 1 的意义在管道中同样保留。

要使用管道，通常的做法是在 `fork` 之前创建管道。这意味着管道在父子进程之间共享。

## 18.12.2 pipec：在管道中运行命令

下一个程序 `pipe2.c`（图 18.2）解决了这个问题。调用 `execvp` 运行 `cat` 命令可以确保 `cat` 的输出连接到管道的写端。

如果我们对父进程中的语句应用类似的推理，最终将导致 `tr` 的标准输入连接到管道的读端的情况。我们已经在 `cat` 和 `tr` 之间建立了一个管道。

## 图 18.14 pipe.c

```c
/* 程序: pipe.c -- 在两个进程之间共享管道。
我们数据从父进程流向子进程。 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(void) {
    int n, fd[2];
    char buf[100];
    if (pipe(fd) < 0)
        quit("pipe", 1);
    switch (fork()) {
        case 1: quit("Fork error", 2);
        case 0: close(fd[1]);
            n = read(fd[0], buf, 100); /* 从输入端读取 */
            write(STDOUT_FILENO, buf, n);
            break;
        default: close(fd[0]);
            write(fd[1], "Writing to pipe\n", 16); /* 向写端写入 */
    }
    exit(0);
}
```

## 图 18.15 pipe2.c

```c
/* 程序: pipe2.c -- 在管道中运行两个程序
子进程运行 cat，父进程运行 tr */

#include <unistd.h>
#include <stdio.h>
#include "quit.h"

int main(void) {
    int fd[2];                               /* 由 pipe() 填充 */
    if (pipe(fd) < 0)                       /* 现在管道有了四个描述符 */
        quit("pipe", 1);
    switch (fork()) {
        case -1: quit("fork", 2);
        case 0: close(fd[0]);                   /* 若 子进程 - 先关闭读端 */
            dup2(fd[1], STDOUT_FILENO);        /* 将标准输出连接到写端 */
            close(fd[1]);                      /* 关闭原始描述符 */
```
