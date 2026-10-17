
异步（并行）I/O (AIO) 减少了缓冲读/写确认之间的等待时间。如果支持，请使用 KAIO，它是 AIO 的额外增强，在内核内部处理 UFS 或原始磁盘，而不是内核之上。因此，它更快。确保设置以下默认启的 `init.ora` 参数：

```
ASYNC_WRITE=TRUE
ASYNC_READ=TRUE
或在某些平台上用 `ASYNC_IO=TRUE` 代替上述两个参数。
```

# 使用多个数据库写入器 (DBWRs)

如果你没有使用 AIO，请设置以下 `init.ora` 参数：

```
DB_WRITERS=<包含数据文件的不同磁盘数量>
```

根据需要将此值增加到包含数据文件的磁盘数量的两倍。这在不使用异步 I/O 的情况下实现了 I/O 并行，因为每个 DBWR 的 I/O 默认是同步的。优先使用 KAIO，其次是多个 DBWR，最后，但不要将这三者同时使用。

# 使用 readv() 系统调用

对于顺序 I/O，`readv()` 减少了缓冲区到缓冲区之间的传输时间。`readv()` 系统调用默认被禁用。通过设置以下内容启用它：

```
USE_READADV=TRUE
```

# 优先使用磁盘外道

由于 Sun 使用了带区记录 (ZBR) 技术，外层道往往优于内层道。外层道是第 0、1 和 3 道，而不是 4、5、6 和 7 道。

> 记住，不要使用第 2 道（重叠道），因为它保留了磁盘的总体尺寸。当这道道发生变化时，某些程序会感到困惑。

# 使用 Oracle POSTWAIT 驱动程序

如果你的平台可用，Oracle postwait 驱动程序提供了一种信号量（semaphores）的替代机制，它更快且为 Oracle 使用提供了与信号量相同的功能。

# 使用 ipcs 或 tstshm 监控共享内存和信号量

监控共享内存使用带 `-mb` 选项 UNIX 进程间通信状态 (`ipcs`) 命令，或者如果有，使用 Oracle 内存工具 (`tstshm`)。监控信号量使用 `ipcs -sb`。这些工具帮助你确定使用了多少共享内存和多少信号量。它们还可以帮助你确定共享内存的碎片情况。详情请参 `ipcs` 页面。以下是每个工具的示例运行：

- # `ipcs -mb`

IPC status from <running system> as of Nov 18 11:59:34

IPC status from <running system> as of Nov 18 11:59:34

Shared Memory:

| ID | KEY | OWNER GROUP | SEGSZ |
| :--- | :--- | :--- | :--- |
| 0 | 0x00000000 | oracle gba | 20968 |
| 1 | 0x00000001 | oracle gba | 20968 |
| 2 | 0x00000002 | oracle gba | 20968 |
| 3 | 0x00000003 | oracle gba | 20968 |
| 4 | 0x00000004 | oracle gba | 20968 |
| 5 | 0x00000005 | oracle gba | 20968 |
| 6 | 0x00000006 | oracle gba | 20968 |
| 7 | 0x00000007 | oracle gba | 20968 |
| 8 | 0x00000008 | oracle gba | 20968 |
| 9 | 0x00000009 | oracle gba | 20968 |
| 10 | 0x00000010 | oracle gba | 20968 |
| 11 | 0x00000011 | oracle gba | 20968 |
| 12 | 0x00000012 | oracle gba | 20968 |
| 13 | 0x00000013 | oracle gba | 20968 |
| 14 | 0x00000014 | oracle gba | 20968 |
| 15 | 0x00000015 | oracle gba | 20968 |
| 16 | 0x00000016 | oracle gba | 20968 |
| 17 | 0x00000017 | oracle gba | 20968 |
| 18 | 0x00000018 | oracle gba | 20968 |
| 19 | 0x00000019 | oracle gba | 20968 |
| 20 | 0x00000020 | oracle gba | 20968 |
| 21 | 0x00000021 | oracle gba | 20968 |
| 22 | 0x00000022 | oracle gba | 20968 |
| 23 | 0x00000023 | oracle gba | 20968 |
| 24 | 0x00000024 | oracle gba | 20968 |
| 25 | 0x00000025 | oracle gba | 20968 |
| 26 | 0x00000026 | oracle gba | 20968 |
| 27 | 0x00000027 | oracle gba | 20968 |
| 28 | 0x00000028 | oracle gba | 20968 |
| 29 | 0x00000029 | oracle gba | 20968 |
| 30 | 0x00000030 | oracle gba | 20968 |
| 31 | 0x00000031 | oracle gba | 20968 |

Semaphores:

| ID | KEY | OWNER GROUP | NSEMS |
| :--- | :--- | :--- | :--- |
| 0 | 0x00000000 | oracle gba | 1 |
| 1 | 0x00000001 | oracle gba | 1 |
| 2 | 0x00000002 | oracle gba | 1 |
| 3 | 0x00000003 | oracle gba | 1 |
| 4 | 0x00000004 | oracle gba | 1 |
| 5 | 0x00000005 | oracle gba | 1 |
| 6 | 0x00000006 | oracle gba | 1 |
| 7 | 0x00000007 | oracle gba | 1 |
| 8 | 0x00000008 | oracle gba | 1 |
| 9 | 0x00000009 | oracle gba | 1 |
| 10 | 0x00000010 | oracle gba | 1 |
| 11 | 0x00000011 | oracle gba | 1 |
| 12 | 0x00000012 | oracle gba | 1 |
| 13 | 0x00000013 | oracle gba | 1 |
| 14 | 0x00000014 | oracle gba | 1 |
| 15 | 0x00000015 | oracle gba | 1 |
| 16 | 0x00000016 | oracle gba | 1 |
| 17 | 0x00000017 | oracle gba | 1 |
| 18 | 0x00000018 | oracle gba | 1 |
| 19 | 0x00000019 | oracle gba | 1 |
| 20 | 0x00000020 | oracle gba | 1 |
| 21 | 0x00000021 | oracle gba | 1 |
| 22 | 0x00000022 | oracle gba | 1 |
| 23 | 0x00000023 | oracle gba | 1 |
| 24 | 0x00000024 | oracle gba | 1 |
| 25 | 0x00000025 | oracle gba | 1 |
| 26 | 0x00000026 | oracle gba | 1 |
| 27 | 0x00000027 | oracle gba | 1 |
| 28 | 0x00000028 | oracle gba | 1 |
| 29 | 0x00000029 | oracle gba | 1 |
| 30 | 0x00000030 | oracle gba | 1 |
| 31 | 0x00000031 | oracle gba | 1 |

- # `ipcs -sb`

IPC status from <running system> as of Nov 18 11:59:34

Semaphores:

| ID | KEY | OWNER GROUP | NSEMS |
| :--- | :--- | :--- | :--- |
| 0 | 0x00000000 | oracle gba | 1 |
