
| `LOCK_NB` | 加锁时不阻塞。可以与其他操作进行位或（OR）组合。 |

成功时返回 `0`；出错时返回 `-1` 并设置 `errno`。目前唯一的错误 `EWOULDBLOCK` 表示文件被锁定且指定了 `LOCK_NB`。

`fcntl()` 可以以多种方式使用，来影响或修改文件描述符的状态：

```c
#include <unistd.h>
#include <fcntl.h>
```

```c
int fcntl (int fd, int cmd);
int fcntl (int fd, int cmd, long arg);
int fcntl (int fd, int cmd, struct flock * lock);
```

`fcntl()` 的行为取决于 `cmd` 的值：

### 表 11.8: fcntl() 命令

| 值 | 含义 |
|---|---|
| `F_DUPFD` | `arg` 将是 `fd` 的拷贝，必要时可以先关闭它（等同于 `dup2()`）。成功时返回新的文件描述符。 |
| `F_GETFD` | 获取 close-on-exec 标志；如果低位为 0，则在 `exec()` 后保持打开；否则关闭。 |
| `F_SETFD` | 将 close-on-exec 标志设置为 `arg` 的最低位。 |
| `F_GETFL` | 读取文件描述符的所有标志。 |
| `F_SETFL` | 将文件描述符的标志设置为 `arg`；仅可以设置 `0_APPEND`, `0_NONBLOCK`, `0_ASYNC`。 |
| 文件锁 | |
| `F_GETLK` | 如果文件未锁定，则将 `flock` 结构的 `l_type` 设置为 `F_UNLCK`。如果文件已锁定，则用值填充整个 `flock` 结构，而不只是 `l_type` 元素。 |
| `F_SETLK` | 如果 `l_type` 为 `F_RDLCK` 或 `F_WRLCK`，则设置锁；否则清除锁（`F_UNLCK`）。如果有人已经持有锁，则立即返回并设置 `errno` 为 `ACCES` 或 `EAGAIN`。 |
| `F_SETLKW` | `F_SETLK` 的阻塞版本。调用进程将睡眠直到锁可用或捕获到信号。 |

此外，命令 `F_GETOWN`, `F_SETOWN`, `F_GETSIG` 和 `F_SETSIG` 可用于控制信号，控制输入或输出是可能的；关于这些许多错误代码的详情，请参阅 `man` 手。

`flock` 结构如下：

```c
struct flock {
    short l_type;     /* 请求的锁类型 */
    short l_whence;   /* SEEK_SET, SEEK_CUR, SEEK_END */
    off_t l_start;    /* 相对于 l_whence 的字节偏移量 */
    off_t l_len;      /* 要锁区域的长度；0 表示文件末尾 EOF */
    pid_t l_pid;      /* 使用 F_GETLK 时，返回锁所有者的 pid */
};
```

`l_type` 可以是 `F_RDLCK`（共享读锁）、`F_WRLCK`（排斥写锁）或 `F_UNLCK`（解锁区域）。

`l_whence`, `l_start` 和 `l_len` 这三组元素的工作方式与 `lseek()` 函数的参数类似。

如果一个文件（或其某个区域）没有锁，则请求读锁或写锁是可以的。如果一个文件有任何读锁，则不能请求写锁。如果一个文件有任何写锁，则不能请求任何类型的锁。强制性锁定通过一种技巧以文件为基础强制执行：设置 `setuid` 位但不设置执行位。一旦这样设置：

- 如果一个进程获取了读锁（使用 `fcntl()`），其他进程可以从该区域读取，但没有一个可以写入。
- 如果一个进程获取了写锁，其他进程既不能从该区域读取也不能写入。请注意，其他进程不需要请求锁就会受到影响。要检查你系统上所有当前的文件锁，可以查看 `/proc/locks`，注意打印的第一个数字是进程 ID。

### 11.6 创建临时文件

通常人们需要生成一个供应用程序使用的临时文件。该文件名的唯一性非常重要，以防止发生冲突。另一个考虑可能是文件名不可轻易预测，这样任何在系统中窥探的人都不会破坏其完整性或安全性。基于进程 ID 生成文件名的古老做法存在此漏洞。Linux 提供了多种函数来实现这一目标。它们在对安全性的严谨程度、对于竞态条件的安全性以及与旧 Unix 类型系统的历史兼容性方面不同：

```c
#include <stdlib.h>

char *template;
mkstemp(char *template);
FILE *tmpfile(void);
```

`mkstemp()` 从 `template` 构建一个唯一文件名，`template` 必须包含 `XXXXX`。此函数还会以 `O_EXCL` 标志打开文件，保证它是唯一的打开者。其返回值是临时文件的文件描述符。要将目录作为模板参数，使用方法完全相同。

| Value | Meaning |
|---|---|
| `EPERM` | 包含 `newpath` 的文件系统不支持符号链接（仅限 `symlink`）。 |
| `EFAULT` | 路径之一是无效内存引用。 |
| `EACCES` | 对 `newpath` 目录没有写权限。 |
| `ENAMETOOL` | `newpath` 目录无效或悬空，或 `oldpath` 为空字符串。 |
| `ENOTDIR` | `newpath` 不是目录。 |
| `ENOMEM` | 可用内存不足。 |
| `EROFS` | `newpath` 在只读文件系统上。 |
| `EXIST` | `newpath` 已存在。 |
| `E` | 符号链接过多。 |
| `ENOSPC` | 设备上没有空间存放目录项。 |
| `EIO` | 发生 I/O 错误。 |
| `EXDEV` | `oldpath` 和 `newpath` 不在同一个文件系统上（仅限 `link()`）。 |
| `EMLINK` | `oldpath` 指向的文件链接过多（仅限 `link()`）。 |

`readlink` 将符号链接路径的内容放入 `buf` 中，并返回放入 `buf` 的字符数。错误返回与 `symlink()` 类似。

`unlink` 删除一个文件。如果名称是符号链接，则删除链接但不删除底层文件。如果名称指向一个正在使用的文件，则在最后一个引用它的文件描述符关闭之前，文件不会被删除。成功时返回 `0`，错误返回 `-1` 并设置 `errno`。错误返回与 `link()` 类似。

## chmod(), chown()

这些函数更改文件系统节点的所有者和权限。

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
```

```c
int chmod (const char *path, mode_t mode);
int chown (const char *path, uid_t owner, gid_t group);
```

`chmod()` 根据 `mode` 更改路径的权限，请参考 `stat()` 函数中讨论的可能值。

`chown()` 更改路径的所有者。超级用户可以更改所有者；任何用户都可以更改其所属的组。对所有者或组 ID 使用 `-1` 则不更改。

还可以使用 `fchmod (int fd, mode_t mode)` 和 `fchown (int fd, uid_t owner, gid_t group)`，它们区别在于使用的是文件描述符而非路径名。`lchown()` 的区别在于它不跟随符号链接。

### 1.8 实验

#### 实验 1：目录

编写一个搜索目录并打印内容的程序。（换句话说，写一个 `ls` 程序。）可选：增强你的代码以八进制显示文件权限、十进制显示用户/组信息以及文件大小；你需要使用 `stat()` 来实现这一点。

#### 实验 2：内存映射

编写一个使用 `mmap` 访问文件的程序。使用内存访问而非 `read/write` 函数来读写文件。（确保不要在你不感兴趣的文件上！）

#### 实验 3：符号链接

编写一个在目录中搜索符号链接的程序。如果找到了，检查链接是否有效或已损坏。

#### 实验 4：文件锁

编写一个检查文件锁的程序。参数可以通过命令行或输入文件指定，说明锁是否应该是排他的、锁应该是读还是写，以及应用于文件的哪个区域（或整个文件）。同时运行多个程序实例以观察发生了什么。

#### 实验 5：临时文件

编写一个使用 `mkstemp()` 和 `tmpfile()` 创建并打开临时文件的程序，并使用 `mktemp()` 处理目录。在程序运行时（你可以使用 `sleep()` 来引入延迟），验证文件已创建并检查它们的名称相对于 `mkstemp()`, `tmpfile()`。你可能想在 `strace` 下运行程序以查看真实情况。

#### 实验 6：使用 inotify 监控目录

使用 `inotify` 监控 `/tmp` 目录的变化。在读取事件时检查返回的掩码以查看发生了哪些事件（当你创建、删除、读取、更改属性等时）。想要获取完整的事件列表。

## 第12 章 进程 - I

我们将学习什么是**进程**以及如何对它们施加限制。我们将理解父进程和子进程之间的关系以及进程组。我们将检查 **proc** 伪文件系统。最后，我们将进程通信的方法。

- 12.1 什么是进程？................................................................................................ . . . . . . . . . . . . . . . . . . . . 89
- 12.2 进程限制.................................................................................................... . . . . . . . . . . . . . . . . . . . 90
- 12.3 进程组....................................................................................................... . . . . . . . . . . . . . . . . 94
- 12.4 proc 文件系统......................................................................................................................... 94
- 12.5 进程间通信方法............................................................................................................... 95
- 12.6 实验......................................................................................................................................... 99

### 12.1 什么是进程？

进程是执行中的一个程序实例。它可能处于不同的状态，如运行、睡眠等。每个进程都有一个 **pid**（进程 ID）、**ppid**（父进程 ID）和一个 **pgid**（进程组 ID）。此外，每个进程都有代码、数据、变量、文件描述符和环境变量。

## CHAPTER 进程 - I

`init` 通常是系统上运行的第一个进程，因此是所有直接从内核启动的后续进程的祖先（在 `ps` 列表中显示为名称 `[] init`）。如果父进程在子进程之前死亡，没有等待其退出代码被称为僵尸（`defunct`）进程。僵尸进程释放了所有资源，仅保留状态。`init` 进程的功能之一是检查其收养的子进程并让它们优雅地退出。因此它被称为僵尸杀手，或更形象地称为僵尸收割者。我们将讨论如何等待进程并解释其状态。进程由调度控制，是完全抢占式的。只有内核有权抢占进程；它们不能相互抢占。以下函数用于获取 `pid`、`ppid` 和 `pgid`：

```c
#include <unistd.h>

pid_t getpid(void);
pid_t getppid(void);
pid_t getpgid(void);
```

由于历史原因，最大的 PID 被限制为 16 位数字，`32768`。

### 12.2 进程限制

每个进程的使用、资源限制由 `rlimit` 结构体数组描述：

```c
struct rlimit {
    unsigned long rlimit_cur;
    unsigned long rlimit_max;
};
```

定义在 `/usr/src/linux/include/resource.h` 中。`rlim_cur` 字段是资源的当前使用限制，`rlim_max` 字段是可以设置的最大值。只有超级用户可以将 `rlim_cur` 更改为大于 `rlim_max` 的值，或者更改 `rlim_max` 字段。这些使用限制大多初始化为 `RLIM_INFINITY`，这意味着没有实施有效限制。

对于 x86，以下资源限制在 `/usr/src/linux/include/resource.h` 中定义：

### 表 12.1：资源限制

| 限制 | 默认 rlim_cur | 默认 rlim_max | 含义 |
| --- | --- | --- | --- |
| `RLIMIT_CPU` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大毫秒 CPU 时间。如果进程超过，将获得 `SIGCPU` 然后不终止。 |
| `RLIMIT_SIZE` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大大小。尝试超过此限制生成 `SIGFSZ` 信号。 |
| `RLIMIT_DATA` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大（堆）数据大小。当内核扩展进程的堆时检查此限制。 |
| `RLIMIT_STACK` | `_STK_LIM=8M` | `RLIM_INFINITY` | 最大栈大小。每当内核扩展进程的用户栈时，都会检查此限制。 |
| `RLIMIT_CORE` | `0` | `RLIM_INFINITY` | 最大核心转储大小。如果设置为 0 则不产生核心转储。 |
| `RLIMIT_RSS` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大驻留大小（进程拥有的页帧数） |
| `RLIMIT_NPROC` | `0` | `0` | 用户可以拥有的最大进程数。两个值在初始化期间重置为最大线程数。 |
| `RLIMIT_NOFILE` | `INR_OPEN=1024` | `INR_OPEN=1024` | 最大打开文件数。 |
| `RLIMIT_MEMLOCK` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大锁定（不可交换）地址空间。 |
| `RLIMIT_AS` | `RLIM_INFINITY` | `RLIM_INFINITY` | 最大地址空间大小。当使用类似 `malloc()` 的函数时检查。 |
| `RLIMIT_LOCKS` | `RLIM_INFINITY` | `RLIM_INFINITY` | 进程持有的文件锁最大数量。 |
| `RLIMIT_SIGPENDING` | `0` | `0` | 可能队列的信号最大数量。 |
| `RLIMIT_MSGQUEUE` | `MQ_BYTES_MAX=819200` | `MQ_BYTES_MAX` | 为 POSIX 消息队列可以分配的最大字节数。 |
| `RLIMIT_NICE` | `0` | `0` | 进程 `nice` 值可以提高的上限。 |
| `RLIMIT_RTRIO` | `0` | `0` | 进程可以拥有的实时优先级上限。 |

从用户空间可以访问以下函数，用以获取和设置使用限制，并报告当前使用总额：

```c
#include <sys/time.h>
#include <sys/resource.h>
```

```c
int getrlimit(int resource, struct rlimit *rlim)
setrlimit(int resource, const struct rlimit *rlim);
```

`getrlimit()` 和 `setrlimit()` 函数用法非常直观，用于获取或设置由 `resource` 参数引用的特定限制；例如，语句

`setrlimit(RLIMIT_CORE, &rlim)`

将最大核心转储大小设置为 8 MB。

人们还可以使用 bash shell 中的 `ulimit` 命令来检查和调整值：

```
$ ulimit -a
core file size (blocks, -c) 0
data seg size (kbytes, -d) unlimited
scheduling priority (-e) 0
file size (blocks, -f) unlimited
pending signals (-i) 38912
max locked memory (kbytes, -l) 64
max memory size (kbytes, -m) unlimited
open files (-n) 1024
pipe size (512 bytes, -p) 8
POSIX message queues (bytes, -p) 819200
real-time priority (-r) 0
stack size (kbytes, -s) 8192
```

## 2. 进程限制

```
cpu time (seconds, -t) unlimited
max user processes (-u) 38912
virtual memory (kbytes, -v) unlimited
file locks (-x) unlimited
```

（注意：`ulimit -p` 提供的管道大小无法更改，且不属于 `RLIMIT` 集合的一部分。）

人们还可以检查 `/proc/[pid]/limits` 来读取特定进程 ID 的值。

通过编辑 `/etc/security/limits.conf` 文件可以设置单独用户和组的值以及系统默认值。
