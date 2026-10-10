
## Understanding RPM filenames

An RPM contains a number of files, but it appears as a single file on your Fedora Core system. By convention, RPM filenames have a specific format. A typical RPM filename looks like this:

openoffice.org-writer-1.9.104-2.i386.rpm

This filename has the following parts, the first three of which are separated by dashes (-):

- Package name: openoffice.org-writer
- Version number: 1.9.104
- Release number: 2
- Architecture: i386 (this package is for Intel 80x86 or Pentium-compatible processors)

Usually, the package name is descriptive enough for you to guess what the RPM may contain. The version number is the same as that of the software package’s current version number (even when it’s distributed in some other form, such as a tar file). Developers assign the release number to keep track of changes. The architecture is i386 or search for the RPMs you want to install on a PC with an Intel x86-compatible processor.

## Querying RPMs

As it installs packages, the rpm command builds a database of installed RPMs. You can use the rpm -q command to query this database to find out information about packages installed on your system.

For example, to find out the version number of the Linux kernel installed on your system, type the following rpm -q command:

```
rpm -q cups
```

You see a response similar to the following:

```
cups-1.1.23-15
```

The response is the name of the RPM for the kernel. (This version is the executable version of the kernel, not the source files.) The name is the same as the RPM filename, except that the last part—.i386.rpm—isn’t shown. In this case, the version part of the RPM tells you that you have cups (the Common UNIX Printing System) version 1.1.23 installed.

## Working with RPM Files

You can see a list of all installed RPMs by using the following command:

`rpm -qa`

You see a long list of RPMs scroll by your screen. To view the list one screen at a time, type:

`rpm -qa | more`

If you want to search for a specific package, feed the output of `rpm -qa` to the `grep` command. For example, to see all packages with kernel in their names, type:

`rpm -qa | grep kernel`

The result depends on what parts of the kernel RPMs are installed on a system.

You can query much more than a package’s version number with the `rpm -q` command. By adding single-letter options, you can find out other useful information. For example, try the following command to see the files in the cups package:

`rpm -ql cups`

Here are a few more useful forms of the `rpm -q` commands to query information about a package. (To use any of these `rpm -q` commands, type the command, followed by the package name.)

- `rpm -qc`: Lists all configuration files in a package.
- `rpm -qd`: Lists all documentation files in a package. These are usually the online manual pages (also known as man pages).
- `rpm -qf`: Displays the name of the package (if any) to which a specified file belongs.
- `rpm -qi`: Displays detailed information about a package, including version number, size, installation date, and a brief description.
- `rpm -ql`: Lists all the files in a package. For some packages, you see a very long list.
- `rpm -qs`: Lists the state of all files in a package. (The state of a file can be one of the following: normal, not installed, or replaced.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_477_0.png)

These rpm commands provide information about installed packages only. If you want to find information about an uninstalled RPM file, add the letter p to the command-line option of each command. For example, to view the list of files in the RPM file named `xrist-6.1.5-792.i386.rpm`, go to the directory where that file is located and type the following command:

`rpm -qpl rdast-*.rpm`

Of course, this command works only if the current directory contains that RPM file.

Two handy rpm -q commands enable you to find out which RPM file provides a specific file and which RPMs need a specified package. To find out the name of the RPM that provides a file, use the following command:

`rpm -q --whatprovides filename`

For example, to see which RPM provides the file /etc/vsftpd.conf, type:

`rpm -q --whatprovides /etc/vsftpd.conf`

RPM then prints the name of the package that provides the file, like this:

vsftpd-2.0.3-1

If you provide the name of a package instead of a filename, RPM displays the name of the RPM package that contains the specified package.

On the other hand, to find the names of RPMs that need a specific package, use the following command:

`rpm -q -f`

For example, to see which packages need the openssl package, type:

`rpm -q -f openssl`

The output from this command shows all the RPM packages that need the openssl package.

## Installing an RPM

To install an RPM, use the rpm -i command. You have to provide the name of the RPM file as the argument. If you want to view the progress of the RPM installation, use rpm -ivh. A series of hash marks (#) displays as the package is unpacked.

For example, to install the kernel-devel RPM (which contains the header files for the Linux operating system) for Fedora Core from the companion DVD-ROM, I insert the DVD, and after it's mounted, I type the following commands:

```
cd /media/cdrom/Fedora/RPMS
rpm -ivh kernel-devel*
```

You don't have to type the full RPM filename — you can use a few characters from the beginning of the name followed by an asterisk (*). Make sure you type enough of the name to identify the RPM file uniquely.

If you try to install an RPM that's already installed, the `rpm -i` command displays an error message. For example, here is what happens when I type the following command to install the man package on my system:

```
rpm -i man-2*
```

I get the following error message from the `rpm -i` command:

```
package man-2.4.1-221 is already installed
```

To force the `rpm` command to install a package even if errors are present, just add `--force` to the `rpm -i` command, like this:

```
rpm -i --force man-2*
```

## Removing an RPM

You may want to remove — uninstall — a package if you realize you don't really need the software. For example, if you have installed the X Window System development package but discover you're not interested in writing X applications, you can easily remove the package by using the `rpm -e` command.

You have to know the name of the package before you can remove it. One good way to find the name is to use `rpm -qa` in conjunction with `grep` to search for the appropriate RPM file.

For example, to remove the package named `qt3-devel`, type:

```
rpm -e qt3-devel
```

To remove an RPM, you don't need the full RPM filename; all you need is the package name — the first part of the filename up to the dash (-) before the version number.

The `rpm -e` command does not remove a package that other packages need.

## Upgrading an RPM

Use the `rpm -U` command to upgrade an RPM. You must provide the name of the RPM file that contains the new software. For example, if I have version 1.1.20 of `cups` (printing system) installed on my system but I want to upgrade to version 1.1.23, I download the RPM file `cups-1.1.23-i5.1386.rpm` from a repository and use the following command:

```
rpm -U cups-1.1.23-i5.1386.rpm
```

The `rpm` command performs the upgrade by removing the old version of the `cups` package and installing the new RPM.

Whenever possible, upgrade rather than remove the old package and install a new one. Upgrading automatically saves your old configuration files, which saves you the hassle of reconfiguring the software after a fresh installation.

When you’re upgrading the `kernel` packages that contain a ready-to-run Linux kernel, install it by using the `rpm -i` command (instead of the `rpm -U` command). That way, you won’t overwrite the current kernel.

## Verifying an RPM

You may not do so often, but if you suspect that a software package isn’t properly installed, use the `rpm -V` command to verify it. For example, to verify the kernel package, type the following:

```
rpm -V kernel
```

This command causes `rpm` to compare the size and other attributes of each file in the package against those of the original files. If everything verifies correctly, the `rpm -V` command does not print anything. If it finds any discrepancies, you see a report of them. For example, I have modified the configuration files for the Apache `httpd` Web server. Here is what I type to verify the `httpd` package:

```
rpm -V httpd
```

Here’s the result I get:

```
S,5....T c /etc/httpd/conf/httpd.conf
```

In this case, the output from `rpm -V` tells me that a configuration file has changed. Each line of this command’s output has three parts:

- The line starts with eight characters: Each character indicates the type of discrepancy found. For example, S means the size is different, and T means the time of last modification is different. Table 4-1 shows each character and its meaning. A period means that that specific attribute matches the original.
- For configuration files, a c appears next; otherwise, this field is blank. That’s how you can tell whether or not a file is a configuration file. Typically, you don’t worry if a configuration file has changed; you probably made the changes yourself.
- The last part of the line is the full pathname of the file. From this part, you can tell exactly where the file is located.
