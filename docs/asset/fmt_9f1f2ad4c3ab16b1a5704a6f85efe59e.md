
# 第 5 章 • 每个开发者应该了解内核

## 5.3 进程调度器

`sleep` 命令执行 `sleep` 系统调用，这导致进程阻塞 1 秒。在这种情况下，进程总共执行了 1.042 秒。因为进程在整个时间内都是阻塞的，它在睡眠期间没有消耗 CPU 周期。另一方面，`dd` 命令勤奋地运行 1000 个块，从 `/dev/urandom` 拷贝数据到 `/dev/null`。在这种情况下，进程总共运行了 527 毫秒，其中 500 毫秒花费在内核模式下。正如被 `SIGTIN` 停止的进程一样，你可以用 `SIGCONT` 唤醒它，但当它尝试完成被最后一次中断的写入时，它会再次回到睡眠。只有当它被带回前台时，进程才会继续。或者，你可以禁用 `tstop` 并向进程发送 `SIGCONT`。

如果你没有在看，这个 `stty` 命令与之前的那个唯一区别在于那个横杠，它表示随后的标志将被禁用。

内核跟踪每个进程的执行时间。内核分别记录每个进程在用户模式和内核模式下所花费的时间。`time` 命令对于说明你的进程如何消耗时间非常有用。此功能内置在 Bash shell 以及其他 shell 中，但也可以作为 `/bin/time` 中的命令可用。在本文示例中，我将使用内置的 Bash 版本：

```bash
$ time sleep 1

real    0m.042s

user    0m.000s

sys     0m.020s
```

```bash
$ dd if=/dev/urandom of=/dev/null count=1000

1000+0 records in

1000+0 records out

real    0m.527s

user    0m.000s

sys     0m.500s
```

如果你的代码因为阻塞设备或系统调用而运行缓慢，那么有几种方法可以加快你的代码。最明显的方法是避免这些调用。如果无法实现，你可以使用线程或异步 I/O 将你的应用程序并行化。

### 5.3.8.1 系统时间单位

POSIX 将时钟（`clock_t`）定义为在用户空间应用程序中测量系统时间的一个单位。遗憾的是，这个特定单位有两个定义。ANSI 定义用于 ANSI `clock` 函数，但该函数不应该在 Linux 程序中使用。该函数返回进程消耗的 CPU 时间量，这大致等于用户时间和系统时间之和。`clock` 返回一个以 `CLOCKS_PER_SEC` 为单位的的值，该值是一个系统定义的宏，GNU 标准库将其定义为 100000。在 Linux 系统上，`clock` 函数的返回值是以微秒为单位的，尽管实际的时钟频率通常要低得多。返回 `clock_t` 的函数使用的频率由 `sysconf` 函数给出，如下：

```c
sysconf(_SC_CLK_TCK);
```

`sysconf` 返回每秒滴答数（或赫兹），任何 `clock_t` 类型的变量都与此值相关。如果你正在进行性能测量，这非常重要，因为它决定了返回 `clock_t` 类型值的函数的精度。

ANSI `clock` 函数的一个问题是它会在一个小时多一点的时间内溢出。对于运行时间超过该时间的进程，`clock` 函数是不合适的。此外，`clock` 函数没有考虑子进程的 CPU 使用情况，并且不区分用户空间内核空间。由于这些问题，在 Linux 系统上使用 `clock` 函数是没有意义的，尽管它是 ANSI C 的。幸运的是，Linux 提供了几种替代方案。

- 注意：ANSI `CLK_TCK` 宏已被 POSIX 废弃，尽管它仍然被定义为 `sysconf(_SC_CLK_TCK)`。

POSIX `times` 函数也使用 `clock_t` 类型，但定义的单位不同。不是 `CLOCKS_PER_SEC` 或微秒，`times` 函数返回的 `clock_t` 值是以系统时钟滴答（ticks）为单位的。这使得溢出的可能性大大降低。

`times` 函数的原型为：

```c
clock_t times(struct tms *tms, unsigned *buf);
```

返回的值代表自过去某个时间以来墙上时钟的滴答数。Linux 将此点定义为启动时间。为了可移植性，返回值应仅作为相对时间的参考，而不是绝对时间。来自 `times` 的重要细节存储在 `struct tms` 结构中，该结构的地址由调用进程传递。`tms` 结构定义如下：

```c
struct tms {
    clock_t tms_utime;   /* 用户时间 */
    clock_t tms_stime;   /* 系统时间 */
    clock_t tms_cutime;  /* 子进程的用户时间 */
    clock_t tms_cstime;  /* 子进程的系统时间 */
};
```

`tms_utime` 值是进程自启动以来执行代码花费的时间。`tms_stime` 字段是进程自启动以来花费内核代码的时间。ANSI `clock` 函数的输出等同于这两个值之和再乘以时钟间隔。`tms_cutime` 和 `tms_cstime` 的值相同，但这些是针对已终止并用其中一个 `wait` 系统调用回收的派生进程测量的。

BSD 中引入的 `getrusage` 函数的替代方案：

```c
int getrusage(int who, struct rusage *usage);
```

与 `times` 不同，`getrusage` 专门获取父进程或子进程的信息。`rusage` 结构除了计时信息外还包含许多字段，但 Linux 内核填充了其中极少数。填充的两个字段是用户时间和系统时间，与 `times` 类似，但它们存储在 `struct timeval` 结构中：

```c
struct timeval ru_utime;
struct timeval ru_stime;
```

与歧义的 `clock_t` 类型不同，`timeval` 结构将时间以秒和微秒的两个整数形式存储：

```c
struct timeval {
    long tv_sec;      /* 秒 */
    long tv_usec;     /* 微秒 */
};
```
