# RAM Disks

RAM disks are block devices that store their data in RAM rather than on a disk. This means they are very fast; nevertheless, RAM disks are rarely used with Linux because Linux has a very good disk-caching scheme, which provides most of the speed benefit of a RAM disk but not the fixed cost in memory.

The most common use for RAM disks is to serve as a root filesystem while Linux is being installed. A compressed filesystem image is loaded into a RAM disk, and the installation process is run from this disk. The RAM disk’s filesystem can be larger than a single diskette because the image is compressed on the diskette.

Although RAM disks are useful with operating systems lacking effective disk buffering, they offer little performance advantage under Linux. If you want to try a RAM disk, they work just like any other block device. For example, to mount a RAM disk as /tmp, you add this line to /etc/fstab:

```
/dev/ram  /tmp  ext2  defaults  0  0
```

Then you create and mount an ext filesystem with the following:

```
/sbin/mkfs -t ext2 /dev/ram
mount /tmp
```

Any performance benefits from doing this are hard to find, but you might find that this helps in unusual circumstances.

The principal advantage of RAM disks is that they provide great flexibility in the boot process. Although it is possible to recompile a kernel including support for your hardware, it makes the initial installation process difficult. Historically, programmers worked around this problem by providing dozens of different installation boot disks, each with support for one or two items of boot hardware (SCSI cards and CD-ROM drives, for example).

A simpler solution is to exploit loadable kernel modules. Instead of having separate boot disks for each type of hardware, all containing different kernels, it is simple to provide just one boot disk containing a modular kernel and the module utilities themselves.

A compressed filesystem is loaded from the diskette into a RAM disk by the kernel loader, LILO, at the same time the kernel is loaded. The kernel mounts this filesystem and runs a program (/linuxrc) from it. This program then mounts the “real” root filesystem and exits, enabling the kernel to remount the real root filesystem on /. This system is convenient to set up, and the process of creating initial RAM disks has been automated by Red Hat Software (see the manual page for mkinitrd). Red Hat Linux systems whose root filesystem is on a SCSI device have a modular kernel and boot by this method.