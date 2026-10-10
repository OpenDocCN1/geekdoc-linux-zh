# About the Media

+   1. Insert the CentOS 5 Live CD into your CD drive and reboot.
+   2. From the boot screen, either let the CD time out and boot or press any key to see other selections. From the boot menu, highlight “Boot” and then press [Enter].
+   3. When you see the login screen, you can select a language or just let the login prompt time out. (No password is required.) The GNOME desktop starts up.

# What’s on the Media

The following sections provide a summary of the software and other materials you’ll find on the media that accompany this book.

# Operating System and Applications

The Live CD provides a version of CentOS 5 that you can test-drive on a 32-bit, x86-compatible computer system. The installation DVD provides the necessary installation and software packages to install CentOS on a new system or as an alternate operating system on an existing computer system. You can install it as an alternate operating system by either repartitioning your disk to provide a partition where CentOS Linux can be installed directly, or as an alternate operating system on an existing Microsoft Windows system that has at least 4 GB of free space without repartitioning.

# Source Code

From time to time, you may want to recompile the Linux kernel or other software package that comes with CentOS. Like the binary software packages, the source code packages are available (http://soredirect.centos.org/centos/5/os/SRPMS/). To work with CentOS source code packages, here is what you need:

+   ■ kernel-devel — The kernel-devel package comes with the CentOS binary packages. Included in the package name is the version number of the kernel it contains. The source code for the current kernel is contained in the /usr/src/kernels directory, ready to be recompiled, if the kernel-devel package is installed.
+   ■ SRPMS Directory — Source code for each binary package outside of the kernel that is included in CentOS is available from any CentOS repository. Install the source code package for the software that interests you (the name ends in .src.rpm) and a copy of that software in subdirectories of the /usr/src/redhat directory.

To do the actual compilations, you will need to install at least the gcc package.