

`EC_CLEANUP_BGN`
    return false;
`EC_CLEANUP_END`
}

同样，`pt_open_slave` 必须在子进程中调用，而不是在父进程中。（我们很快就会看到一个示例。）对于定义了 `NEED_STREAM_SETUP` 的系统，例如 Solaris，需要向流推入两个模块：`ptem`（伪终端仿真器）和 `ldterm`（常规终端模块）。¹¹（`ioctl` 系统调用和 `I_PUSH` 命令是标准化的，但用于设置 pty 的模块名称不是标准化的。）

在 `pt_open_slave` 的末尾，我们更改 pty 的模式，因为在某些系统上它可能没有合适的权限。然而，由于它可能不属于该进程的用户 ID（这取决于系统），`fchmod` 调用（第 3.7.1 节）可能会失败，在这种情况下，我们仍然会继续执行，寄希望于最好的结果。

步骤 7、8 和 9 不是通过 pt 库完成的，而是通过第 5 章和第 6 章中介绍的系统调用完成的。不过，我将在本节稍后出现的示例中展示代码。

由于子进程（从端）和父进程（主端）是独立运行的，父进程必须确保子进程完全设置好之后，才开始在第 9 步中读取和写入 pty。因此，pt 库提供了一个供父进程使用的调用，该调用在可以安全继续之前不会返回：

```c
bool pt_wait_master (PTINFO *p)
{
    fd_set fd_set_write;

    FD_ZERO(&fd_set_write);
    FD_SET(PT_GET_MASTER_PD(p), &fd_set_write);
    ec_negl( select(PT_GET_MASTER_PD(p) + 1, NULL, &fd_set_write, NULL,
        NULL) )
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

> 11. 要在 Solaris 系统（以及可能其他实现 STREAMS 的系统）上阅读关于这些的内容，请运行 `man ptem` 和 `man ldterm`。

我们只是使用 select（第 4.2.3 节）等待直到 pt 可写。下一个函数是 **pt\_close\_master**，在父进程中调用以在不再需要 pt 时关闭文件描述符并释放 PTINFO 结构体。

```c
bool pt_close_master(PTINFO *p)
{
	ec_neg1( close(p->pt_fd_m) )
	free(p);
	return true;

EC_CLEANUP_BGN
	return false;
EC_CLEANUP_END
}
```

还有一个 **pt\_close\_slave**，但通常不会调用它，因为在步骤 8 中，子进程会被另一个程序覆盖。此外，由于我们重定向了文件描述符，此时 pt 的子进程端由标准文件描述符（0、1 和 2）表示，而这些标准文件描述符在进程终止时几乎总是会自动关闭。以下是它的代码：

```c
bool pt_close_slave(PTINFO *p)
{
	(void)close(p->pt_fd_s); /* 可能已经关闭 */
	free(p);
	return true;
}
```

如果你发现自己在代码中调用了 **pt\_close\_slave**，那你很可能做错了什么。

请注意，**pt\_close\_master** 和 **pt\_close\_slave** 都释放了 PTINFO 结构体。这是应该的，因为当它们执行时，该结构体在父进程和子进程中都被分配了。当第 5.5 节解释 *fork* 时，这一点会更清楚。

综合所有内容，以下是使用 pt 库调用的一般框架：

```c
PTINFO *p = NULL;
bool ok = false;
	ec_null( p = pt_open_master() ) /* 步骤 1、2 和 3 */
switch (fork()) { /* 步骤 4 */
case 0:
	ec_false( pt_open_slave(p) ) /* 步骤 5 和 6 */

/*
	重定向文件描述符并 exec（未显示） - 步骤 7 和 8
*/
	break;
case -1:
    EC_FAIL
}
ec_false( pt_wait_master(p) )  /* 在步骤 9 之前同步 */

/* 父进程（主端）现在按需要读取和写入 pty - 步骤 9 */
ok = true;
EC_CLEANUP

EC_CLEANUP_BGN
if (p != NULL)
    (void)pt_close_master(p);
    /* 其他清理工作放在这里 */
exit(ok ? EXIT_SUCCESS : EXIT_FAILURE);
EC_CLEANUP_END
```

这就是我即将介绍的应用程序的样子。

### 4.10.2 录制和播放示例

我将使用 pty 来构建一个录制/播放系统，该系统可以录制命令的输出，然后像命令正在运行一样回放录制的输出。这意味着不仅屏幕必须与原始显示完全相同，而且回放速度也必须相同。为了了解我的意思，这里有一个脚本，它显示时间，等待 5 秒，然后再次显示时间：

```bash
$ cat >script1
date
sleep 5
date
$ chmod +x script1
$ script1
Wed Nov  6 10:46:31 MST 2002 [5秒暂停]
Wed Nov  6 10:46:36 MST 2002
```

当然，正如你从时间中看到的，第一次和第二次执行 date 命令之间有一个 5 秒的暂停。（括号中的注释不是输出的一部分。）

但是，如果我们只是在文件中捕获输出并显示该文件，文件中的文本会非常快地显示。没错，文件中的时间确实是 date 命令写入的内容，但当 cat 命令打印输出时没有暂停：

```bash
$ script1 >tmp
$ cat tmp
Wed Nov 6 10:55:24 MST 2002   /* 无暂停 */
Wed Nov 6 10:55:29 MST 2002
```

然而，这不是我们想要的。我们想要以与录制相同的速度回放输出，这通过我们稍后展示的一个名为 `record` 的命令来实现（其 `-p` 选项会回放录制内容）：

```bash
$ record script1
Wed Nov 6 10:57:18 MST 2002   /* 5秒暂停 */
Wed Nov 6 10:57:23 MST 2002
$ record -p
Wed Nov 6 10:57:18 MST 2002   /* 5秒暂停 */
Wed Nov 6 10:57:23 MST 2002
```

你在页面上看不到，但在显示第一行后，在显示第二行之前有一个 5 秒的暂停，这与输出录制时的速度相同。

因此，至少 `record` 需要保存 `事件`（events）：时间以及字符，以便回放部分知道以多快的速度将它们写入标准输出。我们希望它与交互式程序一起工作，所以它不能仅用管道捕获输出——它必须使用 pty 设置命令，因为像 `vi`、`emacs` 和其他全屏应用程序等有趣的命令只能在终端上工作。录波器、录制内容和被录制的命令是如何连接的，如图 4.7 所示。`record` 从标准输入读取的内容写入 pty，而从 pty 读取的内容既写入其标准输出 `and` 也写入 `事件` 文件。

首先，我将展示用于将命令的输出记录为一系列 `事件` 的数据结构和函数。然后，我将展示 `读取`

![](img/41b4c8f6d6a5c349eee321a301703d97_282_0.png)

图 4.7 与 `script1` 的录制交互。

事件并在适当的时间显示其中数据的播放函数。播放不涉及 pty，因为命令实际上并未运行。最后，我将展示录波器，它遵循我在上一节中展示的使用 pt 库的框架。

每次被录制的进程写入一些数据时，pty 的主端都会读取它并将其视为一个事件。它将自录制开始以来的相对时间和数据长度存储在一个 *事件*（event）结构中。然后将该结构和数据本身写入名为 `recording.tmp` 的文件。图 4.8 显示了文件中的三个这样的事件。

![](img/41b4c8f6d6a5c349eee321a301703d97_283_0.png)

**图 4.8** 录制文件的布局。

这是 *事件*（event）结构体，以及用于文件名称和读写数据缓冲区大小的全局文件描述符和宏：

```c
#define EVFILE "recording.tmp"
#define EVBUFSIZE 512

struct event {
    struct timeval e_time;
    unsigned e_datalen;
};
static int fd_ev = -1;
```

*timeval* 结构体在第 1.7.1 节中解释过。

录波器使用 `ev_creat` 打开录制文件（必要时创建该文件），使用 `ev_write` 向其中写入事件，并使用 `ev_close` 关闭它：

```c
static bool ev_creat(void)
{
    EC_NEG1( fd_ev = open(EVFILE, O_WRONLY | O_CREAT | O_TRUNC,
        PERM_FILE) )
    return true;

    EC_CLEANUP_BGN
        return false;
    EC_CLEANUP_END
}

static bool ev_write(char *data, unsigned datalen)
{
    struct event ev = { { 0 } };

    get_rel_time(&ev.e_time);
    ev.e_datalen = datalen;
    ec_negl( writeall(fd_ev, &ev, sizeof(ev) ) )
    ec_negl( writeall(fd_ev, data, datalen) )
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}

static void ev_close(void)
{
    (void)close(fd_ev);
    fd_ev = -1;
}
```

`writeall` 是写入完整缓冲区的一种简单方法，即使这需要多次调用 write；它来自第 2.9 节。

函数 `get_rel_time` 执行调用 `gettimeofday`（第 1.7.1 节）获取当前时间并从起始时间（它在第一次调用时保存）中减去的操作，使用另一个函数 `timeval_subtract`：

```c
static void get_rel_time(struct timeval *tv_rel)
{
    static bool first = true;
    static struct timeval starttime;
    struct timeval tv;

    if (first) {
        first = false;
        (void)gettimeofday(&starttime, NULL);
    }
    (void)gettimeofday(tv, NULL);
    timeval_subtract(&tv, &starttime, tv_rel);
}

static void timeval_subtract(const struct timeval *x,
    const struct timeval *y, struct timeval *diff)
{
    if (x->tv_sec == y->tv_sec || x->tv_usec >= y->tv_usec) {
        diff->tv_sec = x->tv_sec - y->tv_sec;
        diff->tv_usec = x->tv_usec - y->tv_usec;
    }
```

