
要以“Sunday, July 3, 10:02.”字体打印日期和时间，其中星期和月份是字符串的指针：

```c
#include <stdio.h>
printf(stdout, "%s, %s, %d, %02din",
weekday, month, day, hour, min);
```

打印五位小数：

```c
#include <math.h>
#include <stdio.h>
printf(stdout, "pi = %.5f\n", 4 * atan(1.0));
```

分配一个 128 字节的字符串并打印其中：

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>

char *newfprint(const char * fmt, ...)
{
    char *p;
    va_list ap;
    if ((p = malloc(128)) == NULL)
        return (NULL);
    va_start(ap, fmt);
    (void)vsnprintf(p, 128, fmt);
    va_end(ap);
    return (p);
}
```

`printf(1)`, `scanf(3)`

`fprintf`, `sprintf`, `vprintf`, `vsprintf`, 和 `vsnprintf` 函数符合 ANSI C3.159-1989（"ANSI C"）。

`q` 是 `long long` 的 BSD 4.4 表示法，而整数转换中的 `l` 或 `u` 符合 GNU 表示法。这些函数的 Linux 版本基于 GNU `glib` 库。查看 GNU `libc(glibc-1.08)` 的文档获取更简洁的描述。

Linux 下某些浮点转换会导致内存泄漏。

所有函数完全符合 ANSI C3.159-1989，但提供了额外的标志 `q`, `Z` 和 `'` 以及 `l` 和 `1` 标志的额外行为。后者被认为是错误，因为它改变了 ANSI C3.159-1989 定义的标志。

## psignal

`psignal`—打印信号

### 语法

```c
#include <signal.h>
void psignal(int sig, const char *s);
extern char *siglist[]
```

### 描述

`psignal()` 函数在 `stderr` 上显示消息，由字符串 `s`、冒号、空格和描述数字的字符串组成。如果 `sig` 无效，消息将指示未知信号。`siglist` 数组持有按信号数量索引的字符串。

### 返回值

`psignal()` 函数不返回值。

### 标准

BSD 4.3

### 参见

`perror(3)`, `strsignal(3)`

## putenv

`putenv`—更改或添加环境变量

### 语法

```c
#include <stdlib.h>
int putenv(const char *string);
```

### 描述

`putenv()` 函数添加或更改环境变量的值。参数字符串的格式为 `name = value`。如果 `name` 在环境中不存在，则将字符串添加到环境中。如果 `name` 存在，则将环境中 `name` 的值更改为 `value`。

### 返回值

`putenv()` 函数成功时返回 0，发生错误时返回 -1。

### 错误

`ENOMEM`

分配新环境的空间不足

### 标准

SVID 3

### 参见

`getenv(3)`, `setenv(3)`, `unsetenv(3)`

## putpwnt

`putpwnt`—写入密码条目

### 语法

```c
#include <pwd.h>
#include <stdio.h>
#include <sys/types.h>
int putpw(const struct passwd *p,FILE *stream);
```

### 描述

`putpw()` 函数将结构 `p` 中的密码条目写入关联的文件。

`passwd` 结构在 `<pwd.h>` 中定义如下：

```c
struct passwd {
    char *pw_name;      /* 用户名 */
    char *pw_passwd;    /* 用户密码 */
    uid_t pw_uid;       /* 用户 ID */
    gid_t pw_gid;       /* 组 ID */
    char *pw_gecos;      /* 真实姓名 */
    char *pw_dir;        /* 目录 */
    char *pw_shell;      /* Shell 程序 */
};
```

### 返回值

`putpw()` 函数成功时返回 0，发生错误时返回 -1。

### 错误

`EINVAL` 给了无效（NULL）参数

### 标准

SVID 3

### 参见

`fgetpw(3)`, `getpwuid(3)`, `setpw(3)`, `endpw(3)`, `getpwnam(3)`, `getpwuid(3)`, `getpw(3)`

# 第三部分：库函数

## 概述

```
#include <stdio.h>
int fputc(int c,FILE *stream);
int fputs(const char *s,FILE *stream);
int putc(int c,FILE *stream);
int putchar(int);
int puts(char *s);
int ungetc(int c,FILE *stream);
```

### 描述

`fputc()` 将字符 `c`（转换为 `unsigned char`）写入 `stream`。

`fputs()` 将字符串 `s` 写入 `stream`，但不包含其末尾的 `\0`。

`putc()` 等同于 `fputc()`，不同区别在于它可能被实现为宏，从而多次评估 `stream`。

`putchar(c)` 等同于 `putc(c,stdout)`。

`puts()` 将字符串 `s` 和末尾的换行符写入 `stdout`。

此处描述的函数调用可以相互混合，也可以与 `stdio` 库中针对同一输出流的其他输出函数混合。

## 返回值

`fputc()`、`putc()` 和 `putchar()` 返回写入的字符（作为 `unsigned char` 转换为 `int`），若出错则返回 `EOF`。

`puts()` 和 `fputs()` 成功时返回非负整数，出错时返回 `EOF`。

## 标准

+ - ANSI C, POSIX.1

### 缺陷

不建议将 `stdio` 库的输出函数调用与针对同一输出流的文件描述符的底层 `write()` 调用混合；其结果是未定义的，且极可能不是你想要的结果。

### 参见

`write(2)`, `fopen(3)`, `fwrite(3)`, `scanf(3)`, `gets(3)`, `seek(3)`, `ferror(3)`

GNU, 1993年4月4日

# qio

`qio`—InterNetServers 的快速 I/O 部分

## 概述

```
#include <qio.h"
IOSTATE *
QIOopen(name, size)
char *name;
int size;
IOSTATE * QIOfdopen(fd, size)
int fd;
int size;
void QIOclose(qp)
IOSTATE *qp;
```

```
char *QIOread(qp)
GIOSTATE *qp;
int QIO0length(qp)
GIOSTATE *qp;
int QIO0long(qp)
GIOSTATE *qp;
int QIO0error(qp)
GIOSTATE *qp;
int QIO0tell(qp)
GIOSTATE *qp;
int QIO0rewind(qp)
GIOSTATE *qp;
int QIO0fileno(qp)
GIOSTATE *qp;
```

### 描述

本手册页描述的例程是 InterNets 库 `libann(3)` 的一部分。它们用于提供快速访问文件。快速 I/O 的 QIO 标准。

`QIOopen` 打开指定的文件进行读取。它使用一个大小为 `size` 字节的缓冲区，该大小必须大于预期的行。头文件定义了常量 `GIO0_BUFFER`。如果 `size` 为 0，则 `qio0open` 将调用 `stat(2)` 并使用返回的块大小：如果失败，则将使用 `qio_BUFFER`。返回 `NULL` 或一个可在其他文件中使用的指针。`QIOopen` 执行的功能与 `fd` 所指的已打开描述符相同。

`QIOclose` 关闭文件并释放其占用的任何资源。

`QIOread` 返回文件中下一行的指针。末尾的换行符将被替换为 `\0`。如果到达 EOF、发生错误或行长于缓冲区，`QIOread` 返回 `NULL`。

在成功调用 `QIOread` 后，`QIO0length` 返回当前行的长度。
