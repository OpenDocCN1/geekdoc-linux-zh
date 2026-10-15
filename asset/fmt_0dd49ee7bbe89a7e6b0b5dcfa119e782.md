
```
$ pfiles 585
585: /spacel/framemaker,v5.5/bin/sunxm.s5.sparc -xrm *iconX:0 -xrm
  Current limit: 64 file descriptors
0: S_IFCHR mode:0066 dev:32,dev:24 ino:143523 uid:0 gid:3 rd:13,2
O_WRONLY_APPEND_LARGEFILE
1: S_IFCHR mode:0066 dev:32,dev:24 ino:143523 uid:0 gid:3 rd:13,2
O_WRONLY_APPEND_LARGEFILE
2: S_IFCHR mode:0066 dev:32,dev:24 ino:143523 uid:0 gid:3 rd:13,2
O_WRONLY_APPEND_LARGEFILE
3: S_IFIFO mode:0066 dev:117,0 ino:41312 uid:0 gid:0
O_WRONLY_NONBLOCK_FD_CLO
4: S_IFREG mode:0664 dev:32,dev:36 ino:41276324 uid:0 gid:0 size:0
O_WRONLY_LARGEFILE_FD_CLO  to nscd[202]
5: S_IFREG mode:0064 dev:32,dev:9 ino:198281 uid:10 gid:10 size:297984
6: S_IFREG mode:0664 dev:32,dev:8 ino:256 uid:19 gid:10 size:29696
O_RDWR_FD_CLO
7: S_IFREG mode:0664 dev:32,dev:8 ino:198281 uid:10 gid:10 size:0
O_RDWR_FD_CLO
8: S_IFREG mode:0664 dev:32,dev:8 ino:266 uid:19 gid:10 size:0
O_RDWR_FD_CLO
9: S_IFCHR mode:0000 dev:32,dev:24 ino:38607 uid:0 gid:0 size:41104
O_RDONLY_FD_CLO
10: S_IFREG mode:0664 dev:32,dev:9 ino:198281 uid:10 gid:10 size:65083
O_RDONLY_CLO
11: S_IFREG mode:0664 dev:32,dev:8 ino:666 uid:10 gid:10 size:4096
O_RDWR
```

在前面的示例中，`pfiles` 命令在 `PID` 585 上执行。`PID` 和进程名被转储，随后是打开的文件列表。对于每个文件，我们看到文件描述符（左侧的数字）、文件类型、文件模式、源设备、节点号、UID 和文件。

# 11.2 编程接口 (APIs)

Solaris 中有多个 API 执行文件 I/O。这些包括标准 I/O——通用缓冲 I/O 机制——以及多种低级系统 I/O。传统的 C 缓冲被称为标准 I/O 函数，简写为 `std`。它们是贝尔实验室于 1976 年添加到 Unix V6 的缓冲 I/O 接口；它们以标准 I/O 机制的形式出现。`stdio` 库存在底层系统调用之上。

在不同类型的系统 I/O 中，最基础的是 `read` 和 `write` 系统调用。更高级（更更新）是通过以下方式实现的 POSIX I/O：

- 通过 `pread` 和 `pwrite` 系统调用
- 通过 `read` 和 `write` 系统实现的 scatter/gather I/O

异步 I/O 通过 `aio_read(3)` 和 `aio_write(3)` 接口实现（`posix` 库的一部分），以及 `aio_read(3)` 和 `aiowrite(3)`（`libaio` 库的一部分）。两组异步 I/O 提供类似的功能，区别在于应用程序代码中的用法。

图 11.2 显示了各种文件相关 API 与底层内核子系统之间的通用关系。

![](img/6356e5c1ac2ea1083732d1b35ecf75_530_0.png)

图 11.2 内核 I/O 接口关系

### 11.2.1 标准 I/O (stdio)

标准 I/O 函数允许文件作为字节的“流”打开，称为文件流。这种方法允许 C 程序通过读写字符和任意长度的字符串来访问文件，而底层库处理实现实际 I/O 操作所需的系统调用。这种设计的优点是它是完全可移植的，即使跨不同的操作系统，程序员不需要考虑任何依赖于机器的特性，例如与文件系统块的对齐。

例如，C 程序可以一次一个字节地读取文件，而不是通过 1 字节 I/O 从磁盘读取，标准 I/O 库会对 I/O 进行缓冲，以便文件系统和 I/O 子系统能以高效的大小读取。标准 I/O 缓冲以每次 I/O 额外的处理开销为代价。

标准 I/O 文件流的基本处理器是 `FILE` 句柄，通过调用 `fopen` 获取。一旦建立了文件句柄，有一套标准 I/O 程序可以句柄执行流 I/O。

传统的 Unix 文件句柄联合在 `<stdio.h>` 中定义 `FILE` 结构，对于直到 Solaris 2.6 版本也是如此。从 Solaris 7 开始，`FILE` 结构定义在 `stdio_impl.h` 中（标准 I/O 头文件的一种）。32 位 `FILE` 结构成员定义如下：以下是针对 32 位和 64 位实现的 `FILE` 结构的两种不同定义。

```
#define _LP64
struct _FILE_TAG {
    long _pad[16];
};
#else
struct _FILE_TAG {
#ifdef _STDIO_REVERSE
    unsigned char *ptr; /* 缓冲区中下一个从此处的字符 */
    size_t _cnt; /* 缓冲区中可用字符数 */
    unsigned char *ptr2; /* 缓冲区中下一个从此处的字符 */
#else
    size_t _cnt; /* 缓冲区 */
    unsigned char *flag; /* 流的状态 */
    unsigned char *file; /* 文件描述符 */
    unsigned char _orientation; /* 流的方向 */
    unsigned char _file6;
#endif
};
```

## 11.3.2 文件打开模式和文件描述符标志

Solaris 环境支持 `O_DELAY` 和 `O_NONBLOCK`。当打开文件时，内核会检查 `O_DELAY` 和 `O_NONBLOCK` 位。如果设置了 `O_DELAY`，则阻塞直到操作完成。如果设置了 `O_NONBLOCK`，操作将失败并将 `errno` 设置为 `EAGAIN`（提示程序员再次尝试）。阻塞意味着内核将进程或线程放入睡眠。当事件发生时（在此例中为文件被释放），内核发出唤醒信号并将进程放入调度队列等待执行。

正如 `open(2)` 手页所述，如果在 `open(2)` 调用中同时设置了这两个标志，`O_NONBLOCK` 标志优先且内核会清除 `O_DELAY` 位。为了维持对文件的读写操作的阻塞（非阻塞）需求，`FNDAY` 被设置在文件结构中。`NONBLOCK`/`NDELAY` 标志在 vnode 或 inode 层没有相应的标志，因为内核不需要将这些信息向下传递。

要查看设置了哪些标志，请使用带有 `F_GETFD` 参数的 `fcntl(2)`。

### 11.3.2.1 非阻塞 I/O

非阻塞 I/O 正如其名，指示系统防止读写操作阻塞。内核实现此点的特定条件取决于文件类型。

对于普通文件，当与强制锁结合使用时可以实现非阻塞 I/O。如果对普通文件尝试读写且存在记录锁，则读写将阻塞直到操作完成。如果设置了 `O_NONBLOCK` 标志，操作将失败并将 `errno` 设置为 `EAGAIN`。

对于其他类型，如套接字、命名管道（FIFO）和设备特殊文件，可能没有数据可读（例如从尚未写入数据的命名管道或套接字读取）。如果没有 `O_NONBLOCK` 或 `O_NDELAY` 标志，读取将简单阻塞直到数据可用。

### 11.3.2.2 独占打开

`O_EXCL` 标志（独占打开）可以配合 `O_CREAT` 标志使用，请求系统在文件已存在时返回错误。如果文件不存在且都设置了这两个标志，文件的创建和向调用进程返回文件描述符的过程保证是原子的。原子性意味着涉及的步骤将完全完成，且不会被其他因素改变状态。原子性使得应用程序能够可靠地创建锁文件，这些文件通常被应用程序实现为持久同步的手段。

`O_CREAT` 标志指示系统在文件不存在时创建该文件。下面的伪代码演示了在不同条件下打开文件的结果。以下信息假设所有其他权限条件均满足

# 系统文件 I/O
