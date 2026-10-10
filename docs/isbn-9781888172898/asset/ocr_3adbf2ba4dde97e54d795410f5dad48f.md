# ## 3.6 Installing

# ### 3.6.1 Booting the Kernel Floppy

To boot the Linux/Alpha kernel from the diskette you made above, use MILO. See Appendix D, *Alpha Miniloader Hownto*, Section D.5 for detailed information about how to load MILO from your MILO floppy. Boot to the MILO> prompt, insert your kernel floppy in the first floppy drive, and give MILO the following command:

```
boot fd0:vmlinuz.gz root=/dev/fd0 load_ramdisk=1 prompt_ramdisk=1
```

MILO reads the Linux kernel from your boot disk and runs it.

If you are using the SRM console to load the kernel instead of MILO, you need to give the following arguments to the kernel:

```
load_ramdisk=1 prompt_ramdisk=1
```

# ### 3.6.2 Starting the Install

After the kernel boots, it prompts for a ramdisk. Insert the ramdisk floppy into the floppy drive and press Enter.

# ### 3.6.3 Issues Specific to Linux/Alpha

# **Disk Partitioning**

Red Hat Linux/Alpha supports two varieties of hard drive partitioning:

+   - **Standard fdisk-style partitioning:** this has the usual oddities (such as extended partitions) and is done in the same way as on Intel platforms (using Linux fdisk). This is the partitioning style you must use if you are using the ARC console.

+   - **BSD-style disk-labelling:** It is normal to make the first partition on a disk-labelled hard drive the swap partition. We don't recommend using BSD disk-labelling unless it is absolutely necessary.