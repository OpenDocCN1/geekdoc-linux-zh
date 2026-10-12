
If you have a system with hardware not supported when you installed Red Hat Linux or for which only experimental support was available, you can rebuild the kernel to include that support once it becomes available.

![](img/5fe8f856723cde0b366f73584b9e64b8_267_0.png)

Before you rebuild the kernel, make sure you have the emergency boot floppy that you prepared when installing Red Hat Linux (covered in Session 1). If the system does not boot after you rebuild the kernel, you can use that emergency boot floppy to start the system using a known good kernel.

![](img/5fe8f856723cde0b366f73584b9e64b8_267_1.png)

Never rebuild and install a new kernel without first making sure that you have an emergency boot floppy. If you did not create the boot floppy during Red Hat Linux installation, use the /sbin/mkbootdisk command to create the boot floppy. Type man mkbootdisk to learn the syntax of that command.

Rebuilding the kernel involves the following steps:

1. Installing kernel source code.
2. Configuring the kernel.
3. Building the kernel.
4. Building and installing kernel modules (if any).
5. Installing the kernel and setting up LILO.

The rest of this session describes these steps in greater detail.

## Installing the Kernel Source Code

To rebuild the Linux kernel, you need the kernel source code, which is usually not installed. So, follow these steps to install it on your system:

1. Log in as root and insert the Red Hat Linux CD-ROM (disk 2) into the CD-ROM drive.
2. Use the mount command to mount the CD-ROM drive on a directory in the file system, as shown here:
   ```
   mount /mnt/cdrom
   ```
3. Change the directory to the RedHat/RPMS directory on the CD-ROM and use the following commands to install the kernel source files:
   ```
   cd /mnt/cdrom/RedHat/RPMS
   rpm -ivh kernel-source*
   ```
   Preparing...
   ######################################## [ 100%]
   1: kernel-source
   ######################################## [100%]

The installation might appear to proceed slowly because the kernel source code RPM is over 20MB in size. After RPM finishes installing the kernel source package, the necessary source files appear in the `/usr/src/linux-2.4` directory.

You have two options for the device drivers needed to support various hardware devices in Linux:

- **Link in support.** You can build the drivers for all hardware on your system into the kernel. As you can imagine, the size of the kernel grows as the device driver code is incorporated into the kernel. A kernel that includes all necessary support code is called a **monolithic kernel**.
- **Use modules.** You can create the necessary device drivers in the form of modules. A **module** is a block of code that the kernel can load after it starts running. You typically use modules to add support for a device without having to rebuild the kernel for each new device. Modules do not have to be device drivers; you can use them to add new functionality to the kernel. A kernel that uses modules is called a **modular kernel**.

You do not have to create a fully monolithic or fully modular kernel. In fact, it is common practice to link some support directly into the kernel. Conversely, you can build infrequently used device drivers in the form of modules. For a company such as Red Hat, it makes sense to distribute a modular kernel. Red Hat provides a generic kernel along with a large number of modules to support many different types of hardware. The installation program configures the system to load only those modules needed to support the hardware installed in a user's system.

## Configuring the Kernel

The first phase in rebuilding a kernel is configuring the kernel. To configure the kernel, log in as **root**. Then change the directory to `/usr/src/linux` by using the `cd` command as follows:

```
cd /usr/src/linux-2.4
```

Red Hat Linux provides three ways for you to configure the kernel:

- Type **make xconfig** to use an X Window System-based configuration program to configure the kernel. You have to run **X** to use this tool.
- Type **make menuconfig** to enter the kernel configuration parameters through a text-based menu interface.
- Type **make config** to use a text-based program that prompts you for each configuration option one by one. When you use this option, you undergo a long question-and-answer process to specify the configuration parameters.

To configure the kernel, you select the features and device drivers that you want to include in your Red Hat Linux system. In essence, you build a copy of Linux that mixes and matches the features you want.

As you configure the kernel, you have to select how to include support for specific devices. For most configuration options, you must type one of the following choices:

- y to build support into the kernel
- m to use a module
- n to skip the support for that specific device
- ? to get help on that kernel configuration option

If a device does not have a modular device driver, you do not see the m option. For some configuration options, you may have to type a specific answer. For example, when responding to the processor type, you type Pentium to indicate that you have a Pentium PC.

The make menuconfig, make xconfig, and make config commands achieve the same end result—each stores your choices in a text file named .config located in the /usr/src/linux directory. Because the filename starts with a period (.), you don't see it when you use the ls command alone to list the directory. Instead, type ls -a to see the .config file in the directory listing.

![](img/5fe8f856723cde0b366f73584b9e64b8_269_0.png)

> All that the kernel configuration step does is capture your choices in the .config file. The kernel file does not change until you actually compile it with the make command. That means you can go through the kernel configuration options as many times as you want.

As noted in the preceding section, you can use any of the configuration tools (make xconfig, make menuconfig, or make config) to perform the kernel configuration. The easiest way is to type make xconfig. This builds an X Window System-based configuration tool and runs it. The initial window displays a set of buttons, each representing a category of kernel configuration options (as shown in Figure 24-1).

![](img/5fe8f856723cde0b366f73584b9e64b8_269_1.png)

Figure 24-1 Buttons in xconfig show categories of kernel configuration options.

The four buttons, grouped together on the lower-right corner of the window, enable you to perform specific actions such as saving the configurations and exiting. To change a configuration option, click a button. For example, if you click the button labeled Processor Type and Features on the upper-left corner, the configuration program displays another window with all the options you can set. From the new window, you can then set specific options. Next to each option in that window, there is a Help button. Whenever you have a question about an option, click the corresponding context-sensitive Help button to view help information for that option.

You can follow this approach—selecting a category button, locating the option, and clicking Help—to specify the options and complete the configuration step. When you are finished specifying the options, click the Save and Exit button in the main window (refer to Figure 24-1).

## Building and Installing the Kernel and Modules

This section describes the next three key phases of rebuilding a kernel: building the kernel, building and installing the modules, and setting up LILO to load the new kernel when you reboot the system.

### Building the kernel

You should initiate the next three tasks with a single command line by entering multiple semicolon-separated commands on the same line. That way, you can type the line, press Enter, and then take a break because building a kernel takes a while. Depending on your system, making a new kernel can take anywhere from a few minutes to over an hour.

Type the following on a single line to initiate the building process:

```
make dep; make clean; make bzImage
```

The make dep command identifies the files that have changed and must be recompiled. The make clean command deletes old, unneeded files, such as old copies of the kernel. Finally, make bzImage creates the new kernel in a compressed file and places it in a certain directory.

As the kernel is built, you see a lot of messages on the screen. When the process is complete, a new kernel in the form of a compressed file named bzImage appears in the /usr/src/1/linux/arch/i386/boot directory.

To use the new kernel, you have to copy it to the /boot directory under a specific name and edit the /etc/lilo.conf file to set up LILO (the Linux Loader). You learn these steps in the “Installing the New Kernel and setting up LILO” section later in this session. After successfully rebuilding the kernel, you have to build and install the modules.

### Building and installing the modules

If you select any modules during the kernel configuration, you have to build the modules and install them. Follow these steps to perform these tasks:

1. The current set of modules in a directory is named after the version of Linux kernel your system is running. For example, if your system runs kernel version 2.4.2-2, the modules reside in the following directory:
   ```
   /lib/modules/2.4.2-2
   ```
