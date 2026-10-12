
You need the name of the package before you can remove it. One good way to find the name is to use `rpm -qa` in conjunction with `grep` to search for the appropriate RPM file. For example, to locate the X Window System development RPM, you can try this:

```
rpm -qa | grep Xfree
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

In this case, `XFree86-devel` is the package name you need. To remove the package, type:

```
rpm -e XFree86-devel
```

![](img/5fe8f856723cde0b366f73584b9e64b8_262_0.png)

The `rpm -e` command does not remove a package that other packages need. For example, when you try to remove the `kernel-headers` package, you might get the following error message:

```
rpm -e kernel-headers
error: removing these packages would break dependencies:
kernel-headers      is needed by glibc-devel-2.1.92-5
kernel-headers      >= 2.2.1 is needed by glibc-devel-2.1.92-5
```

As the output from the `rpm -e` command shows, the `glibc-devel` package needs the `kernel-headers` package in order to function properly. In RPM parlance, `glibc-devel` depends on `kernel-headers`.

### Upgrading RPMs with the rpm command

When you use the `rpm -U` command to upgrade an RPM, you must provide the name of the RPM file that contains the new software. For example, suppose you have version 4.74 of Netscape Communicator installed on your system, but you want to upgrade to version 4.76. You'd download the RPM file `netscape-communicator-4.76-11.i386.rpm` from Red Hat's FTP server (`ftp://ftp.redhat.com/pub/redhat/update/`, or one of the mirror sites listed at `http://www.redhat.com/mirrors.html`), and then use the following command:

```
rpm -U netscape-communicator-4.76-11.i386.rpm
```

The `rpm` command performs the upgrade by first removing the old version of the Netscape Communicator package and then installing the new RPM.

Whenever possible, you should use `rpm -U` to upgrade software, rather than doing it manually yourself by removing the old package (`rpm -e`) and then installing the new version (using `rpm -i`). Why? Allowing RPM to perform the upgrade using `rpm -U` automatically saves the old configuration files, which saves you the hassle of configuring the software after a fresh installation. If you manually type `rpm -e` followed by `rpm -i` to erase an old RPM and install its replacement, the erase operation *also* deletes the old configuration files. The `rpm` upgrade command contains logic to save the old configuration files.

![](img/5fe8f856723cde0b366f73584b9e64b8_263_0.png)

> When you upgrade the kernel and the kernel module packages that contain a ready-to-run Linux kernel, do not use the `rpm -U` command. Instead, install it with the `rpm -i` command. Using `rpm -i` ensures that you don't overwrite files being used by the current kernel.

### Verifying RPMs with the `rpm` command

You may not do this often, but if you suspect that a software package is not properly installed, use the `rpm -V` command to verify the package. For example, to verify the kernel package, type the following:

```
rpm -V kernel
```

This causes `rpm` to compare size and other attributes of each file in the package against the original files. If everything verifies correctly, the `rpm -V` command does not print anything. If it detects any discrepancies, `rpm` displays a report of the discrepancies. For example, suppose you modified the configuration files for the Apache Web server. Here is what you might see when you verified the Apache package:

```
rpm -V apache
S,5....T c /etc/httpd/conf/httpd.conf
```

In this case, the output from `rpm -V` shows that a configuration file has changed. Each line of this command's output consists of three parts:

- The line starts with eight characters; each character indicates the type of discrepancy found. For example, S means the size has changed since the file was originally installed. T means the last modification time has changed. A period (.) indicates that a specific attribute matches the original.
- For configuration files, an `c` appears next; otherwise, this field is blank. That's how you can tell whether a file is a configuration file. Typically, you don't have to worry if a configuration file has changed because you probably made the changes yourself.
- The last part of the line is the file's full pathname. From this part, you can tell the exact location of the file.

### Troubleshooting

If you get error messages when using the `rpm` command to install, upgrade, or remove an RPM, make sure you are the root user. Any user can use the `rpm` command (or Gnome RPM) to query and verify RPMs, but only the root user can add, delete, or upgrade RPMs.

If you get an error message resembling “Package foo Is Already Installed” and want to re-install the foo RPM again anyway, use the `--force` option with `rpm -i`. The reason that RPM does not reinstall already installed RPMs is to try and minimize the chance of overwriting configuration files or otherwise altering the configuration of a running system.

Similarly, if you are removing an RPM using `rpm -e` and encounter an error message resembling “Error: Removing These Packages Would Break Dependencies,” you can use the `--nodeps` option with `rpm -e` (rpm `-e --nodeps`) to tell RPM to ignore the dependencies and remove the package anyway. However, before using `--nodeps`, make sure you will not compromise your system’s integrity and stability and be sure to have a way to boot the system and restore the original configuration.

### Review

This session introduced you to the Red Hat Package Manager (RPM) and its associated rpm commands. You learned to use the Gnome RPM graphical utility to install and uninstall RPMs. You also learned the syntax of a number of rpm commands to query, install, upgrade, remove, and verify RPMs.

### Quiz Yourself

1. What is an RPM? (See “Using Gnome RPM to Install and Remove Packages.”)
2. What can you do with Gnome RPM and how do you run it? (See “Using Gnome RPM to Install and Remove Packages.”)
3. What is the syntax of the rpm command to find out all of its command-line options? (See “Using the rpm Command to Install and Remove Packages.”)
4. Which rpm command do you use to view a list of all installed RPMs? (See “Querying RPMs with the rpm command.”)
5. How do you install a new RPM from this book’s companion CD-ROM containing the Red Hat Linux RPMs? (See “Installing RPMs with the rpm command.”)

![](img/5fe8f856723cde0b366f73584b9e64b8_266_0.png)

![](img/5fe8f856723cde0b366f73584b9e64b8_266_1.png)

## SESSION 24

## Building a New Kernel

### Session Checklist

- Installing the source files and rebuilding the kernel
- Configuring the kernel
- Building and installing the kernel and modules
- Rebooting the system with a rebuilt kernel

At some point, you may want or need to rebuild the kernel — the very core of the operating system — from scratch, that is, from the source code. For example, you may want to take advantage of a new driver not available in the kernel version shipped on the Red Hat Linux CD-ROMs. This session shows you how to install the kernel’s source files; how to configure the kernel; and how to build and install the new kernel and modules. Finally, you will learn how to reboot the system using the newly built and installed kernel.

*10 Min. To Go*

### Rebuilding the Kernel

Rebuilding the kernel refers to creating new versions of the binary files constituting the heart of the Linux operating system. You may have to (or want to) rebuild the kernel for various reasons, including the following:

- You can recompile the kernel to support your specific CPU, especially features that improve performance. The default Red Hat Linux installation uses a kernel configured to run on the widest possible variety of Intel CPUs, all the way back to 386s and 486s. As a result, it does not take advantage of all the features and improvements available in the newest CPUs.
- You may want to create a new kernel that includes support for only the hardware actually installed on your system. The default kernel supports a wide variety of the most common hardware, but no single system needs all of that support.
