
current version number (even when it is distributed in some other form, such as a tar file). Red Hat assigns the release number to keep track of changes. The architecture should be i386 or noarch for the RPMs you want to install on a PC with an Intel x86-compatible processor.

## Querying RPMs with the rpm command

As it installs packages, the rpm command builds a database of installed RPMs. You can use the rpm -q command to query this database in order to find out information about packages installed on your system. For example, to find out the version number of the Linux kernel installed on your system, type the following rpm -q command:

```
rpm -q kernel
kernel-2.2.16-21
```

The response is the name of the RPM for the kernel (the executable version of the kernel; not the source files). The name is the same as the RPM filename except that the last part — .i386.rpm — does not appear. In this case, the version part of the RPM tells you that the kernel is 2.2.16.

You can see a list of all installed RPMs by typing the following command:

```
rpm -qa | more
```

If you want to search for a specific package, feed the output of rpm -qa to the grep command. For example, to see all packages with kernel in their names, type:

```
rpm -qa | grep kernel
kernel-pcmcia-cs-2.2.16-21
kernel-headers-2.4.0-0.20
kernel-2.2.16-21
kernel-source-2.2.16-21
kernelcfg-0.5-9
kernel-utils-2.2.16-21
```

You can query much more than a package’s version number with the rpm -q command. By adding single-letter options, you can find out other useful information about a package. For example, try the following command to see the files in the kernel package:

```
rpm -ql kernel
/boot/System.map-2.2.16-21
```
/boot/module-info-2.2.16-21
/boot/vmlinuz-2.2.16-21
/boot/vmlinuz-2.2.16-21
/lib/modules
/lib/modules/2.2.16-21
/lib/modules/2.2.16-21/.rhmvtag
/lib/modules/2.2.16-21/block
(rest of the listing deleted)

The following are several useful forms of rpm -q commands to query information about a package. (To use any of these rpm -q commands, type the command followed by the package name.)

- `rpm -qa` Lists all installed RPMs.
- `rpm -qc` Lists all configuration files in a package.
- `rpm -qd` Lists all documentation files in a package. These are usually the online manual pages (also known as man pages).
- `rpm -qi` Displays detailed information about a package including version number, size, installation date, and a brief description.
- `rpm -ql` Lists all the files in a package. For some packages, this can be a very long list.
- `rpm -qs` Lists the state of all files in a package.

## Installing RPMs with the rpm command

To install an RPM, you have to use the rpm -i command. You must provide the name of the RPM file as the argument. A typical example is to install an RPM from this book's companion CD-ROM containing the Red Hat Linux RPMs. As usual, you have to first mount the CD-ROM and then change to the directory in which the RPMs are located. Then, use the rpm -i command to install the RPM followed by the name of the RPM.

For example, to install the kernel-source RPM (which contains the source files for the Linux operating system) from my CD-ROM, I type the following commands:

```
mount /mnt/cdrom
cd /mnt/cdrom/RedHat/RPMS
rpm -i kernel-source*
```

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_293_0.png)

You do not have to type the full RPM filename — you can use a few characters from the beginning of the name followed by an asterisk. Make sure that you type enough of the name to uniquely identify the RPM file.

If you try to install an already installed RPM, the rpm command displays an error message. For example, here is what happens when I try to install the Emacs editor on my system:

```
rpm -i emacs-20*
package emacs-20.7-13 is already installed
```

To force the rpm command to install a package even if there are errors, just add --force to the rpm -i command as follows:

```
rpm -i --force emacs-20*
```

## Removing RPMs with the rpm command

You can remove — uninstall — a package if you realize that you don’t really need the software. For example, if you install the X Window System development package, but you are not interested in writing any X applications, you can easily remove the package by using the rpm -e command.

You need the name of the package before you can remove it. One good way to find the name is to use rpm -qa in conjunction with grep to search for the appropriate RPM file. For example, to locate the X Window System development RPM, you can try this:

```
rpm -qa | grep XFree
XFree86-75dpi-fonts-4.0.1-0.43
XFree86-twm-4.0.1-0.43
XFree86-libs-4.0.1-0.43
XFree86-xfs-4.0.1-0.43
XFree86-4.0.1-0.43
XFree86-devel-4.0.1-0.43
XFree86-tools-4.0.1-0.43
XFree86-xdm-4.0.1-0.43
XFree86-SVGA-3.3.6-32
```

In this case, XFree86-devel is the package name you need. To remove the package, type:

```
rpm -e XFree86-devel
```

You do not need the full RPM filename. All you need is the package name — the first part of the filename up to the dash (-) before the version number.

The rpm -e command does not remove a package that other packages need. For example, when I try to remove the kernel-headers package, I get the following error message:

```
rpm -e kernel-headers
error: removing these packages would break dependencies:
    kernel-headers  is needed by glibc-devel-2.1.92-5
    kernel-headers >= 2.2.1 is needed by glibc-devel-2.1.92-5
```

## Upgrading RPMs with the rpm command

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_294_0.png)

When you use the rpm -U command to upgrade an RPM, you must provide the name of the RPM file that contains the new software. For example, suppose I have version 4.72 of Netscape Communicator installed on my system, but I want to upgrade to version 4.74. I download the RPM file netscape-communicator-4.74-0.6.2.i386.rpm from Red Hat's FTP server (ftp://ftp.redhat.com/pub/redhat/updates/ or one of the mirror sites listed at http://www.redhat.com/mirrors.html) and then use the following command:

```
rpm -U netscape-communicator-4.74-0.6.2.i386.rpm
```

The rpm command performs the upgrade by first removing the old version of the Netscape Communicator package and then installing the new RPM.

Whenever possible, you should upgrade (rather than remove) the old package and then install the new version. Upgrading automatically saves the old configuration files, which saves you the hassle of configuring the software after a fresh installation.

When you upgrade the kernel and the kernel module packages that contain a ready-to-run Linux kernel, do not use the rpm -U command. Instead, install it with the rpm -i command. This is to ensure that you don't overwrite files being used by the current kernel.

## Verifying RPMs with the rpm command

You may not do this often, but if you suspect that a software package is not properly installed, use the rpm -V command to verify the package. For example, to verify the kernel package, type the following:

```
rpm -V kernel
```

This causes rpm to compare size and other attributes of each file in the package against the original files. If everything verifies correctly, the rpm -V command does not print anything. If it detects any discrepancies, you see a report of the discrepancies. For example, I modified the configuration files for the Apache Web server. Here is what I see when I verify the apache package:

```
rpm -V apache
S.5....T c /etc/httpd/conf/httpd.conf
```

In this case, the output from rpm -V shows that a configuration file has changed. Each line of this command’s output consists of three parts:

- The line starts with eight characters; each character indicates the type of discrepancy found. For example, S means the size is different and T means the time of last modification is different. A period indicates that a specific attribute matches with the original.
- For configuration files, a c appears next; otherwise, this field is blank. That’s how you can tell whether a file is a configuration file. Typically, you don’t have to worry if a configuration file has changed because you probably made the changes yourself.
- The last part of the line is the full pathname of the file. From this part, you can tell the exact location of the file.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_295_0.png)

## REVIEW

This session introduced you to the Red Hat Package Manager (RPM) and its associated rpm commands. You learned to use the Gnome RPM graphical utility with which you can install and uninstall RPMs. You also learned the syntax of a number of rpm commands to query, install, upgrade, remove, and verify RPMs.
