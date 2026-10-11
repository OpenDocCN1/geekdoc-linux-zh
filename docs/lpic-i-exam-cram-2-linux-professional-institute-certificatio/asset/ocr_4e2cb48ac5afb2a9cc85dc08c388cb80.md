start the process of writing the `\images\bootdisk.img` image to the A: drive, like so:

```
D:\dosutils\rawrite.exe d:\images\bootdisk.img
```

When you’re using NT, Win2k, or XP, you need to get the rawwritewin.exe tool from the following link:

http://uranus.it.swin.edu.au/~jn/linux/rawrite.htm

This application allows the writing of the boot disk images to the floppy. Windows NT and higher won’t normally allow direct access to hardware from a DOS program such as rawrite.exe.

# ## Boot Loaders

A Linux computer has the boot loader in one of two places: the master boot record (MBR) or the first sector of the Linux partition. Because many other operating systems use the same methodology—particularly Windows claiming the exact same MBR location as Linux—conflicts can occur.

Dual-booting Linux and Windows can be a challenge, but if you install them in the correct order and use LILo or GRUB to manage the boot loader environment, it’s not difficult. I recommend installing the Windows product first because it’s pickier about the MBR. Then, after the final reboot, install the Linux system in the prepared free space, allowing LILo or GRUB to notice and configure the Windows partition in the boot loader setup.

# ## LILo—The Linux Loader

The LILo package consists of the /sbin/lilo command, the /etc/lilo.conf configuration file, help documentation, and boot loader files. The relationships between the /sbin/lilo command, its configuration file, and the MBR/First Sector targets are as follows:

+   1. The /sbin/lilo program is invoked.
+   2. The /etc/lilo.conf file is read and parsed.
+   3. The salient files mentioned in the file are located and errors are produced if they’re not found.
+   4. The resulting binary image is written by default to the MBR.
+   5. The /sbin/lilo program exits.