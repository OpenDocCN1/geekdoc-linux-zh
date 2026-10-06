
# Chapter 28 ✦ Emulation and Virtualization 721

## User Mode Linux UML Installation and Setup

There are a number of UML packages that need to be installed. In particular, you need to install the packages yast2-uml, um-host-kernel, um-host-install-initrd and uml-utilities. After this has been done, YaST will display an icon for the UML installation module in the Software section. Clicking this icon starts the UML installation for you, you need to set up a networked installation source offered over NFS from localhost (the copies of the installation DVD to a directory) and that directory to /etc/exports, restart the NFS server). A CD or DVD installation source will not work.

A new user is created for UML (the first user is called um0, with a home directory/um0). A virtual disk (a file called um0) for UML is created in this directory, and the UML kernel executable that is used to run the UML session is also placed in this directory. The packages are installed into the virtual hard disk (you may see a SUSE pop up in an xterm window). When the installation is complete, you can log in as the user um0 and run the executable (simply called linux) in that directory, the UML instance will start. You will see the boot messages appearing in an xterm window.

## FAUmachine Installation and Setup

After you have installed the FAUmachine packages, run the command faum. This starts a wizard that enables you to set up details of the virtual machine, and then you can start the machine itself. It boots in a graphical window. One of the major disadvantages of FAUmachine is whatever version of Linux you want to run as a guest, you need a specially modified boot loader and kernel; otherwise performance will be slow, if not gratis. SUSE offers a variety of these as special additional packages, but not for the current SUSE version. At the current time of writing, FAUmachine must be regarded more as an academic project than a practical way of running guest operating systems under Linux, but there are reasons to think that it may improve very quickly as time goes on.

## Other Emulators

SUSE provides a number of other open sources for legacy game systems and the like. These can be found in YaST's software selection: Package Groups ❖ System Emulators ❖ Other.

## The Kernel

The kernel is the heart of Linux; indeed, strictly speaking, the kernel is Linux — hence, the naming controversy. (Those who prefer the kernel GNU/Linux stress the fact that the system as a whole contains a Linux kernel and the GNU utilities.)

In this chapter we discuss the kernel in general and the SUSE kernel packages, and we explain how to configure and build a kernel. We also look at some of the problems involved with running third-party software that requires specific kernel versions.

## In This Chapter

- SUSE kernels and vanilla kernels
- Kernel packages
- Configuring and building the kernel
- Kernel modules
- Kernel parameters
- The initial ramdisk

## Why You Probably Don’t Need This Chapter

At one time, this would have been one of the most important chapters in the book. Knowing how to configure and recompile a kernel was a vital skill in the early years of Linux. It has changed for various reasons. The kernel is modular and vendors such as SUSE provide a kernel with anything you might need available as a module. This means that it is very unlikely you will need to configure and recompile to get support for some particular device; the support will already be there in the form of a loadable module. In most circumstances, SUSE will be unwilling to support you if you are not running the shipped kernel binaries.

Also, the relationship between the size of the kernel and the amount of memory on a system has changed beyond all recognition; the kernel has grown over the years, but amounts of memory have rocketed. This means that the old motivation for creating a minimal, monolithic kernel supporting your hardware (which used to be a common practice) is no longer a factor.

## Why You Might Need This Chapter

First of all, kernel configuration is interesting, and an understanding of the process is useful. You may have much occasion to rebuild the kernel provided by SUSE in order to make an unusual configuration change to get support for experimental or unusual features that are not allowed in the default configuration.

You might want to experiment with creating a monolithic kernel supporting the exact hardware on your system without loading anything as a module (although, as noted previously, this will not have a serious effect on performance).

You also might want to experiment with functionality that is available only in the form of kernel patches; to do this, you will first need to patch the kernel source and then rebuild it.

But it is only in unusual cases that you will need to put most of this into practice; usually the work has been done for you by the nice people at SUSE. Note that SUSE always provides experimental kernels as RPM packages (the "kernel of the day”).

## SUSE Kernels and Vanilla Kernels

Traditionally, the kernels shipped by SUSE and other commercial Linux vendors have always differed from the official kernels (often known as vanilla kernels) that are available from www.kernel.org. Exactly how much difference has there been varied with time. During the long period when the 2.4 kernel series was the stable kernel and extensive development was being done on the 2.5, a large number of 2.5 features were backported into SUSE's 2.4 kernels. The 2.4 kernels with various backported features were standard for a long time until version 9.0 Professional and SUSE Linux Enterprise (SLES) 8.

The first release of the 2.6 kernel was in December 2003. SUSE moved to the 2.6 kernel with SUSE Linux 9 and SLES 8. In SLES 9 on x86 are the packages kernel-bigmp, kernel-default, kernel-smp, and kernel-debug (and the specific user Linux kernels). SUSE Professional 9.3 and above offer the Xen kernels.

During the installation process, hardware detection ensures that a kernel package appropriate to your system is installed:

- For a machine with a single processor, that is the kernel-default package.
- For a multiprocessor machine, it is either kernel-smp or kernel-bigmp.
- The kernel debug package is not intended for production use but has all debugging options enabled.

Updated kernel packages are released often, for the purpose of adding functionality and to fix known problems including security issues. In the case of security issues, just as for other packages, details are available at www.suse.com/de/security/announcements/. Full details of updates for SLES can be found on the SUSE Linux Maintenance site at http://portal.suse.com/psdb/index.html.

## Version Numbers

A Linux kernel has a version number like 2.6.11.4-21.7. The convention is that the stable kernel has an even number. Thus 2.0, 2.2, 2.4, and 2.6 are stable series. The odd numbers represent the development series. At the time of writing, a 2.7 tree has not been opened. To find out what kernel you are currently running, use the command uname -r.

```
user: ~ uname -r
2.6.11.4-21.7-default
```

This corresponds to the package name kernel-default-2.6.11.4-21.7. So this is a 2.6.11.4 kernel with additional SUSE version information in the trailing digits.

## The Binary Kernel Packages

SUSE provides a choice of binary kernel packages: typically during installation the correct kernel will be automatically selected and installed. In SLES 9 on x86 are the packages kernel-bigmp, kernel-default, kernel-smp, and kernel-debug.

Each binary kernel package contains not only the kernel itself but also the additional files that are installed under /boot and the entire (very large) set of modules installed under /lib/modules/<version-number>/.

The kernel-sym package contains kernel symbol information for modules and is used to ensure that modules match the running kernel. The different kernels are all generated from the same source, as noted previously is a patched version of the vanilla sources.

