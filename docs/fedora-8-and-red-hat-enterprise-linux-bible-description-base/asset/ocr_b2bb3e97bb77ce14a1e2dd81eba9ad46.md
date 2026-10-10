```
# ls /mnt/win
```

The `-oro` option to mount will mount the file system read-only. Read/write support is not considered to be stable (so if you remove the `-oro` option to mount read/write, you do so at your own risk). Replace the `ntfs` with `vfat` if your Windows partition is a VFAT file system. The `ls` command is just to find out if you can see the contents of your Windows partition.

You can have the mount occur permanently by adding an entry to the `/etc/fstab` file. Here's an example of the line you could add to `/etc/fstab` to have the partition mounted every time the system reboots:

```
/dev/sda1 /mnt/win ntfs ro 0 0
```

At this point, you can use the files from your Windows partition as you would any other files on your system. You can open a folder or change directories to the `/mnt/win` directory to see the contents. Then use any applications you choose to open your documents (OpenOffice.org), music (Rhythmbox), images (gimp), or any other content type you want to use from your Windows partition in Linux.

> **NOTE:** If your Linux system uses an ext2 or ext3 file system (as Fedora typically does), you can do the reverse of what was just described as well: access your Linux partition from Windows. For information on how to do this, see The Ext2 Installable File System for Windows (www.fs-driver.org).

# Partitioning your disks

The hard disk (or disks) on your computer provides the permanent storage area for your data files, applications programs, and the operating system (such as Fedora or RHEL). Partitioning is the act of dividing a disk into logical areas that can be worked with separately. There are several reasons you may want to do partitioning:

+   - **Multiple operating systems** — If you install Fedora or RHEL on a PC that already has a Windows operating system, you may want to keep both operating systems on the computer. To run efficiently, they must exist on completely separate partitions. When your computer boots, you can choose which system to run. Note that you are limited in the number of partitions you can have (with IDE drives you can have 63 partitions; with SCSI devices, you are limited to 15 partitions per device).

+   - **Multiple partitions within an operating system** — To protect from having their entire operating system run out of disk space, people often assign separate partitions to different areas of the Linux file system. For example, if `/home` and `/var` were assigned to separate partitions, then a gluttonous user who fills up `/home` partition wouldn't prevent logging daemons from continuing to write to log files in the `/var/log` directory.