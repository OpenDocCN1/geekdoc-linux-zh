10. You run Linux's fdisk and modify your partition layout. Before exiting the program, you realize that you've been working on the wrong disk. What can you do to correct this problem?

+   A. Nothing; the damage is done, so you'll have to recover data from a backup.

+   B. Type w to edit fdisk without saving changes to disk.

+   C. Type q to edit fdisk without saving changes to disk.

+   D. Type u to undo the operations you've made in error.

+   E. Type t to undo all changes and return to the original disk state.

11. What does the following command accomplish?

```
# mkfs -t ext2 /dev/sda4
```

+   A. It sets the partition type code for /dev/sda4 to ext2.

+   B. It converts a FAT partition into an ext2fs partition without damaging the partition's\ preexisting files.

+   C. Nothing; the -t option is not valid, and it causes mkfs to abort its operation.

+   D. It converts an ext2 filesystem to an ext4 filesystem.

+   E. It creates a new ext2 filesystem on /dev/sda4, overwriting any existing filesystem and data.

12. Which of the following summarizes the differences between DOS's FDISK and Linux's fdisk?

+   A. Linux's fdisk is a simple clone of DOS's FDISK but written to work from Linux rather than from DOS or Windows.

+   B. The two are completely independent programs that accomplish similar goals, although Linux's fdisk is more flexible.

+   C. DOS's FDISK uses GUI controls, Linux's fdisk uses a command-line interface, but they have similar functionality.

+   D. Despite their similar names, they are completely different tools—DOS's FDISK handles disk partitioning, whereas Linux's fdisk formats floppy disks.

+   E. DOS's FDISK manages GPT disks whereas Linux's fdisk manages MBR disks.

13. What mount point should you associate with swap partitions?

+   A. /

+   B. /swap

+   C. /boot

+   D. /mem

+   E. None of the above