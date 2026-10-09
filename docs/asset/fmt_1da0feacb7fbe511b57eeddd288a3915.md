
`ioctl` 函数包含在单 Unix 规范（Single UNIX Specification）中，作为处理 STREAMS 设备的扩展 [Rago 1993]，但在 SSU4 中被移至废弃状态。IX 系统实现使用 `ioctl` 处理许多杂杂设备操作。某些实现甚至将其扩展到了普通函数。

我们展示的原型对应于 POSIX1。FreeBSD 8.0 和 Mac OS X 10.6.8 声明为 `unsigned long`。这个细节并不重要，因为第二个参数始终来自头文件的定义名称。

对于 ISO C 原型，使用省略号 `...` 表示剩余参数。然而，通常只有一个参数，且它通常是一个指向变量或结构的指针。

在这个原型中，我们展示了函数本身所需的头文件。通常还需要额外的特定于设备的头文件。例如，终端 I/O 的 `ioctl` 命令（除了 POSIX.1 指定的基本操作外）都要求包含 `<term.h>` 头文件。

每个设备驱动程序都可以定义自己的一套 `ioctl` 命令。系统为不同类设备提供了一些通用的 `ioctl` 命令。FreeBSD 中提供的这些通用 `ioctl` 命令的某些类别示例总结在图 3.15 中。

| 类别 | 常量名称 | 头文件 | ioctls 数量 |
|---|---|---|---|
| 磁盘标签 | `DIOXXX` | `<sys/dislabel.h>` | 4 |
| 文件 I/O | `FIOXXX` | `<sys/filio.h>` | 14 |
| 映射标记 I/O | `MTIOXXX` | `<sys/mtio.h>` | 11 |
| Socket I/O | `SIOXXX` | `<sys/sockio.h>` | 73 |
| 终端 I/O | `TXXX` | `<sys/ttycom.h>` | 43 |

图 3.15 常见的 FreeBSD `ioctl` 选项

磁带标记操作允许我们在磁带上写入文件结束标记、倒带磁带、跳过指定数量的文件或记录等。这些操作中没有无法容易地用本章中的函数（`read`, `write`, `lseek` 等）表示，因此处理这些设备最简单的方法一直是通过 `ioctl` 访问它们的操作。

我们在第 18.12 节中使用 `ioctl` 来查找并设置终端窗口的大小，并在第 19.7 节中在访问伪终端的高级功能时使用它。

## 3.16 /dev/fd

较新的系统提供了一个目录 `/dev/fd`，其条目是命名为 `0`、`1` 等的文件。打开文件 `/dev/fd` 等同于复制描述符 $n$（假设该描述符是打开的）。`/dev/fd` 功能是由 Tom 在 Research UNIX 系统第 8 版开发的。书中描述的所有系统都支持它：FreeBSD 8.0、Linux 3.2、Mac OS X 10.6.8 和 Solaris 10。它不是 POSIX.1 的一部分。

在函数

```c
fd = open("/dev/fd", mode);
```

中，大多数系统忽略指定的模式，而其他系统则要求该模式是引用文件（如果是标准输入）原始打开时使用的模式的子集。由于之前的 `open` 等于

```c
fd = dup(0);
```

描述符 `0` 和 `fd` 共享同一个文件表项（图 3.9）。例如，如果描述符 `0` 是只读的，我们只能在 `fd` 上进行读取。如果系统忽略 `open` 并且

```c
fd = open("/dev/fd", O_RDWR);
```

（注：此处原文似乎存在逻辑重复或片段错误，已根据语意尽量翻译）

（注：由于原文在描述 `/dev/fd` 处的文本存在多处逻辑重复和断句，上述翻译已尽可能保留了原文结构并确保术语准确。）

### 3.6 问题

如果你用追加标志打开一个文件进行读写，你还能使用 `lseek` 从文件的任何地方读取内容吗？你可以使用 `lseek` 替换文件中已的数据吗？请编写一个程序验证这一点。

# 4 文件与目录

## 4.1 引言

在上一章中，我们涵盖了执行 I/O 的基本函数。讨论集中在普通文件的 I/O——打开文件、读取或写入文件。我们将查看文件系统的额外功能和文件的属性。我们将从 `stat` 函数开始，遍历 `stat` 结构的每个成员，查看文件的所有属性。在此过程中，我们还会描述修改这些属性的每个函数：更改所有者、更改权限等。我们还将更详细地查看 UNIX 文件系统的结构和符号链接。我们以操作目录的函数结束本章，并开发一个层层遍历目录层次的函数。

## 4.2 stat, fstat, fstatat, 和 lstat 函数

本章的讨论集中在四个 `stat` 函数以及它们返回的信息。

```c
#include <sys/stat.h>

int stat(const char *restrict pathname, struct stat *restrict buf);
int fstat(int fd, struct stat *buf);
int lstat(const char *restrict pathname, struct stat *restrict buf);
int fstatat(int fd, const char *restrict pathname, struct stat *restrict buf, int flag);
```

所有四个函数返回：成功为 `0`，错误时返回 `-1`。

给定一个路径，`stat` 函数返回一个关于该命名文件的信息结构。`fstat` 函数获取已在描述符 `fd` 上打开的文件信息。`lstat` 函数与 `stat` 类似，但当命名文件是符号链接时，`lstat` 返回关于符号链接的信息，而不是符号链接所引的文件。（在 4.22 节中遍历目录层次结构时，我们需要用到 `lstat`。）

`fstat` 函数提供了一种返回相对于 `fd` 参数表示的打开目录的相对路径的方法。`flag` 参数控制是否跟随符号链接；当设置 `AT_SYMLINK_NOFOLLOW` 标志时，`fstat` 不跟随符号链接，而是返回链接本身的信息。否则，默认跟随符号链接，返回其所指向的文件信息。如果 `fd` 参数值为 `AT_FDCWD` 且 `pathname` 参数是相对路径，则 `fstat` 相对于当前目录评估该路径。如果 `pathname` 是绝对路径，则忽略 `fd` 参数。在这两种情况下，`fstat` 的行为类似于 `stat` 或 `lstat`，取决于 `flag` 的值。

`buf` 参数指向我们必须提供的结构指针。该结构的定义在不同实现之间可能不同，但可能如下：

```c
struct stat {
    mode_t  st_mode;      /* 文件类型 & 模式（权限） */
    ino_t   st_ino;       /* 节点号（序列号） */
    dev_t   st_dev;       /* 设备号（文件系统） */
    dev_t   st_rdev;      /* 特殊文件的设备号 */
    nlink_t st_nlink;     /* 链接数 */
    uid_t   st_uid;       /* 所有者用户 ID */
    gid_t   st_gid;       /* 所有者组 ID */
    off_t   st_size;      /* 普通文件的字节（字节） */
    struct timespec st_atim; /* 最后访问时间 */
    struct timespec st_mtim; /* 最后修改时间 */
    struct timespec st_ctim; /* 最后文件状态改变时间 */
    blksize_t st_blksize;  /* 最佳 I/O 块大小 */
    blkcnt_t st_blocks;   /* 分配的磁盘块数 */
};
```

`st_blksize` 和 `st_blocks` 字段并不是 POSIX 要求。它们在单 Unix 规范中被定义为 XSI。

`timespec` 结构定义了秒和纳秒的时间。它包含以下字段：

```c
time_t tv_sec;
long tv_nsec;
```

在 2008 版标准之前，这些字段命名为 `st_at`、`st_mtime` 和 `st_ctime`，类型为 `time_t`（以秒表示）。`timespec` 结构实现了更高分辨率的时间戳。为了兼容性，可以通过 `tv_sec` 成员来定义旧名称。例如，`st_atim` 可以定义为 `st_atim.tv_sec`。

![](img/5dc46842acde5fbcadfab4612cdecbbc_127_0.png)

注意，`stat` 结构的大多数成员由基本数据类型指定（见 2.8 节）。我们将遍历该结构的每个成员以检查文件的属性。`stat` 函数最大的用户可能是 `ls -1` 命令，用于学习一个关于文件的所有信息。

## 4.3 文件类型

到目前，我们讨论了两种类型的文件：普通文件和目录。UNIX 系统上的大多数文件都是普通文件或目录，但还有其他类型的文件。

- 普通文件：最常见的文件类型，包含数据。
- 目录文件：包含其他文件名称的文件。
- 特殊文件：提供对设备访问的文件。
- 字符特殊文件：用于面向字符的设备。
- FIFO：先进先出管道，用于通信。
- Socket（套接字）：用于网络通信。
- 符号链接：指向另一个文件的文件。

`stat` 函数最大的用户可能是 `ls -1` 命令，用于获取关于文件的所有信息。

文件的类型编码在 `stat` 结构的 `st_mode` 成员中。

| 宏 | 文件类型 |
| --- | --- |
| `S_ISREG()` | 普通文件 |
| `S_ISDIR()` | 目录文件 |
| `S_ISCHR()` | 字符特殊文件 |
| `S_ISBLK()` | 块特殊文件 |
| `S_ISFIFO()` | 管道或 FIFO |
| `S_ISLNK()` | 符号链接 |
| `S_ISSOCK()` | socket |

图 4.1 `<sys/stat.h>` 中的文件类型

POSIX.1 实现将进程间通信（IPC）对象（如消息队列和信号量）表示为文件。图 4.2 所示的宏允许根据 `stat` 结构确定 IPC 对象的类型。这些宏与 4.1 节中的宏不同，这些宏的不同之处在于它们的参数是指向 `stat` 结构的指针。

| 宏 | 对象类型 |
| --- | --- |
| `S_TYPEMSG()` | 消息队列 |
| `S_TYPESEM()` | 信号量 |
| `S_TYPESHM()` | 共享内存对象 |

图 4.2 `<sys/stat.h>` 中的 IPC 类型

消息队列、信号量和共享内存对象在第 15 章中讨论。然而，本书中讨论的各种 Unix 系统实现都没有将这些对象表示为文件。

图 4.3 中的程序打印每个命令行参数的文件类型。

```c
#include "apue.h"

int main(int argc, char *argv[])
{
    int i;
    struct stat buf;
    char *ptr;

    for (i = 1; i < argc; i++) {
        printf("%s: ", argv[i]);
        if (stat(argv[i], &buf) < 0) {
            err_ret("stat error");
            continue;
        }
        if (S_ISREG(buf.st_mode))
            ptr = "regular";
        else if (S_ISDIR(buf.st_mode))
            ptr = "directory";
        else if (S_ISCHR(buf.st_mode))
            ptr = "character special";
        else if (S_ISBLK(buf.st_mode))
            ptr = "block special";
        else if (S_ISFIFO(buf.st_mode))
            ptr = "fifo";
        else if (S_ISLNK(buf.st_mode))
            ptr = "symbolic link";
        else if (S_ISSOCK(buf.st_mode))
            ptr = "socket";
        else
            ptr = "unknown mode";
        printf("%s\n", ptr);
    }
    exit(0);
}
```

图 4.3 为每个命令行参数打印文件类型

图 4.3 的示例输出

```
$ ./aout /etc/passwd /etc /dev/log /dev/tty /var/lib/oprofile/opd_pipe /dev/sr0 /dev/cdrom
/etc/passwd: regular
/etc: directory
/dev/log: socket
/dev/tty: character special
/var/lib/oprofile/opd_pipe: fifo
/dev/sr0: block special
/dev/cdrom: symbolic link
```

在历史上，我们必须将 `st_mode` 值与 `S_ISXX` 宏进行逻辑与（AND）操作，然后将结果与名为 `S_IFxx` 的常量进行比较。大多数系统将此掩码和剩余常量定义在 `<sys/stat.h>` 文件中。如果我们检查这个文件会发现 `S_ISDIR` 宏的操作如下：

```c
#define S_ISDIR(mode)    ((mode) & S_IFMT) == S_IFDIR
```

我们已经说过普通文件占主导，但查看给定系统中各种类型文件的百分比是非常有趣的。图 4.4 显示了作为单用户工作站的 Linux 系统的计数和百分比。这些数据来自第 4.22 节。

| 文件类型 | 计数 | 百分比 |
| --- | --- | --- |
| 普通文件 | 415,803 | 79.77 % |
| 目录 | 62,197 | 11.93 % |
| 符号链接 | 40,018 | 8.25 % |
| 特殊字符设备 | 155 | 0.03 % |
| 特殊块设备 | 47 | 0.01 % |
| 套接字 | 45 | 0.01 % |
| FIFO | 0 | 0.00 % |

图 4.4 不同文件类型的计数和百分比

## 4.4 设置用户 ID (Set-User-ID) 和组 ID (Group-ID)

每个进程都关联有六个或更多 ID。这些如图 4.5 所示。

| 真实用户 ID | 我们究竟是谁 |
| 真实组 ID | |
| 有效用户 ID | |
| 有效组 ID | 用于文件访问权限检查 |
| 补充组 ID | |
| 保存的设置用户 ID | |
| 保存的设置组 ID | 由 `exec` 函数保存 |

图 4.5 与每个进程关联的用户 ID 和组 ID

- 真实用户 ID 和真实组 ID 标识了我们究竟是谁。这些字段来自我们登录时密码文件中的条目。通常，这些值在登录会话期间不会改变，尽管超级用户进程有方法更改它们，我们在第 8.11 节中描述。
- 有效用户 ID、有效组 ID 和补充组 ID 决定了我们的文件访问权限，正如我们在下一节中描述的。（我们在第 1.8 节中定义了补充组 ID）。
- 保存的设置用户 ID 和保存的设置组 ID 在程序执行时，分别包含有效用户 ID 和有效组 ID 的副本。我们在第 8.11 节的 `setuid` 函数中描述了这两个值的功能。

从 POSIX.1 的 2001 版本开始，要求使用保存的 ID。在旧版本的 POSIX 中，它们是可选的。应用程序可以在编译时测试常量 `_POSIX_SAVED_IDS` 或在运行时调用 `sysconf()`，以查看实现是否支持此功能。

通常，有效用户 ID 等于真实用户 ID，有效组 ID 等于真实组 ID。

每个文件都有一个所有者和一个组所有者。所有者由 `stat` 结构中的 `st_uid` 成员指定；组由 `st_gid` 成员指定。

## 4.5 文件访问权限

当我们执行程序时，进程的有效用户 ID 通常是真实用户 ID，有效组 ID 通常是真实组 ID。然而，我们也可以在文件的模式字 (`st_mode`) 中设置一个特殊标志，表示：“当执行此文件时，进程的有效用户 ID 为文件的所有者。”

有效用户 ID、有效组 ID 和补充组 ID 决定了我们的文件访问权限，正如我们在下一节中描述的。（我们在第 1.8 节中定义了补充组 ID）。

保存的设置用户 ID 和保存的设置组 ID 在程序执行时，分别包含有效用户 ID 和有效组 ID 的副本。我们在第 8.11 节的 `setuid` 函数中描述了这两个值的功能。
