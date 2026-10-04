
# 466 Working with Red Hat Package Manager

If you provide the name of a package instead of a filename, RPM displays the name of the RPM package that contains the specified package.

On the other hand, to find the names of RPMs that need a specific package, use the following command:

```bash
rpm -q --whatrequires packename
```

For example, to see which packages need the openssl package, type

```bash
rpm -q --whatrequires openssl
```

Here is a typical output from this command showing all the RPM packages that need openssl:

```
libcap-0.8.3-3
sendmail-8.12.11-4.6
curl-7.11.1-1
mod_ssl-2.0.49-4
openssl-devel-0.9.7a-35
dovecot-0.99.10.4-4
```

## Installing an RPM

To install an RPM, use the rpm -i command. You have to provide the name of the RPM file as the argument. A typical example is installing an RPM from this book's companion DVD-ROM containing the Fedora RPMs. As usual, you have to mount the DVD-ROM and change to the directory in which the RPMs are located. Then use the rpm -i command to install the RPM. If you want to view the progress of the RPM installation, use rpm -ivh, A series of hashes (#) displays as the package is unpacked.

For example, to install the kernel-source RPM (which contains the source files for the Linux operating system) from the companion DVD-ROM, I insert the DVD and after it is mounted, use the following command:

```bash
cd /mnt/cdrom/RPM
rpm -i kernel-source-*
```

You don't have to install the full RPM filename — you can use a few characters from the beginning of the name followed by an asterisk (*). Make sure you type enough of the name to identify the RPM file uniquely.

![](img/d9230b719dc0efd80851f363d8c6f571_492_0.png)

If you try to install an RPM that's already installed, the rpm -i command displays an error message. For example, here is what happens when you type the command to install the man package on your system:

```bash
rpm -i man-1*
```

## Working with Red Hat Package Manager 467

I get the error message from the rpm -i command:
package man-1.5m2-6 is already installed

To force the rpm command to install a package even if errors are present, just add --force to the rpm -i command, like this:

```bash
rpm -i --force man-1*
```

## Removing an RPM

You may remove — uninstall — a package if you realize you don't really need the software. For example, if you have installed the X Window development package but discover you're not interested in working X applications, you can easily remove the package using the rpm -e command.

You have to know the name of the package before you remove it. One good way to find the name is to use rpm -qa in conjunction with grep to search for the appropriate RPM file. For example, to locate the X Window System development RPM, try the following command:

```bash
rpm -qa | grep xorg
```

xorg-x11-devel happens to be the package name of the X Window System development RPM. To remove that package, type

```bash
rpm -e xorg-x11-devel
```

To remove an RPM, you don't need the full RPM filename; all you need is the package name — the first part of the filename to the dash (- ) before the version number.

The rpm -e command does not remove package other packages needed. For example, to remove the vim-common package, type the following command:

```bash
rpm -e vim-common
```

Then I get the error message:

```
error: Failed dependencies:
vim-common is needed by (installed) vim-enhanced-6.2.457-1
```

## Upgrading an RPM

Use the rpm -U command to upgrade RPM. You must provide the name of the RPM file that contains the new software. For example, if I have version 2.0.48 of Apache httpd (Web server) installed on my system but I want to upgrade to version 2.0.49, I download the RPM file httpd-2.0.49-4.1386.rpm from one of Red Hat update sites (listed at fedora.redhat.com/download/mirrors.html) and use the following command:

```bash
rpm -U httpd-2.0.49-4.1386.rpm
```

The rpm command performs the upgrade by removing the old version of the httpd package and installing the new RPM.

![](img/d9230b719dc0efd80851f363d8c6f571_494_0.png)

Whenever possible, upgrade rather remove the old package and install a new one. Upgrading automatically saves your old configuration files, saves you the hassle of reconfiguring the software after a fresh install.

When you're upgrading the kernel packages that contain a ready-to-run Linux kernel, install it by using the rpm -i command (instead of the rpm -U command). That way you won't overwrite the current kernel.

## Verifying an RPM

You may not do so often, but if you suspect that a software package isn't properly installed, use the rpm -V command to verify it. For example, to verify the kernel package, type the following:

```bash
rpm -V kernel
```

This command causes rpm to compare the size and other attributes of each file in the package against those of the original files. If everything verifies correctly, the rpm -V command does not print anything. If it finds any discrepancies, you see a report of them. For example, I have modified the configuration files for the Apache httpd web server. Here is what I type to verify the httpd package:

```bash
rpm -V httpd
```

Here's the result:

```
S.5....T c /etc/httpd/conf/httpd.conf
```

In this case, output from rpm -V tells me that a configuration file has changed. Each line of this command's output has three parts:

- - The line starts with eight characters; each character indicates the type of discrepancy found. For example, S means the size is different, and T means the time of last modification. Table 4-1 shows each character and its meaning. A period means that that specific attribute matches the original.
- * For configuration files, a c appears next; otherwise, this field is blank. That's how you can tell whether or not a file is a configuration file.
- * Typically, you don't worry if a configuration file has changed; you probably made the changes yourself.
- * The last part of the line is the full pathname of the file. From this part, you can tell exactly where the file is located.

| Table 4-1 Characters Used in RPM Verification Reports |
| Character | Meaning |
| --- | --- |
| S | Size has changed |
| M | Permissions and file type are different |
| 5 | Checksum computed with the MD5 algorithm is different |
| D | Device type is different |
| L | Symbolic link is different |
| U | File's user is different |
| G | File's group is different |
| T | File's modification time is different |

## Building Software Packages from Source Files

Many open-source software packages are distributed in source, without executable binaries. Before you can use such software, you have to build the binary. In this section, I show you how to build packages from source files.

### Downloading and unpacking the software

Open-source software files are typically distributed in compressed archives. These archives are created by the tar program and compressed with the gzip program. The distribution is in the form of a single file .tar.gz or .tarZ often referred to as a tarball. If you want the software, you have to download the tarball and unpack it.

Download the source files using anonymous FTP or through your Web browser. Save them in the /usr/local/src directory (be sure to log in as root; otherwise you cannot save in /usr/local/src). After downloading the compressed tar file, examine the contents with the following command:

```bash
tar ztf xmms*.gz | more
```

You see a listing similar to the following:

```
xmms-1.2.0/
xmms-1.2.0/int/
xmms-1.2.0/int/ChangeLog
xmms-1.2.0/int/Makefile.in
xmms-1.2.0/int/config.charset
xmms-1.2.0/int/locale.alias
xmms-1.2.0/int/ref-add.sin
xmms-1.2.0/int/ref-del.sin
xmms-1.2.0/int/gmo.h
xmms-1.2.0/int/getextP.h
xmms-1.2.0/int/hash-string.h
xmms-1.2.0/int/loadinfo.h
rest of the output not shown
```

The output of this command shows you what's in the archive and gives you an idea of the directories that are created after you unpack the archive. In this case, a directory named xmms-1.2.0 is created in the current directory, which, in my case, is /usr/local/src. From the listing, you also learn the programming language used to write the package.

To extract the contents of the compressed tar archive, type the following command:

```bash
tar xvf xmms*.gz
```

You see again the long list of files as you extract from the archive and copy to the appropriate directories on your hard drive.

Now you're ready to build the software.
