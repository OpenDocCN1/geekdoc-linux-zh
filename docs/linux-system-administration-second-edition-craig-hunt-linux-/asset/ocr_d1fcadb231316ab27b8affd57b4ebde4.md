unmount a floppy disk before ejecting it.

# ## Using Removable Media

Linux's model of the disk world makes little distinction between hard disks and removable disks. You use the same mount and umount commands to access both types of devices, and you can create similar /etc/fstab entries for both types of media. Nonetheless, there are a few caveats and special features that apply to removable media only.

# ### Accessing Floppy Disks

The most important caveat concerning floppy disks is about accidentally ejecting them, as noted in the preceding Warning. Beyond this, you can access floppy disks as if they were very small hard disk partitions. The usual device file for accessing floppies is /dev/fd0. If your system has two floppy drives, the second is accessible as /dev/fd1. There are also a number of specialized device access files, such as /dev/fd0H1440, which provide forced access to a disk of a specific capacity, such as 1440KB for /dev/fd0H1440. (In normal operation, you can use /dev/fd0 to access disks of any capacity.)

If you're presented with an unformatted floppy disk, you must format it. In DOS or Windows, this procedure is handled with a single command, FORMAT. In Linux, by contrast, you perform two actions. First, you do a low-level format using the fdformat command, as in fdformat /dev/fd0. (It's here that the capacity-specific device files can be most useful, because they can force a format at a specified capacity.) Second, you create a filesystem on the disk, as described in "Creating a Filesystem" later in this chapter.

Most filesystems that you use on hard disks can be used on floppy disks, with a few exceptions. Most notably, some journalling filesystems require journal files larger than floppies can hold. You can use Linux's ext2fs on floppy disks, but ext2fs has enough overhead that it's not the best choice. The Minix filesystem is popular on floppy disks because it includes support for Linux permissions and ownership, and it consumes less overhead than ext2fs. FAT filesystems, too, are popular on floppies, even for transfer between Linux systems. The drawback to FAT is that you lose Linux ownership and permissions unless you also archive files into a tar or similar carrier file.

# **Disk Access without a Filesystem**

It's possible to access a floppy disk without using a filesystem *per se*. This is commonly done by writing a tar file directly to a floppy disk. Suppose you want to transfer a directory, somedir, between systems. You can do so by issuing the following tar command on the source system:

```
`$ tar -cvf /dev/fd0 somedir`
```

This command copies the contents of somedir to a tar file on the floppy disk. You can reverse the process on the target system by issuing this command:

```
`$ tar -xvf /dev/fd0`
```

Of course, you can also transfer tar files in a similar way by mounting a disk with a filesystem and then using an appropriate tar file on the disk (such as /mnt/floppy/somedir.tar) rather than the device file (/dev/fd0). Why use direct access, then? It's most useful when transferring files between versions of Unix that don't share an appropriate common filesystem. You can be sure that a tar file written without a filesystem can be read by any Unix-like OS, because tar is so widely available. Support for any given filesystem is not so universal, although FAT filesystem support is extremely