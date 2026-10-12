# Information Options

You can specify what information to display about queried packages. The following options are used to select the type of information for which you are searching:

+   * -i displays package information such as name, description, release, size, build date, install date, vendor, and other miscellaneous information.
+   * -l displays the list of files that the package “owns.”
+   * -s displays the state of all the files in the package.
+   * -d displays a list of files marked as documentation (man pages, info pages, READMEs, and so on).
+   * -c displays a list of files marked as configuration files. These are the files that you change after installation to adapt the package to your system (sendmail.cf, passwd, inittab, and so on).

For those options that display file lists, you can add -v to the query command to view the list in the familiar ls -l format.

Here’s an example of doing a more sophisticated query:

```
[scooby@cartoons]$ rpm -qi kernel
Name       : kernel                Relocations: (not relocatable)
Version    : 2.2.16    Build Date: Wed 26 Jul 2000 09:19:08 PM EST
Release    : 5.0
Install date: Sat 05 Apr 2000 08:44:13 AM EDT   Build Host: porky.redhat.com
Group      : System Environment/Kernel Source RPM: kernel-2.2.16-17.src.rpm
Size       : 15122940         License: GPL
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : The Linux kernel (the core of the Linux operating system).
Description:
The kernel package contains the Linux kernel (vmlinuz), the core of your
Red Hat Linux operating system. The kernel handles the basic functions
of the operating system: memory allocation, process allocation, device
input and output, etc.
```

For more details about using RPM, check out [scooby@cartoons]$ man rpm.

# Using Gnome-RPM

Red Hat Linux includes a very nice tool named Gnome-RPM that is also referred to as gnome RPM. Gnome-RPM is a Gnome-compliant GUI for the Red Hat package manager. With Gnome-RPM, you can easily perform many of the same package management tasks that are available to the command line.

![](bbox=[0.91, 0.11, 1.0, 0.23])