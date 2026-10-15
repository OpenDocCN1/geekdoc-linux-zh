
| `O_WRONLY` | 仅以只写方式打开文件。 |

| `O_RDWR` | 以读写方式打开文件。 |

| `O_CREAT` | 如果文件不存在则创建文件。如果你使用此选项，必须将新创建文件的访问权限作为第三个参数 `mode` 指定。 |

| `O_APPEND` | 每次写操作都在文件末尾追加。 |

| `O_TRUNC` | 如果文件存在，其长度将被设置为 0。以前的文件内容将不再可访问。 |

# 表 18.4 `open()` 系统调用失败的几个常见原因

| 失败原因 | `errno` 的值 |
|---|---|
| 路径中的某个组件不存在。 | `ENOENT` |
| 路径中的某个组件不是目录。 | `ENOTDIR` |
| 指定的文件是一个目录。 | `EISDIR` |
| 路径中的某个组件未设置搜索权限。 | `EACCESS` |
| 进程已打开系统允许的最大文件数，即 `PPFDT` 已满。 | `EMFILE` |
| 系统已达到可同时打开的最大文件数限制（即系统范围的文件表已满）。 | `EMFILE` |
| 文件打开操作被信号中断。 | `EINTR` |
| 路径中的某个组件超过文件名大小限制（255 个字符）或整个路径超过 1023 个字符。 | `ENAMETOOLONG` |
| 指定的文件是特殊文件，但与该文件关联的设备不存在。 | `ENXIO` |
| 指定了 `O_CREAT` 标志以创建文件，但文件系统为只读。 | `EROFS` |
| 指定了 `O_CREAT` 标志且在为新文件创建 inode 或为待创建文件创建目录项时发生错误。 | `EIO` |
| 指定了 `O_CREAT` 和 `O_EXCL` 标志且路径中指定的文件已存在。 | `EEXIST` |

`open()` 系统调用会跟随符号链接并访问该链接指向的文件的数据或属性。如果您想读取符号链接的数据或属性，则必须使用 `readlink()` 系统调用。同样，`creat()` 系统调用只能创建普通文件。如果您想创建符号链接，应使用 `symlink()` 系统调用。您应浏览这些调用的手册页以了解更多信息。

## 练习 18.6

给出 `symlink()` 和 `readlink()` 系统调用的原型。简要描述这些调用的每个参数。

## 18.8.2 关闭文件

您可以使用 `close()` 系统调用关闭文件，该调用以文件描述符作为参数并释放与给定描述符对应的 `PPFDT` 槽位。以下是该调用的简要描述。

```
#include <unistd.h>
int close(int fd);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

`close()` 系统调用可能因多种原因而失败。两个常见的原因在表 18.5 中给出，并附有与这些错误对应的 `errno` 变量的符号值。

# 表 18.5 `close()` 系统调用失败的常见原因

| 失败原因 | `errno` 的值 |
|---|---|
| `fd` 不是活动描述符，即不对应已打开的文件。 | `EBADF` |
| 文件关闭操作被信号中断。 | `EINTR` |

如果一个已打开的文件被多个进程引用——也就是说，如果多个 `PPFDT` 中的条目指向 `SFT` 中的一个条目——则关闭文件只会释放相关 `PPFDT` 中的条目并将引用计数减一。只有当该引用计数变为零时，文件才会被关闭。当进程终止时，内核会自动关闭其所有已打开文件。

在下面的示例中，我们打开作为唯一命令行参数传递的文件，显示该文件的描述符，然后关闭该文件。示例程序的编译和执行显示了程序输出。请注意，默认编译器命令在 Solaris 和 PC-BSD 上分别为 `gcc` 和 `gcc48`。我们展示了在 BSD 系统上编译程序。我们使用带有 `-w` 选项的编译器命令以抑制警告信息。

```
% cat open_close.c
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int fd;

    /* Open file */
    if (argc == 1) {
        printf("No file specified as command line argument.\n");
        exit(1);
    }
    if ((fd = open(argv[1], O_RDONLY)) == -1) {
        perror("File opening");
        exit(1);
    } else
        printf("The file descriptor is %d.\n",fd);
    /* Close file */
    if (close(fd) == -1) {
        perror("File closing");
        exit(1);
    }
    else
        printf("File closed successfully.\n");
    exit(0);
}
```

```
% gcc48 -w open_close.c
% ./a.out foobar
The file descriptor is 3.
File closed successfully.
%
```

请注意，这是该进程打开的第一个也是唯一一个文件。由于内核已经为该进程打开了标准文件，因此当程序打开 `foobar` 时，内核分配了文件描述符 3。

我们现在稍微修改程序，使其先关闭标准输入，然后再打开作为命令行参数传递给它的文件。为此，我们只需要在 `open()` 系统调用之前插入以下行即可：

```
close(0);
```

以下是更新后的程序：

```
% cat open_close.c
#include <fcntl.h>
#include <unistd.h>
int main(int argc, char *argv[])
{
    int fd;
    /* Open file */
    if (argc == 1) {
        printf("No file specified as command line argument.\n");
        exit(1);
    }
    close(0); /* Close standard input */
    if ((fd = open(argv[1], O_RDWR)) == -1) {
        perror("File opening");
        exit(1);
    } else
        printf("The file descriptor is %d.\n",fd);
    /* Close file */
    if (close(fd) == -1) {
        perror("File closing");
        exit(1);
    }
    else
        printf("File closed successfully.\n");
    exit(0);
}
% gcc48 -w open_close.c
% ./a.out foobar
```

The file descriptor is 0.

File closed successfully.

%

正如你所见，正如预期的那样，内核将文件描述符 0 分配给了新打开的文件 `foobar`。

## EXERCISE 18.7

编译并运行第 18.8.1 节和 18.8.2 节中给出的程序。它们是否按预期工作？

## 18.8.3 Reading from a File

一旦使用 `open()` 系统调用打开了文件，就可以使用 `read()` 系统调用读取其内容。以下是 `read()` 调用的简要说明。

```
#include <sys/types.h>
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t nbytes);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

此调用尝试从文件描述符为 `fd` 的文件读取 `nbytes` 字节到 `buf` 指向的主内存区域。数据从读写文件指针的当前位置开始读取。完成后，`read()` 调用返回实际读取的字节数，可能少于 `nbytes`。文件指针按实际读取的字节数前进。对于普通文件，如果文件在文件结束符 `EOF` 之前还有这些字节，则调用保证读取 `nbytes`。然而，对于管道或套接字等其他文件，参见第 19 章和第 20 章，则不能保证。`read()` 系统调用在遇到 `EOF` 时返回 0。

失败时，`read()` 返回 -1，并且 `errno` 被设置为指示失败原因。表 18.6 显示了 `read()` 调用对于普通文件失败的一些常见原因。

TABLE 18.6 Some Common Reasons for the `read()` System Call to Fail
