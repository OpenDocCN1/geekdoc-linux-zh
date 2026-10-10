this context, called a *mount point*). If this directory does not exist in the final root file system, the *initrd* image is simply discarded.

If the kernel command line contains a `root=` parameter specifying a ramdisk (`root=/dev/ram0`, for example), the previously described *initrd* behavior changes in two important ways. First, the processing of the *linuxrc* executable is skipped. Second, no attempt is made to mount another file system as root. This means that you can have a Linux system with *initrd* as the only root file system. This is useful for minimal system configurations in which the only root file system is the ramdisk. Placing `/dev/ram0` on the kernel command line allows the full system initialization to complete with the *initrd* as the final root file system.

# **6.4.6 Building an initrd Image**

Constructing a suitable root file system image is one of the more challenging aspects of embedded systems. Creating a proper *initrd* image is even more challenging because it needs to be small and specialized. For this section, we examine *initrd* requirements and file system contents.

Listing 6-12 was produced by running the `tree` utility on our example *initrd* image from this chapter.

# **Listing 6-12**

# **Contents of Example initrd**

```
```text
|-- bin
|   |-- busybox
|   |-- echo -> busybox
|   |-- mount -> busybox
`-- sh -> busybox
|-- dev
|   |-- console
|   |-- ram0
`-- ttyS0
|-- etc
|-- linuxrc
`-- proc
```
```

4 directories, 8 files