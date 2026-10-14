# SOFTWARE REQUIREMENTS–DSL VERSIONS

Damn Small Linux is available in several different versions. The version you use depends on the environment in which you are running DSL. The four versions DSL offers include:

+   - **A SYSLINUX version**—Used for older PCs that require the boot medium to be no larger than a floppy image (even if that image is on a CD). For more information on the SYSLINUX boot loader, refer to the SYSLINUX FAQ (http://syslinux.zytor.com/faq.php).

+   - **An ISOLINUX version**—Used most often for booting live CDs, because it needs no special floppy emulation disk. For more information on the ISOLINUX boot loader, refer to the ISOLINUX FAQ (http://syslinux.zytor.com/iso.php).

+   - **A Qemu Virtual Machine version**—Sets up Qemu to run DSL virtually within a running Linux system.

+   - **A VMware Virtual Machine version**—Sets up VMware to run DSL virtually within a running Windows system.

The first two versions concern booting from the CD, which is the topic of this chapter. The other two versions are discussed in Chapter 7, “Running DSL Embedded in Windows.” Why are there two versions for CD? Because DSL targets older and smaller hardware, many such systems could only boot from a CD if there existed an actual emulated boot floppy. This emulated boot floppy was restricted to the size of a real floppy. Later machines were made without such a restriction.

So, the first rule is this: If your machine cannot begin the boot process, or if your machine is an older variety, use the SYSLINUX version.

The SYSLINUX version of DSL emulates a single floppy at boot time. There are fewer drivers in the SYSLINUX version because they must all fit within a single floppy-sized file. The reason Knoppix and the other derivatives went with ISOLINUX is that there is no single floppy size limitation. The ISOLINUX version has many more drivers to support booting from newer computers.

# GETTING DAMN SMALL LINUX

There are several versions of Damn Small Linux included on the CD that comes with this book. You can read about what those versions are and how to use them by referring to Appendix A, “On the CD.” However, if you don’t have the CD handy or if a later version of DSL is available, you might consider downloading a copy of DSL to make your own bootable CD.