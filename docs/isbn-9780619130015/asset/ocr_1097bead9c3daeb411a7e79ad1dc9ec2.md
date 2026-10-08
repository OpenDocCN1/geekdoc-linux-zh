# The /sbin Directory

The /sbin directory is reserved for the system administrator. Programs that start the system, programs needed for file system repair, and essential network programs are stored here.

# The /tmp Directory

Many programs need a temporary place to store data during processing cycles. The traditional location for these files is the /tmp directory.

# The /var Directory

The /var directory holds subdirectories whose sizes often change. These subdirectories contain files such as error logs and other system performance logs that are useful to the system administrator. The /var/spool/mail subdirectory contains mail from the network, which remains there until you read and delete it.

# Using the mount Command

As you learned, UNIX uses the mount command to connect the file system partitions to the directory tree when the system starts. Users can access virtually any file system that has been mounted and to which they have been granted permission. Additional file systems can be mounted at any time using the mount command. The floppy disk and CD-ROM drive are the file system devices beyond the hard disk that are most commonly mounted.

> tip
To ensure security on the system, only the root user can normally use the mount command. Ordinary users can sometimes mount and unmount file systems located on floppy disks and CDs.

Suppose you want to access files on a CD for the Dominion Consulting database. The system administrator mounts a CD-ROM by inserting a disk in the drive and uses the following mount command:

```
mount -t iso9660 -r /dev/cdrom /mnt/cdrom
```

This command mounts the CD on a device called “cdrom” located in the /dev directory. The actual mount point in UNIX is /mnt/cdrom, a directory that references the CD-ROM device. Once the CD is mounted, you can access its files through the /mnt/cdrom directory. UNIX supports several different types of file systems. The type of file system is specified with the -t option. CD-ROMS are classified as iso9660 devices, so the system administrator types -t, followed by the argument iso9660. The -r indicates that the CD-ROM device is read-only.