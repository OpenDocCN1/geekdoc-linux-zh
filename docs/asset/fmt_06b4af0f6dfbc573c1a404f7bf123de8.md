
```
$ cat orphan.c ...列出程序。
#include <stdio.h>
main () {
  int pid;
  printf("I'm the original process with PID %d and PPID %d.\n",
      getpid(), getppid());
  pid = fork (); /* 复制。子进程和父进程从这里继续 */
  if (pid != 0) /* 根据 fork () 的返回值进行分支 */
  {
    /* pid 不为零，所以我必须是父进程 */
    printf("I'm the original process with PID %d and PPID %d.\n",
      getpid(), getppid());
    printf("My child's PID is %d\n", pid);
  }
  else
  {
    /* pid 为零，所以我必须是子进程 */
    sleep(5); /* 确保父进程先终止 */
    printf("I'm the child process with PID %d and PPID %d.\n",
      getpid(), getppid());
  }

  printf("PID %d terminates.\n", getpid()); / * 两个进程都执行
此句: */
$ orphan ...运行程序。
I'm the original process with PID 13364 and PPID 13363.
I'm the parent process with PID 13364 and PPID 13363.
PID 13364 terminates. ...父进程终止。
I'm the child process with PID 13365 and PPID 13364.
PID 13365 terminates. ...子进程终止。
$-
```

图 13.35 演示了孤儿化的效果。![](img/4245b8ee77539f33ff090ce0a0dd7eb6_509_0.png)

图 13.35

收养。

## 终止进程：`exit()`

进程可以随时通过执行 `exit()` 来终止，其工作原理如图 13.36 所示。子进程的终止代码可能被父进程用于。

### 系统调用：`void exit(int status)`

`exit()` 关闭进程的所有文件描述符，释放代码、数据和栈，然后终止进程。当子进程终止时，它向父进程发送 `SIGCHLD` 信号并等待终止状态被接受。只有状态的低位被使用，因此值限制为 0–255。等待父进程接受其返回代码的进程是僵尸进程。内核通过将它们的 PPID 设置为 1 来确保所有终止的儿子都被“init”收养。“init”进程总是接受其孩子的返回代码。

`exit()` 不返回。

图 13.36

`exit()` 系统调用描述。

Shell 通过它们的特殊变量访问最后一个子进程的终止代码。例如，在以下代码中，C shell 将最后一个命令的终止代码存储在 `$status` 中：

```
% cat myexit.c ...列出程序。
#include <stdio.h>
main() {
    printf("I'm going to exit with return code 42\n");
    exit(42);
}
myexit ...运行程序。
I'm going to exit with return code 42
echo $status ...显示终止代码。
42
- _
```

在所有其他 shell 中，返回值存储在特殊 shell 变量 `$` 中。

## 僵尸进程

终止的进程在接受其返回代码之前无法离开系统。如果它的父进程已经死亡，它将已经被“init”进程收养，该进程总是接受其孩子的返回代码。然而，如果一个进程存活且从不执行 `wait()`，子进程的返回代码将永远不会被接受，该进程将保持为僵尸状态。僵尸进程不包含任何代码、数据或栈，因此不会占用大量的系统资源，但它仍然占据固定大小的进程表。过多的僵尸进程可能需要系统管理员干预。（详情请参见第 15 章）。

下一个程序创建了一个僵尸进程，这在 `ps` 工具的输出中有所体现。当我杀死父进程时，子进程被“init”收养并允许它安息息了。以下是代码：

```c
cat zombie.c ...列出程序。
#include <stdio.h>
#include <stdlib.h>
main() {
    int pid;
    pid = fork(); /* 从 fork() 复制值 */
    if (pid != 0) /* 根据 fork() 的返回值进行分支 */
    {
        while (1) /* 永远不终止，永远不执行 wait() */
            sleep(1000);
    }
    else
    {
        exit(42); /* 用一个奇怪的数字退出 */
    }
}
zombie & ...在后台执行程序。
[1] 13545
ps ...获取进程状态。
PID TT STAT TIME COMMAND
13535 p S 0:00-ksh (ksh) ...shell。
13542 p S 0:00 zombie ...父进程。
13546 p Z 0:00<defunct> ...僵尸子进程。
13547 p R 0:00 ps ...杀死父进程。
$ kill 13545
[1] Terminated zombie
$ ps ...注意僵尸现在消失了。
PID TT STAT TIME COMMAND
13535 p S 0:00-ksh (ksh)
13548 p R 0:00 ps
```

## 等待子进程：`wait()`

父进程可以通过执行 `wait()` 来等待其中一个子进程终止并接受其子进程的终止码，如图 13.37 所示。在下一个示例中，子进程在程序结束前通过执行返回值为 42 的 `exit()` 终止了。与此同时，父进程执行了 `wait()` 并挂起，直到接收到子进程的终止码。此时，父进程提供了有关子进程死亡的信息，并执行了程序的剩余部分。代码如下：

```c
cat mywait.c ...列出程序。
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
main ()
{
  int pid, status, childPid;
  printf("I'm the parent process and my PID is %d\n", getpid());
  pid = fork(); /* 复制 */
  if (pid != 0) { /* 根据 fork() 的返回值进行分支 */
    printf("I'm the parent process with PID %d and PPID %d\n", getpid(), getppid());
    childPid = wait(&status); /* 等待子进程终止。 */
    printf("A child with PID %d terminated with exit code %d\n", childPid, status >> 8);
  } else {
    printf("I'm the child process with PID %d and PPID %d\n", getpid(), getppid());
    exit(42); /* 用一个奇怪的数字退出 */
  }
  printf("PID %d terminates\n", getpid());
}
$ mywait ...运行程序。
I'm the parent process and my PID is 13464
I'm the child process with PID 13465 and PPID 13464
I'm the parent process with PID 13464 and PPID 13464
A child with PID 13465 terminated with exit code 42
PID 13465 terminates
```

### 系统调用：`pid_t wait(int* status)`

`wait()` 会导致进程挂起，直到其中一个子进程终止。成功调用 `wait()` 会返回终止子进程的 PID，并放置一个如下方式编码的状态码：

- 如果 `status` 的最右侧位为零，则最左侧字节包含子进程 `exit()` 或 `return()` 返回值的低八位。

- 如果最右侧位非零，则最右侧七位等于导致子进程终止的信号编号，如果子进程产生了核心转储（core dump），则最右侧位的剩余位为 1。

如果一个进程执行 `wait()` 且没有子进程，`wait()` 将立即返回 -1。如果一个进程执行 `wait()` 且其一个或多个子进程已经是僵尸进程，`wait()` 将立即返回其中一个僵尸的状态。

图 13.37：`wait()` 系统调用的描述。
