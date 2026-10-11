
## 6.2.1 superblock 结构

当文件系统被挂载时，关于它的所有信息都存储在 `superblock` 中。我们展示了结构定义以及对一些重要字段的解释：

对于基于磁盘的文件系统，`superblock` 结构由存储在特殊扇区的信息填充。由于 VFS 允许编辑 `superblock` 结构，`superblock` 结构中的信息可能与磁盘数据不同。此字段标识 `superblock` 结构已被编辑，需要与磁盘同步。

```c
include <linux/fs.h>
struct super_head s_list;
struct dentry *s_dev;
unsigned long s_blocksize;
unsigned char s_blocksize;
unsigned char s_dirt;
struct file_type *s_type;
struct super_operations *s_op;
struct alloc_operations *s_op;
struct export_operations *s_export;
unsigned long s_flags;
unsigned long s_magic;
struct dentry *s_root;
struct semaphore *s_mount;
struct semaphore s_lock;
```

```c
int s_count;
int s_syncing;
int s_need_sync_fs;
atomic_t s_active;
void *s_security;
struct list_head s_dirty;
struct list_head s_io;
struct list_head s_anon;
struct list_head s_files;
struct block_device *s_bdev;
struct list_head s_instances;
struct quota_info s_dquot;
char s_id[32];
struct kobject kobj;
void *s_fs_info;
struct semaphore s_vfs_rename_sem;
```

`s_list` 字段的类型为 `list_head`，它是指向嵌入此 `superblock` 的双向链表中下一个和上一个元素的指针。与 Linux 内核中许多其他结构一样，`super_block` 结构维护在一个双向链表中。`list_head` 类型包含指向两个其他 `list_head` 的指针：下一个 `superblock` 对象的 `list_head` 和上一个 `superblock` 对象的 `list_head`。（全局变量 `super_blocks` (`fs/super.c`) 指向链中的第一个元素）。

第 2 章“探索工具包”详细描述了 `list_head` 类型。

### 第 673 行

此类型为 `unsigned long` 的字段定义了文件系统允许的最大文件大小。

### 第 674 行

超级块（`superblock`）结构包含了通用文件系统信息。然而，它需要与特定的文件系统信息关联（例如，`MSDOS`、`ext2`、`MINIX` 和 `NFS`）。`file_system_type` 结构持有配置到内核中的每种类型文件系统的特定文件系统信息。该字段指向相应的特定文件系统结构体，它是 VFS（虚拟文件系统）管理从通用请求到特定文件系统操作之间交互的方式。

图 6.4 显示了超级块和 `file_system_type` 结构之间的关系。我们展示了 `superblock->s_type` 字段如何指向 `file_systems` 列表中相应的 `file_system_type` 结构。（在本章稍后的“全局和本地列表引用”部分中，我们将展示 `file_systems` 列表是什么。）

![](img/6525157588f931c50a65c5a42af9a432_335_0.png)

图 6.4 `superblock` 与 `file_system_type` 之间的关系

## 6.2 Linux 虚拟文件系统

### 第 675 行

该字段是一个 `super_operations` 结构体类型的指针。此数据类型持有超级块操作表。`super_operations` 结构本身持有函数指针，这些指针使用特定文件系统的超级块操作进行初始化。下一节将详细详细解释 `super_operations`。

### 第 681 行

该字段是一个指向 `dentry` 结构体的指针。`dentry` 结构持有文件的路径。这个特定的 `dentry` 对象是与其超级块所属的挂载目录关联的。

### 第 690 行

`s_dirty` 字段（不要与 `s_dirt` 混淆）是一个 `list_head` 结构，指向属于该文件系统的脏节点（dirty inodes）列表中的第一个和最后一个元素。

### 第 696 行

`s_files` 字段是一个 `list_head` 结构，指向一个正在使用并分配给超级块的 `file` 结构列表的第一个元素。在“file 结构”部分中，你会发现这是文件结构可以所属的三个列表之一。

### 第 702 行

此 `void *` 数据类型指向特定特定文件系统的额外超级块信息（例如 `ext3_sb_info`）。它充当该特定文件系统磁盘上任何超级块数据的“大杂烩”，这些数据尚未被抽象到虚拟超级块概念中。

### 6.2.1.2 超级块操作

超级块的 `s_op` 字段指向文件系统超级块可以执行的操作表。此列表对每个文件系统都是特定的，因为它直接在文件系统的实现上操作。操作表存储在类型为 `super_operations` 的结构中：

```
include/linux/fs.h
struct super_operations {
    struct inode *(*alloc_inode) (struct super_block *sb);
    void (*destroy_inode) (struct inode);

void (*read_inode) (struct inode);

void (*dirty_inode) (struct inode);
void (*write_inode) (struct inode *, int);
void (*put_inode) (struct inode);
void (*drop_inode) (struct inode);
void (*delete_inode) (struct inode);
void (*put_super) (struct super_block *);
void (*write_super) (struct super_block *);
void (*sync_fs) (struct super_block *sb, int wait);
void (*write_super_lockfs) (struct super_block *);
void (*alloc_blocks) (struct super_block *sb, struct kstatfs *);
int (*statfs) (struct super_block *, struct kstatfs *, int *, char *);
int (*remount_fs) (struct super_block *, int *, char *);
void (*clear_inode) (struct inode);
void (*umount_begin) (struct super_block *);

int (*show_options) (struct seq_file *, struct vfs_mount *);
};
```

当文件系统的超级块初始化时，`s_op` 字段被设置为指向适当的操作表。在本章稍后的“从通用到‘特定’”部分中，我们将展示该操作表在 `ext2` 文件系统中是如何实现的。下表 6.2 显示了超级块操作列表。这些函数中的某些是可选的，仅由部分支持的文件系统子集填充。不支持特定函数 `set` 的文件系统会将操作结构体中的该字段设置为 `NULL`。

## 6.2 Linux 虚拟文件系统

表 6.2

超级块操作

| 超级块操作名称 | 说明 |
|---|---|
| `alloc_inode` | 2.6 新引入。它在超级块下分配并初始化一个 vfs inode。初始化的具体细节取决于特定的文件系统。分配通过在 inode 缓存上调用 `kmem_cache_create()` 或 `kmem_cache_alloc()` 完成（见第 4 章）。 |
| `destroy_inode` | 2.6 新引入。它释放与超级块相关的指定 inode。释放通过调用 `kmem_cache_free()` 完成。 |
| `read_inode` | 读取由 `inode->i_ino` 字段指定的 inode。inode 的字段从磁盘数据更新。特别重要的是 `inode->i_op`。 |
