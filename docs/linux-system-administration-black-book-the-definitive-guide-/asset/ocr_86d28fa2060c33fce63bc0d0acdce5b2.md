This method of managing kernel development can make selecting a kernel a confusing process. The important information to understand is how each kernel version is named, so you can choose the most appropriate options at a glance.

A kernel's name ends with a string of numbers in the format X.Y.Z. Each number is incremented as new features and bug fixes are added. X is the slowest to change; it could be years before there are kernels that begin with 3, for example. Deciding to change a major version number is a subjective act. Moving from a 2-based kernel to 3 would represent some kind of monumental advance. For example, when the version numbers jumped from 1 to 2, the following new items were added:

+   - Support for four new hardware architecture platforms (including Apple PowerPC and Atari)
+   - Additional IDE device drivers, better IDE error handling, autodetection of some IDE characteristics, and the ability to handle more controllers
+   - Additional SCSI device drivers
+   - Greatly expanded Ethernet card list
+   - The modern modular structure
+   - Advanced Power Management (APM) for devices such as laptop computers
+   - IP tunneling, masquerading, and additional routing capabilities
+   - ISDN support
+   - The VFAT and SMB file system support, among others
+   - File system quota support

Essentially, Linus Torvalds determines it is time to change the X kernel number when he feels that we are dealing with a brand-new starting point for kernel development.

The Y component changes on a semiregular basis, perhaps every six months or so. This is the crucial digit when determining whether the kernel is production or experimental. Experimental kernels have an odd-numbered Y component; for example, 2.3.12, 3.7.16, and 4.19.92. Production kernels, on the other hand, have an even-numbered Y component, such as 2.2.12, 3.8.16, or 4.20.92. The method for advancing this component is explained earlier in this section.

Perhaps the easiest to explain is the Z changes. Any time a change is made to the kernel code, the Z component advances. This method is used among most software developers. It is a way of knowing exactly what source code you are looking at. In fact, you may even see kernel versions in the format X.Y.Z-A. When you see this, you are looking at a version that was altered specifically for your Linux distribution.

For those who are more visually oriented, Figure 5.1 shows the full kernel development path and how the branches work out.