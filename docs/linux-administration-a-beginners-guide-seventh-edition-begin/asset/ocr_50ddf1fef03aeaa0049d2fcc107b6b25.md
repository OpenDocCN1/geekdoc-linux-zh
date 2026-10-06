# 270 Linux Administration: A Beginner's Guide

Most operating systems offer a mechanism by which the insides of the OS can be probed and operational parameters can be set when needed. In Linux, this mechanism is provided by the so-called application programming interface (API) file systems (virtual or pseudo-file systems). Unlike the other file systems (ext4, Btrfs, XFS, and so on) that we discussed in Chapter 7, virtual file systems are not backed by actual physical storage (such as hard disks). The API file systems are typically not listed explicitly in the system'setc/stab configuration file, though you will still find them in the output of the mount command or find command.

The proc file system is a popular virtual file system on Linux-based OSs. The proc directory is the mount point for the proc file system, and the two terms (proc vs. proc) are used interchangeably.

Other operating systems make use of virtual file systems in different forms and to varying degrees. For example, Microsoft Windows systems make use of the Registry, which allows manipulation of system runtime parameters to some degree. Solaris OS also make use of the proc file system and can be manipulated through the use of ndd.

In this chapter, we discuss the proc file system and how it works under Linux. We'll step through some overviews and study some entries in /proc, and then we'll demonstrate some common administrative tasks using /proc. We'll end with a brief mention of the SysFS, tmpfs, and cgroup virtual file systems.

# # What's Inside the /proc Directory?

Because the Linux kernel is a key component, it's important that there be a method for exchanging information with the kernel. Traditionally, this is done through system calls—special functions written for programmers to use in requesting the kernel to perform functions on their behavior. In the context of system administration, however, system calls make a developer needs to write a tool for us to use (unless, of course writing your own). When you need a simple tool to extract or to some statistics from the kernel, writing a custom tool from scratch for this purpose might be an overkill.

To improve and enhance communication between users and the kernel, the proc file system was created. The entire file system is especially interesting because it doesn't really exist on disk anywhere; it's purely an abstraction of kernel information. All of the files in the directory correspond either to a function in the kernel or to a set of variables in the kernel.

> NOTE The fact that proc is abstract doesn't mean it isn't a file system. It does mean that a special file system had to be developed to treat proc differently from normal disk-based file systems.