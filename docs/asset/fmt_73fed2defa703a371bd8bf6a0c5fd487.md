
这消除了移植性问题。如果你知道程序将只运行在 POSIX 系统上，你可能希望使用`bsd_signal()`代替`signal()`。

一个注意事项是，该函数也被标记为`obsolescent`（过时的），意味着它可能会从未来的标准中撤销。在实践中，即使它被撤销，供应商可能仍继续支持它很长时间。（正如我们将看到的，如果你需要，POSIX `sigaction()` API 提供了足够的设施让你编写出功能类似的版本。）

## 10.4.3 忽略信号

一个注意事项是，该函数也被标记为`obsolescent`（过时的），意味着它可能会从未来的标准中撤销。在实践中，即使它被撤销，供应商可能仍继续支持它很长时间。（正如我们将看到的，如果你需要，POSIX `sigaction()` API 提供了足够的设施让你编写出功能类似的版本。）

## 10.4.4 可重启的系统调用

## 10.4 信号处理程序的实际应用

### 10.4.4.1 示例：GNU Coreutils 的 `safe_read()` 和 `safe_write()`

GNU Coreutils 使用`safe_read()`和`safe_write()`两个程序来处理传统系统上的`EINTR`情况。由于同一个文件通过`#include`和宏实现了这两个函数，代码变得有点复杂。Coreutils 分发版中的`lib/safe-read.c`如：

```c
/* 一个在中断后重试读和写的接口。

Copyright (C) 1993, 1994, 1998, 2002 Free Software Foundation, Inc.

... 很多模板代码 ...
*/

#ifdef safe_WRITE
# include "safe-write.h"
# define safe_rw_safe_write
# define rw write
#else
# include "safe-read.h"
# define safe_rw_safe_read
# define rw write
# undef const
# define const /* empty */
#endif

/* 通过 BUF(from) 描述符读(写) 最多 count 字节，如果被
   中断则重试。返回实际读(写)的字节数，EOF 时返回，
   或出错时返回 SAFE_READ_ERROR(SAFE_WRITE_ERROR)。 */
size_t
safe_rw (int fd, const void *buf, size_t count)
{
    size_t result;

/* POSIX 限制 < INT_MAX，但我们进一步限制了它，要求
   COUNT <= INT_MAX，这触发了 Tru6 5.1 中的一个 bug。
   当减少 COUNT 时，保持指针块对齐。
   注意，在任何情况下，read(write) 都可能成功，但 read(write)
   返回的字节数少于 count，因此调用者必须准备好处理
   部分结果。 */
if (count > INT_MAX)
    count = INT_MAX & ~8191;

do
    {
    result = rw (fd, buf, count);
    }
while (result < 0 && IS_EINTR (errno));
return (size_t)result;
}
```

第 57–64 行处理定义，根据情况创建`safe_read()`和`safe_write()`（见下文的`safe_write.c`）。

第 77–84 行反映了现实世界常见的复杂情况。在这里，一种特定的 Unix 变体无法处理大于`INT_MAX`的`count`值，因此第 83–84 行同时执行两个操作：将计数减少到`INT_MAX`以下，并保持数量为 8192 的倍数。后者维持了 I/O 操作的效率：以基本磁盘块大小的倍数进行 I/O 总是比奇数更高。正如注释所示，代码维护了`read()`和`write()`的语义，返回的计数可能少于请求的计数。

注意`count`参数确实可以大于`INT_MAX`，因为`count`是无符号的`size_t`。而`INT_MAX`是普通的`int`，在所有现代系统上都是符号。

第 86–90 行是实际循环，只要因`EINTR`失败就会重复执行操作。虽然没有显示`IS_EINTR()`宏，但它处理了未定义`EINTR`的系统情况（那里至少有一个定义，否则代码不会费心设置该宏；这可能是为了在非 Unix 系统上实现 Unix 或 POSIX 仿真）。

这里是`safe_write.c`：

第 18 行的`#define`定义了`SAFE_WRITE`；这与`safe-read.c`中的第 57–60 行对应。

### 10.4.4.2 仅限 GLIBC：`TEMP_FAILURE_RETRY()`

GLIBC`<unistd.h>`定义了一个宏`TEMP_FAILURE_RETRY()`，你可以用它来封装任何可能失败并将`errno`设置为`EINTR`的系统调用。它的“声明”如下：

```c
#include <unistd.h>

GLIBC

int TEMP_FAILURE_RETRY(expression);
```

这是该宏的定义：

`/* 求值 EXPRESSION，只要它返回 -1 且 'errno' 设置为 EINTR，则重复。 */`

```c
#define TEMP_FAILURE_RETRY(expression) \
(__extension__ {
  long int __result;
  do __result = (long int)(expression);
  while (__result == -1L && errno == EINTR);
  return __result;
})
```

该宏使用了 GCC 对 C 语言的扩展（由`__extension__`关键字标记），它允许括号内的大括号语句返回值，作用就像一个简单的表达式一样。

使用这个宏，我们可以如下重写`safe_read()`：

```c
size_t safe_read(int fd, void const *buf, size_t count) {
  size_t result;
  /* 诚如前面的注释限制 count。 */
  if (count > INT_MAX) 
    count = INT_MAX & -8191;
  result = TEMP_FAILURE_RETRY(read(fd, buf, count));
  return (size_t)result;
}
```

### 10.4.5 竞态条件与 `sig_atomic_t`

`count`参数确实可以大于`INT_MAX`，因为`count`是无符号的`size_t`。`INT_MAX`是普通的`int`，在所有现代系统上都是符号。

仅围绕`sig_atomic_t`构建应用程序是不可靠的。处理信号的正确方法将在后所示。

`IS_EINTR()`宏未显示，但它处理了未定义`EINTR`的系统情况（那里至少有一个定义，否则代码不会费心设置该宏；这可能是为了在非 Unix 系统上实现 Unix 或 POSIX 仿真）。

`volatile`关键字告诉编译器该变量可以从外部改变。

```c
volatile sig_atomic_t signal_flag = 0;

void handler(int signum) {
    signal_flag = 1;
}

int main(int argc, char **argv) {
    signal(SIGINT, handler);

    while (1) {
        if (signal_flag) {
            signal_flag = 0;
            // 处理信号
        }
    }
```
