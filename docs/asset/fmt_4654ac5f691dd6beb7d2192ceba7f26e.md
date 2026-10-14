
```c
errExit("sysconf");
}

clockTime = clock();

if (clockTime == -1)
    errExit("clock");

printf(" clock() returns: %ld clocks-per-sec.%.2f secs)\n"
       (long)clockTime, (double)clockTime / CLOCKS_PER_SEC);

if (times(&t) == -1)
    errExit("times");

printf("times: yields user CPU:%.2f; system CPU: %.2f\n"
       (double)t.tms_utime / clockTicks,
       (double)t.tms_stime / clockTicks);
```

```c
int
main(int argc, char *argv)
{
    int numCalls, j;
    printf("CLOCK_PER_SEC=%ld sysconf(_SC_CLK_TCK)=%ld\n\n"
       (long)CLOCKS_PER_SEC, sysconf(_SC_CLK_TCK));
    displayProcess("At program start:\n");
    numCalls = (argc > 1) ? getint(argv[1], GN_GT_0, "num-calls") : 100000000;
    for (j = 0; j < numCalls; j++)
        (void)getppid();
    displayProcess("After getppid() loop:\n");
    exit(EXIT_SUCCESS);
}
```

`time/process_time.c`

## 10.8 总结

实际时间（Real time）对应于日常时间的定义。当从某个标准点测量实际时间时，我们将其称为日历时间（calendar time），与之相对的是经过时间（elapsed time），是从进程生命周期中的某点（通常是开始点）开始量的。

进程时间（Process time）是进程使用的 CPU 时间量，分为用户部分和系统部分。各种系统调用允许我们获取和设置系统时钟（即自 Epoch 以来以秒为单位的日历时间），一系列库函数允许在日历时间与其他格式之间进行转换，包括人类可读的字符串。

使用和显示时间是许多应用程序的重要部分，我们将在书的后面频繁使用本章描述的函数。我们还将在第 3 章中详细介绍时间的测量。

## 更多信息

Linux 内核如何测量时间的细节可以在 GNU 库手册中找到（在线地址为 http://www.gnu.org/）。SUS3 文档还详细涵盖了区域（locales）。

## 10.9 练习

1. 假设一个系统中 `sysconf(_SC_CLK_TCK)` 返回值为 100。假设 `times()` 返回的值是一个无符号 32 位整数。如果 `CLOCKS_PER_SEC` 的值是 `clock()` 返回的，那么需要多久会溢出？

# 11 限制与选项

每个 UNIX 实现对各种功能和资源设定限制，并提供——或不提供——选项。例如：

- 进程可以同时打开多少个文件？
- 系统支持实时吗？
- `int` 类型中可以存储的最大值是多少？
- 参数列表可以有多大？
- 路径名的长度是多少？

虽然我们可以将限制硬编码到应用程序中，但这会降低可移植性，因为限制和选项各异：

- 跨 UNIX 实现：尽管限制在单个实现中是固定的，但在不同实现之间可能会不同。
- 在特定实现上的运行时：内核可能经过重新配置以更改限制。或者，应用程序可能在一个系统中编译，但在具有不同限制系统中运行。
- 文件系统之间：例如，传统的 V 文件系统允许 14 字节的文件，而 BSD 文件系统和大多数 Linux 文件系统允许 255 字节。

## 11.1 系统限制

对于它指定的每个限制，SUS3 要求所有实现都支持一个最小值。在大多数情况下，这个最小值定义在 `<limits.h>` 中，并带有 `_POSIX_` 前缀，且（通常）包含 `_MAX` 字符串；因此名称的格式为 `_POSIX_XX_MAX`。

如果应用程序限制于 SUS3 要求的最小值，那么它将通用于所有实现。然而，这样做会阻止应用程序利用提供更高限制的实现。因此，最好在特定系统上使用 `<limits.h>`、`sysconf()` 或 `pathconf()` 来确定限制。

在某些情况下，为限制提供了最大值，这些名称包含 `_MIN` 字符串。对于这些常量，情况反之：它们代表某些资源的下限，而标准规定，在合规的实现中，该下限不能大于某个值。例如，`FLT_MIN` 限制 (e-37) 定义了实现可以设置的最小表示浮点数的最大值，且所有合规实现都能够表示至少这样的浮点数。

每个限制都有一个名称，它与上述描述的最小值名称对应，但缺少 `_POSIX_` 前缀。实现可以在 `<limits.h>` 中定义一个该名称的常量，以指示该实现对应的限制。

如果已定义，此限制将始终至少等于上述描述的最小值的大小（即 `XXX_MAX >= POSIX_XXX_MAX`）。
SUSv3 将其指定的限制划分为三类：运行时不变值、路径名变量值和运行时可增加值。在接下来的段落中，我们将描述这些类别并提供一些示例。

### 运行时不变值（可能不确定）

运行时不变值是指一种在 `<limits.h>` 中定义时，该值对于该实现来说是固定的限制。然而，该值可能是不确定的（也许因为取决于可用内存），因此在 `<limits.h>` 中被省略。在这种情况下（即使它在 `<limits.h>` 中也有定义），应用程序也可以使用 `sysconf()` 在运行时确定该值。

`PRIO_MAX` 是运行时不变值的一个示例。如 52.5.1 所述，POSIX 消息队列的消息优先级有一个限制。SUSv3 定义了常量 `POSIX_PRIO_MAX`，值为 32，这是所有符合标准的实现都必须提供的最小值。这意味着我们可以预期，所有符合标准的实现都允许从 0 到 31 的消息优先级。UNIX 实现可以设置比此更高的限制，在 `<limits.h>` 中定义常量 `POSIX_PRIO_MAX` 值为其限制的大小。例如，在 Linux 上，`PRIO_MAX` 定义的值为 32,768。该值也可以通过以下调用在运行时确定：

```
lim = sysconf(SC_PRIO_MAX);
```

### 路径名变量值

路径名变量值是指与路径名（文件、目录、终端等）相关的限制。每个限制对于特定实现来说可能是常量，也可能在不同系统之间变化。在限制可以根据路径名而变化的情况下，应用程序可以使用 `pathconf()` 或 `fpathconf()` 来确定其值。`NAME_MAX` 限制是路径名变量值的一个示例。该限制定义了特定文件系统上文件名的最大长度。SUSv3 定义了常量 `POSIX_NAME_MAX`，值为 14（OS V 文件系统限制），作为实现必须允许的最小值。实现可以定义比此更高的 `NAME_MAX` 限制，并/或通过以下调用获取特定文件系统的信息：

```
lim = pathconf(directory_path, _PC_NAME_MAX);
```
