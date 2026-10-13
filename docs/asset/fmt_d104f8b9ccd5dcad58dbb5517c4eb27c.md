
| Filesystem state: | clean |
| Errors behavior: | Continue |
| Filesystem OS type: | Linux |
| Inode count: | 25688 |
| Block count: | 102400 |
| Reserved block count: | 5120 |
| Free blocks: | 93504 |
| Free inodes: | 25677 |
| First block: | 1 |
| Block size: | 1024 |
| Fragment size: | 1024 |
| Group descriptor size: | 64 |
| GDT blocks: | 256 |
| Blocks per group: | 8192 |
| Fragments per group: | 8192 |
| Inodes per group: | 1976 |
| Inode blocks per group: | 247 |
| Flex block group size: | 16 |
| Filesystem created: | Sat May 16 03:44:37 2015 |
| Last mount time: | n/a |
| Last write time: | Sat May 16 03:44:37 2015 |
| Mount count: | 0 |
| Maximum mount count: | -1 |
| Last checked: | Sat May 16 03:44:37 2015 (<none>) |
| Check interval: | 0 4447 kB |
| Lifetime writes: | 0 (user root) |
| Reserved blocks uid: | 0 (group root) |
| First inode: | 11 |
| Inode size: | 128 |
| Journal inode: | 8 |
| Default directory hash: | half_md4 |
| Directory Hash Seed: | a87a5804-f7c6-4028-89ed-799c2bb47133 |
| Journal backup: | inode blocks |

如你所示，`tune2fs -l`命令显示了许多文件系统属性。一个有趣的属性是文件系统标签，显示为`Filesystem volume name`。标签用于为文件系统设置唯一名称，使得即使底层设备名称发生变化，文件系统也可以被挂载。此外，文件系统特性和默认挂载选项也非常有趣。

# 338 红帽 RHCSA/RHCE 7 认证指南

要更改任何默认文件系统选项，`tune2fs`命令允许你通过其他参数来实现。下面列出了一些常见的用法示例：

- 使用`tune2fs -o`设置文件系统挂载选项。当设置到文件系统后，通过`/etc/fstab`挂载时就不再需要指定该选项了。例如，使用`tune2fs -o acl,user_xattr`来开启访问控制列表，并在选项前使用`^`符号将其关闭，如`tune2fs -o ^acl,user_xattr`所示。
- 使用`tune2fs`切换可能默认启用的文件系统特性。要启用某个文件系统特性，使用`tune2fs -O`后跟该特性。要关闭某个特性，在特性名称前使用`^`。
- 使用`tune2fs -L`在文件系统上设置标签。正如本章后面“挂载文件系统”部分所述，你可以使用文件代替设备名。除了`tune2fs -L`，`label`命令也允许你完成操作。

## 管理 XFS 文件系统属性

XFS 文件系统是一个完全不同的文件系统，因此拥有一套完全不同的工具来管理其属性。它不允许在元数据中设置文件系统属性。然而，你可以使用`xfs_admin`命令更改 XFS 属性。例如，使用`xfs_admin -L`设置文件系统标签。

## 管理 Swap 分区

在 Linux 上，绝大多数分区都用于普通文件系统。在 Linux 上，空间通常分配在磁盘上。这可以是分区或 LVM 卷（第 15 章讨论）。紧急情况下，你可以使用文件来扩展可用 swap。在 Linux 上使用 swap 是提高内存利用的一种方便方法。如果发生 RAM 不足，使用的页面可以移动到 swap，从而为需要访问内存的程序提供更多 RAM。由于如此，大多数 Linux 服务器都配置了 swap。

*(注：由于原文中该段落出现了大量重复，翻译处已根据“不要重复输出原文”的原则进行了去重处理，保留了核心逻辑)*

## 添加 Swap 文件

在 Linux 上，你使用大多数分区用于普通文件系统。在 Linux 上，空间通常分配在磁盘上。这可以是分区或 LVM 卷（第 15 章讨论）。紧急情况下，你可以使用文件来扩展可用 swap。在 Linux 上使用 swap 是提高内存利用的一种方便方法。如果发生 RAM 不足，使用的页面可以移动到 swap，从而为需要访问内存的程序提供更多 RAM。由于如此，大多数 Linux 服务器都配置了 swap。

*(注：此处同样重复，请参考上文)*

## 练习 14.5 创建 Swap 分区

- 1. 使用`fdisk /dev/vda`打开磁盘。
- 2. 按`n`创建新分区。
- 3. 按`p`选择主分区。
- 4. 按`3`选择分区号。
- 5. 按回车使用默认起始扇区。
- 6. 输入`+2G`设置分区大小。
- 7. 按`w`保存并退出。
- 8. 使用`mkswap /dev/vda3`格式化分区。
- 9. 使用`swapon /dev/vda3`启用分区。
- 10. 使用`swapon --show`确认结果。

## 添加 Swap 文件

要添加 swap 文件，你需要先创建一个 1G 的文件：

```bash
