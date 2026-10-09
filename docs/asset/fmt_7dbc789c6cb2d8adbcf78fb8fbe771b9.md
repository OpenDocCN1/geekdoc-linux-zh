
# 函数返回值

返回：成功返回读取的字节数，错误为 1。

该函数结合了`open`、`read`和`close`的操作。如果函数成功，它返回放入`buf`中的字节数。返回在`buf`中的符号链接内容不是空结尾的。

## 4.18. 文件时间

每个文件维护三个时间字段。它们的目的总结在图 19 中。

| 字段 | 描述 | 示例 | 选项 |
|---|---|---|---|
| `st_atime` | 文件数据的最后访问时间 | `read` | `-u` |
| `st_mtime` | 文件数据的最后修改时间 | `write` | 默认 |
| `st_ctime` | `inode`状态的最后更改时间 | `chmod`, `chown` | `-c` |

注意修改时间（`st_mtime`）和状态更改时间（`st_ctime`）之间的区别。修改时间是文件内容被修改的时间。状态更改时间是文件`inode`最后被修改的时间。在本章中，我们描述了许多许多文件内容但影响`inode`的操作：更改访问权限、更改用户 ID、更改链接数等。`inode`中的所有信息与文件的实际内容分开存储。

对目录硬链接的需求早已消失。有了符号链接和`mkdir`函数，我们不再需要创建目录的硬链接。

当我们打开一个文件时，`open`路径名创建一个符号链接，`open`跟随链接指向文件。如果符号链接指向的文件不存在，`open`返回错误。这可能会让不熟悉符号链接的用户感到困惑。例如（重复上文）：

`-l`选项给了我们两个信息：第一个字符是`l`，表示符号链接；序列`->`表示符号链接。`ls`的另一个选项`-F`会为符号链接的文件名添加`@`，这有助于在目录列表中识别符号链接。

修改时间（`st_mtime`）和状态更改时间（`st_ctime`）之间的区别。修改时间是文件内容被修改的时间。状态更改时间是文件`inode`最后被修改的时间。在本章中，我们描述了许多许多文件内容但影响`inode`的操作：更改访问权限、更改用户 ID、更改链接数等。`inode`中的所有信息与文件的实际内容分开存储。对目录硬链接的需求早已消失。有了符号链接和`mkdir`函数，我们不再需要创建目录的硬链接。

## 4.20. 各种函数对访问、修改和状态更改时间的影响

修改时间是文件内容被修改的时间。状态更改时间是文件`inode`最后被修改的时间。在本章中，我们描述了许多许多文件内容但影响`inode`的操作：更改访问权限、更改用户 ID、更改链接数等。`inode`中的所有信息与文件的实际内容分开存储。

| 函数 | 引用的文件或目录 | 章节 | 备注 |
|---|---|---|---|
| `chmod`, `fchmod` | a, m, c | | |
| `chown`, `fchown` | a, m, c | | |
| `create` | a | 3.4 | `O_CREATE` |
| `create` | m | 3.4 | `O_TRUNC` |
| `exec` | a | 10 | |
| `lchown` | a | 11 | |
| `link` | a | 15 | |
| `mkdir` | a | | 20 |
| `open` | a | 3.3 | `O_CREAT` |
| `open` | a | 3.3 | `O_TRUNC` |
| `pipe` | a | 15 | |
| | a | | |
| | a, a | 15 | |
| `truncate`, `ftruncate` | a | 13 | |
| `unlink` | a | 15 | |
| `utime` | a | 19 | |
| `write` | a | 3.8 | |

## 4.19. `utime` 函数

可以使用`utime`函数更改文件的访问时间和修改时间。

```c
#include <utime.h>

int utime(const char *pathname, const struct utimbuf *times);
```

返回：成功为 0，错误为 1。

该函数使用的结构体是：

```c
struct utimbuf {
    time_t actime; /* 访问时间 */
    time_t modtime; /* 修改时间 */
};
```

结构体中的两个值是日历时间，即自 Epoch 以来的秒数，如第 1.10 节所述。该函数的操作以及执行它的权限取决于`times`参数是否为`NULL`。

*   如果`times`是空指针，则访问时间和修改时间都被设置为当前时间。要实现这一点，进程的有效用户 ID 必须等于文件的所有者 ID，或者进程对文件具有写权限。
*   如果`times`是非空指针，则访问时间和修改时间被设置为指向结构体中的值。对于这种情况，进程的有效用户 ID 必须等于文件的所有者 ID，或者进程必须是超级进程。仅仅拥有文件的写权限是不够的。

注意，我们无法指定状态时间`st_ctime`（即`inode`最后更改的时间），该字段在调用`utime`函数时会自动更新。

在某些 Unix 系统版本中，`touch(1)`命令使用此函数。此外，标准归档程序`tar(1)`和`cp(1)`可选调用`utime`将文件的时间设置为归档时保存的时间。

### 示例

图 4.21 中的程序使用`open`函数的`O_TRUNC`选项将文件截断为零长度，但不会更改访问或修改时间。为了实现，程序通过`stat`函数获取文件时间，截断文件，然后使用`utime`函数重置时间。

我们可以通过以下脚本演示图 4.21 中的程序：

```bash
$ ls -l changed times
-rw-r-- -x 1 sar 15019 Nov 18 18:53 changed
-rw-r-- -x 1 sar 16172 Nov 19 20:05 times

$ ls -lu changed times
-rw-r-- -x 1 sar 15019 Nov 18 18:53 changed
-rw-f-- -x 1 sar 16172 Nov 19 20:05 times

$ date
Thu Jan 22 06:55:17 EDT 2004

$ ./aout changed times
-rw-r-- -x 1 sar 0 Nov 18 18:53 changed
-rw-f-- -x 1 sar 0 Nov 19 20:05 times

$ ls -lu changed times
-rw-f-- -x 1 sar 0 Nov 18 18:53 changed
-rw-f-- -x 1 sar 0 Nov 19 20:05 times

$ ls -lc changed times
-rw-f-- -x 1 sar 0 Jan 22 06:55 changed
-rw-f-- -x 1 sar 0 Jan 22 06:55 times
```

如我们所见，修改时间和最后访问时间没有改变。然而，状态状态（changed-status）被更改为程序运行的时间。

## 图 4.21. `utime` 函数示例

```c
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>

int
main(int argc, char *argv[])
{
    int i, fd;
    struct stat statbuf;
    struct utime timbuf;

    for (i = 1; i < argc; i++) {
        if (stat(argv[i], &statbuf) < 0) { /* fetch current times */
            perror("%s: stat error", argv[i]);
            continue;
        }

        if ((fd = open(argv[i], O_RDWR | O_TRUNC)) < 0) { /* truncate */
            perror("%s: open error", argv[i]);
            continue;
        }

        close(fd);

        timbuf.actime = statbuf.st_atime;
        timbuf.modtime = statbuf.st_mtime;

        if (utime(argv[1], &timbuf) < 0) {  /* reset times */
            return err_ret("%s: error", argv[1]);
        }
    }
    exit(0);
}
```

![](img/902515e97eef28cac8083866e00a6f4c_191_0.png)

## 4.20. `mkdir` 和 `rmdir` 函数

使用`mkdir`函数创建目录，使用`rmdir`函数删除目录。

```c
#include <sys/stat.h>

int mkdir(const char *pathname, mode_t mode);
```

返回值：如果 OK 返回 0，错误返回 -1。

此函数创建一个新的空目录。`.`和`..`目录目会被自动创建。指定的访问权限`mode`会被进程的文件创建掩码（umask）修改。

一个常见的错误是指定与文件相同的模式，例如：仅读和写权限。对于目录，我们通常希望至少启用一个位，以允许访问目录中的文件名（参见练习 4.16）。

新目录的用户 ID 和组 ID 根据第 4.6 节中的规则建立。

Solaris 9 和 Linux 2.4.22 还会从父目录继承新的设置组组 ID（set-group ID）。这样做是为了让在新目录中创建的文件继承该目录的组 ID。在 Linux 中，文件系统的实现决定了是否支持此功能。例如，ext2 和 ext3 文件系统的这种行为由`mount(1)`命令的选项控制。然而，该行为是不可选择的；它继承设置组组 ID 以模拟历史上的 BSD 系统实现，其中目录的组 ID 继承自父目录。

基于 BSD 的实现不传播设置组组 ID 位；它们只是作为过程的一部分继承组 ID。由于 FreeBSD 5.2.1 和 Mac OS 10.3 是基于 4.2BSD 的，因此它们不需要这种设置组组 ID 的继承。在这些平台上，新创建的文件和目录总是继承父目录的组 ID，无论设置组位如何。

早早版本的 UNIX 系统没有`mkdir`函数。它是随着 4.2BSD 和 SVR3 引入的。在早早版本中，必须调用`mknod`来创建新目录。但该函数被限制为超级进程（super processes）。为了绕过这一点，使用了创建目录的普通命令`mkdir(1)`。

`rmdir()`函数删除目录。为了使`rmdir()`成功，目录必须为空。目录必须只包含`.`和`..`条目。

```c
#include <unistd.h>

int rmdir(const char *pathname);
```

返回值：如果 OK 返回 0，错误返回 -1。

## 4.21. 读取目录

可以使用目录例程来读取目录。`DIR`结构是六个函数用于维护目录信息的内部结构。`DIR`结构的目的是使用标准定义的`FILE`，以便我们遍历目录中的所有文件。

由`opendir`返回的`DIR`结构指针随后被其他函数使用。`opendir`初始化后，第一次`readdir`读取目录中的第一个条目。目录内条目的顺序取决于实现，并且不一定按字母顺序排列。

`dirent`结构定义在`<dirent.h>`中，包含目录条目的信息。`dirent`的实际格式取决于实现，但符合 POSIX 的系统定义的结构至少包含以下内容：

```c
#include <dirent.h>

struct dirent {
    ino_t d_ino;        /* 节点号 */
    char d_name[NAME_MAX + 1]; /* 以空结尾的文件名 */
};
```

`NAME_MAX`不是定义的常量；该值通常通过`pathconf()`函数获取，`NAME_MAX`的值为 255。

目录例程用于访问目录内容。在单 Unix 规范中，`ftw`和`nftw`包含在 POSIX.1 基本的 XXI 扩展中。实现包含了 Solaris 9 和 Linux 2.4.22。基于 BSD 的系统有一个不同的函数`fts(3)`，它提供了相似的功能。

```c
#include "apue.h"
#include <dirent.h>
#include <limits.h>

/* 为每个文件名调用的函数类型 */
typedef int (*Myfunc)(const char *, struct stat *);

static Myfunc myfunc;
static int myftw(char *, Myfunc *);
static int dopath(Myfunc *);
static long nreg, ndir, ndbk, nfrlo, niflo, nslink, nsock, nrot, ntot, nchr;

int
main(int argc, char *argv[])
{
    int ret;

    if (argc-1 != 2)
        err_quit("use: ftw <starting-path>");

    ret = myftw(argv[1], myfunc); /* 遍历所有文件 */
    ntot = nreg + ndir + ndbk + nfrlo + nslink + nsock;
    if (ntot == 0)
        ntot = 1; /* 避免除以零；所有计数均打印 0 */

    printf("regular files = %td, %5.2f%%\n", nreg, nreg*100.0/ntot);
    printf("directories = %td, %5.2f%%\n", ndir, ndir*100.0/ntot);
    printf("block special = %td, %5.2f%%\n", ndbk, ndbk*100.0/ntot);
    printf("char special = %td, %5.2f%%\n", nchr, nchr*100.0/ntot);
    printf("FIFO = %td, %5.2f%%\n", niflo, niflo*100.0/ntot);
    printf("symbolic links = %td, %5.2f%%\n", nslink, nslink*100.0/ntot);
    printf("sockets = %td, %5.2f%%\n", nsock, nsock*100.0/ntot);

    exit(ret);
}

/* 遍历层级结构，从 "pathname" 开始
调用者的 func() 会为每个文件被调用一次。 */
#define FTW_F 1 /* 目录以外的文件 */
#define FTW_D 2 /* 目录 */
#define FTW_NR 3 /* 无法读取的目录 */
#define FTW_NS 4 /* 无法 stat 的文件 */

static char *fullpath; /* 包含每个文件的完整路径 */
/* 我们返回 func() 的返回值 */

static int
myftw(char *pathname, Myfunc func)
{
    int len;

    fullpath = path_alloc(&len); /* 为 PATH_MAX+1 字节分配内存 */
    strncpy(fullpath, pathname, len); /* 产生缓冲区溢出 */
    fullpath[len-1] = 0;

    return dopath(func);
}

/* 遍历层级结构，从 "fullpath" 开始
如果 "fullpath" 是目录以外的任何内容，则 stat(it) 并返回。对于目录，对目录中的每个名称递归调用自身。 */

static int
dopath(Myfunc func)
{
    struct stat statbuf;
    struct dir *dirp;
    DIR *dp;
    int ret;
    char *ptr;

    if (stat(fullpath, &statbuf) < 0) /* stat 错误 */
        return func(fullpath, FTW_NS);
    if (S_ISDIR(statbuf.st_mode) == 0) /* 不是目录 */
        return func(fullpath, FTW_F);

    /* 它是一个目录。首先为目录调用 func()，
    然后处理目录中的每个文件名。 */
    if ((ret = func(fullpath, &statbuf, FTW_D)) != 0)
        return(ret);

    ptr = fullpath + strlen(fullpath); /* 指向 fullpath 的末尾 */
    *ptr++ = '/'; *ptr = 0;

    if ((dp = opendir(fullpath)) == NULL) /* 无法读取目录 */
        return func(fullpath, &statbuf, FTW_NR);

    while ((dirp = readdir(dp)) != NULL) {
        if (strcmp(dirp->d_name, ".") == 0 ||
