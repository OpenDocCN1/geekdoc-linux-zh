# Chapter 7: Managing Partitions

2. Use the ARROW keys to scroll down to the **Configure** option and press ENTER.
The FreeBSD Configuration Menu opens, as shown next.

![](bbox=[0.15, 0.16, 0.88, 0.55])

3. The **Fdisk** option enables you to edit the x86 partition table, much as you can with the *fdisk* utilities in other OSs. If you use this option, you'll be automatically moved to the next option when you finish.

4. The **Label** option enables you to edit the FreeBSD partition table (also known as the *disk label*) within the FreeBSD slice. Editing the disk label enables you to set up FreeBSD partitions.

The details of the last two steps are described in Chapter 2, so consult it when you create new partitions using *sysinstall*. When you finish using the FreeBSD Disklabel Editor tool, use the *w* option to save your changes. At this point, *sysinstall* runs the *newfs* utility, which creates filesystems on your new FreeBSD partitions. Thus, *sysinstall* can control the entire partition-creation process—creating a FreeBSD slice, creating BSD partitions within that slice, and creating filesystems on the partitions.

# Using Command-Line Tools

The *sysinstall* utility is a convenient way to create partitions, but sometimes you need to dig into the underlying tools that it uses. There are three of these, as far as partition creation is concerned: *fdisk*, *disklabel*, and *newfs*. Variants of this last one create filesystems other than FFS. These tools control the creation of the x86 primary partition

BASIC SYSTEM
ADMINISTRATION