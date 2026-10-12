
> **Tip**
> If you don't plan to compile the kernel ever, you may skip the *kernel-headers-2.*.xx-x.*.i386.rpm* and *kernel-source-2.*.xx-x.*.i386.rpm* packages, because they are needed only for compiling custom kernels.

After you upgrade the new kernel and its related packages, you need to create the initial ramdisk image file needed by the kernel to boot the system. The initial ramdisk image file allows a kernel to access modules such as disk drivers, which in turn are needed to access the rest of the modules residing on the root file system.

## Creating the initial ramdisk

The `mkinitrd` command is used to create the initial ramdisk. Replacing `2.*.xx-x` with the version number of your new kernel, run the following command:

```
mkinitrd /boot/initrd-2.*.xx-x.img 2.*.xx-x
```

This creates the `/boot/initrd-2.*.xx-x.img` initial ramdisk image file. Using the `ls` utility, confirm that this file is really created in `/boot` directory. After you create the initial ramdisk, you need to modify the `/etc/lilo.conf` file to configure LILO for the new kernel.

## Configuring LILO

Configuring LILO is critical to your kernel installation, and you must not reboot the system until you have reconfigured LILO as discussed here. Using your favorite text editor, add a new configuration segment, such as the following, to your `/etc/lilo.conf` file:

```
image=/boot/vmlinuz-2.*.*.x-x
    label=new-linux
    root=/dev/hda1
    initrd=/boot/initrd-2.*.*.x-x.img
    read-only
```

> **Tip**
> Before you modify your /etc/lilo.conf file, make a copy of it just in case you need to revert to the old configuration.

Replace 2.x.x-x with the appropriate kernel version number for both the image= and initrd= lines. The label= line should be set to an arbitrary string of your choice. The root device should point to your root disk partition.

For example, if your current partition is /dev/sda1, make sure the root= line is set to that partition. If Linux does not recognize memory above 64MB, you use the append= line to set the memory size to an appropriate limit.

After you modify and save the /etc/lilo.conf file, run /sbin/lilo

This makes LILO read the new configuration file and update the boot sector of the appropriate root partition. You can use the -v flag with the preceding command to make LILO be a bit more verbose. After you run LILO, you are ready to reboot the system.

## Booting with the new kernel

Enter the shutdown -x now command to reboot your system as usual. At the LILO prompt, press the Tab key to see your choices. The labels you enter (in the label= lines) for your old and new kernels will appear onscreen. Enter the new label (in the preceding example, this label is new-linux) at the LILO prompt to boot the system with the new kernel.

The next step probably depends on your facial expression after you have told LILO to start the new kernel. If you are smiling, your new kernel is up and running. If you are screaming or not smiling at all, do not panic—you still have the old kernel. If the system locks up, press Ctrl+Alt+Del or do a hard reboot. After you get the LILO prompt again, enter the label name for your old kernel. The system should reboot as usual. In such a case, check the steps you have already taken, especially regarding the /etc/lilo.conf file. Make sure that you have the new configuration set up correctly. Rerun /sbin/lilo and try to boot the system with the new kernel. If the problem persists, you need to post the details of your problem (such as what is shown on the console when you attempt to boot the new kernel) to a comp.linux newsgroup. If your software license permits, you may also contact Red Hat for help.

In most cases, the new installation will go smoothly, without any incident. To make sure you are running the new kernel, run the following command:

```
uname -a
```

This displays the kernel version number along with other information. After your new kernel is up and running, create a new boot disk using the mkbootdisk command, as you did earlier in the preparation section of this installation.

## Customizing the Kernel

The only way to customize a kernel to your liking is with custom compilation. To compile a kernel on your Red Hat Linux server system, you need to get the kernel header and source RPM packages. If the kernel you are trying to customize is not production grade, an RPM version might not be available. In such a case, you have to download the source in compressed tar format (.tar.gz). Check the official Red Hat Web site for availability of the kernel source and header RPM packages. If you can't find the RPM packages, download the .tar.gz distribution from the official http://www.kernel.com/ site (or any of its mirrors). This section assumes that you want to customize the latest 2.2.5 kernel and have downloaded the linux-2.2.2.tar.gz source distribution from the site just mentioned.

### Installing Linux kernel source

Extract the linux-2.2.2.tar.gz distribution in /usr/src directory by entering the tar xvzf linux-2.2.2.tar.gz command. The source distribution will be stored in a subdirectory called linux-2.2.2 in /usr/src. The Linux kernel is traditionally stored in /usr/src/linux. Actually, /usr/src/linux is a symbolic link to the /usr/src/linux-x.x.x directory. Remove the symbolic link using rm /usr/src/linux and then create a new symbolic link using the following command:

```
ln -s /usr/src/linux-2.2.2    /usr/src/linux
```

The series of commands that you have to perform to arrive at this stage might look like the following:

```
cd /usr/src
tar xvfz linux-2.2.2.tar.gz
rm -f /usr/src/linux
ln -s linux-2.2.2 linux
```

> **Tip**
> When I extracted the source distribution in the /usr/src directory, it created a linux subdirectory, and therefore the symbolic link was unnecessary. However, if you plan to experiment with various kernels, I recommend that you keep a particular source distribution in the /usr/src/linux-x.x.x directory and always point a symbolic link (linux) to the kernel you are currently working on.

Although a freshly downloaded source distribution is not going to have any stale object files, it is wise to run the following command to clean up any such files just in case:

```
make mrproper
```

You are ready to configure (that is, customize) the kernel. You have multiple choices as to how you can customize the kernel.

### Configuring the kernel the old-fashioned way

To configure the kernel the old-fashioned way, you need to run the following command from the /usr/src/linux directory:

```
make config
```

This is the simplest way to configure a kernel; however, it might not be the most suitable for beginning kernel hackers. Next, I will discuss a sample kernel configuration session using the make config method. However, you should know that as features and support for various devices are added to Linux, the exact steps that make config shows also change. Therefore, what you will see in the following section might not be exactly what you see when you run make config on your system. I discuss the major decision points here. If you find a new configuration question when you run `make config`, you can find more about it by entering ? at the prompt, or you can choose to go with the default.

### Code maturity-level options

In this section, you have to decide if you want to be asked about features not yet ready for prime time. In other words, you are asked if you want to be prompted for experimental features. You can choose to see (and perhaps use) these experimental features if you are configuring the kernel for a system where experimentation or down time and crashes are part of the fun and not a burden. The prompt appears as follows:

**Prompt for development and/or incomplete code/drivers**  
**(CONFIG_EXPERIMENTAL)** [N/y/?]

The default answer is N, for no. You can choose the default answer by pressing the Enter key. Note that the default answer is always a capital letter.

### Processor type, memory model, and features

In this section, you are asked about the processor family, the memory model, the math coprocessor, multiprocessors, and other processor-specific questions. Here is the first:

Processor family (386, 486/Cx486, 586/R5/x586/6x86,  
Pentium/K6/TSC, PPro/6x86MX) [PPro/6x86MX]

If the default processor architecture is incorrect, choose one of the listed ones. In my case, the default is wrong, so I enter Pentium/K6/TSC as the processor family.

Maximum Physical Memory (1GB, 2GB) [1GB]

The default memory model is 1GB, which should be fine if your system has 1GB or less RAM. If you have 2GB or less, choose 2GB. In my case, I choose the default.

`defined CONFIG_M686`

Math emulation (CONFIG_MATH_EMULATION) [N/y/?]
