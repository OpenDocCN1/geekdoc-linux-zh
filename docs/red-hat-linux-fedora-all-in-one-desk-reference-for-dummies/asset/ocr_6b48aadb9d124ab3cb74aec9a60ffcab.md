+   - Find out the version numbers and other information about the RPMs installed on your system.
+   - Install a new software package from an RPM. You may install a package you have skipped during the initial installation. For example, you have to install the source files for the Linux kernel before you can rebuild the kernel. You can do that with the `rpm` command.
+   - Remove (uninstall) unneeded software you have previously installed from an RPM. You may uninstall a package to reclaim the disk space, if you find that you rarely (or never) use the package.
+   - Upgrade an older version of an RPM with a new one. You may upgrade after you download a new version of a package from Red Hat's FTP server. Often you must upgrade an RPM to benefit from the fixes in the new version.
+   - Verify that an RPM is in working order. You can verify a package to check that all necessary files are in the correct locations.

As you can see, the rpm command is versatile — it can do a lot of different things depending on the options you use.

If you ever forget the rpm options, type the following command to see a list:

```
rpm --help | more
```

The number of rpm options will amaze you!

# Understanding RPM filenames

An RPM contains a number of files, but it appears as a single file on your Red Hat Linux system. By convention, the RPM filenames have a specific format. To see the names of some of the RPM files on the companion DVD, follow these steps:

+   1. **Place the first DVD in the DVD drive. The DVD should be automatically mounted if you're using GNOME or KDE graphical desktops. Otherwise, mount it with the following command (you must be logged in as root):**
+      `mount /dev/cdrom`
+   2. **Type the following command to go to the directory in which the RPMs are located:**
+      `cd /mnt/cdrom/RedHat/RPMS`
+   3. **View the listing using the ls command. For example, to see RPMs with names that start with cups, type**
+      `ls cups*`