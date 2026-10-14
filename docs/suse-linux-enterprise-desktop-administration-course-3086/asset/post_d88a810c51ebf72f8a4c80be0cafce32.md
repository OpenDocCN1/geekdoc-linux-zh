
+   4. Send the PID of your bash shell as SIGCONT. What happened and why?
+   5. Send the PID of your bash shell as SIGKILL. What happened and why?

## Process Priorities

Log in to tty1 as the root user and perform the following actions in order. For each action, write down the command(s) that you used. When finished, log out of tty1.

+   1. Start the ps -1 command with the default nice value. What nice value is shown in the output?
+   2. Start the ps -1 command with a nice value of -20 and verify the correct nice value in the output. Did this command run with high or low priority? Which users can run this command?
+   3. Start the ps -1 command with a nice value of +19 and verify the correct nice value in the output. Did this command run with high or low priority? Which users can run this command?

## Scheduling Processes Using the at Daemon

The at command is versatile in that it can understand nearly any time format. Log in to tty1 as the root user, ensure that the at daemon is running, and schedule the date and who commands to run at a time (use the at teatime command). When you have finished scheduling the at job, note the time that the two commands will be scheduled. Following this, remove your at job and use the manual or info pages to research other time formats that can be used with the at command. When finished, log out of tty1.

## Cron Tables

Write the lines that you could use in your crontab to schedule the /bin/sample command to run:

+   1. every Friday at 1:30 a.m.
+   2. at 4:30 p.m. on May 15th only
+   3. at 4:00 p.m. and 4:30 p.m. on the first Sunday of every month
+   4. every 10 minutes from 9:00 a.m. to 5:00 p.m. on Monday
+   5. at 8:15 a.m. and 6:30 p.m. Monday to Friday

![](img/9129877170834ca9d5fdac5319bf5f12_384_0.png)

## Manage System Initialization

In this section, you learn how the SUSE Linux Enterprise Desktop system boots. You also learn how to manage that process by setting runlevels, kernel parameters, and boot loader options, and adjusting other system configurations.

## Objectives

- - Objective 1—Describe the Linux Load Procedure
- - Objective 2—GRUB (Grand Unified Bootloader)
- - Objective 3—Manage Runlevels

## Objective 1—Describe the Linux Load Procedure

Figure 11-1 represents the basic steps of booting a computer with a Linux system installed.

![](img/9129877170834ca9d5fdac5319bf5f12_385_0.png)

Figure 11-1

The following sections describe the process:

- - BIOS and Boot Manager
- - Kernel
- - initramfs (Initial RAM File System)
- - init

## BIOS and Boot Manager

The BIOS (Basic Input Output System) performs a power-on self test, conducts the initial detection and setup of hardware, and accesses bootable devices (such as a CD or hard drive). If the bootable device is a hard drive, BIOS also reads the MBR (Master Boot Record). Using the code in the MBR, the BIOS starts the boot manager.

The *boot manager* (such as GRUB) loads the kernel and the initrd to memory and starts the kernel.

## Kernel

The kernel (/boot/vmlinuz, which is a link to /boot/vmlinuz-kernelversion), uncompresses itself and then organizes and takes control of the continued booting of the system.

The kernel checks and sets the console (the BIOS registers the graphics cards and the screen output format), reads BIOS settings, and initializes basic hardware interfaces.

Next, the drivers, which are part of the kernel, probe existing hardware and initialize it accordingly.

The kernel controls the entire system, managing hardware access and allocating CPU time and memory to programs.

## initramfs (Initial RAM File System)

The Initial RAM File System (initramfs) is a cpio archive that the kernel can load to a RAM disk. It provides a minimal Linux environment that enables the execution of programs before the actual root file system is mounted. The initramfs must always provide an executable named init that should execute the actual init program on the root file system for the boot process to proceed.

Former SUSE Linux versions used an initial RAM disk, initrd, instead. Despite the fact that the format is now changed, the filename is still /boot/initrd; /boot/initrd is a link to /boot/initrd-kernelversion, the file that holds the gzipped cpio archive.

The kernel starts the program init contained in the initramfs. It is a shell script that, among other things, loads the kernel modules needed to mount the actual root file system, mounts the root file system, and then finally starts /sbin/init from the root file system.

To look at the script init in initramfs, unpack the cpio archive:

```
da10:~ # mkdir /tmp/initramfs
da10:~ # cd /tmp/initramfs/
da10:/tmp/initramfs # gunzip -c /boot/initrd-2.6.16.14-6-smp | cpio -i
12765 blocks
da10:/tmp/initramfs # ls
bin bootsplash dev etc init lib proc root sbin sys tmp
da10:/tmp/initramfs # less init
```

The initramfs is created with the proper modules included, such as those needed to access the file system, during installation. The modules to include are listed in the `INITRD_MODULES` variable in `/etc/sysconfig/kernel`. If additional or different modules are needed (because of a hardware change, for example), you would edit the list of modules, and then rebuild the initramfs. The command is the same as the one to build an initrd, `mkinitrd`:

```
da10:~ # mkinitrd
Root device:    /dev/sda2 (mounted on / as reiserfs)
Module list:    piix aixxxx sym53c8xx processor thermal
fan reiserfs edd (xennet xenblk)

Kernel image:   /boot/vmlinuz-2.6.16.14-6-smp
Initrd image:   /boot/initrd-2.6.16.14-6-smp
Shared libs:    lib/ld-2.4.so lib/libacl.so.1.1.0
lib/libattr.so.1.1.0 lib/libc-2.4.so lib/libdl-2.4.so
lib/libhistory.so.5.1 lib/libncurses.so.5.5
lib/libreadline-2.4.so lib/libreadline.so.5.1 lib/librt-
2.4.so lib/libuuid.so.1.2

Driver modules: ide-core ide-disk scsi_mod sd_mod piix
scsi_transport_spi aixxxx sym53c8xx processor thermal fan
edd
Filesystem modules: reiserfs
Including:       initramfs fsck.reiserfs
Bootsplash:      SuSE-SLES (1024x768)
12765 blocks
```

![](img/9129877170834ca9d5fdac5319bf5f12_387_0.png)

The manual page for mkinitrd lists the parameters that can be passed to the init program in the initramfs via the kernel command line.

## init

After checking the partitions and mounting the root file system, the program init located in initramfs starts /sbin/init, which boots the system with all its programs and configurations.

The init process is always assigned a process ID number of 1, and relies on the /etc/inittab file for configuration information on how to run the initialization process.

After the init process starts, it begins by accessing the /etc/init.d/boot script. The /etc/init.d/boot script controls the start of services such as initializing disk quotas and mounting local file systems.

After the boot script has been completed, init starts the /etc/init.d/rc script, which uses configured runlevels to start services and daemons.

Each runlevel has its own set of services that are initiated. For example, runlevel 5 includes the X Window components that run the Linux desktop.

![](img/9129877170834ca9d5fdac5319bf5f12_387_1.png)

For additional details on init, see “Manage Runlevels.”

## Objective 2—GRUB (Grand Unified Bootloader)

To manage GRUB, the Grand Unified Bootloader, you need to know the following:

- - What a Boot Manager Is
- - Boot Managers in SUSE Linux
- - Start the GRUB Shell
- - Modify the GRUB Configuration File
- - Configure GRUB with YaST
- - Boot a System Directly into a Shell

### What a Boot Manager Is

To boot a system, you need a program that can load the respective operating system into memory. This program, called the *boot loader*, loads the operating system kernel, which then loads the system.

After running the power-on self test (POST), the PC BIOS searches various media configured in the BIOS for a boot loader. If it finds one, it turns control of the boot process over to the boot loader.

The boot loader then locates the operating system files on the hard drive and starts the operating system.

A *boot manager* is not only a boot loader, but it can also handle several operating systems. If more than one operating system is present, the boot manager presents a menu, allowing you to select a specific operating system to be loaded.

Linux boot managers can be used to load Linux or other operating systems, such as Microsoft Windows.

GRUB is designed with the following two-stage architecture:

- - *Stage 1*—The first stage of a boot loader is usually installed in the Master Boot Record (MBR) of the hard disk (first-stage boot loader). It can also be installed in the boot sectors of the partitions or on a floppy disk.
  
    Because the space in the MBR is limited to 446 bytes, this program code merely contains the information for loading the GRUB file system drivers (`/boot/grub/filesystem_stage1_5`) and the next stage.
  
- - *Stage 2*—This stage usually contains the actual boot loader. The files of the second-stage boot loader are located in the `/boot/grub/` directory.

### Boot Managers in SUSE Linux

SUSE Linux Enterprise Desktop provides two boot managers for the Linux environment: GRUB (Grand Unified Bootloader) and LILO (Linux Loader).

To understand these boot managers, you need to know the following:

- - GRUB Boot Manager
- - LILO Boot Manager
- - Map Files, GRUB, and LILO
