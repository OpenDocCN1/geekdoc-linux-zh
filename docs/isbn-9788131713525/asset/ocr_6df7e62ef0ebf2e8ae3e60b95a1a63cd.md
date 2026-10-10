After the kernel copies the ramdisk from physical memory into a kernel ramdisk, it returns this physical memory back to the available memory pool. You can think of this as transferring the initrd image from physical memory at the hard-coded address into the kernel's own virtual memory (in the form of a kernel ramdisk device).

One last comment about Listing 6-11: The mount command in which the /proc file system is mounted seems redundant in its use of the word proc. This command would also work:

```
mount -t proc none /proc
```

Notice that the device field of the mount command has been changed to none. The mount command ignores the device field because no physical device is associated with the proc file system. The -t proc is enough to instruct mount to mount the /proc file system on the /proc mount point. I use the former invocation as a mental reminder that we are actually mounting the kernel pseudo device (the /proc file system) on /proc. The mount command ignores this argument. Use the method that you prefer.

# ## 6.4.5 The initrd Plumbing

As part of the Linux boot process, the kernel must locate and mount a root file system. Late in the boot process, the kernel decides what and where to mount in a function called prepare_namespace(). If initrd support is enabled in the kernel, as illustrated in Figure 6-1, and the kernel command line is so configured, the kernel decompresses the compressed initrd image from physical memory and eventually copies the contents of this file into a ramdisk device (/dev/ram). At this point, we have a proper file system on a kernel ramdisk. After the file system has been read into the ramdisk, the kernel effectively mounts this ramdisk device as its root file system. Finally, the kernel spawns a kernel thread to execute the linuxrc file on the initrd image.8

When the linuxrc script has completed execution, the kernel unmounts the initrd and proceeds with the final stages of system boot. If the real root device has a directory called /initrd, Linux mounts the initrd file system on this path (in

> 8 Out of necessity (space), this is a very simplified description of the sequence of events. The actual mechanism is similar in concept, but several significant details are omitted for clarity. You are encouraged to consult the kernel source code for more details. See .../init/main.c and .../init/do_mounts.c.