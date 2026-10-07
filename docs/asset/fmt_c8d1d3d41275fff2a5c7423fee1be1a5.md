
最终，由 `ptyFork()` 创建的子进程将会终止。如果父进程没有同时终止，则它必须等待子进程以消除产生的僵进程。然而，这一步可以省略，因为使用伪终端的应用程序通常设计为父进程与子进程同时终止。

BSD 衍生版提供了两个用于处理伪终端的相关非标准函数。其中第一个是 `openpty()`，它打开一对伪终端，返回主设备和从设备的文件描述符，并可选地根据类似于 `slaveTermios` 和 `slaveWS` 的参数设置终端属性和窗口大小。另一个 `forkpty()` 与我们的 `fork()` 相同，但它没有提供 `snlen` 参数的对应项。在 Linux 上，这两个函数都由 `glibc` 提供。

### 列表 64-2：`ptyFork()` 的实现

```c
#include <fcntl.h>
#include <termios.h>
#include <sys/ioctl.h>
#include "pty_master.h"
#include "pty_fork.h"                /* 声明 ptyFork() */
#include "tlp_hdr.h"
```

```c
#define MAX_SNAME 1000

pid_t
ptyFork(const char *slaveName, size_t snLen,
	const struct termios *slaveTermios, const struct winsize *slaveWS)
{
	int mfd, slaveFd, savedErrno;
	pid_t childPid;
	char slname[MAX_SNAME];
```

```c
mfd = ptyMasterOpen(slname, MAX_SNAME);
if (mfd == -1)
    return -1;
```

```c
if (slaveName != NULL) { /* 向调用者返回从设备名称 */
    if (strlen(slaveName) < snLen) {
        strncpy(slaveName, slname, snLen);
```

```c
} else { /* 'slaveName' 太小了 */
    close(mfd);
    errno = EOVERFLOW;
    return -1;
  }
```

```c
childPfd = fork();

if (childPfd == -1) { /* fork() 失败 */
    savedErrno = errno; /* close() 可能会改变 'errno' */
    close(mfd); /* 防止泄露文件描述符 */
    errno = savedErrno;
    return -1;
}
```

```c
if (childPfd == 0) { /* 父进程 * */
    *masterFd = mfd; /* 只有父进程获取 master fd */
    return childPfd; /* 类似于 fork() 的父进程 */
}
```

```c
if (setsid() == -1) { /* 开启新会话 */
    err_exit("ptyfork:setsid");
}
```

```c
close(mfd); /* 子进程不需要 */
```

```c
slaveFd = open(slname, O_RDWR); /* 变为控制 tty */
if (slaveFd == -1)
    err_exit("ptyfork:open-slave");
```

```c
#ifdef TIOCSCTTY /* BSD 上获取控制 tty * */
if (ioctl(slaveFd, TIOCSCTTY, 0) == -1)
    err_exit("ptyfork:TIOCSCTTY");
#endif
```

```c
if (slaveTermios != NULL) { /* 设置从设备类型属性 */
    if (tsetattr(slaveFd, TCSANOW, slaveTermios) == -1)
        err_exit("ptyfork:tsetattr");
}
```

```c
if (slaveWS != NULL) { /* 设置从设备窗口大小 * */
    if (ioctl(slaveFd, TIOCSWINSZ, slaveWS) == -1)
        err_exit("ptyfork:TIOCSWINSZ");
}
```

```c
/* 将 pty 从设备复制为子进程的 stdin, stdout 和 stderr */

if (dup2(slaveFd, STDIN_FILENO) != STDIN_FILENO)
    err_exit("ptyfork:dup2-STDIN_FILENO");
if (dup2(slaveFd, STDOUT_FILENO) != STDOUT_FILENO)
    err_exit("ptyfork:dup2-STDOUT_FILENO");
if (dup2(slaveFd, STDERR_FILENO) != STDERR_FILENO)
    err_exit("ptyfork:dup2-STDERR_FILENO");

if (childPfd == 0) { /* 子进程 */
    close(slaveFd);
    return 0;
}

/* 父进程 */
*masterFd = mfd; /* 只有父进程获取 master fd */
return childPfd; /* 类似于 fork() 的父进程 */
}
```

## 伪终端

伪终端是一种允许程序表现得像终端的机制。它们由一对设备组成：主设备和从设备。主设备由控制程序使用，而从设备由子进程使用。

`ptyFork()` 函数提供了一种设置伪终端对并派生子进程的方法，从而为子进程设置环境。

## 数据包模式 (Packet mode)

数据包模式是一种机制，允许运行在伪终端主设备之进程在从设备发生以下与软件流控制相关的事件时获得通知：

- 输入或输出队列被刷新；
- 终端输出停止或启动（Control-S/Control-Q）；
- 流控制被启用或禁用。

数据包模式有助于处理某些网络服务的伪终端应用程序（例如 `telnet` 和 `rlogin`）中的流控制。

通过对指向伪主设备的文件描述符应用 `ioctl()` `TIOCPK` 操作来启用数据包模式：

```c
int arg;
arg = 1;      /* 1 == 启用; 0 == 禁用 */
if (ioctl(mfd, TIOCPK, arg) == -1)
    err_exit("ioctl");
```

当数据包模式运行时，从伪主设备读取会返回一个非零控制字节（表示从设备上发生的状态变化的位掩码），或者返回写入伪从设备的一个或多个字节的 0 字节。

当处于数据包模式的伪主设备发生状态变化时，`select()` 表示主设备上发生了异常情况（`except` 参数），而 `poll()` 在事件字段中返回 `POLLIN`。（有关 `select()` 和 `poll()` 的描述请参考第 63 章）。

数据包模式在 SUS3 中并未标准化，某些 UNIX 实现中存在差异。Linux 上数据包模式的更多细节（包括用于指示状态变化的位掩码值）可以在 `tty_ioctl(4)` 手页中找到。

### 64.6 实现 script(1)

我们现在准备好实现标准 `script(1)` 程序的简单版本。该程序启动一个新的 shell 会话，并将会话中的所有输入和输出记录到一个文件中。书中显示的大多数 shell 会话都是使用 `script` 记录的。

在正常的登录会话中，shell 直接连接到用户的终端。当我们运行 `script` 时，它会将自己置于用户终端和 shell 之间，并使用伪终端对（pseudoterminal pair）在它与 shell 之间创建一个通信通道（见图 64-4）。shell 连接到伪终端的从端。`script` 进程充当用户的代理，获取在终端输入的输入并将其写入伪终端主端，同时从伪终端主端读取输出并将其写入用户的终端。

此外，`script` 会产生一个输出文件（默认命名为 `typescript`），该文件包含了伪终端主端上输出的所有内容的副本。这种效果是不仅记录了 shell 会话产生的输出，还记录了提供它的输入。输入之所以被记录，是因为在传统的终端设备中，内核通过将输入字符复制到终端输出队列来回显输入字符（见第 1291 页的图 62-1）。然而，当禁用终端回显时（如读取密码的程序所示），伪终端从端的输入不会被复制到从端输出队列，因此也不会被复制到 `script` 输出文件中。

![](img/9979af2ec677a84a39c7b1fd105c84a4_1433_0.png)

图 64-4：script 程序

我们对 `script` 的实现如列表 64-3 所示。该程序执行以下步骤：

- 获取程序运行 ① 所在的终端的属性和窗口大小。这些属性被传递给后续的 `ptyFork()` 调用，该调用使用它们来设置伪终端从端设备的对应值。
- 调用我们的 `ptyFork()` 函数（列表 64-2）来创建一个子进程，该子进程通过伪终端对 ② 与父进程连接。
- 在 `ptyFork()` 调用之后，子进程执行一个 shell ③。shell 的选择取决于环境变量 `SHELL` 变量的设置 ④。如果 `SHELL` 变量未设置或为空字符串，则子进程执行 `/bin/sh`。
- 在 `ptyFork()` 调用之后，父进程执行以下步骤：
    - 打开 `script` 文件 ⑤。如果提供了命令行参数，则将其用作脚本文件名。如果没有提供命令行参数，则使用默认名称 `typescript`。
    - 将终端设置为原始模式（raw mode）（使用第 1310 页列表 62-3 中的 `ttySetRaw()` 函数），这样所有输入字符都会直接传递给 `script` 程序，而不被终端驱动程序修改 ⑥。script 程序输出的字符同样不会被终端驱动程序修改。

    > 处于原始模式并不意味着未解释的控制字符将传输到 shell（或伪终端从端设备所属的任何进程组中），也不意味着该进程的输出将传递到用户的终端。终端特殊字符的解释是在从端内部进行的（除非该从端也由应用程序显式地置于原始模式）。通过将用户的终端设置为原始模式，我们防止了对输入和输出字符发生第二轮解释。

    - 调用 `atexit()` 安装一个处理程序，在程序终止时将终端重置为原始模式 ⑦。
    - 执行一个循环，在终端和伪终端主端之间双向传输数据 ⑧。在每次循环迭代中，程序使用 `select()`（第 63.2.1 节）监控终端和伪终端主端的输入 ⑨。如果终端可用输入，程序读取部分输入并将其写入伪终端主端 ⑩。同样，如果伪终端主端有可用输入，程序读取部分输入并将其写入终端以及 `script` 文件 ⑪。该循环一直执行，直到在某个被监控的文件描述上检测到文件结束或错误。

### 列表 64-3：script(1) 的简单实现

```c
#include <sys/stat.h>
#include <fcntl.h>
#include <libgen.h>
#include <termios.h>
#include <sys/select.h>
#include <pty.h>           /* ptyFork() 的声明 */
#include <tty_functions.h> /* ttySetRaw() 的声明 */
#include <tlpi_hdr.h>

#define BUF_SIZE 256
#define MAX_SNAME 1000

struct ttyOrig;

static void         /* 程序退出时重置终端模式 */
ttyReset(void)
{
    if (tcgetattr(STDIN_FILENO, TCANOW, &ttyOrig) == -1)
        errError("tcsetattr");
}

int main(int argc, char *argv[])
{
    char slaveName[MAX_SNAME];
    char *shell;
    int masterFd, scriptFd;
    struct winsize ws;
    fd_set infds;
    char buf[BUF_SIZE];
    size_t numRead;
    pid_t childPid;

    if (tcgetattr(STDIN_FILENO, &ttyOrig) == -1)
        errError("tcgetattr");
    if (ioctl(STDIN_FILENO, TIOCGWZ, &ws) < 0)
        errError("ioctl-TIOCGWZ");

    childPid = ptyFork(&masterFd, slaveName, MAX_SNAME, &ttyOrig);
    if (childPid == -1)
        errError("ptyFork");

    if (childPid == 0) { /* 子进程在伪终端从端执行 shell */
        shell = getenv("SHELL");
        if (shell == NULL || *shell == '\0')
            shell = "/bin/sh";

        execl(shell, (char *)NULL); /* 如果这里出错了 */
        errError("execl");
    }

    /* 父进程：在终端和伪终端主端之间转发数据 */
    scriptFd = open(argc > 1 ? argv[1] : "typescript",
              O_WRONLY | O_CREAT | O_TRUNC,
              S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP |
              S_IROTH | S_IWOTH);

    if (scriptFd == -1)
        errError("open");

    ttySetRaw(STDIN_FILENO, &ttyOrig);

    if (atexit(ttyReset) == 0)
        errError("atexit");

    for (;;) {
        FD_ZERO(&infds);
        FD_SET(STDIN_FILENO, &infds);
        FD_SET(masterFd, &infds);

        if (select(masterFd + 1, &infds, NULL, NULL) == -1)
            errError("select");

        if (FD_ISSET(STDIN_FILENO, &infds)) { /* stdin -> pty */
            numRead = read(STDIN_FILENO, buf, BUF_SIZE);
            if (numRead < 0)
                exit(EXIT_SUCCESS);
            if (write(masterFd, buf, numRead) != numRead)
                errError("failed write (masterFd)");
        }

        if (FD_ISSET(masterFd, &infds)) { /* pty -> stdout */
            numRead = read(masterFd, buf, BUF_SIZE);
            if (numRead < 0)
                exit(EXIT_SUCCESS);
            if (write(STDOUT_FILENO, buf, numRead) != numRead)
                errError("failed write (STDOUT_FILENO)");
            if (write(scriptFd, buf, numRead) != numRead)
                errError("failed write (scriptFd)");
        }
    }
}
```

## pty/script.c

在下面的会话中，我们演示列表 64-3 中程序的使用。首先显示登录 shell 运行时 xterm 使用的终端名称以及登录 shell 的进程 ID。这些信息在 shell 会话中很有用。

```bash
$ tty
/dev/pts/1
$ echo $$
```

然后我们启动 script 程序的实例，它调用了一个子 shell。再次显示运行 shell 的终端名称和 shell 的进程 ID：

```bash
$ ./script
$ tty
/dev/pts/24
$ echo $$
29825
```

script 打开的伪终端从端

script 启动的子 shell 进程

现在我们使用 `ps(1)` 显示 shell 以及运行 script 的进程信息，然后终止 script 启动的 shell：

```bash
$ ps -p 7979 -p 29825 -C script -o "pid ppid sid tty cmd"
PID PPID SID TT CMD
7979 7972 7979 pts/1 /bin/bash
29824 7979 7979 pts/1 /script
29825 29824 29825 pts/24 /bin/bash
$ exit
```
