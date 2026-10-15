
`inode->i_gid = 0;`

`inode->i_blocks = 0;`

`inode->i_atime = inode->i_ctime = CURRENT_TIME;`

```c
switch (mode & S_IFMT) {
    default:
        init_special_inode(inode, dev);
        break;
    case S_IFREG:
        inode->i_fop = &debugfs_file_operations;
        break;
    case S_IFDIR:
        inode->i_op = &simple_dir_inode_operations;
        inode->i_fop = &simple_dir_inode_operations;
```

```c
/* 目录 inode 的初始 i_nlink 等于 2
 * (对于 "*, *entry) */
inc_nlink(inode);
break;
}
}
return inode;
```

除了分配 `struct inode` 的新实例外，内核还需要根据访问模式中的信息决定将哪些文件和 inode 操作与文件关联。对于设备特殊文件，使用了标准程序 `init_special_file`（该程序与库无关联）。然而，更有趣的情况是普通文件和目录。目录需要上述讨论的标准文件和 inode 操作；这确保了新目录被正确处理而无需额外。

普通文件无法提供样板文件操作。至少需要管理读、写和打开方法。读用于从内核内存准备数据并将其拷贝到用户空间，而写可用于从用户某种方式读取输入。这就是实现自定义文件的所有要求！

文件系统还需要超级块（superblock）。坦率地说，对于懒惰的程序员来说，libfs 提供了 `simple_fill_super` 方法，用于填充给定的超级块：

```c
<fs.h>
int simple_fill_super(struct super *s, int magic, struct tree_desc *files);
```

`s` 是所讨论的超级块，`magic` 指定了一个用于识别文件系统的唯一数字。`files` 参数提供了一种方便的方法，用虚拟文件系统应该包含的内容填充：文件！遗憾的是，该方法只能指定单个目录中的文件，但对于虚拟文件系统来说这不是真正的限制。可以动态添加更多内容。

使用带有 `struct tree_desc` 元素的数组来描述初始文件集。该结构定义如下：

```c
<fs.h>
struct tree_desc {
    char *name;
    const struct file_operations *ops;
    int mode;
};
```

`name` 定义文件名，`ops` 指向关联的文件操作，`mode` 指定访问位。

> 列表中的最后一个条目必须是形式 "{ *, NULL, 0 }。"

## 10.2.3 调试文件系统

使用 libsfs 的特定文件系统是调试文件系统 debugfs。它为内核开发者提供了向用户提供信息的可能性。这些信息不应该编译到生产内核中。相反，它仅作为开发新功能的辅助。只有在编译内核时带有 `DEBUG_FS` 配置选项，才会激活调试支持。在 debugfs 中注册文件的代码需要被 `CONFIG_DEBUG_FS` 的 C 预处理器条件包裹。

## 示例

回顾本章之前讨论的 kprobes 作为顺序文件机制的示例。结果文件通过几行代码通过 debugfs 导出——简单到极！

```c
kernel/kprobes.c
#ifdef CONFIG_DEBUG_FS
static int debugfs_init(void)
{
    struct dentry *dir, *file;
    unsigned int value = 1;
    dir = debugfs_create_dir("kprobes");
    file = debugfs_create_file("list", 0444, dir, &debugfs_operations);
    return 0;
}
#endif
```

## 编程接口

由于 debugfs 是整洁、简单且文档良好的，无需对编程接口添加备注。有三个函数用于创建文件系统对象：

```c
<debugfs.h>
struct dentry *debugfs_create_file(const char *name, mode_t mode,
              struct dentry *parent, void *data,
              const struct file_operations *fops);
struct dentry *debugfs_create_dir(const char *name);
```

文件系统对象可以是普通文件、目录或符号链接。两个操作允许重命名和删除文件：

```c
<debugfs.h>
void debugfs_remove(struct dentry *dentry);
struct dentry *debugfs_rename(struct dentry *old_dir, struct dentry *old_dentry,
              struct dentry *new_dir, const char *new_name);
```

当调试内核时，需要导出并操作像 int 或 long 这样的单一值。Debugfs 还提供了几个创建新文件以从用户空间读取值并向内核粘贴值的函数。它们共享相同的原型：

```c
<debugfs.h>
struct dentry *debugfs_create_XX(const char *name, mode_t mode,
              struct dentry *parent, void *value);
```

`name` 指定文件名和地址，而 `parent` 指向父目录的实例。`value` 非常重要：指向导出的可以通过写入文件修改的值。如果 XX 被替换为标准内核数据类型 u8、u16、u32 或 u64，则允许读取不允许更改值。如果使用 x8、x16 或 x32，也可以从用户空间更改值。

布尔值可以通过 `debugfs_create_bool` 创建：

```c
<debugfs.h>
struct dentry *debugfs_create_bool(const char *name, mode_t mode,
              struct dentry *parent, u32 value);
```

最后，还可以与用户空间交换短二进制数据（通常为二进制 blob）。为此目的提供了以下函数：

```c
<debugfs.h>
struct dentry *debugfs_create_blob(const char *name, mode_t mode,
              struct dentry *parent,
              struct debugfs_blob_wrapper *blob);
```

二进制数据由特殊数据结构表示，该结构包含指向数据内存位置的指针和数据长度：

```c
<debugfs.h>
struct debugfs_blob_wrapper {
    void *data;
    unsigned long size;
};
```

# 第 10 章：无持久化存储的文件系统

## 10.2.4 伪文件系统

回想第 8.4.1 节，内核支持伪文件系统，它们收集相关的 inode，但无法被挂载，因此对用户是不可见的。Libfs 还提供了一个辅助函数来实现리这种特殊类型的文件系统。

内核使用伪文件系统来跟踪所有代表块设备的 节点：

```c
fs/block_dev.c
static int bd_get_sb(struct file_system_type *fs_type,
    int flags, char *dev_name, void *data, struct vfsmount *mnt)
    {
        return get_sb_pseudo(fs_type, "bdev", &dev_ops, 0x062464576, mnt);
}
static struct file_system_type bd_type = {
    .name = "bdev",
    .get_sb = bd_get_sb,
    .kill_sb = kill_anon,
};
```
