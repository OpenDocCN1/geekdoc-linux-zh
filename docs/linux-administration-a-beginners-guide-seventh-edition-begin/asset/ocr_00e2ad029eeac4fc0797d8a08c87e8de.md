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
You can set this up for every network card, one based on the DEC Tulip chipset and for example, if you have two network cards,