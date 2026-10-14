
## ypbind — (Version 3.3, 48K)

[W][S]

The Network Information Service (NIS) is a system which provides network information (login names, passwords, home directories, group information) to all of the machines on a network. NIS can enable users to login on any machine on the network, as long as the machine has the NIS client programs running and the user's password is recorded in the NIS passwd database. NIS was formerly known as Sun Yellow Pages (YP). This package provides the ypbind daemon. The ypbind daemon binds NIS clients to an NIS domain. Ypbind must be running on any machines which are running NIS client programs. Install the ypbind package on any machines which are running NIS client programs (included in the yp-tools package). If you need an NIS server, you'll also need to install the ypserv package to a machine on your network.

## ypserv — (Version 1.3.6.91, 289K)

The Network Information Service (NIS) is a system which provides network information (login names, passwords, home directories, group information) to all of the machines on a network. NIS can enable users to login on any machine on the network, as long as the machine has the NIS client programs running and the user's password is recorded in the NIS passwd database. NIS was formerly known as Sun Yellow Pages (YP). This package provides the NIS server, which will need to be running on your network. NIS clients do not need to be running the server. Install ypserv if you need an NIS server for your network. You'll also need to install the yp-tools and ypbind packages onto any NIS client machines.

## Kernel

This section contains packages that are related to the Linux kernel on which Red Hat Linux is based.

## kernel — (Version 2.2.5, 9,812K)

[B]

The kernel package contains the Linux kernel (vmlinuz), the core of your Red Hat Linux operating system. The kernel handles the basic functions of the operating system: memory allocation, process allocation, device input and output, etc.

## kernel-BOOT — (Version 2.2.5, 5,881K)

This package includes a trimmed down version of the Linux 2.2.5 kernel. This kernel is used on the installation boot disks only and should not be used for an installed system, as many features in this kernel are turned off because of the size constraints.

## Appendix C: Package List

## kernel-pcmcia-cs — (Version 2.2.5, 561K)
[B]

Many laptop machines (and some non-laptops) support PCMCIA cards for expansion. Also known as "credit card adapters," PCMCIA cards are small cards for everything from SCSI support to modems. PCMCIA cards are hot swappable (i.e., they can be exchanged without rebooting the system) and quite convenient to use. The kernel-pcmcia-cs package contains a set of loadable kernel modules that implement an applications program interface, a set of client drivers for specific cards and a card manager daemon that can respond to card insertion and removal events by loading and unloading drivers on demand. The daemon also supports hot swapping, so that the cards can be safely inserted and ejected at any time. Install the kernel-pcmcia-cs package if your system uses PCMCIA cards.

## kernel-smp — (Version 2.2.5, 9,494K)

This package includes a SMP version of the Linux 2.2.5 kernel. It is required only on machines with two or more CPUs, although it should work fine on single-CPU boxes.

## modutils — (Version 2.1.121, 841K)
[B]

The modutils packages includes the kerneld program for automatic loading of modules under 2.0 kernels and unloading of modules under 2.0 and 2.2 kernels, as well as other module management programs. Loaded and unloaded modules are device drivers and filesystems, as well as other things.

## Libraries

This section contains the packages associated with the libraries that are required to run programs under Red Hat Linux.

## XFree86-libs — (Version 3.3.3.1, 2,060K)
[W][S]

XFree86-libs contains the shared libraries that most X programs need to run properly. These shared libraries are in a separate package in order to reduce the disk space needed to run X applications on a machine without an X server (i.e, over a network). If you are installing the X Window System on your machine, you will need to install XFree86-libs. You will also need to install the XFree86 package, the XFree86-75dpi-fonts package or the XFree86-100dpi-fonts package (depending upon your monitor's resolution), the Xconfigurator package and the X11R6-contrib package. And, finally, if you are going to be developing applications that run as X clients, you will also need to install XFree86-devel.
