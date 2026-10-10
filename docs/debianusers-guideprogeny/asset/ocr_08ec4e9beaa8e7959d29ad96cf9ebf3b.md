Set the partition or file for swapping. Type: `mkswap PARTITION` or `mkswap FILE`.

Active the partition or file.

To activate swapping temporarily, type: `swapon PARTITION` or `swapon FILE`.

To use a swap partition permanently, add an entry to `/etc/fstab`. You can copy the existing swap file entry. See “Column Settings in `/etc/fstab` (Mounting Filesystems),” page 366.

![](bbox=[0.18, 0.29, 0.85, 0.37])

# Configuring the Boot Loader

Progeny Debian uses the Grand Unified Boot Manager (GRUB). The boot manager is a program that lets you choose which operating system to use when you start your computer.

You can also use a boot manager to run different Linux kernels. In fact, if you recompile the kernel, you can guarantee that your system remains workable by making a copy of your kernel and adding an entry for the copy to the boot manager.

# Understanding the GRUB Naming Conventions

GRUB uses its own naming convention for hard drives and partitions. This convention is different from either the Linux or Windows conventions:

+   * All numbering starts at 0, so that `(hd0)` is the first hard drive.
+   * No distinction is made between IDE and SCSI devices. `(hd0)` could be either type of hard drive.
+   * Primary and extended partitions are numbered from 0 to 3.
+   * LogicalSee “Configuring a Network Connection From the Command Line,” page 387 partitions are numbered from 4.