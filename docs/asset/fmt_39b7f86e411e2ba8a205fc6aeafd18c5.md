
## 24.3.3 ZFS File System Commands and the `zfs` Command

The subcommands and options shown in this section are presented in the following general way, with Solaris syntax shown by default.

- `x.` What the command, subcommand, and options accomplish.

  The command, subcommand, options, and command arguments

  Commentary or explanation.

  Further examples:

  More variations of the command, subcommand, options, and command arguments

  Commentary or explanation.

### 1. Displaying ZFS file systems

```
zfs list
```

Lists all ZFS file systems.

Further examples:

```
zfs list -t filesystem
zfs list -t snapshot
zfs list -t volume
zfs list -t all -r poolname
```

Lists different types (file system, snapshot, volume) by `poolname`.

```
zfs list -r data01/sarwar
```

Recursive display.

```
zfs list -o poolname,mounted,sharenfs,mountpoint
```

Complex listing: there are a number of attributes that you can use in a complex listing; see the man page for `zfs`.

### 2. How to create a file system

```
zfs create data01/sarwar
```

Presumes a pool called `data01`, creates a `/data01/sarwar` ZFS file system.

Further examples:

```
zfs create -o mountpoint=/users/data01/users data01/sarwar
```

Creates at a different mount point.

### 3. How to destroy a file system

```
zfs destroy data01/sarwar
```

Further examples:

```
zfs destroy -r data01/sarwar
```

```
zfs destroy -R data01/sarwar
```

Uses the recursive options `-r` (all children), `-R` (all dependents).

### 4. How to mount a file system

```
zfs mount data01
```

Further examples:

```
zfs mount -o mountpoint=/tmpmnt data01/sarwar
```

You can create a temporary mount that expires after unmounting. You can apply all the normal mount options—that is, `ro/rw`, `setuid`, and so on.

### 5. How to unmount a file system

```
zfs umount data01
```

### 6. How to share a file system

```
zfs share data01
```

Further examples:

```
zfs set sharenfs=on data01
```

This file system persists after reboots!

```
zfs set sharenfs="*rw@192.168.0.13/24" data01/sarwar
```

Shares with specific hosts.

### 7. How to unshare a file system

```
zfs unshare data01
```

Further examples:

```
zfs set sharenfs=off data01
```

此文件系统在重启后仍然持久存在！

### 8. 如何对文件系统进行快照

对文件系统进行“快照”就像拍照一样：当原始文件系统发生变化时，变化会被记录到快照中；要删除一个数据集，必须先删除所有之前的快照。你也可以重命名快照。如果快照存在克隆，则无法销毁该快照。

```
zfs snapshot data01@10022010
```

创建快照。

更多示例：

```
zfs snapshot data01@10022010 data01@mybackup
```

重命名快照。

```
zfs destroy data01@10022010
```

销毁快照。

### 9. 如何回滚文件系统

默认情况下，你只能回滚到最新的快照。要回滚到更旧的快照，必须删除所有更新的快照。

```
zfs rollback data01@10022010
```

### 10. 克隆/提升文件系统

克隆是从快照升级而来的可写文件系统。只要克隆存在，对快照的依赖就会保留。克隆使用快照中的数据来存在。随着你使用克隆，它会使用与快照分开的空间。克隆不能跨 `zpool` 创建，你需要使用 `zfs send/receive` 命令来完成此操作，如示例 24.4 所示。

```
zfs clone data7@10022010 data8/clone
```

```
zfs clone -o mountpoint=/clone data7@10022010 data8/clone
```

克隆，并更改克隆的挂载点。

更多示例：

```
zfs promote data8/clone
```

提升克隆。这允许你销毁克隆所附属的原始文件系统。克隆必须位于同一个池中！

### 11. 重命名文件系统

```
zfs rename data03/koretksy_disk01 data03/koretksy_d01
```

数据集必须保留在同一个池内。此命令有两个选项：`-p` 创建所有不存在的父数据集；`-r` 递归重命名所有后代数据集的快照（仅与快照一起使用）。

### 12. 文件系统的压缩

```
zfs set compression=lzjb data03/sarwar
```

你可以通过设置特性来启用压缩。压缩选项有 `on`、`off`、`lzjb`、`gzip`、`gzip[1-9]` 和 `zle`。压缩仅在你打开时才开始；其他现有数据不会被压缩。

更多示例：

```
zfs get compressratio data03/sarwar
```
