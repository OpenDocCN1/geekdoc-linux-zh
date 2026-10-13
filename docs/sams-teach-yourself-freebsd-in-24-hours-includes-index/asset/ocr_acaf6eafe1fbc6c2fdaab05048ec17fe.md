entire disk. Floppy disks don’t generally need this, but many CD-ROM drives do. You will generally want to use /dev/acd0c instead of /dev/acd0 to address a CD-ROM drive. If one name doesn’t work, try the other.

# Formatting Disks

Floppy disks and hard disks must be formatted before you can mount them. To format a floppy that has never been formatted before, use the fdformat command (noting, of course, that all its contents will be erased):

```
# fdformat /dev/fd0
Format 1440 floppy '/dev/fd0'? (y/n):y
```

After fdformat finishes formatting the disk, issue disklabel and newfs commands to complete preparing the disk for use with FreeBSD:

```
# disklabel -w -r /dev/fd0 fd1440
# newfs /dev/fd0
```

Hard disks are more difficult to format and label from the command line. There are many more options you might want to set, including possibly partitioning the disk (which is done with a utility called fdisk). To format a hard disk, it’s best to use the sysinstall program. Refer back to Hour 2 for directions on how to use sysinstall to format and partition a hard disk.

CD-ROMs don’t need to be formatted; if you have a CD or DVD burner, the process of writing data to the disc is coupled with the necessary formatting and labeling, and the resulting ISO 9660 filesystem type is compatible with all operating systems.

# The mount Command

Mounting a disk is done with the mount command. In its most common form, using mount is a simple and straightforward procedure. All that’s involved is picking a location somewhere in the directory tree to attach your disk, making sure that an empty directory is located there, and issuing the appropriate mount command.