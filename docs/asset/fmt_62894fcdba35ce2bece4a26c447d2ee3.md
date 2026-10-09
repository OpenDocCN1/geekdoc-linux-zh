
同样，正如我们之前描述的，我们也可以将其封装在一个调用 `C shell` 的 `bash` 脚本中，但需要更多的开销。

如果我们有这三种 `shell` 且 `awk` 不使用 `#` 作为它们的注释字符，上述这些操作都将无法实现。

## 8.13. system 函数

从程序执行命令字符串是非常方便的。例如：

```
system("date > file");
```

`ISO C` 定义了该函数，但其操作很大程度上取决于系统。`POSIX` 定义了该函数，但其操作也很大程度上取决于系统。

```
#include <stdlib.h>
int system(const char *cmdstring);
```

返回值：（见下文）

如果 `cmdstring` 为空指针，只有当命令处理器可用时，`system` 返回非零。在 `UNIX` 下，`system` 总是用的。

- 1. 如果 `fork` 或 `waitpid` 返回非 `EINTR` 错误，`system` 返回 `errno`。
- 2. 如果 `exec` 失败，返回值为 127。
- 3. 否则，当 `fork`、`exec` 和 `wait` 函数均成功，返回 `shell` 的退出状态。

某些 `system` 的实现在 `waitpid` 被信号中断时会返回错误（`EINTR`）。`POSIX` 后来增加了在这种情况下 `system` 不返回错误。（我们在 10.5 节中讨论）。

### 图 8.22. 无信号处理的 system 函数

```
#include <sys/wait.h>
#include <errno.h>
#include <unistd.h>

int
system(const char *cmdstring) /* 无信号处理的版本 */
{
    pid_t pid;
    int status;

    if (cmdstring == NULL)
        return(1); /* 作为 UNIX 命令处理器 */

    if ((pid = fork()) == 0) {
        status = -1; /* 可能进程耗尽 */
    } else if (pid == 0) { /* 子进程 */
        execcl("/bin/sh", "sh", "-c", cmdstring, (char *)0);
        exit(127); /* exit 错误 */
    } else { /* 父进程 */
        while (waitpid(pid, &status, 0) < 0) {
            if (errno == EINTR) /* waitpid 非 EINTR 错误 */
                break;
        }
    }

    return(status);
}
```

### 图 8.23. 调用 system 函数

```
#include "apue.h"
#include <sys/wait.h>

int
main(void)
{
    int status;
    if ((status = system("date")) < 0) {
        err_sys(system("error"));
        pr_exit(status);
    }
    if ((status = system("nosuchcommand")) < 0) {
        err_sys(system("error"));
        pr_exit(status);
    }
    if ((status = system("who: exit 44")) < 0) {
        err_sys(system("error"));
        pr_exit(status);
    }
    exit(0);
}
```

运行图 8.23 中的程序将我们得到：

```
$ /a.out
Sun Mar 21 18:41:32 2004
normal termination, exit status = 0 for date
sh: nosuchcommand: command not found
normal termination, exit status = 127 for nosuchcommand
sar 0 Mar 18 19:45
sar pts/0 Mar 18 19:45 (0)
sar pts/1 Mar 18 19:45 (0)
sar pts/2 Mar 18 19:45 (0)
sar pts/3 Mar 18 19:45 (0)
normal termination, exit status = 44 for exit
```

使用 `system` 而不是直接使用 `fork` 和 `exec` 的优点是它包含了所有所需的错误处理和（在本文 10.18 节的下一个版本中）所有所需的信号处理程序。

早期系统（使用 `SVR3.2` 和 `4BSD`）没有 `waitpid` 函数。相反，父进程使用如下语句等待子进程：

```c
while ((waitpid = wait(&status)) != 0 && waitpid != -1)
;
```

如果子系统在调用 `system` 之前生成了自己的子进程，就会出现问题。因为 `while` 循环会一直运行直到 `system` 生成的子进程终止，如果任何子进程在 `pid` 标识的进程之前终止，这些其他子进程的进程 ID 和状态将被 `while` 语句丢弃。事实上，这种无法等待特定子进程的能力正是 `POSIX.1` 包含 `waitpid` 函数的原因之一。我们将在 15.3 节中看到，如果系统不提供 `waitpid` 函数，`open` 和 `close` 函数也会出现同样的问题。

## Set-User-ID 程序

如果从用户-ID 程序中调用 `system` 会发生什么？这样做是一个安全漏洞，绝对不应该这样做。图 8.24 显示了一个简单的程序，它仅对其命令行参数调用 `system`。

### 图 8.24. 使用 system 执行命令行参数

```c
#include "apue.h"

int
main(int argc, char *argv[])
{
    int status;

    if (argc < 2)
        err_quit("command-line argument required");

    if ((status = system(argv[1])) < 0)
        err_sys("system() error");
    pr_exit(status);

    exit(0);
}
```

我们将此程序编译为可执行文件 `tsys`。

图 8.25 显示了另一个简单的程序，它打印它的真实用户 ID 和有效用户 ID。

### 图 8.25. 打印真实和有效用户 ID

```c
#include "apue.h"

int
main(void)
{
    printf("real uid = %d, effective uid = %d\n", getuid(), geteuid());
    exit(0);
}
```

我们将此程序编译为可执行文件 `printuids`。运行这两个程序将得到如下：

- `$ tsu printuids normal execution, no special privileges`
  - `real uid = 205, effective uid = 205`
  - `normal termination, exit status = 0`

- `$ su become superuser`
  - `Password: enter superuser password`

`chown root tsys change owner`
`chmod u+s tsys set-user-ID`
`ls -tsys verify file's permissions and owner`

我们赋予 `tsys` 程序的超级用户权限在 `system` 执行的 `fork-exec` 过程中被保留了。

当 `/bin/sh` 是 `bash` 版本 2 时，之前的示例不起作用，因为当有效用户 ID 与真实用户 ID 不匹配时，`bash` 会将有效用户 ID 重置为真实用户 ID。

如果以具有特殊权限的 `set-user-ID` 或 `set-group-ID` 运行并产生另一个进程，应该直接使用 `fork-exec`，并确保在 `fork-exec` 之后恢复普通权限。永远不应在 `set-user-ID` 或 `set-group-ID` 程序中使用 `system` 函数。

这种承认的原因之一是 `system` 调用 `shell` 来解析命令字符串，而 `shell` 使用 `IFS` 变量作为输入字段分隔符。旧版本的 `shell` 不会将该变量重置为正常的字符集。这允许恶意用户在调用 `system` 之前设置 `IFS`，导致 `system` 执行不同的程序。

![](img/902515e97eef28cac8083866e00a6f4c_371_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_371_1.png)

## 8.14. 进程会计

大多数 `UNIX` 系统都提供进程会计选项。启用时，内核会在每个进程终止时写入一条会计记录。这些会计记录通常是少量的二进制数据，带有命令名称、使用的 `CPU` 时间、用户 ID 和组、开始时间等。我们将在本节中详细查看会计记录，因为它提供了跟踪进程的机会。

进程会计未由标准规定。因此，所有实现之间存在令人讨厌的差异。例如，`Solaris` 的 `I/O` 计数以字节为单位，而 `Linux 2.4` 则不维护 `I/O` 统计。

`acct` 函数启用和禁用进程会计。超级用户执行 `acct` 并带有参数启用会计。会计记录写入指定的文件，在 `Solaris` 上为 `/var/account/acct`。

会计记录的结构定义在 `<sys/acct.h>` 中，如下：

```c
struct {
    u_short flag;    /* 16位 */
    time_t time;    /* 用户时间 */
    time_t stime;   /* 系统时间 */
    time_t etime;   /* 经过时间 */
    int mem;         /* 内存使用 */
    int io;          /* 传输的块 */
    int rw;          /* 写入的块 */
    uid_t uid;      /* 真实用户 ID */
    gid_t gid;      /* 真实组 ID */
    dev_t tty;      /* 控制终端 */
    char comm[32];  /* 命令名称 */
};
```

`ac_flag` 成员记录了执行期间的某些事件。这些事件见图 8.26。

| ac_flag | 描述 | FreeBSD | OS X | Solaris |
| :--- | :--- | :--- | :--- | :--- |
| `AFORK` | 进程是 `fork` 的结果 | | 10.3 | 8 |
| `ASU` | 使用超级权限 | | | |
| `ACOMPAT` | 使用兼容模式 | | | |
| `ACORE` | 转储核心 | | | |
| `AXSIG` | 进程被信号杀死 | | | |
| `AEXPND` | 扩展条目 | | | |

会计记录对应于进程，而不是程序。在执行新程序后，内核为子进程初始化一个新的记录。`exec` 不会创建新的会计记录，命令名称会改变，然后 `AFORK` 标志被清除。这意味着如果我们有一系列进程 `A exec`，然后 `B exec`，最后 `C` 退出，只写入一条记录。命令名称对应于程序 `C`，但 `CPU` 时间是程序 `A`、`B` 和 `C` 的示例。

### 示例

为了有可以检查的会计数据，我们将创建一个测试程序来实现图 8.27 中的图。测试程序的源码见图 8.28。每个子进程 `fork` 四次。每个子进程都执行不同的事情并终止。

符号本身，因为在 `Linux` 上，它们被定义为枚举（`enum`），我们无法在 `field` 表达式中使用它们。

为了进行测试，我们执行了以下操作：

1. 变为超级用户并启用账户，请注意，当此命令结束时，它应该是开启的；因此，应该在会计文件中找到第一条记录。
2. 退出超级用户 `shell` 并运行图 8.28 所示的程序。这应该向会计文件中添加记录：一个属于超级用户 `shell` 的，一个属于父进程的，以及四个子进程各一个。第二个子进程没有创建新进程。第二个子进程只有一个会计记录。
3. 变为超级用户并关闭。如果 `accton` 命令结束时会计功能是关闭的，那么它将不应该出现在会计文件中。
4. 运行图 8.29 的程序来打印会计文件中的选定字段。

步骤 4 的输出如下。在随后的讨论中，我们为每行输出添加了*斜体*格式的进程描述。

```
accton e = 6, chars = stat = 0: S
sh e = 2106; stat = 15632; stat = 0: S
ddd e = 8, chars = 273344; stat = 0:
aout e = 202, chars = 921; stat = 0: second child
out e = 407, stat = 0; stat = 134: F parent
aout e = 600, stat = 0; stat = 9: F first child
aout e = 801, stat = 0; stat = F fourth child third child
```

经过的时间用*斜体*表示，它是进程的状态，但它对应于我们在第 8.6 节中讨论的进程终止状态。会计文件中唯一的信息是核心转储标志位（`core-flag bit`，通常是高位）和信号量（通常是低 7 个位）。对于第一个子进程，该值为 `128+6`。`128` 是核心转储标志位，而 `6` 恰好是进程中 `sleep(2)` 的值，对应于经过的时间。对于第一个子进程，`sleep(4)` 变成了 `407` 刻。进程睡眠的时间不是精确的。（我们将在第 10 章重新回到 `sleep` 函数）。此外，`fork` 和 `exit` 也需要一些时间。

注意，`stat` 成员并不是进程的真实状态，而是对应于我们讨论的进程终止状态。如果进程异常终止，我们无法从会计文件中看到退出信息。对于第一个子进程，该值为 `128+6`。`128` 是核心转储标志位，而 `6` 恰好是进程中 `sleep(2)` 的值，对应于经过的时间。对于第一个子进程，`sleep(4)` 变成了 `407` 刻。进程睡眠的时间不是精确的。（我们将在第 10 章重新回到 `sleep` 函数）。此外，`fork` 和 `exit` 也需要一些时间。

第二个子进程中 `dd` 进程复制的文件大小为 `136633` 字节。`I/O` 次数是它的两倍多。值也是两倍，因为读取了 `136633` 字节，但也写出了 `136633` 字节。即使输出的是空字节，也会存储在文件中。

`stat` 标志值如我们预期设置。除了第二个子进程外，所有进程都设置了 `F` 标志。父进程没有设置 `F` 标志，因为执行父进程的会计进程执行了 `fork`，然后 `exec` 执行一个输出文件。第一个子进程调用了 `abort`，它产生 `SIGABRT` 来生成核心转储。`kFlag` 标志或 `D` 标志都没有开启，因为 `Solaris` 不支持它们；它们代表的信息可以从 `ac_stat` 字段推导出来。第四个子进程因为信号而终止，`SIGKILL` 信号不会产生核心转储；它只会终止进程。

最后说明一点，第一个子进程的 `I/O` 字符数为 0，该进程生成了一个核心文件。这似乎写入核心文件所需的 `I/O` 并没有计入在进程进程中。

### 图 8.27. 会计示例的进程结构

[查看全图]

![](img/902515e97eef28cac8083866e00a6f4c_376_0.png)

### 图 8.28. 生成会计数据的程序

```
#include "apue.h"

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) { /* 父进程 */
        sleep(2);
        exit(2); /* 用退出状态 2 终止 * */
    }

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {
        sleep(4);
        abort(2); /* 产生核心转储终止 * */
    }

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {
        execcl("/bin/dd", "dd", "-f=/etc/termcap", "-of=/dev/null", NULL); /* 不应该到这里 * */
    }

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid != 0) {
        /* 第一个子进程 */
    }
```

此处在原文中：
