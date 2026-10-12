
# 第 3 章 — 配置与调优 I/O

要在 Solaris 上的 Oracle 7 Server 中启用异步 I/O，需要设置 `init.ora` 参数 `async_read=true` 和 `async_write=true`。在 Oracle 8 和 Oracle8i 中，设置 `init.ora` 参数 `disk_async_io=TRUE`。在 Solaris 上，文件系统和原始设备都支持异步 I/O。Solaris 上的异步 I/O 由异步 I/O 库 `libaio.so` 处理。要在 Solaris 上发起异步 I/O 调用，可以调用 Solaris I/O 库 `libaio.so` 提供的 `aioread()` 和 `aiowrite()` 函数。Solaris I/O 库使用线程来处理非阻塞读写。Solaris 2.6 和 Solaris 7 对异步 I/O 层进行了重大改进。Solaris 2.6 支持对 POSIX 异步 I/O 调用 `aio_read()` 和 `aio_write()`，这些调用由 `libposix4` 共享库提供。在 Solaris 上，Oracle Server 使用 Solaris 的 I/O 调用。

从 Solaris 2.5.1 开始，Sun Ultra 系统 `sun4u` 支持对大于 2 GB 的文件的异步 I/O。Solaris 2.6 通过提供基于 64 位文件偏移的大文件支持，提供了创建大于 2 GB 文件的能力。

根据特定平台，通常使用 `SIGIO` 和 `SGAIO` 信号在异步 I/O 请求完成后通知进程。

## 标准的 Solaris 异步 I/O 调用

标准的 Solaris 异步 I/O 调用 `aioread()` 和 `aiwrite()` 支持对大小不超过 2 GB 的文件进行异步 I/O。这是由于 `libaio.so` 共享库使用 `lseek()` 系统调用来定位文件偏移。`lseek()` 调用仅支持 32 位文件偏移，而 `lseek()` 系统调用通过允许 64 位文件偏移扩展了 `lseek()` 系统调用。`pread64()` 和 `aiwrite64()` 支持基于 64 位文件的大文件异步 I/O。这允许 Oracle 中使用更大的数据文件，从而允许对大于 2 GB 的文件进行异步 I/O。Solaris 上的 Oracle8 和 Oracle 支持大文件的异步 I/O。

在 Oracle 2.6 中配合文件系统的异步 I/O 出现过一些问题。如果你正在运行 Solaris 2.6 且数据库基于文件系统，建议通过 `init.parameter` 禁用异步 I/O。Solaris 7 通过支持文件系统的异步 I/O 解决了这些问题。此外，值得注意的是，文件系统上的异步 I/O 通常不会产生太大收益，因为当向同一文件发出并发 I/O 请求时，Solaris 会获取 vnode（即文件）的独占写锁。为了解决这个问题，请确保你有许多小文件，而不是少数大文件，或者使用 Veritas Quick I/O 选项。I/O 模拟了基于文件系统的设备行为。

## 3.9 异步 I/O

```
/dev/async crw-rw---- oracle dba 150
```

`/dev/async` 的权限应允许 Oracle 读写。例如，如果 `/dev/async` 的权限与上述示例不同，请使用以下命令设置正确的权限。

```
chown oracle /dev/async
chgrp dba /dev/async
chmod 660 /dev/async
```

除了创建 `/dev/async` 设备外，还应设置内核参数 `max_async_ports`，用于指定同时打开异步设备的进程数。`max_async_ports` 设置过低会导致进程在尝试打开异步设备时失败。

### 3.9.2 HP-UX 中的异步 I/O

若要在 HP 上启用异步 I/O，Oracle 7 在 `init.ora` 中使用 `use_async_io=TRUE`，Oracle 8 和 Oracle8i 使用 `disk_async_io=TRUE`。在 HP 上，你必须使用 SAM 工具在驱动程序区域配置磁盘驱动器。之后必须重新生成内核并重启。使用 SAM 工具重新生成内核。新内核将在 `/stand/build/vmunix_test` 创建，用于创建内核的相应文件位置为 `/stand/build/SYSTEM.SAM`。

为了使新更改生效，使用 `mv` 命令移动 `/stand/build/vmunix_test`，并将配置文件 `/stand/build/SYSTEM.SAM` 配置到 `/stand/system.SAM`。在将新生成的内核移动到 `/stand` 目录之前，请记住备份旧内核和旧配置文件。一旦将新生成的内核和相应的配置文件移动到 `/stand`，请重启系统以强制异步更改生效。HP 上的异步 I/O 仅在访问原始（字符）设备时才会使用。这意味着如果你的数据库由文件系统组成，将不会使用异步 I/O。

### 3.9.3 SEQUENT 中的异步 I/O

若要在 Sequent 上启用异步 I/O，Oracle 7 使用 `async_write=TRUE`，Oracle8i 使用 `disk_async_io=TRUE`。异步 I/O 仅支持原始设备。异步 I/O 通过 `/usr/lib/libsq` 库的 DIO 接口处理，该接口提供了可以执行直接 I/O 和异步 I/O 的多个程序。`DIO_Read()` 和 `DIO_Write()` 系统调用用于对原始设备执行异步 I/O。Sequent 还通过 `DIO_Read64()` 和 `DIO_Write64()` 系统调用提供了大文件 I/O 支持。如果你计划使用异步 I/O，还应设置某些与异步 I/O 相关的内核参数。`MAXIO` 和 `NABUF` 内核参数分别指定并发异步 I/O 请求的最大数量。对于重 I/O 系统，将 `MAXIO` 设置为 512，`NABUF` 设置为 1024。记住，异步 I/O 请求在请求完成或取消之前会持有数据内存映像。因此，当发出大量异步 I/O 请求时，内存可能会迅速减少。为 `NABUF` 和 `MAXIO` 设置高值时，请确保你有足够的内存。

### 3.9.4 ORACLE 中的异步 I/O

Oracle Server 在 UNIX 平台上提供了异步 I/O。异步 I/O 通过执行非阻塞 I/O 提高了 DBMS 性能。它通过避免等待每个 I/O 完成而阻塞 DBWR 的标准（同步）I/O 调用，也实现了高吞吐量。异步 I/O 的概念非常简单。在同步

## 第3章 - I/O 的配置与调优

在 I/O 中，每次写入或读取都可能会阻塞，直到调用本身完成。这意味着每个 LGWR 和 DBWR 发出的对日志文件和数据文件的写入，每个相应的进程都必须等待（阻塞）直到每个写入调用完成。这可能会导致 LGWR 和 DBWR 产生瓶颈，并导致其他 Oracle 进程等待 SGA 中的空间，因为 LGWR 和 DBWR 尚未完成它们的脏写。如果你配置 Oracle 服务器使用异步 I/O，需设置 Oracle 7 的 `init.ora` 参数 `db_writer=1`。在 Oracle 8 `8.0.4` 中，设置 `init.ora` 参数 `db_writer_processes=1`。由于启用了异步 I/O，DBWR 和 LGWR 在写入时将不会阻塞。因此，不需要多个 DBWR 进程，除非 DBWR 无法跟上缓冲区缓存的负载。你可以通过查看 `v$system_event` 视图，检查是否有大量时间消耗在“free buffer waits”来此判断。使用异步 I/O 并设置 `db_processes=1` `Oracle 7` 或 `db_writer=1` `Oracle8` 和 `Oracle8i` 可以减少多个 Oracle 后台进程的开销。它消除了主 DBWR 与从进程之间的互连通信；当 `db_writers=1` 时，只有一个 DBWR 进程。

## 3.10 ORACLE8 中的 I/O 从进程
