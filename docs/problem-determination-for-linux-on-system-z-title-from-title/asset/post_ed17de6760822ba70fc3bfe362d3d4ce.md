
Mar 10 12:54:10 linux kernel: IUCV lowlevel driver initialized
Mar 10 12:54:10 linux kernel: iucv: NETIUCV driver initialized
Mar 10 12:54:12 linux kernel: eth0: no IPv6 routers present

## Information regarding network cards

This part of the log (Example 9-7) shows information regarding network cards. This information is recorded while the network card is starting. If we have more than one network card, all information devices will be printed.

### Example 9-7 Network cards logs on /var/log/messages

```
Mar 10 13:00:57 lxinstd ifup: lo
Mar 10 13:00:57 lxinstd ifup: 1o
Mar 10 13:00:57 lxinstd ifup: IP address: 127.0.0.1/8
Mar 10 13:00:57 lxinstd ifup:
Mar 10 13:00:57 lxinstd ifup: eth0
```

## 9.3 Scenarios

In this section, we cover common and possible problems that could occur during the installation or device configurations. When we are talking about installation problems, we can say that we have two possibilities:

-   Problems during the installation
    These are problems that occur while running the program interface installer, for example, a problem with creating partitions, packages dependencies, devices not found, and problems with network setup.
-   Problems after the installation
    These are problems that occur after the Linux install is done successfully, for example, problems with device configurations and problems logging into Linux.

### 9.3.1 Trouble during the installation

In this section we discuss problems during the installation.

#### Scenario 1: Problems cloning Linux system when SuSE v10 and SP1 are used

Problem determination: If we take the default device names of SP1 during installation, your system will be unable to clone.

Solution: We can change device naming through YaST or change it directly in /etc/fstab.

```
lnxhs:~ # cat /etc/fstab
/dev/dasdal  /       ext3   acl,user_xattr   1 1
/dev/dasdb1  swap     swap   defaults       0 0
proc     /proc    proc   defaults       0 0
sysfs    /sys     sysfs  noauto       0 0
debugfs    /sys/kernel/debug    debugfs   noauto       0 0
devpts    /dev/pts    devpts   mode=0620,gid=5     0 0
```

*Figure 9-6  /etc/fstab example*

### 9.3.2 Trouble after the installation

In this section we discuss problems after the installation.

#### Scenario 1: forgotten root password (SuSE or Red Hat)

Problem description: We have configured the root password during the installation but when we try to log in after the reboot we have problems.

This problem can occur when we forget the password or typed it in wrong during the installation.

Solution: To solve this problem, boot your Linux system using Linux single mode or init 1. When are you booting at Linux single mode or init 1 the root file system is mounted as read-only. After the boot, we will have access to the prompt, so we must type the command below:

```
# passwd  root
```

We will set the new root password. Reboot your system using init 6 or by typing the command below:

```
# shutdown -r now
```

## Booting problems

This chapter helps you to identify most problems that you could encounter with the boot process. In the first section we show how the boot process normally works. This makes the problem determination much easier.

This chapter covers the following topics:

-   Understanding the boot process
-   Gathering information regarding boot
-   Commands
-   Boot problem examples
-   Scenarios

### 10.1 Understanding the boot process

The Linux operating system for System z has four phases on its boot process. They are IPL, boot loader, kernel, and Init phases. See Figure 10-1.

![](img/f332344337ca8bf6846cb313a66ee0b3_301_0.png)

Now we describe each process phase.

#### 10.1.1 IPL phase

Initial Program Loader (IPL) is a mainframe term for the loading of the operating system into the computer's main memory. IPL is to mainframe as boot is for other architectures. See Figure 10-2.

![](img/f332344337ca8bf6846cb313a66ee0b3_302_0.png)

The IPL phase consists of reading the boot loader code from the operator-specified device into memory and starting boot loader (zIPL).

DASD, SCSI disk, tape, and VM reader can be used as IPL devices.

#### 10.1.2 Boot loader phase

The main boot loader function is to load other software for the operating system to start. It is found at the start of the IPL device. The boot loader used for IBM S/390 and zSeries machines is called zIPL. Boot loader code is made by the /sbin/zipl command and installed on a user-specified IPL device. Figure 10-3 shows an example of how zIPL works.

![](img/f332344337ca8bf6846cb313a66ee0b3_303_0.png)

*Figure 10-3 How zIPL works*

The bootloader phase consists of loading the initial RAM disk image (initrd) and starting the Linux kernel, and then finally booting the Linux Operating System.

After loading boot Linux kernel, the control is passed to the Linux kernel, as shown in Figure 10-4.

![](img/f332344337ca8bf6846cb313a66ee0b3_304_0.png)

You will find a configuration for a ziPL. See Example 10-1.

##### Example 10-1 Configuration for a ziPL

```
[defaultboot]
defaultmenu = menu

:menu
default = 1
prompt = 1
target = /boot/zipl
timeout = 1
1 = ipl

[ipl]
image = /boot/image
target = /boot/zipl
ramdisk = /boot/initrd,0x1000000
parameters =
"root=/dev/disk/by-id/ccw-IBM.750000000BABL81.89e9.10-part1
elevator=deadline TERM=dumb"
```

#### 10.1.3 Kernel phase

Kernel is the heart of the operating system. The kernel is the heart of the operating system. Some functions of the kernel are to manage system resources (memory, CPU, and so on) and communicate between software and hardware.

The kernel phase consists of probing and initializing the hardware, as well as initializing the kernel subsystems and decompressing initrd and loading some device drivers. After that, mount the root file system with read-only access and check the file system with the fsck program, then start /sbin/init. After this the kernel will sleep, as shown in Figure 10-5.

![](img/f332344337ca8bf6846cb313a66ee0b3_305_0.png)

*Figure 10-5 Kernel phase*

Let us talk a little bit more about each kernel phase.

-   • Recognition and initialization of basic hardware

This step recognizes and initiates basic hardware (processors, memory, console, and so on) included in the kernel. Initialization of various kernel subsystems like SMP, page table, and NET are part of this step.

First of all, Linux kernel decompresses the kernel image on memory, then initializes several devices and subsystems with the start_kernel() function.

Devices and subsystems initialized by the kernel are:

-   Initialize kernel page table.
-   Outputs kernel banner.
-   Initialize physical memory.
-   Initialize CPU cachel.L/2.
-   Initialize scheduler.
-   Registration of interrupt, trap, and task gate.
-   Initialize read-copy update (RCU).
-   Initialize PID hash table.
-   Initialize class-based kernel resource management (CKRM).
-   Initialize timer.
-   Initialize system clock.
-   Initialize console.
-   Initialize VFS.
-   Initialize signal.

The process of PID 1 is started when the initialization of the main hardware is completed, and the following processing is executed by the init () function.

> Note: PID 1 is called init process and it stays alive until Linux is shut down.

-   Initialize multi-processor.
-   Initialize kernel addition function.
    -   Initialize devices management data.
    -   Initialize network management data.
-   Process Initial RAM DISK (initrd).
-   Mount / file system.
-   Run /sbin/init.

-   • Decompressing initial RAM disk (initrd)

This process is required to mount the root file system, load kernel drivers modules, and recognize devices that should be recognized when each service starts.

RAM disk image file includes driver, basic commands and scripts (linuxrc) to mount real root file system. After the mount, the linuxrc script is executed and the following processes occur:

-   Processing of linuxrc script
-   Mounting the proc and sys file systems
-   Starting the udev service
-   Loading the driver module /lib/modules or its subdirectory
-   Recognizing DASD devices and making them online
-   Recognizing FCP channels and putting FCP volumes online
-   Recognizing LVM volumes and activating them
-   Recognizing real root file systems
-   Writing path information to /proc/sys/kernel/real-root-dev

The mount preparation of the root file system is completed by processing the linuxrc script.

### Mounting root file system

This step mounts the root file system in read-only mode. Note that read-write (rw) mount is done later by the init phase. At this point all file systems are checked with the fsck command.

Linux kernel mounts the root file system with read-only (ro) mode, and fsck is executed. Then the device that includes the real root file system can be recognized. At this time, initrd that was mounted previously as a root file system is saved in the /initrd directory.

> Note: In SLES9 and SLES10, the initrd is annulled because /initrd does not exist.

The reason for doing the mount with read-only is to prevent the root file system from breaking and being changed by fsck.

As for the root file system, remount is done with read-write (rw) in the init phase.

### Starting /sbin/init

At this point Linux kernel will sleep. The /sbin/init and the child process do all the start processing afterwards.
