
对于每个文件，`nftw()` 在调用 `func` 时传递四个参数。其中第一个参数 `pathname` 是文件的路径。如果 `dirpath` 指定为相对路径，则该路径可能是绝对路径，也可以是相对于调用 `nftw()` 时调用进程当前的工作目录的相对路径。第二个参数 `statbuf` 是指向 `stat` 结构（第 15.1 节）的指针，包含有关文件的信息。第三个参数 `typeflag` 提供有关文件的更多信息，并具有以下值之一：

- `FTW_D`：这是一个目录。
- `FTW_DNR`：这是一个不可读目录（且 `nftw()` 不遍历其任何后代）。
- `FTW_DP`：我们正在对目录进行后序遍历（`FTW_DEPTH`），且当前项是一个其文件和子目录已处理过的目录。
- `FTW_F`：这是一个除目录或符号链接外的任何类型的文件。
- `FTW_NS`：调用 `stat()` 处理该文件失败，可能是由于权限限制。`statbuf` 中的值未定义。

`openfd` 参数指定了 `nftw()` 可能使用的文件描述符的最大数量。如果树的深度超过此最大值，`nftw()` 会进行一些记录工作以避免每层打开文件描述符。

## FTW_SL

这是一个符号链接。只有在调用 `nftw()` 时带上 `FTW_PHYS` 标志，才会返回此值。

## FTW_SLN

此项是一个悬空符号链接。只有在 `flags` 参数中未指定 `FTW_PHYS` 时，才会出现此值。

`func` 的第四个参数 `ftwbuf` 是指向结构体的指针，定义如下：

```c
struct FTW {
    int base;      /* 路径名基名部分的偏移量 */
    int level;     /* 文件在树遍历中的深度 */
};
```

该结构体的 `base` 字段是 `func` 的 `pathname` 参数中文件名部分（/ 之后的内容）的整数偏移量。`level` 字段是项目相对于遍历起始点的深度（起始点为 level 0）。

`func` 每次被调用时，必须返回一个整数值，该值由 `nftw()` 解释。返回 0 表示继续树遍历；如果所有对 `func` 的调用都返回 0，则 `nftw()` 本身向其调用者返回 0。非零值告诉 `nftw()` 立即停止树遍历，此时 `nftw()` 返回与其返回值相同的非零值。

由于 `nftw()` 使用了动态分配的结构，程序提前终止目录树遍历的唯一方法是从 `func` 返回非零值。使用 `longjmp()`（见第 6.8 节）退出 `func` 可能会导致不可预测的结果——至少会导致程序中出现内存泄漏。

### 示例程序

列表 18-3 展示了 `nftw()` 的用法。

#### 列表 18-3：使用 `nftw()` 遍历目录树

```c
#define _XOPEN_SOURCE 600      /* 获取 nftw() 和 S_IFSOCK 声明 */
#include <ftw.h>
#include "tlpl_dirent.h"

static void
usageError(const char *progName, const char *msg) {
    if (msg == NULL) {
        fprintf(stderr, "Usage: %s [-d] [-m] [-p] [directory-path]\n", progName);
        fprintf(stderr, "\t-d 使用 FTW_DEPTH 标志\n");
        fprintf(stderr, "\t-m 使用 FTW_MOUNT 标志\n");
        fprintf(stderr, "\t-p 使用 FTW_PHYS 标志\n");
        exit(EXIT_FAILURE);
    }
}

static int                /* 被 nftw() 用的函数 */
dirTree(const char *pathname, const stat *sbuf, int type,
    struct FTW *ftw)
```

![](img/f77eaa15a5bf88efd4fac6bc0be0e69d_397_0.png)

列表 18-3 中的程序显示了目录树中文件的缩进层级，每行一个文件，以及文件类型和 i 节点号。可以使用命令行选项来指定调用 `nftw()` 时使用的标志设置。以下 shell 会话显示了运行程序时看到的内容示例。我们首先创建一个新的空子目录，并在其中填充各种类型的项目：

```bash
$ mkdir dir
$ touch dir/a dir/b      创建一些普通文件
$ ln -s -a dir/dsl          以及一个符号链接
$ ln -s x dir/dsl           以及一个悬空符号链接
$ mkdir dir/sub             以及一个子目录
$ touch dir/sub             带有它自己的文件
$ mkdir dir/sub2            另一个子目录
$ chmod 0 dir/sub2          不可读的
```

然后我们使用我们的程序在 `flags` 参数为 0 的情况下调用 `nftw()`：

```bash
$ /nftw_dir_tree dir
D D 2327983 dir
- F 2327984 a
- F 2327985 b
- F 2327984 s1      符号链接 s1 被解析为
1 SLN 2327987 dsl
D D 2327988 sub
- F 2327989 x
d DNR 2327994      sub2
```

在上述输出中，我们可以看到符号链接 s1 已被解析。

接着，我们使用我们的程序在 `flags` 参数包含 `FTW_PHYS` 和 `FTW_DEPTH` 的情况下调用 `nftw()`：

```bash
$ /nftw_dir_tree -p -d dir
- F 2327984 a
- F 2327985 b
1 SL 2327986 s1      符号链接 s1 已解析
1 SL 2327987 dsl
- F 2327989 x
d DP 2327988 sub
d DNR 2327994 sub2
d DP 2327983 dir
```

从上述输出中，我们可以看到符号链接 s1 已经解析了。

### `nftw()` 的 `FTW_ACTIONRETVAL` 标志

从 2.3.3 版本开始，glibc 允许在 `flags` 中指定一个额外的非标准标志。该标志 `FTW_ACTIONRETVAL` 改变了 `nftw()` 解释 `func()` 调用返回值的方式。当指定此标志时，`func()` 应该返回以下值之一：

`FTW_CONTINUE`

继续处理目录树中的项，与传统的返回相同。

`FTW_SKIP_SIBLINGS`

不处理当前项目的兄弟节点。

`FTW_SKIP_TREE`

如果当前项目是目录，则不进入。

`FTW_STOP`

立即停止树遍历。

`FTW_ACTIONRETVAL` 标志允许 `func()` 返回一个特定的值，`nftw()` 随后返回该值。这对于复杂的树遍历逻辑有用。

# 修改当前工作目录

`chdir()` 系统调用将当前进程的工作目录更改为 `pathname` 中指定的相对或绝对路径名（如果是符号链接，则会被引用）。

```c
#include <unistd.h>

int chdir(const char *pathname);
```

成功时返回 0，错误时返回 -1

`fchdir()` 系统调用与 `chdir()` 相同，不同在于目录是通过之前通过 `open()` 打开目录获得的文件描述符来指定的。

```c
#include <unistd.h>

int fchdir(int fd);
```

成功时返回 0，错误时返回 -1

我们可以使用 `fchdir()` 将进程的当前工作目录改为另一个位置，然后返回原始位置，如下所示：

```c
int fd;

fd = open(".", O_RDONLY);
chdir(somepath);
fchdir(fd);
close(fd);

/* 记住我们所在的位置 */
/* 去往别处 */
/* 返回原始目录 */
```

使用 `chdir()` 的等实现如下：

```c
char buf[PATH_MAX];

/* 记住我们所在的位置 */
getcwd(buf, PATH_MAX);
/* 去往其他地方 */
chdir(somepath);
/* 返回原始目录 */
chdir(buf);
```

## 18.1 相目录文件描述符进行操作

从内核 2.6.16 开始，Linux 了一了一系列新的系统调用，它们执行与各种传统调用相似的任务，但提供了对某些应用程序有用的额外功能。这些系统调用汇总在表 18-2 中。我们在本章中描述这些系统调用，是因为它们提供了进程当前工作目录传统语义的变体。
