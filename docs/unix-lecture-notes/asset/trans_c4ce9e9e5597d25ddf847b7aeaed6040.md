

```c
ssize_t read(int fildes, void *buf, size_t nbyte);
```

## DESCRIPTION

read() 尝试从文件描述符 fd 读取最多 count 个字节到以 buf 开始的缓冲区中。
如果 count 为零，read() 返回零且没有其他结果。
如果 count 大于 SSIZE_MAX，结果是不确定的。

## RETURN VALUE

成功时，返回读取的字节数（零表示文件结束），并且文件位置按此数量前进。如果此数字小于请求的字节数则不是错误；例如这可能发生在实际可用的字节更少时（也许因为接近文件末尾，或者因为我们正在从管道或终端读取），或者因为 read() 被信号中断。在出错时，返回 -1，并且 errno 被适当地设置。在这种情况下，文件位置（如果有）是否改变是不确定的。

要使用 read() 函数，程序必须包含头文件 <unistd.h>。该头文件有多种用途，对我们而言最相关的是它包含了（POSIX 兼容的）系统调用的原型。

## <stdio.h> 和 <unistd.h> 的区别。

以 "f" 开头的函数：fopen()、fread()、fwrite()、fclose() 等，它们操作文件流指针（FILE 指针），都属于 ANSI 标准 C I/O 库，其头文件为 <stdio.h>。它们是 C 函数，你可以在任何操作系统上使用。我们在第 1 章中使用了 fopen() 和 fclose() 来实现我们版本的 more 命令。

open()、read()、write() 和 close() 函数是 UNIX 系统调用，它们的原型定义在 <unistd.h> 中，这是一个 POSIX 头文件。<unistd.h> 头文件定义了各种符号常量和类型，并声明了各种函数，其中包括这些调用。这些函数只存在于 UNIX 系统中，只要你使用的系统是 POSIX 兼容的，无论使用什么语言都存在。POSIX 并未规定它们应该是系统调用还是库函数，只规定它们作为其中之一存在。这些系统调用操作文件描述符，而不是文件流。UNIX 系统调用直接操作内核；ANSI 标准 C I/O 库调用处于更高层。

read() 函数有三个参数。手册页说 read() 函数从与文件描述符关联的文件中读取。文件描述符是一个小的非负整数。我们将在后面的章节更详细地研究文件描述符。第二个参数是指向内存中某个位置的指针，读取的字节将被存储到该位置。第三个参数是要读取的字节数。返回值是实际读取的字节数，它永远不会更大，但可能更小，或者在出错时为 -1。

举例说明，假设 filedesc 是一个可用于读取的有效文件描述符，buffer 是一个大小为 100 的 char 数组，num_bytes_read 是一个整型变量。下面的代码片段展示了如何每次从该文件流读取 100 个字节，直到找到数据末尾

```c
while ( !done ) {
    num_bytes_read = read(filedesc, buffer, 100);
    if ( 0 > num_bytes_read )
        // an error code was returned during reading - bail out
    if ( 0 == num_bytes_read )
        // the end of file was reached - stop reading
        done = 1;
    else
        // do whatever has to be done to the data
}
```

这是一个典型的读循环结构。read() 调用在没有数据时不会失败；它只是返回 0。这就是检测输入数据结束的方法。

程序如何将文件描述符与文件关联起来？查看手册页的 SEE ALSO 部分，你会找到对 fcntl()、creat()、open() 和许多其他系统调用的引用。其中大多数都使用文件描述符。open() 系统调用是我们现在需要的，因为 open() 调用打开一个文件并为其分配一个文件描述符。

## 2.6.2 open() 和 close() 系统调用

要从二进制文件读取，进程必须

- 打开文件以便读取。
- 读取字节，并且
- 关闭文件。

open() 系统调用在进程和文件之间建立连接。把连接想象成一个管理进程对文件 I/O 操作的对象。该对象包含诸如下一次操作的文件偏移、各种状态标志以及进程可以调用的内核函数指针等内容。它由文件描述符表示。一个进程可以打开多个文件，每个文件都有自己的文件描述符。事实上，它可以两次打开同一个文件，每次连接都有不同的文件描述符。UNIX 不会阻止你或任何人多次打开同一个文件。协调对文件的访问是用户及其程序的责任。

如果你查看手册页，你会看到 open() 调用的以下概要。

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *path, int oflag, /* mode_t mode */...);
```

