Nothing has yet been done to the disk. Select **Q** to quit the Slice Editor. You'll now be prompted for what kind of boot manager to install. If this is a secondary disk that you're adding to an already running system, select **None**. Install the FreeBSD Boot Manager (BootMgr) if you will be booting from this disk (if you're prepping this disk to be used in a new machine, for example) or to replace the existing disk in your current system. Otherwise, select **Standard** to do the equivalent of the DOS command `fdisk /MBR`, which removes operating system-specific boot managers (such as Linux's LILO and FreeBSD's BootMgr) from the Master Boot Record and makes it available to other operating systems (for example, if you're reusing the disk to make a new Windows machine).

# **CAUTION**

The Slice Editor has a **Write Changes** option: the **W** command. This should be used before quitting the Slice Editor if, and only if, you are modifying an existing disk setup. If you're installing FreeBSD for the first time, or if you're prepping a new disk for installation, just quit the Slice Editor and move on directly to the Disk Label Editor. The **W** option reiterates this warning if you use it.

# # Creating the Disk Labels

The disk is now sliced and has been made FreeBSD friendly, but it still isn't formatted—you can't use it in your system yet. You do that next, in the Disk Label Editor.

Still in `sysinstall`, select **Label** (the Disk Label Editor). You'll again be asked to select from the list of installed disks; use the **spacebar** to select **ad1**. You're presented with the Disk Label Editor screen, a visual interface to the command-line `disklabel` command. This is where you assign the BSD partitions and format the disk.

# **CAUTION**

FreeBSD's Disk Label Editor doesn't allow you to resize existing partitions. A partition can't be modified without reformatting it and losing its data, so consider carefully what your partitions will be used for before you commit your changes!

# ## Creating a Complete FreeBSD Partition Layout

If you're just adding a new disk to the system, skip ahead to the “Adding a New Disk” section. This section of the chapter, however, demonstrates how to use the DiskLabel Editor to assign BSD partitions and mount points for a complete FreeBSD system, including a root partition, `/usr` and `/var` partitions, and a swap partition. This is useful if you're going to be installing FreeBSD onto the new disk (for example if you're replacing your current disk with a larger one).