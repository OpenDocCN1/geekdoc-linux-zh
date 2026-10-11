
`brk` 将数据段的端设置为 `end_data_segment` 指定的值。

`data_segment` 必须大于文本段的结束，且必须在栈结束之前的 16KB 处。

`sbrk` 按 `increment` 字节增加程序空间。`sbrk` 不是系统调用；它只是一个 C 库包装器。

# 返回值

成功时，`brk` 返回 0，`sbrk` 返回新区域的起始指针。出错时，返回 -1 并设置 `errno` 为 `ENOMEM`。

# 符合

`BSD 4.3`

`brk` 和 `sbrk` 未在 C 标准中定义，并刻意排除在 `POSIX.1` 标准之外（参见段 `B.1.1.3` 和 `B.8.3.3`）。

# 另需

`execve(2)`, `getlimit(2)`, `malloc(3)`, `end(3)`

`Linux 0.99.11`, `1999年7月21日`

# cacheflush

`cacheflush`—刷新指令和/或数据缓存的内容

## 概要

```c
#include <asm/cachectl.h>
int cacheflush(char *addr,int nbytes,intcache);
```

## 描述

`cacheflush` 刷新从 `addr` 到 (`addr+nbytes-1`) 范围内的指定缓存内容。缓存可以是以下之一：

- `ICACHE`: 刷新指令缓存。
- `DCACHE`: 将数据写回内存并使受影响的有效缓存行失效。
- `BCACHE`: 等同于 (`ICACHE|DCACHE`)。

# 返回值

`cacheflush` 成功返回 0，错误时返回 -1。如果检测到错误，`errno` 将指示错误类型。

# 错误

- `EINVAL`: 缓存参数不是 `ICACHE`、`DCACHE` 或 `BCACHE` 之一。
- `EFAULT`: 从 `addr` 到 (`addr+nbytes-1`) 的地址范围部分或全部不可访问。

# 缺陷 (BUG)

当前实现忽略了 `addr` 和 `nbytes` 参数。因此，整个缓存始终会被刷新。

## 注意

此系统仅适用于基于 MIPS 的系统。

## 参见

- `cachectl(2)`

`Linux`, `1995年6月27日`

# chdir, fchdir

`chdir`, `fchdir`—更改工作目录

## 语法概要

```c
#include <unistd.h>
int chdir(const char *path)
int fchdir(int fd);
```

## 描述

`chdir` 将当前目录更改为 `path` 中指定的目录。

`fchdir` 与 `chdir` 相同，只是通过打开的文件描述符来提供目录。

# 返回值

成功时返回 0。错误时返回 -1，并适当地设置 `errno`。

# 错误

取决于文件系统，可能会返回其他错误。此处列出了更通用的错误：

- `EPERM`: 进程对该目录没有执行权限。
- `EFAULT`: `path` 指向你的可访问地址空间之外。
- `ENAMOOLONG`: `path` 太长了。

## 第二部分：系统调用

| `EBADF` | `fd` 不是有效的文件描述符。 |

| `ENOENT` | 文件不存在。 |

| `ENOMEM` | 内内核内存不足。 |

| `ENOTDIR` | 路径前缀的一个组件不是目录。 |

| `EACCES` | 路径前缀的一个组件被拒绝搜索权限。 |

| `ELOOP` | `path` 包含循环引用（即通过符号链接） |

## 参见

`chroot(3)`, `chroot(2)`

`Linux 1.2.4`, `1995年4月15日`

# chmod, fchmod

`chmod`, `fchmod`—更改文件的权限

## 语法概要

```c
#include <sys/types.h>
#include <sys/stat.h>
int chmod(const char *path, mode_t mode);
int fchmod(int fd, mode_t mode);
```

## 描述

文件的模式由 `path` 给出或通过标志引用。

通过给出以下内容指定模式：

| 标志 | 值 | 描述 |
| :--- | :--- | :--- |
| `S_ISUID` | `04000` | 执行时设置用户 ID |
| `S_ISGID` | `02000` | 执行时设置组 ID |
| `S_ISVTX` | `01000` | 粘滞位 (Sticky bit) |
| `S_IRUSR` (`S_READ`) | `00400` | 所有者读 |
| `S_IWUSR` (`S_WRITE`) | `00200` | 所有者写 |
| `S_IXUSR` (`S_EXECUTE`) | `00100` | 所有者执行/搜索 |
| `S_IRGRP` | `00040` | 组读 |
| `S_IWGRP` | `00020` | 组写 |
| `S_IXGRP` | `00010` | 组执行/搜索 |
| `S_IROTH` | `00004` | 其他人读 |
| `S_IWOTH` | `00002` | 其他人写 |
| `S_IXOTH` | `00001` | 其他人执行/搜索 |

进程的有效 `UID` 或 `GID` 必须为 0 或与文件所有者匹配。

取决于文件系统，如果文件被覆盖，设置用户 ID 和组执行位可能会被关闭。在某些文件系统上，超级用户设置了粘滞位，这可能具有特殊含义（即对于目录，文件只能由所有者或超级用户删除）。

# 返回值

成功时返回 0。错误时返回 -1，并适当地设置 `errno`。

# chown, fchown

# 错误

取决于文件系统，可能会返回其他错误。此处列出了 `chmod` 更通用的错误：

- `EPERM` 有效 `UID` 与文件所有者不匹配且不为 0。
- `EROFS` 命名的文件位于只读文件系统中。
- `EFAULT` `path` 指向你的可访问地址空间之外。
- `ENAMETOOLONG` `path` 太长了。
- `ENOENT` 内内核内存不足。
- `ENOTDIR` 路径前缀的一个组件不是目录。
- `EACCES` 路径前缀的一个组件被拒绝权限。
- `ELOOP` `path` 包含循环引用（即通过符号链接）

`chmod` 的通用错误列举如下：

- `EBADF` 描述符不是有效值。
- `ENOENT` 见上文。
- `EPERM` 见上文。
- `EROFS` 见上文。

## 参见

`open(2)`, `chown(2)`

`Linux 0.99`, `1993`

# chown, fchown

`chown`, `fchown`—更改文件的所有者

## 语法概要

```c
#include <sys/types.h>
#include <unistd.h>
int chown(const char *path, uid_t owner, gid_t group);
int fchown(int fd, uid_t owner, gid_t group);
```

## 描述

文件的所有者由 `path` 指定或通过标志引用。

`fchown` 与 `ch` 相同，只是通过打开的文件描述符提供目录。

# 返回值

成功时返回 0。错误时返回 -1，并适当地设置 `errno`。

# 错误

取决于文件系统，可能会返回其他错误。此处列出了 `chown` 更通用的错误：

- `EPERM` 有效 `UID` 与文件所有者不匹配且不为 0；或者组错误。
- `EROFS` 命名的文件位于只读文件系统中。
- `EFAULT` `path` 指向你的可访问地址空间之外。
- `ENAMETOOLONG` `path` 太长了。
- `ENOENT` 内内核内存不足。
- `ENOTDIR` 路径前缀的一个组件不是目录。
- `EACCES` 路径前缀的一个组件被拒绝权限。
- `ELOOP` `path` 包含循环引用（即通过符号链接）

`chmod` 的通用错误列举如下：

- `EBADF` 描述符不是有效值。
- `ENOENT` 见上文。
- `EPERM` 见上文。
- `EROFS` 见上文。

## 参见

`open(2)`, `chown(2)`, `stat(2)`

`Linux 0.99`

# chroot

`chroot`—更改根目录

## 语法概要

```c
#include <unistd.h>
int chroot(const char *path);
```

## 描述

`chroot` 将根目录更改为 `path` 中指定的目录。

对于以 `/` 开头的路径名，将使用根目录。超级用户可以更改根目录。

# 返回值

成功时返回 0。错误时返回 -1，并适当地设置 `errno`。

# 错误

取决于文件系统，可能会返回其他错误。此处列出了通用的错误：

- `EPERM` 有效 `UID` 与文件所有者不匹配且不为 0；或者组错误。
- `EROFS` 命名的文件位于只读文件系统中。
- `EFAULT` `path` 指向你的可访问地址空间之外。
- `ENAMETOOLONG` `path` 太长了。
- `ENOENT` 内内核内存不足。
- `ENOTDIR` 路径前缀的一个组件不是目录。
- `EACCES` 路径前缀的一个组件被拒绝权限。
- `ELOOP` `path` 包含循环引用（即通过符号链接）

## 参见

- `chdir(2)`

# clone

`clone`—创建子进程

## 语法概要
