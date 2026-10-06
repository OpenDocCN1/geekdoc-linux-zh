
# CHAPTER 11 TCP/IP for System Administrators 327 

## Summary

This chapter covered the fundamentals of TCP/IP and other protocols, ARP, subnetting and netmasks, and routing. It's a lot to digest, but hopefully this simplified version should make it easier to understand. Specifically, we discussed the following:

- How TCP/IP relates to the OSI OSI seven-layer model
- The composition of a packet
- The specifications of packet headers and how to explore them using tcpdump
- The complete process of a TCP connection setup, data transfer, and connection teardown
- How to calculate netmasks
- How static routing works
- How dynamic routing works with RIP
- Several packet analysis examples covering the use of tcpdump
- A brief overview of IPv6

Because the information here is (substantially) simplified, you might want to take a look at some other books for more information regarding this topic. This is especially important if you have complex networks in which your machines need to participate or if you need to understand the operation of your firewall better.

One classic book we recommend is TCP/IP Illustrated, Volume 1, by Richard Stevens (Addison-Wesley, 1994). This book covers TCP/IP in depth as well as several popular protocols that give their data over IP. The complex subject of TCP/IP is explained in a clear and methodical manner. Another recommended book is TCP/IP Network Administration, Third Edition, by Craig Hunt (O'Reilly Media, 2002).

As always, the manual pages for the various tools and utilities discussed will always be a good source of information. For example, the latest version of tcpdump’s documentation (man page) can be found at www.tcpdump.org/tcpdump_man.html.

# CHAPTER 12 Network Configuration

# Linux Administration: A Beginner's Guide

As with most modern operating systems, Linux distributions come with a robust set of graphical tools for administrating most of the networking-related functions within the system. Examples of these tools include NetworkManager (nm) and Wireless Interface Connection (WICD). Invariably, the GUI tools are merely pretty front-ends for manipulating plain-text files or very simple databases in the back-end.

Understanding how network configuration works under the hood in Linux distributions is invaluable and can come handy in many scenarios. First and foremost is when things are breaking and you can't start your favorite GUI, you'll find that being able to handle network configuration from the command line is crucial. Another benefit is remote administration: You might not be able to run a graphical configuration tool from a remote site. Issues such as firewalls and network latency will properly restrict your remote administration to the command line only. Finally, it's always nice to be able to manage network configuration through scripts, and command-line tools are well suited for scripting.

In this chapter, we will tackle an overview of network interface drivers, the tools necessary for performing command-line administration of your network interface(s).

# Modules and Network Interfaces

Network devices under Linux break the tradition of accessing all devices through the file abstraction layer. Until the network driver initializes the interface and registers itself with the kernel does there exist a mechanism for anything to access the interface. Typically, Ethernet devices register themselves with names such as ethX, emX, ensX, or pXpX, where X is the device or index number.

Depending on how your kernel was compiled, the device drivers for your network interface cards (NICs) may be compiled as a module. For most distributions, this is the default mechanism, since it makes it much easier to probe for new hardware.

If the driver is configured as a module and you have auto-loading modules set (default behavior), you might sometimes need to tell the kernel the mapping between device names and the module, or you simply need to pass on some special options to the module. This can be done by using (creating) an appropriate configuration file under the /etc/modprobe.d directory. For example, if your eth0 device is an Intel PRO/1000 card, you would add the following line to your /etc/modprobe.d/conf file:

```
alias eth0 e1000
```

Here, e1000 is the name of the device driver.
You can set this up for every network card, one based on the DEC Tulip chipset and for example, if you have two network cards, another on the RealTek 8169 chipset, your sample module configuration file—/etc/modprobe.d/example.conf—may include these lines:

```
alias eth0 tulip
alias eth1 r8169
```

Here, tulip refers to the network card with the Tulip chip on it, and r8169 refers to the RealTek 8169 card.

> TIP udev subsystem is the official mechanism for manipulating device names assigned to network devices such as Ethernet cards. This can be useful in overcoming the occasional unpredictability with the Linux kernel names and detects network devices.

You can find all of the network device drivers that are installed for your kernel in /lib/modules/uname -r/kernel/drivers/net directory, like so:

```
[rootserver]# cd /lib/modules/`uname -r`/kernel/drivers/net
[rootserver]# ls
```

Note backticks (versus single quotes) surround the embedded uname-r command. This will let be sure you are using the correct driver version for your current kernel version. If you are using a standard installation of your distribution, you to find that only one subdirectory should appear in the /lib/modules directory. If you have upgraded or compiled your kernel, you might find more than one directory.

If you want to see a driver's description without having to load the driver, use the modinfo command:

```
[rootserver]# modinfo
```

Keep in mind that not all drivers have descriptions associated with them, but most do.

# Consistent Device Naming

Recent Linux distributions use different mechanisms to achieve network device naming. This need was brought about by the way in which Linux kernel discovers and assigns names to Ethernet interface is not always predictable (it is influenced by hardware initialization, PCI bus topology, device code, and other factors). Most solutions rely on udev subsystem in one form or another. One of the approaches to solving this problem is to query the system BIOS for flags and name devices using a udev helper program called biosdevname. The aim is to guarantee that Ethernet cards and ports will be assigned names that match their physical location on the system board, and it specifically affects network adapters embedded on the motherboard and add-on adapters. This particular approach is common on Red Hat-based distributions (such as CentOS, RHEL, and Fedora), but is not common on the other distros such as Debian, Ubuntu, openSUSE, and so on.

The network device naming convention using biosdevname works like this:

- The Ethernet interface on systems with onboard NICs are named with the prefix em<PORT_NUMBER>, where <PORT_NUMBER> is the physical chassis label. (Continued)

The previous naming convention holds true when the following conditions are met:

- The system BIOS is SMBIOS version 2.6 or higher.
- The biosdevname=1 is specified as a boot-option/argument to the kernel.

The biosdevname naming scheme can be completely bypassed by passing the biosdevname=0 argument as a boot-option to the kernel in supported platforms.

# Network Device Configuration Utilities (ip, ifconfig, and nmcli)

A number of graphical and menu-driven tools have been written to wrap around the various command-line tools that we discuss in the following sections. Many of the wrapper GUI programs run with the various Linux distros, especially the distros that run in full desktop graphical mode.

As an administrator, you should get familiarity with and know how to configure network devices using any of the command-line utilities directly. Knowing how to do this is invaluable, for example, many additional options not shown in GUIs are exposed in the command-line interface (CLI). To help you gain familiarity
