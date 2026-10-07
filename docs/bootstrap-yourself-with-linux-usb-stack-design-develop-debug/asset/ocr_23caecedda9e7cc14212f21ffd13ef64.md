# CHAPTER 6

# DEVICE FILE SYSTEM

In This Chapter

+   - Bootstrap Essentials: Virtual File System
- Linux USB Device File System
- Creating the Linux USB File System

The Linux Virtual File System (VFS) is a thin kernel framework that provides a file system interface to the user space applications, allowing them to access the kernel internals. The Linux kernel supports different file system formats, such as Network File System (NFS) and Extended File System (EXT2, EXT3, and EXT4). The VFS provides an abstraction between different file system formats, creating the necessary transparency for applications to access the file information. Figure 6.1 illustrates a simplistic view of VFS inside Linux.

Linux developers are encouraged to create VFS files for the device instead of populating Linux kernel system files to share device details. The Linux USB subsystem also creates the VFS file *usbfs*, which produces files for universal serial bus (USB) and USB devices and allows user space applications to interact with connected USB devices.

This chapter initially explores the essential data structures and infrastructure for developing VFS. Subsequently, it explores the design and sequence of activity in the *usbfs* VFS implementation. This chapter concludes by implementing a simple VFS file for the Linux USB subsystem.