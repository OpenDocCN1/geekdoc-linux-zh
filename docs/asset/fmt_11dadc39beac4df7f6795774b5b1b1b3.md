
当你处于 shell 中并执行创建一个若干子进程的程序时，键盘上的单个 `Ctrl-C` 通常会终止该程序及其子进程，并返回 shell。为了支持这种行为，UNIX 引入了几个新概念：

- 除了具有唯一的进程 ID 数字外，每个进程都是进程组的成员。多个进程可以是同一个进程组的成员。当进程 `fork` 时，子进程继承其父进程的进程组。进程可以使用 `setpgid()` 将其进程组更改为新值。当进程 `exec` 时，其进程组保持不变。

- 每个进程都可以关联一个控制终端——通常是启动该进程的终端。当进程 `fork` 时，子进程继承其父进程的控制终端。当进程 `exec` 时，其控制终端保持不变。

## 信号 (499)

- 每个终端都可以关联一个控制进程。当检测到如 `Control-C` 等元字符时，终端会向其控制进程进程组中的所有进程发送适当的信号。

- 如果进程尝试从其控制终端读取，且不是终端控制进程所在同一进程组的成员，则该进程将收到 `SIGTTIN` 信号，这通常会将其挂起。

以下是 shell 如何使用这些特性：

- 当交互式 shell 启动时，它是终端的控制进程，并将该终端作为其控制终端。这种情况超出了本书的范围。

- 当 shell 执行前台进程时，子 shell 在 `exec` 命令之前会将自己放入不同的进程组，并接管终端。因此，从终端生成的任何信号都会发送给前台命令，而不是原始父 shell。当前台命令终止时，原始父进程重新接管终端的控制。

- 当 shell 执行后台进程时，子 shell 在 `exec` 之前会将自己放入不同的进程组，但不接管终端。从终端生成的任何信号继续发送给 shell。如果后台进程尝试从其控制终端读取，它会被 `SIGTTIN` 信号挂起。

图 13.49 阐述了一个典型的设置。假设进程 145 和进程 230 是后台作业的进程组首，进程 171 是前台作业的进程组首。`setpgid()` 更改进程组，其工作方式如图 13.50 所示。进程可以通过 `getpid()` 获取其当前的进程组 ID，其工作方式如图 13.51 所示。

![](img/4245b8ee77539f33ff090ce0a0dd7eb6_532_0.png)

图 13.49

控制终端与进程组。

## 500 第 13 章 系统编程

系统调用：`pid_t setpgid (pid_t pid, pid_t pgrpid)` 如果 `pid` 为非零，`setpgid()` 将 PID 为 `pid` 的进程进程组 ID 设置为 `pgrpid`。如果 `pid` 为零，则将调用者的进程组 ID 设置为 `pgrpid`。为了让 `setpgid()` 成功并设置进程组 ID，必须满足以下条件之一：

- 调用者与指定的进程必须具有相同的所有者。

- 调用者必须由超级用户拥有。

当进程想要启动自己的特有进程组时，它通常会将自己的进程 ID 数字作为第二个参数传递给 `setpgid()`。如果 `setpgid()` 失败，它返回 -1。

图 13.50

`setpgid()` 系统调用的描述。

系统调用：`pid_t setpgid (pid_t pid)`

`getpgid()` 返回 PID 为 `pid` 的进程进程组 ID。如果 `pid` 为零，则返回调用者的进程组 ID。

图 13.51

`getpgid()` 系统调用的描述。

下一个示例说明了终端将信号分发给其控制进程进程进程组中的所有进程。由于子进程继承了父进程的进程组，父、子进程都可以捕获 `SIGINT` 信号。代码如下：

```c
$ cat pgrp.c ...list program
#include <signal.h>
#include <stdio.h>
void sigintHandler();
main()
{
    signal(SIGINT, sigintHandler); /* 处理 Control-C */
    if (fork () == 0)
        printf("Child PID %d PGRP %d waits\n", getpid(), getpgid(0));
    else
        printf("Parent PID %d PGRP %d waits\n", getpid(), getpgid(0));
    pause(); /* 等待信号 */
}
void sigintHandler() {
```

```c
(
printf("Process %d got a SIGINT\n",getpid());
)
$ pgrp1 ...run the program.
Parent PID 453 PGRP 453 waits
Child PID 454 PGRP 454 waits
      ...Control-C.
Process 454 got a SIGINT
Process 453 got a SIGINT
$ _
```

如果进程将自己放入不同的进程组，它不再与终端的控制进程关联，也不会接收来自终端的信号。在下面的示例中，子进程不受影响：

```c
$ cat pgrp2.c ...list the program.
#include <signal.h>
#include <stdio.h>
void sigintHandler();
main() {
    int i;
    signal(SIGINT, sigintHandler); /* 安装处理器 */
    if (fork () == 0) {
        setpgid(0, getpid()); /* 将子进程放入自己的进程组 */
        for (i = 1; i <= 3; i++) { /* 循环三次 */
            printf("Process %d is alive\n", getpid());
            sleep(1);
        }
    }
}
void sigintHandler() {
    printf("Process %d got a SIGINT\n",getpid());
    exit(1);
}
$ pgrp2 ...run the program.
Parent PID 453 PGRP 453 waits
Child PID 454 PGRP 454 waits
      ...Control-C.
Process 454 got a SIGINT
Process 453 got a SIGINT
$ _
```

管道（Pipes）是一种进程间通信机制，允许两个或多个进程相互发送信息。它们通常在 shell 内部用于将一个工具的标准输出连接到另一个工具的标准输入。重要的是，管道中的写入进程和读取进程是并发执行的；如果管道太满，管道会自动缓冲写入者的输出。同样，如果管道为空，读取进程将被挂起，直到更多输出可用。

所有版本的 UNIX 都支持管道，即 shell 使用的管道。例如，这里有一个确定系统上有多少用户的简单命令：

```bash
$ who | wc -1
```

`who` 工具为每个用户生成一行输出。该输出被“管道”到 `wc` 工具，后者在带有 `-1` 参数调用时会输出总行数。因此，管道命令通过计算 `who` 生成的行数巧妙地计算出用户总数。图 13.52 显示了管道图。

管道是一种单向通信链路，它会自动缓冲其输入（最大大小随 UNIX 版本而异，约为 5K），并可以使用 `pipe()` 系统调用创建。管道的每端都有一个关联的描述符。管道的“写入”端可以使用 `write()` 写入，“读取”端可以使用 `read()` 读取。当进程完成对管道文件描述符的操作后，应该使用 `close()` 将关闭。图 13.53 显示了 `pipe()` 如何工作。
