
```c
#include <dirent.h>
#include <tlpi_hdr.h>

/* 列出目录 'dirPath' 中的所有文件 */
static void
listFiles(const char *dirpath)
{
    DIR *dir;
    struct dirent *dp;
    Boolean isCurrent /* 如果 'dirpath' 为 "." 则为 True */

    isCurrent = strcmp(dirpath, ".") == 0;
    dir = opendir(dirpath);
    if (dir == NULL) {
        errMsg("opendir failed on %s", dirpath);
        return;
    }
    /* 对于目录中的每个条目，打印 dirpath + filename */
    for (;;) {
        errno = 0 /* 区分错误与目录结束 */
        dp = readdir(dir);
        if (dp == NULL)
            break;

        if (strcmp(dp->d_name, ".") == 0 || strcmp(dp->d_name, "...") == 0)
            /* 跳过 和 ... */
            continue;

        if (isCurrent)
            printf("%s/%s", dirpath);
        printf("%s\n", dp->d_name);
    }

    if (errno != 0)
        errExit("readdir");

    if (closedir(dir) == -1)
        errMsg("closedir");
}

int
main(int argc, char *argv[])
{
    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usageErr("%s [dir...]\n", argv[0]);

    if (argc == 1) /* 无参数 - 使用当前目录 */
        listFiles(".");
else
    for (argv++; *argv, argv++)
        listFiles(*argv);
}
```

`dirs_r/list_file.c`

## readdir_r(r) 函数

`readdir_r()` 函数是 `readdir()` 的变体。`readdir_r(r)` 和 `readdir(r)` 之间的关键语义区别在于前者是重入的（reentrant），而后者不是。这是因为 `readdir_r(r)` 通过调用者分配的参数返回文件条目，而 `readdir(r)` 则通过指向静态分配结构的指针返回信息。我们将在第 21.1.2 节和第 31.1 节中讨论了重入性。

```c
#include <dirent.h>
int readdir_r(DIR *dirp, struct dirent *entry, struct **result);
// 成功时返回 0，出错时返回正数
```

给定 `dip`（之前通过 `opendir()` 打开的目录流），`readdir_r()` 将将下一个条目放入 `entry` 所指的 `dirent` 结构中。此外，指向该结构的指针被放在 `result` 中。如果到达目录流的末尾，则在 `result` 中放入 `NULL`，`readdir_r()` 返回 0。否则，`readdir_r()` 不返回 -1，而是返回与 `errno` 值对应的正整数。

在 Linux 上，`dirent` 结构中的 `d_name` 字段的大小为 256 字节的数组，足以容纳最大的文件名。尽管其他几个 UNIX 实现也为 `d_name` 定义了相同的大小，但 SUS3 未对此点进行规定，而某些 UNIX 实现将该字段定义为 1 字节数组，允许调用程序负责分配正确大小的结构。

```c
struct dirent *entry;
size_t len;
```

使用 `offsetof()` 宏（定义在 `<stddef.h>` 中）以避免对特定实现的依赖。

## 18.9 树遍历：nftw()

`nftw()` 函数允许程序对子树中的每个文件遍历整个子树（即调用程序员定义的函数）。这是旧 `ftw()` 的增强，`ftw()` 执行类似的任务。

GNU 库提供了 `fts`，`nftw()` 遍历由 `dirpath` 指定目录，为树中的每个文件调用程序员定义的函数。

```c
#define _OPEN_SOURCE 500
#include <ftw.h>

int nftw(const char *dirpath, int (*func)(const char * pathname, struct stat *statbuf, int typeflag), int openfd, int flags);
```

成功遍历树后返回 0，出错时返回 -1，或返回 `func` 返回的非零值

`nftw()` 的 `flags` 参数通过按位或 (`|`) 零个或多个以下常量创建，这些常量会修改函数的运算：

- `FTW_CHDIR`: 在处理目录内容之前通过 `chdir()` 进入每个目录。如果 `func` 设计用于在路径所在的目录中执行工作，则此项很有用。

- `FTW_DEPTH`: 对目录树进行后序遍历。这意味着 `nftw()` 在处理目录本身之前，先对目录内的所有文件（和子目录）调用 `func`。（名字有点误导性——`nftw()` 总是以深度优先而非广度优先的方式遍历目录树。）

- `FTW_MOUNT`: 不跨越另一个文件系统。因此，如果树的某个子目录是挂载点，则不会进行遍历。

- `FTW_PHYS`: 默认情况下，`nftw()` 会解析符号链接。此标志告诉它不要这样做。相反，符号链接将以 `typeflag` 值 `FTW_SL` 传递给 `func`，如下所示。

对于每个文件，`nftw()` 在调用 `func` 时传递四个参数。第一个参数 `pathname` 是文件的路径。如果 `dirpath` 被指定为绝对路径或相对于调用 `nftw()` 时调用进程的工作目录，则该路径可能是绝对路径。第二个参数 `statbuf` 是一个指向 `stat` 结构（第 15.1 节）的指针，包含有关该文件的信息。第三个参数 `typeflag` 提供有关文件的更多信息，并具有以下值之一：

- `FTW_D`: 这是一个目录。

- `FTW_DNR`: 这是一个无法的目录（因此 `nftw()` 不遍历其任何后代）。

- `FTW_DP`: 我们正在对目录进行后序遍历（`FTW_DEPTH`），且当前项是一个已经处理过的文件的目录。

- `FTW_F`: 这是一个目录或符号链接外的任何类型的文件。

- `FTW_NS`: 对此文件调用 `stat()` 失败，可能是由于权限限制。`statbuf` 中的值未定义。

`FTW_SL`

这是一个符号链接。只有在调用 *nftw()* 时带有 `FTW_PHYS` 标志时，才会返回此值。

`FTW_SLN`

这是一个悬空符号链接。只有当在 `flags` 参数中未指定 `FTW_PHYS` 时，才会出现此值。

*func, fbuf* 的第四个参数是一个指向如下定义的结构的指针：

```
struct FTW {
    int base;       /* 指向 pathname 中 basename 部分的偏移量 *
    int level;     /* 文件在树遍历中的深度 *
};
```

该结构体的 `base` 字段是 *func* 的 `pathname` 参数中文件名（斜杠 `/` 之后的部分）的整数偏移量。`level` 字段是该项目相对于遍历起始点的深度（起始点为 level 0）。

每次调用 *func* 时，它必须返回一个整数值，该值由 *nftw()* 返回。返回 0 继续树的遍历；如果对 *func* 的所有调用都返回 0，则 *nftw()* 本身将向调用者返回 0。返回非零值将告诉 *nftw()* 立即停止树遍历，在这种情况下，*nftw()* 返回该非零值作为其返回值。

由于 *nftw()* 使用动态分配的数据，程序提前终止目录树遍历的方法是从 *func* 返回一个非零值。使用 *longjmp()*（见第 6.8 节）退出 *func* 可能会导致不可预测的结果——至少会导致程序出现内存泄漏。

## 示例程序

列表 18-3 展示了 *nftw()* 的用法。

列表 18-3：使用 *nftw()* 遍历目录树

![](img/9979af2ec677a84a39c7b1fd105c84a4_403_0.png)

```
#define XOPEN_SOURCE 600      /* 获取 nftw() 和 S_IFSOCK 声明 */
#include <ftw.h>
#include "tlpi_hdr.h"

static void
usageerror(const char *progName, const char *msg) {
    if (msg != NULL) {
        fprintf(stderr, "%s\n", msg);
        fprintf(stderr, "Usage: %s [-d] [-p] [directory-path]\n", progName);
        fprintf(stderr, "-d FTW_DEPTH flag\n");
        fprintf(stderr, "-m FTW_MOUNT flag\n");
        fprintf(stderr, "-p FTW_PHYS flag\n");
        exit(EXIT_FAILURE);
    }
}

static int      /* 由 nftw()调用的函数 */
dirTree(const char *pathname, const struct stat *sbuf, int type,
    struct FTW *ftwb)
{
  switch (sbuf->st_mode & S_IFREG) {
    case S_IFREG: printf("-"); break;
    case S_IFDIR: printf("%d"); break;
    case S_IFCHR: printf("%c"); break;
    case S_IFBLKK: printf("%b"); break;
    case S_IFLNK: printf("%l"); break;
    case S_IFIFO: printf("%p"); break;
    case S_IFSOCK: printf("%s"); break;
    default:
      printf("%q"); break;
  }
}

/* 打印文件类型 */

```

printf("%s",

```

/* 永远不会发生（在 Linux 上） */

/* 明智地缩进 */

```

printf("%*s", 4 * ftw->level, "");

printf("%s\n", ftw->base);

return 0;

```

/* 告诉 nftw() 继续 */

```

int

main(int argc, char *argv[])

{

  int flags, opt;

  flags = 0;

  while ((opt = getopt(argc, argv, "dmp")) != -1) {

    switch (opt) {

      case 'd': flags |= FTW_DEPTH; break;

      case 'm': flags |= FTW_MOUNT; break;

      case 'p': flags |= FTW_PHYS; break;

      default: usageerror(argv[0], NULL);

    }

  }

  if (argc > optind + 1)

    usageerror(argv[0], NULL);

  if (nftw((argc > optind) ? argv[optind] : ".", dirTree, 10, flags) == -1)

    perror("nftw");

    exit(EXIT_FAILURE);

  }

  exit(EXIT_SUCCESS);

}

```

`dirs_links/nftw_dir_tree.c`

列表 18-3 中的程序显示了目录树中文件名的缩进层次结构，每行一个文件，以及文件类型和 inode 节点。可以使用命令行选项来指定 nftw() `flags` 参数的设置。以下会话显示运行此程序时看到的示例。我们首先创建一个新的空子目录，并向其中填充各种类型的文件：

```

$ mkdir dir/a dir/b

$ touch dir/a/sl

$ ln -s x dir/dsl

$ mkdir dir/sub

$ touch dir/sub/x

$ mkdir dir/sub2

$ chmod 0 dir/sub2

创建一些普通文件、一个符号链接、一个带有自己的文件的子目录、另一个不可读的子目录

```

我们使用我们的程序在 `flags` 参数为 0 的情况下调用 nftw()：

```

$ .nftw_dir_tree

dir

-a

  -sl

  -dsl

  sub

    -x

  sub2

```

使用 `chdir()` 的等效方法如下：

```

char buf[PATH_MAX];

```

```

/* 记住我们所在的位置//* 去另一个地方 */

/* 返回原始目录 */

```

```

getcwd(buf, PATH_MAX);

chdir(somepath);

chdir(buf);

```

## 11.11 相目录文件描述符进行相对操作

从内核 2.6.16 开始，Linux 提供了一系列新的系统调用，它们执行着与各种传统系统调用相似的任务，但提供了某些应用程序有用的额外功能。这些系统调用在表 18-2 中总结。我们在本章中描述这些系统调用，是因为它们提供了对进程当前工作目录传统语义的变体。

**表 18-2:** 使用目录文件描述符解释相对路径名的系统调用

| 接口 | 传统 | 备注 |
| --- | --- | --- |
| faccess() | access() | 支持 AT_EACCESS 和 AT_SYMLINK_NOFOLLOW 标志 |
| fchmod() | chmod() | |
| chown() | chown() | 支持 AT_SYMLINK_NOFOLLOW 标志 |
| fstat() | stat() | 支持 AT_SYMLINK_NOFOLLOW 标志 |
| link() | link() | 支持（自 Linux 2.6.18 起）AT_SYMLINK_FOLLOW 标志 |
| mkdirat() | mkdir() | |
| mkfifoat() | mkfifo() | 构建在 mknod() 之上的库函数 |
| mknodat() | mknod() | |
| openat() | open() | |
| readlink() | readlink() | |
| renameat() | renameat() | |
| symlinkat() | symlink() | |
| unlinkat() | unlink() | 支持 AT_REMOVEDIR 标志 |
| utimensat() | utimes() | 支持 AT_SYMLINK_NOFOLLOW 标志 |

为了描述这些系统调用，我们将使用一个特定的示例：`openat()`。

```c

#define _XOPEN_SOURCE 700    /* 或者定义 POSIX_SOURCE >= 200809 */

#include <fcntl.h>

int openat(int dirfd, const char *pathname, int flags, ... /* mode_t mode */);

// 成功时返回文件描述符，失败时返回 -1
```
