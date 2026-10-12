If mtools is installed, the output shows you the full name of the mtools package. The sample output shows that mtools version 3.9.7 is installed on the system. To try mtools, follow these steps:

+   1. Log in as root, or type su and then enter the root password.
+   2. Place an MS-DOS floppy disk in your system's A: drive.
+   3. Type mdir. You should see the directory of the floppy disk (in the standard DOS directory-listing format).

# Checking the /etc/mtools.conf file

The mtools package should work with the default setup; but if you get any errors, you should check the /etc/mtools.conf file. This file contains the definitions of the drives (such as A:, B:, and C:) that the mtools utilities see. Following are a few lines from a typical /etc/mtools.conf file:

```
drive a: file="/dev/fd0" exclusive 1.44m
drive b: file="/dev/fd1" exclusive 1.44m

# First SCSI hard disk partition
#drive c: file="/dev/sda1"

# First IDE hard disk partition
drive c: file="/dev/hda1"

# IDE Zip drive
drive X: file="/dev/hdd4" exclusive
```

The pound sign (#) indicates the start of a comment. Each line defines a drive letter, the associated Linux device name, and some keywords that indicate how the device is accessed. In this example, the first two lines define drives A: and B:. The third non-comment line defines drive C: as the first partition on the first IDE drive (/dev/hda1). If you have other DOS drives (D:, for example), you can add another line that defines drive D: as the appropriate disk partition.

If your system's A: drive is a high-density, 3.5-inch drive, you do not have to change anything in the default /etc/mtools.conf file.