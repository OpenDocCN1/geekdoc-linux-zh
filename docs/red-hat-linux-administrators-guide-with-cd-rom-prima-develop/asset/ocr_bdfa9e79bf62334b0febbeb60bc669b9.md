This section will explain how to access your GNUware CD. It is designed with the novice Linux user in mind. Accessing information from off a CD using Linux requires mounting the device. Because Linux treats different devices such as floppy drives and CD-ROMs as file systems, you need to mount the device itself into your partition table. Once you are through, be sure to unmount the device, otherwise you will encounter errors upon the next reboot.

The easiest way to mount a CD on your CD-ROM is to become root. After placing the CD in the drive, type the following:

```
mount -t iso9660 /dev/cdrom /mnt/cdrom
```

Change directories to the /mnt/cdrom directory. Using the ls command, you will be able to see the various directories containing the individual files. Copy the files from out of their respective directories to an install location. I recommend using your home directory, the /tmp directory, or a unique directory in /usr/local. Use the cp command as follows:

```
cp <filename> /usr/local/gnu/
```

When you are done copying the files down from off the CD, you will need to unmount the drive. First, make sure you are not accessing any files from within the /mnt/cdrom directory. Type the following:

```
umount /mnt/cdrom
```

Make sure you type it as "umount" and NOT "unmount". UNIX lost the "n" some time ago.

Another good way to peruse the contents of the CD is, after mounting the CD as per the instructions above, start up a Web browser. Netscape accomplishes this task quite well. Click on "File, Open Page..." and look for the file "/mnt/cdrom/index.html". This will allow you to look at the entire CD's contents using a javascript-enabled browser. It features a collapsible tree structure and further information on each program. You can then copy the file of choice