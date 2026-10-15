
对于父子关系，我们经常遇到以下场景：例如，父进程和子进程都有机会操作。例如，父进程可以在日志文件中记录子进程的 ID，而子进程可能帮助父进程创建一个文件。在示例中，我们要求各自在完成初始操作后通知对方，并等待对方完成后再继续自己的工作。以下代码说明了这一点：

### 示例

图 8.12 中的程序输出两个字符串：一个来自子进程，一个来自父进程。该程序包含竞态条件，因为输出取决于内核运行进程的顺序以及进程运行的时间。

```c
#include "apue.h"
static void charatime(char *);
int
main(void)
{
    pid_t pid;
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {
        charatime("output from child\n");
    } else {
        charatime("output from parent\n");
    }
    exit(0);
}
static void charatime(char *str)
{
    char *ptr;
    int c;
    setbuf(stdout, NULL);
    for (ptr = str; *ptr != '\0'; ptr++) {
        putc(*ptr, stdout);
    }
}
```

这些函数之间的第一个区别是，前四个接受路径（`pathname`）参数，接下来两个接受文件名（`filename`）参数，而最后一个接受文件描述符（`file descriptor`）参数。当指定了文件名参数时：

- 如果文件名包含斜杠，则它被视为路径。
- 否则，在 `PATH` 环境变量指定的目录中搜索可执行文件。

`PATH` 变量包含目录列表，称为路径前缀（`path prefixes`），它们之间用冒号分隔。例如，`name=value` 环境变量字符串：

```
PATH=/usr/bin:/usr/local/bin/:
```

指定了四个搜索目录。最后一个路径前缀指定当前目录。

（零长度的前缀也表示当前目录。可以通过值开头的冒号、连续两个冒号或值结尾的冒号来指定。）

> 出于安全考虑，永远将当前目录包含在搜索路径中。参见 Garfinkel 等人 [2003]。

如果 `execpl` 或 `execvp` 使用路径前缀找到了可执行文件，该函数将假设该文件是一个 shell 脚本，并尝试将文件名作为输入传递 shell 来调用 `/bin/sh`。

使用 `fexecve` 时，我们意识到了寻找正确可执行文件的问题，并依赖调用者来完成。通过使用文件描述符，调用者可以验证文件确实是预期的文件，并在无竞态的情况下执行。否则，具有适当权限的恶意用户可能会在文件定位并验证之后、在调用者执行之前，替换可执行文件（或可执行文件路径的一部分）（回想第 3.3 节中对 `TOCTOU` 错误的讨论）。

下一个区别涉及参数列表的传递（`l` 代表 list，`v` 代表向量 `vector`）。`exec1`、`execpl` 和 `execve` 函数要求将每个命令行参数作为新程序的参数指定为独立的参数。我们用空指针标记参数的结束。对于其他函数（`execv`、`execvp`、`fexecve`），我们必须构建一个指向参数的指针数组，该数组的地址是这三个函数的参数。

在在使用 ISO C 原型之前，显示 `exec1`、`execle` 和 `execvp` 三个函数命令行参数的标准方法是：

```
char *arg0, char *arg1, ..., char *argn, (char * )0
```

这种语法显式显示了最后一个命令-参数后面跟着一个空指针。该空指针由常量 `0` 指定，我们必须将其强制转换为指针；否则，它会被解释为整数。如果整数的大小与 `char *` 的大小不同，则 `exec` 函数的实际参数将错误。

最后的区别是将环境列表传递给新程序。以 `e` 结尾的三个函数（`execle`、`execve` 和 `fexecve`）允许我们传递一个指向环境字符串指针数组的指针。然而，其他四个函数使用调用进程中的 `environ` 变量为新程序创建现有环境。（回想我们在 7.9 节和图 7.8 中对环境字符串的讨论。我们提到如果系统支持 `setenv` 和 `putenv` 这样的函数，我们可以更改当前环境以及任何后续子进程的环境。）通常，进程允许其环境传递给子进程，但在某些情况下，进程想为子指定特定的环境。后者的一个例子是 `login` 程序，它创建一个定义了一些变量的特定环境，并允许通过启动文件在登录时向环境添加变量。在使用 ISO C 原型之前，`exec` 的参数显示为：

```
char *pathname, char *arg0, ... *argn, (char *)0, char *envp[]
```

这种语法专门显示了最后一个参数是指向环境字符串字符指针数组的地址。ISO C 原型没有显示这一点，因为所有命令行参数、空指针和 `envp` 指针都是为了便于记忆。

这七个 `exec` 函数的参数需要记忆。函数名中的字母有些帮助。字母 `p` 表示该函数接受文件名参数并使用 `PATH` 环境变量查找可执行文件。字母 `l` 表示该函数接受参数列表，并与字母 `v` 互斥，`v` 表示它接受一个 `arg[]` 向量。最后，字母 `e` 表示函数接受 `envp[]` 而不是使用当前环境。图 8.14 显示了这七个函数之间的区别。

| Function | pathname | filename | fd | Arg list | argv[] | envp[] |
|---|---|---|---|---|---|---|
| execcl | | | | | | |
| execclp | | | | | | |
| exec | | | | | | |
| execv | | | | | | |
| execvp | | | | | | |
| execve | | | | | | |
| (letter name) | p | f | 1 | v | e |

图 8.14 七个 `exec` 函数之间的区别

每个系统对参数列表和环境列表的总大小都有限制。根据第 2.5.2 节和图 2.8，该限制由 `ARG_MAX` 给出。在 POSIX.1 系统上，该值至少为 4096。当我们使用 shell 的文件名扩展功能来生成文件名列表时，有时会遇到这个限制。在某些系统上，命令：

```
grep getrlimit /usr/share/man/*/
```

可以生成如下形式 shell 错误：

```
Argument list too long
```

从历史上看，旧版 System V 实现的限制是 5,120 字节。旧版 BSD 系统限制为 20,480 字节。当前系统的限制要高。（参见图 2.14 中程序的输出，该输出在图 2.15 中进行了总结。）

为了规避参数大小的限制，我们可以使用 `xargs(1)` 命令拆分长参数列表。要查找系统手册页中所有 `getrlim` 的出现处，我们可以使用：

```
find /usr/share/man -type f -print | xargs grep getrlim
```

然而，如果系统的手册页是压缩的，我们可以尝试：

```
find /usr/share/man -type f -print | xargs zgrep getrlim
```

### 示例

图 8.16 程序演示了 `exec` 函数。

```c
#include "apue.h"
#include <sys/wait.h>

char *env_init[] = { "USER-unknown", "PATH=/tmp", NULL };

int
main(void) {
    pid_t pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定路径，指定环境 */
        if (execle("/home/sar/bin/echoall", "myarg1",
            "MY ARG", (char*)env_init) < 0)
            err_sys("execle error");
    }

    if (wait(pid, NULL, 0) < 0)
        err_sys("wait error");

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) { /* 指定文件名，继承环境 */
        if (execcl("echoall", "echoall", "only 1 arg", (char*)0) < 0)
            err_sys("execcl error");
    }
}
exit(0);
```

> 图 8.16 `exec` 函数示例

我们首先调用 `execle`，它需要一个路径名和一个特定的环境。下一次调用是 `execcl`，它使用文件名并将调用者的环境传递给新程序。`execcl` 调用能够成功的唯一原因是 `/home/sar/bin` 目录是当前路径前缀之一。我们还注意到，路径名的第一个参数（新程序中的 `argv[0]`）是该路径的文件名。这是一种约定；我们可以将 `argv[0]` 设置为任何字符串。`login` 命令在 `argv[0]` 前加一个连字符作为前缀，以表示它是作为登录壳（`login shell`）被调用的。登录 shell 会执行启动配置命令，而而非登录 shell 则不会。

`echoall` 程序在图 8.16 程序中执行了两次，如图 8.17 所示。它是一个简单的程序，用于回显它的命令行参数和整个环境变量列表。

# 8.11 修改用户 ID 和组 ID

```c
#include "apue.h"
int
main(int argc, char *argv[])
{
    int i;
    char **ptr;
    extern char **environ;

    for (i = 0; i < argc; i++) /* 回显所有命令行参数 */
        printf("%s\n", i, argv[i]);

    for (ptr = environ; *ptr; i, ptr++) /* 以及所有环境变量字符串 */
        printf("%s\n", *ptr);

    exit(0);
}
```

图 8.17 回显所有命令行参数和环境变量字符串

当我们执行图 8.16 中的程序时，我们得到：

```bash
$ ./a.out
argv[0]: echoall
argv[1]: myarg1
argv[2]: MY ARG
USER=unknown
PATH=/tmp
$ argv[0]: echoall
argv[1]: only 1 arg
USER=sar
LOGNAME=sar
SHELL=/bin/bash
HOME=/home/sar
```

注意，shell 提示符出现在第二次 `exec` 打印 `argv[0]` 之前。这是因为父进程没有等待该进程结束。

在 UNIX 系统中，权限（例如能够更改系统对当前日期的定义）和访问控制（例如能够读取或写入特定文件）是基于用户 ID 和组 ID 的。当我们的程序需要额外的权限或为了获得当前未被允许访问的资源时，它们需要将用户 ID 或组 ID 更改为具有相应权限或访问权限的 ID。同样，当我们的程序需要降低权限或防止对某些资源的访问时，它们通过将用户 ID 或组 ID 更改为没有该权限或无法访问资源的 ID 来来实现。

### 进程控制

通常情况下，我们在设计应用程序时会尝试使用最小权限模型。根据这一原则，我们的程序应该使用完成任何给定任务所需的最少权限。这减少了由于恶意用户试图欺骗我们的程序以意想不到的方式使用其权限而导致安全漏洞的风险。

我们可以用 `setuid` 函数设置真实用户 ID 和有效用户 ID。同样，我们可以用 `setgid` 函数设置真实组 ID 和有效组 ID。

```c
#include <unistd.h>
int setuid(uid_t uid);
int setgid(gid_t gid);

两者均返回：成功返回 0，错误返回 -1
```

关于谁可以更改 ID 有相应的规则。让我们只考虑用户 ID。（我们对用户 ID 描述的所有内容也适用于组 ID。）

1. 如果进程具有超级用户权限，`setuid` 函数会将真实用户 ID、有效用户 ID 和保存的设置-set-user-ID（`saved set-user-ID`）都设置为 `uid`。
2. 如果进程不具有超级用户权限，但 `uid` 等于真实用户 ID 或保存的设置-set-user-ID 中的任意一个，则 `setuid` 仅将有效用户 ID 设置为 `uid`。真实用户 ID 和保存的设置-set-user-ID 不发生变化。
3. 如果这两个条件都不满足，则 `errno` 被设置为 `EPERM` 并返回 -1。

在这里，我们假设 `POSIX_SAVED_IDS` 为真。如果 `POSIX_SAVED_IDS` 为假，则 `errno` 被设置为 `EPERM` 并返回 -1。

> 保存 ID 是 POSIX 2001 版本的强制性功能。在旧版本的 POSIX 中它们是可选的。

我们可以对内核维护的三个 ID 进行几点陈述：

1. 只有超级用户进程可以更改真实用户 ID。通常，`login(1)` 程序在我们登录时设置真实用户 ID，因为它调用 `setuid` 时会设置三个 ID。
2. 只有当文件设置了设置用户位时，`exec` 才会设置有效用户 ID。这允许 set-user-ID 程序以后再次切换以进行 set-user-ID 操作。
3. 保存-user-ID 由 `exec` 从有效用户 ID 复制。如果设置了设置用户位，保存-user-ID 从真实用户 ID 复制。

图 8.18 总结了这些 ID 的各种更改方式。

| ID | 设置用户位关闭 | 设置用户位开启 | setuid(uid) |
| :--- | :--- | :--- | :--- |
| 真实用户 ID | 不 | 不 | 设置为 uid |
| 有效用户 ID | 不 | 从 uid 设置 | 设置为 uid |
| 保存用户 ID | 从有效 ID 复制 | | 不 |

**图 8.18** 修改 ID 的方式

注意，我们只能通过 8.2 中的函数获取真实用户 ID 和有效用户 ID 的当前值。我们没有可移植的方法来获取保存用户 ID 的当前值。

FreeBSD 和 Linux 3.2.0 提供了 `getuid` 和 `getgid` 函数，分别用于获取设置-user-ID 和保存-group-ID。

# setuid 和 setregid 函数

历史上，BSD 通过 `setuid` 函数交换真实用户 ID 和有效用户 ID。

```c
#include <unistd.h>

int setuid(uid_t ruid, uid_t euid);
setregid(gid_t rgid, gid_t egid);

两者均返回：成功返回 0，错误返回 -1
```

我们可以为任何一个参数提供 -1 值，以表示相应的 ID 应保持不变。

规则很简单：非超级用户可以始终在真实用户 ID 和有效用户 ID 之间切换。这允许 set-user-ID 程序以后再次切换以进行 set-user-ID 操作。当 POSIX.1 引入保存-user-ID 功能时，规则得到了增强，允许非超级用户将其有效用户 ID 设置为其保存用户 ID。

由于 `setuid` 和 `setregid` 都包含在 POSIX.1 的 XSI 选项中。因此，预计 UNIX 系统实现将对它们提供支持。

## seteuid 和 setegid 函数

POSIX.1 包含了 `seteuid` 和 `setegid` 两个函数。这些函数与 `setuid` 和 `setegid` 类似，但只更改有效用户 ID（`effective user ID`）或有效组 ID（`effective group ID`）。

```c
#include <unistd.h>
int seteuid(uid_t uid);
int setegid(gid_t gid);
```

无权限用户可以将有效用户 ID 设置为真实用户 ID（`real user ID`）或保存的安全用户 ID（`saved set-user-ID`）。对于特权用户，只有有效用户 ID 被设置为 `uid`。（这种行为与 `setuid` 函数不同，`setuid` 会改变三个用户 ID。）

图 8.19 总结了我们在这里描述的所有修改三个用户 ID 的函数。

![](img/5dc46842acde5fbcadfab4612cdecbbc_291_0.png)

图 8.19 设置各种用户 ID 的函数总结

## 组 ID

我们在本节中在此为止说的所有内容也以类似的方式适用于组 ID。补充组 ID（`supplementary group IDs`）不受 `setgid`、`setregid` 或 `setegid` 的影响。

### 示例
