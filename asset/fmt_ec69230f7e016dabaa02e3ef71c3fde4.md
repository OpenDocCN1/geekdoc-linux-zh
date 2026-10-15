
- 1. 变为超级用户并启用账户，请注意当此命令结束时，它应该是开启的；因此，应该在会计文件中找到第一条记录。
- 2. 退出超级用户 `shell` 并运行图 8.28 所示的程序。这应该向会计文件中添加记录：一个属于超级用户 `shell` 的，一个属于父进程的，以及四个子进程各一个。
- 3. 变为超级用户并关闭。如果 `accton` 命令结束时会计功能是关闭的，那么它将不应该出现在会计文件中。
- 4. 运行图 8.29 的程序来打印会计文件中的选定字段。

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

经过的时间用*斜体*表示，它是进程的状态，但它对应于我们在第 8.6 节中讨论的进程终止状态。会计文件中唯一的信息是核心转储标志位（core-flag bit，通常是高位）和信号量（通常是低 7 个位）。对于第一个子进程，该值为 `128+6`。`128` 是核心转储标志位，而 `6` 恰好是进程中 `sleep(2)` 的值，对应于经过的时间。对于第一个子进程，`sleep(4)` 变成了 `407` 刻。进程睡眠的时间不是精确的。（我们将在第 10 章重新回到 `sleep` 函数）。此外，`fork` 和 `exit` 也需要一些时间。

注意，`stat` 成员并不是进程的真实状态，而是对应于我们讨论的进程终止状态。如果进程异常终止，我们无法从会计文件中看到退出信息。对于第一个子进程，该值为 `128+6`。`128` 是核心转储标志位，而 `6` 恰好是进程中 `sleep(2)` 的值，对应于经过的时间。对于第一个子进程，`sleep(4)` 变成了 `407` 刻。进程睡眠的时间不是精确的。（我们将在第 10 章重新回到 `sleep` 函数）。此外，`fork` 和 `exit` 也需要一些时间。

第二个子进程中 `dd` 进程复制的文件大小为 `136633` 字节。I/O 次数是它的两倍多。值也是两倍，因为读取了 `136633` 字节，但也写出了 `136633` 字节。即使输出的是空字节，也会存储在文件中。

`stat` 标志值如我们预期设置。除了第二个子进程外，所有进程都设置了 `F` 标志。父进程没有设置 `F` 标志，因为执行父进程的会计进程执行了 `fork`，然后 `exec` 执行一个输出文件。第一个子进程调用了 `abort`，它产生 `SIGABRT` 来生成核心转储。`kFlag` 标志或 `D` 标志都没有开启，因为 Solaris 不支持它们；它们代表的信息可以从 `ac_stat` 字段推导出来。第四个子进程因为信号而终止，`SIGKILL` 信号不会产生核心转储；它只会终止进程。

最后说明一点，第一个子进程的 I/O 字符数为 `0`，该进程生成了一个核心文件。这似乎写入核心文件所需的 I/O 并没有计入在进程中。

## 图 8.27. 会计示例的进程结构

[查看全图]

![](img/902515e97eef28cac8083866e00a6f4c_376_0.png)

## 图 8.28. 生成会计数据的程序

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
```

## 8.16. 进程时间

在第 1.10 节中，我们描述了三种可以测量的时间：挂钟时间（wall clock time）、用户 CPU 时间和系统 CPU 时间。任何进程都可以调用 `times` 函数来获取自身以及任何已终止子进程的数值。

```c
#include <sys/times.h>
clock_t times(struct timesval *buf);
```

返回：如果成功，返回以答（ticks）为单位的已挂钟时间；出错则返回 `1`

该函数填充由 `buf` 指向 `times` 结构体：

```c
struct tms {
clock_t t_utime; /* 用户 CPU 时间 */
clock_t t_stime; /* 系统 CPU 时间 */
clock_t t_cutime; /* 子进程的用户 CPU 时间 */
clock_t t_cime; /* 子进程的系统 CPU 时间 */
};
```

注意，该结构体并不包含任何挂钟时间的测量值。相反，该值是从过去的某个任意点开始测量的，因此我们不能取其绝对值；而是使用它的相对值。例如，我们调用 `times` 并返回相同的值。在稍后，我们再次调用 `times` 并从新值中减去早的值。差值即为挂钟时间。虽然可能，但长时间运行的进程可能会导致挂钟时间溢出；练习 1.6。

用于子进程的两个字段仅包含已通过 `wait`、`wait4` 或 `waitpid` 等待的子进程的值。

此函数返回的所有 `clock_t` 值都通过 `sysconf()` 返回的每秒时钟频率 `SC_CLK_TCK`（第 2.5.4 节）转换为秒。

大多数实现提供了 `getrusage()` 函数。该函数返回 CPU 时间和 14 个其他资源使用值。从历史上看，它源于 BSD 操作系统，因此 BSD 衍生实现通常比实现支持更多字段。

### 示例

图 8.30 中的程序将每个命令行参数作为 shell 命令字符串执行，修剪命令并打印来自 `tms` 结构体的值。

如果我们运行这个程序，将得到：

### `/a.out "sleep 5" "date"`

```
command: sleep 5
real: 5.02
user: 0.00
sys: 0.00
child user: 0.01
child sys: 0.00
normal termination, exit status = 0

command: date
Mon Mar 22 00:43:58 EST 2004
real: 0.01
user: 0.00
sys: 0.00
child user: 0.01
child sys: 0.00
normal termination, exit status = 0
```

在这两个示例中，所有的 CPU 时间都出现在子进程中，这正是 shell 和命令执行的地方。

### 图 8.30. 时间并执行所有命令行参数

```c
#include "apue.h"
#include <sys/times.h>
```

```c
static void pr_times(clock_t t, struct tms *, struct tms *);
static void do_cmd(char *);
```

```c
int
main(int argc, char *argv[])
{
	int i;
	setbuf(stdout, NULL);
	for (i = 1; i < argc; i++)
		do_cmd(argv[i]); /* 每个命令行参数执行一次 */

	exit(0);
}
```

```c
static void
do_cmd(char *cmd)
{
	/* 执行并计时 "cmd" */
	struct tms tmsstart, tmsend;
	clock_t start, end;
	int status;

	printf("incommand: %s\n", cmd);

	if ((start = times(&tmsstart)) == -1) /* 获取起始值 */
		err_sys("time error");

	if ((status = system(cmd)) < 0) /* 执行命令 */
		err_sys("system error");

	if ((end = times(&tmsend)) == -1) /* 获取结束值 */
		err_sys("time error");

	pr_times(end-start, &tmsstart, &tmsend);
	pr_exit(status);
}

static void
pr_times(long long clock_real, struct tms *tmsstart, struct tms *tmsend)
{
    static long clck = 0;
    if (clck == 0) /* 第一次获取每秒时钟频率 */
        if ((clck = sysconf(SC_CLK_TCK) < 0)
            err_sys("sysconf error");
    printf("real: %.2fn\n", clock_real / (double) clck);
    printf("user: %.2fn\n", (tmsend->t_utime - tmsstart->t_utime) / (double) clck);
    printf("sys: %.2fn\n", (tmsend->t_stime - tmsstart->t_stime) / (double) clck);
    printf("child user: %.2fn\n", (tmsend->t_cutime - tmsstart->t_cutime) / (double) clck);
    printf("child sys: %.2fn\n", (tmsend->t_cime - tmsstart->t_cime) / (double) clck);
}
```

## 8.17. 总结

深入理解进程关系对于高级编程至关重要。原语 `wait`、`wait4` 和 `waitpid` 用于等待子进程。用于子进程的两个字段仅包含已等待的子进程的值。`times` 返回的所有 `clock_t` 值都通过 `SC_CLK_TCK` 转换为秒。大多数实现提供了 `getrusage()`，它返回 CPU 时间和 14 个其他资源使用值。BSD 衍生实现通常比其他实现支持更多字段。

## 9.2. 终端登录

让我们先来看下登录 UNIX 系统时执行的程序。在早期的 UNIX 系统中（例如第 7 版），用户登录到连接在硬线连接上的盲终端（dumb terminals）。这些终端是局部的（直接连接）或远程的（通过介质连接）。无论何种情况，这些登录都是通过内核中的终端驱动程序程序完成的。例如，PDP-11 上常见的设备是 DH-11s 和 DZ-11s。主机有固定数量的此类终端设备，同时登录人数没有上限限制。

随着位图图形终端的出现，窗口系统也应运而生，为用户提供了与主机计算机交互的新方式。为了创建“终端窗口”而开发的应用程序模拟了基于字符的终端，允许用户以熟悉的方式（即通过命令行）与主机进行交互。

如今，某些平台允许你在登录后启动窗口系统，而另一些平台则会自动为你启动窗口系统。在后一种情况下，取决于窗口系统的配置，你可能仍需要登录（某些窗口系统可以配置为自动登录）。

我们现在描述的程序是使用终端登录 UNIX 系统的方法。无论我们使用哪种类型的终端（可以是基于字符的终端、模拟简单字符终端的图形终端，或者是运行窗口系统的图形终端），该过程都是相似的。

### BSD 终端登录

这个过程在过去的 30 年里没有太大变化。系统管理员创建一个文件（通常为 `/etc/tty`），每个终端设备占一行。每行指定了设备名称以及传递给 `getty` 的其他参数。例如，一个参数是终端的波特率。当系统启动时，内核创建进程 ID 为 `1` 的进程——`init` 进程，由 `init` 多用户系统。`init` 进程读取 `/etc/tty` 文件，并对每个允许登录的终端设备在 `getty` 中执行 `fork` 后执行 `exec`。该过程如图 9.1 所示。

> 图 9.1. init 调用的用于允许终端登录的进程

![](img/902515e97eef28cac8083866e00a6f4c_388_0.png)

图 9.1 中所示的所有 `getty` 进程的真实用户 ID 均为 `0`，有效用户 ID 均为 `0`（即它们都具有超级用户权限）。`init` 进程在空环境中执行 `exec getty` 程序。

是 `getty` 调用了 `open` 来打开终端。终端以读写模式打开。如果该设备是调制调器，`open` 可能会阻塞设备驱动程序，直到调制调器拨号接接。一旦设备打开，文件描述符 `0`、`1` 和 `2` 就会指向该设备。然后 `getty` 输出类似 `login:` 的内容，并等待我们输入用户名。如果终端支持多种速度，`getty` 可以检测特殊字符来更改终端速度（波特率）。请参阅你的 UNIX 手册获取有关 `getty` 程序和 `gettytab` 数据文件可以引用的更多细节。

当我们输入名称后，`getty` 的任务就完成了，它调用 `login` 程序，类似于 `execle("/bin/login", "login", "-p", username, (char *)j0, env))`。

（`gettytab` 中可以有调用其他进程的选项，但默认是 `login` 程序。） `init` 在空环境下执行 `getty`；`getty` 为 `login` 的 `env` 参数创建一个环境，包含终端名称（如 `TERM-foo`，其中终端类型 `foo` 来自 `gettytab` 文件）以及 `gettytab` 中指定的任何环境变量字符串。`-p` 标志告诉 `login` 保留传递给它的环境变量并在此添加，而不是替换。图 9.2 显示了在调用 `login` 后这些进程的状态。

### 图 9.2. 调用 login 后的进程状态

![](img/902515e97eef28cac8083866e00a6f4c_389_0.png)

![](img/902515e97eef28cac8083866e00a6f4c_389_1.png)

图 9.2 中所示的所有进程具有超级权限，原始进程也具有超级权限。图 9.2 中三个进程的 ID 相同，进程 ID 在它们之间没有改变。此外，除了原始 `init` 进程外，其他进程的父均为 `1`。

`login` 程序执行很多操作。在我们的案例中，我们可以使用 `getpwnam` 获取密码；读取我们的密码（带加密，已禁用）。或者调用 `crypt` 对我们输入的 `getpass` 密码进行加密，并将结果复制到影子密码文件的 `pw_passwd` 字段中。如果密码无效导致登录失败（多次后），`login` 将带参数 `1` 调用 `exit`。这会被父进程（`init`）注意到，随后它会在 `exec getty` 后再次 `fork`，从而为该终端重新启动程序。

这是 UNIX 系统上传统的认证方式。现代系统如 FreeBSD、Linux、macOS 和 X 也支持一种更灵活的方案，称为 PAM（可插拔认证模块）。PAM 允许管理员为编写使用 PAM 库的服务配置认证方法。

如果我们的需求是验证用户是否具有相应权限，我们可以硬编码，也可以使用 PAM 库。PAM 的优势是管理员可以为不同的用户配置不同的认证方式。

- 切换到我们的主目录 (`chdir`)
- 更改终端设备的权限 (`chown`)
- 设置组 ID (`setgid`)
