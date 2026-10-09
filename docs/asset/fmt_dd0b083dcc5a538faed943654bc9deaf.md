
```c
if ((fd = open(path, O_WRONLY)) < 0) {
    if (errno == ENOENT) {
        if ((fd = create(path, mode)) < 0) {
            err_sys("create error");
        } else {
            err_sys("open error");
        }
    }
}
```

如果在 `open` 和 `create` 之间由另一个进程创建了文件，就会出现问题。如果在这两个函数调用之间另一个进程创建了文件，并且该进程向文件写入了内容，那么这些数据在执行此 `create` 时会被擦除。将存在检查和创建合并为单个原子操作可以避免这个问题。

通常情况下，“原子操作”术语指的是一个由多个步骤组成的操作。如果操作是以原子方式执行的，要么所有步骤都执行了（成功），要么一个都不执行（失败）。不能只执行了步骤的子集。我们将在描述 `link` 函数（第 4.15 节）和记录锁定（第 14.3 节）时再次回到原子操作的话题。

## 3.12 dup dup2 函数

可以通过以下函数之一复制现有的文件描述符：

```c
#include <unistd.h>

int dup(int fd);
int dup2(int fd, int fd2);

// 均返回：成功时返回新的描述符，错误时返回 -1
```

`dup` 返回的新文件描述符保证是编号最小的可用文件描述符。使用 `dup2`，我们通过 `fd2` 参数指定新描述符的值。如果 `fd2` 已经打开，则会将其关闭。如果 `dup2` 返回 `fd2` 则表示没有关闭它。否则，`fd2` 的 `FD_CLOEXEC` 标志会被清除，这意味着如果进程调用 `exec`，则 `fd2` 将保持打开。

作为函数返回值的新文件描述符与 `fd` 参数共享同一个文件表项。我们在图 3.9 中展示这一点。

![](img/5dc46842acde5fbcadfab4612cdecbbc_113_0.png)

图 3.9 dup(1) 后的内核数据结构

图中，我们假设进程启动时执行了：

```
newfd = dup(1);
```

我们假设下一个可用的描述符是 3（这很可能，因为 0、1 和 2 已被 shell 打开）。由于两个描述符都指向同一个文件表项，它们共享相同的文件状态标志——读、写、追加等——相同的当前文件偏移量。

每个描述符都有自己的一套文件描述符标志。正如我们在第 3.14 节中描述的，新描述符的 `close-on-exec` 文件描述符标志总是会被 `dup` 函数清除。

复制描述符的另一种方法是使用 `fcntl` 函数，我们在第 3.14 节中描述了它。事实上，调用

```
dup(fd);
```

等同于

```c
fcntl(fd, F_DUPFD, 0);
```

同样，调用

```c
dup2(fd, fd2);
```

等同于

```c
close(fd2);
fcntl(fd, F_DUPFD, fd2);
```

在最后一种情况下，`dup2` 并不等同于 `close` 后接 `fcntl`。区别如下：

1. `dup2` 是一个原子操作，而另一种形式涉及两个函数调用。在后一种情况下，可能会在 `close` 和 `fcntl` 之间调用信号处理程序，该程序可能会修改文件描述符。（我们在第 10 章描述了信号）。如果不同的线程更改了文件描述符也会发生相同的问题。（我们在第 11 章描述了线程。）
2. `dup2` 和 `fcntl` 之间存在一些 `errno` 差异。

`dup2` 系统调用起源于 Version 7，并通过 BSD 版本传播。使用 `fcntl` 复制文件描述符的方法出现在 System III 并在 System V 中继续。SVR3 采用了 `dup2` 函数，而 4BSD 采用了 `fcntl` 函数，且 `F_DUPFD` 功能同时需要 `dup2` 和 `fcntl` 的 `F_DUPFD` 特性。

## 3.13 sync, fsync, 和 fdatasync 函数

传统的 UNIX 系统内核中有一个缓冲区缓存或页缓存，内核通过它执行 I/O 操作。当我们向文件写入时，数据通常由内核拷贝到它的缓冲区之一，并排队稍后写入磁盘。这被称为延迟写入（Bach [1986] 的第 3 章详细讨论了这种缓冲区缓存）。

内核最终所有延迟写入块写入磁盘，通常是在它需要重用该缓冲区处理其他磁盘时。为了确保文件系统与缓冲区缓存内容的一致性，提供了 `sync`、`fsync` 和 `fdatasync`。

```c
#include <unistd.h>

int fsync(int fd);
int fdatasync(int fd);
void sync(void);

// 成功返回 0，错误返回 -1
```

`sync` 系统调用确保缓冲区缓存中所有修改过的数据写入磁盘。`fsync` 系统调用类似，但它还确保元数据写入磁盘。`fdatasync` 系统调用类似于 `fsync`，但它只刷新数据部分，除非访问数据所必须的元数据。

## 3.14 fcntl 函数

`fcntl` 函数可以更改已打开文件的属性。

```c
#include <fcntl.h>

int fcntl(int fd, int cmd, ...);

// 返回：成功时取决于 cmd，错误时返回 -1
```

在本节的示例中，第三个参数是一个整数，对应于所示函数。我们在第 14.3 节描述记录锁定时，第三个参数将变为结构体指针。`fcntl` 函数用于不同的目的：

1. 复制现有的描述符（`cmd = F_DUPFD` 或 `F_DUPFD_CLOEXEC`）
2. 获取/设置文件描述符标志（`cmd = F_GETFD` 或 `F_SETFD`）
3. 获取/设置文件状态标志（`cmd = F_GETFL` 或 `F_SETFL`）
4. 获取/设置异步 I/O 所有者（`cmd = F_GETOWN` 或 `F_SETOWN`）
5. 获取/设置记录锁（`cmd = F_GETLK, F_SETLK, F_SETLKW`）

我们现在描述 11 个 `cmd` 值中的前 8 个。我们将在第 14.3 节再描述最后 3 个，它们处理记录锁定。

### 3.14.1 文件描述符标志

注意，某些现有程序在处理文件描述符标志时并没有使用常量 `FD_CLEXECEC`。相反，这些程序将标志设置为 0（执行时不关闭文件，默认值）或 1（执行时关闭文件）。

`F_GETFL` 返回 `fd` 的文件状态标志作为函数的返回值。我们在描述 `open` 函数时已经描述过文件状态标志。它们列在 3.10 节中。

| 文件状态标志 | 说明 |
| :--- | :--- |
| `O_RDONLY` | 仅读打开 |
| `O_WRONLY` | 仅写打开 |
| `O_RDWR` | 读写打开 |
| `O_EXEC` | 仅执行打开 |
| `O_SEARCH` | 仅打开用于的目录 |
| `O_APPEND` | 每次写入时追加 |
| `O_NONBLOCK` | 非阻塞模式 |
| `O_SYNC` | 等待写入完成（数据和属性） |
| `O_DSYNC` | 等待写入完成（数据） |
| `O_RSYNC` | 同步读写 |
| `O_FSYNC` | 等待写入完成（仅限 FreeBSD 和 Mac OS X） |
| `O_ASYNC` | 异步 I/O（仅限 FreeBSD 和 Mac OS X） |

图 3.10 fcntl 的文件状态标志

遗憾的是，访问模式标志——`O_RDONLY`、`O_WRONLY`、`O_RDWR` 和 `O_SEARCH`——并不是可以测试的位。（如前文所述，由于历史原因，前三个值分别为 0、1 和 2。此外，这些值是互斥的；一个文件只能启用其中一个。）因此，我们必须首先使用 `O_ACCMODE` 掩码获取访问模式位，然后将结果与任何一个值进行比较。

`F_SETFL` 将文件状态标志设置为第三个参数的值（取整数）。可以更改的标志包括 `O_APPEND`、`O_NONBLOCK`、`O_SYNC`、`O_DSYNC`、`O_RSYNC`、`O_FSYNC` 和 `O_ASYNC`。

`F_GETOWN` 获取当前接收 `SIGIO` 和 `SIGURG` 信号的进程 ID 或进程组 ID。我们在 14.5.2 节中描述了这些异步 I/O 信号。

`F_SETOWN` 设置接收 `SIGIO` 和 `SIGURG` 信号的进程或进程组 ID。正数参数指定进程 ID。负数参数表示进程组 ID 等于该参数的绝对值。

`fcntl` 的返回值取决于其他 `cmd`。以下命令在发生错误时返回 -1，或者返回其他值。以下四个命令有特殊的返回值：`F_DUPFD`、`F_GETFD`、`F_GETFL` 和 `F_GETOWN`。第一个命令返回新的文件描述符，下一个返回相应的标志，最后一个命令返回正数的进程 ID 或负数的进程组 ID。

### 示例

图 3.11 中的程序接受一个命令行参数，该参数指定一个文件描述符，并打印该描述符所选文件标志的描述。

```c
#include "apue.h"
#include <fcntl.h>

int main(int argc, char *argv[]) {
    int val;

    if (argc != 2)
        err_quit("usage: a.out <descriptor>");

    if ((val = fcntl(atoi(argv[1]), F_GETFL, 0)) < 0)
        err_dump("error for %d", atoi(argv[1]));

    switch (val & O_ACCMODE) {
        case O_RDONLY:
            printf("read only");
            break;
        case O_WRONLY:
            printf("write only");
            break;
        case O_RDWR:
            printf("read write");
            break;
        default:
            err_dump("unknown access mode");
    }

    if (val & O_APPEND)
        printf(", append");
    if (val & O_NONBLOCK)
        printf(", nonblocking");
    if (val & O_SYNC)
        printf(", synchronous writes");

#if defined(POSIX_C_SOURCE) && defined(O_FSYNC) && (O_FSYNC != O_SYNC)
    if (val & O_FSYNC)
        printf(", synchronous writes");
#endif

    putchar('\n');
    exit(0);
}
```

图 3.11 为指定的描述符打印文件标志

注意，我们使用了特性 `_POSIX_C_SOURCE` 并条件编译了不属于 POSIX 的访问标志。以下脚本显示了程序从 bash（Bourne-again shell）调用时的操作。结果将会有所不同，取决于你使用哪种 shell。

```bash
$ ./a.out 0 < /dev/tty
read only

$ ./a.out 1 > temp.foo
write only

$ ./a.out 2 >> temp.foo
write only, append

$ ./a.out 5 < temp.foo
read write
```

子句 `5<temp.foo` 以读写模式打开文件 `temp.foo`。

当我们修改现有的文件描述符或状态标志时，我们必须小心地获取标志值，按需进行修改，然后设置新值。我们不能简单地发出 `F_SETFD` 或 `F_SETFL` 命令，因为这可能会关闭已设置的位。图 3.12 显示了一个设置一个或多个标志的函数。

```c
#include "apue.h"
#include <fcntl.h>

void set_fl(int fd, int flags) {
    int val;

    if ((val = fcntl(fd, F_GETFL, 0)) < 0)
        err_dump("error for %d", fd);

    val |= flags; /* turn on */
    if (fcntl(fd, F_SETFL, val) < 0)
        err_dump("error for %d", fd);

    val &= ~flags; /* turn off */
    if (fcntl(fd, F_SETFL, val) < 0)
        err_dump("error for %d", fd);
}
```

图 3.12 `set_fl` 函数，为描述符设置一个或多个标志

图 3.13 中的一行，但由于 `O_SYNC` 标志没有产生预期的效果，最后一行的行为与第五行相同。

图 3.14 显示了在 Mac OS X 10.6.8 上运行测试的计时结果，该系统使用 HFS 文件系统。请注意，这些时间符合我们的预期：同步写入的开销比延迟写入大得多，而且在同步写入中使用 `fsync` 区别微乎其微。注意，在延迟写入的末尾添加 `fsync` 调用几乎没有产生可衡量的差异。很可能是因为在我们向文件写入新数据时，操作系统已经将之前写入的数据刷到了磁盘，因此当我们调用 `fsync` 时，已经没没多少工作需要做了。

| 操作 | 用户态 CPU (秒) | 内核 CPU (秒) | 时钟时间 (秒) |
|---|---|---|---|
| 写入 /dev/null | 0.14 | 1.02 | 5.28 |
| 正常写入磁盘文件 | 0.14 | 3.21 | 17.04 |
| 设置 O_SYNC 写入磁盘文件 | 0.39 | 16.89 | 60.82 |
| 写入磁盘后接 fsync | 0.13 | 3.07 | 17.10 |
| 设置 O_SYNC 写入磁盘后接 fsync | 0.39 | 18.18 | 62.39 |

图 3.14 使用各种同步机制的 Mac OS X HFS 计时结果

将 `fsync` 和 `fdatasync`（两者都在我们明确要求时更新文件内容）与使用带有 `O_SYNC` 标志打开的文件名进行比较，后者在每次我们写入文件时都会更新文件内容。每种方案的性能将取决于许多因素，包括底层的操作系统的实现、驱动器的速度以及文件系统的类型。

通过这个例子，我们看到了 `fcntl` 的必要性。我们的程序在描述符（标准输出）上操作，永远不知道在该描述符上打开的文件名。由于文件是由 shell 打开的，我们无法在打开文件时设置 `O_SYNC` 标志。通过 `fcntl`，我们只需要知道打开文件的描述符，就可以修改描述符的属性。当我们需要描述非阻塞管道时（第 15.2 节），我们还需要另一个 `fcntl`，因为我们对于管道所拥有的只有描述符。

## 3.15 ioctl 函数

`ioctl` 函数一直是 I/O 操作的“万能工具”。任何无法用该类中其他一个函数表示的内容通常都通过 `ioctl` 来指定。终端 I/O 是该函数最大的用户。（当我们读第 18 章时，我们会看到 POSIX.1 已用单独的函数替换了终端 I/O 操作。）

```c
#include <unistd.h> /* System V */
#include <sys/ioctl.h> /* BSD and Linux */

int ioctl(int fd, int request, ...);

// 返回：错误时返回 -1，成功时返回其他值
```
