
写入设备，返回写入的字节数。错误代码：负值可能表示设备末尾，且不是错误。如果设备未就绪且进程设置了非阻塞标志，你也可以选择阻塞。

关于不使用用户指针的考虑同样适用。这里人们应该使用

```c
int itbytes = -copy_from_user(buffer, kbuf + *ppos, len);
```

由于我们

```c
int (*inode)(struct file *file, void *filler, int_t *fillid);
```

应该用于设备节点；仅用于目录，并由文件系统驱动程序使用，我们使用 `file_operations` 结构。

```c
unsigned int (*poll)(struct file *file, struct poll_table *pwaitqueue);
```

检查设备是否可读可写或处于某些用户空间状态。这通过 `poll()` 和 `select()` 调用访问。返回描述设备状态的位掩码。

```c
int (*ioctl)(struct inode *inode, struct file *file, int, unsigned long arg);
```

发布设备特定命令的接口。注意，某些命令是设备特有的，并且在不引用你的用户入口的情况下访问。

```c
long (*locked_inode)(struct file *file, struct inode *inode, unsigned int);
```

遵循标准的入口点；调用前不获取内核锁，调用后释放。如果两个入口点都存在，将使用后者。

```c
int (*release)(struct file *file, struct vm_area_struct *);
```

向进程请求设备消息。如果你没有实现这个，系统将返回

```c
int (*open)(struct inode *inode, struct file *file);
```

打开设备。如果为 `NULL` 则打开设备成功，但驱动程序不会通知。`open()` 方法应该：

- 如果设备是第一次被打开，检查硬件。
- 如果需要，注意设备设备号。
- 使用文件结构的 `private_data` 字段设置任何数据结构。

# 第 4 章 字符设备

## 4.9 文件和 Inode 结构

```c
int (*flush) (struct file *file);
```

当驱动程序打开文件的文件描述符时。它执行并等待设备上的操作完成。通常使用 `NULL` 即可。

```c
int (*release)(struct inode *inode, struct file *file);
```

关闭节点。当进程终止时，所有文件描述符都会关闭，除非异常退出，否则此条目可以被正确链接。`release()` 方法应该是由以下执行的操作的反操作：

```c
int (*close)(struct file *file, struct dentry *dentry, int datasync);
```

用于刷新任何挂起的数据。

```c
int (*fsync)(struct inode *inode, struct file *lock);
```

检查 `DEVICEFSYNC` 标志以进行异步通知。除非你的驱动程序支持异步通知。

```c
int (*unlock)(struct file *file, struct i_ *lock);
```

用于实现文件锁定；通常由设备驱动程序使用，仅限文件。

```c
int (*dir_notify)(struct file *file, unsigned long arg);
```

当调用 `readdir()` 请求目录更改通知时被触发。不在设备驱动程序中使用。

```c
int (*fsck)(struct inode *inode, int mode, struct file *lock);
```

用于锁定。不在设备驱动程序中使用。

## 文件和 Inode 结构

文件和 inode 结构定义在 `/usr/include/linux/fs.h` 中。两者对于控制设备都非常重要。每当打开文件时都会创建一个文件结构，并在关闭文件时释放。文件结构与用户空间无关。

一些重要的结构：

- 如果设备是第一次被打开，检查硬件。
- 如果需要，注意设备号。
- 使用文件结构的 `private_data` 字段设置任何数据结构。

引用计数嵌入在模块数据结构中，可以通过函数 `module_refcount()` 获取。它防止了模块在使用在使用时被移除。

## 4.11 实验

### 实验 1：改进基础字符驱动程序

从 `sample_driver.c` 开始，将其扩展为以下功能：

- 跟踪自加载以来被打开的次数，并在每次打开设备时打印计数器。
- 在打开设备时打印主设备号（major numbers）。

为了练习你的驱动程序，编写一个程序使用标准的 Unix I/O 函数（`read()`、`write()`、`close()`）对节点进行读（和或）写。

使用 `insmod` 加载模块（这等于输入 `cat /proc/modules/`）。

### 实验 2：每次打开的私有数据

修改之前的驱动程序，确保每次打开设备都会分配其自己的数据区域，并在释放时释放。数据不会在多次打开之间持久化。

### 实验 3：寻址与设备末尾

适配之前的一个驱动程序，使其读写条目能够监控设备末尾。

实现一个 `lseek()` 入口点。参阅 `lseek()` 的手册页（man page）以查看如何指定返回值和错误代码。

作为一个额外练习，使用 `POSIX_SEEK` 位使得任何寻址尝试都导致错误。

### 实验 4：动态节点创建 (I)

适配之前的驱动程序以动态分配主设备号。

编写加载和卸载脚本，用以确定分配的主设备号并根据需要移除节点。

### 实验 5：动态节点创建 (II)

适配使用 `udev` 的动态注册驱动程序以动态创建设备节点。

# 第5章 内核配置与编译

![](img/5f0cab84232061dba742ffc69894b1f1_37_0.png)

我们将检查 Linux 内核源码的布局。我们将考虑浏览源码的方法。我们提供编译、安装和更新修改后的内核步骤。我们将考虑 `initrd` 镜像的使用。

| 章节 | 页码 |
| --- | --- |
| 5.1 内核源码的安装与布局 | 53 |
| 5.2 内核浏览器 | 56 |
| 5.3 内核配置文件 | 56 |
| 5.4 编译你自己的内核 | 57 |
| 5.5 initrd 和 initramfs | 60 |
| 5.6 实验 | 63 |

## 5.1 内核源码的安装与布局

Linux 内核源码必须对所有发行版都容易获得。最新和较旧的内核通常都可以下载。（记住 `www.kernel.org` 将为你提供最新内核版本的快速概览。）

所有内核的原始源码始终可以从 http://www.kernel.org 上的内核维护者处获取，或者从分发版处获取，大多数发行版都会对源码进行（可能是下一次）更改。这些更改也可能免费提供。

源码树的确切位置没有强制规定。当针对内核构建外部模块时，它包含了实际源码，或指向源码的符号链接。

为了方便起见，我们获取原始源码位于 `/usr/src/`，并为了显示代码，从真实代码创建一个符号链接。这不应被解释为在普通开发系统上的操作建议。使用 `/usr/src/`（实际位置）我们发现：

### 5.1. 内核源码的安装与布局

这里是最新内核版本的代码源码列表（包含所有子目录）。

| 目录 | 目的 |
| --- | --- |
| arch | i386, i6886, alpha, arm, sparc64, mips, mips64, i386, ppc, a330... 用于启动、同步和进程管理的架构代码。 |
| kernel | 主内核例程：交换、映射、malloc。 |
| init | 内核启动代码：驱动, block, scsi, cdrom... 按类型排序的驱动程序。 |
| sound | 内核低层接口。每个架构特定的驱动程序。 |
| fs | 文件系统。 |
| net | 以太网, ip4, ipv5, ipv6, applets 和网络代码。 |
| security | 安全模型, SELux |
| crypto | 加密算法。 |
| lib | 标准库例程，用于测试。 |
| ipc | 进程间通信代码。 |
| user | 用户交互代码。 |
| scripts | 用于编译内核的各种脚本。 |
| Documentation | 各种文档。 |
| virt | 虚拟化架构。 |
| firmware | 与内核一起的固件。 |
| samples | 用于跟踪、分析和调试的示例内核代码。 |
| tools | 用户空间工具。 |
| include | 系统头文件。 |
