
## Extra-Useful Files

I thought I would put one group of files together in this section. These are the files that anyone who is getting ready to upgrade their kernel should read or at least look through before doing so. These files are:

- *Changes*—This file contains a list of kernel resource Web sites. However, that is not what makes this file something to put under this section. The wonderful thing about the Changes file is that it includes a list of what version you need of all of the software that the kernel or building the kernel requires, and how to determine what version you have now. Further, it contains notes about what capabilities were updated in this particular kernel release.
- *Configure.help*—This file contains a list of every single kernel feature and driver that you can turn on or off during the kernel configuration process, along with a paragraph or more discussing what this feature does and who may or may not want to use it. If you are not sure whether you want to implement something, this is the place to look for further information.
- *devices.tex*, *devices.txt*—Both of these items are the same file. One is in TEX format, which is a markup language for laying out documents. The other is an ASCII text file. The devices file contains a list of all of the device numbers and files handled by the kernel.
- *inird.txt*—There is often confusion about the boot RAM disk you can create when compiling a new kernel. This file addresses what type of uses this RAM disk has and how to put them into practice.
- *kbuild*—This subdirectory contains files dealing with the kernel build process. Recommended reading.
- *proc.txt*—This file contains a discussion of the /proc section of the file system and what it contains.
- *sysctl*—This subdirectory contains files dealing with making changes to the /proc/sys/ files. If you think you might want to mess with these files, or want at least to understand what you might be able to do with them, read the file stored here.
- *sysrq.txt*—Many people do not know that they can turn on a set of key bindings that allows them to send commands directly to the kernel. Of course, you may not want to turn this on if others have access to the machine. Learn about the magic key bindings and why or why not to use them in this file.

## Miscellaneous Widgets

Some items defy easy categorization. Those files are listed here:

- *VGA-softcursor.txt*—How to alter your cursor in command line mode.
- *logo.gif*—The unofficial Linux logo.
- *logo.txt*—Explanation of logo.gif.
- *nbd.txt*—Discussion of the experimental network block device drivers.
- *nfsvroot.txt*—How to mount the root file system through an NFS mount on a diskless system. See Chapter 17 for information on NFS.
- *spinlocks.txt*—Discussion of making spinlocks efficient in both multi- and uniprocessor machines.
- *svga.txt*—Discussion of kernel-level video mode selection on 80x86 machines.
- *unicode.txt*—Discussion of how the kernel uses Unicode to refer to characters.
- *xterm-linux.xpm*—X pixel map of a penguin.

# Immediate Solutions

## Getting The Kernel's Version And Other System Information

The **uname** command allows you to get system information by choosing the appropriate flags. The flags available with **uname** are listed in Table 5.1.

**Table 5.1** Flags available with the **uname** command.

| Flag | Purpose |
| :--- | :--- |
| -a | Gives the information for all of the flags at once. |
| -m | Lists what architecture this machine is. |
| -n | Lists the machine's host name. |
| -p | Gives the machine's processor type. |
| -r | Gives the kernel version. |
| -s | Lists what operating system you are using. |
| -v | States when this operating system was installed. |

## Obtaining The Latest Kernel Source

It is important to get your kernel source from a trustworthy site. Some of the best places to get source from are:

- **www.kernelnote.org**
- **www.kernel.org**

**TIP:** If you want to know which version of the kernel you are currently running, type **uname -r**.

## Installing A New Kernel

Installing a new kernel, whether it is an upgrade or a newly compiled version of the one you already have, is a complex, but not intensely difficult, process. To add a new kernel, do the following:

1. Acquire the kernel source, either from one of the sites listed in the section “Obtaining The Latest Kernel Source” or from the distribution CD. For Red Hat 6.2, the Red Hat Package Manager (RPM) is kernel-source-2.2.14-50.i386.rpm.
2. Install the source. If you are not using an RPM, unpack the tarball in `/usr/src`.
3. There are certain packages you need to make sure are also installed. Here’s a list of them with Red Hat 6.2 version numbers included for the full file name:
    - *kernel-headers-2.2.14-50.i386.rpm*—Contains the header files for the kernel source
    - *cpp-1.1.2-30.i386.rpm*—The C preprocessor package used for compilation
    - *egcs-1.1.2-30.i386.rpm*—The C compiler
    - *glibc-devel-2.1.3-15.i386.rpm*—The C development library set
    - *make-3.77-6.i386.rpm*—The build manager you will utilize to compile the source
    - *ncurses-5.0-11.i386.rpm*—Necessary to control the cursor if you choose the **menuconfig** option to configure the kernel parameters
    - *ncurses-devel-5.0-11.i386.rpm*—Necessary to control the cursor if you choose the **menuconfig** option to configure the parameters
4. Change to the `/usr/src/linux-version` directory for the package. For Red Hat 6.2, this is `/usr/src/linux-2.2.14`.
5. Type “make oldconfig” to build a configuration file based on your current kernel settings. This is a good starting point if you do not want to risk forgetting to include things you have added already.
6. Choose which kernel configuration tool you want to use. See the following sections for your options: “Configuring The Kernel With **config**,” “Configuring The Kernel With **menuconfig**,” and “Configuring The Kernel With **xconfig**.”
7. Once you have chosen a kernel configuration tool, follow the instructions in the section that covers it as listed in Step 6, then go to Step 8.
8. Type “make dep” to build a list of source dependencies. See Chapter 22 for more on working with C source code.
    > *NOTE:* *Keep in mind that although each of these make steps is short to read, they can take several minutes or longer, depending on your CPU’s speed.*
9. Type “make clean” to clean out the temporary files used up to this point.
10. Type “make bzImage” to compile the base kernel.
11. Type “make modules” to compile the modules that the kernel will load on the fly.
12. The compiler places the kernel source in the directory /usr/src/linux/arch/i386/boot/bzImage. Copy this file into the /boot directory.
13. Rename /boot/bzImage to /boot/vmlinuz-version with the mv command, where version is the new kernel version you are in the process of installing.
14. Copy the file /boot/System.map to /boot/System.map-old.
15. Copy the file /usr/src/linux/System.map to the /boot directory.
16. Type “make modules_install” to install the modules to /lib/modules/version.
17. Although not necessary, it is a good policy to create a special boot version of the kernel containing modules that are needed by boot time hardware— for example, if your primary hard drive is SCSI. To do so, use mkinitrd /boot/initrd-version version.
18. Proceed to the section “Updating LILO” at the end of the chapter. You will not be able to boot with the new kernel until you tell LILO where to find it.

| Related solutions: | Found on page: |
| :----------------- | :-------------- |
| Opening Or Creating Tarballs | 110 |
| Installing RPMs | 114 |

## Configuring The Kernel With config

The config kernel configuration tool is entirely text-based with no bells and whistles. It takes some time to work through the entire configuration process, as config obtains the new kernel configuration by asking questions one at a time. Although an end user probably shouldn’t use this option, it is useful for system administrators to try it a few times just to get a feeling for how many choices they can make if they want to. Rather than provide a sample run-through, which is a
