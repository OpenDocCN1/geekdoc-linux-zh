
- `tc_setraw` 的 Curses 版本是 `raw`。

本书中不再涉及 Curses 的其他内容，因为它不是内核服务。$^{10}$

Curses 是 SUS2 和 SUS3 的一部分，因此你可以在 SUS2 网站 `www.unix-systems.org/version2/online.html` 上在线阅读规范。在大多数系统上，你也可以输入 `man curses` 或 `man ncurses`（Curses 的一个免费版本）。

### 4.9 STREAMS I/O

STREAMS 是一些 UNIX 实现中的一种机制，允许以模块化方式实现字符设备驱动程序。应用程序可以在一定程度上将各种 STREAMS 模块串联起来，以获得所需的驱动程序功能。这在某种程度上类似于 UNIX 过滤器在 shell 层面的工作方式；例如，`who` 命令可能没有排序输出的选项，但如果你想要的话，可以通过管道将其输入到 `sort` 中。

我将在下一节中展示一个基于 STREAMS 的伪终端示例。在那里我将做的是 `open` 一个设备文件以获取伪终端，然后使用 `ioctl` 将两个 STREAMS 模块（`ldterm` 和 `ptem`）“推送”到该模块上，使其表现得像一个终端。与 shell 管道不同，在 shell 管道中你可以从数十种过滤器中选择，并以数百种创造性的方式组合它们；STREAMS 模块通常以配方式（cookbook fashion）方式使用——你推送文档告诉你需要推送的模块，并且就像烹饪一样，如果你随意推送东西，不会得到任何美味的结果。（不应将 STREAMS 与标准 I/O 流概念混淆，后者用于 `fopen`、`fwrite` 等。两者完全没有关系。）

SUS1 和 SUS2 要求具备 STREAMS 功能，但 SUS3 并不要求。将 `_XOPEN_VERSION` 设置为 500（表示它是 SUS2）的 Linux 不提供 STREAMS，因此从某种意义上说它是非符合标准的。

除了我在下一节中使用 STREAMS 进行伪终端以及本书中的其他几处提及之外，我将不会全面介绍 STREAMS。了解更多关于它们的最好方法是参考 SUS 或 Sun 的网站 `www.sun.com`，在那里你可以找到 STREAMS Programming Guide。

> 10. 此外，如果我们包含 Curses，我们就必须包含 X，而那会要我们的命。（在此语境中，“我们”指的是“你和我”。）

### 4.10 伪终端

正常的终端设备驱动程序将进程连接到实际的终端，如图 4.5a 所示，其中终端处的用户正在运行 `vi`。伪终端设备驱动程序对于交互式（从属）进程（`vi`）而言表现得与终端完全一样，但另一端连接的是主进程，而不是实际设备。这允许主进程将输入提供给从属进程，就好像输入来自实际终端一样，并捕获从属进程的输出，就好像输出要去往实际终端一样。从属进程可以像往常一样使用 `tcgetattr`、`tcsetattr` 和其他仅限终端的系统调用，并且它们都将按预期工作。

![](img/41b4c8f6d6a5c349eee321a301703d97_270_0.png)

a) 连接到终端的 tty 驱动程序

b) 连接到进程的 pty 驱动程序

图 4.5 终端驱动程序与伪终端驱动程序。

你可以将伪终端连接到进程的概念类比为通过 shell 重定向其输入和输出，但使用的是某种终端而不是管道。事实上，`vi` 无法使用管道：

```sh
$ vi >tmp
ex/vi: Vi's standard input and output must be a terminal
```

伪终端最常见的用途之一是由 `telnetd` 服务器使用，如图 4.6 所示。它通过网络与 `telnet` 客户端通信，并通过伪终端与 `telnet` 用户执行的操作进行通信。在实践中，`telnet` 会话通常以 shell 开始，就像实际终端会话一样；在

![](img/41b4c8f6d6a5c349eee321a301703d97_271_0.png)

图 4.6 由 `telnet` 服务器（`telnetd`）使用的伪终端。

图中，`vi` 正在运行，因为用户向 shell 输入了 `vi` 命令。事实上，如今使用 `telnet` 或 `xterm` 比使用实际终端更为常见，因为大多数用户通过网络而不是直接拨号连接 UNIX 计算机。（他们可能拨号连接互联网服务提供商（ISP），但这只是为了让他们进入互联网。）我不会展示如何实现 `telnetd` 服务器（参见练习 4.6）；我们只关注图中的伪终端部分。

在伪终端的主侧，主进程获取从属进程写入的内容。在 `vi` 和其他面向屏幕的程序的情况下，这些数据包括转义序列（例如，用于清屏），如我们在 4.8 节中所见。终端驱动程序或伪终端驱动程序都关心这些序列是什么。另一方面，使用 `tcsetattr` 执行的控制操作完全由驱动程序处理，不会到达主进程。因此，在图 4.6 中，`vi` 生成的转义序列一直传输到左侧计算机上运行的 `telnet` 进程。如果它在全屏模式下运行，它可以将其直接发送到实际终端。更常见的是，`telnet` 进程根本不连接到终端驱动程序，而是运行在窗口系统下。在这种情况下，它必须知道如何将这些转义序列转换为窗口系统显示窗口中字符所需的内容。这样的程序被称为终端模拟器。因此，请记住终端模拟器和伪终端是两件非常不同的事情：前者处理转义序列，后者替代终端驱动程序，以便将 I/O 重新路由到主进程。

#### 4.10.1 伪终端库

> 由于本节使用了一些第 5 章中的系统调用（例如 `fork`），你可能希望在阅读完该章之后再阅读本节。

伪终端（从现在起称为“pty”），像所有其他设备一样，由特殊文件表示，其名称因系统而异。不幸的是，将进程连接到 pty 并不像执行以下操作那样简单直接：

```sh
$ vi </dev/pty/01 > /dev/pty/01
```

它更复杂：我们必须获取 pty 的名称，执行一些系统调用来准备它，并将其设置为控制终端。其中一些系统调用由 SUS1（1.5.1 节）及后续标准标准化，但诸如 FreeBSD 等 pre-SUS 系统以完全不同的方式处理此事。更糟糕的是，使用 STREAMS 实现 ptys 的系统需要额外的步骤，并且 SUS2 和 SUS3 之间发生了一些变化。

我将把系统之间的差异封装到一个小型函数库中，每个函数都以 `pty_` 开头。然后，我将使用这个 pty 库来实现一个记录/播放应用程序作为示例。

以下是使用 ptys 的总体方案，分为九个步骤：

1. 打开 pty 的主侧以进行读写。
2. 获取对 pty 的访问权限（如下文所述）。
3. 从主侧的名称或文件描述符获取从侧的名称。暂时不要打开它。
4. 执行 `fork` 系统调用（5.5 节）以创建子进程。
5. 在子进程中，调用 `setsid`（4.3.2 节）使其放弃其控制终端。
6. 在子进程中，打开 pty 的从侧。它将变成新的控制终端。在支持 STREAMS 的系统（例如 Solaris）上，你必须设置 STREAM。在 BSD 系统上，你必须显式使用以下命令使其成为控制终端：

```c
ec_neg1(ioctl(fd, TIOCSCTTY));
```

7. 将子进程的标准输入、输出和错误文件描述符重定向到 pty。
8. 执行 `execvp` 系统调用（第 5.3 节），让子进程运行所需的程序（例如 `vi`）。（“exec”系统调用的六种变体中的任何一种都可以工作；我在示例中使用的是 `execvp`。）
9. 现在，父进程可以使用在第 1 步中获得的文件描述符来读写 pty 的主端。子进程将像往常一样从其标准输入读取，并写入其标准输出和标准错误输出（它不知道自己是在什么上下文中被执行的），而这些文件描述符的行为就好像它们打开到了终端设备上一样。

所有这些管道处理如图 4.5b 所示。

打开 pty 主端（第 1 步）有三种方法：

- A. 在 SUS3 系统上，你只需调用 `posix_openpt`（见下文）。
- B. 在大多数 SUS1 和 SUS2 系统（包括 Solaris 和 Linux）上，你打开克隆文件 `/dev/ptmx`，这将提供一个唯一的 pty，尽管你可能不知道实际的文件名，甚至可能根本不存在。这没关系，因为你只需要打开的文件描述符。
- C. 在基于 BSD 的系统上，有一组特殊文件，其名称形式为 `/dev/ptyXY`，其中 X 和 Y 是数字或字母。你必须尝试所有文件，直到找到一个可以打开的文件。（不是开玩笑！）

我们可以使用 `XOPEN_VERSION` 宏来区分方法 A 和方法 B，并为使用方法 C 的系统定义宏 `MASTER_NAME_SEARCH`。在之前的 9 个步骤中的第 6 步，我们将为需要设置 STREAM 的系统定义宏 `NEED_STREAM_SETUP`，并为需要 `ioctl` 调用的系统定义宏 `NEED_TIOCSCCTTY`。以下是 pt-library 中为 Solaris 和 FreeBSD 设置这些宏的代码；Linux 不需要设置其中任何一个：

```c
#if defined(SOLARIS) /* add to this as necessary */
#define NEED_STREAM_SETUP
#endif

#if defined(FREEBSD) /* add to this as necessary */
#define NEED_TIOCSCCTTY
#endif

#ifdef XOPEN_UNIX
#define MASTER_NAME_SEARCH
#endif
```

如果你的系统尚未被考虑到，你可能需要为此代码进行扩充。

以下是 `posix_openpt` 的原型，仅适用于符合 SUS3 的系统：

```c
posix_openpt—open pty
#include <stdlib.h>
#include <fcntl.h>

int posix_openpt(
    int oflag               /* O_RDWR optionally Ored with O_NOCTTY */
);
/* Returns file descriptor on success or -1 on error (sets errno) */
```

使用标志 `O_NOCTTY` 可以防止主端成为控制终端，以防进程尚未拥有控制终端。（请记住，对于没有控制终端的进程，打开的第一个终端设备将成为其控制终端。）我们通常不希望主端成为控制终端，但我们确实希望从端（第 5 步）正好是这样的，因此我们将使用 `O_NOCTTY` 标志。

现在，继续编写 pt-library 代码，它需要一些不在 `defs.h` 中的头文件包含：

```c
#ifdef _XOPEN_UNIX
#include <string.h>  /* for STREAMS */
#endif
#ifdef NEED_TIOCSCTTY
#include <sys/ttycom.h> /* for TIOCSCTTY */
#endif
```

pt-library 的所有函数都操作于一个 `PTINFO` 结构体，该结构体保存主端和从端的文件描述符及其路径名（如果已知）：

```c
#define PT_MAX_NAME 20

typedef struct {
    int pt_fd_m;             /* master file descriptor */
    int pt_fd_s;             /* slave file descriptor */
    char pt_name_m[PT_MAX_NAME]; /* master file name */
    char pt_name_s[PT_MAX_NAME]; /* slave file name */
} PTINFO;

#define PT_GET_MASTER_FD(p)  ((p)->pt_fd_m)
#define PT_GET_SLAVE_FD(p)   ((p)->pt_fd_s)
```

这两个宏供调用 pt-library 的应用程序使用，因为它们需要文件描述符。

稍后展示的函数 `pt_open_master` 会分配一个 `PTINFO` 结构体并返回指向它的指针，以便与其他库函数一起使用，正如标准 I/O 库使用 `FILE` 结构体一样。内部地，`pt_open_master` 调用 `find_and_open_master` 来实现第 1 步，使用前面概述的三种方法之一：

```c
#if defined(MASTER_NAME_SEARCH)
#define PTY_RANGE \
       "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"

#define PTY_PROTO   "/dev/ptyXY"
#define PTY_X       8
#define PTY_Y       9
#define PTY_MG      5 /* replace with 't' to get slave name */
#endif /* MASTER_NAME_SEARCH */

static bool find_and_open_master(PTINFO *p)
{
#if defined(_XOPEN_UNIX)
#if _XOPEN_VERSION >= 600
    p->pt_name_m[0] = '\0'; /* don't know or need name */
    ec_negl( p->pt_fd_m = posix_openpt(O_RDWR | O_NOCTTY) )
#else
    strcpy(p->pt_name_m, "/dev/ptmx"); /* clone device */
    ec_negl( p->pt_fd_m = open(p->pt_name_m, O_RDWR | O_NOCTTY) )
#endif
#elif defined(MASTER_NAME_SEARCH)
    int i, j;
    char proto[] = PTY_PROTO;

    if (p->pt_fd_m != -1) {
        (void)close(p->pt_fd_m);
        p->pt_fd_m = -1;
    }

    for (i = 0; i < sizeof(PTY_RANGE) - 1; i++) {
        proto[PTY_X] = PTY_RANGE[i];
        proto[PTY_Y] = PTY_RANGE[0];
        if (access(proto, F_OK) == -1) {
            if (errno == ENOENT)
                continue;
            EC_FAIL
        }
        for (j = 0; j < sizeof(PTY_RANGE) - 1; j++) {
            proto[PTY_X] = PTY_RANGE[j];
            if ((p->pt_fd_m = open(proto, O_RDWR)) == -1) {
                if (errno == ENOENT)
                    break;
            }
            else {
                strcpy(p->pt_name_m, proto);
                break;
            }
        }
        if (p->pt_fd_m != -1)
            break;
    }
    if (p->pt_fd_m == -1) {
        errno = EAGAIN;
        EC_FAIL
    }
#else
    errno = ENOSYS;
    EC_FAIL
#endif
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

`find_and_open_master` 中的大部分代码用于那个愚蠢的名称搜索——多达 3844 个名称！为了稍微加快速度，我们使用 `access`（第 3.8.1 节）来测试形式为 `/dev/ptyX0` 的每个名称是否存在，如果不存在，我们就不必理会 `/dev/ptyX1`、`/dev/ptyX2` 以及该系列中的其他 59 个名称，而是直接移动到下一个 `X`。

第 2 步是获取对 pty 的访问权限。在 SUS 系统上，你必须调用 `grantpt` 来获取对从端的访问权限，并在 pty 被锁定时调用 `unlockpt`：

**grantpt**—获取 pty 从端的访问权限

```c
#include <stdlib.h>
int grantpt(
    int fd           /* file descriptor */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

**unlockpt**—解锁 pty

```c
#include <stdlib.h>
int unlockpt(
 int fd /* file descriptor */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

第 3 步是获取从端的名称。在 SUS1 系统上有一个系统调用用于此目的：

**ptsname**—获取 pty 从端的名称

```c
#include <stdlib.h>
char *ptsname(
 int fd /* file descriptor */
);
/* Returns name or NULL on error (errno not defined) */
```
