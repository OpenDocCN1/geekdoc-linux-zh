
1. `read_inode`：从文件系统读取 inode。它仅从 `iget4()` 中的 `fs/inode.c:get_new_inode()`（因此也包括 `iget()`）调用。如果文件系统希望使用 `iget()`，则必须实现 `read_inode()` – 否则 `get_new_inode()` 将引发 panic（内核恐慌）。在读取 inode 期间它是锁定的（`inode->i_state = I_LOCK`）。当函数返回时，所有等待在 `inode->i_wait` 上的进程都会被唤醒。文件系统的 `read_inode()` 方法的工作是定位包含要读取的 inode 的磁盘块，并使用缓冲区缓存 `bread()` 函数将其读入，并初始化 inode 结构的各个字段，例如 `inode->i_op` 和 `inode->i_fop`，以便 VFS 层知道可以在该 inode 或对应文件上执行哪些操作。未实现 `read_inode()` 的文件系统是 ramfs 和管道。例如，ramfs 有自己的 inode 生成函数 `ramfs_get_inode()`，根据需要调用所有的 inode 操作。

2. `write_inode`：将 inode 写回磁盘。类似于 `read_inode()`，它需要定位磁盘上相关的块，并通过调用 `mark_buffer_dirty(bh)` 与缓冲区缓存交互。当 inode 需要单独或作为整个文件系统同步的一部分进行同步时，此方法会在脏 inode（那些用 `mark_inode_dirty()` 标记为脏的 inode）上调用。

3. `put_inode`：每当引用计数减少时调用。

4. `delete_inode`：每当 `inode->i_count` 和 `inode->i_nlink` 都达到 0 时调用。文件系统删除 inode 的磁盘副本，并调用 VFS inode 的 `clear_inode()` 以“以最极端的方式终止它”。

5. `put_super`：在 `umount(2)` 系统调用的最后阶段调用，以通知文件系统应释放关于此实例的任何私有信息。通常，这会 `brelse()` 包含超级块的块，并 `kfree()` 为空闲块、inode 等分配的任何位图。

6. `write_super`：当超级块需要写回磁盘时调用。它应找到包含超级块的块（通常保存在 `sb-private` 区域）并 `mark_buffer_dirty(bh)`。它还应清除 `sb->s_dirt` 标志。

7. `statfs`：实现 `statfs(2)` 系统调用。注意，作为参数传递的 `struct statfs` 指针是内核指针，而不是用户指针，因此我们不需要执行任何到用户空间的 I/O。如果未实现，则 `statfs(2)` 将因 `ENOSYS` 而失败。

8. `remount_fs`：每当文件系统正在重新挂载时调用。

9. `clear_inode`：从 VFS 层的 `clear_inode()` 调用。将私有数据附加到 inode 结构（通过 `generic_ip` 字段）的文件系统必须在此处释放它。

### 3.6 虚拟文件系统示例：pipefs

那么，让我们来看看挂载一个基于磁盘的（`FS_REQUIRES_DEV`）文件系统时会发生什么。 `mount()` 系统调用的实现在 `fs/super.c:sys_mount()` 中，它只是一个包装器，将选项、文件系统类型和设备名称复制给 `do_mount()` 函数，而真正的繁重工作是由 `do_mount()` 完成的：

- 如果必要，加载文件系统驱动程序，并增加其模块的引用计数。请注意，在挂载操作期间，文件系统模块的引用计数被增加了两次——一次是 `do_mount()` 调用 `get_fs_type()` 时，另一次是如果 `read_super()` 成功，`get_sb_dev()` 调用 `get_filesystem()` 时。第一次增加是为了防止我们在 `read_super()` 方法内部时模块被卸载，而第二次增加是为了表明该模块正被此挂载实例使用。显然，`do_mount()` 在返回前会减少计数，因此总体而言，每次挂载后计数只增加 1。

- 由于在我们的情况下，`fs_type->fs_flags & FS_REQUIRES_DEV` 为真，超块通过调用 `get_sb_bdev()` 进行初始化，该函数获取对块设备的引用，并与文件系统的 `read_super()` 方法交互以填充超块。如果一切顺利，`super_block` 结构体将被初始化，我们将拥有对文件系统模块的额外引用以及对底层块设备的引用。

- 分配一个新的 `vfsmount` 结构体，并将其链接到 `sb->s_mounts` 列表和全局的 `vfsmnt_list` 列表。 `vfsmount` 字段 `mnt_instances` 允许找到所有挂载在相同超块上的实例。 `mnt_list` 字段允许找到系统中所有超块的所有实例。 `mnt_sb` 字段指向此超块，而 `mnt_root` 持有 `sb->s_root` 目录项（dentry）的新引用。

作为一个不需要块设备即可挂载的 Linux 文件系统的简单示例，让我们来看看 `fs/pipe.c` 中的 pipefs。文件系统的序言相当简单明了，几乎不需要解释：

```c
static DECLARE_FSTYPE(pipe_fs_type, "pipefs", pipefs_read_super,
                      FS_NOMOUNT|FS_SINGLE);

static int __init init_pipe_fs(void)
{
    int err = register_filesystem(&pipe_fs_type);
    if (!err) {
        pipe_mnt = kern_mount(&pipe_fs_type);
        err = PTR_ERR(pipe_mnt);
        if (!IS_ERR(pipe_mnt))
            err = 0;
    }
    return err;
}

static void __exit exit_pipe_fs(void)
{
    unregister_filesystem(&pipe_fs_type);
    kern_umount(pipe_mnt);
}

module_init(init_pipe_fs)
module_exit(exit_pipe_fs)
```

文件系统类型为 `FS_NOMOUNT | FS_SINGLE`，这意味着它不能从用户空间挂载，且系统范围内只能有一个超块。 `FS_SINGLE` 标志还意味着它必须通过 `kern_mount()` 进行挂载（在它通过 `register_filesystem()` 成功注册之后，这正是 `init_pipe_fs()` 中所做的）。此函数中唯一的 bug 是，如果 `kern_mount()` 失败（例如，因为 `add_vfsmnt()` 中的 `kmalloc()` 失败），那么文件系统将保持已注册状态，但模块初始化失败。这将导致 `/proc/filesystems` 失败。（我刚刚发送了一个补丁给 Linus，指出虽然这不是当今的一个真正的 bug，因为管道不能被编译为模块，但应该考虑到将来它可能会变成模块化的观点）。

`register_filesystem()` 的结果是 `pipe_fs_type` 被链接到 `file_systems` 列表中，因此可以读取 `/proc/filesystems` 并找到其中的“pipefs”条目，其中带有“nodev”标志，表明未设置 `FS_REQUIRES_DEV`。 `/proc/filesystems` 文件实际上应该增强以支持所有新的 `FS_` 标志（我制作了一个补丁来实现这一点），但由于这会破坏所有使用它用户应用程序，所以无法这样做。尽管 Linux 内核接口在用户空间兼容性方面每分钟都在变化（只有改进），但 Linux 是一个非常保守的操作系统，它允许许多应用程序在很长一段时间内无需重新编译即可使用。

`kern_mount()` 的结果是：

- 通过在 `unnamed_dev_in_use` 位图中设置一位来分配一个新的未命名（匿名）设备号；如果没有更多位可用，则 `kern_mount()` 以 `EMFILE` 失败。

- 通过 `get_empty_super()` 分配一个新的超块结构体。 `get_empty_super()` 函数遍历由 `super_block` 引导的超块列表，寻找空条目，即 `s->s_dev == 0`。如果找不到这样的空超块，则使用 `GFP_USER` 优先级通过 `kmalloc()` 分配一个新的。系统范围内超块的最大数量在 `get_empty_super()` 中进行检查，因此如果开始失败，可以调整可调节的 `/proc/sys/fs/super-max`。
