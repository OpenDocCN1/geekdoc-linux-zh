
```
#include "apue.h"

static int pfd1[2], pfd2[2];

void TELL_WAIT(void)
{
  if (pipe(pfd1) < 0 || pipe(pfd2) < 0)
    err_sys("pipe error");
}

void TELL_PARENT(void)
{
  if (write(pfd2[1], "c", 1) != 1)
    err_sys("write error");
}

void WAIT_PARENT(void)
{
  char c;
  if (read(pfd1[0], &c, 1) != 1)
    err_sys("read error");

  if (c != 'p')
    err_quit("WAIT_PARENT: incorrect data");
}

void TELL_CHILD(pid_t pid)
{
    if (write(pfd1[1], "p", 1) != 1)
    err_sys("write error");
}

void WAIT_CHILD(void)
{
    char c;
    if (read(pfd2[0], &c, 1) != 1)
        err_sys("read error");

    if (c != 'c')
        err_quit("WAIT_CHILD: incorrect data");
}
```

## 图 15.8. 使用两个管道进行父子同步

`img/902515e97eef28cac8083866e00a6f4c_680_png`

### 15.3. `popen` `pclose` 函数

由于一种常见操作是为另一个进程创建管道以读取其输出或发送，`I/O` 库历史上提供了 `popen` 和 `pclose` 函数。这两个函数处理了我们一直在做的工作：创建管道、`fork` 子进程、关闭未使用的端、执行 `shell` 运行命令以及等待命令终止。

```
#include <stdio.h>

FILE *popen(const char *cmdstring, const char *type);
```

返回：文件指针，错误时返回 `NULL`

```
int pclose(FILE *fp);
```

返回：`cmdstring` 的终止状态，错误时返回 `1`

函数 `popen` 执行 `fork-exec` 并返回一个标准 `I/O` 管道指针。如果 `type` 为 `"r"`，则文件指针连接到 `cmdstring` 的标准输出（图 15.9）。

## 图 15.9. `fp = popen(cmdstring, "r")` 的结果

![](img/902515e97eef28cac8083866e00a6f4c_682_0.png)

如果 `type` 为 `"w"`，则文件指针连接到 `cmdstring` 的标准输入，如图 15.10 所示。

## 图 15.10. `fp = popen(cmdstring, "w")` 的结果

记忆最后一个参数的方法是记住：与 `popen` 一样，返回的文件指针如果是 `"r"` 就是可读的，如果是 `"w"` 就是可写的。

`pclose` 函数关闭 `I/O` 流，等待命令并返回 `shell` 的终止状态。（我们在第 8.6 节描述了终止状态。第 8.13 节描述的系统函数也返回终止状态。）如果无法执行 `shell`，`pclose` 返回的终止状态就像 `shell` 执行了 `exit(127)`。

`cmdstring` 由 `Bourne shell` 执行，例如：

```
sh -c cmdstring
```

这意味着 `shell` 会扩展 `cmdstring` 中的任何字符。这允许我们说，例如：

```
fp = popen("ls -c", "r");

或者
fp = popen("cmd 2>&1", "r");
```

#### 示例

让我们重做图 15.6 中的程序。这是使用 `popen`。如图 15.11 所示。

使用 `popen` 减少了我们需要编写的代码量。

`shell` 命令 `$PAGER:-more` 表示如果 `shell` 变量 `PAGER` 定义且不为空则使用其值；否则使用字符串 `more`。

## 图 15.11. 使用 `popen` 将文件拷贝到分页器程序

```
#include "apue.h"
#include <sys/wait.h>

#define PAGER "${PAGER:-more}" // 环境变量或默认值 \n
int
main(int argc, char *argv[])
{
    char line[MAXLINE];
    FILE *tpin, *fpout;
```

### `popen` 和 `pclose` 函数

图 15.12 显示了我们版本的 `popen` 和 `pclose`。

虽然 `popen` 的代码与我们在本章早些时候使用的代码相似，但我们需要进行一些细节处理以清除文件描述符。首先，每次调用 `popen` 时，我们必须记住我们创建的子进程的 `PID`，以及它的文件描述符或 `PID`。我们选择将子 `PID` 存储在一个数组 `childpid` 中，并用文件描述符进行索引。这样，我们就可以将 `FILE` 指针作为参数进行关闭，因为我们使用标准 `I/O` `fileno` 获取描述符，然后获取子进程 `ID` 以供 `waitpid` 调用。由于进程可能会多次调用 `popen`，因此我们动态地分配了 `childpid` 数组（在第一次调用 `popen` 时），预留了与描述符数量相同的子进程空间。

调用 `popen` 和 `fork`，然后为每个进程复制相应的描述符，这与在本章早些时候的操作相似。`POSIX.1` 要求 `popen` 关闭所有从之前的 `popen` 调用中仍打开的流。为了做到这一点，我们遍历 `childpid` 数组并关闭任何仍然打开的描述符。

如果 `pclose` 调用建立了 `SIGCHLD` 信号处理程序会发生什么？`pclose` 中的 `waitpid` 调用将返回错误 `EINTR`。由于调用者允许捕获此信号（任何其他中断 `waitpid` 的信号），如果 `waitpid` 被捕获的信号中断，我们只需再次调用 `waitpid`。

请注意，如果应用程序调用 `waitpid` 并获取了由 `popen` 创建的子进程的退出状态，那么当应用程序调用 `pclose` 时，我们将等待并返回 `errno` 设置为 `ECHLD`。在这种情况下，`POSIX.1` 要求这种行为。

某些早期版本的 `pclose` 如果在等待期间被信号 `SIGINT`、`SIGQUIT` 和 `SIGHUP` 中断，会返回 `EINTR` 错误。此外，某些早期版本的 `pclose` 会阻塞或忽略 `SIGINT`、`SIGQUIT` 和 `SIGHUP` 信号。这是 `POSIX.1` 不允许的。

## 图 15.12. `popen` 和 `pclose` 函数

```c
#include "apue.h"
#include <errno.h>
#include <fcntl.h>
#include <sys/wait.h>

/*
 * 指向运行时分配的数组的指针
 */
static pid_t *childpid = NULL;

/*
 * 来自我们的 open_max()，图 2.16。
 */
static int maxfd;

FILE *
popen(const char *cmdstring, const char *type)
{
    int i;
    int pfd[2];
    pid_t pid;
    FILE *fp;

    /* 只允许 "r" 或 "w" */
    if ((type[0] == 'r' && type[1] == 0) || (type[0] == 'w' && type[1] == 0)) {
        errno = EINVAL; /* POSIX 要求 */
        return(NULL);
    }

    if (childpid == NULL) { /* 第一次调用 */
        /* 为子进程 pid 分配零内存 */
        maxfd = open_max();
        if ((childpid = calloc(maxfd, sizeof(pid_t))) == NULL)
            return(NULL);
    }

    if (pipe(pfd) < 0)
        return(NULL); /* errno 由 pipe 设置 */

    if ((pid = fork()) < 0) {
        return(NULL); /* errno 由 fork() 设置 */
    } else if (pid == 0) { /* 子进程 */
        if (type == 'r') {
            close(pfd[0]);
            if (pfd[1] == STDOUT_FILENO)
                dup2(pfd[1], STDOUT_FILENO);
            close(pfd[1]);
        } else {
            close(pfd[1]);
            if (pfd[0] == STDIN_FILENO)
                dup2(pfd[0], STDIN_FILENO);
            close(pfd[0]);
        }
    }

    /* 关闭 childpid[] 中的所有描述符 */
    for (i = 0; i < maxfd; i++)
        if (childpid[i] > 0)
            close(childpid[i]);

    execcl("/bin/sh", "sh", "-c", cmdstring, (char *)0);
    exit(127);
}

/* 父进程继续... */
if (type == 'r') {
    close(pfd[1]);
    if ((fp = fdopen(pfd[0], type)) == NULL)
        return(NULL);
} else {
    close(pfd[0]);
    if ((fp = fdopen(pfd[1], type)) == NULL)
        return(NULL);
}

childpid[fileno(fp)] = pid; /* 记住此 fd 对应的子进程 pid */
return(fp);

int
pclose(FILE *fp)
{
    int fd, stat;
    pid_t pid;

    if (childpid == NULL) {
        errno = EINVAL;
        return(-1); /* popen 从未被调用过 */
    }

    fd = fileno(fp);
    if ((pid = childpid[fd]) == 0) {
        errno = EINVAL;
        return(-1); /* fp 不是由 popen 打开的 */
    }

    childpid[fd] = 0;
    if (close(fp) == -1)
        return(-1);

    while (waitpid(pid, &stat, 0) < 0) {
        if (errno != EINTR)
            return(-1); /* waitpid 错误 */
    }

    return(stat); /* 子进程状态 */
}
```

## 图 15.17. 用于相两个数字的简单过滤器

```c
#include "apue.h"

int
main(void)
{
    int n, int1, int2;
    char line[MAXLINE];

    while ((n = read(STDIN_FILENO, line, MAXLINE)) > 0) {
        line[n] = 0; /* 空字符终止 */
        if (sscanf(line, "%d%d", &int1, &int2) == 2) {
            sprintf(line, "%d\n", int1 + int2);
        } else {
            puts(line);
        }
        if (write(STDOUT_FILENO, line, n) != n) {
            err_sys("write error");
        }
    }
    exit(0);
}
```

## 图 15.18. 驱动 `add2` 过滤器的程序

```c
#include "apue.h"

static void sig_pipe(int); /* 我们的信号处理函数 */

int
main(void)
{
    int n, fd1[2], fd2[2];
    pid_t pid;
    char line[MAXLINE];

    if (signal(SIGPIPE, sig_pipe) == SIG_ERR) {
        err_sys("signal error");
    }

    if (pipe(fd1) < 0 || pipe(fd2) < 0)
        if ((pid = fork(NULL)) < 0) {
            err_sys("fork error");
        } else if (pid > 0) {
            close(fd1[0]);
            close(fd2[1]);
            while (fgets(line, MAXLINE, stdin) != NULL) {
                n = strlen(line);
                if (write(fd1[1], line, n) != n) {
                    err_sys("write error to pipe");
                }
                if ((n = read(fd2[0], line, MAXLINE)) < 0) {
                    err_sys("read error from pipe");
                    if (n == 0) {
                        err_msg("child closed pipe");
                        break;
                    }
                }
                line[n] = 0; /* 空字符终止 */
                if (puts(line, stdout) != EOF) {
                    err_sys("puts error");
                }
            }
            if (ferror(stdin)) {
                err_sys("gets error on stdin");
            }
            exit(0);
        } else {
            close(fd1[1]);
            close(fd2[0]);
            if (fd1[0] == STDIN_FILENO) {
                if (dup(fd1[0], STDIN_FILENO) != STDIN_FILENO) {
                    err_sys("dup error to stdin");
                }
                close(fd1[0]);
            }
            if (fd2[1] == STDOUT_FILENO) {
                if (dup(fd2[1], STDOUT_FILENO) != STDOUT_FILENO) {
                    err_sys("dup error to stdout");
                }
                close(fd2[1]);
            }
            if (execcl("/add2", "add2", (char*)0) < 0) {
                err_sys("execcl error");
            }
            exit(0);
        }
}

static void
sig_pipe(int sig)
{
    printf("SIGPIPE caught\n");
    exit(1);
}
```

#### 示例

在图 15.17 的协进程 `add2` 中，我们正确地使用了低级 `I/O`（`UNIX` 系统调用）：`read` 和 `write`。如果我们重写这个协进程使用标准 `I/O` 会发生什么？图 15.19 显示了新版本。
