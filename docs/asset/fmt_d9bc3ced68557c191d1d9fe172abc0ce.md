
如果 `expression` 为假（比较等于零），`assert()` 会向 `stderr` 打印错误消息并通过调用 `abort(3)` 终止程序。`expression` 可以是任何返回整数的有效 C 语句，例如 `fputs("some string", somefile)`。因此，例如列表 13.1 中的程序将在第 17 行突然终止，因为第 16 行的 `fopen()` 调用将失败（除非，你恰好在当前目录下有一个名为 `bar_baz` 的文件）。

## 处理错误
第 13 章

### 列表 13.1 badptr.c——使用 assert()

```c
/*
  * 列表 13.1
  * badptr.c - 测试 assert()
 */
#include <assert.h>
#include <stdio.h>
int main(void)
{
  FILE *fp;
  fp = fopen("foo_bar", "w"); /* 这应该可以工作 */
  assert(fp);
  fclose(fp);
  fp = fopen("bar_baz", "r"); /* 这应该失败 */
  assert(fp);
  fclose(fp); /* 永远不会到达这里 */
  return 0;
}
```

示例运行结果如下：
```
$ badptr.c:17: main: Assertion 'fp' failed.
IO trap
```

输出显示了发生错误的程序 `badptr.c`、断言失败的行号 `17` 以及断言失败的文件。

使用 `assert()` 的缺点是，当频繁调用时，它会极大影响执行速度。然而，偶尔调用是可以接受的。由于性能影响，许多程序员在开发过程中使用 `assert()`，但在发布版本中，通过在包含 `<assert.h>` 之前插入 `#define NDEBUG` 来禁用所有的 `assert()` 调用，如下：

```c
#include <stdio.h>
#define NDEBUG
#include <assert.h>
```

如果定义了 `NDEBUG`，`assert()` 宏就不会被调用。`NDEBUG` 的值并不，可以为 0。`NDEBUG` 的存在足以禁用 `assert()` 调用。然而，像往一样，有一个陷阱！考虑语句：

```c
assert(p = malloc(sizeof(char)*100) == NULL);
```

因为 `NDEBUG` 阻止了 `assert()` 的调用，`p` 将无法正确初始化，因此这样做会导致问题。在使用 `assert()` 时，正确的写法方式是：

```c
p = malloc(sizeof(char) *100);
assert(p);
```

即使 `assert()` 语句被禁用，你仍然需要测试 `p`，但至少代码不会为其分配内存。如果你将 `malloc()` 调用嵌入 `assert()` 语句中，它将永远不会被调用。正如你所见，`assert()` 是很有用的，但突然终止程序并不是你希望用户处理的问题。真正的目标应该是“优雅降级”，以便只有在分层错误处理调用全部失败且你没有替代方案时，才需要终止程序。你在后台成功解决了不需要涉及或通知用户的错误越多的，你的程序在用户看来就越显得健壮。

## 使用预处理器

除了 `assert()` 函数外，C 标准还定义了两个宏 `__LINE__` 和 `__FILE__`，它们在程序执行涉及错误的各种情况下都非常有用。例如，你可以将其与 `assert()` 结合使用，更准确地指出导致 `assert()` 失败的错误位置。事实上，`assert()` 使用 `__LINE__` 和 `__FILE__` 来完成工作。列表 13.2–13.14 定义并使用了更健壮的打开文件函数 `open_file()`。

### 列表 13.2 filecn.h

```c
/*
 * 列表 13.2
 * filecn.h - 声明一个新的打开文件函数
 */
#ifndef FILECN_H_
#define FILECN_H_
```

## 错误处理
## 第 13 章

```c
8 int open_file(FILE *fp, char *fname, char *mode,
int line, char *file);
9
10 #endif /* FILECN_H_ */
```

这里没有什么特别的。

### 列表 13.3 filefcn.c

```c
/*
 * Listing 13.3
 * filefcn.c - 使用 __LINE__ 和 __FILE__
 */
#include <stdio.h>
#include "filefcn.h"

int open_file(FILE *fp, char *fname, char *mode, int line,
char *file);
```

```c
 if((fp = fopen(fname, mode)) == NULL) {
    fprintf(stderr, "[%s:%d] open_file) failed\n", file, line);
    return 1;
 }
 return 0;
}
```

我们在这里仅仅定义函数。同样，没什么寻常的。

### 列表 13.4 testmacs.c

```c
/*
 * Listing 13.4
 * testmacs.c - 测试 filefcn.c 中定义的函数
 */
#include <stdio.h>
#include <stdlib.h>
#include "filefcn.h"

int main(void)
{
    FILE *fp;
    int ret;

    if(open_file(fp, "foo bar", "w", __LINE__, __FILE__))
        exit(EXIT_FAILURE);
    if(fp)
        fclose(fp);
```

# 系统编程
## 第二部分

### 列表 13.4 续

```c
  ret = open_file(fp, "bar_baz", "r", __LINE__, __FILE__);
  if(ret)
      exit(EXIT_FAILURE);
  fclose(fp);

  return 0;
}
```

在编译之前，预处理器会将 `__LINE__` 符号替换为 14 和 19，并将 `__FILE__` 替换为 `testmac.c`，即源文件的名称。如果 `open_file()` 调用成功，它会向调用者返回 0；否则，它会打印一条诊断信息，指示失败所在的（调用者处的）文件名和行号，并返回 1。如果我们在 `open_file()` 的定义中使用 `__LINE__` 和 `__FILE__`，那么行号和文件名将不会很有用。按照我们现在的定义方式，你可以确切知道函数在何处失败。

执行程序：
```
$ ./testmac
[testmac.c:19] open_file() failed
```

我们看到它在 `testmac.c` 的第 19 行失败了，这是我们预期的结果。`__LINE__` 和 `__FILE__` 对于追踪 bug 非常有帮助。学会使用它们。

## 标准库设施

在此语境下，“标准库”指的是支持标准的 C 环境中强制要求包含的变量、宏和函数。本节将深入研究五个函数和一个变量（ge，这听起来像像某部关于编程的电影，“五个函数和一个变量”），它们是任何错误处理中的重要部分。它们的原型（头文件）如下所示：

- `stdlib.h` `abs(void);`
- `stdlib.h` `void exit(int status);`
- `stdlib.h` `int atexit(void (*const fcn)(void));`
- `stdio.h` `void perror(const char *s);`
- `string.h` `void *strerror(int errno);`
- `errno.h` `int errno;`

这三个函数也是错误处理工具箱的重要组成部分。它们都声明在 `<stdio.h>` 中。

```c
void clearerr(FILE *stream);
清除流的结束文件 (EOF) 和错误指示器。
```

```c
int feof(FILE *stream);
如果流的 EOF 指示被设置，则返回非零值。
```

```c
int ferror(FILE *stream);
如果流的错误指示被设置，则返回非零值。
```

## 理解 errno

许多（但不是所有）库函数在发生错误时会将全局变量 `errno` 设置为非零值（这些函数大部分位于数学库中）。然而，没有任何库函数会清除 `errno`（设置 `errno = 0`），因此为了避免虚假错误，在调用可能设置 `errno` 的库函数之前应清除 `errno`，如列表 13.5 中的代码段所示：

### 列表 13.5 errno 变量

```c
#include <errno.h>
/* 在此处执行更多操作 */
errno = 0;
y = sqrt(X);
if(errno != 0) {
    fprintf(stderr
```

数学库中的函数会将 `errno` 设置为 `EDOM` 和 `ERANGE`。当传递给函数的值的值超出其定义域时，会发生 `EDOM` 错误。例如，`sqrt(-1)` 会产生域错误。当数学库中的函数返回的值太大，无法用 `double` 表示时，会发生 `ERANGE` 错误。`log(0)` 会产生范围错误，因为 `log(0)` 是未定义的。某些函数可能会同时设置 `EDOM` 和 `ERANGE` 错误，因此需要将 `errno` 与 `EDOM` 和 `ERANGE` 进行比较，以确定发生了哪一个以及如何继续操作。

## 使用 abort() 函数

这是一个粗暴的调用。调用它时，会导致程序异常终止。

## 使用 exit() 函数

`exit()` 是文明的亲戚。像 `abort()` 一样，它终止程序并向操作系统返回一个值。

## 使用 atexit() 函数

`atexit()` 函数注册一个在正常终止时调用的函数。它不接受参数并返回 `void`。如果注册成功，`atexit()` 返回 0，否则返回 1。列表 13.6 展示了 `atexit()` 如何工作。

### 列表 13.6 atexit() 函数

```c
/*
 * Listing 13.6
 * chkexit.c - 使用 atexit() 的练习
 */
#include <stdio.h>
#include <stdlib.h>
```

## 错误处理
## 第 13 章

```c
void fatexit(void)
{
    fprintf(stdout, "Here we are in fatexit()\n");
}
int main(int argc, char *argv[]) {
    fprintf(stdout, "Here we are in main()\n");
    if(atexit(fatexit) != 0) {
        fprintf(stderr, "Failed to register atexit()\n");
    }
    fprintf(stdout, "Exiting...\n");
    if(atoi(argv[1])) {
        abort();
    }
    return 0;
}
```

第 16 行是关键行。通过将裸函数名 `fatexit` 传递给 `atexit()`，并测试返回值以确保函数注册成功；传递它 1 或 0。如果你传递 `chkexit 0`，它将正常终止，但非零参数会导致异常终止。当我们运行程序时，它确认了在 `main()` 返回后调用了 `atexit()`：

```
$ ./chkexit 0
Here we are in main
Exiting...
Here we are in fatexit
$ ./chkexit 1
Here we are in main
Exiting...
IOT trap/Abort
```

## 使用 strerror() 函数

如果发生错误，对于你的用户（或者对你来说）知道操作系统出了什么问题可能会很有帮助。使用 `strerror()`。它返回一个指向描述与 `errno` 相关错误码的字符串的指针。因此，如果你将 `errno` 传递给 `strerror()`，你将得到关于发生了了的人的人类可读解释，而不是一个冰冷、毫无信息的数字。

## 使用 perror() 函数

这个实用的函数可以打印系统错误消息。如果你的代码执行的系统调用失败，该调用将返回 -1，并将变量 `errno` 设置为描述最后一个错误的值，正如许多库函数所做的那样。`perror()` 使用此值，打印字符串参数、一个冒号、一个空格、与 `errno` 对应的错误消息以及换行符。因此，调用

`perror("Oops");`

等同于调用

`printf("Oops: %s\n", strerror(errno));`

列表 13.7 展示了 `strerror()` 和 `perror()`。

### 列表 13.7 errs.c

```c
/*
 * Listing 13.7
 * errs.c - Demonstrate perror() and strerror()
 */
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#include <errno.h>

int main()
{
double d;

errno = 0;
d = sqrt(-1);
if(errno)
fprintf("stderr: %s\n", strerror(errno));

errno = 0;
d = sqrt(-2);
if(errno)
perror("sqrt");

exit(EXIT_SUCCESS);
}
```

执行时，你无法区分 `perror()` 的输出与使用 `strerror()` 的输出的区别。

## 系统日志设施

记录日志消息已经多次提到。好消息是，你不需要自己编写这个功能。Linux 使用两个守护进程——`klogd` 和 `syslog` 提供了集中的系统日志设施。我们将关注 `syslog`，因为它控制了从用户空间程序生成的消息。对于需要日志功能的应用程序，应该使用的工具是借自 BSD 的 `syslog` 设施。在许多 Linux 系统上，日志文件位于 `/var/log` 下。取决于你使用的 Linux 发行版，这些日志文件包括消息（messages）、调试（debug）、邮件（mail）和新闻（news）。标准控制台守护进程 `syslog` 维护这些文件。头文件 `<syslog.h>` 定义了 `syslog` 的接口。系统管理员在 `/etc/syslog.conf` 中设置 `syslog` 的行为。要创建一个日志消息，使用 `syslog()` 函数，原型如下：

```c
#include <syslog.h>
void syslog(int priority, char *format, ...);
```
