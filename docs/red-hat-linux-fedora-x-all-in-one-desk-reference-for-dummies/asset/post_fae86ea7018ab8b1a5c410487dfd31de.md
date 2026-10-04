
## 460 Using mtools

1. Use the fdfformat command to low-level-format a floppy disk.

The fdfformat command uses the floppy device name as the argument; the device name includes all parameters necessary for formatting the floppy disk.

Figure 3-5 illustrates the device-naming convention for the floppy-drive device. As shown in Figure 3-5, you use the following command to format a 3.5-inch, high-density floppy disk in your system's A:

```
mformat /dev/fd0HJ440
```

Figure 3-5: Here's how you can construct the name of a floppy disk drive in Fedora Core.

![](img/d9230b719dc0efd80851f363d8c6f571_486_0.png)

3 or 4 digits indicating capacity of floppy disk in kilobytes:
- 5.25-inch: 360, 720, or 1200
- 3.5-inch: 360, 720, or 1440

One of the following letters:
- d = low-density 5.25-inch
- D = low-density 3.5-inch
- h = high-density 5.25-inch
- h = high-density 3.5-inch

One of the following letters:
- 0 = first floppy drive (A);
- 1 = second floppy drive (B:)

2. Use the mformat command to put an MS-DOS file system on the low-level-formatted floppy disk.

If the floppy is in drive A, type the following command to create a formatted DOS floppy:

```
mformat a:
```

## Chapter 4: Managing Applications

### In This Chapter

- Finding out about RPMs
- Installing and removing software RPMs
- Building applications from source files
- Updating Fedora Core applications with Up2date and Yum

Most software packages for Fedora Core are distributed in special files called Red Hat Package Manager (RPM) files, which is why you know how to install or remove software packages that come in the form of RPM files. In this chapter, I show you how to work with RPM files.

Many other open-source software packages come in source-code form, usually in compressed archives. You have to build and install the software to use it. I describe the steps you typically follow when downloading, building, and installing source-based software packages.

Finally, I briefly describe how you can use Up2date (Red Hat's Update Agent) and Yum to update Fedora Core applications.

## Working with Red Hat Package Manager

Red Hat Package Manager (RPM) is a system for packaging all the necessary files for a software product in a single file — called an RPM file or simply an RPM. In fact, the entire Fedora Core distribution is a whole lot of RPMs. The best way to work with RPMs is through the RPM commands. You have to type these commands at the shell prompt in a terminal window or text console.

## Using the RPM commands

When you install Fedora Core from the companion DVD-ROMs, the Fedora Core installer uses the rpm command to unpack the packages (RPM files) and to copy the contents to your hard drive.

## 462 Working with Red Hat Package Manager

You don't have to understand the internal structure of an RPM file, but you need to know how to use the rpm command to work with RPM files. Here are some of the things you can do with the rpm command:

- Find out the version numbers and other information about the RPMs installed on your system.
- Install a new software package from an RPM. For example, you may install a package skipped during the initial installation. You can do that with the rpm command.
- Remove (uninstall) unneeded software you previously installed from an RPM. You may uninstall a package to reclaim the disk space, if you find that you rarely (or ever) use the package.
- Upgrade an older version of an RPM with a new one. You may upgrade after you download a new version of a package from Fedora Core download sites (listed online at fedora.redhat.com/download/mirrors.html). Often you must upgrade RPM to benefit from the fixes in the new version.
- Verify that an RPM is in working order. You can verify a package to check that all necessary files are in the correct locations.

As you can see, the rpm command is versatile — it can do a lot of different things depending on the options you use.

If you ever forget rpm options, type the following command to see a list:

```
rpm --help | more
```

The number of rpm options will amaze you!

### Understanding RPM filenames

An RPM contains a number of files, but it appears as a single file on your Fedora Core system. By convention, the RPM filenames have a specific format. To see the names of some of the RPM files on the companion DVD-ROMs, follow these steps:

1. Place the DVD-ROM in the DVD drive. The DVD-ROM automatically mounts if you're using the GNOME or KDE graphical desktops. Otherwise, mount it with the following command (you must be logged in root):

```
mount /dev/cdrom
```

If you are inserting the DVD-ROM into your system's second CD/DVD drive, type mount /dev/cdrom1 to mount the DVD-ROM.

## Working with Red Hat Package Manager 463

2. Type the following command to go to the directory in which the RPMs are located:

```
cd /mnt/cdrom/Fedora/RPMS
```

3. View the listing using the ls command. For example, to see RPMs that start with cups, type

```
ls cups*
```

You see a listing that looks like:

```
cups-1.20-6.i386.rpm
cups-libs-1.20-6.i386.rpm
```

As you may guess from the listing, names of files end with .rpm. To understand the various parts of the filename, consider the following RPM:

```
cups-1.20-6.i386.rpm
```

This filename has the following parts, separated by dashes (-):
- **Package name:** cups
- **Version number:** 1.20
- **Release number:** 6 (a Red Hat assigned release number)
- **Architecture:** i386 (this package is for Intel 386-compatible processors)

Usually, the package name is descriptive enough for you to guess what the RPM may contain, the same as the software's current version (even when distributed in some other format, such as tar file). Developers assign the release number to keep track of changes. The architecture is i386 or noarch for the RPMs you want to install on a PC with an x86-compatible processor.

### Finding about RPMs

As it installs packages, the rpm command builds a database of RPMs. You can use the rpm -q command to query this database to find information about packages installed on your system. For example, to find the version number of the Linux kernel on your system, type the following rpm -q:

```
rpm -q kernel
```

## 464 Working with Red Hat Package Manager

You see a response similar to the following:

```
kernel-2.6.5-1.386
```

The response is the name of the RPM (for the kernel this is the executable version of the kernel, not source files). The name is the same as the RPM filename, except that the last part — i386.rpm — isn't shown. In this case, the version part of the RPM tells you it is 2.6.5.

You can see a list of all installed RPMs by using the following command:

```
rpm -qa
```

You see a long list of RPMs scroll your screen. To view the list one screen at a time,

```
rpm -qa | more
```

If you want to search for a specific package, feel the output of rpm -qa to the grep command. For example, to see all packages with kernel in their names, type

```
rpm -qa | grep kernel
```

The result depends on what parts of the kernel RPMs are installed on a system. For this example our system shows the following:

```
kernel-2.6.5-1.386
kernel-source-2.6.5-1.386
```

You can query more than a version number with the rpm -q command. By adding single-letter options, you can find other information. For example, try the following command to see the files in the kernel package:

```
rpm -ql kernel
```

Here are few lines from the output of this command:

```
/boot/System.map-2.6.5-1.386
/boot/config-2.6.5-1.386
/boot/bzImage-2.6.5-1.386
/lib/modules/2.6.5-1.386/
/lib/modules/2.6.5-1.386/build/
/lib/modules/2.6.5-1.386/build/Makefile
/lib/modules/2.6.5-1.386/build/arch
/lib/modules/2.6.5-1.386/build/alpha
/lib/modules/2.6.5-1.386/build/alpha/Kconfig
/lib/modules/2.6.5-1.386/build/alpha/Makefile
```

```
/lib/modules/2.6.5-1.386/build/arch/alpha/boot
/lib/modules/2.6.5-1.386/build/arch/alpha/boot/Makefile
/lib/modules/2.6.5-1.386/build/arch/alpha/kernel
/lib/modules/2.6.5-1.386/build/arch/alpha/kernel/Makefile
(rest of the listed deleted)
```

Here are a few more useful forms of the rpm -q commands to query information about a package (to use any of these rpm -q commands, type the command, followed by the package name):

- rpm -qc: Lists all configuration files in a package.
- rpm -qd: Lists all documentation files in a package. These are usually the online manual pages (also known as man pages).
- rpm -qf: Displays the name of the package (if any) to which a specified version number, size, installation date, and a brief description.
- rpm -qi: Displays detailed information about a package, including version.
- rpm -ql: Lists all the files in a package. For some packages, you see a very long list.
- rpm -qs: Lists the state of all files in a package.

![](img/d9230b719dc0efd80851f363d8c6f571_491_0.png)

These rpm commands provide information about installed packages only. If you want to find information about an uninstalled RPM file, add the letter p to the command-line option of each command. For example, to view the list of files in the RPM file named rdist-6.1.5-32.1386.rpm, go to the directory where that file is located and then type the following command:

```
rpm -qpl rdist-*.rpm
```

Of course, this command works only if the current directory contains the RPM file.

![](img/d9230b719dc0efd80851f363d8c6f571_491_1.png)

Two handy rpm -q commands enable you to find out which RPM file provides a specific file and which RPMs need a specified package. To find out the name of the RPM that provides a file, use the following command:

```
rpm -q --whatprovides filename
```

For example, to see which RPM provides the file /etc/yum.conf, type

```
rpm -q --whatprovides /etc/yum.conf
```

RPM then prints the name of the package that provides the file, like this:

```
yum-2.0.7-1.1
```
