
```c
pid_t childpid;
pid_t pgid;

childpid = fork();
if (childpid < 0) {
    perror("fork");
} else if (childpid == 0) {
    /* 子进程 */
    if (setpgid(0, pgid) == -1 && errno != EACCES) {
        perror("setpgid");
    }
    execve(...);
} else {
    /* 父进程 */
    if (setpgid(childpid, pgid) == -1) {
        perror("setpgid");
    }
    // 等待子进程...
}
```

在某些 UNIX 实现中（例如 HP-11），只有当进程与调用进程处于同一个会话时，`getsid()` 才能用于检索该进程的会话 ID（session ID）（`SUSv3` 允许这种可能性）。换句话说，该调用仅通过其成功或失败（返回 `EPERM`）来告知我们指定的进程是否与调用者处于同一个会话中。这种限制在 `Linux` 或大多数实现中并不存在。

如果调用进程不是组组，`setsid()` 将创建一个新的会话。

```c
#include <unistd.h>

pid_t setsid(void);
```

返回新会话的会话 ID，或出错时返回 `(pid_t) ~1`

`setsid()` 系统调用按照所示创建一个新会话：

- 调用进程成为新会话的引导，并成为该会话内一个新进程组的引导。调用进程的组 ID（`GID`）和会话 ID（`SID`）设置为与其进程 ID（`PID`）相同的值。
- 调用进程没有控制终端。任何之前存在的控制终端的连接都会断开。

如果调用进程是组长，`setsid()` 将因错误 `EPERM` 失败。确保这种情况不发生的最简单方法是执行 `fork()` 并让父进程退出，而子进程继续调用 `setsid()`。由于子进程继承了父进程的组 ID 并接收了自己的进程 ID，因此它可以成为一个进程引导。

禁止组长调用 `setsid()` 的限制是必要的。如果没有这个限制，进程引导将能够自己置于另一个（新的）会话中，而进程组的其他成员仍留在原始会话中。（由于不会创建新的进程组，因为根据定义，进程引导的进程组 ID 已经与其进程 ID 相同。）这将违反了会话和进程组之间严格的二层层级结构，即进程组的成员必须属于同一个会话。

当通过 `fork()` 创建新进程时，内核不仅确保它具有唯一的进程 ID，还确保该进程 ID 不与任何现有进程的进程组 ID 或会话 ID 匹配。然而，即使进程组或会话的引导已经退出，新进程也不能重用引导的进程 ID 并意外地成为现有会话或进程的引导。

列表 34-2 展示了使用 `setsid()` 创建新会话的用法。为了检查它是否不再拥有控制终端，该程序尝试打开特殊文件 `/dev/tty`（在下一节中）。当我们运行此程序时，看到以下内容：

```
$ ps -p $$ -o pgid=sid,command # $$ 是 shell 的 PID
PID PGID SID COMMAND
12243 12243 bash             PID, PGID, and SID of shell
 ./setsid
$ PID=12352, PGID=12352, SID=12352
ERROR [ENXIO Device not configured] /dev/tty
```

* 进程组、会话与作业控制 705

从输出可以看出，进程成功地将自己置于新会话中的新进程组中。由于该会话没有控制终端，`open()` 调用失败。（在上述程序输出的倒数第二行，我们看到 shell 提示符与程序输出混合在一起，因为 shell 注意到进程在 `fork()` 调用后已退出，因此打印子进程下一个提示符已完成。）

## 34-2: 创建新会话

```c
#define XOPEN_SOURCE 500
#include <unistd.h>
#include <fcntl.h>
#include "tlpi_hdr.h"

int
main(int argc, char *argv[])
{
    if (fork() != 0) /* 退出父进程，或出错 */
        exit(EXIT_SUCCESS);

    if (setsid() == -1)
        errxit("setid");

    printf("PID=%ld, PGID=%ld, SID=%ld\n", (long) getpid(),
        (long) getppid(), (long) getsid(0));

    if (open("/dev/tty", O_RDWR) == -1)
        errxit("open /dev/tty");
    exit(EXIT_SUCCESS);
}
```

`pgsjc/t_tetsid.c`

## 34.4 控制终端与控制进程

会话中的所有进程可能拥有（唯一的）控制终端。在创建时，会话没有控制终端；当会话引导首次打开一个并非该会话控制终端的终端时，控制控制终端，除非在调用 `open()` 时指定了 `O_NOCTTY`。`SUSv3` 规定了函数 `getsid(int fd)`（原型在 `<termios.h>` 中），它返回与控制终端关联的会话 ID。该函数在 `glibc` 中提供（其中使用 `ioctl(fd, TIOCSGID)` 实现）。控制终端由 `fork()` 的子进程继承并在跨 `exec()` 期间保留。如果发生终端断开，内核会向控制进程发送一个 `SIGHUP` 信号以通知它。我们将在第 34.6 节中详细讨论这一点。

如果进程有一个控制终端，打开特殊文件 `/dev/tty` 即可获得该终端的文件描述符。如果标准输入和输出被重定向，且程序希望确保自己正在与控制终端通信，这将非常有用。例如，第 8.5 节描述的 `open()` 函数就为此目的打开了 `/dev/tty`。如果进程没有控制终端，`/dev/tty` 将因错误 `ENXIO` 失败。

## 移除进程与终端的关联

使用 `ioctl(fd, TIOCNOTTY)` 操作可以移除进程与控制终端的关联。如果进程有一个控制终端，打开 `/dev/tty` 即可获得该终端的文件描述符。如果标准输入和输出被重定向，且程序希望确保自己正在与控制终端通信，这将非常有用。例如，第 8.5 节描述的 `open()` 函数就为此目的打开了 `/dev/tty`。如果进程没有控制终端，`/dev/tty` 将因错误 `ENXIO` 失败。

如果调用进程是组长，`setsid()` 将因错误 `EPERM` 失败。确保这种情况不发生的最简单方法是执行 `fork()` 并让父进程退出，而子进程继续调用 `setsid()`。由于子进程继承了父进程的组 ID 并接收了自己的进程 ID，因此它可以成为一个进程引导。

禁止组长调用 `setsid()` 的限制是必要的。如果没有这个限制，进程引导将能够自己置于另一个（新的）会话中，而进程组的其他成员仍留在原始会话中。（由于不会创建新的进程组，因为根据定义，进程引导的进程组 ID 已经与其进程 ID 相同。）这将违反了会话和进程组之间严格的二层层级结构，即进程组的成员必须属于同一个会话。

当通过 `fork()` 创建新进程时，内核不仅确保它具有唯一的进程 ID，还确保该进程 ID 不与任何现有进程的进程组 ID 或会话 ID 匹配。然而，即使进程组或会话的引导已经退出，新进程也不能重用引导的进程 ID 并意外地成为现有会话或进程的引导。

列表 34-2 展示了使用 `setsid()` 创建新会话的用法。为了检查它是否不再拥有控制终端，该程序尝试打开特殊文件 `/dev/tty`（在下一节中）。当我们运行此程序时，看到以下内容：

```
$ ps -p $$ -o pgid=sid,command # $$ 是 shell 的 PID
PID PGID SID COMMAND
12243 12243 bash             PID, PGID, and SID of shell
 ./setsid
$ PID=12352, PGID=12352, SID=12352
ERROR [ENXIO Device not configured] /dev/tty
```

* 进程组、会话与作业控制 705

从输出可以看出，进程成功地将自己置于新会话中的新进程组中。由于该会话没有控制终端，`open()` 调用失败。（在上述程序输出的倒数第二行，我们看到 shell 提示符与程序输出混合在一起，因为 shell 注意到进程在 `fork()` 调用后已退出，因此打印子进程下一个提示符已完成。）

## 34-2: 创建新会话
