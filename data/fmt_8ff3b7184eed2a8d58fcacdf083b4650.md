
# 列表 A.4 (number.c) 一元数实现

```c
/* 对一元数进行操作。 */

#include <assert.h>
#include <stdlib.h>
#include <limits.h>
#include "definitions.h"

/* 创建一个表示零的数字。 */
number make_zero ()
{
    return 0;
}

/* 如果数字表示零，则返回非零。 */
int zerop (number n)
{
    return n == 0;
}

/* 将一个正数减 1。 */
number decrement_number (number n)
{
    number answer;
    assert (zerop (n));
    answer = n->one_less_;
    free (n);
    return answer;
}

/* 给数字加 1。 */
number add_one (number n)
{
    number answer = malloc(sizeof (struct LinkedListNumber));
    answer->one_less_ = n;
    return answer;
}

/* 销毁一个数字。 */
void destroy_number (number n)
{
    while (!zerop (n)) {
        n = decrement_number (n);
    }
    free(n);
}

/* 拷贝一个数字。需要此函数仅是因为内存分配的原因。 */
number copy_number (number n)
{
    number answer = make_zero ();
    while (!zerop (n)) {
        answer = add_one (answer);
        n = decrement_number (n);
    }
    return answer;
}

/* 相加两个数字。 */
number add (number n1, number n2)
{
    number answer = copy_number (n2);
    while (!zerop (n1)) {
        answer = add_one (answer);
        n1 = decrement_number (n1);
    }
    return answer;
}

/* 从另一个数字中减去一个。 */
number subtraction (number n1, number n2)
{
    number answer = copy_number (n1);
    while (!zerop (n2)) {
        answer = decrement_number (answer);
    }
    return answer;
}

/* 返回两个数字的积。 */
number product (number n1, number n2)
{
    // 实现省略以保持简练
    return 0;
}
```

## B 低级 I/O (输入输出)

`GNU/Linux` 上的程序员可以使用两套输入/输出函数。标准 C 库 I/O 函数提供了 `printf`、`fopen` 等函数¹。`Linux` 内核本身提供了另一组 I/O 操作，其运行级别比 C 库函数更低。

由于本书是为已经熟悉 C 语言的人编写的，我们假设你已经遇到过并知道如何使用 C 库 I/O 函数。

通常有充分的理由使用 `Linux` 的底层 I/O 函数。其中许多是内核系统调用，为应用程序提供了对底层能力最直接的访问。事实上，标准 C 库 I/O 程序是实现在 `Linux` 低级 I/O 系统调用之上的。使用后者通常是执行输入输出操作最高效的方法——有时也更加方便。

- + 1. C++ 标准库提供了具有类似功能的 `istream`。C++ 语言同样可以使用标准 C 库。
- 2. 请参阅第 8 章“`Linux` 系统调用”，了解系统调用与普通函数调用之间的区别。

在本书中，我们假设你熟悉本附录中所描述的调用。你可能已经熟悉了它们，因为它们与其他 `UNIX` 和类 `UNIX` 操作系统（以及 `Win32` 平台）提供的调用几乎相同。然而，如果你不熟悉，请继续读下去；如果你先熟悉这些材料，你会发现本书的其他部分更容易理解。

### B.1 读取和写入数据

你在学习 C 语言时可能遇到的第一个 I/O 函数是 `printf`。它将格式化一个文本字符串并将其打印到标准输出。通用版本 `fprintf` 可以将文本打印到标准输出以外的流中。流由 `FILE*` 指针表示。你通过 `fopen` 打开文件来获取 `FILE*` 指针。除了 `fprintf`，你还可以用 `fclose` 关闭它。你可以使用 `fput`、`fputs` 和 `fwrite` 等函数向流写入数据，或使用 `scanf`、`fscanf`、`gets` 和 `fread` 读取数据。

使用 `Linux` 低级 I/O 操作时，你使用称为文件描述符（file descriptor）的句柄而不是 `FILE*` 指针。文件描述符是一个整数，指向单个进程中的特定打开文件。它可以以读、写或读写模式打开。文件描述符并不一定指向一个打开的文件；它也可以代表与能够发送或接收数据的另一个系统组件的连接。例如，请参阅第 6 章“设备”，如打开的套（见第 5 章“进程间通信”，第 5.5 节“`Sockets`”）或管道的一端（见第 5.4 节“`Pipes`”）。

如果你使用此处描述的任何低级 I/O 函数，请包含头文件 `<stdio.h>`、`<sys/types.h>`、`<sys/stat.h>` 和 `<unistd.h>`。

#### B.1.1 打开文件

要打开文件并生成访问该文件的描述符，使用 `open` 调用。它以文件路径（字符字符串）和指定打开方式的标志作为参数。你可以使用 `open` 创建新文件；如果是这样，传递第三个参数来指定新文件的访问权限。

如果第二个参数是 `O_RDONLY`，则文件以只读模式打开；如果你随后尝试写入生成的文件描述符，将会报错。同样，`O_WRONLY` 导致文件描述符为只写。指定 `O_RDWR` 会产生一个可以同时读取和写入的文件描述符。注意，并非所有文件都可以在所有三种模式下打开。例如，文件的权限可能会禁止特定进程以读或写方式打开；只读设备（如 `CD-ROM` 驱动器）上的文件可能无法以写打开。

你可以通过将此值与一个或多个标志进行位或运算来指定额外的选项。这些是最常用的值：

- `O_TRUNC`：如果打开的文件之前存在，则将其截断。写入文件描述符的数据将替换文件之前的内容。
- `O_APPEND`：向现有文件追加内容。写入文件描述符的数据将将添加到文件末尾。
- `O_CREATE`：创建一个新文件。如果你提供给 `open` 的文件名不存在，且该文件目录存在且进程有权限在该目录下创建文件，则将创建一个新文件。如果文件已存在，则打开它。
- `O_EXCL` 配合 `O_CREATE` 使用，强制创建一个新文件。如果文件已存在，调用将失败。

如果你带有 `O_CREATE` 调用 `open`，请提供一个额外的参数来指定新文件的权限。请参阅第 10 章“安全”，第 10.3 节“文件系统权限”，获取权限位及其使用方法的描述。

例如，列表 B1 中的程序根据命令行上指定的文件名创建一个新文件。如果你在调用 `open` 时使用 `O_EXCL` 标志，那么如果文件已存在，就会发生错误。新文件将赋予所有者和所属组读写权限，并仅赋予其他人读取权限（如果你的 `umask` 设置为非零值）。

#### Umasks

当你创建一个文件时，`umask` 决定了权限。`umask` 被设置为非零值。要更改 `umask`，请使用 `umask` 命令并指定数值。例如，`umask 0022` 设置权限，使所有者具有读写访问权限，而组和其他人只有读取权限。

要更改 `umask`，请使用 `umask` 命令并指定数值。例如，`umask 0022` 设置权限，使所有者具有读写访问权限，而组和其他人只有读取权限。

`umask` 是一个掩码，用于从新创建的文件中屏蔽某些权限。例如，如果 `umask` 为 0022，用权限 0666 创建的文件将具有 0644 (`rw-r--r--`) 权限。

`umask` 是一个掩码，用于从新创建的文件中屏蔽某些权限。例如，如果 `umask` 为 0022，用权限 0666 创建的文件将具有 0644 (`rw-r--r--`) 权限。

#### B.1.2 关闭描述符

当你完成文件描述符的操作后，应该关闭它。在某些情况下（如 B1 中的程序），没有必要显式关闭，因为进程会终止。

`Linux` 限制了进程同时允许打开的文件描述符数量。典型的限制是每个进程 1024 个描述符。你可以使用 `setlimit` 系统调用调整此限制；请查看第 8.5 节“`getlimit` 和 `setlimit`”获取更多信息。

#### B.1.3 写入数据

使用文件描述符、缓冲区指针和写入字节数向文件描述符写入数据。文件描述符必须已打开。写入的数据不需要字符串；`write` 将任意字节复制到文件描述符。

列表 B2 中的程序将当前时间追加到命令行指定的。。如果文件不存在，则会创建它。此程序还使用了 `time`、`localtime` 和 `ctime` 函数来获取并格式化当前时间；请查看各自的手页（man pages）获取更多信息。

##### 附录 B 代码示例

```c
char* get_timestamp() {
    time_t now = time(NULL);
    return asctime(localtime(&now));
}

int main (int argc, char *argv[]) {
    /* 要追加时间戳的文件。 */
    char *filename = argv[1];
    /* 获取当前时间戳。 */
    char *timestamp = get_timestamp();
    /* 以写模式打开文件。如果存在则追加；否则创建一个新文件。 */
    int fd = open(filename, O_WRONLY | O_CREATE | O_APPEND, 0666);
    /* 计算时间戳字符串的长度。 */
    size_t length = strlen(timestamp);
    /* 将时间戳写入文件。 */
    write(fd, timestamp, length);
    /* 完成。 */
    close(fd);
    return 0;
}
```

`## 286 附录 B 低级 I/O`

以下 `timestamp` 程序的工作原理如下：

```bash
% ./timestamp tsfile
% cat tsfile
Thu Feb 1 23:25:20 2001
% ./timestamp tsfile
% cat tsfile
Thu Feb 1 23:25:20 2001
Thu Feb 1 23:25:47 2001
```

注意，当我们第一次调用 `timestamp` 时，它创建文件 `tsfile`，而第二次调用时则是追加到该文件中。

`write` 调用返回实际写入的字节数，如果发生错误则返回 -1。对于某些类型的文件描述符，写入的字节数可能少于请求的字节数。在这种情况下，由你再次调用 `write` 来写入剩余数据。函数 B.3 演示了如何这样做。请注意，对于某些应用程序，你可能需要在写入操作中间检查特殊情况。例如，如果你正在向网络套接字写入，你必须增强此函数以检测网络连接是否在写入操作过程中已关闭，如果是，则必须做出适当反应。

##### 列表 B.3 `(write-all.c)` 写入缓冲区中的所有数据

```c
/* 将 BUFFER 中的所有 COUNT 字节写入文件描述符 FD。
   出错时返回 -1，或返回写入的字节数。 */

size_t write_all(int fd, const void* buffer, size_t count)
{
    size_t left_to_write = count;
    while (left_to_write > 0) {
        size_t written = write(fd, buffer, count);
        if (written == -1)
            /* 发生错误；退出。 */
            return -1;
        else
            /* 记录我们还需要写入多少字节。 */
            left_to_write -= written;
    }
    /* 我们写入的内容应该超过 COUNT 字节！ */
    assert(left_to_write == 0);
    /* 写入的字节数正好等于 COUNT。 */
    return count;
}
```

#### B.1.4 读取数据

读取数据的对应调用是 `read`。像 `write` 一样，它接受一个文件描述符、一个缓冲区指针和一个计数。计数器指定了从文件描述符读取到缓冲区中的字节数。`read` 调用在出错时返回 -1，或返回实际读取的字节数。这可能小于请求的字节数，例如，如果文件中剩余的字节数不足。

##### 读取 DOS/Windows 文本文件

在读完这本书后，我们非常确定你会选择为 `GNU/Linux` 编写所有的程序。你的程序偶尔可能需要读取由 `DOS` 或 `Windows` 程序生成的文本文件。预判这两个平台之间文本文件结构上的重要差异是非常重要的。

在 `GNU/Linux` 编辑器中，每行都通过换行符与下一行分隔。换行符由字符常量 `'\n'` 表示，其 ASCII 码为 10。然而，行之间是由两个字符组合分隔的：一个回车（字符 `'\r'`，其 ASCII 码为 13），后跟一个换行符。

某些 `GNU/Linux` 文本编辑器在显示 `Windows` 文本文件时，会在每行尾显示 '`M`'——这就是回车字符。`Em` 能正确显示 `Windows` 文本文件，但通过在缓冲区底部的状态行中显示 `(DOS)` 来指示它们。某些编辑器（如记事本）会将 `GNU/Linux` 文本文件中的所有文本显示在单行，因为它们期望每行尾有一个回车。处理 `GNU/Linux` 和 `Windows` 文本文件的其他程序在输入格式错误的文本文件时，可能会报告某些神秘的错误。

如果你的程序读取由 `Windows` 程序生成的文本文件，你可能希望将序列 `'\r\n'` 替换为单个换行符。同样，如果你的程序编写所需的 `Windows` 程序读取的文本文件，请将单独的换行符替换为 `'\r\n'` 组合。无论你是使用本文介绍的底层 I/O 调用还是标准库 I/O 函数，都必须这样做。

列表 B.4 提供了 `read` 的简单演示。该程序输出命令行指定的文件的内容的十六进制转储。每行显示文件中的偏移量和后续 6 个字节。

##### 列表 B.4 `(hexdump.c)` 打印文件的十六进制转储

```c
#include <fcntl.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
  unsigned char buffer[16];
  size_t offset = 0;
  size_t bytes_read;
```

`Hexdump` 运行示例。它显示正在打印其自身可执行文件的转储：

```text
% ./hexdump
0x000000: 7f 45 4c 4f 46 01 01 00 00 00 00 00 00 00 00 00
0x000010: 02 00 03 00 01 01 00 00 c8 03 04 08 34 00 00 00
0x000020: e6 23 01 00 00 00 00 00 00 00 00 00 00 00 00 00
0x000030: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

`Hexdump` 运行示例。它显示正在打印其自身可执行文件的转储：

你的输出可能不同，取决于你如何编译 `hexdump`。

## B.2 stat（系统调用）

通过 `open` 和 `read`，你可以提取文件的内容。但其他信息呢？例如，调用 `ls -1` 会显示当前目录下的文件信息，如文件大小、最后修改时间、权限和所有者。

`stat` 调用用于获取文件信息。调用时传入你感兴趣的文件路径和一个指向 `struct stat` 类型变量的指针。如果 `stat` 调用成功，它将返回 0 并用该文件的信息填充结构体的字段；否则，它返回 -1。

以下是 `struct stat` 中最实用的字段：

- `st_mode` 包含文件的访问权限。文件权限在第 10.3 节“文件权限”中解释。
- 除了访问权限外，`st_mode` 字段在高位中编码了文件类型。请参阅此列表随后的文本获取有关解码这些信息的说明。
- `st_uid` 和 `st_gid` 分别包含文件所属的用户 ID 和组 ID。用户 ID 和组 ID 在第 10.1 节“用户和组”中描述。
- `st_size` 包含文件的大小，单位为字节。
- `st_atime` 包含文件最后被访问（读取或写入）的时间。
- `st_mtime` 包含文件被修改的时间。

这些宏检查 `st_mode` 字段的值以确定你调用的是什么种类型的文件。如果文件属于该类型，则宏为真。

```
S_ISBLK (mode) 块设备
S_ISCHR (mode) 字符设备
S_ISDIR (mode) 目录
S_ISFIFO (mode) fifo (命名管道)
S_ISLN (mode) 符号链接
S_ISREG (mode) 普通文件
S_ISSOCK (mode) socket
```
