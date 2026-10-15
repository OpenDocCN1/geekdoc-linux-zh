
```c
struct IO_FILE {
    char    *IO_read_ptr;   /* 当前指针 */
    char    *IO_read_end;   /* get 区域的结束。 */
    char    *IO_read_base; /* 回退和 get 区域的起始。 */
    char    *IO_write_base; /* put 区域的起始。 */
    char    *IO_write_ptr; /* 当前 put 指针。 */
    char    *IO_write_end; /* put 区域的结束。 */
    char    *IO_buf_base;   /* reserve 区域的起始。 */
    char    *IO_buf_end;    /* reserve 区域的结束。 */
    int     fileno;
    int     blksize;
};
typedef struct _IO_FILE FILE;
```

该结构的每个字段将在本章中更详细地分析。然而，首先考虑所有的 `open()` 和 `read()` 系统调用：

```c
fd = open("/etc/passwd", O_RDONLY);
read(fd, buf, 1024);
```

当 `open()` 等系统调用返回一个用于访问文件的文件描述符时，`stdio` 库在一个 `FILE` 结构（或文件流）上操作。这基本上是一个字符缓冲区，保存了足够的信息来记录当前和写入文件指针以及其他辅助信息。在 Linux 上，定义 `FILE` 结构的 `IO_FILE` 结构所示。请注意，这里并没有显示该结构的全部。

## FILE 结构

当 `open()` 等系统调用返回一个用于访问文件的文件描述符时，`stdio` 库在一个 `FILE` 结构（或文件流）上操作。这基本上是一个字符缓冲区，保存了足够的信息来记录当前和写入文件指针以及其他辅助信息。在 Linux 上，定义 `FILE` 结构的 `IO_FILE` 结构所示。请注意，这里并没有显示该结构的全部。

```c
struct IO_FILE {
    char    *IO_read_ptr;   /* 当前指针 */
    char    *IO_read_end;   /* get 区域的结束。 */
    char    *IO_read_base; /* 回退和 get 区域的起始。 */
    char    *IO_write_base; /* put 区域的起始。 */
    char    *IO_write_ptr; /* 当前 put 指针。 */
    char    *IO_write_end; /* put 区域的结束。 */
    char    *IO_buf_base;   /* reserve 区域的起始。 */
    char    *IO_buf_end;    /* reserve 区域的结束。 */
    int     fileno;
    int     blksize;
};
typedef struct _IO_FILE FILE;
```

`de` 字段指向直接范围（文件系统块），而 `des` 字段是范围的大小。

# 标准输入输出库

```c
fp1->fileno = 0x3
Address of fp2 = 0x80499d0
fp2->fileno = 0x4
```

```c
fp1->IO_buf_base = 0x40019000
fp1->IO_buf_end = 0x4001a000
fp2->IO_buf_base = 0x4001a000
fp2->IO_buf_end = 0x4001b000
```

注意，用户可以通过运行 `trace`、`truss` 等工具可以看到该库将执行的相应系统调用。

```bash
$ strace 2>&1 | grep
open("/etc/passwd"
```

注意，程序的 `stdio` 尝试从每个文件流中只读取单个字符，随后的 `getc()` 调用在缓冲区中的所有字符被读取完之前，不需要再次调用 `read()`。

有两个额外的函数可以被调用来打开文件流，即 `fdopen()` 和 `freopen()`：

```c
#include <stdio.h>

FILE *fdopen(int fildes, const char *mode);
FILE *freopen(const char *filename, const char *mode, FILE *stream);
```

`fdopen()` 函数用于将已存在的文件流与文件描述符关联。此函数通常与返回文件描述符的函数（如 `pipe()` 和 `fcntl()`）配合使用。`fdopen()` 打开由 `filename` 指向的文件，并将 `stream` 指向的流与之关联。原始流（如果存在）会首先被关闭。这通常用于将文件与预定义的流之一（标准输入、标准输出或标准错误）相关联。例如，如果调用者希望使用像 `printf()` 这样默认在标准输出上操作的函数，但又想为标准输出使用不同的文件流，该函数可以实现这一预定所需的效果。

# 标准输入输出库缓冲

`stdio` 缓冲数据的目的是尽可能地减少对 `read()` 和 `write()` 系统调用的次数。使用了三种不同类型的缓冲：

- **全缓冲（块缓冲）**。当字符被写入流时，它们会被缓存，直到缓冲区填满。在此阶段，数据会被写入流所引用的文件。类似地，读取操作如果可能，将读取一整个缓冲区的数据。
- **行缓冲**。当字符被写入流时，它们会被缓存，直到写入换行符为止。在此时，包括换行符在内的整行数据会被写入流所引用的文件。读取操作也是如此，字符会一直读取到发现换行符为止。
- **无缓冲**。当输出流无缓冲时，任何写入流的数据都会被立即写入该流流关联的文件。

ANSI C 标准规定输入和输出应该是全缓冲的，而标准错误应该是无缓冲的。通常，标准输入和标准输出被设置为对于终端设备为行缓冲，对于其他设备为全缓冲。

可以使用 `setbuf()` 和 `setvbuf()` 函数来改变流的缓冲特性：

```c
#include <stdio.h>

void setbuf(FILE *stream, char *buf, int type, size_t size);
int setvbuf(FILE *stream, char *buf);
```

缓冲函数必须在流打开之后、对该流进行任何 I/O 操作之前调用。由 `buf` 参数指定的缓冲区将替代 `stdio` 库将使用的缓冲区。这允许调用者根据应用程序的需求优化 `read()` 和 `write()` 调用的次数。

`setvbuf()` 函数可以在任何阶段调用以改变流的缓冲特性。`type` 参数可以是 `_IONBF`（无缓冲）、`_IOLBF`（行缓冲）或 `_IOFBF`（全缓冲）之一。由 `buf` 参数指定的缓冲区至少要有 `size` 字节大。在下一次 I/O 之前，如果流中已经分配了缓冲区，该缓冲区将替换它。如果 `buf` 为 `NULL`，则会改变缓冲模式。

无论使用全缓冲还是行缓冲，都可以使用 `fflush()` 函数强制所有缓冲数据写入流引用的文件，如所示：

```c
#include <stdio.h>

int fflush(FILE *stream);
```

注意，通过将 `stream` 设置为 `NULL` 可以刷新所有输出流。另一个值得提到的点是进程的终止。在进程退出之前，任何当前打开的流都会被刷新并关闭。

# 从/写入读写

有许多 `stdio` 函数用于读写。本节描述了一些可用的函数，并展示了使用不同缓冲选项实现的 `cp` 程序。下所示程序演示了使用 `getc()` 函数读取单个字符对 `FILE` 结构的影响：
