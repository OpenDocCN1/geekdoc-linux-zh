# Using mtools 455

+   4. Log out and log in as a normal user.

+   5. To confirm that you can mount a DOS floppy as a normal user and not just root, insert a DOS floppy in the A drive and type the following command:

```
mount /a
```

The mount operation succeeds, and you see a listing of the DOS floppy when you type the command ls /a.

+   6. To unmount the DOS floppy, type mount /a

# Mounting an NTFS Partition

Nowadays, most PCs come with Windows XP and Windows 2000 preinstalled on the hard drive. Both Windows XP and 2000, as well as Windows NT, typically use the NT File System (NTFS). Linux supports read-only access to NTFS partitions, and Fedora Core does not have the ntfs.ko kernel module that needed to access an NTFS partition.

If you have installed Fedora Core on a Windows XP system and want to access files on the NTFS partition, you can build the kernel after selecting an NTFS module during the kernel configuration step (see Chapter 6 of this minibook for detailed instructions on configuring, building, and installing the kernel).

After rebooting and booting from the new kernel, log in as root, and type the following command to create a mount point for the NTFS partition (in this case I am creating a mount point in the /mnt directory);

Now, you can mount the NTFS partition with the following command:

```
mount /dev/hda2 /mnt/xp -t ntfs -r - umask=0222
```

Replace /dev/hda2 with the device name for the NTFS partition on your system. Most PCs come with Windows XP preinstalled, the second one is the second (/dev/hda2) — the first partition (/dev/hda1) is usually a hidden partition used to hold files for Windows XP installation.

![](bbox=[0.125, 0.693, 0.183, 0.745])

# Using mtools

To access the MS-DOS file system is to mount the hard drive or floppy disk by using the mount command and then use Linux commands, such as ls and cp, to work with the mounted DOS file system. This approach of mounting a DOS file system is fine for hard drives. Linux can mount the DOS partition automatically at startup, and you can access the DOS directories on the hard drive at any time.