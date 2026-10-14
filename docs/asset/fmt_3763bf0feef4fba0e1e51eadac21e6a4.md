
- 如果程序在管道中，它打印所有进程产生的输出。为了测试它是否是初始（或最终）进程，程序使用 `isatty()` 函数（第 10 章）检查其标准输入（或输出）是否为终端。如果文件描述符指向管道，`isatty()` 返回 `false` (`0`)。程序构建传递给后继进程的消息。该消息指示此进程在管道中的位置。因此，对于初始进程，消息包含数字 `1`。如果是初始进程，消息初始化为 `0`。如果不是初始进程，程序从前驱进程读取消息。程序在继续下一步之前递增消息值。无论其在管道中的位置如何，程序都会显示包含其管道位置、进程 ID、父进程 ID、进程组 ID 和会话 ID 的行。除非它是管道中的最后一个命令，否则程序会为后继进程写入整数消息。最后，程序无限循环并使用 `pause()` 等待信号。

### 列表 34-5：观察作业控制下的进程

```c
#define _GNU_SOURCE             /* 获取 strsignal() 的声明 */
#include <string.h>
#include <signal.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

/* 各信号的处理器 */
static int cmdNum;               /* 在管道中的位置 */
static void handler(int sig)
{
    if (sig == SIGSTOP) /* 如果我们捕获到 SIGSTOP，它不会停止我们。因此我们引发 SIGSTOP 以真正停止。 */
        raise(SIGSTOP);

    if (getpid() == getppid()) /* 如果是进程组长
        printf(stderr, "Terminal FG group process: %ld\n", (long) tcgetgrp(STDIN_FILENO));

    printf(stderr, "Process %ld received signal %d (%s)\n", (long) getpid(), sig, strsignal(sig));
}

int main(int argc, char *argv[])
{
  struct sigaction sa;
  sigemptyset(&sa.sa_mask);
  sa.sa_flags = SA_RESTART;
  sa.sa_handler = handler;
  if (sigaction(SIGINT, &sa, NULL) == -1)
    errxit("sigaction");
  if (sigaction(SIGSTOP, &sa, NULL) == -1)
    errxit("sigaction");
  if (sigaction(SIGCONT, &sa, NULL) == -1)
    errxit("sigaction");

  if (isatty(STDIN_FILENO)) /* 如果 stdin 是终端，这是管道中的第一个进程：
    printf(stderr, "Terminal FG group process: %ld\n", (long) tcgetgrp(STDIN_FILENO));
    printf(stderr, "Command PIP PIPP SID:%d\n", getid());
    cmdNum = 0;
  } else {
    if (read(STDIN_FILENO, &cmdNum, sizeof(cmdNum)) <= 0)
      fatal("read failed: EOF or error");
  }
  cmdNum++;
  printf(stderr, "%4d %ld %ld %ld\n", cmdNum, (long) getpid(), (long) getppid(), (long) getpgrp(STDERR_FILENO));

  /* 如果不是最后一个进程，将消息传递给下一个进程 */
  if (!isatty(STDOUT_FILENO)) /* 如果不是 tty，应该是管道 */
    if (write(STDOUT_FILENO, &cmdNum, sizeof(cmdNum)) == -1)
      errMsg("write failed");

  for(;;)
    /* 等待信号 */
    pause();
}
```

以下 shell 会话演示了列表 3-5 中程序的使用。

我们首先显示 shell 的进程 ID（它是会话领导者，也是它所处唯一成员进程组的领导者），并创建一个包含两个进程的后台作业：

```
$ $ 
1204
$ ./job_mon | ./job_mon & 
[1] 1227
Terminal FG process group: 1204
Command PID PPID PGRP SID
1 1226 1024 1226 1204
2 1227 1224 1226 1204
```

显示 shell 的 PID

启动一个包含 2 个进程的作业

从上面的输出中，我们可以看到 shell 仍然是终端的前台进程。我们还可以看到新作业与 shell 处于同一会话中，所有的进程都在同一个进程组中。查看进程 ID，可以看到作业中进程的创建顺序与命令行上给出命令的顺序相同。（大多数 shell 都是这样做，但某些实现按不同的顺序创建进程）。

我们继续操作，创建一个由三个进程组成的后台作业：

```
$ ./job_mon | ./job_mon | ./job_mon & 
[2] 1230
Terminal FG process group: 1204
Command PID PPID PGRP SID
1 1228 1024 1228 1204
2 1229 1024 1228 1204
3 1230 1024 1228 1204
```

我们看到 shell 仍然是终端的前台进程。我们还看到新作业中的进程与 shell 在同一会话中，但与第一个作业处于不同的进程组。现在我们将第二个作业调入前台并向它发送一个 SIGINT 信号：

```
$ fg
./job_mon | ./job_mon | ./job_mon
Type Control-C to generate SIGINT (signal 2)
Process 1230 (3) received signal 2 (Interrupt)
Process 1229 (2) received signal 2 (Interrupt)
Terminal FG group: 1228
Process 1228 (1) received signal 2 (Interrupt)
```

从上面的输出中，我们看到 SIGINT 信号被传递给了终端前台进程的所有进程。接下来，我们向作业发送一个 SIGSTP 信号：

```
Type Ctrl-Z to generate SIGSTP (signal 20 on Linux/x86-32).
Process 1230 (3) received signal 20 (Stopped)
Process 1229 (2) received signal 20 (Stopped)
Terminal FG group: 1228
Process 1228 (1) received signal 20 (Stopped)
```

+ [2]+ Stopped ./job_mon | ./job_mon | ./job_mon

现在进程组组的所有成员都已停止。输出表明进程组 1228 是前台作业。然而，在该作业停止后，shell 变为了前台进程组，尽管我们无法从输出中判断出这一点。

随后我们通过 `bg` 命令重启作业，该命令向作业中的进程发送一个 SIGCONT 信号：

```
$ bg                    Resume job in background
[2]+./job_mon | ./job_mon | ./job_mon &
Process 1230 (3) received signal 18 (Continued)
Process 1229 (2) received signal 18 (Continued)
Terminal FG process group: 1204      The shell is in the foreground
Process 1228 (1) received signal 18 (Continued)
$ kill %1                                 We finished: clean up
[1]- Terminated         ./job_mon | ./job_mon
[2]+ Terminated         ./job_mon | ./job_mon | ./job_mon
```

### 34.7 处理作业控制信号
