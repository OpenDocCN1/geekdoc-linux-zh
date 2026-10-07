Entering the BIOS to make this change is usually accomplished by depressing a particular key immediately after turning on the computer, such as Del or F2. After entering the BIOS, navigate to the BIOS Boot menu, as shown in Figure 2.2.

![](bbox=[0.195, 0.163, 0.775, 0.535])

**FIGURE 2.2** In order to install an boot using your Red Hat Linux CD-ROM, set your BIOS to have your computer boot using its CD drive.

# Creating a Boot and Auxiliary Driver Disk

Some installation methods require the use of a boot and auxiliary driver disk. These disks can be created using the DOSatWRITE.EXE command or the Linux dd command using disk images on the first Red Hat Linux CD-ROM.

> To use a CD-ROM-based installation, you will need to use a boot floppy if your PC's BIOS (or hardware) does not support booting from a CD-ROM drive. You can upgrade the BIOS of many PCs, however, to add upgraded features, bug fixes, or to enable new hardware (such as larger hard drives). Upgrade by downloading your motherboard's BIOS image from the manufacturer's Web site onto a boot floppy and then use the boot floppy to reboot the PC. During reboot, the boot floppy reflashes the BIOS memory. Upgrading a PC's BIOS can be risky, however, because a power outage or drive failure during the upgrade could render your PC unbootable.