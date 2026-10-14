
```
};
```

该结构在每次调用 `readdir()` 时都会被覆盖。这些非标准字段中最有趣的是上述 `dirent` 结构中的类型。

`rewinddir()` 函数将目录流移回开头，以便下一次调用 `readdir()` 再次从目录中的第一个文件开始。

```c
#include <dirent.h>

void rewinddir(DIR *dirp);
```

`closedir()` 函数关闭由 `dirp` 引的打开目录流，释放流使用的资源。

```c
#include <dirent.h>

closedir(DIR *dirp);
```

两个函数 `telldir()` 和 `seekdir()` 在 SUSv3 中也有规定，它们允许在目录流中进行随机访问。有关这些函数的更多信息请参考手册页。

## 目录流与文件描述符

目录流关联有一个文件描述符。`dirfd()` 函数返回与 `dirp` 所指的目录流相关的文件描述符。

```c
#define BSD_SOURCE  /* #define SVID_SOURCE */
#include <dirent.h>

int dirfd(DIR *dirp);
```

例如，我们可以将 `dirfd()` 返回的文件描述符传递给 `fchdir()`（第 18.10 节），以更改相应目录当前的工作目录。或者，我们可能将文件描述符作为进程传递给第 18.11 节中描述的函数之一的 `dirfd` 参数。

> `dirfd()` 函数也出现在 BSD 系统上，但在其他实现中也存在。它在 SUSv3 中未规定，但在 SUSv4 中进行了规定。

在此值得提到，`open()` 会为目录流关联的文件描述符设置 `close-on-exec` 标志（`FD_CLOEXEC`）。这确保了执行 `exec()` 时文件描述符会自动关闭。（这在第 27.4 节中有描述。）

## 示例程序

示例 1-2 使用 `opendir()`、`readdir()` 和 `closedir()` 列出命令行中指定的每个目录的内容（如果没有提供参数，则列出当前工作目录）。以下是该程序的使用示例：

```bash
$ mkdir sub
$ touch sub/a sub/b
$ ./list_files sub
sub/a
sub/b
```

在测试目录中创建某些文件

列出目录

## 示例 18-2：扫描目录

```c
#include <dirent.h>
#include <tlpi_hdr.h>

static void      /* 列出 'dirpath' 中的所有文件 */
listfiles(const char *dirpath)
{
    DIR *dir;
    struct dirent *dp;
    Boolean isCurrent;      /* 如果 dirpath 为 "." 则为真 */

    isCurrent = strcmp(dirpath, ".*") == 0;
    dir = opendir(dirpath);
    if (dir == NULL) {
        errMsg("opendir failed on %s", dirpath);
        return;
    }

    /* 对于目录中的每个条目，打印目录+文件名 */
    for (;;) {
        errno = 0;          /* 区分错误与目录结束 */
        dp = readdir(dir);
        if (dp == NULL)
            break;

        if (strcmp(dp->d_name, ".*") == 0 || strcmp(dp->d_name, "..") == 0)
            continue;      /* 跳过 . 和 .. */

        if (!isCurrent)
            printf("%s/", dirpath);
        printf("%s\n", dp->d_name);
        isCurrent = 1;
    }

    if (errno != 0)
        errMsg("readdir");

    if (closedir(dir) == -1)
        errMsg("closedir");
}

int
main(int argc, char *argv[])
{
    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usage("%s [dir...]\n", argv[0]);

    if (argc == 1)      /* 无参数 - 使用当前目录 */
        listfiles(".");
else
  for (argv++; *argv; argv++)
    listfiles(*argv);

exit(EXIT_SUCCESS);
```

--- `dirs_links/list_file.c`

## readdir_r() 函数

`readdir_r()` 函数是 `readdir()` 的变体。`readdir_r()` 和 `readdir()` 关键语义区别在于前者是重入的，而后者不是。因为 `readdir_r()` 通过调用者提供的参数返回文件条目，而 `readdir()` 通过静态分配的结构体返回。我们在第 21.1.2和31.1节中讨论了重入性。

```c
#include <dirent.h>
int readdir_r(DIR *dirp, struct dirent *entry, struct dirent **result);
// 成功时返回0，错误时返回正整数
```

给定 `dirp`（之前通过 `opendir()` 打开的目录），`readdir_r()` 将关于下一个条目的信息放入调用者提供的结构中。此外，该结构的指针被放入 `result`。如果到达目录流的末尾，则在 `result` 中放入 `NULL`（而 `readdir()` 返回 0）。出错时，`readdir_r()` 不返回 -1，而是返回对应 `errno` 值的正整数。

在 Linux 上，结构体的 `d_name` 字段是一个 256 字节的数组，足够容所需的文件名。尽管其他几个 UNIX 实现定义了相同的 `d_name` 大小，但 SUS 未指定该字段，某些 UNIX 实现将其定义为 1 字节数组。执行此操作时，应用程序应如下分配结构：

```c
struct dirent *entry;
size_t len;

len = offsetof(struct dirent, d_name) + NAME_MAX + 1;
entry = malloc(len);
if (entry == NULL)
  errExit(malloc);
```

使用 `offsetof()` 宏（定义在 `<stddef.h>` 中）可以避免对特定实现的依赖。`nftw()` 函数允许通过为目录中的每个文件调用程序员定义的函数来遍历整个树。`nftw()` 函数是旧版本 `ftw()` 的增强，提供了处理符号链接更大的灵活性。

```c
#define _OPEN_SOURCE 500
#include <ftw.h>

int nftw(const char *dirpath, int (*func)(const char *pathname, struct stat *statbuf, int typeflag, int openfd, int flags);
// 成功遍历整个树后返回0，错误时返回-1
```

`nftw()` 的 `flags` 参数通过对以下零或多个常量进行位或（`|`）创建，这些常量会修改函数的执行：

- `FTW_CHDIR`：在处理内容之前进入每个目录执行 `chdir()`。这对于在文件所在的目录执行工作很有用。

- `FTW_DEPTH`：对目录树进行后序遍历。这意味着 `nftw()` 在对目录本身执行 `func` 之前，先对目录内的所有文件和子目录调用 `func`。（该标志名称具有误导性——`nftw()` 总是执行深度优先而非宽度优先遍历。）

- `FTW_MOUNT`：不要跨越另一个文件系统。因此，如果树的一个子目录是挂载点，则不进行遍历。

- `FTW_PHYS`：默认情况下，`nftw()` 会引用符号链接。此标志告诉它不要这样做。相反，符号链接将带有 `FTW_SL` 的 `typeflag` 传递给 `func`，如下所示。
