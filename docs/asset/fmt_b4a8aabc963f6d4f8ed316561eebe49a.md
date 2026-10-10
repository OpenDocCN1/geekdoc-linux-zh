
```
26: if (argv[2][0] == 'x') {

27:     scanf(argv[2], "0x%x", &length);

28: } else {

29:     scanf(argv[2], "%d", &length);

30: }

31:

32: fd = open("/dev/mem", O_RDONLY);

33: if (fd == -1) {

34: addr = (unsigned char *)mmap(NULL, length,

35:             PROT_READ, MAP_SHARED,

36:            fd, offset);

37:

38: if (addr != NULL) {

39:     waddr = addr;

40:

41:     for (count = 0; count < length; count++) {

42:         if (count % 16 == 0) {

43:             printf("\n%8p *", waddr);

44:         }
45:         printf("%02x *", *waddr++);

46:     }

47:

48:     munmap(addr, length);

49: } else {

50:     printf("Unable to map memory.\n");

51: }

52:

53: close(fd);

54: printf("\n");

55:

56: return 0;

57: }
```

当栈空间增长时，内核会向该进程发送 `SIGSEGV`（段错误）信号，导致其终止。

`munlockall` 系统调用为为调用进程映射的页面重新启用分页。它不接受任何参数，并在成功时返回零：

```c
/* 解锁此进程的页面 */
munlockall();
```

`munlockall` 系统调用应在进程完成时间处理后调用。

# GNU 错误报告

在第 11 节“GNU/Linux 中的文件处理”中，你首次遇到了 Linux 的错误报告机制，即 `errno` 变量。该变量是给定进程（或线程）发生的最后一个错误（每个线程都有自己的 `errno` 变量）。如果发生了另一个错误，`errno` 变量会被覆盖。因此，在应用程序检测到错误后（例如系统调用返回非零值），应该检查 `errno` 变量并处理该错误。

使用 `errno` 变量时，你必须通过包含 `errno` 头文件来使你的应用程序可以使用该变量。这里（或在此头文件包含的文件中）还定义了各种错误代码符号常量。

每个系统调用都会向用户呈现一组不同的错误。每个返回一个或多个错误的系统调用都会在相应的 man 页（帮助手册）中呈现这些错误（以及产生它们的条件）。

现在来看一个简单应用程序中使用 `errno` 变量的示例（参见列表 20.7）。在示例示例中，第 2 行包含了必要的头文件。第 4–8 行用于检查输入参数的数量，然后将第一个参数作为文件打开。第 10 行是错误处理的目标（打开文件）。如果文件返回 `NULL`（在第 12 行检查），你就知道发生了错误。在第 14–28 行检查 `errno` 变量（具体而言检查了两个已知错误 `EACCES` 和 `EIODDIR`），并输出一个字符串以通知用户错误。

## 列表 20.7 展示 errno 的用法

```c
1: #include <stdio.h>
2: #include <errno.h>

4: int main(int argc, char *argv[])
5: {
6: FILE *fp;

8: if (argc < 2) return 1;

10: fp = fopen(argv[1], "w");

12: if (fp == NULL) {

14: switch (errno) {

16: case EACCES:
17: printf("Can't access file.\n");
18: break;

20: case EISDIR:
21: printf("Can't operate on directory.\n");
22: break;

24: default:
25: printf("another error occurred.\n");
26: break;

28:

29: }
30: return 1;

32: }

34: fclose(fp);

36: return 0;
37: }
```

在大多数情况下，列表 20.7 中显示的所有内容都不是必须的，相反，只需要对发生的错误进行指示（特别是当你没有办法从错误中恢复时）。在这种情况下，输出错误代码是所希望的结果。在这些情况下，你可以使用简单的一行：

```c
printf("Error occurred: %d\n", errno);
```

但由于有大约 130 个唯一的错误代码，表示错误类型的字符串会更好。GNU C 库提供了几个专门为此目的的函数。这些函数的原型可以在 `string.h` 中找到。

第一个是 `strerror` 函数，它接收错误代码并输出一个描述性字符串。其原型如下：

```c
char *strerror(int errno);
char *strerror_r(int errno, char *buf, size_t n);
```

与其简单地打印错误代码，你可以输出与错误代码相关的字符串，如下：

```c
printf("%s\n", strerror(errno));
```

如果错误是 `EACCES`，则输出以下字符串：

Permission denied（拒绝访问）

如果你在多线程应用程序中工作，不能使用 `strerror`，因为它为进程静态分配字符串。对于每个线程，你希望提供自己的缓冲区。这就是为什么 `strerror_r` 的函数原型接受错误代码的原因。该函数还返回指向用户提供的缓冲区指针（作用与 `strerror` 函数相同）。

最后，你还有 `perror` 函数。这特别有用，因为它直接将错误信息输出到 `stderr`。其原型如下：

```c
void perror(const char *message);
```

该函数接收一个消息并将其附加输出前面（通常传入导致 `errno` 设置的函数）。与上一个示例类似，`perror` 可以如下使用：

对于 `EACCES` 错误，结果如下：

perror: Permission denied

关于 `errno` 需要记住的是它的状态可以在每个系统调用中被设置。因此，如果你想保留某个特定错误代码，你需要在调用其他（会修改它的）系统调用之前将其存储。此外，只有在系统调用返回错误后，`errno` 变量才是有效的。

## 总结

本章涵盖了许多开发应用程序和工具软件中有用的系统调用。这些包括用于解析命令行参数的 `getopt` 和 `getopt_long` 调用、各种时间和及时间转换函数、用于收集高级系统信息的 `sysinfo` 调用、用于映射文件的 `mmap` 系统调用、两对帮助构建高性能应用程序的页面锁定函数（通过避免页面交换惩罚），最后用于输出错误代码和描述性字符串的例程。

# API 总结

```c
#include <unistd.h>
int getopt(int argc, char * const argv[], const char *optstring);
extern char *optarg;
extern int optopt, optind;
```

```c
#include <time.h>
int getopt_long(int argc, char * const argv[],
const char *optstring,
const struct option *longopts, int *longindex);
extern char *optarg;
extern int optopt, optind;
```

```c
#include <time.h>
time_t time(time_t *t);
struct tm *localtime(const time_t *timep);
struct tm *gmtime(const time_t *timep);
char *asctime(const struct tm *tm);
char *ctime(const time_t timepDay);
time_t mktime(struct tm *tm);
```

```c
#include <sys/mman.h>
void mmap(void *start, size_t length, int prot, int flags,
```
