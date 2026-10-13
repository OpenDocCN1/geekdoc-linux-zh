
# Tip

The red hat-config-packages tool does not support kernel package installation. You have to install the kernel package manually using the rpm command in a terminal window.

If you are customizing the kernel, installing the source code and headers for the kernel is also essential. You need the source code to generate any modules and tailor the kernel to your own needs. For example, you can use the source code to generate modules containing device drivers for any uncommon devices you may have installed, as shown here:

```
# rpm -Uvh kernel-source-2.4.22-1.2115.nptl.i386.rpm
```

On most distributions, kernels are installed in the /boot directory. Performing an ls -l operation on this directory lists all the currently installed kernels. A file for your old kernel and a file for your new one now exist, as well as a link file called vmlinuz that links to the new kernel file. If you took the precautions described in the preceding section, you may have already renamed the older kernel. If you are using a boot loader such as GRUB, you needn't change its configuration file (grub.conf), because the entry to invoke the kernel still references the /boot/vmlinuz link, which now points to the new kernel. The kernel boots using the /boot/vmlinuz link to the kernel file. In your grub.conf file, the kernel line for the kernel file references this link. You also need to include a line for the RAM disk, initrd.

```
kernel /boot/vmlinuz-2.4.22-1.2115.nptl ro root=/dev/hda 3
initrd /boot/initrd-2.4.22-1.2115.nptl.img
```

# Tip

Although it is not included with Red Hat 10, user-mode Linux (UML) is an optional version of the kernel designed to run as a standalone program separate from the kernel. In effect, it

![](img/32a48d8db4c23e6e2eb70d1e5034c976_794_0.png)

# Precautionary Steps for Modifying a Kernel of the Same Version

If you want to modify your kernel configuration and build a new one, you should retain a copy of your current kernel. In case something goes wrong with your modified version, you can always boot from the copy you kept. You do not have to worry about this happening if you are installing a new version of the kernel. New kernels are given different names, so the older one is not overwritten.

To retain a copy of your current kernel, you can make a backup copy of it, letting the original be overwritten. An installed version of a kernel makes use of several files in the /boot directory. Each file ends with that kernel version's number. These include the vmlinuz file, which is the actual kernel image file, along with several support files, System.map, config, and module-info. This System.map file contains kernel symbols needed by modules to start kernel functions. For example, the kernel image file is called vmlinuz-version, where version is the version number attached, as in vmlinuz-2.4.22-1. The System.map file for this kernel called System.map-2.4.22-1. Here are the kernel files for version 2.4.22-1.

```
/boot/vmlinuz-2.4.22-1
/boot/System.map-2.4.22-1
/boot/module-info-2.4.22-1
/boot/config-2.4.22-1
```

The vmlinuz, System.map, and module-info files for a particular kernel also have symbolic links using those names without the version number. For example, vmlinuz is a link to the current kernel image file-in this case, vmlinuz-2.4.22-1 and System.map is a link to the current System.map file, System.map-2.4.22-1. When you install a new kernel, the links are changed to that kernel. So if you installed a new version, such as 2.4.22-10, the /boot/vmlinuz would then link to that kernel's vmlinuz file, /boot/vmlinuz-2.4.22-10.

```
/boot/vmlinuz          /boot/vmlinuz-2.4.22-1
/boot/System.map       /boot/System.map-2.4.22-1
/boot/module-info      /boot/module-info-2.4.22-1
```

If, on the other hand, you are creating a modified version of the same kernel, the kernel file, here called vmlinuz-2.4.22-1, will be overwritten with the new kernel image file, along with the System.map and module-info files. To keep your current working version, you first have to make a copy of these files. You would make a copy of the /boot/vmlinuz-2.4.22-1 file, giving it another name, as shown here:

```
cp /boot/vmlinuz-2.4.22-1 /boot/vmlinuz-2.4.22-1.old
```

You would also make a backup of the System.map and module-info files. The System.map file is a symbolic link to the System.map-2.4.22-1 file. You should also back up your modules located in the /lib/modules/version directory, where version is the version number of the kernel. Otherwise, you will lose the modules already set up to work with the original kernel. For version 2.4.22-1, the libraries are located in /lib/modules/2.4.22-1. If you are compiling a different version, those libraries are placed in a new directory named with the new version number.

## Boot Loader

If you are using a boot loader, you should create a new entry for the old kernel in the boot loader configuration file. You can then make an entry for the new kernel. Leaving the entry for the old kernel is advisable in case something goes wrong with the new kernel. This way, you can always reboot and select the old kernel. For example, in grub.conf, add a new entry, similar to the one for the old kernel, which references the new kernel in its kernel statement. The grub.conf entry would look something like the following code. You could then select the entry with the title "Old Linux (2.4.22-1.old)" at the GRUB menu to launch the old kernel.

```
title Old Linux (2.4.22-1.old)
    root (hd0,2)
    kernel /boot/vmlinuz-2.4.22-1.old root=/dev/hda3
    initrd /boot/initrd-2.4.22-1.old.img
```

If you use a label for the boot partition, the `root` option for the `kernel` statement would look like this for a boot partition labeled /:

```
kernel /boot/vmlinuz-2.4.22-1.old ro root=LABEL=/
```

## Boot Disk

You should also have a boot disk ready, just in case something goes wrong with the installation (normally you created one during installation). With a boot disk, you can start your system without using the boot loader. You can create a boot disk using the `mkbootdisk` utility. To create a boot disk, you need to know the full version number for your kernel. You can, in fact, have several kernels installed, and create boot disks for each one (your `grub.conf` file lists your kernel version number). If the kernel version is 2.4.22-1, use it as the argument to the `mkbootdisk` command to create a boot disk for your system:

```
mkbootdisk 2.4.22-1
```

If you want to make a boot CD-ROM, you can use the `--iso` option with the `--device` option to specify the CD image file. You can then burn the image file to a CD-ROM disk. In the next example, the user creates a CD-ROM image file, called `myimage.iso`, for a boot CD-ROM of the 2.4.22-1 kernel:

```
mkbootdisk --iso --device myimage.iso 2.4.22-1
```

## Compiling the Kernel from Source Code

Instead of installing already compiled binary versions of the kernel, you can install the kernel source code on your system and use it to create the kernel binary files yourself. Kernel source code files are compiled with the gcc compiler just as any other source code files are. One advantage to compiling the kernel is that you can enhance its configuration, adding support for certain kinds of devices such as Bluetooth devices. The 2.4 kernel is described here.

### Installing Kernel Sources: Kernel Archives and Patches

You can obtain a recent version of the kernel source code from your distribution. It will have the name kernel-source. New versions can be downloaded with your distribution update agent, or by directly accessing the distribution's FTP site. As noted previously, you simply install them as you would any RPM package.

```
# rpm -ivh kernel-source-2.4.22-1.2115.nptl.i386.rpm
```

The source files are placed in the /usr/src directory, within the subdirectory that has the prefix linux and a suffix consisting of the kernel version, as in linux-2.4.22-1 for kernel 2.4, revision 20, patch 8. The full directory will be /usr/src/linux-2.4.22-1. When you download and install a new kernel, a separate subdirectory is created for it. For example, the 2.4.22-1 kernel is placed in /usr/src/linux-2.4.22-1. A link is created called /usr/src/linux-2.4 that links to the most recent kernel source directory that you installed. You can use this link to access your most recent kernel source. Originally, this would link to /usr/src/linux-2.4.22-1. If you later installed the 2.5.67 kernel, this would link to /usr/src/linux-2.5.67.

You can also obtain the most recent version of the source code from www.kernel.org. These versions are normally much more recent than those available on your distribution site, but they may not have been thoroughly tested on the distribution platform. The kernel source is in the form of compressed archives (.tar.gz). They have the prefix linux with the version name as the suffix. You decompress and extract the archive with the following commands. You first change to the /usr/src directory and then unpack the archive. It creates a directory called linux where the source files are placed. The following example extracts the 2.4.22-1 kernel:

```
cd /usr/src
tar -xzvf linux-2.4.22-1.tar.gz
```

Be sure to unpack the archive in the /usr/src directory. The archive extracts a directory named linux that holds the source code files. This way, the files are located in the /usr/src/linux directory. You should rename this directory, adding the kernel version, as Red Hat does, /usr/src/linux-2.4.22-1.

Tip If you are using the original kernel source, you should also check for any patches.

### Configuring the Kernel

Once the source is installed, you must configure the kernel. Configuration consists of determining the features for which you want to provide kernel-level support. These include drivers for different devices, such as sound cards and SCSI devices. You can configure features as directly included in the kernel itself or as modules the kernel can load as needed. You can also specifically exclude features. Features incorporated directly into the kernel make for a larger kernel program. Features set up as separate modules can also be easily updated. Documentation for many devices that provide sound, video, or network support can be found in the /usr/share/doc directory. Check the kernel-doc package to find a listing of the documentation provided.

```
rpm -ql kernel-doc
```

Note If you configured your kernel previously and now want to start over from the default settings, you can use the make mrproper command to restore the default kernel configuration.

### Kernel Configuration Tools
