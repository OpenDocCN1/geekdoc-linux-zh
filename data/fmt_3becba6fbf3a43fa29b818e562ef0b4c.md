
如果流的 EOF 指示器为真，则返回非零值。

```c
int ferror(FILE *stream);
```

如果流的错误指示器为真，则返回非零值。

# 理解 `errno`

许多（但不是所有）库函数在发生错误时会将全局变量 `errno` 设置为非零值（这些函数大部分位于数学库）。然而，没有库函数会清除 `errno`（设置 `errno = 0`），因此为了避免虚假错误，在调用可能设置 `errno` 的库函数之前清除 `errno`，列表 13.5 中的代码段所示——

# 列表 13.5 `errno` 变量

```c
#include <errno.h>
/* 更多内容 */

errno = 0;
y = sqrt(x);
if(errno != 0) {
    fprintf(stderr, "sqrt() error! Goodbye!\n");
    exit(EXIT_FAILURE)
}
```

在数学库函数中将 `errno` 设置为 `EDOM` 和 `ERANGE`。当传递给函数的值超出其定义域时，会发生 `EDOM` 错误。例如，`sqrt(-1)` 会产生定义域错误。当数学库函数返回的值太大而无法用 `double` 表示时，会发生 `ERANGE` 错误。`log(0)` 会产生范围错误，因为 `log(0)` 是未定义的。某些函数可能会同时设置 `EDOM` 和 `ERANGE` 错误，因此将 `errno` 与 `EDOM` 和 `ERANGE` 比较以找出发生了哪一个以及如何继续。

# 使用 `abort()` 函数

这是一个剧烈的调用。调用时，它会导致程序异常终止，因此通常清理任务（如关闭文件）以及任何用 `atexit()` 注册的函数都不会执行（`atexit()` 将在本章稍后部分讨论）。然而，`abort()` 会向操作系统返回一个实现定义的值表示终止未成功。如果不受 `ulimit` 限制，`abort()` 还会转储核心文件辅助事后调试。为了方便调试，请始终使用调试符号编译代码（使用 `gcc` 时使用 `-g` 或 `-ggdb` 选项）并且不要 `strip`（剥）。

注意：使用 `strip` 命令从可执行文件中移除调试符号会导致无法调试的遗憾后果。

# 使用 `exit()` 函数

`exit()` 是一个文明的表亲。像 `abort()` 一样，它向操作系统返回一个值，但是在执行了清理任务（如关闭文件）以及用 `atexit()` 注册的任何函数之后。如果传递非零值，它异常终止；如果传递 0，它正常终止。它定义在 `<stdlib.h>` 中。

# 使用 `atexit()` 函数

`atexit()` 注册一个在终止时调用的函数。它不接受参数并返回 `void`。正如上一节所述，使用 `atexit()` 可以保证清理代码已执行。

# 列表 13.6 `chkexit.c`

```c
1 /*
  * Listing 13.6
  * chkexit.c - 展示 atexit()
  */
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 void cleanup(void)
7 {
    printf("Cleaning up...\n");
8 }
9
10 int main()
11 {
12    atexit(cleanup);
13    printf("Program running...\n");
14    exit(0);
15 }
```

# 处理错误

当发生错误时，让用户知道发生了什么可能非常有帮助。

```c
1 # Handling Errors
2 #include <stdio.h>
3 #include <stdlib.h>
4 #include <errno.h>
5
6 void check_error(int status)
7 {
    perror("Error occurred");
8 }
9
10 int main(int argc, char *argv[])
11    FILE *f = fopen("non_existent.txt", "r");
12    if (f == NULL) {
13        perror("Error opening file");
14        exit(EXIT_FAILURE);
15    }
16    fclose(f);
17    return 0;
18 }
```

```bash
$ ./chkexit
Error opening file: No such file or directory
```

# 使用 `strerror()` 函数

当发生错误时，让用户知道发生了什么可能非常有帮助。使用 `strerror()`。它返回一个指向与 `errno` 相关字符串的指针。因此，如果你传递 `errno`，你将得到对发生情况的人类解释，而不是一个冰冷的、无信息的数字。

# 使用 `perror()` 函数

此函数打印系统错误消息。如果你的代码调用的系统调用失败，调用返回 -1 并将变量 `errno` 设置为描述错误的值，正如库函数一样。`perror()` 使用该值，打印字符串参数 `s`、冒号、空格、对应于 `errno` 的错误消息以及换行符。因此，调用

`perror("oops");`

同于调用

`printf("oops: %s\n", strerror(errno))`

# 列表 13.7 `errs.c`

```c
/*
  * Listing 13.7
  * errs.c - 展示 perror() 和 strerror()
 */
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#include <errno.h>

int main()
{
    errno = 0;
    d = sqrt(-1);
    if(errno)
        fprintf(stderr, "sqrt: %s\n", strerror(errno));

    errno = 0;
    d = sqrt(-2);
    if(errno)
        perror("sqrt");

    exit(EXIT_SUCCESS);
}
```

执行时，你无法区分 `perror()` 的输出与使用 `strerror()` 的输出。

![](img/66f6e6c242a0e6a79aeee4012c6ff547_236_0.png)

## 处理错误

第 13 章

## 系统日志设施

文中多次提到写入日志消息。好消息是，你不需要自己编写此功能。Linux 提供了通过两个守护进程——`klogd` 和 `syslog` 运行的集中式系统日志设施。我们将关注 `syslog`，因为它控制了来自用户空间程序的消息的生成。如果你的应用程序需要日志功能，要使用的工具是借自 BSD 的 `syslog` 设施。在大多数 Linux 系统上，日志文件位于 `/var/log` 下。取决于你使用的 Linux 发行版，这些日志文件包括消息（messages）、调试（debug）、邮件（mail）和新闻（news）。标准控制台日志进程 `syslog` 维护这些文件。头文件 `<syslog.h>` 定义了 `syslog` 的接口。系统管理员在 `/etc/syslog.conf` 中设置 `syslog` 的行为。要创建日志消息，使用 `syslog()` 函数，原型如下：

```c
#include <syslog.h>
void syslog(int priority, char *format, ...);
```

`priority` 是级别（level）和设施（facility）的按位或组合，级别指示消息的严重性，设施告诉 `syslog` 消息由谁发送以及如何响应。它会格式化消息以写入日志以及任何指定的类似于 `printf()` 的格式。如果调用过 `strerror(errno)`，特殊说明符 `%m` 将被 `strerror()` 分配给 `errno` 的错误消息替换。表 13.1 按降序列出了优先级的可能值。

# 表 13.1 `syslog` 日志级别

| 级别 | 严重性 |
| :--- | :--- |
| `LOG_EMERG` | 系统不可用 |
| `LOG_ALERT` | 需要立即采取行动 |
| `LOG_CRIT` | 严重错误，如硬件故障 |
| `LOG_ERR` | 错误情况 |
| `LOG_WARNING` | 警告情况 |
| `LOG_NOTICE` | 正常但重要的消息 |
| `LOG_INFO` | 纯信息性消息 |
| `LOG_DEBUG` | 调试或跟踪输出 |

处理错误

# 表 13.2 `syslog` 设施名称

| 设施 | 消息来源 |
| --- | --- |
| `LOG_AUTHPRIV` | 私有安全和授权消息 |
| `LOG_CRON` | 计时守护进程 (`cron` 和 `atd`) |
| `LOG_DAEMON` | 其他系统守护进程 |
| `LOG_KERN` | 内核消息 |
