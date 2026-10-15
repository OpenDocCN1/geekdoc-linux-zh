
```
# rm /mnt/hello
# cat /snap/hello
# ls -l /snap
total 128098
-rw-r-- 1 root other 655600 Mar 9 11:28 64m
drw-xr-x 2 root 8192 Mar 9 11:27 last+found
# ls -l /mnt
total 128096
-rw-r-- 1 root other 655600 Mar 9 11:28 64m
drw-xr-x 2 root 8192 Mar 9 11:27 last+found
```

为了完全演示其工作原理，再次考虑原始文件系统的大小。UFS 文件系统为 100MB 并包含一个 64MB 的文件。快照位于 10MB 的 VxFS 系统中。以下显示从 UFS 文件系统中删除 64MB 文件时发生的情况：

```
# rm /mnt/64m
# df -k
```

## 基于磁盘的文件系统案例研究 223

| Filesystem | kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/dsk/c07d0s0 | 1521031 | 1653877 | 13315944 | 12% | / |
| /proc | 0 | 0 | 0 | 0% | /proc |
| fd | 0 | 0 | 0 | 0% | /dev/fd |
| mntab | 0 | 0 | 0 | 0% | /etc/mntab |
| swap | 4705000 | 16 | 4704984 | 1% | /var/run |
| swap | 4705000 | 16 | 4704984 | 1% | /tmp |
| /dev/vx/dsk/fsnap | 95983 | 9 | 86376 | | /mnt |
| /dev/vx/dsk/snap | 102240 | 840 | | 13% | /snap-space |
| /dev/fsnap | 95983 | 64050 | 22325 | 75% | /snap |

注意 64MB 文件删除后，快照使用的空间减少了。因为 64MB 文件的数据块是空闲但未被覆盖，因此不需要将它们复制到快照设备。然而，如果使用 `dd` 在 UFS 文件系统中创建另一个文件如下：

```
# dd if=/dev/zero of=/mnt/64m bs=65536 count=1000
1000+0 records in
1000+0 records out
```

创建了一个新文件，分配了块并覆盖，原始内容被复制到快照。由于没有足够的空间复制 64MB 数据，快照空间耗尽，导致系统内核消息。VxFS 文件系统报告空间不足。由于没有更多数据可以复制到快照，快照不再激活并自动删除。

* Mar 9 11:03:03 vxfs: [ID 330226 kern.notice]

NOTICE: mgscnt 2 vxfs: msgseq 001: vx_namespace /dev/vx/dsk/snap1 file system (full block)

* Mar 9 11:03:03 fsnap: [ID 433356 kern.warning]

WARNING: fsnap_write_taskq: error writing to backing file. DELETING SNAPSHOT 0, backing path /snap-space/snapshot0, offset 1272972 bytes, error 5.

* Mar 9 11:03:03 fsnap: [ID 433356 kern.warning]

WARNING: fsnap_write_taskq: error writing to backing file. DELETING SNAPSHOT 0, backing path /snap-space/snapshot0, offset 12648448 bytes, error 5.

* Mar 9 11:03:03 fsnap: [ID 894761 kern.warning]

WARNING: Snapshot 0 automatically deleted.

为了确认空间不足的文件系统，最后运行一次 `df`：

| Filesystem | kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/dsk/c07d0s0 | 1521031 | 1653877 | 13315944 | 12% | / |
| /proc | 0 | 0 | 0 | 0% | /proc |
| fd | 0 | 0 | 0 | 0% | /dev/fd |
| mntab | 0 | 0 | 0 | 0% | /etc/mntab |
| swap | 4705000 | 16 | 4704984 | 1% | /var/run |
| swap | 4705000 | 16 | 4704984 | 1% | /tmp |
| /dev/vx/dsk/fsnap | 95983 | 9 | 86376 | | /mnt |
| /dev/vx/dsk/snap | 102240 | 840 | | 13% | /snap-space |
| /dev/fsnap | 95983 | 64050 | 22325 | 75% | /snap |

## ext2 文件系统的特性

下面显示了 ext2 支持的主要特性：

**4TB 文件系统。** 这要求在 VFS 层中进行更改。请注意，最大文件和文件系统的大小是底层文件系统和内核实现的属性。

**255 字节文件名。** 目录条目的长度是可变的，最大大小为 255 字节。

**可选的文件语义。** 通过挂载选项，管理员可以选择使用 BSD 还是 SVR4 文件语义。这在创建文件时会对比组 ID（group ID）产生影响。在 BSD 语义下，创建的文件将具有与父目录相同的组 ID。对于 System V 语义，如果目录设置了组 ID，则新文件将继承父目录的组 ID，子目录继承父目录的组 ID 和组 ID 位；否则，文件和目录将继承调用进程的主组 ID。

**多个文件系统块大小。** 可以在 `mkfs` 中指定作为选项的 1024、2048 和 4096 字节的块大小。

**预留空间。** 文件系统最多有 5% 的空间可以留给仅限 root 用户的文件，以便在文件系统损坏时进行某些恢复。

**每个文件属性。** 可以在文件或目录上设置属性以影响随后的访问。这在下一节中进行了详细描述。

**类 BSD 同步更新。** 挂载选项确保所有元数据（inode、位图、间接块和目录）在修改时都会同步写入磁盘。这以牺牲性能为代价，增加了文件系统的完整性。

**定期文件系统检查。** 为了强制执行文件系统的完整性，ext2 有两种方法可以确保在文件系统上频繁地多次调用完整的 `fsck`。系统会保留一个计数，直到达到指定的计数次数，就会调用一次完整的 `fsck`。或者，可以使用基于时间的系统来确保定期对文件系统进行清理。

**快速符号链接。** 与 VxFS 一样，符号链接存储在 inode 本身中，而不是单独的分配块中。

接下来的章节将更详细地描述这些特性。

## 每个文件属性

除了上一节列出的特性外，还有一组每个文件的属性，可以使用 `chattr` 命令设置并使用 `lsattr` 显示。支持的属性包括：

- `EXT2_SECRM_FL`。使用此属性，每当文件被截断时，数据块首先会被随机数据覆盖。这确保了一旦文件被删除，文件数据在后后的阶段无法在另一个文件中恢复。

- `EXT2_UNMR_FL`。此属性允许文件被撤销。

- `EXT2_SYNC_FL`。使用此属性，文件元数据（包括间接块）在更新后将始终同步写入磁盘。但注意，这并不适用于普通文件数据。

- `EXT2_COMPR_FL`。文件被压缩。所有随后的访问必须使用压缩和解压缩。

- `EXT2_APPEND_FL`。使用此属性，文件只能以追加模式（`O_APPEND`）打开进行写入。人都无法删除该文件。

- `EXT2_IMMUTABLE_FL`。如果设置了此属性，文件只能被读取，不能被任何人删除。

属性可以设置在普通文件和目录上。设置在目录上的属性对于在目录内创建的文件来说是不可更改的。下面的示例显示了如何在文件上设置不可变属性。首先将 `passwd` 文件复制到当前目录，并显示其对 root 可写。调用 `chmod` 命令设置该属性，可以通过调用 `lsattr` 显示。这两次操作显示已无法删除该文件或扩展该文件：
