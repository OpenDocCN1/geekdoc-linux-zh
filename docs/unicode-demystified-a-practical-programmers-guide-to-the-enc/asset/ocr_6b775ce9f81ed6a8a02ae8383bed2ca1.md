# Locating Source Code

When the kernel source is on your system, the /usr/src directory will look something like the following:

```
$ ls -l /usr/src
total 8
rwxr-xr-x 1 root root 15 Oct 03:15 linux-2.4 -> linux-2.4.18-14
drwxr-xr-x 17 root root 4096 Oct 03:14 linux-2.4.18-14
drwxr-xr-x 1 root root 4096 Oct 01 03:28 redhat
```

The usual setup has a longer, descriptive name in the directory that contains the kernel source and a shorter name that points to the directory with the longer name. In the preceding example the name linux-2.4.18-14 means that the directory contains version 2.4 of the Linux kernel, release 18-14. The name linux-2.4 always points to the version of the kernel that you are running or building. Before you make sure that /usr/src/linux-2.4 points to the new release. If the source code is present on your system, skip to “Cleaning the Source Tree” on page 1034.

# Installing Source Code

When the source is not present on your system, you need to find it on the installation CD-ROM set or on the Red Hat Web Site. You need kernel-source*.rpm. The kernel used in the examples came from kernel-source-linux-2.4.18-i386.rpm. You need to work as root to use rpm to install the kernel package.

Once you have located the kernel-source rpm package, give an rpm command to install it. The following command installs the kernel-source rpm package from the directory that contains the package (refer to “rpm: Red Hat Package Manager” on page 928 for more information on using rpm):

```
$ rpm -ivh kernel-source*.rpm
```

# Read the Documentation

The kernel package includes the latest documentation, some of which may not be available in other documents. Review the README file and the relevant files in the Documentation directory. Read the Linux Kernel-HOWTO for an excellent, detailed guide to installing and configuring the Linux kernel.

Always have Appendix A: Building a Custom Kernel of the Red Hat Customization Guide in front of you as you proceed (on the Red Hat documentation-ROM and at www.redhat.com/docs/manuals/linux).

> 37. With Red Hat version 7.2 and earlier, you must also install the kernel-headers*.rpm file.