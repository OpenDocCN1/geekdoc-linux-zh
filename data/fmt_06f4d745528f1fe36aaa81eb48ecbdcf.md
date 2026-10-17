
| 选项 | 描述 |
| --- | --- |
| `LOG_CONS` | 错误时记录到控制台 |
| `LOG_NDELAY` | 不要延迟注册 |
| `LOG_ERROR` | 记录错误消息 |
| `LOG_PID` | 包含进程 ID |

`closelog` 可以在应用程序结束时调用。

## 13.4 `daemon_init` Function

图 13.4 显示了 `daemon_init`：使进程守护化。

`daemon_init.c`

```c
#include "unp.h"
#include "syslog.h"
#define MAXFD 64
extern int daemon_proc; /* defined in error.c */
int daemon_init(const char *pname {
    openlog(pname, LOG_PID, facility);
    return (0); /* success */
}
```

### `fork`

我们首先调用 `fork`，然后父进程终止，留下子进程运行。如果进程是在前台启动的命令，当父进程终止时，shell 认为命令已完成。这使得进程在后台运行。此外，子进程继承了父进程的 PID，但获得了自己的 PID。这保证了子进程不是进程组首，这是后续调用 `setid` 必须的。

### `setid`

`setsid` 是创建一个新会话的 POSIX 函数。（APUE 第 9 章详细讨论了进程关系和会话。）进程成为新会话的首，成为新进程组的首，并且没有控制终端。

### Ignore `SIGHUP` and Again

我们忽略 `SIGHUP` 并再次调用 `fork`。当此函数返回时，父进程实际上是第一个孩子，它终止，留下第二个孩子运行。第二次 `fork` 的目的是保证守护进程在打开终端设备时自动获取终端。当没有控制终端的会话首打开终端设备（该设备不是当前某个会话的控制终端）时，终端变为该会话的控制终端。通过再次调用 `fork`，我们保证第二个孩子不再是会话首，因此无法获取终端。当会话首（第一个孩子）终止时，由于忽略 `SIGHUP`，会话中的所有进程（我们的第二个孩子）都不会收到 `SIGHUP`。

### Set Flag for Error Functions

我们将 `daemon_proc` 设置为非零。这个外部变量由我们的 `err_XXX` 函数（节 D.3）定义，当其值非零时，我们告诉它们调用 `syslog` 而不是向标准执行 `fprintf`。这避免了在服务器不是守护进程运行时（即我们在测试服务器时）遍历所有的代码和我们的错误函数，但在其作为守护进程运行时调用 `syslog`。

### Change Working Directory

我们将工作目录更改为根目录，尽管某些守护进程可能有理由更改其他目录。例如，打印机守护进程可能会更改到打印机的池目录，在那里执行工作。如果守护进程生成了核心文件，它将生成在工作目录。更改工作目录的另一个原因是守护进程可能在任何文件系统中启动，如果它留在那里，该文件系统将无法卸载（至少不能使用某些具有破坏性的、强制性的措施）。

### 关闭打开的文件描述符

25–27 我们关闭了从执行守护进程的进程（通常是 shell）继承而来的打开描述符。问题在于确定正在使用的最高描述符：没有一个 Unix 函数可以提供这个值。虽然有方法确定进程可以打开的最大描述符数量，但这变得很复杂（见 APUE 第 43 页），因为限制可能是无限的。我们的解决方案是关闭前 64 个描述符，尽管它们大部分可能并没有被打开。

Solaris 提供了一个名为 `closefrom` 的函数，供守护进程使用以解决这个问题。

### 将 `stdin`、`stdout`、`stderr` 重定向到 `/dev/null`

29–31 我们为标准输入、标准输出和标准错误打开 `/dev/null`。这保证了这些常用描述符是打开的，对其中任何描述符的读取都会返回 `EOF`，且内核会丢弃写入它们的任何内容。打开这些描述符的原因是，守护进程调用的任何库函数如果从标准输入读取，或者写入标准输出或错误，都不会失败。失败可能是危险的。如果守护进程结束了打开到客户端的套接，该套接描述符将变成 `stderr`，随后对类似 `perror` 的某些错误调用可能会向客户端发送意想不到的数据。

### 使用 `syslog` 处理错误

32 `Openlog` 第一个参数来自调用者，通常是程序名称（例如 `argv[0]`）。我们指定在每条日志消息中添加进程 ID（PID）。设施（facility）也由调用者指定，采用图 13.2 中的值，或者如果接受默认的 `LOG_USER` 则设为 0。

我们注意到，守护进程在没有控制终端的情况下运行，它应该接收来自内核的 `SIGHUP` 信号。因此，如果守护进程的配置发生了变化，守护进程应该重新读取文件。守护进程永远不接收的两个信号是 `SIGINT` 和 `SIGWINCH`，因此守护进程可以安全地使用这些信号作为管理员指示守护进程做出反应变化的另一种方式。

### 示例：作为守护进程的日期服务器

图 13.5 是我们来自图 13.14 的协议无关服务器的函数，它调用了我们的 `daemon_init` 函数作为守护进程运行。

只有两个：我们在程序启动时调用 `daemon_init` 函数，并使用 `printf` 调用我们的 `err_msg` 函数来打印客户端的 IP 地址和端口。如果我们希望程序作为守护进程运行，我们必须避免调用 `printf` 和 `fprint` 函数，并使用我们的 `err_msg` 函数。

注意我们在调用 `daemon_init` 之前如何检查 `arg` 并使用正确的用法提示。这允许启动守护进程的用户在命令行参数数量不正确时获得立即反馈。`daemon_init` 之后，所有后续错误消息都将发送 `syslog`。

如果我们在 Linux 主机 `linux` 上运行此程序，然后在从同一台机器（例如 `localhost`）连接后检查 `/var/log/messages` 文件（我们发送所有 `LOG_USER` 消息的地方），我们将得到

```
Jun 10 09:54:37 linux dayimetcpsrv2[24288]: connection from 127.0.0.1.55862
```

（我们包装了这一行。）日期、时间和主机名由 `syslog` 守护进程自动添加前缀。

### 图 13.5：作为守护进程运行的协议无关日期服务器

`inetd/dayimetcpsrv2.c`

```c
#include "unp.h"
#include <time.h>

int
main(int argc, char **argv)
{
    int listenfd, confd;
    socklen_t addrlen, len;
    struct sockaddr *cliaddr;
    char buff[MAXLINE];
    time_t ticks;

    if (argc < 2 || argc > 3) {
        err_quit("usage: dayimetcpsrv2 <host> <service or port>");
    }
    daemon_init(argv[0], 0);

    if (argc == 2) {
        listenfd = Tcp_listen(NULL, argv[1], &addrlen);
    } else {
        listenfd = Tcp_listen(argv[1], argv[2], &addrlen);
    }

    cliaddr = Malloc(addrlen);
    for ( ; ; ) {
        len = &addrlen;
        confd = Accept(listenfd, cliaddr, &len);
        err_msg("connection from %s", getname(cliaddr, len));

        ticks = time(NULL);
        snprintf(buff, sizeof(buff), "Date: %s", ctime(&ticks));
        Write(confd, buff, strlen(buff));
        Close(confd);
    }
}
```

## 13.5 守护进程 (wait/nowait)

我们注意到，守护进程在没有控制终端的情况下运行，它应该接收来自内核的 `SIGHUP` 信号。因此，如果守护进程的配置发生了变化，守护进程应该重新读取文件。守护进程永远不接收的两个信号是 `SIGINT` 和 `SIGWINCH`，因此守护进程可以安全地使用这些信号作为管理员指示守护进程做出反应变化的另一种方式。
