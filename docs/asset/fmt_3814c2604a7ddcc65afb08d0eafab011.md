
44     .read        = `generic_file_read`,

45     .write       = `generic_file_write`,

56 };

#### 第 44–45 行

我们没有调用 `generic_file_read()`，而是调用了 `generic_file_write()`。`generic_file_write()` 获取文件的锁，以防止两个写入者同时写入同一个文件，并调用了 `generic_file_write_nolock()`。`generic_file_write_nolock()` 将文件指针和缓冲区转换为 `kbio` 和 `iovec` 参数，并调用页缓存写入函数 `generic_file_aio_write_nolock()`。

这就是写和读的分叉点。如果要写入的页不在页缓存中，写操作不会直接落设备。相反，它会将页读入页缓存，然后执行写操作。页缓存中的页不会立即写入磁盘；相反，它们被标记为“脏页”（dirty），并定期地将所有脏页写入磁盘。

370

第 6 章 • 文件系统

与 `read()` 函数 `readpage()` 有类似的函数。在 `generic_file_aio_nolock()` 中，`address_space_operations` 访问 `prepare_write()` 和 `commit_write()`，这两个都特定于它所在的文件系统类型。回想 `ext2_aops`，我们看到 ext2 驱动使用了自己的函数 `ext2_prepare_write()` 和通用函数 `generic_commit_write()`。

`fs/ext2/inode.c`

```c
628 static int

629 ext2_prepare_write(struct file *file, struct page *page,

630     unsigned from, unsigned to)

631 {

632     return block_prepare_write(page, from, ext2_get_block);

633 }
```

#### 第 632 行

`ext2_prepare_write()` 仅仅是通用文件系统函数 `block_prepare_write()` 的封装，后者传递了参数。

#### 6.5.4 刷新脏页

如果要写入的页不在页缓存中，写操作不会直接落设备。相反，它会将页读入页缓存，然后执行写操作。页缓存中的页不会立即写入磁盘；相反，它们被标记为“脏页”，并定期地将所有脏页写入磁盘。

与 `read()` 函数 `readpage()` 有类似的函数。在 `generic_file_aio_nolock()` 中，`address_space_operations` 访问 `prepare_write()` 和 `commit_write()`，这两个都特定于它所在的文件系统类型。回想 `ext2_aops`，我们看到 ext2 驱动使用了自己的函数 `ext2_prepare_write()` 和通用函数 `generic_commit_write()`。

`ext2_prepare_write()` 仅仅是通用文件系统函数 `block_prepare_write()` 的封装，后者传递了参数。

总结：写操作在以下情况下刷新脏页：
- 系统空闲内存低于阈值。
- 脏页达到一定时间。

> ^14 `pdflush` 进程相当复杂，对于我们追踪写的目的，可以忽略其复杂性。然而，如果你对细节感兴趣，`mm/pdflush.c`、`mm/fs-writeback.c` 和 `mm/page-writeback.c` 包含了相关代码。

```c
fs/ext2/inode.c

628 static int

629 ext2_prepare_write(struct file *file, struct page *page,

630     unsigned from, unsigned to)

631 {

632     return block_prepare_write(page, from, ext2_get_block);

633 }
```
