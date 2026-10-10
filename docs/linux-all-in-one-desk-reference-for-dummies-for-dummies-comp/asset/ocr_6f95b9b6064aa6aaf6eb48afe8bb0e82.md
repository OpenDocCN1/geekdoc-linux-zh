# Updating Linux Applications Online 465

To install a specific source RPM and build the application, follow these steps:

+   1.  **Mount the DVD-ROM by typing mount /media/cdrom or wait for the GNOME desktop to mount the DVD.**
+   2.  **Typically, source RPMs are in the SRPMS directory. Change to that directory by typing the following command:**
+       `cd /media/cdrom/SRPMS`
+   3.  **Install the source RPM file by using the rpm -i command. For example, to install the Web server (httpd) source, type**
+       `rpm -ivh httpd*.src.rpm`
+   4.  **Use the rpmbuild command with the spec file to build the software.**
+       You perform different tasks, from unpacking the source files to building and installing the binaries by using different options with the `rpmbuild` command. For example, to process the entire spec file, type:
+       `rpmbuild -ba packagename.spec`

The files install in the `/usr/src/redhat/SOURCES` directory. A spec file with a _.spec extension is placed in the `/usr/src/redhat/SPECS` directory. The spec file describes the software and also contains information used to build and install the software.

Here packagename is the name of the SRPM. This command typically builds the software and installs the binary files.

# Updating Linux Applications Online

Each of the Linux distributions — Debian, Fedora Core, MEPIS, SUSE, Ubuntu, and Xandros — come with utilities that enable you to update the software online. In the following sections, I provide an overview of the update methods in Debian, Fedora Core, MEPIS, SUSE, Ubuntu, and Xandros.

![](bbox=[0.12, 0.7, 0.2, 0.76])

You need a fast Internet connection (such as a DSL or cable modem) to easily update your Linux applications or download new software packages. Make sure that your Internet connection is up and running before you attempt to update your Linux system online.

# Keeping Debian, MEPIS, and Ubuntu updated with APT

![](bbox=[0.12, 0.85, 0.2, 0.91])

The best way to keep your Debian system updated is to use APT. More specifically, you use the `apt-get` command-line utility with appropriate options. Because MEPIS and Ubuntu are Debian-based, you can use APT to update MEPIS and Ubuntu as well.