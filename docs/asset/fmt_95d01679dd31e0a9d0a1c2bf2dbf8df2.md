
这返回与 VFS inode 关联的 inode 特有数据。图 1-1 描述了这种情况。

## 第 10 章：无持久化存储的文件系统

| `proc_inode` | VFS |
| :--- | :--- |
| 这里的实际数据，而不是指向结构实例的指针。 |

## 持久化存储

换句话说，直接每个与 `proc` 文件系统链接的 `inode` 实例，内存中都有额外的数据，可以使用容器机制从 `proc_inode` 实例中提取。由于内核频繁使用以下辅助过程：

```c
// proc_fs.h

static inline struct proc_inode *PROC_I(const struct inode *inode)
{
    return container_of(inode, struct proc_inode, vfs_inode);
}
```

这返回与 VFS inode 关联的 inode 特有数据。图 1-1 描述了这种情况。

这是 VFS 层用于节点管理的相同数据。换句话说，直接每个与 `proc` 文件系统链接的 `inode` 实例，内存中都有额外的数据，可以使用容器机制从 `proc_inode` 实例中提取。由于内核频繁使用以下辅助过程：

```c
// proc_fs.h

static inline struct proc_inode *PROC_I(const struct inode *inode)
{
    return container_of(inode, struct proc_inode, vfs_inode);
}
```

这返回与 VFS inode 关联的 inode 特有数据。图 1-1 描述了这种情况。
