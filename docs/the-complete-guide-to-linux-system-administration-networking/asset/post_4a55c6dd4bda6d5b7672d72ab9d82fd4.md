
check the network cable before trying more complex solutions. Because Linux is so widely used, you can often find the solution to a problem, once you have narrowed down its cause, by searching online. You can search specific sites, such as the documentation on Red Hat Software’s Web site (www.redhat.com/docs/), or the Linux Documentation project site (www.tldp.org). You will often find a solution by typing in key words on the Google search engine, at www.google.com.

## Troubleshooting Linux Installation

Linux installation can be trouble free, completed in about 15 minutes plus the time it takes to copy files from the CD-ROM to your hard disk. But that doesn’t always happen. The following sections provide ideas on solving some common problems you might encounter during a difficult Linux installation.

### The Installation Program Doesn’t Boot

If the Linux installation program does not start, the following are likely causes:

- The boot disk was created incorrectly. Try using a new disk and recreating the boot disk using the rawwritewin or dd programs. The dd program is more likely to cause trouble if you are unfamiliar with Linux utilities.
- The BIOS is configured to start the operating system from the hard disk without first checking the floppy disk or CD-ROM (whichever you are trying to use). This is a handy security feature that some systems implement by default; it also saves time because most people boot their systems from a hard disk. Edit the BIOS settings as needed.
- If the installation program starts but then appears to crash, the installation program may not be able to detect your video card. Try starting the installation by entering the word “text” at the first screen of text.

### After Linux Is Installed, the System Doesn’t Boot

Once you install Linux, the system sometimes does not boot into the newly installed Linux system. Here are some likely causes:

- You may have installed the boot manager on the active partition (as selected by default), but another boot manager installed in the MBR causes control to pass to another partition (not the active partition). Use the boot disk you created at the end of the installation to boot into your new Linux system—the boot disk “knows” which partition on your system contains Linux. You can also reinstall Linux, placing the Linux boot manager on the MBR.
- The system may have trouble identifying hardware on your system that was not detected during the installation process. In this case it may help to specify information about the hardware via a boot parameter. The boot manager starts the Linux kernel with this parameter attached. These parameters are used both to affect how Linux recognizes hardware devices, and to alter the enabled features of the operating system.

### The Graphical Interface Doesn't Work

Sometimes the graphical interface doesn't work even though the installation program appears to detect your video hardware without a complaint. In this case, you probably selected a color depth or resolution that is not supported by the Linux driver. This can be true even if higher resolutions are supported on Windows—the Linux driver may still be in development or the developers lack critical technical information to make the video card perform to its capabilities.

Some video cards that are not supported by XFree86 are supported by commercial X Window System products that you can purchase and add to your Linux system after installing Linux. One such server is available from Xi Graphics (see www.xig.com). In the rare case that your card is not supported by any of these products, you can only use Linux in text mode. This is typical for many server installations, but if you want to use a graphical desktop, you need to invest in a different video card.

### A Device or Part of Memory Isn't Available

Sometimes hardware that is included on the list of supported hardware on the Linux vendor's Web site is nevertheless not available after starting Linux. This is often because the hardware is not correctly configured. As with a system that won't boot, the configuration can sometimes be corrected by adding a boot parameter when starting Linux. For example, some computers running Linux cannot access the CD-ROM drive correctly unless the device name is added as a boot parameter, like this:

```
linux cdrom=/dev/hdc
```

Or, Linux may not access all of the available system RAM because of limitations in the computer's BIOS. (The free command displays the amount of memory available to Linux.) You can tell Linux the amount of RAM on the system using this format:

```
linux mem=<amount of memory>M
```

So to indicate 512 MB of RAM, you use the following command:

```
linux mem=512M
```

Be sure to use the correct value for the amount of RAM on your computer, or Linux crashes as it tries to work with nonexistent memory.

You can combine multiple boot parameters on a single line separated by spaces. For example:

```
linux cdrom=/dev/hdc mem=512M
```

### Diagnosing Device Status

Linux includes a number of utilities to help you learn about devices attached to your system and configure those devices for use in Linux. Some of these require a fairly detailed knowledge of the hardware in question.

The directories of the /proc file system can provide information about many devices. For example, looking in the /proc/interrupts, /proc/ioports, /proc/pci, or /proc/dma displays helpful device information. Linux also includes specific utilities to display this and other device information in a useful format. These utilities include lspci, setserial, and usbmodules.

Similar information is available graphically using the Hardware Browser in Red Hat Linux and Fedora (choose System Tools, then Hardware Browser on the GNOME main menu).

### Troubleshooting Network Connections

Networking can become very complex; the larger the network and the more diverse the technologies it uses, the more difficult troubleshooting becomes. Table 15-2 lists some common networking problems that you can diagnose and troubleshoot with the tools you have learned about.

Table 15-2 Basic Networking Troubleshooting Review

| Trouble | Things to check |
|---|---|
| Networking doesn't appear to function at all | Use the ifconfig command to see whether networking is up and running; if not, try the network script in /etc/rc.d/init.d. (Remember to check things that seem too obvious: Is the cable plugged into the Ethernet card? Is an Ethernet card installed? Is the cable plugged into the wall or a hub?) |
| The network script doesn't appear to work | Use the lsmod command to see whether any network modules are installed in the kernel; if not, use modprobe -t or a graphical utility to install the right kernel module for your networking card |
| Can't ping any other systems on the local network segment | Check the cables; check with ifconfig to see whether a valid IP address has been assigned; check the routing tables to see that a route is listed for the local network |
| Can't ping any system on another segment within the organization | Check the cables at the hub or server room; check with ifconfig to see if a valid IP address is assigned and how that address compares or conflicts with those on the other network segment; does the routing table include a route for the other network that refers to an intermediate router, if necessary? |

### Table 15-2 Basic Networking Troubleshooting Review (continued)

| Trouble | Things to check |
|---|---|
| Traffic to another segment seems very slow | Check the routing table to see whether the most direct route is defined, and check whether another system has the same IP address assigned. Review the output of the ifconfig command to see whether a large number of collisions are occurring—if so the network may be overloaded. Check ifconfig output to see whether a large number of errors are occurring—if so the NIC may be defective. Review whether fragmentation problems between the two segments could be slowing down traffic; use traceroute to see at what point along the way the transmission slows down significantly. |

### Creating Rescue Disks

A fairly common system failure is a hard disk problem or other trouble with booting the system. Sometimes this takes the form of a complete crash, in which case you may have to restore all of the data to a new hard disk from a backup archive. In other cases, part of the disk is corrupted so that the system cannot boot. Sometimes a hard disk problem can even be caused by something that the system administrator has done to the system. In the case of many hard drive failures, you cannot boot the Linux system normally from the hard disk; you must boot from a removable disk or bootable CD-ROM before you can access the hard disk and solve the problem.

A rescue disk is a 3.5-inch disk that you can use to boot a Linux-based computer. It may have only a boot manager and enough information to locate the Linux partition on your hard disk. Often, it includes a minimal version of Linux and enough system utilities to diagnose and repair problems in hard disk files. After booting the system from a rescue disk, you can mount the hard disks where Linux is installed to correct problems. One popular preconfigured rescue disk is Tom's Boot disk, which you can download from www.toms.net/rb.

Some system administrators always boot their servers from a 3.5-inch disk. This takes more time than booting from a hard drive, but because a server is rarely rebooted, speed of booting is not really a concern. By doing this, the system administrator can control how the system boots and easily maintain a backup of the removable disk in case of problems. A separate rescue disk is used when the boot disk or hard disk fails.

Ideally, you create a boot disk for your system when installing Linux, as described in Chapter 8. This guarantees that the boot disk and the boot manager information on the computer's hard disk are compatible. You can also use the mkbootdisk command to create a boot disk after your system is running.

When you are working with Red Hat Linux or Fedora and have problems booting the system, or have a hard disk crash or other serious hard disk problem, you can start the system in rescue mode using Fedora CD 1. After booting from that CD, enter linux rescue at the
