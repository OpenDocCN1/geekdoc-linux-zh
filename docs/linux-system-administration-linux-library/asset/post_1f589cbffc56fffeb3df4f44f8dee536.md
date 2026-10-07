
[content]
# In Sum 297

overall kernel philosophy. If there are only a few security fixes, you can upgrade those packages only, and leave the rest alone. You'll get more comfortable with what requires an upgrade as you progress.

# In Sum

A computer's performance can be influenced by many factors, both hardware and software. If your system isn't performing to your liking, you might try upgrading your hardware, but devoting some time to optimizing your computer may save you the cost of hardware upgrades. Indeed, some hardware upgrades won't do much good unless accompanied by appropriate software tuning. Enabling 32-bit DMA transfers on IDE hard disks is one such case. You can tune your computer's use of the hard disk, of memory, and of the CPU by appropriate configuration options. Some optimizations (particularly for the CPU) require you to recompile software for your system, or at least to locate software compiled with better-than-386 optimizations.

One class of optimizations that's covered in this chapter relates to the placement of file-systems on the hard disk. Chapter 10 extends this topic and covers alternatives to the standard Linux ext2 filesystem, some of which may improve performance, particularly after a system crash or power outage.

![](img/4fb617eb648f87def380ef5d92052d01_324_0.png)

## Filesystems and Disk Management

One of Linux's strengths as an operating system is its support for a wide variety of filesystems. Not only does Linux support its native filesystem, the Second Extended Filesystem (ext2fs or ext2), but it also supports a wide array of files used by other Unix-like OSs, Windows, macOS, and others. This support makes Linux a particularly effective OS in a multi-boot environment, and it can be quite useful for a Linux-only system. You can use Linux's extensive filesystem support to read removable media and hard disks from other computers.

> NOTE The word filesystem has two meanings. As used in this chapter, filesystem means a disk- or network-based data structure for storing files. It also refers to the hierarchy of directories and files on a disk. In this second sense, the filesystem is a logical structure that you can view with a file manager or with Linux commands such as ls. (Chapter 3 discusses filesystems in this second sense.) By contrast, the low-level data structures that constitute a filesystem in its first meaning are largely invisible to a user or system administrator—but its effects are important nonetheless, as illustrated throughout this chapter.

In order to access these filesystems, however, you must understand the tools that Linux uses to make this access possible. Most critically, you must recognize how Linux mounts and unmounts filesystems—that is, how the OS grafts a removable disk or hard disk partition onto its existing directory structure. In addition, you should be familiar with the tools available to help you prepare a filesystem for use and keep it working smoothly.

This chapter begins with an overview of Linux's filesystem capabilities, including the major filesystems it supports. The discussion then moves to practical issues of filesystem handling—how to mount and unmount both hard disk and removable-media filesystems. It concludes with a look at maintaining your filesystems and adding new ones.

# Linux Filesystem Support

Linux filesystem support is excellent, but not perfect. Some filesystems do not work on a default installation of Red Hat Linux (or of other distributions, for that matter). These filesystems require that you use the appropriate drivers, and in all probability, recompile your kernel. Other filesystems work, but their features are limited. Most importantly, many filesystem drivers are available in read-only formats—they can be used to read files from the foreign filesystem, but not to write to them. Still others work in full read/write mode, but their feature sets do not mesh perfectly with Linux's assumptions and requirements. For all these reasons, you must understand the specific filesystems you are using in order to be aware of the limitations and work around them where possible.

# Locating Filesystems

Most Linux filesystems come with the Linux kernel, and Red Hat Linux includes most of these filesystems in its default configuration. Many of these filesystems are available as kernel modules. You can find which filesystem modules are available by typing the command:

```
$ ls /lib/modules/x.y.z/fs
```

In this command, x.y.z is the kernel version number, as of 2.2.16. In response, you'll see a set of filesystem driver modules, as hfs.. These modules are usually named after the filesystems they implement. Some of these drivers are true of modules, however, and not independent filesystems. (This is particularly true of nls_cp*. models, which implement language support by FAT and Juliet filesystems.) Also, be aware that not all filesystems appear in this directory—some are built into the kernel file itself. Most importantly, the filesystem from which Linux boots (ext2fs in most cases) must be built into the kernel.

# Preparing to Use a Standard Filesystem

If a filesystem you want isn't present on your computer, you can check the Linux kernel to see if it's present in the source tree but not compiled for your system. To do so, you must check the filesystems available in the Linux kernel File Systems and Network Filesystems menus (Figure 10.1 shows the kernel File Systems menu). Chapter 8 discusses the kernel configuration menus and kernel configuration options in greater detail.

> NOTE In Linux kernels 2.2.x, filesystems appear in their own menu. In 2.3.x and 2.4.x, network filesystems appear as submenu of the main File Systems 10.1 kernel has been patched to include ReiserFS.

![](img/4fb617eb648f87def380ef5d92052d01_328_0.png)

If you're unsure of what filesystem supports, click the Help button for that to see a brief description. Once you've opened the kernel configuration menu, you can then select the kernel driver as just described, and compile a kernel or kernel modules with the necessary support.

# Unusual Filesystems

A few filesystems don't ship with the regular kernel. Most of these are development filesystems—they're new enough that have yet to be added to the kernel. The most interesting of these filesystems are the journaling filesystems, which are described shortly, in "Journaling Filesystems." (That section includes pointers to these filesystems' homes on the Internet). Journaling filesystems can greatly speed boot times after a crash. If your Linux system operates in an environment with speedy recovery from power outages or system crashes is important, or if you have hard disks larger than 20GB, you may want to investigate these filesystems.

If you're looking for a specific filesystem and can't find it in the kernel, try a search on Deja News (http://www.deja.com/usenet/), or with a search engine as Yahoo! (http://www.yahoo.com) or Google (http://www.google.com). There's a good chance you'll find a lead.

Most substandard filesystems require that you patch your Linux kernel—that is, add files to the kernel source. These patches usually come with instructions for accomplishing this task, you should follow these instructions. You can then select the kernel driver as just described in "Preparing to Use a Standard Filesystem," and compile a kernel or kernel modules with the necessary support.

# Linux Native Filesystems

A native filesystem is one that can be used as the primary filesystem for an OS. Linux can run using nothing but a single native filesystem that, it doesn't need a mix of two or more filesystems. An OS's native filesystems are often designed for a specific OS, although in some cases an OS "inherits" or "adopts" a native filesystem from a predecessor or later. Throughout its history, Linux has inherited and adopted filesystems and has Linux-specific filesystems designed for it. (Chapter 3 details this history for Linux.) This is in contrast to foreign filesystems, which are designed for another OS. As a general rule, foreign filesystems don't mesh well with Linux as native filesystems.

This discussion separates native filesystems into two camps: traditional and journaling. Other categorizations could also be made, but for purposes this one is quite useful. "Traditional" does not insignificant or poorly performing. In early 2001, the most important filesystem for Linux, ext2fs, falls into the traditional category. These filesys
