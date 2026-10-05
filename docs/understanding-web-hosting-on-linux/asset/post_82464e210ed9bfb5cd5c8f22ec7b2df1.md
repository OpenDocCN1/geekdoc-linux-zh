
# 42 · CHAPTER 3

- 1. rpm -Uhv package_name.rpm updates or installs a package. If the package is not installed, it will be installed. If it is already installed, older versions of the software will be replaced by the newer version.
- 2. rpm -ivh package_name.rpm installs a package. This option is typically used when updating a kernel package, since it allows the older version of the kernel to remain. Should anything go wrong with the newer version, you can always boot the older version.

Assume, for example, that you have a package on your system called foo. To see what version of foo is currently installed, type the command `rpm -q foo`. You should get a response like `foo-1.4.5-10`. Assuming a new package has become available, say `foo-1.5.0-1.rpm`, you download it and type the command `rpm -Uhv foo-1.5.0-1.rpm`. Once the package has been installed, the command rpm -q would return `foo-1.5.0-1`, indicating that the update was successful.

# Chapter Summary

This chapter outlined the steps required to install Linux. It emphasized preparation, with the focus on creating a system that is flexible and can be easily upgraded or reconfigured. Good system administration requires that the system software be kept up-to-date to ensure the latest security upgrades and enhancements are in place. To ensure a smooth installation, nothing beats reading the documentation prior to installation. And no system is complete without a boot diskette.

# End of Chapter Review

# Key Terms

| Boot diskette | LILO | Swap space |
| :--- | :--- | :--- |
| boot.img | Logical partition | tar |
| DBMS | Partition | Three-partitioning |
| Desktop workstation | Partition table | UDMA-100 |
| disk raid | Primary partition | UDMA-33 |
| EIDE | Root directory | UDMA-66 |
| EIDE UDMA-100 | Root partition | Ultra-160 SCSI |
| Extended partition | RPM | Virtual console |
| fdisk (mke2fs) | SCSI | x86 platform |
| FHS | Server | |
| GMT | SMP | |
| IDE | Swap partition | |

# Review Questions

- 1. List two undesirable consequences that may occur as a result of poor planning for a server installation.
- 2. What is the name of the command that allows you to access a partition?
- 3. The Red Hat Package Manager (RPM) is useful for what purpose?
- 4. Why do the authors recommend installing a fresh copy of a new distribution versus upgrading a previous version of that distribution?
- 5. Why is it necessary to create at least one normal user during a Linux install?

# Programming Assignment

Exercise: Install Linux

- 1. Follow the Red Hat install prompts.
- 2. Use the suggestions in the chapter for selecting options during the Red Hat install.
- 3. [Optional] Load Linux on another machine.

# 4

# Linux Configuration and Startup

The Linux lifecycle is composed of four phases:

- Booting on or starting up Linux
- Logging on
- Using Linux applications
- When necessary for system maintenance, shutting down the system

This chapter covers all four of these phases.

# Starting Up

The term booting the system was borrowed from the saying “pulling yourself up by your bootstraps,” which refers to someone going without any help from anyone else. Picture some cowboy out on the prairie knocked unconscious after being thrown by a horse—with no help available, he has to pull himself up and get going again. Bootstrapping your computer is basically the same thing. The bootstrap of Linux, and most operating systems, is a small file contained either on a floppy disk or on the first sector of your system’s primary hard drive, known as the Master Boot Record, or MBR.

Your computer’s hardware contains a little piece of software called the BIOS (Binary Input/Output System) that is hard-wired to your system’s board. When you power on your system, the BIOS looks for the startup file on your system’s floppy or primary drive. A Linux diskette contains a compressed version of the Linux kernel. Once loaded into memory, the kernel decompresses itself and starts executing.

# 6 • CHAPTER 4

Many Linux systems use LILO (Linux Loader) to control the boot process. LILO is installed on the MBR of your primary hard drive. Figure 4.1 show the L configuration file (/etc/lilo.conf) from a particular laptop. As mentioned in chapter 3, the Red Hat installation will configure LILO for you, but it's a good idea to understand what the various sections of lilo.conf accomplish. The first three statements of the file set the basic parameters for Linux. The boot statement sets the name of the device where LILO should install itself in the MBR, /dev/hda in this system's case. Note that hda is the Linux name of a physical device, not a logical partition as hda2. The install statement names the file containing the boot sector to use on the MBR, and the map statement specifies the file that LILO creates when installed.

```
# basic parameters
boot=/dev/hda
install=/boot/boot.b
map=/boot/boot.b

# Boot option: Linux Version 2.4
image=/boot/vmlinux-2.4.2-2
label=linux
read-only
root=/dev/hda5

# Boot option: NetTraverse's Win4Lin kernel
image=/boot/win4lin
label=win4lin
root=/dev/hda5

# section for Windows/2000
other=/dev/hda1
optional
label=dos

# boot-time options
append="mem=512"
```

Figure 4.1: The lilo.conf file supports boot-time options for multiple operating systems.

The next three sections of the LILO configuration file in Figure 4.1 qualify three operating-system options. LILO supports the optional booting of various operating systems. At boot time on this example, you could select to Linux version 2.4, a custom version of Linux by NetTraverse Win4Lin (that supports running Windows 98 operating system in a Linux process), or Windows 2000.

The last statement of the lilo.conf file in Figure 4.1 is a boot-time option. There are a dozen or so possible boot-time options, but this one qualifies that the laptop has 512 Mb of memory.

Messages will be displayed while your system is booting, but there are many that you might important error messages. So, after the boot process is complete, review all the messages in log file /var/messages.

Note: If you modify lilo.conf, you must run /sbin/lilo as root to place the options into the boot process.

Until Linux came around, IBM's iSeries supported one operating system. As a result, iSeries did not have a generic process for loading and installing operating systems. Also, iSeries runs as secondary partition in primary partition.

To start up Linux on iSeries machine, you load the kernel into the partition, initialize it, and link to the root system. You do this with iSeries's Create Network Description (CRTNSD).

# Initialization

After device drivers are installed by the boot process, the init program (located under /sbin directory in Red Hat) is executed. This program starts or stops various Linux applications during system startup or shutdown. The processing completed by the init program is controlled by a special file called initabb, see Figure 4.2 (located under /etc directory in Red Hat). Like lioconf, the Red Hat initialization will configure initabb for you, but it is still a good idea to understand how it drives the processing of the init program.

| initabb | This file describes how INIT process should set up the system in a certain run-level |
| :--- | :--- |
| Author: Miguel van Soenburg, -miquels@drinkel.net | Modified for RH Linux by Marc Ewing and Donna Barnes |

- Default runlevel; the runlevels used by RHS are:
- 0 halt (DO NOT set initdefault to this)
- 1 Single user mode
- 2 Multiserver, without NFS (The same as 3, if you do not have networking)
- 4 unused
- 5 X1
- 6 reboot (DO NOT set initdefault to this)

```
# 3:initdefault:
# System initialization.
sis::sysinit/etc/rc.d/rc.sysinit

10:0:wait/etc/rc.d/rc 0
11:1:wait/etc/rc.d/rc 1
12:2:wait/etc/rc.d/rc 2
13:3:wait/etc/rc.d/rc 3
14:4:wait/etc/rc.d/rc 4
15:5:wait/etc/rc.d/rc 5
16:6:wait/etc/rc.d/rc 6
```

- Things to run in every runlevel.
once:/sbin/bin/update
- Trap CTRL-ALT-DELETE
ca:ctrapdel:/sbin/shutdown -t3 -r now
- When our UPS tells us power failed, assume we have a few minutes of power left. Schedule a shutdown for 2 minutes from now.

Figure 4.2: The initabb file controls the initialization sequence of Red Hat Linux (part 1 of 2).
