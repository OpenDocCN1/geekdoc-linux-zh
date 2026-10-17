
当文件系统向内核注册时，代码是编译为模块还是永久编译进内核并没有区别。两种方法的处理方法相同，无论注册时间何时（永久编译的文件系统在启动时注册，模块在相关模块加载到内核时注册）。

使用 `fs/super.c` 中的 `register_filesystem` 向内核注册文件系统。该函数的结构非常简单。文件系统存储在一个单链表中，每个文件系统的名称以字符串存储在对象中。当新文件系统向内核注册时，会逐个扫描列表直到到达列表末尾或找到所需的文件系统。在后者，会返回适当的错误消息（无法注册文件系统），描述新文件系统的对象放在列表末尾，从而完成内核注册。

描述文件系统的结构定义如下：

```c
<fs.h>
struct file_type {
    const char *name;
    int fs_flags;
    struct super_block *(get_sb) (struct file_type *, int, const char *, struct vfs_block *);
    void (*kill_sb) (struct super_block *);
    struct module *owner;
    struct file_type *next;
    struct list_head fs_supers;
};
```

¹³在早期的 UNIX 版本中，此命令在逻辑上称为 unmount，但该名称在漫长的操作系统历史中丢失了。

`name` 以字符串形式持有文件系统名称（因此包含如 reiserfs、ext3 等值）。`fs_flags` 是使用的标志位，例如用于指示只读挂载、禁止 setuid 执行或进行其他调整。`owner` 是一个指向结构体的指针，如果文件系统作为模块加载（永久编译进内核），则该指针包含一个值。可用的文件系统通过（此处原文逻辑略显混乱，按语意翻译）...`fs_flags` 是标志位...`owner` 是指针...可用的文件系统...

（注：由于原文后部分段落存在较多重复和逻辑碎片，翻译时已根据技术术语逻辑进行了对齐处理）

`name` 以字符串形式持有文件系统名称（因此包含如 reiserfs、ext3 等值）。`fs_flags` 是使用的标志位，例如用于指示只读挂载、禁止 setuid 执行或进行其他调整。`owner` 是一个指向结构体的指针，如果文件系统作为模块加载（永久编译进内核），则该指针包含一个值。可用的文件系统...（此处原文文本存在大量重复性乱码，翻译已保留核心语意）。

## 挂载与卸载

挂载和卸载目录比简单的注册文件系统要复杂得多，因为挂载操作需要挂载树结构。在详细讨论挂载步骤之前，我们需要明确挂载树中的数据系统。使用挂载结构来描述挂载点。

### VFS 挂载结构

Unix 采用分层结构来集成新的文件系统，挂载点中的结构如图 8-4 所示。

```
wolfgang@meiter ext2 (rw)
/dev/da2 reiserfs (rw)
/dev/da3 reiserfs (rw)
/dev/hdc /mnt/cdrom iso960 (ro,noexec,nosuid,nodev)
```

挂载时，挂载点的内容被替换为挂载系统的根目录。当卸载时，挂载点不再需要。

## 第 8 章：虚拟文件系统

```
atomic_t mnt_count;
int mnt_expiry_mark; /* 如果标记为过期则为真 */
```

`mnt_mountpoint` 是文件系统挂载时所在父目录中挂载点的 dentry（目录项）；文件系统自身的相对根目录存储在 `mnt_root` 中。两个 dentry 实例表示同一个目录（即挂载点）。这意味着在文件系统卸载后，没有必要从内存中删除之前的挂载点信息并使其重新可用。当我讨论 `mount` 系统调用时，对两个 dentry 的需求将变得清晰易懂。

`mnt_sb` 创建了一个指向关联超级块（superblock）的链接（每个挂载的文件系统恰好有一个实例）；`mnt_parent` 指向父文件系统的 `vfsmount`。

父子关系由结构体中两个元素实现的链表表示。`mnt_lists` 头是子文件系统列表的起始点。各个列表元素通过 `mnt_child` 字段相互连接。

该实例的每个 `vfsmount` 还可以通过另外两种方式识别：由 `namespace->list` 头的链表包含了所有挂载。各个对象通过 `mnt_list` 连接。我忽略了拓扑结构，因为所有挂载都是顺序执行的。

在 `mnt_flags` 中可以设置与特定类型无关的标志。以下常量列出了所有可能的标志：

```
<mnt.h>
#define MNT_NOSUID 0x01
#define MNT_NODEV 0x02
#define MNT_NOEXEC 0x04
#define MNT_NOATIME 0x08
#define MNT_NODIRATIME 0x10
#define MNT_RELATIVE 0x20

#define MNT_SHINKABLE 0x100
#define MNT_SHARED 0x1000 /* 如果 vfsmount 是共享挂载 */
#define MNT_UNBINDABLE 0x2000 /* 如果 vfsmount 是不可绑定的挂载 */
#define MNT_PNODE_MASK 0x3000 /* 传播标志掩码 */
```

第一个块包含经典属性，允许在挂载时延迟设备文件的存在，或者如何管理访问时间的处理。如果文件系统是虚拟的、没有物理备用设备，则设置 `MNT_NODEV`。`MNT_SHINKABLE` 是 NFS 和 UFS 的特性，用于标记不可绑定的挂载。带有此锁的挂载允许被自动移除。

最后一个块包含指示不可绑定挂载的标志。关于这些类型的用途的细节，请参阅第 8.4.1 节。

还使用了定义在 `fs/namespace.c` 中的哈希表 `count_hashable`。溢出列表通过 `mnt_hash` 实现为链表。`vfsmount` 实例的地址和关联 dentry 对象的地址被用于计算哈希和。`mnt_namespace` 是挂载所属的命名空间。

使用 `mnt_count` 实现了一个计数器。每当一个 `vfsmount` 实例不再需要时，必须通过 `mntput` 递减计数器。`mntget` 是在实例被使用时需要调用的对应操作。

剩余字段用于实现几种新的挂载类型，这些类型大部分是在内核 2.6 开发期间引入的。`mnt_slave`、`mnt_slave_list` 和 `mnt_master` 用于实现从属挂载（slave mounts）。主节点将所有从属挂载保持在一个链表中，`mnt_slave_list` 用作列表头，而 `mnt_slave_list` 作为列表元素。所有从属挂载通过 `mnt_master` 指回它们的主节点。

共享挂载（Shared mounts）更容易实现。内核需要做的只是将所有共享对等挂载保持在一个环形列表中。`mnt_share` 作为这些列表元素。

挂载过期通过 `mnt_expiry_mount` 处理。该元素用于指示挂载是否未被使用。`mnt_expire` 允许将所有受自动过期影响的挂载放在链表中。第 8.4.1 节详细说明了过期挂载的实现。

最后，`mnt_ns` 指向挂载所属的命名空间。

## 超级块管理

挂载结构不是在新文件系统挂载时在内存中生成的唯一对象。挂载操作从读取一个名为超级块（superblock）的结构开始。我多次提到了这个结构，但没有费善地定义它。现在我来这样做。

存储在 `file_system_type` 对象中的函数指针 `read_super` 返回一个 `superblock` 类型的对象，它代表内存中的一个超级块。它是通过底层实现的帮助生成的。

该结构体定义非常长。我在下面复制了一个简化版本（它本身一点也不短）。
