# Chapter 6 = Device File System

```
NULL, &ubsfs_devices_fops,
listuid, listgid;
```

```
--cut--
}
nconst struct file_operations ubsfs_devices_fops = {
    llseek = usb_device_lseek,
    read = usb_device_read,
    poll = usb_device_poll,
};
```

After the successful creation of files, you need to define the file operations to provide access to the files. The drivers/usb/core/devices.c file implements the file operation callbacks required for the devices file.

The Linux device file is read only. The read callback dumps information from the file to the user space. You can read Chapter 16, "USB Virtual File Systems", to learn more about the devices’s contents and how to use the information in the file.

# SUMMARY

The Linux device drivers use the Linux kernel's VFS infrastructure to extend control of the devices to the user space. The Linux USB subsystem VFS files export information about the devices and allow you to develop an application from the user space. The next chapter explores the USB power management framework of the Linux host subsystem along with its usage.

# MORE READING

This chapter briefly covered the Linux VFS. You can read more about the Linux VFS framework in the Documentation/filesystems/vfs.txt of the kernel packages. Also, you can read Chapter 16 to learn how to use the ubsfs files. Furthermore, Documentation/usb/proc_usb_info.txt explains how to use the USB file system in user space.