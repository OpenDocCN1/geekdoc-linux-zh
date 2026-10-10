
**vgdisplay command** A command used to view LVM VG.

**vgextend command** A command used to add additional physical volumes to an LVM VG.

**vgscan command** A command used to view LVM VGs.

**Volume Group (VG)** A group of PVs that are used by the LVM.

## Review Questions

1. Which of the following commands can be used to create partitions on either a MBR or GPT hard disk?
   - a. `gdisk`
   - b. `cfdisk`
   - c. `fdisk`
   - d. `parted`

2. After a partition on a hard disk drive is formatted with a filesystem, all partitions on that hard disk drive must use the same filesystem. True or False?

3. You want to see the file systems that are presently in use on the system. What command could you use?
   - a. `cat /etc/fstab`
   - b. `ls -1 /etc/fstab`
   - c. `cat /etc/mtab`
   - d. `ls -1 /etc/fstab`

4. Jim has just purchased two new SCSI hard disk drives and a controller card for them. He properly installs the hardware in his machine. Before he can use them for data storage and retrieval, what must he do? (Choose all that apply.)
   - a. Mount the two hard drives so they are accessible by the operating system.
   - b. Mount a filesystem to each of the hard disk drives.
   - c. Create one or more partitions on each of the hard disk drives.
   - d. Use the vi editor to edit `/etc/mtab` and create an entry for the controller card and the hard disk drives.
   - e. Mount any partitions created on the two hard drives such that they are accessible by the operating system.
   - f. Format any partitions created with a valid filesystem recognized by Linux.

5. Given the following output from `/etc/fstab`, which filesystems will be automatically checked on boot by the `fsck` command?

```
/dev/sda1              /                 ext4    defaults    1  1
none                  /dev/pts          devpts  gid=5,mode=620    0  0
none                  /proc             proc  defaults    0  0
none                  /dev/shm          tmpfs  defaults    0  0
/dev/sdc2             swap              swap  defaults    0  0
/media/dvd            /media/dvd        iso9660 noauto,ro  0  0
/dev/fd0              /media/floppy     auto  noauto    0  0
```

   - a. none, as `fsck` must be run manually for each filesystem
   - b. `/`, `/dev/pts`, and `/dev/shm`
   - c. `/`, `/proc`, and `swap`
   - d. all of them, as `fsck` is run automatically at boot for all filesystems

6. A user mounts a device to a mount point directory and realizes afterward there are files previously found within the mount point directory that are needed. What should this user do?
   - a. Nothing; the files are lost and cannot ever be accessed.
   - b. Nothing; the files could not have been there because you can only mount to empty directories.
   - c. Unmount the device from the directory.
   - d. Run the `fsck` command to recover the file.
   - e. Look in the lost+found directory for the file.

7. Which command is used to display the amount of free space that exists on a filesystem?
   - a. `fsck`
   - b. `quota`
   - c. `du`
   - d. `df`

8. What must you do to successfully run the `fsck` command on a filesystem?
   - a. Run the `fsck` command with the `-u` option to automatically unmount the filesystem first.
   - b. Choose yes when warned that running `fsck` on a mounted filesystem can cause damage.
   - c. Unmount the filesystem.
   - d. Ensure that the filesystem is mounted.

9. Character devices typically transfer data more quickly than block devices. True or False?

10. What does the `du /var` command do?
    - a. shows the users connected to the /var directory
    - b. shows the size of all directories within the /var directory
    - c. dumps the /var directory
    - d. displays the amount of free space in the /var directory

11. What does the command `dump2fs -h` do?
    - a. backs up an ext2 filesystem
    - b. displays the number of inodes used and available in an ext2 filesystem
    - c. dumps an ext2 filesystem
    - d. is not a valid command

12. The first floppy drive on the system is not responding. You enter the `file /dev/fd0` command and receive the following output. What is the problem?

```
[root@server1 root]# file /dev/fd0
/dev/fd0: ASCII text
[root@server1 root]#
```

    - a. The floppy drive cable has come loose.
    - b. There is no floppy disk in the drive.
    - c. The device file has become corrupt.
    - d. The floppy drive is seen as a character device.

13. Which of the following statements are true? (Choose all that apply.)
    - a. Quotas can only limit user space.
    - b. Quotas can only limit the number of files a user can own.
    - c. Quotas can limit both user space and the number of files a user can own.
    - d. Hard limits can never be exceeded.
    - e. Hard limits allow a user to exceed them for a certain period of time.
    - f. Soft limits can never be exceeded.
    - g. Soft limits allow a user to exceed them for a certain period of time.
    - h. Either a hard limit or a soft limit can be set, but not both concurrently.

14. A device file \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_. (Choose all that apply.)
    - a. has no inode section
    - b. has no data section
    - c. has no size
    - d. displays a major and minor number in place of a file size
    - e. has a fixed size of 300 kilobytes

![](img/c27875544958897d817484d558c208c8_272_0.png)

15. Which of the following statements regarding LVM structure is correct?
    - a. PVs are collections of VGs.
    - b. LVs are created from the free space available within PVs.
    - c. VGs are comprised of one or more PVs.
    - d. PVs use the space within LVs to create VGs.

16. The `lvextend` command can be used to add additional unused space within a volume group to an existing logical volume. True or False?

17. You plug a USB flash memory drive into a system that has two SATA hard disks. How will the partition on this USB flash memory drive be identified by Linux?
    - a. `/dev/sda1`
    - b. `/dev/sda2`
    - c. `/dev/sdb1`
    - d. `/dev/sdc1`

18. Which command mounts all existing filesystems in `/etc/fstab`?
    - a. `mount -f`
    - b. `mount -a`
    - c. `mount /etc/fstab`
    - d. `mount /etc/mtab`

19. A user runs the `fsck` command with the `-a` option on a filesystem that is showing signs of corruption. How would that user locate any files the system was unable to repair?
    - a. Look in the root of the filesystem.
    - b. The system prompts the user for a target location when it comes across a file it cannot repair.
    - c. Mount the filesystem and check the lost+found directory underneath the mount point.
    - d. View the contents of the directory `/lost+found`.

20. Which command is used to format a partition on a hard disk drive with the ext4 filesystem?
    - a. `format_ext4 device`
    - b. `ext4mkfs device`
    - c. `e2mkfs -t ext4 device`
    - d. `makeext4FS device`

## Hands-on Projects

![](img/c27875544958897d817484d558c208c8_274_0.png)

These projects should be completed in the order given. The hands-on projects presented in this chapter should take a total of three hours to complete. The requirements for this lab include:

- A computer with Fedora 20 installed according to Hands-on Project 2-1

### Project 5-1

In this hands-on project, you view and create device files.

1. Boot your Fedora Linux virtual machine. After your Linux system has loaded, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2**. Log in to the terminal using the user name of **root** and the password of **LNxrock1**.

2. At the command prompt, type **ls -l /dev/tty6** and press **Enter**. What device does */dev/tty6* represent? Is this file a block or character device file? Why? What are the *major* and *minor* numbers for this file?

3. At the command prompt, type **rm -f /dev/tty6** and press **Enter**. Next, type **ls -l /dev/tty6** at the command prompt and press **Enter**. Was the file removed successfully?

4. Switch to the command-line terminal (tty6) by pressing **Ctrl+Alt+F6** and attempt to log in to the terminal using the user name of **root** and the password of **LNxrock1**. Were you successful?

5. Switch back to the command-line terminal (tty2) by pressing **Ctrl+Alt+F2**, type the command **mknod /dev/tty6 c 4 6** at the command prompt, and press **Enter**. What did this command do? Next, type **ls -l /dev/tty6** at the command prompt and press **Enter**. Was the file re-created successfully?

6. At the command prompt, type **reboot** and press **Enter**. After your Linux system has loaded, switch to a command-line terminal (tty6) by pressing **Ctrl+Alt+F6** and log in to the terminal using the user name of **root** and the password of **LNxrock1**. Why were you successful?

7. At the command prompt, type **ls -l /dev/tty?** and press **Enter**. What is similar about all of these files? Is the major number different for each file? Is the minor number different for each file? Why?

8. At the command prompt, type **find /dev** and press **Enter** to list all of the filenames underneath the */dev* directory. Are there many files? Next, type **du -s /dev** at the command prompt and press **Enter**. How large in kilobytes are all files within the */dev* directory? Why?

9. At the command prompt, type **cat /proc/devices | more** and press **Enter**. Which devices and major numbers are present on your system? What character devices have a major number of *4*? How does this compare with what you observed in Step *2*?

10. Type **exit** and press **Enter** to log out of your shell.
