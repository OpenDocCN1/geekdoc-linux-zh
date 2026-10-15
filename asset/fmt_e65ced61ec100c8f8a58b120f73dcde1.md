
# 实现锁的继承与释放

三条规则支配着记录锁的自动继承和释放。

## 1. 锁与进程和文件相关

锁与进程和文件相关。这有两个含义。第一个是显而易见的：当进程终止时，其所有的锁都会被释放。第二个并不显而易见：当描述符关闭时，该描述符所引用文件的任何锁都会被释放。这意味着如果我们

```c
fd1 = open(pathname, ...);
read_lock(fd1, ...);
fd2 = dup(fd1);
```

关闭 `fd1` 后，对该文件的任何锁都会被释放。`F_GETLK` 命令定义规定，返回给现有锁的信息将阻止我们创建自己的锁。`F_SETLK` 和 `F_SETLK` 命令如果存在现有锁，则总是替换该锁；我们永远不会在自己的锁上阻塞；因此，`F_GETLK` 命令永远不会报告我们自己的锁。

## 2. 锁的继承规则

死锁的发生是：当两个进程都在等待另一个进程已锁定的资源时，就会发生死锁。如果一个控制锁的进程在尝试锁定另一个由不同进程控制的资源时进入睡眠，就存在死锁的可能性。图 14.7 显示了死锁的示例。子进程锁定字节 0，父进程锁定字节 1。然后，子进程尝试锁定另一个被锁定的字节。通过使用第 8.9 节产生的同步结果（`TELL_WAIT`/`WAIT`）使得每个进程都能等待另一个进程解锁。运行图 14.7 中的程序将得到：

```bash
$ .out
parent: got the lock, byte 1
child: got the lock, byte 0
child: write_lock error: Resource already avoided
parent: got the lock, byte 0
```

## 3. 锁的释放规则

我们在图 14.2 中看到，Linux 2.4.2 和 Solaris 9 提供了强制记录锁，但 FreeBSD 5.2.1 和 Mac OS X 10.3 则没有。强制记录锁并不是 Single UNIX 规范的一部分。在 Linux 上，如果你想使用强制锁，需要通过 `mount` 命令的 `-o mand` 选项在文件系统上启用它。

当文件的 `group-get ID` 开启时，强制锁会被启用，但当 `group-exit ID` 关闭时则没有意义。（见图 4.12；由于 `group-get ID` 的存在，SVR3 的开发者选择这种方式来指定对文件的锁定是强制的而非可选的。）

如果一个进程尝试读取或写入一个启强制锁的文件，且该文件的指定部分当前正被另一个进程读锁或写锁，会发生什么？答案取决于操作类型（读或写）、另一个进程持有的锁类型（读锁或写锁）以及该进程的描述符类型（读或写）。图 4.11 显示了这八种可能性。

### 图 14.11. 强制锁对其他进程读写操作的影响

| 其他进程持有的现有锁类型 | 阻塞，尝试读取 | 非阻塞，尝试写入 |
| :--- | :--- | :--- |
| 读锁 | OK，阻塞 | OK, `EAGAIN` |
| 写锁 | 阻塞，阻塞 | `EAGAIN`, `EAGAIN` |

除了图 14.11 中的 `read` 和 `write` 函数外，`open` 函数也会受到另一个进程持有的强制记录锁的影响。通常情况下，即使打开的文件启用了强制记录锁，`open` 也会成功。读锁或写锁遵循图 14.11 中列出的规则。如果 `open` 调用中的标志指定了 `O_TRUNC` 或 `O_CREAT`，则 `open` 将返回 `EAGAIN` 错误，无论是否指定了 `O_NONBLOCK`。

它仅将 `O_CREAT` 视为错误类。Linux 允许在打开带有强制锁的文件时指定 `O_CREAT`。为 `O_TRUNC` 生成错误是有意义的，因为如果文件被另一个进程读锁或写锁，则无法创建该文件。为 `O_CREAT` 生成错误则意义不大；这种锁会在文件不存在时创建文件，但必须由另一个进程通过记录锁来指定。

这种对锁的处理可能会导致出意想不到的结果。在开发本节的练习时，运行了一个测试程序，该程序打开了一个文件（指定了强制锁），在某个条目上建立了记录锁，然后睡眠了一会儿。（回想图 14.11，读锁本应阻止其他进程写入该文件。）在此期间，在不同的 UNIX 系统中指定了以下操作：

- 使用 `ed` 编辑器编辑同一个文件，并将结果写回磁盘！强制锁完全没有起作用。UNIX 系统版本中的系统调用跟踪功能显示了这种行为，即 `ed` 将新内容写入临时文件，然后将原始文件重命名为该文件。强制锁函数对此这种发生的情况产生影响。
- 在 Solaris 下，进程的系统调用跟踪通过 `truss` 获得；FreeBSD 和 Mac OS 使用 `trace(1)` 和 `dump(1)` 命令。Linux 提供了 `trace` 命令来跟踪系统调用。
- `vi` 编辑器无法编辑该文件。它可以读取文件内容，但每当我们尝试向文件写入新数据时，都会返回 `EAGAIN`。如果我们尝试向文件追加新数据，这就是我们预期的结果。
- 使用 Korn shell 的 `>` 和 `>>` 运算符覆盖或追加文件会导致“无法创建（cannot create）”错误。
- 在 Bourne shell 中使用两个运算符时，`>` 会导致错误，但 `>>` 运算符会一直持续到执行强制锁为止，然后进行处理。在追加运算符的处理中，是内核使用 `O_CREAT` 和 `O_APPEND` 打开文件，而我们提到过 `O_CREAT` 会产生错误。如果文件已经存在，Bourne shell 不会指定 `O_CREAT`，因此 `open` 成功但 `write` 阻塞。

结果取决于你所使用的操作系统版本。本练习的结论是：要警惕强制锁。如果它存在，就可以被绕过。

强制锁还可能被恶意用户用于对公共可读的文件持有锁。这可以防止任何人向该文件写入。（当然，这种情况的发生要求文件必须启用强制锁，这可能需要用户能够更改文件的权限位。）考虑一个可读且启用了强制锁的数据库。如果恶意用户一直持有整个文件的锁，则其他进程将无法写入该文件。

### 示例

图 14.12 中的程序确定系统是否支持强制锁。

该程序创建一个文件并对其启用强制锁。然后程序分分为父进程和子进程，父进程获取该文件的写锁。第一个子进程将其描述符设置为非阻塞，然后尝试获取该文件的读锁，预期会产生错误。如果没有报错，我们将看到系统返回的是 `EACCES` 还是 `EAGAIN`。接下来，子进程刷新文件并尝试从其读取。如果提供了强制锁，读取应该返回 `EACCES` 或 `EAGAIN`（因为描述符是非阻塞的）。否则，读取将返回它所获得的数据。在下面运行此程序：

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/file.h>
#include <sys/stat.h>
#include <errno.h>
#include <string.h>

// Figure 14.12. Determine whether mandatory locking is supported by a system
int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "usage: %s <filename>\n", argv[0]);
        exit(1);
    }

    // 创建文件并对其启用强制锁
    int fd = open(argv[1], O_RDWR | O_CREAT | O_TRUNC, 0666);
    if (fd == -1) {
        perror("open");
        exit(1);
    }

    struct flock fl;
    // 获取写锁
    fl.l_type = F_WRLCK;
    fl.l_whence = SEEK_SET;
    fl.l_start = 0;
    fl.l_len = 0;
    if (fcntl(fd, F_SETLK, &fl) == -1) {
        perror("fcntl");
        exit(1);
    }

    pid_t pid = fork();
    if (pid == -1) {
        perror("fork");
        exit(1);
    }

    if (pid > 0) { // 父进程
        // 释放写锁
        fl.l_type = F_UNLCK;
        fl.l_whence = SEEK_SET;
        fl.l_start = 0;
        fl.l_len = 0;
        if (fcntl(fd, F_SETLK, &fl) == -1) {
            perror("fcntl");
        } else {
            printf("mandatory locking is supported\n");
        }

        sleep(5);
        wait(pid, NULL, 0);
        close(fd);
    } else { // 子进程
        int cfd = open(argv[1], O_RDONLY);
        if (cfd == -1) {
            perror("open");
            exit(1);
        }

        // 尝试获取读锁
        fl.l_type = F_RDLCK;
        fl.l_whence = SEEK_SET;
        fl.l_start = 0;
        fl.l_len = 0;
        if (fcntl(cfd, F_SETLK, &fl) == -1) {
            if (errno == EAGAIN || errno == EACCES) {
                printf("mandatory locking is supported\n");
            } else {
                perror("fcntl");
            }
        } else {
            printf("mandatory locking is not supported\n");
        }

        char buf[100];
        ssize_t n = read(cfd, buf, sizeof(buf)-1);
        if (n == -1) {
            perror("read");
        } else {
            buf[n] = '\0';
            printf("read: %s\n", buf);
        }
        close(cfd);
        exit(0);
    }
    return 0;
}
```

## 14.4. STREAMS

STREAMS 机制由 System V 提供，作为通信驱动程序与内核交互的通用方法。我们需要讨论 STREAMS 以理解 System V 中的终端接口、第 14.5.2 节中用于 I/O 复用的 `poll` 函数，以及第 17.2 和 17.1 节中基于 STREAMS 的管道和命名管道的实现。

不要将此处的 `streams` 一词用法与我们之前在 5.2 节标准 I/O 库中的用法混淆。STREAMS 机制由 Dennis Ritchie (1984) 开发，用于清理传统的字符 I/O (`c-lists`) 并适应网络协议。STREAMS 机制后来被添加到 SVR3 中，对其进行了一定的增强并使用了大写名称。SVR4 提供了对 STREAMS 的完整支持（即基于 STREAMS 的 I/O 系统）。SVR4 的实现描述在 AT&T 964 (1993) 书中，该书中同时讨论了用户级 STREAMS 编程和内核级 STREAMS 编程。

STREAMS 是单 Unix 规范（包含在 XSI STREAMS 选项组中）中的一个可选功能。在本文讨论的平台中，只有 Solaris 提供 STREAMS 的原生支持。Linux 提供了 STREAMS 子系统，但你需要自行添加它。它默认并不包含在其中。

流（stream）在用户进程和设备驱动程序之间提供了一条全双工路径。流不需要直接与硬件设备通信；流也可以与伪设备驱动程序一起使用。图 14.13 显示了所谓简单流的最佳视图。

### 图 14.13. 简单流

![](img/902515e97eef28cac8083866e00a6f4c_632_0.png)

在流头（stream head）之下，我们可以向流中推入（push）处理模块。这是通过使用 `ioctl` 命令完成的。图 14.14 显示了一个带有单个处理模块的流。我们还用两个箭头显示了这些方框之间的连接，以强调流的全双工特性，并突出一个方向的处理与另一个方向的处理是分开的。

### 图 14.14. 带有处理模块的流

![](img/902515e97eef28cac8083866e00a6f4c_633_0.png)

向流中推入任意数量的处理模块。我们使用“推”（push）一词，是因为每个新模块都位于流头之下，推动任何之前推入的模块。（这类似于后进先出的栈。）在图 14.14 中，我们标记了流的下游（downstream）和上游（upstream）侧。我们写入流的数据被向下游发送。来自设备驱动的数据被向上游发送。

STREAMS 与驱动程序的相似之处在于，它们作为内核的一部分执行，并且通常在构建内核时链接到内核中。如果系统支持动态加载内核模块（如 Linux 和 Solaris），那么我们可以获取一个尚未链接到内核的 STREAM 模块，并尝试将其推入流中；然而，无法保证模块和驱动程序的任意组合能够协同工作。

我们使用第 3 章中的函数 `open`、`close`、`read`、`write` 和 `ioctl` 来访问流。此外，SVR4 内核新增了三个函数以支持 STREAMS（`getmsg`、`putmsg` 和 `poll`），SVR4 又增加了另外两个（`getmsg` 和 `putmsg`）来处理流中具有不同优先级边界的消息。

我们为流打开的路径通常具有设备名称。仅通过 `ls -l` 使用设备名，我们无法判断该设备是否为 STREAM。所有的 STREAMS 设备都是字符文件。

尽管某些 STREAMS 实现意味着我们可以编写处理模块并随意的地将其推入流中，但编写这些模块需要与编写驱动程序相同的技能和细心。通常，特殊的应用程序或函数会推入和弹出 STREAMS。
