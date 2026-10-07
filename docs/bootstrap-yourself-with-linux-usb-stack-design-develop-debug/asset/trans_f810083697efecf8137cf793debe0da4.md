

![](img/779a74a6577501a55983f193067274a3_93_0.png)

**图 6.2**
USB VFS 框架的简单自顶向下分解。

该框架为每个连接到主机的 USB 创建目录，并为连接到总线的每个 USB 设备在目录内创建文件。该框架还实现了文件操作，用于访问由 USB VFS 框架创建的文件。框架还包含了实用程序，作为与通知框架和模块初始化的接口。

接下来的章节将探索 Linux USB 设备文件框架中的关键函数和活动序列。Linux USB 设备文件框架提供了接口函数 `usbfs_init` 和 `usbfs_cleanup`。这些接口函数的定义位于 `drivers/usb/core/hcd.h` 中。

```
extern void usbfs_init(void);
extern void usbfs_cleanup(void);
```

`usbfs_init` 从 `uscore` 模块初始化开始启动 VFS 框架的初始化和设置。`usbfs_cleanup` 在模块退出时调用，以清理 VFS 文件和通知处理程序。这些函数作为 `uscore` 的 `drivers/usb/core/inode.c` 文件可用。

## 第 6 章 = 设备文件系统

在初始化期间，框架向 USB 通知注册，以便在系统添加新的 USB 总线和 USB 设备时获取事件。定义为 `/drivers/usb/core/inode.c` 的 `usbfs_nb` 通知块注册了 `usbfs_notify` 回调处理程序，用于收集来自 USB 总线/设备的添加和移除事件。

```
static struct notifier_block usbfs_nb = {
    notifier_call = usbfs_notify,
};
static int usbfs_notify(struct notifier_block *self, unsigned long action, void *dev)
{
    switch (action) {
        case USB_DEVICE_ADD:
            usbfs_add_device(dev);
            break;
        case USB_DEVICE_REMOVE:
            usbfs_remove_device(dev);
            break;
        case USB_BUS_ADD:
            usbfs_add_bus(dev);
            break;
        case USB_BUS_REMOVE:
            usbfs_remove_bus(dev);
            break;
    }
    usbfs_update_special();
    usbfs_conn_disc_event();
    return NOTIFY_OK;
}
```

`usbfs_notify` 接收四个指示 USB 设备和 USB 总线添加及移除的事件。这些事件通过在框架内设置 VFS 对象来触发 USB 文件的创建。

图 6.3 展示了 USB VFS 框架初始化和退出期间的活动序列。当 `uscore` 调用 `usbfs_init` 函数注册到 USB 文件系统和通知回调时，USB VFS 框架开始运行。文件系统的注册触发了超级块（super block）对象的创建。同样，在 `uscore` 模块退出时，会调用 `usbfs_cleanup` 函数，它成功地注销了文件系统和通知回调。

![](img/779a74a6577501a55983f193067274a3_95_0.png)

图 6.3
Linux USB 设备文件系统的初始化和退出序列。

## 第 6 章 = 设备文件系统

USB VFS 框架在 `usbfs` 挂载路径的根目录下创建特殊设备。图 6.4 捕捉了设备文件生命周期的活动。`usbfs` 的其他文件也具有类似的活动set。

`create_special_files` 函数在第一个 USB 总线被添加时创建设备。在创建过程中，会传递访问文件所需的文件操作对象。该文件操作对象被更新为设备文件创建的 inode，并链接到早先创建的超级块。设备文件的文件操作实现在 `drivers/usb/core/devices.c` 中。当用户应用程序读取设备文件时，`read` 系统调用会调用通过 `file_operations` 数据结构注册的 `usb_device_read` 函数。随后，`usb_device_dump` 将信息打印到读取缓冲区并传递给用户应用程序。

接下来的章节将探索如何基于 Linux 设备文件系统创建一个 Linux VFS。

## 创建 Linux USB 文件系统

Linux USB 文件系统（称为 `usbfs`）从用户空间挂载 USB 文件系统。接下来的章节将探索 `usbfs` 是如何创建的。它从定义文件系统类型并向内核注册该文件系统开始。

```
static struct file_system_type us_fs_type = {
    .owner = THIS_MODULE,
    .name = "usbfs",
    .get_sb = usb_get_sb,
    .kill_sb = kill_litter_super,
};
```

文件系统的注册发生在 `usbfs` 函数中，该函数在 `usbcore` 通过 `usb_init` 函数初始化时被调用。

```
int __init usbfs_init(void) {
    int retval;

    retval = register_filesystem(&usb_fs_type);
    if (retval)
```

![](img/779a74a6577501a55983f193067274a3_97_0.png)

**图 6.4**
设备的生命周期。

## 第 6 章 = 设备文件系统

`usbfs_cleanup` 函数在模块退出时调用，以清理 VFS 文件和通知处理程序。这些函数作为 `uscore` 的 `drivers/usb/core/inode.c` 文件可用。

文件系统的注册发生在 `usbfs` 函数中，该函数在 `usbcore` 通过 `usb_init` 函数初始化时被调用。

```
#define USBDEVICE_SUPER_MAGIC 0x9fa2
static int usbfs_fill_super(struct super_block *sb, void *data)
{
  --cut--
  sb->blocksize = PAGE_CACHE_SIZE;
```

```
sb->blocksize_bits = PAGE_CACHE_SHIFT;
sb->s_magic = USBDEVICE_SUPER_MAGIC;
sb->s_op = &ubsfs_ops;
sb->s_time_gran = 1;
inode = usbfs_get_inode(sb, S_IFDIR | 0755, 0);
--cut--
root = d_alloc_root(inode);
--cut--
sb->s_root = root;
--cut--
}
```

该过程的下一步是为根目录创建 inode 数据结构。`usbfs_get_inode(sb, S_IFDIR | 0755, 0)` 函数调用为根目录创建了一个 inode。`S_IFDIR` 表示为目录创建一个 inode 数据结构。`usbfs_get_inode` 使用来自 VFS 框架的目录操作更新 inode，因为 `usbfs` 不需要特殊的目录操作。以下来自 `usbfs_get_inode` 的代码显示了带有目录操作的更新 inode。

```
case S_IFDIR:
inode->i_op = &simple_dir_inode_operations;
inode->i_fop = &simple_dir_operations;
```

一旦你设置了根目录及其操作，超级块就会被成功初始化。下一步是创建文件。`usbfs` 为主机上的每个总线和添加到系统的设备创建文件。它使用通知器链回调为连接到主机的设备和总线创建文件。同时，`usbfs` 会创建一个特殊设备文件，列出连接到主机的 USB 设备的信息。`create_special_files` 函数创建设备文件，并传递处理设备所需的的文件操作 `ubsfs_devices_fops`。

```
static int create_special_files(void)
{
--cut--
```

```
parent = ubsfs_mount->mnt_sb->s_root;
devices_ubsfs_dentry = fs_create_file("devices",
listmode | S_IFREG, parent,
```

