
参数 `pathname` 指明要删除的目录。如果发生问题，变量 `errno` 可以取以下值：

| 错误 | 含义 |
|---|---|
| EACCES | 进程对 `pathname` 指定目录的父目录没有写权限 |
| EBUSY | pathname 指定的目录正在作为当前目录或进程的根目录使用 |
| EFAULT | pathname 指定的文件名过长 |
| ENAMETOOLONG | pathname 指向一个不存在的文件 |
| ELOOP | 遇到了符号链接 |
| ENOMEM | 内核无法为其内部描述符分配内存 |
| ENOTDIR | pathname 中用作目录名的组件之一不是目录，或 pathname 未指定目录名 |
| ENOTEMPTY | `pathname` 指定的目录不为空 |
| EROFS | 文件系统仅处于读模式 |

## 6.2.3.3 当前目录

所有进程都关联一个当前目录。进程使用的相对文件名是相对于该目录解析的。

系统调用 `chdir` 和 `fchdir` 允许进程更改其当前目录。它们的语法如下：

```c
#include <unistd.h>
```

```c
int chdir (const char *pathname);
```

```c
int fchdir (int fd);
```

`chdir` 使用参数 `pathname` 来指明新当前目录的名字。而 `fchdir` 则使用之前调用底层 `open` 获取的输入/输出描述符（参数 `fd`）。

如果 `chdir` 发生问题，变量 `errno` 可以取以下值：

| 错误 | 含义 |
|---|---|
| EFAULT | pathname 包含无效地址 |
| ENOENT | pathname 指向一个不存在的文件 |
| ENAMETOOLONG | pathname 指定的文件名过长 |
| ELOOP | 遇到了符号链接循环 |
| ENOMEM | 内核无法为其内部描述符分配内存 |
| ENOTDIR | pathname 中用作目录名的组件之一不是目录，或 pathname 未指定目录名 |
| EPERM | 进程没有 `pathname` 指定目录的执行权限 |

此外，`fchdir` 可能会返回错误 `EBADF`，表示描述符 `fd` 无效。

没有系统调用可以直接允许进程获取其当前目录的名字，但库函数 `getcwd` 起到了这个作用。它的语法如下：

```c
#include <unistd.h>
```

```c
char *getcwd (char *buf, size_t size);
```

`getcwd` 在 `buf` 指向的缓冲区中返回当前目录的绝对路径。参数 `size` 指定缓冲区的大小，如果执行成功，`getcwd` 返回的指针为参数 `buf`。如果发生错误，则返回 `NULL`。只有当缓冲区大小太小无法容纳当前目录的绝对路径时，才会返回错误码 `ERANGE`。

## 6.2.3.4 根目录

所有进程都关联一个根目录，它可能与真实的根目录不同。进程使用的文件绝对路径相对于该目录进行解析。通常，该目录对所有进程都是相同的，并对应于文件树结构的根。具有超级权限的进程可以通过系统调用 `chroot` 更改根目录，以便限制在其有权访问的文件结构的子级中。

```c
#include <unistd.h>
```

```c
int chroot (const char *pathname);
```

参数 `pathname` 指定要使用的新根目录的名字。如果成功，`chroot` 返回值 0，当前进程将被限制在指定目录的子级文件和中。如果发生错误，`chroot` 返回值 -1。

如果 `chroot` 发生问题，变量 `errno` 可以取以下值：

| 错误 | 含义 |
|---|---|
| EFAULT | pathname 包含无效地址 |
| ENOENT | pathname 指向一个不存在的文件 |
| ENAMETOOLONG | pathname 指定的文件名过长 |
| ELOOP | 遇到了符号链接循环 |
| ENOMEM | 内核无法为其描述符分配内存 |
| ENOTDIR | pathname 中用作目录名的组件之一不是目录，或 pathname 未指定目录名 |
| EPERM | 进程不是特权进程 |

`chroot` 的主要应用是在受安全原因限制的环境中执行应用程序。

## 6.2.3.5 目录导航

虽然目录像文件一样管理，但进程无法直接访问其内容。为了遍历目录中的项，Linux 提供了三个系统调用：`opendir`、`readdir` 和 `closedir`。它们的语法如下：

```c
#include <sys/types.h>
#include <dirent.h>
#include <unistd.h>
```

```c
DIR *opendir (const char *pathname);
struct dirent *readdir (DIR *dir);
int closedir (DIR *dir);
```

`opendir` 以读模式打开目录并返回一个打开描述符。如果发生问题，变量 `errno` 可以取以下值：

| 错误 | 含义 |
|---|---|
| EACCES | 进程对 `pathname` 指定目录没有写权限 |
| EMFILE | 进程打开的文件最大数已达到 |
| ENFILE | 系统中打开的文件最大数已达到 |
| ENOENT | pathname 指向一个不存在的文件 |
| ENOMEM | 内核无法为其内部描述符分配内存 |
| ENOTDIR | pathname 中用作目录名的组件之一不是目录，或 pathname 未指定目录名 |

`readdir` 对通过 `dir` 传递的目录项执行读取操作。它返回一个指向包含当前目录项特征结构的指针，每次调用 `readdir` 都会替换之前的内容。当遇到文件尾时，返回 `NULL`。

`closedir` 关闭通过参数 `dir` 传递的目录。如果发生错误，变量 `errno` 可以取值 `EBADF`，表示 `dir` 指定的描述符无效。

`dirent` 结构定义在头文件 `<dirent.h>` 中，包含以下字段：

| 类型 | 字段 | 描述 |
|---|---|---|
| long | d_ino | 目录项对应的 inode 节点 |
| unsigned short | d_reclen | 返回的结构的大小 |
| char | d_name | 目录项包含的文件名 |

```c
while (dp !=NULL) {
    printf("%s\n", dp->d_name);
    dp = readdir(dir);
}
    /* 关闭目录 */
    closedir(dir);
    /* 结束程序 */
    exit(0);
}
```

# ListeRep.c

原语 `getdents` 最近被添加到 Linux 内核中。它的操作与 `readdir` 相同，但允许在单次调用中读取多个连续的目录项。语法如下：

```c
#include <unistd.h>
#include <dirent.h>
#include <unistd.h>
int getdents(int fd, struct dirent *dirp, unsigned int count);
```

参数 `fd` 指定与目录关联的输入/输出描述符，`dirp` 包含存储结果的缓冲区地址，而 `size` 表示该缓冲区的字节大小。调用 `getdents` 时，一个或多个 `dirent` 类型结构体的变量被放入缓冲区中，并返回初始化的字节数。为了使用这些结果，必须扫描缓冲区中创建的目录项列表。

如果发生问题，变量 `errno` 可以取以下值：

| 错误 | 含义 |
|---|---|
| EBADF | dir 指定的描述符无效 |
| EFAULT | 路径名包含无效地址 |

以下程序是之前程序的变体：它打开当前目录，通过调用 `getdents` 获取目录项，显示它们，然后关闭目录。

# ListeRep2.c

```c
#include <sys/types.h>
#include <dirent.h>
#include <unistd.h>
#include <errno.h>
```

# 基础系统调用

```c
#include <fcntl.h>
#include <stdio.h>
void main (void) {
    int dir;
    struct dirent *dp;
    char buf[1024];
    int i,
    n;
    /* 打开当前目录 */
    dir = open(".", O_RDONLY);
    if (dir == -1) {
        perror("open");
