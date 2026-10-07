
![](img/779a74a6577501a55983f193067274a3_93_0.png)

**Figure 6.2**
A simple top-down breakdown of the USB VFS framework.

The framework creates a directory for each USB that's connected to the host and files inside the directory for each USB device connected to the bus. The framework also implements file operations to access the files created by the USB VFS framework. The framework includes utility routines that act as interfaces with the notification framework and module initialization.

The following section explores key functions and the sequence of activity in the Linux USB device file framework. The Linux USB device file framework provides interface functions `usbfs_init` and `usbfs_cleanup`. These interface function definitions are available in drivers/usb/core/hcd.h.

```
extern void usbfs_init(void);
extern void usbfs_cleanup(void);
```

The `usbfs_init` starts initialization and setup of the VFS framework from the `uscore` module initialization. The `usbfs_cleanup` is called when the module exits to clean up the VFS files and notification handlers. These functions are available as part of `uscore`: drivers/usb/core/inode.c file.

## Chapter 6 = Device File System

During initialization, the framework registers with the USB notification to get events when new USB bus and USB devices are added to the system. The `usbfs_nb` notifier block defined as `/drivers/usb/core/inode.c` registers the `usbfs_notify` callback handler to collect addition and removal events from the USB bus/device.

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

The `usbfs_notify` receives four events that indicate the addition and removal of USB devices and USB bus. These events trigger the creation of USB files by setting up the VFS objects within the framework.

Figure 6.3 illustrates the sequence of activities during initialization and exit of the USB VFS framework. The USB VFS framework starts when the `uscore` calls upon the `usbfs_init` function registers to the USB file system and notifier callback. The registration to the file system triggers creation of the super block objects. Similarly, during exit of the module `uscore`, the `usbfs_cleanup` function is called, which successfully unregisters the file system and the notifier callback.

![](img/779a74a6577501a55983f193067274a3_95_0.png)

Figure 6.3
Initialization and exit sequence of Linux USB device file system.

## Chapter 6 = Device File System

The USB VFS framework creates a special devices in the root directory of the `usbfs` mount path. Figure 6.4 captures the set of activities the devices file life cycle. Other files of `usbfs` have a similar set of activities.

The `create_special_files` function creates the devices when the first USB bus is added. During creation, the file operation object that's required to access the file is passed. This file operation object is updated to the inode created for the devices file and linked to the super block created earlier. The file operations of the devices file are implemented in the drivers/usb/core/devices.c. When a user application reads the devices file, the read system call invokes the `usb_device_read` function registered through the `file_operations` data structure. Subsequently, the `usb_device_dump` prints to the read buffer and passes the information to the user application.

The subsequent section explores how to create a Linux VFS based on the Linux device file system.

## CREATING THE LINUX USB FILE SYSTEM

The Linux USB file system, referred to as the `usbfs`, mounts the USB file system from the user space. The following section explores how `usbfs` is created. It starts by defining the file system type and registering the file system with the kernel.

```
static struct file_system_type us_fs_type = {
    .owner = THIS_MODULE,
    .name = "usbfs",
    .get_sb = usb_get_sb,
    .kill_sb = kill_litter_super,
};
```

The registration of the file system occurs as part of the `usbfs` function, which is called when the `usbcore` is initialized through the `usb_init` function.

```
int __init usbfs_init(void) {
    int retval;

    retval = register_filesystem(&usb_fs_type);
    if (retval)
```

![](img/779a74a6577501a55983f193067274a3_97_0.png)

**Figure 6.4**
The life cycle of the devices.

## Chapter 6 = Device File System

The `usbfs_cleanup` function is called when the module exits to clean up the VFS files and notification handlers. These functions are available as part of `uscore`: drivers/usb/core/inode.c file.

The registration of the file system occurs as part of the `usbfs` function, which is called when the `usbcore` is initialized through the `usb_init` function.

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

The next step in the process is creating the inode data structure for the root directory. `usbfs_get_inode(sb, S_IFDIR | 0755, 0)` function call creates an inode for the root directory. The `S_IFDIR` indicates creating an inode data structure for a directory. `usbfs_get_inode` updates the inode with directory operations that are available from the VFS framework because the `usbfs` does not require a special directory operation. The following code from `usbfs_get_inode` shows the updating inode with directory operations.

```
case S_IFDIR:
inode->i_op = &simple_dir_inode_operations;
inode->i_fop = &simple_dir_operations;
```

Once you've set the root directory and its operations, the super block is successfully initialized. The next step is creating the files. The `usbfs` creates files for each bus in the host and devices that are added to the system. It uses notifier chain callbacks to create files for the devices and buses that are connected to the host. Along with these, the `usbfs` creates a special devices file that lists information of the USB devices connected to the host. The `create_special_files` function creates the devices file and passes on the file operations `ubsfs_devices_fops` required to handle the devices.

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
