
**表 13-10** *来自 `segmap` 段驱动程序的统计信息（续）*

| 字段名称 | 描述 |
|---|---|
| `rel_abort` | 该槽位已释放，并因一次失败且被中止的写操作而被要求从 `segmap` 段中移除。 |
| `rel_dontneed` | 该槽位已释放，并通知 VM 系统释放该页，因为不会再需要它。这些页被放在缓存列表头部，以便优先复用。 |
| `released` | 该槽位已释放，且此次释放并非由 `rel_abort`、`rel_async` 或 `rel_write` 引起。 |
| `pagecreate` | 在 `segmap_pagecreate` 函数中创建的页。 |

我们的示例 segmap 统计信息显示，在总共 16,109,564 次 getmap 调用中，有 15,257,790 次对槽位进行了回收，这相当于 95% 的槽位在文件和偏移量均正确的情况下被复用，也就是 segmap 中文件系统页的缓存命中率为 95%。请注意，实际的文件页到缓存命中率可能更高，因为即使未命中 segmap，这些页仍可能位于页缓存中，只需要重新加载该页的地址转换。较低的 segmap 命中率和较高的页到缓存命中率是大内存机器的典型特征；在这样的机器上，物理内存可能达到数 GB，而 segmap 只能使用其中的 256 MB。

写入是类似的过程。同样，会调用 `segmap_getmap` 为文件和偏移量获取或创建一个映射，完成 I/O，然后释放 segmap 槽位。如果文件正在扩展，或者要在文件空洞中创建新页，则还会涉及一个额外步骤。该额外步骤调用 `segmap_pagecreate` 函数创建并锁定新页，然后调用 `segmap_pageunlock()` 解锁在 `page_create` 期间锁定的页。

segmap 缓存会随着页面换入换出以及页扫描程序回收页面而增大或缩小，但其最大大小受架构特定上限的约束。

## 13.5 路径名管理

除少数 vnode 方法外，其余 vnode 方法都操作 vnode 指针，而不是路径名或文件描述符。在调用文件系统 vnode 方法之前，vnode 框架会先将路径名和文件描述符转换成 vnode 引用。文件描述符可以直接转换为其所引用文件的 vnode，而路径名则必须先通过查找路径名组件并引用底层文件，才能转换为 vnode。与文件系统无关的 `lookuppn()` 函数负责将路径名转换为 vnode；另一个包装函数 `lookupname()` 则负责处理来自用户态系统调用的路径名转换。

### 13.5.1 lookupname() 和 lookuppn() 方法

给定一个路径名，`lookuppn()` 方法尝试返回一个指向表示该路径名的 vnode 的指针。如果该文件已经打开，则建立对该文件的新引用；如果尚未打开，则先打开该文件。`lookuppn()` 函数按“/”分隔路径名的各个组件，并为路径名的每个组件调用特定于文件系统的 `vop_lookup()` 方法。

如果路径名以“/”开头，路径名遍历从用户的根目录开始；否则，从用户当前目录所指向的 vnode 开始。`lookuppn()` 使用 `vop_lookup()` vnode 方法一次一个组件地遍历路径。`vop_lookup()` 接受一个目录 vnode 和一个组件作为参数，并返回表示该组件的 vnode。

如果目录 vnode 设置了 `v_vfsmountedhere`，那么它就是一个挂载点。如果 `lookuppn()` 在沿文件系统树向下遍历时遇到挂载点，则沿该 vnode 的 `v_vfsmountedhere` 指针进入已挂载的文件系统，并调用 `vfs_root()` 方法获取该文件系统的根 vnode。路径名遍历随后从该点继续。

如果 `lookuppn()` 在跟随“..”时遇到根 vnode（`v_flag` 中设置了 `VROOT` 标志），则 `lookuppn()` 会沿该 vnode 关联的 vfs 中的 `vfs_vnodecovered` 指针获取被覆盖的 vnode。

如果 `lookuppn()` 遇到符号链接，则调用 `vn_readlink()` vnode 方法获取该符号链接。如果符号链接以“/”开头，则从根目录重新开始路径名遍历；否则，从最后一个目录继续遍历。`lookuppn()` 的调用者指定路径名的最后一个组件如果是符号链接，是否要跟随该链接。

该过程持续进行，直到路径名用完或发生错误。当 `lookuppn()` 完成时，它返回表示目标文件的 vnode。

### 13.5.2 vop_lookup() 方法

`vop_lookup()` 方法在目录中搜索与提供的路径名匹配的路径名组件。`vop_lookup()` 方法接受一个目录 vnode 和一个字符串路径名组件作为参数，并返回一个指向表示该文件的 vnode 的 vnode 指针。如果找不到该文件，则返回 `ENOENT`。许多常规文件系统会首先检查目录名查找缓存；如果找到条目，则返回该条目。如果在目录名缓存中未找到条目，则执行一次真正的文件查找。

### 13.5.3 vop_readdir() 方法

`vop_readdir()` 方法将目录内容分块读入 `uio` 结构。每个块可容纳的条目数以 `uio` 结构提供的大小为上限。`uio_resid` 结构成员显示 `getdents` 请求的大小（以字节为单位），该大小除以 `vop_readdir()` 方法生成的目录项大小，即可计算出要返回的目录项数量。

目录是通过内核缓冲文件函数 `fbread` 和 `fbwrite` 从磁盘读取的。这些函数在表 13-11 中描述，是通用文件系统基础设施的一部分。

**表 13-11** *从内核内部对文件进行缓存访问的函数*

| 函数名称 | 描述 |
|---|---|
| `fbread()` | 对于给定的 `<vp, off>`，返回指向已锁定内核虚拟地址的指针，长度为 `len` 字节。该读取不能跨越 `MAXBSIZE`（8192）字节的边界。 |
| `fbzero()` | 与 `fbread()` 类似，但调用 `segmap_pagecreate()` 而不是 `segmap_fault()`，以便 `SOFTLOCK` 可以在不使用 `VOP_GETPAGE()` 的情况下创建页。然后，`fbzero()` 将长度按页边界取整，并清零相应范围。 |
| `fbwrite()` | 直接写入。 |
| `fbwritei()` | 直接写入并使页失效。 |
| `fbdwrite()` | 延迟写入。 |
| `fbrelease()` | 释放 fbp。 |
| `fbreleasei()` | 释放 fbp 并使页失效。 |

### 13.5.4 路径名遍历函数

几个路径名操作函数辅助路径名的分解。路径名函数使用如下所示的路径名结构来传递路径名组件。

```
/*
 * Path-name structure.
 * System calls that operate on path names gather the path name
 * from the system call into this structure and reduce it by
 * peeling off translated components. If a symbolic link is
 * encountered, the new path name to be translated is also
 * assembled in this structure.
 *
 * By convention pn_buf is not changed once it's been set to point
 * to the underlying storage; routines which manipulate the path name
 * do so by changing pn_path and pn_pathlen. pn_pathlen is redundant
 * since the path name is null-terminated but is provided to make
 * some computations faster.
 */
typedef struct pathname {
        char     *pn_buf;          /* underlying storage */
        char     *pn_path;         /* remaining pathname */
        size_t    pn_pathlen;      /* remaining length */
        size_t    pn_bufsize;      /* total size of pn_buf */
} pathname_t;
```

**头文件** `<sys/pathname.h>`

路径名函数见表 13-12。

**表 13-12** *来自 `<sys/pathname.h>` 的路径名遍历函数*

| 方法 | 描述 |
|---|---|
| `pn_alloc()` | 分配一个新的路径名缓冲区。 |
| `pn_get()` | 从用户空间复制路径名字符串，并将参数装配到一个路径名结构中。 |
| `pn_set()` | 将路径名设置为给定的字符串。 |
| `pn_insert()` | 组合两个路径名。 |
| `pn_getsymlink()` | 跟踪路径名的符号链接。 |
| `pn_getcomponent()` | 提取下一个分隔的路径名组件。 |
| `pn_setlast()` | 将组件追加到路径名末尾。 |
| `pn_skipslash()` | 跳过路径名中连续的斜杠。 |
| `pn_fixslash()` | 消除路径名末尾的任何斜杠。 |
| `pn_free()` | 释放一个路径名结构。 |

### 13.5.5 目录名查找缓存（DNLC）

目录名查找缓存基于 BSD 4.2 代码。它被移植到 Solaris 2.0，进行了线程化，并经历了一些重大修订。DNLC 的大部分增强都集中在性能和线程化方面，但少数可见的
