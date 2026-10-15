

```
% gcc48 -w open_close.c
% ./a.out foobar
The file descriptor is 3.
File closed successfully.
%
```

请注意，这是该进程打开的第一个也是唯一一个文件。由于内核已经为该进程打开了标准文件，因此当程序打开 foobar 时，内核分配了文件描述符 3。

我们现在稍微修改程序，使其先关闭标准输入，然后再打开作为命令行参数传递给它的文件。为此，我们只需要在 open() 系统调用之前插入以下行即可：

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

正如你所见，正如预期的那样，内核将文件描述符 0 分配给了新打开的文件 foobar。

## EXERCISE 18.7

编译并运行第 18.8.1 节和 18.8.2 节中给出的程序。它们是否按预期工作？

## 18.8.3 Reading from a File

一旦使用 open() 系统调用打开了文件，就可以使用 read() 系统调用读取其内容。以下是 read() 调用的简要说明。

```
#include <sys/types.h>
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t nbytes);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

此调用尝试从文件描述符为 fd 的文件读取 nbytes 字节到 buf 指向的主内存区域。数据从读写文件指针的当前位置开始读取。完成后，read() 调用返回实际读取的字节数，可能少于 nbytes。文件指针按实际读取的字节数前进。对于普通文件，如果文件在文件结束符 EOF 之前还有这些字节，则调用保证读取 nbytes。然而，对于管道或套接字等其他文件，参见第 19 章和第 20 章，则不能保证。read() 系统调用在遇到 EOF 时返回 0。

失败时，read() 返回 -1，并且 errno 被设置为指示失败原因。表 18.6 显示了 read() 调用对于普通文件失败的一些常见原因。

TABLE 18.6 Some Common Reasons for the read() System Call to Fail

| Reason for failure | Value of errno |
| --- | --- |
| The fd argument is not a valid descriptor for reading. | EBADF |
| The buf argument points to a memory location outside the process address space. | EFAULT |
| An I/O error occurred while reading from the file system. | EIO |
| The file reading operation was interrupted. | EINTR |
| The pointer associated with the fd argument is negative. | EINVAL |
| The nbytes value is greater than INT_MAX, i.e., the maximum value of an integer. | EINVAL |

## 18.4 Writing a File

一旦使用 open() 或 creat() 系统调用打开了文件，就可以使用 write() 系统调用向其写入。以下是 write() 调用的简要说明：

```
#include <sys/types.h>
#include <unistd.h>

ssize_t write(int fd, const void *buf, size_t nbytes);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

此调用尝试从 buf 指向的主内存区域写入 nbytes 字节到文件描述符为 fd 的文件。数据从读写文件指针的当前位置开始写入。完成后，write() 调用返回实际写入的字节数，可能少于 nbytes。文件指针按实际写入的字节数前进。对于普通文件，如果磁盘未满或文件大小未超过 UNIX 系统支持的最大文件大小，则调用保证写入 nbytes。然而，对于套接字等其他文件，参见第 20 章，则不能保证。

### TABLE 18.7 Some Common Reasons for the write() System Call to Fail

| Reason for failure | Value of errno |
| --- | --- |
| The fd argument is not a valid descriptor for writing | EBADF |
| The fd argument is associated with a negative pointer. | EINVAL |
| File size limit for the process or the maximum file size limit has reached | EFBIG |
| The file system containing the file is full. | ENOSPC |
| The user's quota of disk blocks on the file system containing the file has been exhausted. | EDQUOT |
| An I/O error occurred while reading from the file system. | EIO |
| The file reading operation is interrupted. | EINTR |
| The nbytes value is greater than INT_MAX, i.e., the maximum value of an integer. | EINVAL |

我们现在增强 open_close.c 程序并将其转换为文件复制程序 cpy，其语法如下：

```
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);
```

该程序将源文件，即现有文件，复制到目标文件，即不存在的文件。示例程序的编译和执行显示了程序输出。

```
% cat cpy.c
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);
```

