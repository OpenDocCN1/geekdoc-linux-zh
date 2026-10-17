
权限标志与此前的`open`系统调用相同。文件类型标志包括：

- `S_IFBLK`: 条目是块特殊设备
- `S_IFDIR`: 条目是目录
- `S_IFCHR`: 条目是字符特殊设备
- `S_IFIFO`: 条目是 FIFO（命名管道）
- `S_IFREG`: 条目是普通文件
- `S_IFLNK`: 条目是符号链接

## 第3 章

其他模式标志包括：

- `S_ISUID`: 条目在执行时设置了 UID
- `S_ISGID`: 条目在执行时设置了 GID

用于解释`st_mode`标志的掩码包括：

- `S_IFMT`: 文件类型
- `S_IRWXU`: 用户读/写/执行权限
- `S_IRWXG`: 组读/写/执行权限
- `S_IRWXO`: 其他人的读/写/执行权限

定义了一些确定文件类型的宏。这些宏只需将经过适当掩码的模式标志与合适的设备类型标志进行比较。它们包括：

- `S_ISBLK`: 测试为块特殊文件
- `S_ISCHR`: 测试为字符特殊文件
- `S_ISDIR`: 测试为目录
- `S_ISIFO`: 测试为 FIFO
- `S_ISREG`: 测试为普通文件
- `S_ISLNK`: 测试为符号链接

例如，要测试文件不是目录，且所有者具有执行权限但没有其他模式，可以使用以下测试：

```c
struct stat statbuf;
mode_t modes;

stat("filename",&statbuf);
modes = statbuf.st_mode;

if(!S_ISDIR(modes) && (modes & S_IRWXU) == S_IXUSR)
..
```

## dup 和 dup2

`dup`系统调用提供了一种复制文件描述符的方法，为我们提供两个或多个访问相同文件的不同描述符。这些描述符可以用于在文件的不同位置进行读写。`dup`系统调用复制文件描述符`fd`，返回一个新的描述符。`dup2`系统通过指定用于复制的描述符，有效地将一个文件描述符复制到另一个。

## 操作文件（继续）

以下是语法：

```c
#include <unistd.h>

int dup(int fd);
int dup2(int oldfd, int newfd);
```

## 标准 I/O 库

标准 I/O 库提供了一个通用的输入输出接口。它通过`stdio.h`提供了许多用于格式化、扫描和引用数据的函数。
