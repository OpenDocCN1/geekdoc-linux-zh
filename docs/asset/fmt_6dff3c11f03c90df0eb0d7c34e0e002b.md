
由于命令字符串被传递给 `shell`，因此你对可以使用的功能具有相当大的灵活性。这包括使用带有通配符文件名的命令行，以及 `shell` 输入和输出重定向操作符。此外，你还可以使用管道符号 `|` 为指向其他进程创建额外的管道。

## 警告

如果你编写的程序使用了 `popen(3)` 函数且必须具有对其他 `UNIX` 操作系统的可移植性，请记住 `shell` 的局限性。某些 `UNIX` 平台上使用了不同的 `shell` 程序，其功能也不相同。

当前进程的环境对于通过 `popen(3)` 调用来启动你命令的 `shell` 至关重要。这意味着你期望调用的任何命令都会在通常 `PATH` 目录中搜索。

## 从管道读取

列表 18.1 中的短程序展示了一个打开到 `ps(1)` 命令管道的简单程序。管道打开后，程序将从管道中读取数据直到遇到文件结束符。所有读取的数据都将显示在标准输出上。

### 列表 18.1. `popen.c`-`popen(3)` 演示与读取 `ps(1)` 输出

```c
/* popen.c */
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv) { /* 输入缓冲区 */
    char buf[256];
    FILE *p;

    /* 打开指向 ps(1) 命令的只读管道： */
    p = popen("ps -l","r");

    if (!p) {
        perror("popen(3)");
    }
    return 1;
}
```

程序首先在第 14 行打开一个指向 `ps -l` 命令的读管道。一旦管道成功打开，程序会在第 24 行和第 25 行的循环中读取每行文本，直到到达文件结束。然后调用 `pclose(3)` 函数来正确关闭管道（第 27 行）。

提供了以下 `FreeBSD` 编译和运行会话：

```bash
$ make popen
cc -Wall popen.c
$ ./popen
UID PID PPID PRI NI VSZ RSS WCHAN STAT TT TIME COMMAND
1001 7590 1 0 10 0 596 344 wait Is p0 0:00.05 - sh (sh)
1001 7593 1 1 10 0 596 344 wait Ss p1 0:00.22 - sh (sh)
1001 7813 1 -6 0 780 408 piperd S p1 0:00.01 ./popen
1001 7813 1 10 0 496 332 S+ p1 0:00.00 sh -c ps -l
$
```

输出的最后三行显示了涉及的进程（之前的是正在使用的 `xterm(1)` 会话）。进程 7813 是执行程序 `./popen` 的进程。然而，注意 `popen(3)` 如何创建了两个新进程。

- 进程 7814 是启动以执行命令的 `shell`。
- 进程 7815 是命令本身（`ps(1)` 命令）。

尽管你看不见使用的单引号，但你可以看到 `popen(3)` 进程如何通过 `shell` 进程 7814 创建了命令进程。如果你能看到单引号，你就会看到：

`sh -c 'ps -l'`

这演示了 `popen(3)` 函数通过调用 `pipe(2)`、`fork(2)` 和 `execve(2)` 为你执行。`fork(2)` 和 `execve(2)` 函数将在第 19 章中讨论。

## 注意

`ps(1)` 命令的命令行选项在不同的 `UNIX` 平台上不同。本章提出的示例假设使用的是 `FreeBSD` 3.4 版本。

## 向管道写入

当当前进程向管道写入数据时，管道另一端的进程正在从其标准输入读取数据。为了说明这一过程，请看列表 18.2 中的示例程序。

### 列表 18.2. `pmail.c`–一个向 `popen(3)` 管道写入的程序

```c
/* pmail.c */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pwd.h>
#include <sys/types.h>

int main(int argc, char **argv) {
    struct passwd *pwd;
    FILE *p;

    /* 获取当前用户的信息 */
    pwd = getpwuid(getuid());
    if (!pwd) {
        perror("getpwuid(2)");
        return 1;
    }

    /* 打开指向 mail 命令的写管道 */
    p = popen("mail -s \"Test\" " , "w");
    if (!p) {
        perror("popen(3)");
        return 1;
    }

    /* 写入邮件内容 */
    fprintf(p, "To: %s\n", pwd->pw_name);
    fprintf(p, "From: %s\n", pwd->pw_name);
    fprintf(p, "\n");
    fprintf(p, "This is a test message sent via popen.\n");

    /* 关闭管道 */
    if (pclose(p) == -1) {
        perror("pclose(3)");
        return 1;
    }

    return 0;
}
```

从管道中读取。这会导致 `UNIX` 内核在尝试写入管道的进程中抛出 `SIGPIPE` 信号。这告诉写入者管道已断开。

对于这一目的，`SIGPIPE` 信号并不总是如所愿的。你可以选择忽略 `SIGPIPE` 信号，并在当此情况发生时允许 `write(2)` 函数返回错误（错误代码 `EPIPE`）。

例如，你可以按照如下方式使用列表 18.2：

```c
/* 示例片段 */
#include <signal.h>

signal(SIGPIPE, SIG_IGN);
```
