

## 2.8 Proc 文件系统

```c
struct proc_dir_entry
{
    unsigned short low_ino;
    unsigned short namelen;
    const char *name;
    mode_t mode;
    nlink_t nlink;
    uid_t uid;
    gid_t gid;
    unsigned long size;

    struct proc_dir_entry *next, *parent, *subdir;
    void *data;
    int (*get_info)(buffer, start, off, count);
    int (*read_proc)(buffer, start, off, count, eof, data);
    int (*write_proc)(file, buffer, count, data);
    int (*readlink_proc)(proc_dir_entry, page);
    unsigned int count; /* 使用计数 */
    int deleted; /* 删除标志位 */
};
```

图 2-10：
proc_dir_entry 结构。

low_ino 是文件的 inode 编号。该值在文件初始化时由 `proc_register` 自动填充。
namelen 指定文件或目录名 `name` 的长度。
`name` 是指向文件（或目录）名称的指针。
mode 指定文件的模式；对于目录，此值设置为 `S_DIR`。
nlinks 指定指向此文件的链接数（默认 = 1）。
uid 或 gid 指定文件的用户 ID 或组 ID。
size 指定文件的长度，如在显示目录时所示的长度。
`data` 是一个可以指向私有数据的指针。
`next`、`parent` 和 `subdir` 是连接 proc 目录结构的指针。
`read_proc()` 在你访问 proc 文件时运行。该函数的唯一任务是将文件的输出填充到 `buffer` 中，并返回写入的字符数作为结果。
`write_proc()` 在访问 proc 文件时被调用。

在早期的内核版本中，向 proc 目录添加每个条目都必须为每个条目创建并初始化 `proc_dir_entry` 结构。如上所示，结构中的许多变量仅在注册后才需要。
定义了以下函数来简化对 proc 条目的处理。

```c
create_proc_entry()                                              fs/proc/generic.c
```

`create_proc_entry(name, mode, parent)` 在 proc 目录中创建一个名为 `name` 的文件。可以在 `name` 中指定相对于 `/proc/` 的相对路径，或者在参数 `parent` 中设置文件应出现的目录的 `proc_dir_entry` 结构指针。对 `/proc` 和 `/proc/net` 目录的引用可以通过 `proc_root` 和 `proc_net` 指针获取。`mode` 参数允许你传递要创建的 proc 文件的属性标志。通常，此值填充为 0。

通过此函数，你将获得指向指向创建的 `proc_dir_entry` 的指针。现在你可以继续处理针对该 proc 文件的读写操作的例程。你还可以将 `data` 指针设置为 proc 条目的私有数据。当一个读或写函数被用于多个 proc 文件时，这一点尤为必要。

以下源代码是一个展示如何创建和初始化 proc 文件 `/proc/net/test` 的良好示例：

```c
test_entry = create_proc_entry("test", 0600, proc_net);
test_entry->nlink = 1;
test_entry->data = (void *) &test_data;
test_entry->read_proc = test_read_proc;
test_entry->write_proc = test_write_proc;
```

```c
remove_proc_entry()
```

`remove_proc_entry(name, parent)` 移除 `name` 中指定的 proc 文件。与 `create_proc_entry()` 类似，你可以指定相对于 `/proc` 的相对路径，或者文件所在目录的 `proc_dir_entry` 结构。

```c
proc_mkdirdir()
```

虽然可以使用 `create_proc_entry()` 在 proc 目录中创建目录，但内核提供了一种更简单的方法 `proc_mkdir(name, parent)`。`name` 和 `parent` 参数可以用于上述函数中。该函数的返回是指向所创建目录的 `proc_dir_entry` 结构的指针。附录 D 中的示例展示了如何使用此函数创建 `/proc/test/test`。

```c
create_proc_read_entry()
```

```c
include/Linux/proc_fs.h
```

我们通常只想在 proc 目录中创建文件以显示信息。这意味着注册一个函数来处理对 proc 文件的读访问就足够了。虽然你可以像我们的示例那样使用 `create_proc_entry()` 然后注册读函数，但内核提供了另一个函数可以一步到位完成此操作。

`create_proc_read_entry(name, mode, base, get_info)` 创建 proc 文件名并使用函数 `get_info()` 初始化读访问。`name`、`mode` 和 `base` 参数被用于 `create_proc_entry()` 中。

在上述示例中，如果对 proc 文件 `/proc/net/test` 没有写访问且不需要传递私有数据，该函数可以简化如下，其中 `get_info()` 是用于处理对 proc 文件读访问的方法：

```c
test_entry = create_proc_read_entry("test", 0600, proc_net, test_get_info());
```

```c
create_proc_info_entry()
include/linux/proc_fs.h
```

`create_proc_info_entry(name, mode, base, get_info)` 创建 proc 文件名并使用函数 `get_info()` 初始化读访问。`name`、`mode` 和 `base` 参数被用于 `create_proc_entry()` 中。

在上述示例中，如果对 proc 文件 `/proc/net/test` 没有写访问且不需要传递私有数据，该函数可以简化如下，其中 `get_info()` 是用于处理对 proc 文件读访问的方法：

```c
test_entry = create_proc_read_entry("test", 0600, proc_net, test_get_info());
```

## 版本控制

