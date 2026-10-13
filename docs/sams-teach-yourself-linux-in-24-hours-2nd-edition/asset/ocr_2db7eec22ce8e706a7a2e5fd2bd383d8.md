# Managing Linux Software with rpm, lisa, and kpackage

Software installation and removal under OpenLinux is accomplished with the Red Hat Package Manager, or rpm command. The rpm command works by using software packages and databases of installed software for your system under the /var/lib/rpm directory. A software package is an archive of files, information, and scripts used before and after files are decompressed and saved into your file system. The rpm command, its databases, and the format of the software packages are the backend system for front-end utilities such as lisa and the kpackage client.

This section introduces you to the rpm command and then shows you how to use the kpackage client and the lisa command to install or remove software.

# Using the rpm Command

You use the rpm command to install, query, upgrade, uninstall, and verify software. What makes rpm so handy is that you can use it to easily track what software is installed and which version of a software package is installed and then upgrade the software package, and if desired, uninstall the software—all with a single command line!

The rpm command has many different command-line options, but most users will only use five of its options, or modes:

+   - -i, or install
+   - -e, or uninstall
+   - -q, or query
+   - -U, or upgrade
+   - -V, or verify

To install a software package (usually with a filename ending in .rpm), use the -i option, followed by the name of a software package. Software package names usually include the name of the program, its version, what computer platform the software is designed for, and an .rpm extension. You must be logged in as the root operator or have root permission before installing or removing software. For example, to install the taper backup software package from your OpenLinux CD-ROM, insert and mount the CD-ROM and then use rpm:

```
# rpm -i /mnt/cdrom/Packages/RPMS/taper-6.8.2-2.1386.rpm
```