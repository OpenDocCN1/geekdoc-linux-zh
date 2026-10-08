# PART 2 Layered Security and Linux

# The /var/ Filesystem

Files in the /var/ directory can easily grow large. Some distributions use subdirectories of /var/ to contain files associated with some servers. Uploads to such servers if limits can be breached, could quickly overload the space available on just any system.

In addition, the /var/ directory contains log files. The logs for enterprise-level Web sites can easily grow to several gigabytes every day. If such a directory is not maintained, this array of large files could quickly overload just any system. The configuration of the /var/ directory on a separate filesystem can limit such risks.

# Read-Only Filesystems

It is possible and even desirable to set up a few filesystems in “read-only” mode. When configured correctly, such filesystems can make it a bit more difficult for black-hat hackers to do damage to your system. Three filesystems candidates for mounting in read-only mode are /boot/, /opt/, and /usr/. Of course, if you were to update a kernel or install a new package, you should remount the filesystem in read-write mode so the kernel or package files could be written to the appropriate directories.

The following is a possible read-only configuration for the /boot/ directory in the /etc/fstab configuration:

```
/dev/sda ext2 ro,exec,auto,nouser,async 1
```

If you're familiar with the format of the /etc/fstab file, you should already know that an option defaults would mount the noted filesystem in read-write mode. Of course, since you'll also have to mount that filesystem in read-write mode when updating related components such as the Linux kernel, it may be helpful to have the read-write configuration line in the same file. That means that /etc/fstab file might also include the following line for the /boot/ directory filesystem:

```
# /dev/sda ext2 defaults 1 2
```

Not all filesystems should be mounted in read-only mode. Users who log in to the GUI need access to the filesystem with the /tmp/ directory. Log information is not available unless the system can write to the filesystem with the /var/ directory. New filesystems can't be installed unless the system has write access to the filesystems associated with the /etc/, /usr/, and /lib/ directories. Of course, you could remount a filesystem in read-write mode when installing or updating software.

Closely related to the concept of a read-only filesystem is the use of a live CD/DVD-based distribution. While users can write to filesystems configured from most live CD/DVDs, files are written only in the RAM memory configured as a virtual drive. Thus changes are lost as soon as the system is shut down. And by definition, anything not written to the live CD/DVD. So if there is a security breach, the information on the CD/DVD media is not affected.