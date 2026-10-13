
`fopen()` 函数以指定的模式打开文件路径。模式的描述详见表 10.1。文本模式和二进制模式之间没有区别；这对于处理行尾方式不同的非 POSIX 系统（如 DOS、Windows）非常重要。在文本模式下，`fopen()` 返回一个文件指针，该指针被传递给其他 stdio 函数以识别流的状态。如果发生错误，它将返回 `NULL` 并设置 `errno`。

### 表 10.1 文件模式

| 模式 | 读 | 写 | 位置 | 截断 | 创建 | 二进制 |
|---|---|---|---|---|---|---|
| r | 是 | | 起始 | | | 文本 |
| r+ | 是 | | 起始 | | | 文本 |
| w | 否 | 是 | 起始 | 是 | 是 | 文本 |
| w+ | 否 | 是 | 起始 | 是 | 是 | 文本 |
| a | 否 | 是 | 结尾 | | | 文本 |
| a+ | 否 | 是 | 结尾 | | | 文本 |
| rb | 是 | | 起始 | | | 二进制 |
| r+b or rb+ | 是 | | 起始 | | | 二进制 |
| wb | 否 | 是 | 起始 | 是 | 是 | 二进制 |
| w+b or wb+ | 否 | 是 | 起始 | 是 | 是 | 二进制 |
| ab | 否 | 是 | 结尾 | | | 二进制 |
| a+b or ab+ | 是 | 是 | 结尾 | | | 二进制 |

`freopen()` 函数接受第三个参数，这是一个已存在的文件指针。它将关闭并重新打开该指针，使其指向新文件。它在 I/O 操作中也应该使用相同的文件描述符。`freopen()` 通常用于重定向标准输出 `stdout`、`stdin` 和 `stderr`。

## 系统编程 第二部分

`fdopen()` 函数用于在通过 `open()`、`pipe()` 或 `accept()` 创建的底层文件描述符之上创建文件指针。`fopen()` 和 `freopen()` 调用容易受到基于竞态条件或符号链接的安全攻击；第 35 章“安全编程”提供了一种更安全但限制较多的 `fopen()` 实现。`fclose()` 系统调用用于关闭文件。成功返回 0，失败返回 -1（请检查 `errno`）。

### 基础读写

`read()` 和 `write()` 函数用于从流（文件）中读取数据或向流写入数据。

```c
#include <stdio.h>

size_t read(void *ptr, size_t size, size_t count, FILE *stream);

size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
```

第一个参数是指向缓冲区的指针。接下来的两个参数是写入的大小和记录数。返回值是写入的记录数（不是字节数）；此值可能小于请求的数目。如果发生错误，返回值通常会小于请求的数目；甚至可能是负数。你需要使用 `eof()` 和 `error()` 来检查操作未完成的原因。

### 状态函数

`eof()` 和 `error()` 函数返回流的当前状态。

```c
#include <stdio.h>

void clearerr(FILE *stream);

int eof(FILE *stream);

int error(FILE *stream);

int fileno(FILE *stream);
```

如果到达文件结束，`eof()` 返回非零值；注意，只有当你实际尝试读取文件末尾之后的内容，文件结束标志才会被设置。使用 `while(!eof(stream))` 可能会导致循环多执行一次。如果流上设置了错误标志，`error()` 函数返回非零值。此函数不会设置 `errno`；实际上遇到了一个的上一个函数调用设置了它。文件结束标志和错误标志可以通过 `clearerr()` 重置。

## 文件操作 第 10 章

`fileno()` 函数返回与流关联的文件描述符编号。这允许你对该流执行描述符 I/O 操作（见第 9 章“I/O 例程”）。例如，你可能需要发出 `ioctl()` 或 `fstat()` 系统调用。跳过 stdio 层时要小心；特别是在此之前，确保已刷新你的缓冲区。

## 格式化输出

`printf()` 函数对任何稍有 C 编程经验的人来说都是熟悉的。它根据控制字符串格式的控制，向流打印输出（包括可选参数）。

```c
#include <stdio.h>

int printf(const char *format, ...);

int fprintf(FILE *stream, const char *format, ...);

int sprintf(char *str, const char *format, ...);

int snprintf(char *str, size_t size, const char *format, ...);
```

```c
#include <stdarg.h>

int vprintf(const char *format, va_list ap);

int vfprintf(FILE *stream, const char *format, va_list ap);

int vsprintf(char *str, const char *format, va_list ap);

int vsnprintf(char *str, size_t size, const char *format, va_list ap);
```

有许多版本的 `printf` 接受 `va_list` 参数。以 "v" 开头的 `printf()` 函数非常有帮助。`printf()` 函数对任何稍有 C 编程经验的人来说都是熟悉的。它根据控制字符串格式的控制，向流打印输出（包括可选参数）。

## 文件操作

## 第 10 章

指定的类型，并作为副作用修改 `ap` 变量以指向下一个参数（在通过堆栈传递参数的传统系统中，使用指定类型的大小作为偏移量）。在 `stdarg` 映射上找到一个实现简易 `printf()` 函数的 `stdargs` 函数的简单示例（实现一个简单的 `printf()` 函数）；关于 `va_arg()` 和 `stdargs` 使用的更多信息，请参阅该文档。与固定参数的函数不同，变长参数函数无法轻易封装在另一个包装函数中。技巧是让实际函数接收一个 `va_list`（而不是它所引用的变长参数），并编写一个简单的包装函数，其作用仅是初始化 `va_list` 并调用另一个函数。现在，程序员通过调用你的实际函数而不是你的包装函数来编写他们自己的包装函数。列表 10.1 中的 `printf()` 函数是一个替换包装函数的示例。ANSI 标准本质上要求 `printf` 系列函数必须实现为接受 `va_list` 的函数和变长参数包装函数，或者至少在某种程度上是这样。由于 `sprintf()` 和 `vprintf()` 做了相同的事情但处理结果的方式不同，合并这两种变体的尝试可能会给那些查看 `printf()` 系列函数代码的人增加困惑。那些想使用 `stdarg.h` 文件来寻找 `stdarg` 魔法所在位置的人会发现比预期更多的东西：该文件消失了。虽然在传统机器上可以在 C 宏中实现 `stdargs`，但 `gcc` 在内部处理这些宏，因为它必须处理许多不同的架构。

## 列表 10.1 printf() 及其伙伴

```c
#include <stdlib.h>
#include <stdio.h>
#include <stdarg.h>

FILE *printer;
FILE *logfile;

int fprintf(const char *format, ...)
{
 va_list ap;
  va_start(ap,format);
  vprintf(format, ap);
  if (printer) vprintf(printer, format, ap);
  if (logfile) vprintf(logfile, format, ap);
  va_end(ap);
}
```

## 系统编程

## 第二部分

### 列表 10.1 续

```c
int old_printf(const char *format,
long a1, long a2, long a3, long a4,
long a5, long a6, long a7, long a8)
{
    printf(format, a1, a2, a3, a4, a5, a6, a7, a8);
    if (printer)
        fprintf(printer,format, a1, a2, a3, a4, a5, a6, a7, a8);
    if(logfile)
        fprintf(logfile,format, a1, a2, a3, a4, a5, a6, a7, a8);
```
