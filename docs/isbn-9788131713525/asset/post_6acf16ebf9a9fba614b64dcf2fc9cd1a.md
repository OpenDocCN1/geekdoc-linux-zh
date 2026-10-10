
Take special note of one feature of the U-Boot bootloader. It fully supports loading kernel and ramdisk images over an Ethernet connection. This is a very useful development configuration. You can get a kernel and ramdisk image onto your board in other ways as well. You can flash them into your Flash memory using a hardware-based flash programming tool, or you can use a serial port and download the kernel and file system images via RS-232. However, because these images are typically large (a kernel can be about a megabyte, and a ramdisk can be tens of megabytes), you will save a significant amount of engineering time if you invest in this Ethernet-based tftp download method. Whatever bootloader you choose, make sure it supports network download of development images.

## 6.4.4 initrd Magic: linuxrc

When the kernel boots, it detects the presence of the *initrd* image, and copies the compressed binary file from the specified physical location in RAM into a proper kernel ramdisk and mounts it as the root file system. The magic of the *initrd* comes from the contents of a special file within the *initrd* image. When the kernel mounts the initial ramdisk, it looks for a specific file called *linuxrc*. It treats this file as a script file and proceeds to execute the commands contained therein. This mechanism enables the system designer to specify the behavior of *initrd*. Listing 6-11 contains a sample *linuxrc* file.

### Listing 6-11: Example linuxrc File

```
#!/bin/sh

echo 'Greetings: this is linuxrc from Initial Ramdisk'
echo 'Mounting /proc filesystem'
mount -t proc /proc /proc

busybox sh
```

In practice, this file would contain directives required before we mount the real root file system. One example might be to load CompactFlash drivers to obtain a real root file system from a CompactFlash device. For purposes of this example, we simply spawn a busybox shell and halt the boot process for examination. You can see the # command prompt from Listing 6-10 resulting from this busybox shell. If one were to type the *exit* command here, the kernel would continue its boot process until complete.

After the kernel copies the ramdisk from physical memory into a kernel ramdisk, it returns this physical memory back to the available memory pool. You can think of this as transferring the initrd image from physical memory at the hard-coded address into the kernel's own virtual memory (in the form of a kernel ramdisk device).

One last comment about Listing 6-11: The mount command in which the /proc file system is mounted seems redundant in its use of the word proc. This command would also work:

```
mount -t proc none /proc
```

Notice that the device field of the mount command has been changed to none. The mount command ignores the device field because no physical device is associated with the proc file system. The -t proc is enough to instruct mount to mount the /proc file system on the /proc mount point. I use the former invocation as a mental reminder that we are actually mounting the kernel pseudo device (the /proc file system) on /proc. The mount command ignores this argument. Use the method that you prefer.

## 6.4.5 The initrd Plumbing

As part of the Linux boot process, the kernel must locate and mount a root file system. Late in the boot process, the kernel decides what and where to mount in a function called `prepare_namespace()`. If initrd support is enabled in the kernel, as illustrated in Figure 6-1, and the kernel command line is so configured, the kernel decompresses the compressed initrd image from physical memory and eventually copies the contents of this file into a ramdisk device (/dev/ram). At this point, we have a proper file system on a kernel ramdisk. After the file system has been read into the ramdisk, the kernel effectively mounts this ramdisk device as its root file system. Finally, the kernel spawns a kernel thread to execute the `linuxrc` file on the initrd image.[1]

When the `linuxrc` script has completed execution, the kernel unmounts the initrd and proceeds with the final stages of system boot. If the real root device has a directory called /initrd, Linux mounts the initrd file system on this path (in this context, called a *mount point*). If this directory does not exist in the final root file system, the *initrd* image is simply discarded.

If the kernel command line contains a `root=` parameter specifying a ramdisk (`root=/dev/ram0`, for example), the previously described *initrd* behavior changes in two important ways. First, the processing of the *linuxrc* executable is skipped. Second, no attempt is made to mount another file system as root. This means that you can have a Linux system with *initrd* as the only root file system. This is useful for minimal system configurations in which the only root file system is the ramdisk. Placing `/dev/ram0` on the kernel command line allows the full system initialization to complete with the *initrd* as the final root file system.

[1] Out of necessity (space), this is a very simplified description of the sequence of events. The actual mechanism is similar in concept, but several significant details are omitted for clarity. You are encouraged to consult the kernel source code for more details. See .../init/main.c and .../init/do_mounts.c.

## 6.4.6 Building an initrd Image

Constructing a suitable root file system image is one of the more challenging aspects of embedded systems. Creating a proper *initrd* image is even more challenging because it needs to be small and specialized. For this section, we examine *initrd* requirements and file system contents.

Listing 6-12 was produced by running the `tree` utility on our example *initrd* image from this chapter.

### Listing 6-12: Contents of Example initrd

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

4 directories, 8 files

As you can see, it is very small indeed; it takes up a little more than 500KB in uncompressed form. Since it is based on busybox, it has many capabilities. Because busybox is statically linked, it has no dependencies on any system libraries. You will learn more about busybox in Chapter 11.

## 6.5 Using initramfs

initramfs is a relatively new (Linux 2.6) mechanism for executing early user space programs. It is conceptually similar to initrd, as described in the previous section. Its purpose is also similar: to enable loading of drivers that might be required before mounting the real root file system. However, it differs in significant ways from the initrd mechanism.

The technical implementation details differ significantly between initrd and initramfs. For example, initramfs is loaded before the call to `do_basic_setup()`, which provides a mechanism for loading firmware for devices before its driver has been loaded. For more details, the Linux kernel documentation for this subsystem is relatively up-to-date. See .../Documentation/filesystems/ramfs-rootfs-initramfs.txt.[2]

[2] `do_basic_setup()` is called from .../init/main.c and calls `do_initcalls()`. This causes driver module initialization routines to be called. This was described in detail in Chapter 5 and shown in Listing 5-10.

From a practical perspective, initramfs is much easier to use. initramfs is a cpio archive, whereas initrd is a gzipped file system image. This simple difference contributes to the ease of use of initramfs. It is integrated into the Linux kernel source tree and is built automatically when you build the kernel image. Making changes to it is far easier than building and loading a new initrd image. Listing 6-13 shows the contents of the Linux kernel .../usr directory, where the initramfs image is built. The contents of Listing 6-13 are shown after a kernel has been built.

## 6.6 Shutdown

### Listing 6-13: Kernel initramfs Build Directory

```
$ ls -l
total 56
-rw-rw-r-- 1 chris chris 834 Mar 25 11:13 built-in.o
-rw-rwx--x 1 chris chris 11512 Mar 25 11:13 gen_init_cpio
-rw-rw-r-- 1 chris chris 10587 Oct 27 2005 gen_init_cpio.c
-rw-rw-r-- 1 chris chris 512 Mar 25 11:13 initramfs_data.cpio
-rw-rw-r-- 1 chris chris 133 Mar 25 11:13 initramfs_data.cpio.gz
-rw-rw-r-- 1 chris chris 786 Mar 25 11:13 initramfs_data.o
-rw-rw-r-- 1 chris chris 1024 Oct 27 2005 initramfs_data.S
-rw-rw-r-- 1 chris chris 113 Mar 25 11:13 initramfs_list
-rw-rw-r-- 1 chris chris 1619 Oct 27 2005 Kconfig
-rw-rw-r-- 1 chris chris 2048 Oct 27 2005 Makefile
```

The file `initramfs_list` contains a list of files that will be included in the `initramfs` archive. The default for recent Linux kernels looks like this:

```
dir /dev 0755 0 0
mod /dev/console 0600 0 0 c 5 1
dir /root 0700 0 0
```

This produces a small default directory structure containing the `/root` and `/dev` top-level directories, as well as a single device node representing the console. Add to this file to build your own initramfs. You can also specify a source for your initramfs files via the kernel-configuration facility. Enable **INITRAMFS_SOURCE** in your kernel configuration and point it to a location on your development workstation; the kernel build system will use those files as the source for your initramfs image.

The final output of this build directory is the `initramfs_data.cpio.gz` file. This is a compressed archive containing the files you specified (either through the `initramfs_list` or via the **INITRAMFS_SOURCE** kernel-configuration option). This archive is linked into the final kernel image. This is another advantage of initramfs over initrd: There is no need to load a separate initrd image at boot time, as is the case with initrd.

Orderly shutdown of an embedded system is often overlooked in a design. Improper shutdown can affect startup times and can even corrupt certain file system types. One of the more common complaints using the EXT2 file system (the
