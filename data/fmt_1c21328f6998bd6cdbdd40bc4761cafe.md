
```c
    */

    if ((fdm = pty_open(pts_name)) < 0)
        err_sys("can't open slave pty: %s");

    close(fdm); /* 子进程中完成主设备的操作 */

    #if defined(TIOCSCTTY)
    /*
     * TIOCSCTTY 是 BSD 获取控制终端的方法。
     */
    if (ioctl(fdm, TIOCSCTTY, (int*)0) < 0)
        err_sys("TIOCSCTTY error");
    #endif

    /*
     * 设置从设备的 termios 和窗口大小。
     */
    if (slave_termios != NULL)
        if (tcsetattr(fdm, TCSANOW, slave_termios) < 0)
            err_sys("tcsetattr error on slave pty: %s");
    if (slave_winsize != NULL)
        if (ioctl(fdm, TIOCWINSIZE, slave_winsize) < 0)
            err_sys("TIOCWINSIZE error on slave pty: %s");

    /*
     * 从设备成为子进程的 stdin/stdout/stderr。
     */
    if (dup2(fdm, STDIN_FILENO) != STDIN_FILENO)
        err_sys("dup2 error to stdin: %s");
    if (dup2(fdm, STDOUT_FILENO) != STDOUT_FILENO)
        err_sys("dup2 error to stdout: %s");
    if (dup2(fdm, STDERR_FILENO) != STDERR_FILENO)
        err_sys("dup2 error to stderr: %s");

    /* 子进程 */
    if (fds != STDIN_FILENO && fds != STDOUT_FILENO && fds != STDERR_FILENO)
        close(fds);

    return(0); /* 子进程返回 0，类似于 fork() */
} else { /* 父进程 */
    *ptrfd = &fdm; /* 返回主设备的 fd */
    return(pid); /* 父进程返回子进程的 pid */
}
}
```

打开 `PTY` 后，调用了 `fork`。正如我们之前提到的，我们希望等待子进程在调用 `pty_open` 之后调用 `setsid` 来建立一个新会话。当它调用 `setsid` 时，子进程并不是进程领导者，列出的三个步骤是：(a) 创建一个以子进程为会话领导者的新会话，(b) 为子进程创建一个新的进程组，以及 (c) 设置新会话的控制终端。在 `FreeBSD` 和 `Mac OS` 下，我们必须调用带有 `TIOCSCTTY` 参数的 `ioctl`（`Linux` 也支持 `TIOCSCTTY` 命令）。两个 `termios` 结构体在子进程中分配。最后，从设备文件描述符被复制到子进程的标准输入、标准输出和标准错误中。这意味着无论调用者 `exec` 什么程序，这三个描述符都将连接到从设备 `PTY`（其控制终端）。在 `fork` 调用后，父进程返回 `PTY` 主描述符和子进程的进程 ID。在下一节中，我们将使用...

```c
static void sig_term(int);
static volatile sig_atomic_t sigcaught; /* 由信号处理程序设置 */
```

```c
void
loop(int pytm, int ignoreof)
{
    pid_t child;
    int nread;
    char buf[BUFSIZE];

    if ((child = fork()) < 0) {
        err_sys("fork error");
    } else if (child == 0) { /* 将 stdin 拷贝到 ptm */
        for (; ; ; ) {
            if ((nread = read(STDIN_FILENO, buf, BUFSIZE)) < 0) {
                err_sys("read error from stdin");
            } else if (nread == 0) {
                break; /* stdin 的 EOF 意味着我们完成了 */
            }

            if (write(ptym, buf, nread) != nread)
                err_sys("written error to master pty");
        }

        /*
         *我们遇到 stdin 的 EOF 时总是终止，
         * 但只有在 ignoreof 为 0 时我们才会通知父进程。
         */
        if (ignoreof == 0) {
            kill(getppid(), SIGTERM); /* 通知父进程 */
            exit(0); /* 并终止；子进程无法返回 */
        }
    }

    /*
     * 父进程将 ptm 拷贝到 stdout。
     */
    if (signal_intr(SIGTERM, sig_term) == SIG_ERR)
        err_sys("signal_intr error for SIGTERM");

    for (; ; ; ) {
        if ((nread = read(ptym, buf, BUFSIZE)) <= 0)
            break; /* 捕获信号，或 EOF */

        if (write(STDOUT_FILENO, buf, nread) != nread)
            err_sys("written error to stdout");
    }

    /*
     * 有三种方式获取：sig_term() 在下方捕获了子进程的 SIGTERM，
     * 在 pty 主设备上读到 EOF（意味着我们必须信号子进程停止），
     * 或者发生了错误。
     */
    if (sigcaught == 0) /* 如果子进程没有向我们发送信号，则告诉它 */
        kill(child, SIGTERM);

    /*
     * 父进程返回调用者。
     */
}

/*
 * 当子进程在 pty 从设备上获取 EOF（read() 失败）时，
 * 向我们发送 SIGTERM。我们可能中断了对 pytm 的 read()。
 */
static void
sig_term(int signos) 
{
    sigcaught = 1; /* 仅设置标记并返回 */
}
```

注意，有两个进程时，当其中一个终止时，它必须通知另一个。我们使用 `SIGTERM` 信号进行通知。

![](img/902515e97eef28cac8083866e00a6f4c_904_0.png)

# 19.6. 使用 `pty` 程序

我们将查看 `pty` 程序的各种示例，以了解命令行选项的必要性。

如果我们的 shell 是 `Korn shell`，我们可以执行：

```bash
pty ksh
```

并获得一个全新的 shell 调用实例，它运行在伪终端下。

如果文件 `ttyname` 是我们在图 18.16 中显示的程序，我们可以按照如下方式运行 `pty` 程序：

```bash
$ who
sar :0 Oct 5 18:07
sar pts/0 Oct 5 18:07
sar pts/1 Oct 5 18:07
sar pts/2 Oct 5 18:07
sar pts/3 Oct 5 18:07
sar pts/4 Oct 5 18:07
pts/4 是当前正在使用的最高 PTY

从 PTY 运行图 18.16 中的程序
$ pty ttyname
fd 0: /dev/pts/5
pts/5 是下一个可用的 PTY
fd 1: /dev/pts/5
fd 2: /dev/pts/5
```

# `umpf` 文件

在 6.8 节中，我们描述了 `umfp` 文件，它记录了当前登录到 `UNIX` 系统的所有用户。问题是在伪终端上运行程序的用户是否被视为已登录。对于远程登录（`telnet` 和 `login`），显然应该为登录到伪终端的用户在 `umfp` 文件中创建一个条目。然而，并没有达成共识，从窗口系统或程序（如脚本）在伪终端上运行 shell 的用户应该在 `umfp` 文件中创建条目。有些系统记录这些内容，有些则没有。如果系统不在 `umfp` 文件中记录这些内容，`who`(1) 程序通常不会显示正在使用的相应伪终端。

除非 `umfp` 允许其他写入权限（这被认为是一个安全漏洞），否则使用伪终端的随机程序将无法写入此文件。

# 作业控制交互

如果我们在 `pty` 下运行作业控制 shell，它会正常工作。例如：

```bash
pty ksh
```

在 `pty` 下运行 `Korn shell`。我们可以在这个新 shell 中运行程序，并像使用登录 shell 一样使用作业控制。如果我们在 `pty` 下运行一个非作业控制的交互式程序，如：

```bash
pty cat
```

在键入 `pty` 控制挂起字符之前，一切都是正常的。在那个时刻，`pty` 控制挂起字符会被忽略。要了解发生了发生了什么，我们需要检查进程组和会话。图 19.14 显示了 `pty` 的布局。

![](img/902515e97eef28cac8083866e00a6f4c_906_png)

当我们键入 `pty` 控制挂起字符时，`pty` 控制挂起字符会被忽略。要了解发生了发生了什么，我们需要检查进程组和会话。图 19.14 显示了 `pty` 的布局。

# 观察长时间运行程序的输出

在图 15.8 中，协进程无法使用标准 I/O 函数，因为标准输入和输出不指向终端，因此标准 I/O 函数将其处理为全缓冲。如果我们通过将以下行：

运行 `pty` 程序：

```c
if (excl("/dev/add2", "add2", (char *)j0) < 0)
```

替换

```c
if (excl("/dev/pty", "pty", "-e", "add2", (char *)j0) < 0)
```

现在程序可以工作了，如果协进程使用了标准 I/O。
图 19.16 显示了当我们使用伪终端作为输入和输出运行协进程时的进程布局。它是一个

# `script` 程序

使用 `pty` 程序，我们可以通过以下 shell 脚本实现 `script(1)` 程序：

```bash
#!/bin/sh
ty "${SHELL:-/bin/sh}" | teescript
```

一旦运行了这个 shell 脚本，我们就可以执行 `ps` 命令查看所有的进程关系，19.15 详细说明了这些关系。

## 图 19.15. `script` shell 的进程布局

![](img/902515e97eef28cac8083866e00a6f4c_908_0.png)

图 19.5 的扩展，显示了所有的进程连接和数据流。标记为“驱动程序”的框是图 15.8 中的程序，并按照之前的描述修改了输出的 `-e` 回显部分。

## 图 19.16. 以伪终端作为输入和输出运行协进程

[查看全尺寸图像]

![](img/902515e97eef28cac8083866e00a6f4c_909_0.png)

这个示例展示了 `pty` 程序需要 `-e` (`echo`) 选项的原因。`pty` 程序没有以交互模式运行，因为它的标准输入没有连接到终端。图 19.12 中的交互标志默认为 `false`，因为对 `isatty` 的调用返回 `false`。这意味着实际终端之上的行律保持在规范模式（canonical mode）并启用了回显。通过指定 `-e` 选项，我们关闭了 `PTY` 属设备上方行律模块中的回显。如果我们不这样做，我们输入的每一个字符都会被行律回显两次。

我们还使用 `-e` 选项关闭 `terms` 结构中的 `ICRNL` 标志，以防止协进程的所有输出都被回车和换行符终止。

在不同系统上测试此示例显示了另一个问题，我们在第 14.8 节描述 `read` 和 `write` 函数时曾提到这一点。描述符返回的数据量不同于普通的磁盘文件，在不同实现之间可能不同。这个使用 `pty` 的协进程示例给出了意想不到的结果，追溯发现是因为图 15.8 程序中管道上的 `read` 函数返回的内容少于一行。解决方案不是使用图 15.8 中的程序，而是使用练习 15 中修改过的程序版本，该版本被修改为使用标准 I/O 库，并将两个管道的标准 I/O 流都设置为行缓冲（line buffering）。通过这种方式，`fgets` 函数会执行所需的多次读取以获取完整的一行。图 15.8 假设发送到协进程的每一行都会返回一个行。

# 非交互式地驱动交互式程序

尽管人们可能认为 `pty` 可以运行任何协进程（即交互式协进程），但它行不通。问题在于 `pty` 只是将其标准输入上的所有内容复制到 `PTY` 和其标准输出，从不看它发送了什么或接收了什么。

例如，我们可以在 `pty` 下运行 `telnet` 命令来与远程主机通信：

```bash
telnet 192.168.1.3
```

这样做与直接输入 `telnet 192.168.1.3` 没有什么好处，但我们想从脚本中运行 `telnet` 程序，也许之后可以检查远程主机。在 `telnet.cmd` 文件中包含以下四行：

- `sar`
- `password`
- `uptime`
- `exit`

第一行是我们用于登录远程主机的名称，第二行是密码，第三行是我们想要运行的命令，第四行终止会话。如果我们如下运行此脚本：

```bash
pty -i < telnet.cmd telnet 192.168.1.3
```

它的执行结果不符合我们的预期。`telnet.cmd` 文件的内容在远程主机提示我们输入账户和密码之前就被发送进去了。当它关闭密码的回显时，`login` 使用了 `tcsetattr` 选项，这会丢弃任何已队列中的数据。因此，我们发送的数据被丢弃了。

当我们运行 `telnet` 程序时，我们在输入之前会与远程主机交互以获取密码提示，但 `pty` 程序并不知道这样做。这就是为什么我们需要一个比 `pty` 更复杂的程序（例如 `expect`）来从脚本文件驱动交互式程序。

即使像我们展示的那样从图 15.8 中的 `pty` 运行，这也没有帮助，图 15.6 中的程序假设我们向其写入的每一行都会在另一个管道上产生一行。但一行的输入可能会产生多行输出。图 15.8 总是在读取协进程之前向其发送一个连接。而我们工作时，我们希望在发送任何内容之前先与协进程交互。

从这里开始有几种方法从脚本驱动交互式程序。我们可以为 `pty` 添加一种命令语言和解释器，但可以使用合理的命令语言并利用 `pty` 的 `fork` 来调用交互式程序。这就是 `expect` 程序所做的。

我们将采取不同的路径，仅提供一个选项 (`-d`) 允许 `pty` 连接到一个驱动程序作为其输入和输出。驱动程序的标准输出是 `pty` 的标准输入和输出。这类似于 socket，但在“另一侧”是 `pty`。产生的进程安排几乎与图 19.16 相同，但在当前场景下，`pty` 对每个进程的驱动执行 `fork` 和 `exec`。此外，我们不再使用双工半管道，而是使用驱动程序和 `pty` 之间的双向管道。

图 19.17 显示了 `do_driver` 函数，当指定 `-d` 选项时，图 19.12 的主函数会调用它。

## 图 19.17. `pty` 程序的 `do_driver` 函数

```c
#include "apue.h"

void
do_driver(char *driver)
{
    pid_t child;
    int pipe[2];

    /*
      创建一个流管道与驱动程序通信。
     */
    if (pipe(pipe) < 0)
        perror("pipe");

    if ((child = fork()) < 0)
        perror("fork");
    else if (child == 0) {
        /* 子进程 */
        dup2(pipe[1], STDIN_FILENO);
        dup2(pipe[0], STDOUT_FILENO);
        close(pipe[0]);
        close(pipe[1]);
        execcl(driver, driver, (char *)NULL);
    } else {
        /* 父进程 */
        close(pipe[1]);
        {
            char c;
            while (read(pipe[0], &c, 1) > 0) {
```
