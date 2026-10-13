
或者 write(2) 系统调用。一旦读或写操作完成，其结果（错误或成功）会被放入由发起 I/O 的代码传入的数据结构中，并向调用进程发送一个信号（SIGIO），以表示 I/O 已完成，或因错误条件而无法完成。程序员需要为 SIGIO 信号编写一个信号处理程序，并根据应用的要求处理相应情况。

Sun 的内部基准测试与实测结果表明，kaio 的实现确实是值得付出的努力。开销的降低以及专门的设备驱动程序级软件的投入，带来了整体更快、更高效的异步 I/O 操作。在相对较小、负载较轻的系统中，改进不那么显著，典型的性能提升约为 5% 到 6%。随着系统规模（处理器数量和内存大小）的增大以及异步 I/O 请求数量（负载）的增长，kaio 方式提供了更具可扩展性的性能，在某些基准测试中性能提升最高可达 30%。当然，具体效果会因环境而异。

kaio 实现为可加载内核模块 /kernel/sys/kaio，并在第一次调用异步 I/O 时加载。你可以使用 modinfo(1M) 判断该模块是否已加载。

```text
# modinfo | grep kaio
105 6084c000  2efd 178  1 kaio (kernel Async I/O)
```

如果上述命令没有返回任何内容，则仅表示 kaio 内核模块尚未加载。系统会在需要时自动加载它。

你可以运行一个相对简单的测试来判断给定文件是否支持 kaio。过程包括编译并运行一个调用 aioread(3) 的小程序，然后对程序使用 truss(1) 来观察系统调用活动。下面是 C 语言源代码。

```c
/*
 * Quick kaio test. Read 1k bytes from a file using async I/O.
 * To compile:
 * cc -o aio aio.c -laio
 *
 * To run:
 * aio file_name
 */
#include <stdio.h>
#include <sys/types.h>
#include <sys/fcntl.h>
#include <sys/aio.h>

#define BSIZE 1024

main(int argc, char *argv[])
{
        aio_result_t res;
        char buf[BSIZE];
        int fd;

        if ((fd = open(argv[1], O_RDONLY)) == -1) {
                perror("open");
                exit(-1);
        }
        aioread(fd, buf, BSIZE, 0, SEEK_SET, &res);
        await(0);
        if (res.aio_return == BSIZE) {
                printf("aio succeeded\n");
                close(fd);
                exit(0);
        }
        perror("aio");
}
```

编译好测试程序后，使用 truss(1) 命令对执行路径进行系统调用跟踪。

```text
# truss -t kaio,lwp_create aio /dev/rsd0c3d0s0
kaio(5, 0xEFFFFFE0, 0xEFFFFFEF, 0xEF6BF50, 0x00000000, 0x00000000) = 0
lwp_create(0xEFFFFFE10, 0, 0xE6FBF44)
 lwp_create(0x00000000, 0x00000000) = 0
kaio(AIOREAD, 3, 0xEFFFFF190, 1024, 0, 0xEFFFF590) = 0
kaio(AIOWAIT, 0x00000000, 0x00000000) = -268438128
aio succeeded
```

请注意，运行此测试需要使用 root 身份，因为它会直接从原始设备特殊文件读取数据。在命令行中，为 truss 指定 -t 标志，以指示 truss 只跟踪 kaio 和 lwp_create 系统调用。

该示例使用原始设备特殊文件作为 aio 程序的参数。（调用 aio 时，必须为文件指定完整路径名。）truss(1) 输出显示一个 kaio 系统调用，随后是两个 lwp_create 调用，最后是两次进入 kaio 例程以执行实际读取，然后是 AIOWAIT。最后一行是 aio 程序的输出（aio succeeded）。在此示例中，kaio 实际上支持此 I/O 操作——带有 AIOREAD 标志的 kaio 调用没有返回错误。

在下面的示例中，该 I/O 不受 kaio 支持。

```text
# truss -t kaio,lwp_create aio /junkfile
kaio(5, 0xFFFFFFFF, 0xFFFFFFFF, 0x0EEBF510, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0x00000000, 0, 0xE6FF64) = 2
kaio(AIOREAD, 3, 0xFFFFFFFF, 1024, 0, 0xEFFFF590) Err#48 ENOTSUP
lwp_create(0xEFFFFDA8, 0, 0xE6FF64) = 3
lwp_create(0x00000000, 0, 0x00000000) = 278369456
lwp_create(0xEFFFFDA8, 0, 0xE6FF64) = 4
lwp_create(0x00000000, 0, 0x00000000) = 5278406320
lwp_create(0xEFFFFDA8, 0, 0xE6F64) = 5
lwp_create(0x00000000, 0, 0x00000000) = 6278443184
lwp_create(0xEFFFFDA8, 0, 0xE6FDD44) = 6
lwp_create(0x00000000, 0, 0x00000000) = 627848048
lwp_create(0xEFFFFDA8, 0, 0xE6F62F44) = 7
lwp_create(0x00000000, 0, 0x00000000) = 278516912
lwp_create(0xEFFFFDA8, 0, 0xE6F59F44) = 8
lwp_create(0x00000000, 0, 0x00000000) = -278553776
lwp_create(0xEFFFFDA8, 0, 0xE6F50F44) = 927859640
lwp_create(0xEFFFFDA8, 0, 0xE6F47F44) = 10
lwp_create(0x00000000, 0, 0x00000000) = 1278627504
lwp_create(0xEFFFFDA8, 0, 0xE6F00F44) = 11
lwp_create(0x00000000, 0, 0x00000000) = -278664368
kaio(AIOWAIT, 0x00000000) = Err#22 EINVAL
kaio(AIOWAIT, 0x00000000) = Err#22 EINVAL
kaio(AIONOTIFY, 17506) = 0
aio succeeded
```

在此示例中，我们读取的是文件系统中的一个文件。跟踪结果显示，我们的示例通过一个 kaio 系统调用进入内核，创建了几个 LWP，并尝试通过 kaio 机制执行异步 I/O。第二个 kaio 调用以 ENOTSUP（不支持）错误失败，系统随后回退到库实现，导致在 I/O 完成前创建了一堆线程（LWP）。请注意，程序输出的最后一行 aio succeeded 表明 aioread(3) 确实成功了——只是我们没有使用 kaio 机制来完成它。

很明显，用户线程实现会导致更多的线程/LWP 创建和管理，从而增加开销、降低效率。那么，为什么 Solaris 环境会为单个异步 I/O 请求创建 11 个 LWP？答案与异步 I/O 库的初始化有关。

第一次调用 aioread(3) 或 aiowrite(3) 时，会调用异步 I/O 库的初始化例程，并创建多个工作线程来执行异步 I/O。系统只是在准备处理多个异步 I/O，因此创建了四个读 LWP 和四个写 LWP，外加一个用于文件同步的线程。这正好解释了上面你看到的九次成功的 lwp_create 调用。如果你在测试程序中加入第二个 aioread(3) 或 aiowrite(3)，并使用 truss(1) 命令重新运行，就不会看到第二个异步 I/O 对应的所有这些 lwp_create 调用。库会使用初始化期间创建的工作线程来处理后续的异步 I/O 请求（当然，为了跟上传入的异步 I/O 请求负载，它也会创建更多工作线程）。

虽然预先创建工作线程池有助于为用户线程异步 I/O 机制提供更好的可扩展性，但与内核异步 I/O 相比，它仍然涉及更多开销和更长的代码路径。

## 11.5 内存映射文件 I/O

到目前为止所讨论的文件 I/O 都是通过 read、write 和 lseek 系统调用完成的，这些调用代表进程执行 I/O，并将数据复制到进程的地址空间或从进程的地址空间复制出来。I/O 先在内核缓冲区中进行，然后再复制到进程地址空间或从进程地址空间复制出来，如图 11.3 所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_550_0.png)

图 11.3 *使用 read(2) 读取文件*

![](img/220ae4af07df2fe8e5be69d27f885d1b_551_0.png)

图 11.4 *内存映射文件 I/O*

mmap(2) 系统调用的函数定义如下所示。

```c
void *mmap(void *addr, size_t len, int prot, int flags, int filedes, off_t off);
```

**头文件** <sys/mman.h>

调用 mmap 系统调用时，需要传入一个打开的文件句柄、被映射文件的偏移量和长度、映射在进程地址空间中的地址和长度、一个选项标志，以及一个保护类型，用于指明该映射应使用的内存保护，如下所示。

```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
        MAP_SHARED, fd, offset)) == NULL) {
        perror("mmap failed");
        exit(1);
}
```

