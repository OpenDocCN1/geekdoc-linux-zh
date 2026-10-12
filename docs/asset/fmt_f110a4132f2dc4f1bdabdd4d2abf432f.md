
```c
    int (*smap) (struct inode *, int);

};

```

- `create(dir, name, len, mode, res_inode)` 此函数打开 `_namei()`。该函数从 VFS `namei()` 内部调用。它执行若干任务。首先，它通过 `get_empty_inode()` 函数从完整的 inode 列表中提取空闲 inode。现在 inode 结构需要填充文件系统特定的数据，例如，在介质上寻找空闲 inode。此 `createO` 进入 `dir` 指定的目录并指定长度的文件名。如果文件系统实现不存在 `createO`，VFS 返回错误 `EACCESS`。

- `Lookup(dir, name, Len, res_inode)` 提供了文件名、其长度以及参数 `res_inode` 中的文件 inode。这是通过扫描 `dir` 指定的目录完成的。目录必须定义 `Lookup()` 函数，否则 VFS 将返回错误 `ENOTDIR`。调用的 VFS 函数 `LookupO` 为名称 `..` 执行特殊过程。如果进程已经在其根目录，则返回根 inode。如果挂载文件系统的根 inode 被 `..` 越过，VFS 使用“隐藏” inode 调用 inode 操作。

- `Link(inode, dir, name)` 此函数建立硬链接。文件 inode 将在指定的名称下以及 `dir` 指定目录中的关联链接链接。在调用 `Link()` 之前，会检查 `dir` 和 `oldname` 是否在同一设备上，以及当前进程是否有权写入 `dir`。如果缺少此函数，VFS 中的调用函数返回错误 `EPERH`。

- `unLink(dir, name, Len)` 此函数删除 `dir` 指定目录中的指定文件。调用函数首先确认此操作拥有相应的权限。如果 `unLO` 未实现，VFS 返回错误 `EPERM`。

- `symLink(dir, name, Len, synonym)` 此函数在 `dir` 目录中建立符号链接名称，`Len` 提供名称长度。在 VFS 调用之前，将通过调用 `permission()` 检查访问权限。如果特定实现中不存在 `symLink()`，VFS 返回错误 `EPERM`。

- `mkdir(dir, name, Len, mode)` 此函数在 `dir` 目录中建立名为 `name` 权限为 `mode` 的子目录。`mkdir()` 函数必须首先检查目录是否允许子目录，然后在数据介质上分配一个空闲 inode 和一个空块，然后写入目录连同其默认条目 `.` 和 `..`。权限在调用的 VFS 函数中已经检查过。如果 `mkdirO` 函数未实现，则返回错误 `EPERM`。

Linux 内核内部 - 174 -

- `rmdir(dir, name, Len)`
此函数从目录中删除子目录名称。该函数首先检查要删除的目录是否为空，以及当前是否被某个进程使用，如果目录设置了粘滞位（sticky bit），还会检查该进程是否为子目录的所有。与已描述的函数一样，访问权限会由 VFS 函数预先检查。如果没有实现 `rmdir()`，VFS 返回 `EPERM`。

- `knod(dir, name, Len, mode, rdev)`
此函数在 `mode` 模式下创建一个新的 inode。该 inode 将在目录 `dir` 中赋予名称。如果该 inode 是设备文件（在这种情况下适用 `s_ISBLK(mode)` 或 `S_ISCHR(mode)` 之一），则参数 `rdev` 提供了设备号。如果未实现此函数，则返回 `EPERM`。

- `rename(inode, oldname, oLen, newname, nlen)`
此函数更改文件的名称。这涉及从目录中移除旧名称并在 `dir` 中输入新名称。调用函数会预先检查目录中相关的访问权限，并进行进一步检查以确保目录 `.` 不作为操作的源或目的。如果缺少该函数，VFS 将生成 `EPERM` 错误。

- `readLink(Inode, buf, size)`
此函数读取符号链接并将路径名复制到用户地址空间的的缓冲区中。如果缓冲区太小，路径名应简单地截断。如果 inode 不是符号链接，应返回 `EINVAL`。在检查了对缓冲区 `buf` 的访问权限并使用 `Namei()` 找到 inode 后，此函数会从 `sys_readlink` 直接调用。如果实现未执行这些，系统调用将返回错误 `EINVAL`。

- `follow(dir, inode, flag, mode, res_inode)`
此函数用于解析符号链接。对于分配给符号链接的 inode，此函数将链接指向的 inode 在参数 `res_inode` 中返回。为了避免无限循环³，LINUX 中将要解析的最大链接数设置为 5。在实现中，这是“硬编码”的，任何编写的实现都应该遵循此示例。
如果缺少 `follow_link()`，VFS 中同名的调用函数将直接返回 inode，就像该链接指向自身一样。这种行为意味着 VFS 函数可以始终调用

而无需测试当前 inode 描述的是文件还是符号链接。

> ³ 符号链接终究可以指向另一个符号链接。

- `bmap(inode, block)`
调用此函数是为了启用文件的内存映射。在参数 `block` 中给出了文件内逻辑数据块的编号。此编号必须由 `bmap()` 转换为介质上块的逻辑编号。为了做到这一点，`bmap()` 在指定 inode 的实际实现中搜索该块并返回其编号。在某些情况下，这可能涉及从介质读取其他块。返回值为 0 表示错误，如果文件系统未定义 `bmap`，则由文件系统的调用函数 `bmap()` 返回该值。
此函数由 `generic_mmap` 使用，将文件映射到用户地址空间中的地址。如果找不到，必须先将可执行文件完全加载到内存中，因为无法无法更高效的高需分页。

- `truncate(inode)`
此函数主要用于缩短文件，但如果特定实现支持，也可以将文件延长到任意长度。`truncate()` 需要的唯一参数是待修改文件的 inode，在调用函数之前会将 `i_size` 字段设置为新长度。`truncate()` 函数在内核的多个处使用，通过系统调用 `sys_truncate()` 以及在打开文件时。它还将释放文件不再需要的块。因此，如果随后清除了介质上的 inode，可以使用 `truncate()` 函数来物理删除文件。虽然该函数的功能描述非常简单，但实现起来可能非常复杂，因为可能会出现同步问题。如果未实现此函数，则不生成错误消息。在这种情况下，由于 `i_size` 组件已预先设置，文件长度似乎发生了变化。

- `permission(inode, flag)`
此函数检查由掩码赋予的文件访问权限。可能的值为 `MAY_READ`、`MAY_WRITE` 和 `MAY_EXEC`。如果该函数不可，虚拟文件系统中的调用函数将检查标准的 UNIX 权限，这意味着该实现实际上是没有必要的，除非要实现额外的访问机制。

- `smap(inode, sector)`
此函数主要用于允许在 UMSDOS 文件系统上创建交换文件。与 `bmap()` 类似，该 inode 为指定文件提供介质上的逻辑扇区编号（不是块或簇）。这意味着该操作仅对

UMSDOS 文件系统实现有意义，但 MS-DOS 文件系统已以 `mdsos_smap()` 函数的形式提供了该功能，然而，它仅在内部使用。在内存管理 `rw_swap_page()` 中，如果 `bmap()` 不可用，则需要 `bmap()` 函数与交换文件配合。

### 6.2.5 文件结构

在多任务系统中，经常出现一个问题：多个进程希望同时访问一个文件进行读取和写入。文件结构用于维护每个打开文件的状态，例如当前偏移量、访问模式和其他信息。这些信息独立于描述文件的 inode。

文件结构定义如下：

```c
struct file {
    mode_t f_mode;          /* 访问模式 */
    loff_t f_pos;           /* 文件位置 */
    unsigned short f_flags; /* 标志位 */
    int f_count;            /* 引用计数 */
    struct inode *f_inode;  /* inode */
    struct file_operations *f_op; /* 操作 */
    void *private_data;      /* 驱动特定数据 */
};
```

在多任务系统中，经常出现一个问题：多个进程希望同时访问一个文件进行读取和写入。文件结构用于维护每个打开文件的状态，例如当前偏移量、访问模式和其他信息。这些信息独立于描述文件的 inode。

### 6.2.6 文件操作

`file_operations` 结构是文件的通用接口，包含了打开、关闭、读取和写入函数。相反，inode 操作只使用 inode。

```c
struct file_operations {
```
