![](bbox=[0.11, 0.1, 0.22, 0.24])

In Fedora Core, the **RPM** commands are suitable only if you have to install only a handful of **RPM** files. To install a large number of **RPM** files, you should choose **Applications→Add/Remove Software** from the desktop. If you install **RPM** files from a CD or DVD, first mount the CD/DVD and then type **system-cdinstall-helper /media/cdrom**. (If your CD/DVD is mounted at some other directory, replace /media/cdrom with that directory name.) That should bring up a Package Management window from which you can select and install groups of packages.

# Using the RPM commands

When you install an RPM-based distribution such as Fedora Core, the installer uses the **rpm** command to unpack the packages (**RPM** files) and to copy the contents to your hard drive.

You don't have to understand the internal structure of an **RPM** file, but you need to know how to use the **rpm** command to work with **RPM** files. Here are some of the things you can do with the **rpm** command:

+   • Find out the version numbers and other information about the RPMs installed on your system.

+   • Install a new software package from an **RPM**. For example, you may install a package you skipped during the initial installation.

+   • Remove (uninstall) unneeded software you previously installed from an **RPM**. You may uninstall a package to reclaim the disk space, if you find that you rarely (or never) use the package.

+   • Upgrade an older version of an **RPM** with a new one. For example, in Fedora Core, you may upgrade after you download a new version of a package from Fedora Core download sites (listed online at http://fedora.redhat.com/download/mirrors.html). You must upgrade an **RPM** to benefit from the fixes in the new version.

+   • Verify that an **RPM** is in working order. You can verify a package to check that all necessary files are in the correct locations.

As you can see, the **rpm** command is versatile — it can do a lot of different things, depending on the options you use.

If you ever forget the **rpm** options, type the following command to see a list:

```
rpm --help | more
```

The number of **rpm** options will amaze you!