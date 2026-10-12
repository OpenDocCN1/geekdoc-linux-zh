# Understanding RPM filenames

An RPM contains a number of files, but it appears as a single file on your Red Hat Linux system. By convention, the RPM filenames have a specific structure. To see the names of RPM files that come on the companion CD-ROM, use the following steps:

+   1. Place the CD-ROM in the CD-ROM drive and mount it with the following command (you must be logged in as root):
+      `mount /mnt/cdrom`
+      This mount command works because there is an entry for this mount point in the /etc/fstab file.
+   2. Go to the directory in which the RPMs are located and view a listing:
+      ```
+      cd /mnt/cdrom/RedHat/RPMS
+      ls *.rpm | more
+      ElectricFence-2.2.2-4.i386.rpm
+      ImageMagick-5.2.2-5.i386.rpm
+      ImageMagick-devel-5.2.2-5.i386.rpm
+      Inti-0.2preview-1.i386.rpm
+      Inti-devel-0.2preview-1.i386.rpm
+      LPRng-3.6.22-3.i386.rpm
+      (some lines deleted)
+      XFree86-100dpi-fonts-4.0.1-0.43.i386.rpm
+      XFree86-3DLabs-3.3.6-32.i386.rpm
+      XFree86-4.0.1-0.43.i386.rpm
+      (rest of the listing deleted)
+      ```

As you can guess from the listing, all RPM files end with an .rpm extension. To understand the various parts of the filename, consider the following RPM:

```
XFree86-4.0.1-0.43.i386.rpm
```

This filename has the following parts separated by dashes (-):

Package name | XFree86
Version number | 4.0.1
Release number | 0.43 (a Red Hat-assigned release number)
Architecture | i386 (for Intel 80386-compatible processors)

Usually, the package name is descriptive enough for you to guess the contents of the RPM. The version number is the same as that of the software package's