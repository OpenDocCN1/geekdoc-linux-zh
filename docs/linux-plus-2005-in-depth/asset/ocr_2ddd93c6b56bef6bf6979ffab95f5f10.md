# 254   Chapter 7    ADVANCED INSTALLATION

Normally, ACPI support is detected and enabled during a Red Hat Fedora installation. However, ACPI was not enabled during the installation, simply add the string `acpi=off` to the end of the kernel line in `/boot/grub/grub.conf` file. If your boot loader is **Grand Unified Bootloader (GRUB)**, or the line append `acpi=off acpi1=on` to the `/etc/lilo.conf` file if your boot loader is **Linux Loader (LILO)**. Boot loaders are further discussed in Chapter 9, “System Initialization and X Windows.”

After ACPI has been enabled, it is configured with default options supported by your hardware. You can also download and use certain applications or applets to view or configure its settings. One example is headload, which can monitor CPU temperature. Another example is the **Linux ACPI Client**, which is a command-line utility that you can download to view ACPI settings, as shown in the following example:

```
[root@server1 root]# acpi -v
Battery 1: discharging, 91%, 02:39:07 remaining
Thermal 1: ok, 44.1 degrees C
AC Adapter 1: off-line
[root@server1 root]#
```

> **NOTE**
> Although ACPI is supported by nearly all mainboards and operating systems as of this writing. it is still a work in progress; you should always ensure that your system has the most recent ACPI Linux kernel patch from http://acpi.sourceforge.net. Patching the Linux kernel is discussed in Chapter 13, "Troubleshooting and Performance."

# ## RAID Configuration

Recall that you typically create several partitions during installation to decrease the likelihood that the failure of a filesystem on one partition will affect the rest of the system. These partitions should be spread across several different hard disks to minimize the impact of a hard disk failure; if one hard disk fails, the data on the other hard disks is unaffected.

If a hard disk failure occurs, you must power down the computer, replace the failed hard disk drive, power on the computer, and restore the data that was originally on the hard disk drive from a back-up source such as a tape device. The whole process can take several hours. For systems that must experience little or no downtime, such as a database server, there exist hard disk configurations that reduce the time it takes to recover from a hard disk failure. These configurations are called **fault tolerant** and are typically implemented by a **Redundant Array of Independent Disks (RAID)**. RAID configurations can be handled by software running on an operating system (software-based RAID), but are more commonly handled by the hardware contained within a SCSI hard disk controller (hardware-based RAID). To configure hardware-based RAID, you must enter the setup utility for your specific SCSI hard disk controller.