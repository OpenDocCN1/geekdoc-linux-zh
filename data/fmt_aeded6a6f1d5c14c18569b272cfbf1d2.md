
SUSv3 未规定。然而，在其他几个 UNIX 实现中也提供了类似的功能，特别是现代 BSD（参见 `extattr(2)`）以及 Solaris 之后版本（参见 `faattr(5)`）。

EAs 并不在 SUSv3 中规定。然而，在其他几个 UNIX 实现中也提供了类似的功能，特别是现代 BSD（参见 `extattr(2)`）以及 Solaris 之后版本（参见 `faattr(5)`）。

### 16.1 概述

EAs 用于实现访问控制列表（第 17 节）和文件能力（第 39 节）。然而，EAs 的设计足够通用，允许它们用于其他用途。例如，EAs 可以用来记录文件版本号、关于文件的 MIME 类型或字符集的信息，或者（指向一个图形图标的指针）。

SUSv3 未规定 EAs。然而，在其他几个 UNIX 实现中也提供了类似的功能，特别是现代 BSD（参见 `extattr(2)`）以及 Solaris 之后版本（参见 `faattr(5)`）。

EAs 并不在 SUSv3 中规定。然而，在其他几个 UNIX 实现中也提供了类似的功能，特别是现代 BSD。

EAs 在 Btrfs, ext2, ext4, Reiserfs 和 XFS 中支持。

对于 EAs 的支持是可选的，在 Linux 2.6 之后支持。

### 命名空间

EAs 以 `namespace.name` 的形式存在。命名空间用于区分不同的 EA 集合。在给定的命名空间内，EA 的名称是唯一的。

命名空间分为以下几类（user、trusted、sticky、security）：

字体 用户（user）命名空间：允许非特权进程操作。操作这些属性需要相应的权限。在 ext2, ext3, ext4、JFS 等文件系统上，只有显式允许的名称可以操作（根据权限的属性通常是允许的）。

- 可信（trusted）命名空间：与用户命名空间类似，但需要特权（`CAP_SYS_ADMIN`）。操作这些属性需要写入权限。

- 粘滞（sticky）命名空间：在某些文件系统中支持但未实现。

- 安全（security）命名空间：用于存储标签（例如 SELinux, https://www.nsa.gov/research/selinux/）。

os 命名空间：用于旧系统，在某些文件系统中未实现。

### 从 shell 创建和查看 EA

在 shell 中，我们使用 `setattr(1)` 和 `getattr(1)` 命令来设置和查看 EA：

```
$ touch file
$ setattr -n user.x "The past is dead." file
$ setattr -n user.y "In fact, it's not even." file
$ getattr -n user.x file
$ getattr -d file
```

获取单个 EA 的值

`getattr` 的提示信息

`getattr` 命令在每个文件的属性后打印一个空行

导出所有用户 EA 的值

user.x="The past is dead."

user.y="In fact, it's not even."

移除 EA

之前的 shell 会话演示了这样一点：EA 的值可能为空字符串，这与未定义的 EA 不同。（会话结束时，user.x 的值为空字符串，而 user.y 未定义）。

默认情况下，`getattr` 只列出用户 EA 的值。可以使用 `-m` 选项指定一个正则表达式模式来选择要显示的的 EA 名称：

```
$ getattr -m 'pattern' file
```

模式默认值为 `^user\.`。我们可以使用以下命令列出文件中所有的 EA：

```
$ getattr -m - file
```

### 16.2 扩展属性实现细节

在本节中，我们将扩展前节的概述，以填充 EAs 实现的一些细节。

用户扩展属性的限制

只有文件和目录可以放置用户扩展属性。其他文件类型被排除的原因如下：

- 对于符号链接，所有用户都拥有所有权限，且这些权限无法更改。（符号链接权限在 Linux 上没有意义，参见第 18.2 节）。这意味着无法通过权限防止任意属性在符号链接上放置用户 EA。解决方法是防止所有用户在符号链接上创建用户 EA。

- 对于设备文件、套接字和 FIFO，权限控制了用户执行底层 I/O 操作的访问权限。操纵这些权限来控制用户 EA 的创建将与此问题冲突。

这可以防止任意用户向如 `/tmp` 等目录附加扩展属性（EA），这些目录是公共可写的的（因此允许任意用户操作该目录上的 EA），但它们设置了粘滞位（sticky bit），以防止用户删除目录中属于其他用户的 EA。

## 实现限制

Linux VFS 对所有文件系统上的 EA 施加了以下限制：

- EA 名称的长度限制为 255 个字符。

- EA 值限制为 64 kB。

此外，某些文件系统对与文件关联的 EA 大小数量实施了更严格的限制：

- 在 ext2、ext3 和 ext4 上，文件上名称和所有 EA 使用的总字节数被限制为逻辑磁盘块的大小（第 14.3 节）：1024、2048 或 4096 字节。

- 在 JFS 上，文件上所有 EA 名称和值所使用的总字节数有一个 128 kB 的上限。

## 操作扩展属性的系统调用

在本节中，我们将查看用于更新、检索和删除 EA 的系统调用。

## 创建和修改 EA

`setattr()`、`lsetattr()` 和 `fsetattr()` 系统调用用于设置文件某个 EA 的值。

```
#include <sys/xattr.h>
int setattr(const char *pathname, const char *name, const void *value,
    size_t size, int flags);
int lsetattr(const char *pathname, const char *name, const void *value,
    size_t size, int flags);
int fsetattr(int fd, const char *name, const void *value,
    size_t size, int flags);

成功时均返回 0，错误时返回 -1
```

这三个调用之间的区别与 `stat()`、`lstat()` 和 `fstat()` 类似（第 15.1 节）：

- `setattr()` 通过路径名识别文件，如果是符号链接，则对文件名进行引用；

- `lsetattr()` 通过路径名识别文件，但不符号符号进行引用；

- `fsetattr()` 通过打开的文件描述符 `fd` 识别文件。

同样的区别也适用于本节其余部分描述的其他组系统调用。

`name` 参数是一个以空结尾的字符串，定义 EA 的名称。`value` 参数是一个指向缓冲区的指针，定义 EA 的新值。`size` 参数指定了该缓冲区的长度。

默认情况下，如果给定的名称不存在，这些系统调用将创建一个新的 EA；如果 EA 已经存在，则替换该 EA 的值。`flags` 参数提供了对此行为更细粒度的控制。它可以被指定为 0 或以下常量之一：

```
XATTR_CREATE
```

如果已存在具有给定名称的 EA，则失败（返回 `EEXIST`）。

```
XATTR_REPLACE
```

如果不存在具有给定名称的 EA，则失败（返回 `ENODATA`）。

以下是一个使用 `setxattr()` 创建用户 EA 的示例：

```
char *value;

value = "The past is not dead.";

if (setxattr(pathname, "user.x", value, strlen(value), 0) == -1)
    errExit("setxattr");
```

## 检索 EA 的值

`getxattr()`、`listxattr()` 和 `fgetattr()` 系统调用检索 EA 的值。

```
#include <sys/xattr.h>

size_t getxattr(const char *pathname, const char *name, void *value,
               size_t size);
size_t listxattr(const char *pathname, const char *name, void *value,
               size_t size);
size_t fgetattr(int fd, const char *name, void *value,
               size_t size);

成功时返回 EA 值的（非负）大小，错误时返回 -1
```

`name` 参数是一个以空结尾的字符串，用于识别我们想要检索的 EA。EA 值返回在由 `value` 指向的缓冲区。该缓冲区必须由调用者分配，且其长度必须在 `size` 中指定。成功时，这些系统调用返回复制到 `value` 中的字节数。

如果文件没有给定名称的属性，系统调用将以错误 `ENODATA` 失败。如果 `size` 太小，这些系统调用将以错误 `ERANGE` 失败。

可以将 `size` 指定为 0，在这种情况下 `value` 被忽略，但系统调用会返回 EA 值的大小。这提供了一种机制，用于确定后续实际检索 EA 值调用时所需的缓冲区大小。然而，我们无法保证在随后尝试检索值时，返回的大小足够大。在此期间，另一个进程可能为该属性分配了更大的值，或者完全删除了该属性。

## 删除 EA

`removevexattr()`、`lremovevexattr()` 和 `fremovexattr()` 系统调用从文件中删除 EA。

```
#include <sys/xattr.h>

int removevexattr(const char *pathname, const char *name);
int lremovevexattr(const char *pathname, const char *name);
int fremovexattr(int fd, const char *name);

    成功时返回 0，错误时返回 -1
```

`name` 中以空结尾的字符串识别要删除的 EA。尝试删除不存在的 EA 将以错误 `ENODATA` 失败。

## 检索关联的 EA 名称

`listxattr()`、`llistxattr()` 和 `fgetattr()` 系统调用检索与文件关联的 EA 名称列表。

```
#include <sys/xattr.h>

size_t listxattr(const char *pathname, const char *name, void *value,
               size_t size);
size_t llistxattr(const char *pathname, const char *name, void *value,
               size_t size);
size_t fgetattr(int fd, const char *name, void *value,
               size_t size);

    成功时返回字节数，错误时返回 -1
```

EA 名称列表以一系列空结尾的字符串形式返回在 `list` 指向的缓冲区中。该缓冲区必须由调用者分配，且其长度必须在 `size` 中指定。成功时，这些系统调用返回 EA 值的字节数。

可以将 `size` 指定为 0，在这种情况下 `list` 被忽略，但系统调用会返回 EA 值的大小。这提供了一种机制，用于确定后续实际检索 EA 值调用时所需的缓冲区大小。然而，我们无法保证在随后尝试检索值时，返回的大小足够大。在此期间，另一个进程可能为该属性分配了更大的值，或者完全删除了该属性。

检索关联的 EA 名称只需要该文件是可访问的（即你对目录具有执行权限）。出于安全原因，特权进程获取的列表可能包含其没有访问权限的属性。但请注意前句中的“可能”（may），这表明文件系统实现并没有义务这样做。

## 示例程序

列表 16-1 检索并显示命令行列出的文件的 EA 名称和值。对于每个文件，程序使用 `listxattr()` 检索所有 EA 名称，并对每个名称执行 `getxattr()` 以检索对应的值。默认情况下，属性值以文本显示。如果提供了 `-x` 选项，则属性值以十六进制字符串显示。以下 shell 会话演示了该程序的使用：

```
$ setxattr -n user.x -v "The past is not dead." tffile
$ setxattr -n user.y -v "In fact, it's not past." tffile
$ ./xattr_view tffile
```

```
tfile:
name=user.x; value=The past is not dead.
name=user.y; value=In fact, it's not even past.
```

# 列表 16-1: 显示文件扩展属性

```
#include <sys/xattr.h>
#include <tlpi_hdr.h>

#define XATTR_SIZE 10000

static void
usageError(char *progName)
{
    printf(stderr, "Usage: %s [-x] file...\n", progName);
    exit(EXIT_FAILURE);
}

int
main(int argc, char *argv[])
{
    char list[XATTR_SIZE], value[XATTR_SIZE];
    ssize_t listlen, valelen;
    int ns, j, k, opt;
    Boolean hexDisplay;
    hexDisplay = 0;
    while ((opt = getopt(argc, argv, "xt")) != -1) {
        switch (opt) {
            case 'x': hexDisplay = 1;      break;
            case 't': usageError(argv[0]);
        }
    }

    if (optind >= argc + 2)
        usageError(argv[0]);
```
