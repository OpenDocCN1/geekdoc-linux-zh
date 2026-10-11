
VFS 使用的另一个结构是 `file` 结构。当进程操作文件时，`file` 结构是 VFS 用来存储有关进程/文件关联信息的数据类型。与其他结构不同，`file` 结构不持有原始的磁盘数据；`file` 结构是在调用 `open()` 系统调用时动态创建的，并在调用 `close()` 系统调用时销毁。回第 3 章，在进程的生命周期内，进程打开的 `file` 结构通过进程描述符（`task_struct`）进行引用。图 6.7 展示了 `file` 结构如何与其他 VFS 结构关联。`task_struct` 指向文件描述符表，该表包含指向进程打开的所有文件描述符的指针列表。回文件描述符表的前三项对应于标准文件描述符。

![](img/6525157588f931c50a65c5a42af9a432_345_0.png)

图 6.7

文件对象

### 第 516 行

我们需要知道进程的所有者，以便在操作文件时确定文件访问权限。这些字段对应启动进程并打开文件结构的用户的 `uid` 和 `gid`。

### 第 517 行

文件可以提前从页缓存（page cache，即内存中的页集合）中读取页面。预读优化涉及在任何页面被请求之前读取文件的相邻页，以减少昂贵的磁盘访问次数。`f_ra` 字段持有类型为 `file_ra_state` 的结构，包含了所有与文件预读状态相关的信息。

### 第 527 行

此字段指向 `address_space` 结构，它对应该文件的页缓存机制。这在“页缓存”部分进行了详细讨论。

## 6.2.2 全局和局部列表引用

内核使用全局变量来持有指向前述结构链表的指针。所有结构都保在一个双向链表中。内核保留一个指向列表头的指针，并作为访问列表的入口。所有结构都有类型为 `list_head` 的字段，它们使用这些字段指向列表中的上一个和后一个元素。表 6.7 总结了内核持有的全局变量及其所引用的列表类型。

`super_block`、`file_system_type`、`dentry` 和 `vfsmount` 结构都保存在自己的列表中。Inode 可以在全局的 `inode_in_use` 或 `inode_unused` 中找到自己，也可以在它们对应的 `superblock` 局部列表中。图 6.9 显示了这些一些结构是如何相互关联的。

> `inode` 结构具有这种变体，称为 `hlist_node`，正如我们在 6.2.1.3 节“inode 结构”中看到的。

## 6.2 Linux 虚拟文件系统

表 6.7

VFS 相关的全局变量

| 全局变量 | 结构类型 |
| --- | --- |
| super_blocks | super_block |
| file_systems | file_system_type |
| dentry_unused | dentry |
| vfsmntlist | vfsmount |
| inode_in_use | inode |
| inode_unused | inode |

![](img/6525157588f931c50a65c5a42af9a432_350_0.png)

正在使用并已分配给 superblock 的 file 结构列表

未未使用但未分配给 superblock 的 file 结构列表

图 6.9

VFS 相关的全局变量

324

第 6 章 • 文件系统

`super_blocks` 变量指向 superblock 列表头，元素通过 `s_list` 字段指向列表中的上一个和下一个元素。`superblock` 结构中的 `s_dirty` 字段反过来指向它拥有的 inodes，这些 inodes 需要与磁盘同步。不在局部 superblock 列表中的 inodes 位于 `inode_in_use` 或 `inode_unused` 列表中。所有 inodes 都通过 `i_list` 字段指向列表中的下一个和上一个元素。

`superblock` 还通过 `s_files` 列表指向包含分配给该 superblock 的 file 结构的列表头。未分配的 file 结构被放置在 `anon_list` 列表的其中一个 `free_list` 列表中。这两个列表都以一个虚拟 file 结构作为列表头。所有 file 结构都使用 `f_list` 字段指向它们列表中的下一个和上一个元素。

参考图 6.6 以查看 inode 如何通过 `i_dentry` 字段指向 dentry 结构列表。

## 6.3 与 VFS 关联的结构

除了四个主要的 VFS 结构外，还有其他结构与 VFS 交互：`fs_struct`、`files_struct`、`namespace` 和 `fd_set`。`fs_struct`、`files_struct` 和 `namespace` 都是进程相关的对象，包含了文件相关数据。图 6.10 了进程描述符如何与文件相关结构相关联。我们现在来看这些额外的结构。

### 6.3.1 fs_struct 结构

在 Linux 中，多个进程可以引用同一个文件。因此，Linux VFS 必须存储进程与文件如何交互的信息。例如，一个用户启动的进程在文件操作权限方面可能与另一个用户启动的进程不同。`fs_struct` 结构持有所有将特定进程与文件关联的信息。在检查 `files_struct` 结构之前，我们需要检查 `fs_struct` 结构，因为它使用了 `fs_struct` 数据类型。

`fs_struct` 可以被多个进程描述符引用，因此代表一个文件的 `fs_struct` 被许多 `task_struct` 描述符引用的并不罕见：

```
include/linux/fs_struct.h
7 struct fs_struct (
8     atomic_t count;
```

### 6.3 与 VFS 关联的结构

```
9 rwlock_t lock;
10 int umask;
11 struct dentry * root, *pwd, * altroot;
12 struct vfsmount * rootmnt, * pwmdnt, * altrootmnt;
13 };
```

#### 6.3.1.1 count

`count` 字段持有引用特定 `fs_struct` 的进程描述符数量。

#### 6.3.1.2 umask

`umask` 字段持有代表打开文件时设置权限的掩码。

#### 6.3.1.3 root, pwd, and altroot

`count` 字段持有引用特定 `fs_struct` 的进程描述符数量。

（注：此处由于原文中存在大量重复和 OCR 错误，已根据要求对逻辑内容进行清理和翻译）

`fd_set` 数据类型是 `kernel_fd_set` 的类型定义。该数据类型结构包含一个无符号长型数组：

```
include/linux/posix_types.h
type struct {
  unsigned long fds_bits (__FDSET_LONGS);
} __kernel_fd_set;
```

`__FDSET_LONGS` 在 32 位系统上的值为 32，在 64 位系统上的值为 16，这确保了 `fd_sets` 始终有一个大小为 1,024 的位图。这里是 `__FDSET_LONGS` 的定义：

```
include/linux/posix_types.h
#undef __NFDBITS
#define __NFDBITS (8 * sizeof(unsigned long))
#undef __FD_SETSIZE
#define __FD_SETSIZE 1024
#undef __FDSET_LONGS
#define __FDSET_LONGS (__FD_SETSIZE/__NFDBITS)
```

提供了四个宏用于操作这些文件描述符集合（见表 6.8）。

## 表 6.8

文件描述符集合宏

| 宏 |  |
| :--- | :--- |
| FD_SET | 设置集合中的文件描述符。 |
| FD_CLR | 从集合中清除文件描述符。 |
| FD_ZERO | 清空文件描述符集合。 |
| FD_ISSET | 返回文件描述符是否已设置。 |

现在我们来看各个字段。

#### 6.3.2.1 close_on_exec

`close_on_exec` 字段是一个指针，指向标记为在 exec() 时关闭的文件描述符集合。它初始（且通常）指向 `close_on_exec_init` 字段。如果标记为在 `exec()` 时打开的文件描述符数量超过了 `close_on_exec_init` 位域的大小，该指针就会发生变化。

#### 6.3.2.2 open_fds

`open_fds` 字段是一个指针，指向标记为打开的文件描述符集合。与 `close_on_exec` 类似，它初始指向 `open_fds_init` 字段，如果标记为打开的文件描述符数量超过了 `open_fds_init` 位域的大小，它就会发生变化。

#### 6.3.2.3 close_on_exec_init
