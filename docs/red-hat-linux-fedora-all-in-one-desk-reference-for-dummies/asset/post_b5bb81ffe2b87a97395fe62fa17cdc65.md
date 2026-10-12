
![](img/a7eec43a54473e95dc5ea333fecf1bd7_520_0.png)

When you install a new kernel RPM, the installation process creates a new initial RAM disk image — a file that the kernel can copy into a block of memory and use as a memory-resident disk. That file's name begins with initrd (initrd is shorthand for initial RAM disk) and has the kernel version number in the filename. The kernel RPM installation also adds a description of the kernel to the GRUB configuration file — /etc/grub.conf. For example, here is a typical GRUB configuration file after I installed a new kernel RPM:

```
title Red Hat Linux (2.4.20-8)
root (hd0,2)
kernel /vmlinuz-2.4.20-8 ro root=LABEL=/
initrd /initrd-2.4.20-8.img
title Red Hat Linux (2.4.20-6)
root (hd0,2)
kernel /vmlinuz-2.4.20-6 ro root=LABEL=/
initrd /initrd-2.4.20-6.img
```

Next time you reboot the system, these two kernels would appear as choices in the GRUB boot screen. From that screen you can select which kernel you want to boot.

## Trying out the new kernel

After installing the new kernel RPM, creating the initial RAM disk file, and reconfiguring GRUB, it's time to try the new kernel. To restart the system, log in as root and type the following command from the Linux prompt:

```
reboot
```

You may also reboot the system from the graphical login screen. Select Reboot from the Options menu on the login dialog box.

When the system reboots and you see the GRUB screen, press the arrow key to select the new kernel's name.

After Red Hat Linux starts, you should see the usual graphical login screen. Log in as a user, open a terminal window, and type the uname -sr command to see the version number. The response should show that your system is running the new version of the kernel.

## Rebuilding the Kernel

Rebuilding the kernel refers to creating a new binary file for the core Linux operating system. This binary file is the one that runs when Red Hat Linux boots. You may wonder why you would ever want to rebuild the kernel. Well, here are a few reasons:

- After you initially install Linux, you may want to create a new kernel that includes support for only the hardware installed on your system. In particular, if you have a SCSI adapter, you may want to create a kernel that links in the SCSI driver. The kernel in the companion DVD includes the SCSI driver as an external module you load at startup.
- If you have a system with hardware for which only experimental support is available, you have to rebuild the kernel to include that support into the operating system.
- You may want to recompile the kernel and generate code that works well on your specific Pentium processor (instead of the generic 386 processor code that comes in the standard Red Hat Linux distribution).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_521_0.png)

Never rebuild and install a new kernel without first making sure you have an emergency boot floppy. If you do have an emergency boot floppy, use the mkbootdisk command to create the boot floppy. Type man mkbootdisk to learn the syntax of that command. The exact command line to build the emergency boot floppy depends on the kernel version number. For example, to create a boot floppy for version 2.4.20-8, log in as root and type the following command in a terminal window (you have to insert a blank floppy disk when prompted):

```
mkbootdisk -device /dev/fd0 2.4.20-8
```

Replace 2.4.20-8 with the version number of your Linux kernel (type the uname -r command to see the version number).

To rebuild the Linux kernel, you need the kernel source files. The kernel source files are not normally installed. Use the following steps to install the kernel source files on your system:

- 1. Log in as root and insert the Red Hat Linux DVD-ROM into the DVD drive.
- 2. If the DVD drive does not mount automatically, type the following command to mount the DVD drive:
  `mount /mnt/cdrom`
  If you're using GNOME or KDE, the DVD is automatically mounted, and you should not have to perform this step manually.
- 3. Change the directory to the RedHat/RPMS directory on the DVD, and use the rpm command to install the kernel source files. Type the following commands:
  `cd /mnt/cdrom/RedHat/RPMS`
  `rpm -ivh kernel-source*`
  After the rpm command finishes installing the kernel source package, the source files appear in the /usr/src/linux-2.4 directory.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_522_0.png)

If you cannot find the `kernel-source` RPM on this book's DVD, you have to download that file from one of the mirror sites listed at www.redhat.com/download/mirror.html. Click the Distribution link next to one of the listed FTP sites and then look in the directory corresponding to the Red Hat Linux version number. For example, the RPM files for Red Hat Linux 9 should be in the `9/en/os/i386/RedHat/RPMS` directory. Use a Web browser to download the `kernel-source` RPM file and install it by following the previous steps.

Building the kernel involves the following phases:

- Configuring the kernel
- Building the kernel
- Building and installing the modules (if any)
- Installing the kernel and setting up GRUB

I explain these phases in the next few sections, but first you should know the difference between linking in a driver vs. building a driver as a loadable module.

## Creating a monolithic vs. a modular kernel

You have two options for the device drivers needed to support various hardware devices in Linux:

- **Link in support:** You can link the drivers for all hardware on your system into the kernel. The size of the kernel grows as device driver code is incorporated into the kernel. A kernel that links in all necessary code is called a *monolithic kernel* because it's one big file.
- **Use modules:** You can create the device drivers in the form of loadable modules. A *module* is a block of code the kernel can load after it starts running. A typical use of modules is to add support for a device without having to rebuild the kernel for each new device. Modules don't have to be device drivers; they can also add new functionality to the kernel. A kernel that uses modules is called a *modular kernel*.

You don't have to create a fully monolithic or fully modular kernel. In fact, it's common practice to link some support directly into the kernel but build infrequently used device drivers in the form of modules. For a company such as Red Hat, it makes sense to distribute a modular kernel. Red Hat provides a generic kernel, along with a large number of modules that can support many different types of hardware. Then the Red Hat installer configures the system to load only modules that are needed to support the hardware installed in a user's system.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_523_0.png)

When you create a custom kernel for your hardware configuration, you may want to link all required device drivers into the kernel. You can keep the size of such a monolithic kernel under control because you link in device drivers only for the hardware installed on your system.

## Configuring the kernel

The first phase in rebuilding a kernel is to configure it. To configure the kernel, log in as root. Then change the kernel source directory by using the cd command as follows:

```
cd /usr/src/linux*
```

To configure the kernel, you have to indicate which features and device drivers you want to include in your Linux kernel. In essence, you build your very own version of the Linux kernel with just the features you want.

Red Hat Linux provides several ways for you to configure the kernel:

- Type make menuconfig to enter the kernel-configuration parameters through a text-based interface similar to the one the Red Hat installation program uses.
- Type make xconfig to use an X Window System-based configuration program to configure the kernel. You have to run X to use this configuration program with a graphical interface.
- Type make config to use a shell script that prompts you for each configuration option one by one. You can use this configuration program from the Linux command prompt. When you use this option, you undergo a long question-and-answer process to specify the configuration parameters. For each question, respond with a y to link support into the kernel, m to build a module, and n to skip the support for that specific device.

The make menuconfig, make xconfig, and make config commands achieve the same end result — each stores your choices in a text file named .config located in the /usr/src/linux* directory. Because the filename starts with a period, you don't see it when you use the ls command alone to list the directory. Instead, type ls -a to see the .config file in the directory listing.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_523_1.png)

The kernel configuration step merely captures your choices in the .config file. (In fact, the .config file does not exist until you configure the kernel once.) The kernel file does not change until you compile the kernel with the make command. That means you can go through the kernel configuration option as many times as you want. If you want to start over with default settings, type the following command before you start configuring the kernel:

```
make mrproper
```
