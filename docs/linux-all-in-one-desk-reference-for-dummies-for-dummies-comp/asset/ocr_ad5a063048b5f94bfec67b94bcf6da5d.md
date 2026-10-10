# # Rebuilding the Kernel

*Rebuilding the kernel* refers to creating a new binary file for the core Linux operating system. This binary file is the one that runs when Linux boots.

You may wonder why you would ever want to rebuild the kernel. Well, here are a few reasons:

+   - After you initially install Linux, you may want to create a new kernel that includes support for only the hardware installed on your system. In particular, if you have a SCSI adapter, you may want to create a kernel that links in the SCSI driver. The kernel on the companion DVD-ROM includes the SCSI driver as an external module that the kernel loads at startup.
+   - If you have a system with hardware for which only experimental support is available, you have to rebuild the kernel to include that support into the operating system.
+   - You may want to recompile the kernel and generate code that works well on your specific Pentium processor (instead of the generic 386 processor code that comes in most Linux distributions).

To rebuild the Linux kernel, you need the kernel source files. The kernel source files are not normally installed. Use your distribution's software installation tool to install the kernel source package.

Fedora Core does not provide the *kernel-source* package. Instead, you have to install the source RPM (SRPM) file *kernel-version.src.rpm* where *version* is the kernel version number. You can find the kernel SRPM in the SRPMS directory of a Fedora Core online repository. You have to install the kernel SRPM with the command `rpm -Uvh kernel-version.src.rpm`. Then type `cd /usr/src/redhat/SPECS` followed by `rpmbuild -bp --target $arch kernel.spec`. To make the kernel sources available at the `/usr/src/linux` directory, type the following commands. (Replace *version* with the version number of the kernel that you can get with the `uname -r` command.)

```
```
cd /usr/src/redhat/BUILD/kernel-VERSION/usr/src/
mv linux-VERSION /usr/src/
cd /usr/src/
ln -s ./linux-VERSION linux
```
```

In SUSE, use YaST's Software Management tool to install the kernel sources — to find it, use the search feature (search for *kernel-source*) in YaST’s software installation window. After installing the kernel-source package, the source files appear in the `/usr/src/linux-version` directory, where *version* is the version number of the kernel. Thus, for kernel version 2.6.13, the source files are in the `/usr/src/linux-2.6.13` directory. Some distributions automatically set up `/usr/src/linux` as a symbolic link (shortcut) to the version-specific directory containing the source files for the Linux kernel.