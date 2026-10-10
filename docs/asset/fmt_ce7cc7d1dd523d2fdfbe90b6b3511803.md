
正如我们在上一个图中看到的，另一个额外好处是包含可执行文件 `grep` 的磁盘文件更小；它不包含共享库代码。对于单个程序来说，这可能看起来并不多，但为（例如）C 库提取公共例程，可以为整个操作系统节省大量的空间。

当然，程序需要的所有内容都需要共享。例如，它所使用的变量在每个进程中都是相互不同的。在这个例子中，我们看到传递给 `grep` 命令的字符串以变量的形式出现在每个进程的数据空间中。这些是独立的，且通常无法被其他进程读取。两个 `grep` 命令中使用的文件也是不同的；进程有自己的一组文件描述符用于访问。

此外，进程拥有自己的栈（`stack`），用于函数中的局部变量以及控制函数调用和返回。它还有自己的环境空间，其中包含了可能为该进程设置的环境变量，正如我们在第 4 章使用 `putenv` 和 `getenv` 时看到的那样。进程还必须维护自己的程序计数器（`program counter`），它记录了执行到了什么种位置，即执行线程。在下一章中，我们将看到当使用线程时，进程可以拥有多个执行线程。

在 Linux 系统和某些 UNIX 系统上，`/proc` 目录中有一组特殊的“文件”。这些文件是特殊的，而不是真正的文件；它们允许你在进程运行时“向内查看”这些进程，就像它们是目录中的文件一样。我们在之前的第 3 章中简要地查看过 `/proc` 文件系统。

最后，像 Linux 一样，UNIX 拥有虚拟内存可以将代码和数据分页到硬盘的一个区域，因此可以管理的进程数量比物理内存能容纳的数量多得多。

## 进程表 (The Process Table)

进程表类似于一种数据结构，描述了当前加载的所有进程，例如它们的 `PID`、状态和命令字符串——这就是 `ps` 命令输出的那种信息。操作系统通过 `PID` 管理进程，并用它们用作进入进程表的索引。该表的大小是限制的，因此系统支持的进程数量也是有限的。早期的 UNIX 系统限制为 256 个进程。更现代的实现放宽了这一限制，可能仅限于用于构建进程表条目的可用内存。

## 查看进程 (Viewing Processes)

`ps` 命令显示我们正在运行的进程、另一个用户正在运行的进程，或者系统上所有的进程。以下是一些示例输出：

```
$ ps -af
UID PID PPID C STIME TTY TIME CMD
root 433 425 0 18:12 tty1 00:00:00 [bash]
rick 445 426 0 18:12 tty2 00:00:00 -bash
rick 456 427 0 18:12 tty3 00:00:00 [bash]
```

## 第 11 章

```
root 467 433 0 18:12 tty 00:00:00 sh /usr/X11R6/bin/start
root 474 467 0 18:12 tty 00:00:00 xinit /etc/X11/xinit
root 478 474 0 18:12 tty 00:00:00 /usr/bin/gnome-session
root 487 1 0 18:12 tty 00:00:00 gnome-promptry --sm-client-id
root 503 1 0 18:12 tty 00:00:00 [enlightenment]
root 506 1 0 18:12 tty 00:00:00 -sm-client-id defaults
root 508 1 0 18:12 tty 00:00:00 xcreensaver -no-splash -timeout
root 510 1 0 18:12 tty 00:00:01 gmc --sm-client-id default0
root 512 1 0 18:12 tty 00:00:01 gnome-help-browser --sm-client-i
root 649 445 0 18:22 tty 00:00:00 su
root 653 669 0 18:24 tty 00:00:00 bash
neil 655 428 1 28:24 tty 00:00:00 terminal
root 715 713 1 18:28 tty 00:00:00 gnome-pty-helper
root 717 716 13 18:28 pts/0 00:00:01 emacs
root 718 653 0 18:22 tty 00:00:00 ps -af
```

这显示了许多进程的信息，以及涉及 Emacs 编辑器的进程。

## 进程与信号

具有高优先级。我们可以使用 `nice` 设置进程的 nice 值，并通过重复使用它来调整值。`nice` 命令将进程的 nice 值增加 10，从而降低其优先级。我们可以使用 `-l` 或 `-f`（长输出选项）来查看活动进程的值。我们感兴趣的值显示在 NI（nice）列中。

| ps | UID | PPID | C | PRI | NI | ADDR | SZ | WCHAN | TTY | TIME | CMD |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 000 S | 500 | 1259 | 1254 | 0 | 75 | - | 0 | 710 wait4 | pts/2 | 00:00:00 | bash |
| 000 S | 500 | 1262 | 1251 | 0 | 75 | - | 0 | 714 wait4 | pts/1 | 00:00:00 | bash |
| 000 S | 500 | 1313 | 1262 | 0 | 75 | - | 0 | 2762 sched | pts/1 | 00:00:00 | emacs |
| 000 S | 500 | 1362 | 1262 | 2 | 80 | - | 0 | 789 sched | pts/1 | 00:00:00 | oclock |
| 000 R | 500 | 1363 | 1262 | 0 | 81 | - | 0 | 782 - | pts/1 | 00:00:00 | ps |

在这里，我们可以带默认的 nice 值运行 oclock 程序（作为进程 1362 运行）。如果我们使用以下命令启动：

```c
$ nice oclock &
```

它将分配一个 +10 的 nice 值。如果我们用命令调整此值：

```
1362: old priority 0, new priority 10
```

时钟程序的运行频率会变降低。我们可以再次通过 `ps` 查看修改后的值：

| F | S | UID | PPID | C | PRI | NI | ADDR | SZ | WCHAN | TTY | TIME | CMD |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 000 S | 500 | 1259 | 1254 | 0 | 75 | - | 0 | 710 wait4 | pts/2 | 00:00:00 | bash |
| 000 S | 500 | 1262 | 1251 | 0 | 75 | - | 0 | 714 wait4 | pts/1 | 00:00:00 | bash |
| 000 S | 500 | 1313 | 1262 | 0 | 75 | - | 0 | 2762 sched | pts/1 | 00:00:00 | emacs |
| 000 S | 500 | 1362 | 1262 | 2 | 80 | 10 | - | 789 sched | pts/1 | 00:00:00 | oclock |
| 000 R | 500 | 1363 | 1262 | 0 | 81 | - | 0 | 782 - | pts/1 | 00:00:00 | ps |

状态行包含 N，表示 nice 值已从默认值发生变化。`ps` 输出的 `PPID` 字段表示父进程 ID，即导致该进程启动的进程 `PID`（或者如果该进程已不再运行，则为 `PID 1`）。

Linux 调度器根据优先级决定哪个进程允许运行。优先级的实现方式各不相同，但高优先级的进程运行得更频繁。在某些情况下，如果高优先级进程已就绪，低优先级进程可能不会运行。

# 启动新进程

我们可以从另一个进程内部触发程序运行，并借用系统库函数创建一个新进程。

```c
#include <stdlib.h>

int system(const char *string);
```

# 第 11 章

`system` 函数将传递给它的字符串作为命令执行，并等待其完成。命令的执行方式就像将以下命令交给了 shell：

```bash
$ sh -c string
```

如果无法启动 shell 来运行命令，`system` 返回 127；如果发生任何其他错误，则返回 -1。否则，`system` 返回命令的退出码。

# 尝试一下—system

我们可以使用 `system` 编写一个程序来为我们运行 `ps`。虽然这本身并不是特别有用，但我们将在后面的示例中看到如何开发这种技术。为了示例简单起见，我们在文中没有检查系统调用是否实际执行成功。

```c
#include <stdlib.h>
#include <stdio.h>

int main()
{
    printf("Running ps with system\n");
    system("ps -ax");
    printf("Done.\n");
    exit(0);
}
```

当我们使用 `system` 编写一个程序来运行 `ps` 时，输出如下：

```text
Running ps with system
[ps 输出内容]
Done.
```

## 进程与信号

当我们运行这个程序 `pexec.c` 时，我们得到了普通的 `ps` 输出，但完全没有看到“Done”消息。注意，输出中并没有对进程 `pexec` 的引用。

```
$ ./pexec
Running ps with exec
PID TTY STAT TIME COMMAND
1 ? S 0:05 init
2 ? S 0:00 [keventd]
...
1262 pts/1 S 0:00 /bin/bash
1273 pts/2 S 0:00 su -
1274 pts/2 S 0:00 -bash
1463 pts/1 S 0:00 clock -transparent -geometry 135x135-10+40
1465 pts/1 S 0:00 emacs Makefile
1514 pts/1 R 0:00 ps -ax
```

## 工作原理

该程序打印它的第一条消息，然后调用 `exec`。`exec` 在 `PATH` 环境变量指定的目录中搜索名为 `ps` 的程序。它会取代我们的 `pexec` 程序执行该程序，就像我们输入了 shell 命令一样：

```
$ ps -ax
```

当 `ps` 完成后，我们得到了一个新的 shell 提示符。我们没有返回 `pexec`，所以第二条消息没有被打印。新进程的 `PID` 与原始进程相同，父 `PID` 和 nice 值也是如的。实际上，发生这一切只是运行中的程序开始从从 `exec` 调用中指定的可执行文件中执行新代码。

对于由 `exec` 函数启动的进程，其参数列表和环境的总大小有一个限制。这由 `ARG_MAX` 决定，在 Linux 系统上为 128 千字节。其他系统可能有更小的限制，这可能会导致问题。POSIX 规范指出 `ARG_MAX` 至少应为 4,096 字节。

`exec` 函数通常不会返回，除非发生错误，在这种情况下，错误变量 `errno` 会返回 -1。

由 `exec` 启动的新进程继承了原始进程的许多特性。打开的文件描述符在新进程中仍保持打开，除非设置了它们的“执行 exec 时关闭标志”（详细信息请参见第 3 章中的 `fcntl` 系统调用）。原始进程中任何打开的目录流将被关闭。

# 复制进程映像

为了让进程同时执行多个功能，我们可以使用线程（在第 12 章中介绍），或者从程序内部创建一个完全独立的进程（如 `init` 所示），而不是像 `exec` 来说那样替换当前的执行线程。

我们可以通过调用 `fork` 来创建一个新进程。此系统调用会复制当前进程，在进程表中创建一个新条目，其许多属性与当前进程相同。新进程与原始进程几乎相同，执行相同的代码，但拥有它自己的数据空间、环境和文件描述符。结合 `exec` 函数使用，`fork` 就是我们创建新进程所需的所有。

```c
#include <sys/types.h>
#include <unistd.h>

pid_t fork(void);
```

如图 11-2 所示，父进程中的 `fork` 调用返回新子进程的 `PID`。新进程继续像原始进程一样执行，不同之处在于子进程中 `fork` 调用返回 0。这允许父进程和子进程都能判断自己是哪个。

如果 `fork` 失败，它返回 -1。这通常是因为父进程可以拥有的子进程数量限制（`CHILD_MAX`），在这种情况下 `errno` 将设置为 `EAGAIN`。如果进程表中没有足够的空间，或者虚拟内存不足，`errno` 变量将被设置为 `ENOMEM`。

一个使用 `fork` 的典型代码段如下：

```c
pid_t new_pid;
new_pid = fork();
switch(new_pid) {
    case -1 :      /* 错误 */
        break;
    case 0 :       /* 我们是子进程 */
        break;
    default :       /* 我们是父进程 */
        break;
}
```

## 进程与信号

让我们来看一个简单的示例 `fork1.c`。

```c
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    pid_t pid;
    char *message;
    int n;

    printf("fork program starting\n");
    pid = fork();
    switch (pid) {
        case -1:
            perror("fork failed");
            exit(1);
        case 0:
            message = "This is the child";
            n = 5;
            break;
        default:
            message = "This is the parent";
            n = 3;
            break;
    }

    for(; n > 0; n--) {
        puts(message);
        sleep(1);
    }
    exit(0);
}
```

该程序作为两个进程运行。创建了一个子进程（出生了？）并打印五次消息。原始进程（父进程）只打印了三次消息。父进程在子进程打印完所有消息之前结束了，因此下一个提示符混杂在输出中。

```
$ ./fork1
fork program starting
This is the parent
This is the child
This is the parent
This is the child
This is the parent
This is the child
$ This is the child
This is the child
```

## 工作原理

当调用 `fork` 时，该程序分裂成独立的进程。父进程通过返回非零值来识别。

# 等待进程

当我们使用 `fork` 启动一个进程时，它会分裂成独立的进程。父进程通过返回非零值来识别。

`wait` 系统调用会让父进程暂停，直到子进程结束。它返回子进程的 `PID`，并通过 `wstatus` 参数传递退出状态。父进程通过 `wait` 来获取子进程结束的状态。

```c
#include <sys/types.h>
#include <wait.h>

pid_t wait(int *wstatus);
```

| 宏 | 定义 |
| :--- | :--- |
| `WIFEXITED(stat_val)` | 进程正常退出 |
| `WEXITSTATUS(stat_val)` | 进程正常退出时的退出码 |
| `WIFSIGNALED(stat_val)` | 进程被信号终止 |
| `WTERMSIG(stat_val)` | 终止进程的信号（且非核心转储） |
| `WSTOPED(stat_val)` | 进程被停止 |
| `WSTOPSIG(stat_val)` | 停止进程的信号 |

# 尝试输出——wait

让我们稍微修改程序，以便我们可以等待并检查子进程的状态。调用 `wait`。
