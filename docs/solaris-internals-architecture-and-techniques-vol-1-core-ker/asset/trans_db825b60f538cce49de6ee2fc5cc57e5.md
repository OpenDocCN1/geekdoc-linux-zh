
可用的标志提供了一层或另一种程度的同步 I/O 完整性保证。请参阅 `fcntl(1)` 手页获取有关文件和数据完整性的记录定义。

`O_RSYNC` 标志提供了读取同步，并与 `O_SYNC` 或 `O_DSYNC` 标志配合使用。使用 `O_SYNC` 标志时会强制文件完整性（数据和 inode）。使用 `O_DSYNC` 标志会强制数据完整性，这意味着任何对文件的待处理写入将在读取完成之前完成。如果同时设置了 `O_RSYNC` 和 `O_SYNC`，则在内核处理读取请求之前，完成完成处理的 I/O 并更新 inode 信息。在未设置任何 `O_SYNC` 标志的文件上发起的读取仅意味着从缓冲区读取时可能读取到尚未写入磁盘的数据。`open(2)` 和 `fcntl(1)` 手页并未明确说明 `O_RSYNC` 必须与 `O_SYNC` 或 `O_DSYNC` 使用，尽管这在某种程度上是隐含的。

各种数据标志在 inode 层没有对应的标志。inode 维护有标志，用于根据文件结构中 `O_SYNC` 标志的状态，在内核文件系统代码中（例如 `ufs_read()`, `ufs_write()`）指示同步操作。这些标志由内核在低级 I/O 程序中使用。Solaris 提供了两个库例程——`fdasync(3R)` 和 `fsync(3C)`，应用程序可以在执行读取或写入之前调用它们进行数据完整性同步。这些调用允许对文件同步数据到磁盘，并仅在写入非易失性存储器完成后才返回。

## 11.3.2 其他文件标志

其他标志维护在每个进程的文件描述符中，在文件描述符级别使用的标志大多供操作系统使用——它们不是用户可设置。

其中一个标志是 FEXEC：`close-on-exec` 标志。此标志通知操作系统，如果进程执行了 `exec(2)` 调用，则在新进程中关闭文件描述符。通常情况下，所有打开的文件都会被子进程继承，这并不总是期望的行为。内核通过从 `exec(2)` 调用的简单 `close_exec()` 内核例程实现 FEXEC。`close_exec()` 遍历文件描述符数组并关闭任何设置了 FEXEC 标志的文件。`fcntl(2)` 设置、清除和检查描述符的标志字段。目前，FEXEC 是唯一可以设置或清除的标志。

## 11.3.2.6 du dup 系统调用

`dup(2)` 系统调用允许我们复制文件描述符，使得两个描述符指向同一个文件条目。我们之前提到过，`open(2)` 调用会获取一个新的文件描述符并导致分配一个新的文件结构，即使该进程已经打开了相同的文件。`dup(2)` 复制文件描述符，并将该文件描述符产生一个新的 `u_entry` 结构。其区别在于，指向文件结构的 `uf_pointer` 将指向与被 `dup` 的描述符相同的文件结构。不会创建新的文件结构，这与对同一文件进行第二次 `open(2)` 的情况不同。

`dup(2)` 适用于程序员希望对同一个文件进行多个引用，以共享当前文件偏移量的相同视图的情况。由于当前的文件指针（字节偏移量）维护在文件结构中，被 `dup` 的描述符共享共同的文件偏移量视图。

考虑一个名为 `ofd` 的测试程序（代码未显示），它对同一个文件进行了两次 `open`。第二次 `open` 设置了 `O_SYNC` 标志（我们添加该标志仅是为了演示如何检查这些文件结构标志）。在两次 `open` 之后，执行了 `dup(2)` 来复制第二个文件描述符。以下是某些输出以及使用 `/usr/proc/bin/pfiles` 查看进程打开文件的示例。

```
$ ofd &
[1] 24788
fawlty.
fd: 3, fd2: 4, fd3: 5
/usr/proc/bin/pfiles 24788
Current limit: 64 file descriptors
0: S_IFCHR mode:0620 dev:32, ino:32408 gid:7 rdev:24,1
1: S_IFCHR mode:0620 dev:32, ino:32408 uid:2021 gid:7 rdev:24,1
2: S_IFCHR mode:0620 dev:32, ino:32408 uid:2021 gid:7 rdev:24,1
3: S_IFREG mode:0755 dev:32, ino:18 uid:2021 gid:30 size:0 ORDWR
4: S_IFREG mode:0755 dev:32, ino:18 uid:2021 gid:30 size:0 ORDWR|O_SYNC
5: S_IFREG mode:0755 dev:32, ino:18 uid:2021 gid:30 size:0 ORDWR
```

在第一行，我们看到在 `open(2)` 和 `dup(2)` 调用之后，测试程序打印了文件描述符值。每个进程分配了文件描述符 0、1 和 2，结果两个打开的文件和复制的文件是文件描述符 3、4 和 5。`pfiles` 命令输出了打开文件的信息，我们看到 fd 4 和 5 设置了 `O_SYNC` 标志，这是因为它们引用同一个文件结构。

现在我们使用 `crash(1)` 来说明测试程序中的文件结构共享。

```
# /etc/crash file = /dev/mem, namelist = /dev/, outfile = stdout
PROC TABLE SLOT PGID SID UID NAME FLAGS
S 5 24774 24716 20821 0 ofd
PROCESS USER AREA FOR PROCESS MISC:
command: ofd start: Tue Apr 21 21:55:1998
mem: 43493; type: inode of current directory: 6002534
OPEN FILES, AND THREAD RECNT:
[0]: 0xffff802ca8, 0, 0
[2]: 0xffff802ca8, 0, 0
[3]: 0xffff802c58, 0, 0
[4]: 0xffff824870, 0, 0
[5]: 0xffff824870, 0, 0
> f 0xffff802c58
ADDRESS RCNT TYPE/ADDR FLAGS
0xffff824870 1 UFS /008bae8 read write
> f 0xffff824870
ADDRESS RCNT TYPE/ADDR FLAGS
0xffff824870 2 UFS /008bae8 read write
```

`crash` 工具转储进程的 `uarea`。对于每个打开的文件，`crash` 提供了对应文件结构的地址。如你所见，尽管我们在同一个进程中打开了同一个文件，fd 3 和 4 引用了不同的文件结构。描述符 4 和 5 显示相同的文件结构地址 (0024870)，因为 5 是 4 的 `dup`。最后，`f` (file) 工具转储文件结构信息。我们首先转储 fd 3 的文件结构 (`f 002c58`)，然后是 fd 4 (`f 824870`)。你可以看到文件结构的引用计数为 2，因为有两个描述符正在引用它，你还可以看到文件结构中设置了 sync 标志，正如原始 `open(2)` 系统调用中所设置的那样。`f` 工具输出中的 TYPE/ADDR 列提供了 vnode 的文件和内核地址。请注意，vnode 是唯一的，因为系统中的任何打开文件都将只有一个 vnode、打开文件数和文件结构。

## 11.3.2 read 和 pwrite 系统调用

POSIX 标准提供了下面所示的接口用于执行基本的读取和 I/O。这些接口与 `read()` 和 `write()` 系统调用类似，但允许文件偏移量作为系统调用的一部分。

```
size_t pread(int fild, void *buf, size_t nbyte, off_t offset);
size_t pwrite(int fild, const void *buf, size_t nbyte, off_t offset);
```

### 头文件 <unistd.h>

通过 `pread(2)` 和 `pwrite(2)`，可以通过一个系统调用在特定偏移量处启动读取或写入，而不是使用结合 `seek()` 和 `read()` 系统调用的传统方法。

## 11.3.2.8 readv 和 writev 系统调用

`readv(3)` 和 `writev()` 系统调用（所示）与 `read(3)` 和 `write()` 系统调用类似，允许在范围内存地址范围内进行传输，而不是在单个内存缓冲区。这种技术通常被称为离散/聚集 I/O (scatter/gather I/O)。

```
size_t readv(int ildes, const struct iovec *iov, int iovcnt);
size_t writev(int ildes, const struct iovec *iov, int iovcnt);
```

### 头文件 <unistd.h>

每个 I/O 请求一个 iovec 结构数组和 iovec 结构数量。该 I/O 的总大小是所有 iovec 结构的大小之和。iovec 结构如下所示。

```
struct iovec {
    addr_t iov_base;
    int iov_len;
};
```

### 头文件 <unistd.h>

每个 iovec 结构提供了内存缓冲器的基地址和字节字节长度。因此，I/O 传输按照指定的模式读取或写入进程内存空间，并按顺序从或写入文件。

## 11.4 异步 I/O

异步 I/O 接口在 Solaris 中已可用了一段时间。Solaris 库中的一组特定接口提供了一种方法，使应用程序发出 I/O 请求而无需在 I/O 完成之前阻塞或停止工作。（不要将这种行为与文件描述符中未设置数据完整性标志时的 I/O 请求行为混淆。参见第 488 页的“数据完整性和同步标志”）

Solaris 中两组接口执行异步 I/O：`aioread(3)` 和 `aiowrite(3)` 例程；以及 POSIX 等效例程 `ai_read(3R)` 和 `write(3R)`，后者基于 POSIX 实时扩展标准。根据定义，实时应用程序必须处理不可预测的外部中断流，这些中断需要可预测的有边界的响应时间。
