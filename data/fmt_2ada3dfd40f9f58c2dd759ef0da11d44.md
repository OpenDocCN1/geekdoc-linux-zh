
在第一行，我们可以看到测试程序在 `open(2)` 和 `dup(2)` 执行后打印了三个打开的文件描述符值。每个进程已经分配了文件描述符 0、1 和 2，因此，两个通过 `open` 和 `dup` 得到的文件是文件描述符 3、4 和 5。`pfiles` 命令转储了进程打开文件的信息，我们看到 `fd 4` 和 `fd 5` 设置了 `O_SYNC` 标志，这是符合逻辑的，因为它们引用了同一个文件结构。

# 系统 I/O

现在，我们通过崩溃（IM）来阐述测试程序中的文件结构共享。

```
# /etc/crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> p 59
PROC TYPE SIZE = 1962
SLOT ST PID PGID SID UID PRI NAME FLAGS
59 24774 24774 24774 20821 0 ofd load
> u 59
PER PROCESS USER AREA FOR PROCESS 59
PROCESS MISC:
command: ofd; parsgs: ofd
start: Tue Apr 21 21:55:51 1998
mem 6349, type: exec
vnode of current directory: 60025394
OPEN FILES, FILEPATH, AND THREAD RECNT:
[0] F 0x06824ca8, 0 [1] F 0x06824ca8, 0
[2] F 0x06824c58, 0 [3] F 0x06824c58, 0
[4] F 0x06824770, 0 [5] F 0x06824770, 0
> f 60824c58
ADDRESS RECNT TYPE/ADDR OFFSET FLAGS
60824c58 1 UFS/6082a88 0 read write
> f 60824770
ADDRESS RECNT TYPE/ADDR OFFSET FLAGS
60824770 2 UFS/6082a88 0 read write
```

`crash` 工具转储了每个进程的 `uarea`。它提供了相应文件结构的地址。如你所见，`fd 3` 和 4 引用了不同的文件，尽管我们在同一个进程中打开了同一个文件。文件描述符 4 和 5 显示了相同的文件结构（`60824770`），因为 5 是 4 的转储。`f`（file）工具转储了文件结构。我们首先转储了 3 的文件结构（`f 60824c58`），然后转储了 4 的（`f 60824770`）。你可以看到该文件结构的引用计数为 2，你还可以看到同步文件在文件结构中，就像原始的 `open(2)` 系统调用一样。`TYPE/ADDR` 列提供了 vnode 的类型和内核地址。注意，vnode 是相同的，因为系统中的任何打开文件都只有一个且仅 vnode。

## 11.3.2 read 和 write 系统调用

POSIX 标准提供了两个接口（如下所示），用于执行基本的读/写 I/O。这些接口与 `read()` 和 `write()` 系统调用类似，但允许将文件偏移量作为系统调用的一部分设置。

```
ssize_t read(int fd, void *buf, size_t nbyte, off_t offset);
ssize_t write(int fd, const void *buf, size_t nbyte, off_t offset);
```

头文件 `<unistd.h>`

通过 `pread(2)` 和 `pwrite(2)`，只需一个系统调用即可在特定偏移处启动读取或写入，而不是使用同时使用 `seek(2)` 和 `read()` 的传统方法。

## 11.3.2 readv 和 writev 系统调用

所示所示 `readv()` 和 `writev()` 系统调用与 `read()` 和 `write()` 系统调用类似，但允许数据在内存地址范围之间进行传输，而不是从单个内存缓冲区。这种技术被称为分散/聚集（scatter/gather）I/O。

```
ssize_t readv(int fd, const struct iovec *iov, int count);
ssize_t writev(int fd, const struct iovec *iov, int count);
```

`iovec` 结构体提供了内存缓冲区的基地址和长度。

```
struct iovec {
    void *iov_base;
    size_t iov_len;
};
```

头文件 `<unistd.h>`

将时间值作为参数传递给 `aiowait(3)`，以便系统只等待指定的时间，如下所示。

```
aio_result_t *aiowait(const struct timeval *timeout);
```

## 11.4.2 内核异步 I/O

尽管线程库实现的异步 I/O 对许多应用程序效果良好，但对于大量使用异步 I/O 设施的应用程序，它并不一定能提供最优性能。例如，商业关系型数据库系统广泛使用了异步 I/O 接口。创建、管理和调度用户线程相关的开销促使人们设计一种开销更小、提供更好性能和可扩展性的实现。通过对现有异步 I/O 架构及后续工程实践的审查，产生了一种名为内核异步 I/O（或 kaio）的实现。

Kaio 首次出现于 Solaris 2.4（带有少量补丁），从此后的每个 Solaris 版本中都可用，但受到某些限制。这些限制与哪些设备和软件包含 kaio 支持以及哪些不包含。对于应用程序而言，好消息是，存储设备、卷管理器和文件系统组合是否存在 kaio 支持是透明的。如果存在 kaio 支持，将会被使用；如果不存在，则将使用基于库的原始异步 I/O。应用程序为了利用 kaio 无需更改。系统会识别哪些功能可用并进入相应的代码路径。

正如其名所示，kaio 在内核内部实现异步 I/O，而不是在用户态通过用户线程实现。I/O 队列在操作系统中创建和管理。基本的事件发生顺序如下：

- 当应用程序调用 `aioread(3)` 或 `aiowrite(3)` 时，会进入相应的库例程序。

- 进入后，库例程序首先尝试用 kaio 处理请求。将执行 kaio 初始化例程并创建一个“清理”线程，该线程旨在确保在异步 I/O 过程中不会出现分配但未释放的内存段。

- 完成后，调用 kaio，此时将进行测试以确定对所请求的 I/O 是否请求 kaio。

对 kaio 的支持需要在设备驱动程序级需要特定的异步 I/O 和写例程。Solaris 内核为所有当前销售的 Sun 存储产品的 SCSI 驱动程序以及 Solstice DiskSuite (SDS) 设备驱动程序提供了这种支持。这些产品包括基于光纤的存储产品，它们在光纤通道连接上实现了 SCSI 协议。

## 异步 I/O

Kaio 仅当异步 I/O 目标是字符设备文件时有效。换句话说，kaio 仅在原始磁盘设备 I/O 上工作。随着用于在 SPARC/Solaris 上创建 RAID 卷的主机卷管理软件，增加了额外的支持：基于 Veritas 的 Enterprise Volume Manager 以及 Solstice DiskSuite。使用 Veritas 或 DiskSuite 创建的 RAID 设备通过 `/dev/vx/rdsk` 和 `/dev/md/rdsk` 设备特殊文件具有原始设备入口点，且为这些卷管理器实现的伪根包含了用于 kaio 的异步 IO 例程。你也可以使用下面描述的 kaio 测试来确定你的底层设备是否支持 kaio。

如果 kaio 可用，发生的情况如下：

- 内核从队列中分配一个 `aio_req` 结构（或通过 `kmem_alloc` 在内核内存中创建一个新的），并调用相应驱动程序中的异步 IO 例程。

- 在驱动程序内部，会设置所需的内核数据结构以支持 I/O，并进入异步特有的物理 I/O 例程 `physio`。

- 同步原始设备 I/O 使用内核 `physio` 函数，而内核会设置内核缓冲区并调用驱动策略执行实际的设备 I/O。

- `physio` 例程通过缓冲区 `biowait()` 内核代码等待驱动例程完成。

- `physio` 例程设置异步 I/O 支持结构和信号机制，然后在等待 I/O 完成的同时调用驱动策略。

出现 `ENOTSUP` 错误信号表示不支持 kaio 支持。这意味着，`libaio` 例程（或如果使用 POSIX 接口则使用 `libposix4`）会发起系统调用，如果不支持 kaio，kaio 调用将返回 `ENOTSUP` 错误。如果 kaio 不可用，所采用的代码路径大不相同。

- 通常，用户线程异步 I/O 设施在异步 I/O 队列中执行 I/O，并将 `aiwrite` 交给在初始化 `libaio` 库时创建的工作线程（在示例后有更多介绍）。

- 代表调用进程执行 I/O 的线程使用 `read(2)` 和 `pwrite(2)` 系统调用进入内核。
