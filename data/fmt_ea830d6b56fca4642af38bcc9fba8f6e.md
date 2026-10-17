
```c
#include <unistd.h>

int exec(const char *pathname, const char *arg0,
    ... /* char *argv[] */);

int execv(const char *pathname, const char *argv[]);

int execle(const char *pathname, const char *arg0, ...
    /* (char *argv[], char *const envp[]) */);

int execve(const char *pathname, const char *argv[],
    char *const envp[]);

int execclp(const char *filename, const char *arg0,
    ... /* (char *argv[] */);

int execvp(const char *filename, const char *argv[]);
```

所有函数均：出错时返回 1，成功时不返回。

这些函数的第一个区别是前四个接受 `pathname`（路径）参数，而后两个接受 `filename`（文件名）参数。当指定 `filename` 参数时：

- 如果 `filename` 包含斜杠，则它被视为路径。
- 否则，在 `PATH` 环境变量指定的目录中搜索可执行文件。

`PATH` 变量包含由冒号分隔的目录列表，称为路径前缀。例如，环境字符串 `name=value`：

`PATH=/usr/bin:/usr/local/bin/;`

指定了要搜索的目录。最后一个路径前缀指定当前目录。零长度的前缀也表示当前目录。它可以是值开头的冒号、搜索中的两个冒号或值结尾的冒号。

出于安全考虑，搜索中不包含当前目录。请见 Garfinkel 等人 [2003]。

如果 `execlp` 或 `execv` 使用其中一个路径前缀找到了可执行文件，但如果它不是由链接器生成的机器执行文件，该函数将假设它是一个脚本，并尝试调用 `/bin/sh` 将 `filename` 作为输入。

下一个区别涉及参数列表的传递（`l` 代表 list，`argv` 代表 vector）。`execcl`、`execle` 和 `execve` 函数将每个命令行参数作为单独参数传递给新程序。我们用空指针标记参数的结束。其他三个函数（`exec`、`execv` 和 `execve`）必须构建一个指向参数的指针数组，该数组的地址是调用这三个函数的参数。

在标准 ISO C 之前，原型必须显示三个函数 `excl`、`execle` 和 `execve` 的命令行参数：

```c
int exec(const char *pathname, const char *arg0,
    ... /* (char *argv[] */);
```

### 图 8.14. 函数之间的区别

| 函数 | pathname | filename | Arg list | argv[] | envp[] |
|---|---|---|---|---|---|
| execcl | | | | | |
| execlp | | | | | |
| execle | | | | | |
| execv | | | | | |
| execvp | | | | | |
| execve | | | | | |

**名称中的字母**

每个系统对参数列表和环境列表的总大小都有限制。根据第 2.5 节和图 2.8，该限制由 `ARG_MAX` 给出。在 POSIX.1 系统上，该值至少为 4096 字节。当我们使用 shell 通配符生成文件名列表时有时会遇到这个限制。在某些系统上，例如命令

```bash
grep getlimit /usr/share/man/*
```

可能会产生格式为 `Argument list too long` 的 shell 错误。

从历史上看，旧的 System V 实现限制为 5120 字节。旧的 BSD 系统限制为 20480 字节。当前系统的限制要大得多。（参见图 2.13 中程序的输出，总结在图 2.14 中）。

为了绕过参数列表的大小限制，我们可以使用 `xargs(1)` 来拆分长参数列表。为了在我们系统的手册页中查找 `getlimit` 的所有出现位置，可以使用

```bash
find /usr/share/man -type f -print | xargs grep getlimit
```

如果手册页是压缩的，我们可以尝试

```bash
find /usr/share/man -type f -print | xargs zgrep getlimit
```

我们使用 `find` 命令的 `type -f` 选项限制列表只包含普通文件，因为 `grep` 命令可以在目录中搜索模式，我们希望避免不必要的错误信息。

`process`：

- 进程 ID 和父进程 ID
- 真实用户 ID 和真实组 ID
- 补充组 ID
- 进程组 ID
- 会话 ID
- 控制终端
- 距离闹钟剩余时间
- 当前工作目录
- 根目录
- 文件创建掩码
- 文件锁
- 进程信号掩码
- 待处理信号
- 资源限制
- `tms_stime`, `tms_stime`, `tms_cutime` 和 `tms_cstime` 的值

对打开文件的处理取决于每个描述符的 `close-on-exec` 标志的值。回想图 3.6 以及第 3.14 节中关于 `exec` 中对 `FD_CLOEXEC` 的提到，每个描述符都有一个 `close-on-exec` 标志。如果该标志被设置，则描述符在执行 `exec` 时会被关闭。否则，描述符在执行 `exec` 时将保持打开状态。默认情况下，除非我们使用 `fcntl` 指定了 `close-on-exec` 标志，否则描述符在执行 `exec` 时将保持打开。

`POSIX.1` 明确要求打开的目录流（回想第 4.21 节中的 `opendir` 函数）在执行 `exec` 时关闭。这通常通过 `opendir` 函数调用 `fcntl` 设置对应目录流的描述符的 `close-on-exec` 标志来实现。

注意，真实用户 ID 和真实组 ID 在执行 `exec` 时保持不变，但有效 ID 可能会发生，取决于要执行程序的 `set-user-ID` 和 `set-group-ID` 状态。如果为新进程设置了用户-ID，则有效用户 ID 变为该程序的所有者 ID。否则，有效用户 ID 不改变（它不会设置真实用户 ID）。组 ID 的处理方式相同。

在许多 UNIX 实现中，这六个函数中只有 `execve` 这一个是内核中的系统调用。其他五个只是库函数，它们不可避免地会调用它。我们将像图 8.15 所示说明这六个函数之间的关系。

### 图 8.15. 六个 exec 函数的关系

在这种安排下，库函数 `execp` 和 `execvp` 会搜索 `PATH` 环境变量，寻找包含名为 `filename` 的可执行文件的第一个路径前缀。

### 示例

图 8.16 中的程序演示了 `exec` 和一个特定的环境。下一个调用是 `execclp`，它使用一个文件名并将调用者的环境传递给新程序。

我们首先调用 `execle`，它需要一个路径和函数。`argv(0)` 和 `execcl` 的工作使得 `/home/sar/bin` 目录是当前路径前缀之一。注意，它还将新程序中的第一个参数 `argv(0)` 设置为路径的文件名部分。某些 shell 会将此参数设置为完整路径。我们将看到将 `argv(0)` 设置为任何字符串的唯一原因。`login` 命令在执行 shell 时就是这样做。在执行 shell 之前，`login` 会添加一个连字符 `-` 作为 `argv(0)` 的前缀，以指示 shell 它正被作为登录 shell 调用的。登录 shell 将执行 `start-profile` 命令，而非登录 shell 则不会。

在图 8.16 程序中执行的 `echo` 程序如图 8.17 所示。这是一个简单的程序，用于回显其所有的命令行参数及其整个环境。

当我们执行来自图 8.16 的程序时，我们得到：

```
$ /asout
argv(0): echoall
argv(1): myarg
argv(2): MY ARG2
USER=unknown
PATH=/tmp
$ argv[0]: echoall
argv(1): only 1 arg
USER=sar
LOGNAME=sar
SHELL=/bin/bash
HOME=/home/sar
47 more lines that aren't shown
```

注意，shell 提示符在第二次 `exec` 打印 `argv(0)` 之前出现。这是因为父进程没有等待子进程完成。

### 图 8.16. exec 函数的示例

```c
#include "apue.h"
#include <sys/wait.h>

char *env_init[] = { "USER=unknown", "PATH=/tmp", NULL };

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定文件名，指定环境 */
        if (execcl("/home/user/bin/bin/echoall", "echoall", "myarg",
            "MY ARG2", (char*)0, env_init) < 0) {
            err_sys("execcl error");
        }
    }

    if (waitpid(pid,NULL, 0) < 0) {
        err_sys("wait error");
    }
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定文件名，继承环境 */
        if (execclp("echoall", "echoall", "only 1 arg", (char*)0) < 0) {
            err_sys("execclp error");
        }
    }

    exit(0);
}
```

# 图 8.17. 回显所有命令行参数和所有环境字符串

```c
#include "apue.h"

int
main(int argc, char *argv[])
{
    int i;
    char *ptr;
    extern char **environ;

    for (i = 0; i < argc; i++) { /* 回显所有命令行参数 */
        printf("argv[%d]: %s\n", i, argv[i]);
    }

    for (i = 0; i < argc; i++) { // 注意：原文逻辑似乎有误，此处按字面翻译
        for (ptr = environ; ptr != NULL; ptr++) {
            printf("%s\n", ptr);
        }
    }

    exit(0);
}
```

## 11. 修改用户 ID 和组 ID

在 UNIX 中，诸如能够更改 ID 的权限（例如访问文件）是基于 `set-user-ID` 和 `set-group-ID` 的。当程序执行 `exec` 时，真实用户 ID 和真实组 ID 保持不变。除非程序设置了 `set-user-ID` 和 `set-group-ID` 标志，否则描述符在执行 `exec` 时将保持打开。

在许多 UNIX 实现中，这六个函数中只有 `execve` 这一个是内核中的系统调用。其他五个只是库函数，它们不可避免地会调用它。我们将像 8.15 所示说明这六个函数之间的关系。

### 图 8.15. 六个 exec 函数的关系

在这种安排下，库函数 `execp` 和 `execvp` 会搜索 `PATH` 环境变量，寻找包含名为 `filename` 的可执行文件的第一个路径前缀。

### 示例

图 8.16 中的程序演示了 `exec` 和一个特定的环境。下一个调用是 `execclp`，它使用一个文件名并将调用者的环境传递给新程序。

我们首先调用 `execle`，它需要一个路径和函数。`argv(0)` 和 `execcl` 工作使得 `/home/sar/bin` 目录是当前路径前缀之一。注意，它还将新程序中的第一个参数 `argv(0)` 设置为路径的文件名部分。某些 shell 会将此参数设置为完整路径。我们将看到将 `argv(0)` 设置为任何字符串的唯一原因。`login` 命令在执行 shell 时就是这样做。在执行 shell 之前，`login` 会添加一个连字符 `-` 作为 `argv(0)` 的前缀，以指示 shell 它正被作为登录 shell 调用的。登录 shell 将执行 `start-profile` 命令，而非登录 shell 则不会。

在图 8.16 程序中执行的 `echo` 程序如图 8.17 所示。这是一个简单的程序，用于回显其所有的命令行参数及其整个环境。

当我们执行来自图 8.16 的程序时，我们得到：

```
$ /asout
argv(0): echoall
argv(1): myarg
argv(2): MY ARG2
USER=unknown
PATH=/tmp
$ argv[0]: echoall
argv(1): only 1 arg
USER=sar
LOGNAME=sar
SHELL=/bin/bash
HOME=/home/sar
47 more lines that aren't shown
```

注意，shell 提示符在第二次 `exec` 打印 `argv(0)` 之前出现。这是因为父进程没有等待子进程完成。

### 图 8.16. exec 函数的示例

```c
#include "apue.h"
#include <sys/wait.h>

char *env_init[] = { "USER=unknown", "PATH=/tmp", NULL };

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定文件名，指定环境 */
        if (execcl("/home/user/bin/bin/echoall", "echoall", "myarg1",
            "MY ARG2", (char*)0, env_init) < 0) {
            err_sys("execcl error");
        }
    }

    if (waitpid(pid,NULL, 0) < 0) {
        err_sys("wait error");
    }
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定文件名，继承环境 */
        if (execclp("echoall", "echoall", "only 1 arg", (char*)0) < 0) {
            err_sys("execclp error");
        }
    }

    exit(0);
}
```

# 图 8.17. 回显所有命令行参数和所有环境字符串

```c
#include "apue.h"

int
main(int argc, char *argv[])
{
    int i;
    char *ptr;
    extern char **environ;

    for (i = 0; i < argc; i++) { /* 回显所有命令行参数 */
        printf("argv[%d]: %s\n", i, argv[i]);
    }

    for (i = 0; i < argc; i++) { // 注意：原文逻辑似乎有误，此处按字面翻译
        for (ptr = environ; ptr != NULL; ptr++) {
            printf("%s\n", ptr);
        }
    }

    exit(0);
}
```
