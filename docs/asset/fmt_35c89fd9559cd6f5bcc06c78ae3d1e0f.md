
| | | | | User | | | Group | | | |

**图 15-1:** `st_mode` 位掩码布局

可以通过与常量 `S_IFMT` 进行按位与 (`&`) 操作来提取文件类型。在 Linux 上，4 位被用于 `st_mode` 字段中的文件类型部分。然而，SUSV 对文件类型的表示方式没有任何规定，这可能随实现的不同而异。得到的值可以与一系列常量进行比较以确定文件类型，如下：

```
if ((statbuf.st_mode & S_IFMT) == S_IFREG)
    printf("regular file\n");
```

由于这是一个常用操作，提供了标准宏将上述操作简化为：

```
if (S_ISREG(statbuf.st_mode))
    printf("regular file\n");
```

完整的文件类型宏（定义在 `<sys/stat.h>` 中）如表 15-1 所示。表 15-1 中的所有文件类型宏在 Sysv3 中都有规定并出现在 Linux 上。其他某些 UNIX 实现定义了额外的文件类型宏（例如，用于 Solaris 中门文件的 `S_IFDOOR`）。类型 `S_IFBLK` 仅由 `stat()` 返回，因为对 `stat()` 的调用总是返回符号链接。

原始的 POSIX.1 标准没有指定表 15-1 第一列中的常量，但其中大多数常量出现在大多数 UNIX 实现中。Sysv3 要求这些常量。

为了从 `<sys/stat.h>` 获取 `S_IFSOCK` 和 `S_ISSOCK()` 的定义，我们必须要么定义 `BSD_SOURCE` 宏，要么定义值大于或等于 500 的 `_XOPEN_SOURCE`。（规则在不同的 glibc 版本中有所不同：在某些情况下，`_XOPEN_SOURCE` 必须定义为 600 或更大）。

## 表 15-1: 结构体 *st_mode* 字段中检查文件类型的宏

| 常量 | 测试宏 | 文件类型 |
| --- | --- | --- |
| `S_IFREG` | `S_ISREG()` | 普通文件 |
| `S_IFDIR` | `S_ISDIR()` | 目录 |
| `S_IFCHR` | `S_ISCHR()` | 字符设备 |
| `S_IFBLK` | `S_ISBLK()` | 块设备 |
| `S_IFIFO` | `S_ISIFO()` | FIFO 或管道 |
| `S_IFSOCK` | `S_ISSOCK()` | Socket |
| `S_IFLNK` | `S_ISLNK()` | 符号链接 |

`*st_mode*` 字段的低 12 位定义了文件的权限。我们在 15.4 节中描述了文件权限位。目前，我们注意到权限位中最低的 9 位是每个所有者、组和其他类别的读、写、执行权限。

### 文件大小、分配的块和最佳 I/O 块大小

对于普通文件，`*st_size*` 字段是文件以字节计算的总大小。对于符号链接，该字段包含链接指向的路径长度（字节）。对于共享内存对象（第 24 章），该字段包含对象的大小。

`*st_blocks*` 字段表示分配给文件的总块数，以 512 字节为单位。此总数包括分配给指针块的空间（参见图 14-2，第 258 页）。选择 512 字节作为测量单位是历史性的——这是 UNIX 下实现的所有文件系统中最小的块。更现代的文件系统使用更大的块大小。例如，对于 ext2，`*st_blocks*` 中的值始终是 2、4 或 8 的倍数，取决于 ext2 的逻辑块大小是 1024、2048 还是 4096。Sysv3 未定义 `*st_blocks*` 的测量单位，但大多数 UNIX 实现使用系统特定的单位（例如，在某些情况下为 1024 字节）。`st_blocks` 字段记录实际分配的磁盘块数。如果文件包含空洞（第 4.7 节），它将比相应的字节数（`st_size`）小。`du -k` 以千字节显示文件分配的实际空间；它是根据 `st_blocks` 值计算的。`bsize` 字段的命名具有误导性。它不是底层系统的块大小，而是该系统进行 I/O 操作的最佳大小（字节）。典型的 `bsize` 值为 4096。

### 文件时间戳

`st_atime`、`mtime` 和 `ctime` 字段包含最后访问、文件修改和状态更改的时间。这些字段是 `time_t` 类型，即自纪元（Epoch）以来的秒数（参见 15.2）。

### 示例程序

15-1 中的程序使用 `stat()` 获取有关命令行指定文件的信息。如果指定了 `-l` 选项，则使用 `lstat()` 获取它指向的符号链接信息。该程序打印返回的结构体的所有字段（关于为什么我们将 `st_size` 和 `st_blocks` 字段转换为 `long`，参见第 15.10 节）。该程序使用的 `displayStatInfo` 函数位于 15-4，第 296 页。以下是该程序的使用示例：

```
$ echo 'All operating systems services for programs' > file
$ chmod 644 file
$ cat file
$ ./t_stat file
All operating systems services for programs
File type: regular file
Device containing i-node: major=3 minor=1
In-number: 23463
Mode: 10644 (rw-r--r--)
special: set
Number of (hard) links: 1
Ownership: UID=1000 GID=100
File size:
Optimal I/O block size: 4096 bytes
512 blocks allocated: 8
Last file access: Mon Jun 8 09:40 2011
Last file modification: Mon Jun 8 09:39 2011
Last status change: Mon Jun 8 09:39 2011
```

#### 15-1:

```c
#define BSD_SOURCE  /* 从 <sys/types.h> 获取 major() 和 minor() */
#include <sys/types.h>
#include <sys/stat.h>
#include <time.h>
#include "file_perms.h"
#include "tlpi_hdr.h"

static void displayStatInfo(const struct stat *sb) {
    printf("File type: %s", file_type(sb->st_mode));
    printf("Last file access: %s", ctime(&sb->st_atime));
    printf("Last file modification: %s", ctime(&sb->st_mtime));
    printf("Last status change: %s", ctime(&sb->st_ctime));
}

int main(int argc, char *argv[]) {
    struct stat sb;
    int statlink;
    int fname;

    /* 如果指定 "-l" (即使用 lstat) */
    /* 文件名在 argv[1] 中的位置 */
    statlink = (argc > 1 && strcmp(argv[1], "-l") == 0);
    /* 对 "-l" 的简单解析 */
    fname = statlink ? 2 : 1;

    if (fname == argc || (argc > 1 && strcmp(argv[1], "--help") == 0)) {
        usageError(argv, "-l - use lstat() instead of stat()\n", argv[0]);
    }

    if (statlink) {
        if (lstat(argv[fname], &sb) == -1)
            errorExit("stat");
    } else {
        if (stat(argv[fname], &sb) == -1)
            errorExit("stat");
    }

    displayStatInfo(&sb);

    exit(EXIT_SUCCESS);
}
```

## 15.2 文件时间戳

`stat` 结构体的 `st_atime`、`st_mtime` 和 `ctime` 字段包含文件时间戳。这些字段分别记录了最后访问、最后文件修改和最后文件状态更改（文件 i 节点信息的最后更改）。时间戳以自纪元（1970 年 1 月 1 日；参见第 10.1 节）秒记录。

大多数 Linux 和 UNIX 系统支持所有时间戳字段，但某些非 UNIX 文件系统可能不支持。

表 15-2 总结了书中描述的各种系统调用和库函数更改的时间戳字段（在某些情况下，为父目录中的相应字段）。在表的头中，a、m 和 c 分别代表 `st_atime`、`st_mtime` 和 `st_ctime` 字段。在大多数情况下，相关时间戳由系统调用设置为当前时间。例外是 `utime()` 和类似的调用（在 15.2.1 节和 15.2.2 节中讨论），它们可用于显式地将最后访问和修改时间设置为任意值。

### 表 15-2：各种函数对文件时间戳的影响

| 函数 | 目录 a m c | 父目录 a m c | 注释 |
|---|---|---|---|---|---|---|---|
| `chmod()` | | | | | | 与 `chmod` 相同 |
| `chown()` | | | | | | 与 `lchown()` 和 `chown` 相同 |
| `exec()` | | | | | | | |
| `link()` | | | | | | | 影响第二个参数的父目录 |
| `mkdir()` | | | | | | | |
| `mkfifo()` | | | | | | | |
| `mnode()` | | | | | | | |
| `mmap()` | | | | | | | 仅在更新 `MAP_SHARED` 映射时才更改 `st_mime` 和 `st_ctime` |
| `msync()` | | | | | | | 仅在文件被修改时更改 |
| `open(), create()` | | | | | | | 创建新文件时 |
| `open(), create()` | | | | | | | 截断现有文件时 |
| `pipe()` | | | | | | | |
| `read()` | | | | | | | |
| `readdir()` | | | | | | 与 `readv(), pread(), 和 readdir(v)` 相同；可能会缓存目录项；仅在读取目录时更新时间戳 |
| `removeattr()` | | | | | | 与 `removexattr()` 和 `lremoveattr()` 相同 |
| `rename()` | | | | | | 影响父目录；Sysv3 未规定文件 `st_ctime` 的更改，但注释中提到某些实现会这样做 |
| `rmdir()` | | | | | | 与 `remove(directory)` 相同 |
| `sendfile()` | | | | | | | 输入文件的时间戳发生变化 |
| `setattr()` | | | | | | 与 `forxattr()` 和 `lsetattr` 相同 |
| `symlink()` | | | | | | 设置链接（而非目标文件）的时间戳 |
| `truncate()` | | | | | | 与 `truncate()` 相同；仅在文件大小发生变化时时间戳才变化 |
| `unlink()` | | | | | | 与 `remove(file)` 相同；如果之前的链接计数为 1，则文件 `st_ctime` 发生变化 |
| `utime()` | | | | | | 与 `utimes(), futimens(), lutimes(), 和 utimensat()` 相同 |
| `write()` | | | | | | 与 `writev(), pwritev(), 和 pwritev()` 相同 |

在第 14.8.1 和 15.5 节中，我们描述了 `mount(2)` 选项和防止更新文件最后访问时间的标志。第 4.3.1 节中描述的 `open()` `O_NOATIME` 标志也具有类似的目的。在某些应用程序中，出于性能考虑，这非常有用，因为减少了访问文件所需的磁盘操作次数。

尽管大多数 UNIX 系统不记录文件的创建时间，但在最近的 BSD 系统上，此时间记录在一个名为 `st_birthtime` 的 `stat` 字段中。

### 纳秒级时间戳

从 2.6 版本开始，Linux 支持 `*stat*` 结构中三个时间戳字段的纳秒级精度。纳秒精度提高了需要根据文件时间戳相对顺序做出决策的程序（例如 `make(1)`）的准确性。

SUSv3 未规定 `*stat*` 结构的纳秒时间戳，但 SUSv4 增加了这一规定。并非所有系统都支持纳秒时间戳。JFS、XFS、ext4 和 Btrfs 不支持，ext2 和 Reiserfs 支持。

通过 glibc API（从 2.3 版本开始），时间戳字段定义为 `*timespec*`（我们在本节讨论 `utimes(1)` 时会描述这一点），它代表由秒和纳秒部分组成的时间。合适的宏定义使得可以使用字段名（`st_atime`、`st_mtime` 和 `st_tv_nsec`）访问这些结构的秒部分。纳秒部分可以通过字段名 `st_atim_nsec` 访问，用于最后文件访问时间的纳秒部分。

### 使用 utime() 和 utimes() 更改文件时间戳

存储在文件 i-node 中的文件最后访问和修改时间戳可以使用 `utime()` 或一组相关系统调用之一显式地更改。像 `tar(1)` 和 `unzip(1)` 等程序使用这些系统调用在解压存档时重置文件时间戳。

```
#include <utime.h>
utime(const char *pathname, const struct utimbuf *buf);
成功返回 0，错误返回 -1
```

`*pathname*` 参数标识我们想要修改的文件时间。如果 `*pathname*` 是符号链接，则会被解引用。`*buf*` 参数可以是 `NULL` 也可以是指向 `utimbuf` 结构的指针：

```
struct utimbuf {
    time_t atime;      /* 访问时间 */
    time_t mtime;      /* 修改时间 */
};
```

该结构中的字段测量的是自 Epoch 以来（第 10.1 节）的秒数。

两种不同的情况决定了 `utime()` 的工作方式：

- 如果 `*buf*` 指定为 `NULL`，则最后访问时间和最后修改时间被设置为当前时间。在这种情况下，要么进程的用户 ID 必须匹配文件的用户 ID（所有者），要么进程必须对文件有写权限（逻辑上，因为对文件有写权限的进程可以使用具有更改这些时间戳副作用的其他系统调用），或者进程必须具有特权（`CAP_OWNER` 或 `CAP_DAC_OVERRIDE`）。

- （准确地说，在 Linux 上，是进程的文件系统用户 ID，而不是有效 ID）如果 `*buf*` 指定为指向 `utimbuf` 结构的指针，则最后访问时间和最后修改时间被设置为当前时间。在这种情况下，要么进程的用户 ID 必须匹配文件的用户 ID（所有者），要么进程必须对文件有写权限（逻辑上，因为对文件有写权限的进程可以使用具有更改这些时间戳副作用的其他系统调用），或者进程必须具有特权（`CAP_OWNER` 或 `CAP_DAC_OVERRIDE`）。

```
struct stat sb;
struct utimbuf buf;

buf.atime = sb.st_atime; /* 访问时间 */
buf.mtime = sb.st_mtime; /* 修改时间 */
if (utime(pathname, &buf) == -1)
    errExit("utime");
```

如果 `times` 指定为 `NULL`，则两个文件时间戳都会更新为当前时间。如果 `times` 不为 `NULL`，则最后访问时间指定在 `times[0]` 中，新的最后修改时间指定在 `times[1]` 中。数组中的每个元素都是如下结构：

```
struct timespec {
    long tv_sec;      /* 秒（'time' 是一个整数类型） */
    long tv_nsec;     /* 纳秒 */
};
```

该结构中的字段指定了自 Epoch（10.1）以来的秒和纳秒级的时间。

要将其中一个时间戳设置为当前时间，我们在相应的 `tv_nsec` 中指定特殊值 `UTIME_NOW`。若要保持其中一个时间戳不变，我们在相应的 `tv_sec` 字段中指定特殊值 `UTIME_OMIT`。在这两种情况下，相应 `tv_sec` 字段中的值都会被忽略。

`dirfd` 参数可以是 `AT_FWD`，也可以指定一个指向目录的文件描述符。后者的目的见第 18.11 节。

`flags` 参数可以是 `0` 或 `AT_SYMLINK_NOFOLLOW`，这意味着如果 `pathname` 是符号链接，则不应对其进行追踪（即更改符号链接本身的时间戳）。相比之下，`utimens()` 总是追踪符号链接。

以下代码段将最后访问时间设置为当前时间，并保持最后修改时间不变：

```
struct timespec[2];
times[0].tv_sec = 0;
times[0].tv_nsec = UTIME_NOW;
times[1].tv_sec = 0;
times[1].tv_nsec = UTIME_OMIT;
if (utimensat(AT_FDCWD, "myfile", 0) == -1)
    errExit("utimensat");
```

使用 `utimensat()` 和 `futimens()` 修改时间戳的权限规则与其他 API 类似：
