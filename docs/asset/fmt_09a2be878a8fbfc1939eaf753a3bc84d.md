
当 Oracle 通过其相应的进程 `DBWR` 或 `LGWR` 写入数据文件或日志文件时，写入是非延迟的。在大多数 UNIX 平台上，Oracle 在打开文件时使用 `O_SYNC` 标志。`O_SYNC` 标志导致数据和文件控制块信息被物理写入磁盘（而不是缓存）。使用 `O_SYNC` 标志是为了保证一致性，因为 Oracle 必须确保数据被物理写入并正确分布，以避免写入期间出现 I/O 瓶颈。即使使用文件系统并拥有较大的 UNIX 文件系统缓存，写入仍会被物理写入磁盘。Oracle 的写入速度高度依赖于 Oracle Server 的配置。

## 3.21 调整 I/O

`vxfs` 文件系统类型提供了额外的挂载选项，例如 `convync` 和 `nolog`。您可以使用 `convync-direct` 或 `dsync` 选项挂载文件系统。`direct` 选项导致读写跳过 UNIX 文件系统缓存，直接从磁盘和用户空间进行读写。在重度 I/O 负载下，使用传统的文件系统 I/O 的 I/O 性能提升了 50%。`dsync` 选项与 `open()` 系统调用配合使用时，会导致写入阻塞直到数据物理写入磁盘，但 inode 信息除外。信息被延迟并稍后写入磁盘。如果发生高程度的文件系统写入并发，`dsync` 选项可以提供 20–30% 的性能提升。如果您的系统和/应用程序没有从 UNIX 文件系统缓存的优势中获益，使用 `dsync` 选项的直接 I/O 可以增加 I/O 性能。

您还可以使用 `nolog` 选项，它可以禁用文件系统日志。这会提高性能；但文件系统的可靠性会降低。使用 `nolog` 选项，您必须使用 `fsck` 工具通过全扫描来修复文件系统。如果没有日志文件，文件系统在崩溃后可能无法恢复。

以下是使用 `vxfs` 选项的示例：

```
myhost {root}->-> mount -F vxfs -o convync-direct \
/dev/vx/dsk/vol1 /mount-point
```

```
myhost {root}->-> mount -F vxfs -o convync-dsync \
/dev/vx/dsk/vol1 /mount-point
```

```
myhost {root}->-> mount -F vxfs -o nolog \
/dev/vx/dsk/vol1 /mount-point
```

### 3.21.7 用于 Oracle 的 Veritas 数据库

除了 Veritas 文件系统，Veritas 还提供了用于 Oracle 的 Database Edition 和 Quick I/O Database Accelerator，后者比标准 UNIX 文件系统 `ufs` 提升了高达 90% 的性能。Quick I/O Database Accelerator 通过允许对数据库文件进行并行更新消除锁瓶颈，支持异步 I/O 并消除了双缓冲。Veritas Server Suite Edition for Oracle 使您的数据库性能大幅优于传统的 `ufs` 系统，如果出于某种原因您不想考虑原始设备，您应该考虑使用 Veritas Database Edition for Oracle 和 Quick I/O Database Accelerator 来帮助提高系统性能。

### 3.2.10 检查点

当 `DBWR` 将 SGA 中的所有脏数据库缓冲区（包括已提交和未提交的数据）写入数据文件时，就会发生检查点。检查点确保 SGA 中被修改的数据块被定期写入磁盘。`DBWR` 使用最不经常使用 `LRU` 算法将块从缓冲区中调出。在这里，如果没有发生检查点，频繁更改的活动块可能不会被写入磁盘。

检查点的另一个优势是，由于到检查点为止的所有更改已应用到数据文件，因此在实例恢复的情况下，不需要应用检查点的重做日志条目。在这里，检查点有助于缩短实例恢复时间。

检查点始终发生在从一个日志组切换到另一个日志组期间。Oracle 更新所有文件的头以指示检查点的发生。

### 3.2.18 VERITAS 文件系统和页面着色

页面着色算法通过这种方式布局文件来提高文件性能，将某些热块或页面分组在一起，从而最小化地减少 I/O。如果您正在使用 Veritas 文件系统 `vxfs`，存在一个已知 Bug 会严重降低 Oracle 可执行文件 `oracle` 等可执行程序的性能。该 Bug 是由于 Veritas 对 Veritas 系统中的文件使用页面着色算法导致的。由于 Veritas 页面着色 Bug，您的 Oracle 系统性能可能会下降高达 50%。例如，如果 `$ORACLE_HOME` 存在于 `vxfs` 文件系统中，数据库性能将随时间继续下降。许多客户通过定期关闭实例、将 oracle 二进制文件 `$ORACLE_HOME/bin/oracle` 复制到临时区域，然后使用 UNIX 复制命令 `cp` 将二进制文件复制回 `$ORACLE_HOME/bin` 来绕过此 Bug。Veritas File System 3.3.2 版本解决了页面着色问题；因此您应该升级到 3.3.2 或更高版本。您可以在 Solaris 上使用 `pkginfo` 命令确定运行的是哪个版本的 Veritas File System。

```
myhost> pkginfo -l RTXvxfs
```

| Field | Value |
| :--- | :--- |
| PKGINST | RTXvxfs |
| NAME | VERITAS File System |
| CATEGORY | utilities |
| VERSION | 3.3.2 |
| VENDOR | Veritas Software |
| DESC | Veritas File System |
| ARCH | sparc |
| DATE | Mar 09 |
| EMAIL | support@veritas.com |
| STATUS | installed |
| FILES | 14 |
| HOTLINE | 800 |
| INSTAMP | 12 |

### 3.21.19 写入锁定时的独占文件系统

当 Oracle 通过其相应的进程 `DBWR` 或 `LGWR` 写入数据文件或日志文件时，写入是非延迟的。在大多数 UNIX 平台上，Oracle 在打开文件时使用 `O_SYNC` 标志。`O_SYNC` 标志导致数据和文件控制块信息被物理写入磁盘（而不是缓存）。使用 `O_SYNC` 标志是为了保证一致性，因为 Oracle 必须确保数据被物理写入并正确分布，以避免写入期间出现 I/O 瓶颈。即使使用文件系统并拥有较大的 UNIX 文件系统缓存，写入仍会被物理写入磁盘。Oracle 的写入速度高度依赖于 Oracle Server 的配置。

# 第 3 章 · I/O 的配置与调

`TRUE`。开启检查点 `checkpoint` 过程可以通过允许独立进程处理数据文件头更新，并允许 `LGWR` 管理重做缓冲区 `redo buffer` 来提高性能。然而，如果你的系统处理器和内存有限，你可能希望考虑允许 `LGWR` 处理数据文件头更新。如果你的系统无法承受额外进程的开销，请将 `checkpoint_process` 设置为 `FALSE`。在 Oracle8 中，检查点进程 `CKPT` 默认启用，且 `init.ora` 参数 `checkpoint_process` 已经废弃。

Oracle8 使用多个恢复差异缓冲区 `recovery diff buffers` 队列来帮助减少完成恢复检查点所需的时间。在 Oracle8 之前，由于存在单个恢复差异缓冲区队列，多个 `DBWR` 进程可能会在检查点队列锁存 `latch` 上发生竞争。因此，完成恢复所需的时间与 `DBWR` 进程的数量 `db_writer_processes` 成正比。多个恢复差异缓冲区队列通过将恢复队列在各个 `DBWR` 进程之间进行分区来提高性能。

你还可以设置启动检查点的间隔时间。`init.ora` 中的 `log_checkpoint_interval` 指定了触发检查点所需的操作系统块数（通常每个块 512 字节）。如果上一次检查点产生的重做日志 `redo logs` 数量超过此数字，则会执行检查点。无论如何，每次重做日志切换 `redo log switch` 后都会发生检查点。当 `LGWR` 以循环方式从一个重做组切换到下一个组时，就会发生日志切换。你可以通过将 `log_checkpoint_interval` 设置为每个重做日志的大小来降低检查点的频率。在这种情况下，检查点只在日志切换后发生。然而，请记住，如果需要实例恢复或介质恢复，这将导致恢复时间增加，以确保检查点的频率将得到降低。

如果你的应用程序需要快速的恢复时间，你可能希望将 `log_checkpoint_interval` 设置为较小的值。你还需要设置 `init.ora` 参数 `log_checkpoints_to_alert=TRUE`。这将允许你通过检查位于 `background_dump_dest` 目录下的 `alert_SID.log` 文件来监控检查点的频率。
