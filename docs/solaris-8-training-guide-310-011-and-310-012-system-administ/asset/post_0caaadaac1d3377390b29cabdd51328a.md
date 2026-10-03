
## Device Auto-Configuration

Auto-configuration offers many advantages over the manual configuration method used in earlier versions of UNIX, in which device drivers were manually added to the kernel, the kernel was recompiled, and the system had to be restarted. Now, with auto-configuration, the administrator simply connects the new device to the system and performs a reconfiguration startup.

## STEP BY STEP

### 16.1 Performing a Reconfiguration Startup

- 1. Create the /reconfigure file with the following command:
  `touch /reconfigure`

  The /reconfigure file causes the Solaris software to check for the presence of any newly installed devices the next time you turn on or start up your system.

- 2. Shut down the system using the shutdown procedure described in Chapter 1, “System Startup and Shutdown.”

  If you need to connect the device, turn off power to the system and all peripherals after Solaris has been properly shut down.

  After the new device is connected, restore power to the peripherals first and then to the system. Verify that the peripheral device has been added by attempting to access it.

> NOTE
> The file named /reconfigure automatically gets removed during the boot-up process.

An optional method of performing a reconfiguration startup is to interrupt the start process and type boot -r at the OpenBoot prompt.

I prefer the first method described because the system administrator can instruct the system to perform the reconfiguration startup at any time by creating the /reconfigure file. Now, at the next restart, whether the administrator is there or not, the system performs the reconfiguration startup. This could happen at 3 a.m. if you like.

> NOTE
> As root, you can also issue the reboot -- -r command from the UNIX shell. The -- -r passes the -r to the boot command.

During a reconfiguration restart, a device hierarchy is created in the /devices directory to represent the devices connected to the system. The kernel uses this to associate drivers with their appropriate devices. Also, any kernel parameter changes that were made to the /etc/system file are parsed by the kernel at this time.

Auto-configuration offers the following benefits:

- Main memory is used more efficiently because modules are loaded as needed.
- There is no need to reconfigure the kernel if new devices are added to the system. When you add devices such as disks or tape drives, however, the system needs to be shut down before you connect the hardware so that no damage is done to the electrical components.
- Drivers can be loaded and tested without having to rebuild the kernel and restart the system.

Occasionally, you might install a new device for which Solaris does not have a supporting device driver. Always check with the manufacturer to make sure that any device you plan to add to your system has a supported device driver. If a driver is not included with the standard Solaris release, the manufacturer should provide the software needed for the device to be properly installed, maintained, and administered.

Third-party device drivers are installed as software packages using the pkgadd command. At a minimum, this software includes a device driver and its associated configuration (.conf) file. The .conf files reside in the /kernel/drv directories. Table 16.2 describes the contents of the subdirectories located in the /kernel directory.

## TABLE 16.2

### THE /KERNEL DIRECTORY

| Directory | Description |
|---|---|
| drv | Contains loadable device drivers and pseudo-device drivers. |
| exec | Contains modules used to run different types of executable files or shell scripts. |
| fs | Contains file system modules, such as ufs, nfs, proc, and so on. |
| misc | Contains miscellaneous system-related modules, such as swap-generic and ipc. |
| sched | Contains OS schedulers. |
| strmod | Contains System V STREAMS loadable modules. |
| sys | Contains loadable system calls, such as system semaphore and system accounting operations. |

## Instance Name

The instance name represents the kernel’s abbreviated name for every possible device on the system. For example, on an Ultra system, dad0 represents the instance name of the IDE disk drive, and hme0 is the instance name for the network interface. Instance names are mapped to a physical device name in the /etc/path_to_inst file. The following shows the contents of a path_to_inst file:

```
more /etc/path_to_inst
#
#       Caution! This file contains critical kernel state
"/pci@1f,0" 0 "pci"
"/pci@1f,0/pci@1,1" 0 "simba"
"/pci@1f,0/pci@1,1/ide@3" 0 "uata"
"/pci@1f,0/pci@1,1/ide@3/sd@2,0" 2 "sd"
"/pci@1f,0/pci@1,1/ide@3/dad@0,0" 0 "dad"
"/pci@1f,0/pci@1,1/ebus@1" 0 "ebus"
"/pci@1f,0/pci@1,1/ebus@1/fdthree@14,3023f0" 0 "fd"
"/pci@1f,0/pci@1,1/ebus@1/su@14,3062f8" 1 "su"
"/pci@1f,0/pci@1,1/ebus@1/se@14,400000" 0 "se"
"/pci@1f,0/pci@1,1/ebus@1/su@14,3083f8" 0 "su"
"/pci@1f,0/pci@1,1/ebus@1/ecpp@14,3043bc" 0 "ecpp"
"/pci@1f,0/pci@1,1/ebus@1/SUNW,CS4231@14,200000" 0 "audiocs"
"/pci@1f,0/pci@1,1/ebus@1/power@14,724000" 0 "power"
"/pci@1f,0/pci@1,1/network@1,1" 0 "hme"
"/pci@1f,0/pci@1,1/SUNW,m64B@2" 0 "m64"
"/pci@1f,0/pci@1" 1 "simba"
"/pci@1f,0/pci@1/pci@1" 0 "pci_pci"
"/pci@1f,0/pci@1/pci@1/SUNW,qfe@1,1" 1 "qfe"
"/pci@1f,0/pci@1/pci@1/SUNW,qfe@0,1" 0 "qfe"
"/pci@1f,0/pci@1/pci@1/SUNW,qfe@3,1" 3 "qfe"
"/pci@1f,0/pci@1/pci@1/SUNW,qfe@2,1" 2 "qfe"
"/options" 0 "options"
"/pseudo" 0 "pseudo"
#
```

Instance names can also be displayed by using the commands dmesg, sysdef, and prtconf, the only command that shows the mapping of the instance name to the physical device is the dmesg command, which displays the following information:

```
dad0 at pci1095,6460 target 0 lun 0
dad0 is /pci@1f,0/pci@1,1/ide@3/dad@0,0
```

If you have an older SPARCstation with an SBus and SCSI disk drives, here's similar output for a SCSI disk drive:

```
sd3 at esp0: target 3 lun 0
sd3 is /iommu@f,e0000000/sbus@f,e0001000,espdma@f,400000/esp@f,800000/sd@3,0
```

In the first example, dad0 is the instance name and /pci@1f,0/pci@1,1/ide@3/dad@0,0 is the physical device name. After the instance name has been assigned to a device, it remains mapped to that device. To keep instance numbers consistent across restarts, the system records them in the /etc/path_to_inst file. This file is read only at startup, and it is updated by the devfsadm daemon described later in this section.

Devices already existing on a system are not rearranged when new devices are added, even if new devices are added to sbus slots that are numerically lower than those that are occupied by existing devices. In other words, the /etc/path_to_inst file is appended to, not rewritten, when new devices are added.

It is generally not necessary for the system administrator to change the path_to_inst file, because the system maintains it. The system administrator can, however, change the assignment of instance numbers by editing this file and doing a reconfiguration startup. However, any changes made in this file are lost if the devfsadm command is run before the system is restarted.

> CAUTION
> Do not remove the path_to_inst file; the system cannot start up without it. The system relies on information found in this file to find the root, usr and swap devices. Make changes to this file only after careful consideration.

In Solaris 8, you can add new devices to a system without requiring a reboot. It’s all handled by the devfsadmd daemon that transparently builds the necessary configuration entries. Before Solaris 7 release 11/99, you needed to run several devfs administration tools such as drvconfig, disks, tapes, ports, and devlinks to add in the new device and create the /dev and /devices entries necessary for the Solaris operating environment to access the new device. These tools are still available, but for compatibility purposes, drvconfig and the other link generators are symbolic links to the devfsadm utility. Furthermore, these older commands are not aware of hot-pluggable devices, nor are they flexible enough for devices with multiple instances. The devfsadm command should now be used in place of all these commands; however, because devfsadmd, the devfsadm daemon, automatically detects device configuration changes, so there should be no need to run this command interactively.

An example of when to use the devfsadm command would be if the system has been started, but the power to the CD-ROM or tape drive was not turned on. During startup, the system did not detect the device; therefore, its drivers were not installed. This can be verified by issuing the sysdef command and examining the output for sd6, the SCSI target ID normally used for the external CD-ROM:

```
sd, instance #6 (driver not attached)
```

To gain access to the CD-ROM, you could halt the system, turn on power to the CD-ROM, and start the system back up, or you could simply turn on power to the CD-ROM and issue the following command at the command prompt:

```
devfsadm
```

Now if you issue the sysdef command, you’ll see the following output for the CD-ROM:

```
sd, instance #6
```

> NOTE
> If you can’t start up from the startup disk because of a problem with the /etc/path_to_inst file, you should start up from the CD-ROM (boot -sw cdrom) and copy the /etc/path_to_inst file contained on the CD-ROM to the /etc/path_to_inst on the startup disk. To do this, start up from the CD-ROM using boot -sw cdrom at the OpenBoot prompt. Then mount the startup disk on /a. Copy the /etc/path_to_inst file to /a/etc/path_to_inst. If you still can’t start up, the problem is deeper than just with the /etc/path_to_inst file.

> NOTE
> Two terms that are often interchanged (and confused) are hot-pluggable and hot-swappable. Hot-pluggable allows the connection and disconnection of peripherals or other components without rebooting the operating system. Dynamic reconfiguration, available on certain SPARC servers, allows a service provider to remove and replace hot-pluggable system I/O boards in a running system, eliminating the time lost in rebooting. Also, if a replacement board is not immediately available, the system administrator can use dynamic reconfiguration to shut down a failing board while allowing the system to continue operation. Hot-swappable allows the connection and disconnection of peripherals or other components without shutting down the hardware, but usually requires a system reboot.
