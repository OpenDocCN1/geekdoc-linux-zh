
# 第 11 章：扩展属性与访问控制列表

用户态程序 `getfacl`、`setfacl` 等用于获取、设置和更改 ACL 的内容。它们使用系统调用来操作扩展属性，不需要与内核进行任何非标准交互。许多其他工具（例如 `ls`）也内置了处理访问控制列表的支持。

### 11.2.1 通用实现

实现 ACL 的通用代码包含两个文件：`fs/posix_acl.c` 和 `fs/xattr_acl.c` 用于扩展属性与 ACL 的通用表示之间转换的函数，反之亦然。通用数据结构定义在 `include/linux/posix_acl.h` 和 `include/linux/posix_acl_xattr.h` 中。

#### 数据结构

内存表示持有与 ACL 相关的所有数据的中心数据结构是：

```
<posix_acl.h>

struct posix_acl_entry {

    short               e_tag;

    unsigned short      e_perm;

    unsigned int        e_id;

};

struct posix_acl {

    atomic_t            a_refcount;
```

³注意，关于 ACL 以及 Linux 支持的各种文件系统中实现状态的另一个良好概述，可以在 Andreas Grünbacher 的 Usenix 论文 [Grü03] 中找到他是 Ext2 和 Ext3 文件系统 ACL 支持的主要负责人之一。

```
unsigned int a_count;

struct posix_acl_entry a_entries[0];
```

每个条目包含一个标记（tag）、一个权限以及 ACL 所引用的（用户或组 ID）。属于给定节点的所有 ACL 均由 `struct posix_acl` 收集。ACL 条目的数量由 `a_count` 给出；由于包含所有条目的数组位于结构体的底部，除了扩展属性的最大限制外，对条目数量没有限制。`a_refcount` 是一个标准的引用计数器。

ACL、类型和权限的符号常量由以下处理器定义给出：

```
<posix_acl.h>

/* acl_user_entry_t 中的 type 字段 */

#define ACL_TYPE_ACCESS  (0x8000)

#define ACL_TYPE_DEFAULT (0x4000)

/* struct posix_acl_entry 中的 e_tag */

#define ACL_USER_OBJ     (0x01)

#define ACL_USER         (0x02)

#define ACL_GROUP_OBJ    (0x04)

#define ACL_GROUP        (0x08)

#define ACL_MASK         (0x10)

#define ACL_OTHER        (0x20)

/* e_perm 字段中的权限 */

#define ACL_READ         (0x04)

#define ACL_WRITE        (0x02)

#define ACL_EXECUTE      (0x01)
```

内核定义了另一组与上述类似的数据结构，用于 ACL 的 xattr 表示。然而，这次这些结构被预期用于与用户空间的外部交互：

```
<posix_acl_xattr.h>

typedef struct {

    __u16 e_tag;

    __u16 e_perm;

    __u32 e_id;

} posix_acl_xattr_entry;

typedef struct {

    __u32 a_version;

    posix_acl_xattr_entry a_entries[0];

} posix_acl_xattr_header;
```

用于内部和外部表示的结构非常相似，不同之处在于使用了定义了字节序（附录 A.8）和显式位长度的类型用于后者；此外，磁盘表示不需要引用计数。

提供了两个在引用之间进行转换的函数：`posix_acl_kattr` 和 `posix_from_xattr`。由于翻译是纯机械的，没有必要详细讨论。然而，重要的一点是，它们工作独立于底层文件系统。

# 权限检查

对于涉及访问控制的权限检查，内核通常需要底层文件系统的支持：要么它们由自己实现所有权限检查（通过 `struct inode_operations` 的权限函数），要么它们为 `generic_permission` 提供一个回调方法。内核中的大多数系统更倾向于后者方法。

回调函数在 `generic_permission` 中注册如下（注意 `check_acl` 表示回调函数）：

```
fs/name.c

generic_permission(struct inode *inode, int mask,

    int (*check_acl)(struct inode *inode, int mask))

{

    if (IS_POSIXACL(inode) && (mask & S_IRMWG) && check_acl) {

        int error = check_acl(inode, mask);

        if (error == -EACCES)

            goto check_capabilities;

        else if (error != -EAGAIN)

            return error;

    }

}
```

`IS_POSIXACL` 检查（挂载时）标志 `MS_POSIXACL` 是否设置了需要使用的 ACL。

即使文件系统提供专门的函数来执行 ACL 权限检查，各个例程通常也归结为某些技术工作，例如获取 ACL 数据。真正的权限检查再次委托给内核提供的标准函数 `posix_acl_permission`。

因此，`posix_acl_permission` 需要详细讨论。给定一个指向 `inode` 的指针、一个指向访问控制列表（内存表示）的指针，以及检查（`MAY_READ`, `MAY_WRITE`, `MAY_EXEC` 模式）的权利，该函数在允许访问时返回 0，否则返回相应的错误代码。实现如下：

```
fs/posix_acl.c

int posix_acl_permission(struct inode *inode, struct posix_acl *acl, int want)

{

    struct posix_acl_entry *pa, *pe, *mask_obj;

    int found = 0;

    FOREACH_ACL_ENTRY(pa, acl, etag) {

        switch (pa->tag) {

            case ACL_USER_OBJ:

                /* (可能已经检查过) */

                if (inode->i_uid == current_fsuid)

                    goto check_perm;

                break;

            case ACL_USER:

                if (pa->e_id == current_fsuid)

                    goto mask;

                break;

            case ACL_GROUP_OBJ:

                if (in_group_p(pa->e_id)) {

                    found = 1;

                    if ((pa->e_perm & want) == want)

                        goto mask;

                    break;

            case ACL_GROUP:

                if (in_group_p(pa->e_id)) {

                    found = 1;

                    if ((pa->e_perm & want) == want)

                        goto mask;

                    break;

            case ACL_MASK:

                break;

            case ACL_OTHER:

                if (found)

                    return -EACCES;

                else
```
