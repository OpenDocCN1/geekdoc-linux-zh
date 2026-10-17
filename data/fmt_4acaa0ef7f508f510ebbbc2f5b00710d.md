
inode 结构定义在 `/src/ufs/ufs/inode.h` 中。对于 `UFS1`，其显示形式如列表 8.9 和图 8.11 所示。

## 列表 8.9.UFS1 中的 inode 结构

```
struct dinode {
    /* 0x00 */  u_int16_t di_mode;      /* 0: IFMT, 权限；见下文。 */
    /* 0x02 */  int16_t    di_nlink;      /* 2: 文件链接计数 */
    /* 0x04 */  union {
        int32_t     di_oldids[2];      /* 4: 旧的未使用 ID 和组 ID */
        int32_t     inumer;         /* 6: LFS: 索引节点号 * */
    } di_u;
    /* 0x08 */  u_int64_t di_size;        /* 8: 文件字节数 */
    /* 0x10 */  int32_t    di_atime;       /* 16: 最后访问时间 * */
    /* 0x14 */  int32_t    di_atimesec;    /* 20: 访问时间 * */
    /* 0x18 */  int32_t    di_mtime;       /* 24: 最后修改时间 * */
    /* 0x1C */  int32_t    di_mtimesec;    /* 28: 最后修改时间 * */
    /* 0x20 */  int32_t    di_ctime;        /* 32: 最后索引节点更改时间 */
    /* 0x24 */  int32_t    di_ctimeec;     /* 36: 最后索引节点更改时间 * */
    /* 0x28 */  ufs_d_t di_db[DBADDDR];     /* 40: 直接磁盘块 * */
    /* 0x58 */  ufs_d_t di_ib[NIADDDR];     /* 88: 间接磁盘块 * */
    /* 0x64 */  u_int32_t  di_flags;        /* 100: 状态标志 (chflags) * */
    /* 0x68 */  int32_t    di_gen;          /* 108: 生成数 * */
    /* 0x70 */  u_int32_t  di_uid;          /* 112: 文件所有者 * */
    /* 0x74 */  u_int32_t  di_gid;          /* 116: 文件组 * */
    /* 0x78 */  int32_t    di_spare[2];     /* 120: 预留；当前未使用 * */
};
```

| 类型/模式 | 链接计数 |
|---|---|
| 用户 ID | 组 ID |
| 文件大小（字节） | |
| 最后访问时间 | |
| 最后修改时间 | |
| 创建时间 | |
| 12 个数据块地址 | |
| 第一级索引块地址 | |
| 扩展（七个 4 字节字） | |
| 32 位 | |

**图 8.11. inode 结构的设计**

在 `UFS2` 中，inode 结构被经过了大幅修改（见列表 8.10）。出现了许多新字段，地址字段的宽度也倍增了。这对于实际数据恢复意味着什么？所有字段的偏移量都发生了变化。然而这并不重要，因为处理 inode 的通用原则保持不变。

# 第 8 章：Linux/BSD 下的数据恢复 227 页

## 列表 8.10.UFS2 中的 inode 结构

```
struct ufs2_inode {
    /* 0x00 */  int16_t    di_mode;         /* 0x0000: 0: IFMT, 权限；见下文。 */
    /* 0x02 */  int16_t    di_nlink;       /* 0x0002: 2: 文件链接计数 */
    /* 0x04 */  int32_t     di_uid;         /* 0x0004: 4: 文件所有者 */
    /* 0x08 */  int32_t     di_gid;         /* 0x0008: 8: 文件组 */
    /* 0x0C */  int32_t     di_blksize;    /* 0x000c: 12: inode 块大小 */
    /* 0x10 */  int64_t     di_size;        /* 0x0010: 16: 文件字节数 */
    /* 0x18 */  int64_t     di_blocks;      /* 0x0018: 24: 实际持有 */
    /* 0x20 */  ufs_time_t  di_atime;      /* 0x0020: 32: 最后访问时间 */
    /* 0x28 */  ufs_time_t  di_mtime;      /* 0x0028: 40: 最后修改时间 */
    /* 0x30 */  ufs_time_t  di_ctime;       /* 0x0030: 48: 最后索引节点更改时间 */
    /* 0x38 */  ufs_time_t  di_birthtime;  /* 0x0038: 56: 创建时间 */
    /* 0x40 */  int32_t     di_mtimsec;   /* 0x0040: 64: 最后修改时间 */
    /* 0x44 */  int32_t     di_atimec;  /* 0x0044: 68: 最后访问时间 */
    /* 0x48 */  int32_t     di_ctimec;  /* 0x0048: 72: 最后索引节点更改时间 */
    /* 0x4C */  int32_t     di_birthnsec;  /* 0x004c: 76: 创建时间 */
    /* 0x50 */  int32_t     di_gen;         /* 0x0050: 80: 生成数 */
    /* 0x54 */  int32_t     di_kernflags;   /* 0x0054: 84: 内核标志 */
    /* 0x58 */  int32_t     di_extflags;   /* 0x0058: 88: 状态标志 (chflags) */
    /* 0x5C */  int32_t     di_extsize;    /* 0x005c: 92: 扩展属性块 */
    /* 0x60 */  ufs2_daddr_t  di_extb[NKADDR];  /* 0x0060: 96: 扩展属性块 */
    /* 0x70 */  ufs2_daddr_t  di_id[NDADDR];   /* 0x0070: 112: 直接磁盘块 */
    /* 0xD0 */  ufs2_daddr_t  di_ibi[NIADDR];   /* 0x00d0: 208: 间接磁盘块 */
    /* 0xE8 */  int64_t      di_spare[3];     /* 0x00e8: 232: 预留；当前未使用 */
};
```

| 文件 | 5 | 目录 | 3 | 文件 | 组 |

**图 8.12. 文件名与目录的存储**

文件名存储在目录中（图 8.12）。inode 中没有文件名。`UFS` 将目录视为特定类型的文件，可以存储在圆柱组的任何位置。`UFS` 支持多种类型的目录哈希；然而，这对于存储结构没有影响。名称存储在称为 `DIRBLKSZ` 的块中，按 4 字节边界对齐。

直接结构定义在 `/src/ufs/ufs/dir.h` 文件（见列表 8.11）。它包含以下信息：描述给定文件的 inode 号、其类型、名称以及用于在块中查找下一个直接结构的长度。

### 列表 8.11. 存储文件名和目录的直接结构

```
struct direct (
    /* 0x00 */ u int32_t dino;           /* 条目的索引节点号 */
    /* 0x04 */ u int16_t dclen;         /* 此记录的长度 */
    /* 0x06 */ u int8_t dtype;          /* 文件类型；见下文 */
    /* 0x07 */ u int8_t damlen;         /* 字符串长度 */
    /* 0x08 */ char d_name[MAXLEN];     /* 带有 MAXLEN 的名称 */
);
```
