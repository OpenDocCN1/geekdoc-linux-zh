# # Chapter 6: Filesystems and Disk Management

# ## Overview

One of Linux’s strengths as an operating system is its support for a wide variety of filesystems. Not only does Linux support its own native filesystem, the Second Extended Filesystem (*ext2fs* or *ext2*), but it also supports a wide array of filesystems used by other Unix-like OSs, Windows, MacOS, and others. This support makes Linux a particularly effective OS in a multi-boot environment, and it can also be quite useful for a Linux-only system. You can use Linux’s extensive filesystem support to read removable media and even hard disks from other computers.

**Note**  The word *filesystem* has two meanings. As used in this chapter, *filesystem* means a disk- or network-based data structure used for storing files. It also refers to the hierarchy of directories and files on a disk. In this second sense, the filesystem is a logical structure that you can view with a file manager or with Linux commands such as ls. (Chapter 7 discusses filesystems in this second sense.) By contrast, the low-level data structures that constitute a filesystem in its first meaning are largely invisible to you as a user or system administrator—but their effects are important nonetheless, as illustrated throughout this chapter.

In order to access these filesystems, you must understand the tools that Linux uses to make this access possible. Most critically, you must recognize how Linux *mounts* and *unmounts* filesystems—that is, how the OS grafts a removable disk or hard disk partition onto its existing directory structure. In addition, you should be familiar with the tools available to help you prepare a filesystem for use and keep it working smoothly.

This chapter begins with an overview of Linux’s filesystem capabilities, including the major filesystems it supports. The discussion then moves to practical issues of filesystem handling—how to mount and unmount both hard disk and removable-media filesystems. It concludes with a look at maintaining your filesystems and adding new ones.

# ## Linux Filesystem Support

Linux filesystem support is excellent, but not perfect. Most distributions lack support for at least some filesystems in their default installations. To use these filesystems, you must locate the appropriate drivers and, in all probability, recompile your kernel. Other filesystems work, but their features are limited. Most importantly, many filesystem drivers are available in read-only forms—they can be used to read files from the foreign filesystem, but not write to the filesystem. Still others work in full read/write mode, but their feature sets don’t mesh perfectly with Linux’s assumptions and requirements. For all these reasons, you must understand the specific filesystems you’re using in order to be aware of the limitations and work around them where possible.

# ## Locating Filesystems

Most Linux filesystems come with the Linux kernel, and Red Hat Linux includes most of these filesystems in its default configuration. Many of these filesystems are available as kernel modules. You can find out which filesystem modules are available by typing the following command:

```
$ ls /lib/modules/x.y.z/kernel/fs
```