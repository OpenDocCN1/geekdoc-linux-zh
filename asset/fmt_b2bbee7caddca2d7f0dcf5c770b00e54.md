
默认 ACL 不参与确定访问目录时授予的权限。相反，它的存在与否会影响在目录中创建的文件和子目录的 ACL 以及权限。（默认 ACL 存储为名为 `system.posix_acl_default` 的扩展属性。）

要查看和设置目录的默认 ACL，我们使用 `setfac` 命令的 `-d` 选项：

```
$ mkdir sub
$ setfac -d m u::rw-,u:paul:r-x,g:teach:rwx,o::-- sub
$ getfacl --omit-header sub
user::rw-
user:paul:r-x
group:teach:rwx
mask::rwx
other::---
```

我们可以使用 `setfac -k` 选项从目录中移除默认 ACL。

如果一个目录具有默认 ACL（default ACL），那么：

- 在该目录中创建的新子目录将继承该目录的默认 ACL 作为其自身的默认 ACL。换句话说，默认 ACL 会沿着树形结构向下传播，直到创建新的子目录。
- 在该目录中创建的新文件或子目录将继承该目录的默认 ACL 作为其访问 ACL（access ACL）。与传统权限位对应的 ACL 条目将与系统调用（`open`、`mkdir` 等）在创建文件或子目录时指定的 `mode` 参数中的对应位进行掩码处理（与运算），以创建该文件或子目录。我们所说的“对应的 ACL 条目”是指：

```
ACL_USER;
ACL_MASK 或（如果 ACL_MASK 不存在，则是 ACL_GROUP_OBJ）；以及
ACL_OTHER.
```

当目录具有默认 ACL 时，进程掩码（第 15.4.6 节）不参与确定目录中创建的新文件条目的权限。

作为一个新文件如何从父目录 ACL 继承其 ACL 的示例，假设我们使用以下 `open()` 调用在上述创建的目录中创建一个新文件：

```
open("sub/tfile", O_RDWR | O_CREATE, S_IRWX | S_IXGRP | S_IXOTH); /* rwx--x--x */
```

新文件将具有以下 ACL：

```
$ getfacl --omit-header sub/tfile
user::
user:r-x #effective::x
group::r-x #effective::x
group:rwx #effective::x
mask::--x
other::--x
```

如果目录没有默认 ACL，那么：

- 在该目录中创建的新子目录也不会有默认 ACL。
- 新文件或目录的权限将按照传统规则（第 15.4.6 节）设置：文件权限被设置为 `mode` 参数（传递给 `open()`、`mkdir()` 等）中的值，并减去被进程掩码关闭的位。这导致在文件文件上产生一个最小的 ACL。

### 17.7 ACL 实现限制

各种文件系统实现对 ACL 条目的数量施加了限制：

- 在 `ext2`、`ext3` 和 `ext4` 上，文件上的 ACL 总数受限于以下要求：文件扩展属性中所有名称和值的字节必须在一个单个逻辑磁盘块内（第 16.2 节）。每个 ACL 条目需要 8 字节，因此一个文件的最大 ACL 条目数量要少一些（因为 ACL 扩展属性名称有一定的开销）。因此，4096 字节的块大小允许最多约 500 个 ACL 条目。（内核 2.6.11 对 `ext2` 和 `ext3` 的 ACL 实施了 32 条的任意限制）。
- 在 `XFS` 上，ACL 被限制为 25 条条目。
- 在 `Reiserfs` 和 `JFS` 上，ACL 可以包含多达 8191 条条目。此限制是 VFS 对扩展属性值施加的大小限制（64 kB）的结果（第 16.2 节）。

在编写时，`Bfs` 将 ACL 限制在 500 条左右。然而，由于 `Bitfs` 仍在大力开发中，此限制可能会发生变化。

上述大多数文件系统允许在 ACL 中创建大量条目，但由于以下原因应避免这样做：

- 维护冗长的 ACL 将变成一项复杂且容易出错的系统管理任务。
- 扫描 ACL 以查找匹配条目（在组 ID 检查时为多个匹配条目）所需的时间随 ACL 条目数量呈线性增长。

通常，我们可以通过在系统组文件（第 8.3 节）中定义合适的组并在 ACL 中使用这些组，将文件的 ACL 条目数量保持在合理范围内。

### 17.8 ACL API

`POSIX.le` 草案标准定义了大量函数和数据结构来操作 ACL。由于这些函数非常多，我们不尝试描述所有这些函数的细节。相反，我们提供了它们使用用法的概述，并以一个示例程序结束。

使用 ACL API 的程序应该包含 `<sys/acl.h>`。如果程序使用了对 `POSIX.le` 草案标准的各种 Linux 扩展，则可能还需要包含 `<libacl.h>`。（Linux 扩展列表在 `acl(5)` 手册页中提供。）使用此 API 的程序必须使用 `-lacl` 选项编译，以便链接到 `libacl` 库。

如前所述，在 Linux 上，ACL 是使用扩展属性实现的，而 ACL API 被实现为一组库函数，这些函数操作用户数据结构，并在必要时调用 `getxattr()` 和 `setxattr()` 来检索和修改持有 ACL 表示形式的磁盘扩展属性。应用程序也可以（尽管不推荐）使用 `getxattr()` 和 `setxattr()` 直接操作 ACL。

#### 概述

构成 ACL API 的函数列在 `acl(5)` 手册页中。初看之下，这些大量的函数和数据结构可能会让人困惑。图 17-2 提供了各种数据结构之间关系的概述，并指出了许多 ACL 函数的使用。

![](img/9979af2ec677a84a39c7b1fd105c84a4_373_3)

图 17-2：ACL 函数与数据结构之间的关系

从图 17-2 中，我们可以看到各种数据结构之间的关系，并指出了许多 ACL 函数的使用。

从图 17-2 中，我们可以看到 ACL API 将 ACL 视为一个分级对象：

- ACL 包含多个条目。
- 每个 ACL 条目由一个标签（tag）、一个可选的限定符（qualifier）和一个权限集（permission set）组成。

我们现在简要查看这些函数。

#### 获取文件的 ACL

`get_file()` 函数检索文件的 ACL 副本到内存：

```
acl_t acl;

acl = get_file(pathname, type);
```

这取决于 `type` 是 `ACL_ACCESS` 还是 `ACL_DEFAULT`。

#### 从内存中检索条目

`get_entry()` 函数返回一个条目的句柄：

```
acl_entry_t entry;

status = get_entry(acl, entry_id);
```

`entry_id` 指定要检索的条目。如果 `entry_id` 指定为 `ACL_FIRST_ENTRY` 或 `ACL_NEXT_ENTRY`。

#### 检索并修改条目中的属性

`get_type()` 和 `set_type()` 函数检索并修改条目中的标签：

```
acl_tag_t tag;

status = get_type(entry);
status = set_type(entry, tag);
```

`tag` 参数的类型为 `acl_type_t`，取值为 `ACL_USER_OBJ`、`ACL_USER`、`ACL_GROUP_OBJ`、`ACL_GROUP`、`ACL_OTHER` 或 `ACL_MASK`。

#### 检索并设置限定符

`get_qualifier()` 和 `set_qualifier()` 函数检索并修改 ACL 中的限定符。这里假设我们已经确定这是一个 `ACL_USER` 条目：

```
/* 指向 UID */
uid_t *qualp;
qualp = get_qualifier(entry);
status = set_qualifier(entry, qualp);
```

限定符仅当条目类型为 `ACL_USER` 或 `ACL_GROUP` 时有效。在前者情况下，`qual` 指向用户 ID (`uid_t *`)；在后者情况下，它指向组 ID (`gid_t *`)。

#### 检索并设置权限集

`get_permset()` 和 `set_permset()` 函数检索并修改条目中的权限集：

```
acl_permset_t permset;

status = get_permset(entry, &permset);
status = set_permset(entry, permset);
```

`acl_permset_t` 类型是一个指向权限集的句柄。以下函数用于操作权限集的内容：

```
int is_set;

is_set = get_perm(permset, perm);

status = add_perm(permset, perm);
status = delete_perm(permset, perm);
status = clear_perms(permset);
```

在这些调用中，`perm` 被指定为 `ACL_READ`、`ACL_WRITE` 或 `ACL_EXECUTE`，其含义显而易见。这些函数的使用如下：

- `acl_get_perm()` 函数如果指定的权限在 `permset` 所指的权限集中启用则返回 1 (true)，否则返回 0。该函数在 `POSIX.1e` 草案中启用。
- `acl_add_perm()` 函数将指定的权限添加到 `permset` 所指的权限集中。
- `acl_delete_perm()` 函数从 `permset` 所指的权限集中移除指定的权限。（如果该权限不在集合中，则移除它不会报错）。
- `acl_clear_perms()` 函数从 `permset` 所指的权限集中移除所有权限。

### 创建和删除 ACL 条目

`acl_create_entry()` 函数在现有 ACL 中创建一个新条目。指向新条目的句柄返回在第二个参数的位置。

```c
acl_entry_t entry;
```

```c
status = acl_create_entry(&acl, &entry);
```

新条目可以使用之前描述的函数进行填充。`acl_delete_entry()` 从 ACL 中移除一个条目。

```c
status = acl_delete_entry(acl, entry);
```

### 更新文件的 ACL

`acl_set_file()` 函数是 `acl_get_file()` 的逆操作。它根据 `acl` 参数指向的内存中 ACL 内容，更新磁盘上的 ACL。

```c
int status;
```

```c
status = acl_set_file(pathname, type, acl);
```

`type` 参数可以是 `ACL_TYPE_ACCESS`（用于更新访问 ACL）或 `ACL_TYPE_DEFAULT`（用于更新目录的默认 ACL）。

### 在内存 ACL 与文本 之间转换

`acl_from_text()` 函数将包含长文本或短文本格式 ACL 的字符串转换为内存中的 ACL，并返回一个句柄，用于在后续函数调用中引用该 ACL。

```c
acl = acl_from_text(acl_string);
```

`acl_to_text()` 函数执行反向转换，返回与 `acl` 参数指向的 ACL 对应的长文本字符串。

```c
char *str;
size_t len;
```

```c
str = acl_to_text(acl, len);
```

如果未指定 `len` 参数为 NULL，则它指向的缓冲区将用于返回函数结果字符串的长度。

### ACL API 中的其他函数

接下来的段落描述了几个在图 17-2 中未显示的常用 ACL 函数。

`acl_calc_mask(&acl)` 计算并设置由参数指向的内存 ACL 中 `ACL_MASK` 的权限。通常，每当我们创建或修改 ACL 时都会使用此函数。`ACL_MASK` 权限被计算为 `ACL_USER`、`ACL_GROUP` 和 `ACL_GROUP_OBJ` 条目中权限的并集。该函数的一个很有用的属性是，如果 `ACL_MASK` 条目不存在，它会创建它。这意味着如果我们向先前的最小 ACL 中添加 `ACL_USER` 和 `ACL_GROUP` 条目，则可以使用此函数来确保创建 `ACL_MASK` 条目。

`acl_valid(acl)` 函数在参数指向的 ACL 有效时返回 0，否则返回 -1。如果满足以下所有条件，则该 ACL 是有效的：

- `ACL_USER_OBJ`、`ACL_GROUP_OBJ` 和 `ACL_OTHER` 条目恰好出现一次；
- 如果存在任何 `ACL_USER` 或 `ACL_GROUP` 条目，则存在一个 `ACL_MASK` 条目；
- 最多有一个 `ACL_MASK` 条目；
- 每个 `ACL_USER` 条目都有唯一的用户 ID；以及
- 每个 `ACL_GROUP` 条目都有唯一的组 ID。

`acl_check(acl)` 和 `acl_error()` 函数（后者是 Linux 扩展）是 `acl_valid()` 的替代方案，它们不那么流行，但对格式错误的 ACL 中的错误提供了更精确的描述。详情请参见手册页。

`acl_delete_file(pathname)` 函数移除 `pathname` 所指目录的默认 ACL。`acl_init(count)` 函数创建一个空的 ACL 结构，初始包含存储至少 `count` 个 ACL 的空间。（`count` 是对系统关于预期用量的提示，而不是硬性限制。）函数返回一个新 ACL 的句柄。`acl_dup(acl)` 函数创建 `acl` 所指 ACL 的副本，并返回副本 ACL 的句柄作为函数结果。`acl_free(handle)` 函数释放由其他 ACL 函数分配的内存。例如，我们使用 `acl_free()` 来释放由调用 `acl_from_text()`、`acl_to_text()`、`acl_get_file()`、`acl_init()` 和 `acl_dup()` 分配的内存。

### 程序

列表 17-1 展示了 ACL 库函数的使用。该程序获取并显示文件的 ACL（即它提供了 `getfac` 命令 的部分功能）。如果指定了 `-d` 命令行选项，则程序将显示（目录的）默认 ACL 而不是访问 ACL。

以下是该程序的使用示例：

```bash
$ tfile
$ setfac -m u:annie:rw,u:paul:rw,g:teach:r tfile
$ ./acl_view tfile
user_obj rw-
user    annie r---
user    paul rw---
group_obj r---
group   teach rw-
mask    r---
other   r--
```

本书的源发行版还包含一个程序 `acl_update.c`，它对 ACL 执行更新（即它提供了 `setfac` 命令的部分功能）。

## 列表 17-1：显示文件上的访问或默认 ACL
