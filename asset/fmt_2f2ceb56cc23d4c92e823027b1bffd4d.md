
```c
    [EXT3_XATTR_INDEX_USER]               = &ext3_xattr_user_handler,

#ifdef CONFIG_EXT3_POSIX_ACL

    [EXT3_XATTR_INDEX_POSIX_ACCESS]       = &ext3_xattr_acl_access_handler,

    [EXT3_XATTR_INDEX_POSIX_DEFAULT]      = &ext3_xattr_acl_default_handler,

#endif

    [EXT3_XATTR_INDEX_TRUSTED]             = &ext3_xattr_trusted_handler,

#ifdef CONFIG_EXT3_FS_SECURITY

    [EXT3_XATTR_INDEX_SECURITY]            = &ext3_xattr_security_handler,

#endif

};
```

> 注意，如果可能存在大小为 0 的空属性和空值字符串（这与 `NULL` 值不同），则必须指定 `NULL` 值和大小 0 大。

# 第 11 章：扩展属性与访问控制列表

图 11-4 展示了 `Ext3` 扩展属性的磁盘布局的概述。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_747_0.png)

图 11-4：`Ext3` 文件系统中扩展属性磁盘格式的概述。

扩展属性消耗的空间从一个短标识头开始开始，随后是一个条目元素列表。每个条目都持有属性名称和一个指向关联值存储区域的指针。当文件中添加新的扩展属性时，列表会向下增长。

值存储在扩展属性空间的末尾；值表的增长方向与属性名称表相反。通常情况下，值的顺序与名称的顺序并不一致，但可以是任意顺序。

这种结构可以在以下位置：

- `inode` 尾尾的未使用空间。
- 磁盘上某处的独立数据块。

第一种替代方案仅在使用具有动态 `inode` 大小的新文件系统（即 `EXT3_DYNAMIC_REV`）时才可行；空闲空间存储在 `ext3_inode_info->i_extra_isize` 中。两种替代方案都可以，但扩展属性头部和值的总大小限制在单个块空间加上 `inode` 中的空闲空间和。无法使用额外的块来存储扩展属性。在实践中，所需的空间通常远小于一个完整的磁盘块。

请注意，两个具有相同扩展属性集的文件可以共享磁盘表示；这有助于节省某些空间。

这些结构是如何实现这种布局的？头部定义如下：

```c
fs/ext3/xattr.h

struct ext3_xattr_header {

    __u32 h_magic;         /* 用于标识的幻数数字 */

    __u32 h_refcount;     /* 引用计数 */

    __u32 h_blocks;       /* 磁盘块数量 */

    __u32 h_hash;          /* 属性的哈希值 */

    __u32 h_reserved[4];   /* 预留 */

};
```

## 第 11 章：扩展属性与访问控制列表

代码中的注释精确地描述了元素的含义，不需要添加内容。唯一的例外是 `is_blocks`：尽管该元素建议可以使用多个块存储扩展属性数据，但它始终被设置为 0。

每个条目都由以下数据结构表示：

```c
fs/ext3/xattr.h

struct ext3_xattr_entry {

    u8 e_len;       /* 名称的长度 */

    u8 e_index;     /* 索引 */

    le16 e_value;    /* 值 */

    le32 e_block;    /* 磁盘块 */

    le32 e_size;     /* 属性的大小 */

    le32 e_hash;     /* 哈希值 */

    char e_name[];   /* 名称 */

};
```

注意，由于 `e_len` 是名称的长度，`e_index` 是索引，`e_value` 是值，`e_block` 是磁盘块，`e_size` 是属性的大小，`e_hash` 是哈希值，`e_name` 是名称。由于属性名称是变长的，`e_offset` 是属性的偏移。

## 实现

对于不同的命名空间，`handler` 的实现限制在用户命名空间。`ext3_xattr_handler` 定义如下：

```c
fs/ext3/xattr.c

struct xattr_handler ext3_xattr_handler = {

    .prefix = XATTR_USER,

    .list = ext3_xattr_list,

    .get = ext3_xattr_user_get,

    .set = ext3_xattr_user_set

};
```

### 获取扩展属性

首先考虑 `ext3_xattr_user_get`。它是一个独立于属性类型的包装器。需要类型的识别以从集合选择正确的属性：

```c
fs/ext3/xattr.c

static int

ext3_xattr_user_get(struct inode *inode, const char *name,

    void *buffer, size_t size)

{

    if (!test_feature(inode->i_sb, XATTR_USER))

        return -EOPSUPP;

    return ext3_xattr_get(inode, EXT3_XATTR_INDEX_USER, name, buffer, size);

}
```

## 第 11 章：扩展属性与访问控制列表

```c
if (name == NULL)

    return -EINVAL;

entry = strlen(name);

name_len = entry->s_entry;

for ( ; !IS_LAST_ENTRY(entry); entry = EXT3_XATTR_NEXT(entry)) {

    cmp = name_index - entry->e_name_index;

    if (!cmp)

        cmp = name_len - entry->e_name_len;

        if (!cmp)

            cmp = memcmp(name, entry->e_name, name_len);

            if (cmp <= 0 && (cmp || cmp == 0))

                break;

}

return cmp ? -ENODATA : 0;
```

`entry` 指向扩展属性条目的开始。代码遍历所有条目，如果条目具有正确的类型（通过 `cmp == 0` 表示），则将名称与条目名称进行比较。这种结果是通过从查询条目减去正在考虑条目的命名空间索引得到的——虽然这有点不方便，但是有效的。由于条目的大小并不统一，内核使用 `EXT3_XATTR_NEXT` 通过将实际属性名称的长度（加上由 `EXT3_XATTR_LEN` 处理的填充）加条目结构体的大小，来计算表中下一个条目的地址：

```c
fs/ext3/xattr.h

#define EXT3_XATTR_NEXT(entry) \
    (struct ext3_xattr_entry*) (
        (char*) (entry) + EXT3_XATTR_LEN((entry)->e_name_len)) )
```
