
上述 `iostat` 输出显示，吞吐量从之前配置的每秒 3.3 MB 增加到每秒 8 MB，平均每秒 125 次读取。平均服务时间减少到 8.5 毫秒（之前为 78.1 毫秒）。通过 `iostat` 和 `sar`，可以识别出产生 I/O 冲突的设备。可能需要重新配置该设备或卷。

### 存储缓存

上述 `iostat` 输出显示，吞吐量从之前配置的每秒 3.3 MB 增加到每秒 8 MB，平均每秒 125 次读取。平均服务时间减少到 8.5 毫秒（之前为 78.1 毫秒）。通过 `iostat` 和 `sar`，可以识别出产生 I/O 冲突的设备。可能需要重新配置该设备或卷。

### 快速缓存

上述 `iostat` 输出显示，吞吐量从之前配置的每秒 3.3 MB 增加到每秒 8 MB，平均每秒 125 次读取。平均服务时间减少到 8.5 毫秒（之前为 78.1 毫秒）。通过 `iostat` 和 `sar`，可以识别出产生 I/O 冲突的设备。可能需要重新配置该设备或卷。

### 原始设备

上述 `iostat` 输出显示，吞吐量从之前配置的每秒 3.3 MB 增加到每秒 8 MB，平均每秒 125 次读取。平均服务时间减少到 8.5 毫秒（之前为 78.1 毫秒）。通过 `iostat` 和 `sar`，可以识别出产生 I/O 冲突的设备。可能需要重新配置该设备或卷。

性能。文件系统引入了额外的开销，包括文件锁定以及文件系统缓存和 inode 控制块的维护。原始设备为数据库管理员在确定文件文件大小和数据库文件布局方面提供了更大的灵活性。这允许 DBA 专注于分配 I/O，并根据容量和预期增长设置文件。

## 3.21.4 异步 I/O

使用原始设备的另一个优点是可以使用异步 I/O。如果您正在使用原始设备，则应该在 Oracle Server 中启用异步 I/O。在 Solaris 上，在 Oracle 7 中设置 `async_write=TRUE` 和 `async_read=TRUE`，在 Oracle 8 和 Oracle 8 中设置 `disk_asynch_io=TRUE`。在 HP 上，在 Oracle 7 中设置 `use_asynch_io=TRUE`，在 Oracle 8 和 Oracle 8 中设置 `disk_asynch_io=TRUE`。在 HP 上，您必须配置 `/dev/async` I/O 驱动程序。按照第 3 章中的说明在 HP 上配置异步 I/O 驱动程序。在 Sequent 上，在 Oracle 7 中设置 `async_write=TRUE`，在 Oracle 8 和 Oracle 8 中设置 `disk_asynch_io=TRUE` 以启用异步 I/O。如果您使用异步 I/O，在 Oracle 7 中设置 `init_ora parameter db_writer=1`，在 Oracle 8.4 或更高版本中设置 `db_writer_processes=1`。在某些情况下，如果数据库写入器落后，多个数据库写入可以提高吞吐量。异步 I/O 和原始设备的结合提供了高 I/O 吞吐量，并随着系统用户的增加最大化了可扩展性。

## 3.21.5 ORACLE 写入

当 Oracle 通过其相应的进程 `DBWR` 或 `LGWR` 写入数据文件或日志文件时，写入是非延迟的。在大多数 UNIX 平台上，Oracle 在打开文件时使用 `O_SYNC` 标志。`O_SYNC` 标志导致数据和文件控制块信息被物理写入磁盘（而不是缓存）。使用 `O_SYNC` 标志是为了保证一致性，因为 Oracle 必须确保数据被物理写入并正确分布，以避免写入期间出现 I/O 瓶颈。即使使用文件系统并拥有较大的 UNIX 文件系统缓存，写入仍会被物理写入磁盘。Oracle 的写入速度高度依赖于 Oracle Server 的配置。

## 3.21.6 VERITAS 文件系统挂载选项

如果您选择使用 Veritas 文件系统 (`vxfs`) 而原始设备，请确保挂载文件系统时不带有 `mcache=closesync`（参考 `vfstab` 选项文件）。`mcache=closesync` 选项会导致文件系统缓存仅在文件关闭时写入任何更新，从而降低了缓存的用处。该选项导致的性能下降约为 10%。

> 9. 有关不同类型标志的更多信息，请参考 `open()` 系统调用的手册页。

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

## 3.21.7 用于 Oracle 的 Veritas 数据库

除了 Veritas 文件系统，Veritas 还提供了用于 Oracle 的 Database Edition 和 Quick I/O Database Accelerator，后者比标准 UNIX 文件系统 (`ufs`) 提升了高达 90% 的性能。Quick I/O Database Accelerator 通过允许对数据库文件进行并行更新消锁瓶颈，支持异步 I/O 并消除了双缓冲。Veritas Server Suite Edition for Oracle 使您的数据库性能大幅优于传统的 `ufs` 系统，如果出于某种原因您不想考虑原始设备，您应该考虑使用 Veritas Database Edition for Oracle 和 Quick I/O Database Accelerator 来帮助提高系统性能。

## 3.2.18 VERITAS 文件系统和页面着色

页面着色算法通过这种方式布局文件来提高文件性能，将某些热块或页面分组在一起，从而最小化地减少 I/O。如果您正在使用 Veritas 文件系统 (`vxfs`)，存在一个已知 Bug 会严重降低 Oracle 可执行文件 (`oracle`) 等可执行程序的性能。该 Bug 是由于 Veritas 对 Veritas 系统中的文件使用页面着色算法导致的。由于 Veritas 页面着色 Bug，您的 Oracle 系统性能可能会下降高达 50%。例如，如果 `$ORACLE_HOME` 存在于 `vxfs` 文件系统中，数据库性能将随时间继续下降。许多客户通过定期关闭实例、将 `oracle` 二进制文件 (`$ORACLE_HOME/bin/oracle`) 复制到临时区域，然后使用 UNIX 复制命令 (`cp`) 将二进制文件复制回 (`$ORACLE_HOME/bin`) 来绕过此 Bug。Veritas File System 3.3.2 版本解决了页面着色问题；因此您应该升级到 3.3.2 或更高版本。您可以在 Solaris 上使用 `pkginfo` 命令确定运行的是哪个版本的 Veritas File System。

```
myhost> pkginfo -l RTXvxfs
```

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
```

## 3.21.19 写入锁定时的独占文件系统
