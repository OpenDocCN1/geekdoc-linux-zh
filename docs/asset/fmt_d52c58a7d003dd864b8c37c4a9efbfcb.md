
## 14. 创建条目

## 14. 读取条目

## 14. 写入条目

## 14. seq_file 接口

## 14. 实验

# 第 14 章：proc 文件系统

## 14.1 什么是 proc 文件系统？

`proc` 文件系统是一个伪文件系统；它只存在于内存中，并挂载在一个空的 `/proc` 目录上。`proc` 文件系统中的信息仅在被访问时生成；它并不会持续更新。

`proc` 中的条目可以在读取时用于获取有关系统（以及设备驱动程序）的信息。向条目写入内容可以设置系统参数并修改设备功能。

## 14.1 什么是 proc 文件系统？

`proc` 文件系统是一个伪文件系统；它只存在于内存中，并挂载在一个空的 `/proc` 目录上。`proc` 文件系统中的信息仅在被访问时生成；它并不会持续更新。

`proc` 中的条目可以在读取时用于获取有关系统（以及设备驱动程序）的信息。向条目写入内容可以设置系统参数并修改设备功能。

## 14. 读取条目

使用 `proc`（与使用 `ioctl()` 或普通文件相比）两个优势是它对所有用户可用且可访问（提供适当的权限）。

```c
write_proc_t *write_proc;
stime_t count;
/* use count */
int deleted;
kndev_t rdev;
```

`proc` 的某些功能已经迁移到 `sys` 文件系统（挂载在 `/sys` 下）。由于 `proc` 的某些部分受到缺乏标准和约定的影响，人们还应该评估 `proc` 是否为最佳选择。

我们将详细讨论的重要字段是读取和写入回调函数 `read_proc()` 和 `write_proc()`。

## 14. 创建条目

数据指针可以像私有的 `data_pointer` 一样使用。特别对于为多个条目使用相同的名称读取和写入回调函数，它非常有用。

在 `proc` 文件系统中创建和管理条目是通过以下方式完成的：

你可以更改上述结构体字段的所有者和权限，这些更改将反映在目录中。

```c
#include <linux/proc_fs.h>

struct proc_dir_entry *create_proc(const char *name, struct mode_t mode,
                                    struct proc_dir_entry *parent);
void remove_proc(struct proc_dir_entry *parent, const char *name, struct proc_dir_entry *parent);
struct proc_dir_entry *create_symlink(const char *name, struct proc_dir_entry *parent, const char *target);
struct proc_dir_entry *create_mkdir(const char *name, struct proc_dir_entry *parent);
```

## 14. 读取条目

当进程尝试读取 `proc` 文件系统中的条目时，会触发与该目录相关的读取回调；即，你将会有这样的代码：

```c
static proc_dir_entry *my_proc_entry;

my_proc_entry = create_entry("my_proc", NULL);
my_proc_entry->proc_read = my_proc_read;
```

赋予条目的名称将根据模块中获得的权限创建。如果父目录参数为 `NULL`，则条目将进入 `/proc/main` 目录。

在 `init_module()` 中，读取回调函数 `proc_read()` 之前已经定义。它具有整数返回类型，原型如下：

```c
typedef int (*readproc)(struct proc_dir_entry *entry, char *buf, loff_t start, loff_t count,
                             void *data);
```

父目录可以使用 `proc_mkdir()` 创建，或者如果你想将其放在 `proc` 下已创建的目录中，请使用 `proc_include(/proc/dev/proc/fs/proc/mnt/net/stat, 和 /proc/driver)`。例如，可以这样做

当我们尝试读取时，数据被写入缓冲区，偏移量最大为 `count`。对于仅几个字节，回调函数通常会忽略这些计数。

```c
my_proc = create_entry("driver/my", NULL);
```

`off` 参数仅在 `offset` 等于 `count` 时使用；它应该指示文件结尾（使用 .）。`start` 参数是某些实现中的遗留，不被使用。`data` 参数用于为多个条目创建一个回调回调函数或用于其他目的。

这里 `proc_dir_entry` 的基本结构如下：

```c
struct proc_dir_entry {
    unsigned short ushort;
    unsigned short name;
    count_t count;
    mode_t mode;
    link_t link;
    void *data;
    gid_t gid_id;
    unsigned long size;
    struct inode_operations;
};
```

函数 `proc_symlink()` 创建符号链接；它等同于 `ln -s name target`。函数 `proc_mkdir()` 在 `parent` 下创建一个目录。

成功时，返回值为写入缓冲区的字节数。这里有一个模块的简单示例：

```c
#include <linux/module.h>
#include <linux/proc_fs.h>
#include <linux/fs.h>
#include <linux/uaccess.h>

static proc_dir_entry *my_proc_entry;

static int my_proc_read(struct proc_dir_entry *entry, char *buf, loff_t start, loff_t count, void *data)
{
    /* implementation */
    return 0;
}

int __init(_)
{
    my_proc_entry = create_entry("my_proc", NULL);
    my_proc_entry->proc_read = my_proc_read;
    return 0;
}
```

## 14.5 proc_)

```c
typedef int (*readproc)(struct proc_dir_entry *entry, char *buf, loff_t start, loff_t count,
                             void *data);
```

    /* implementation */

    return 0;

}
