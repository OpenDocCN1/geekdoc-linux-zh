
# 头文件 `<sys/async.h>`

这些例程允许调用进程在发出读或写请求后继续处理。发出异步读或写的线程在 I/O 操作完成或发生错误条件时，通过信号（`SIGIO`）接收通知。该实现基于调用线程将数据结构传递给异步 I/O 读写调用。调用结果设置在结构体的一个成员中；调用程序必须测试结果以确定 I/O 是否成功或是否遇到错误。传递的结构体在发生错误时提供了存储错误号的空间（结构体在 `libaio` 和 `libposix4` 接口之间是不同的）。

# 11.4.1 文件系统异步 I/O

异步 I/O 通过用于普通文件系统的用户态线程库，以及用于原始磁盘设备的私有内核接口（内核异步 I/O）来实现。`aioread(3)` 和 `aiowrite(3)` 的实现创建了一个 I/O 请求队列，并通过用户级线程处理它们。当进入 `aioread(3)` 或 `aiowrite(3)` 时，系统会将 I/O 放入队列并创建一个 LWP（线程）来执行 I/O。当 I/O 完成（或发生错误）时，LWP 返回，并通过特殊信号 `SIGIO` 通知调用者。程序员必须安置一个信号处理程序来接收 `SIGIO` 并采取适当的行动。此类行动至少必须通过读取相应的结构体成员（结构体在 `libaio` 和 `libposix4` 接口之间不同）来包含或写的返回状态。

作为基于信号的 `SIGIO` 通知的替代方案，你可以在发出 `aioread(3)` 或 `aiowrite(3)` 后调用 `aiowait(3)`。这会使调用线程阻塞，直到挂起的异步 I/O 完成。你可以设置一个时间值并作为参数传递给 `aiowait(3)`，以便系统等待指定的时间，如下所示。

```
aio_result_t *aiowait(const struct timeval *timeout);
```

# 11.4.2 内核异步 I/O

尽管异步 I/O 的线程实现对许多应用程序效果良好，但对于需要大量使用异步 I/O 设施的应用程序，它并不一定能提供最优性能。例如，传统的数据库系统广泛使用异步 I/O 接口。与用户线程创建、管理和调度相关的开销促使了需要更少开销并提供更好性能和扩展性的实现设计。对现有异步 I/O 架构的审查以及随后的工程努力产生了一种被称为内核 I/O（或 `kaio`）的实现。

`kaio` 首次出现在 Solaris 2.4（带有少量修订补丁），并且从那后的每个 Solaris 版本中都可用（带有某些限制）。这些限制与哪些设备和软件支持、哪些不支持有关。对于应用程序来说，好消息是，存储设备、卷管理器和文件系统的组合是否存在 `kaio` 支持是透明的。如果存在 `kaio` 支持，将会被使用。如果没有，则将使用原始基于库的异步 I/O。应用程序不需要为了利用 `kaio` 而改变。系统会找出哪些是可用并进入相应的代码路径。

正如名称所示，`kaio` 是在内核内部实现异步 I/O，而不是在用户态通过用户线程实现。基本事件序列是：

- 当应用程序调用 `aioread(3)` 或 `aiocwrite(3)` 时，进入相应的库例程。
- 进入后，库例程首先尝试用 `kaio` 处理请求。执行 `kaio` 初始化并创建一个“清理”线程，该线程旨在确保在异步 I/O 过程中没有剩余分配但未释放的内存段。
- 一旦完成……

对 `kaio` 的支持需要在设备驱动层具有特定的异步 I/O 读写例程。Solaris 内核为所有当前销售 Sun 存储产品的 SCSI 驱动程序以及 Solstice DiskSuite (`SDS`) 设备驱动程序提供了这种支持。这些产品包括基于光纤的存储产品，它们在纤上实现了 SCSI 协议。

# Solaris 文件与文件 I/O

设备驱动程序级的支持可以带来整体更快、更高效的 I/O 操作。在规模较小、负载较低的系统中，这种改进并不显著，典型的性能提升在 5 到 6 百分比之间。随着系统规模（处理器数量和内存容量）的增加以及异步 I/O 请求（负载）的增长，`kaio` 方法提供了更具可扩展性的性能，在某些基准测试中改进幅度高达 30%。当然，具体效果取决于你的使用场景。

`kaio` 实现为一个可加载内核模块 `/kernel/sys/kaio`，并在第一次调用异步 I/O 时加载。你可以通过 `modinfo(IM)` 来判断该模块是否已加载。

```
$ modinfo | grep kaio

105 608c4000 2efd178 1 kaio (kernel Async I/O)
```

如果上述命令没有返回任何内容，则意味着 kaio 内核尚未加载。系统会根据需要自动加载。

你可以运行一个相对简单的测试，来确定特定文件是否可用 kaio 支持。这涉及编译并运行一个小型程序，该程序调用 `airead(3)` 并对程序使用 `truss(1)` 来监控系统调用活动。首先，这里是 C 语言源代码。

```c
* Quick kaio 测试。使用异步 I/O 从文件读取 lk 字节。
* 编译：
* cc -o aio.c -laio
* 运行：
* aio file_name
 *
#include <sys/stdio.h>
#include <sys/types.h>
#include <sys/fcntl.h>
#include <sys/aio.h>
#define BSIZE 1024
main(int argc, char *argv[])
{
    aio_result t res;
    char buf[BSIZE];
    int fd;
    if ((fd = open(argv[1], O_RDONLY)) == -1) {
        perror("open");
        exit(-1);
    }
    airead(fd, buf, BSIZE, 0, SEEK_SET, &res);
    aitwait(0);
    if (res.aio_return == BSIZE) {
        printf("aio succeeded\n");
        close(fd);
        exit(0);
    }
    perror("aio");
}
```

# 异步 I/O

一旦编译好测试程序，使用 `truss(1)` 命令对执行路径进行系统调用跟踪。

```
# truss -t kaio,kaio create aio /dev/rdsk/c0t3d0s0                                                              = 9
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 2
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio_create(3, 0xFFEFF19, 1024, 0xFFEFB590)                                     = -268438128
kaio (AIOWAIT, 0x00000000)
aio succeeded
```

注意，你以 root 身份运行此命令是因为它直接从原始设备特定文件读取。在命令中，通过 truss 指定 `-t` 标志，指示 truss 只跟踪 `kaio` 和 `lwp_create` 系统调用。

示例使用了原始设备特定文件作为 `aio` 的参数。当你调用 `aio` 时，必须指定文件的完整路径。`truss(1)` 输出显示了句 kaio 系统调用，随后是两个 `lwp_create` 调用，然后是进入 kaio 例程进行实际读取，最后是 `aitwait`。最后一行是 kaio 的输出（aio succeeded）。在这个示例，kaio 实际上支持此 I/O 操作——带有 `AIREAD` 标志的 kaio 调用没有返回错误。

在另一个示例中，该 I/O 不支持 kaio。

```
# truss -t kaio,kaio create junk
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 2
```
