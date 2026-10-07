> WARNING Linux locks most removable devices, such as CD-ROM and Zip drives, so that you can't eject the disk while it's mounted. When you unmount the disk, the Eject button will work again. Floppy disk drives on x86 computers, however, cannot be locked. It's therefore possible to eject a floppy disk while it's still mounted. Because Linux caches writes to its filesystems, this mistake can cause serious filesystem corruption. Be very careful to mount a floppy disk before ejecting it.

# # Removable Media

Linux's model of the disk world makes little distinction between hard disks and removable disks. You use the same mount and unmount commands to access both types of device, and you can use similar /etc/fstab entries for both types of media. Nonetheless, there are a few caveats and special features that apply to removable media devices only.

# # Accessing Floppy Disks

The most important caveat concerning floppy disks is about ejecting them, as noted in the preceding Warning. Beyond this, you can access floppy disks as if they were very small hard disk partitions. The usual device file for accessing floppies is /dev/fd0. If your system has two floppy drives, the second is accessible as /dev/fd1. There are also a number of specialized device access files, such as /dev/fd0H1440, which provide forced access to a disk of a specific capacity, such as 144KB for /dev/fd0H1440. In normal operation, /dev/fd0 can be used to access any disks of any capacity.

If you're presented with an unformatted floppy disk, you must format it using Format. In Linux, by contrast, you perform two actions. First, you do a low-level format using the fdformat command, as in **fdformat /dev/fd0**. (It's here that the capacity-specific device files can be the most useful, because they can force a format at a specified capacity). Second, you create a filesystem on the disk, as described in "Creating a Filesystem" later in this chapter.

Most filesystems that use on hard disks can be used on floppy disks, with a few exceptions. Most notably, some journaled filesystems require files larger than floppies can hold. You can use Linux's ext2fs on floppy disks, but ext2fs has enough overhead that it's not the best choice. The Minix filesystem is popular on floppy disks because it includes support for Linux permissions and ownership, and consumes less overhead than ext2fs. FAT filesystems, too, are popular on for transfer between Linux systems. The drawback to FAT is that you lose Linux ownership and permissions unless you also archive files into a tar or similar file.

![](bbox=[0.238, 0.856, 0.762, 0.933])