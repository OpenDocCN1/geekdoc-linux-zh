# CHAPTER 2 | Basic Components of Linux Security

# More Boot Process Issues

The Transmission Control Protocol/Internet Protocol (TCP/IP) suite includes default port numbers for hundreds of services, such as 22 for SSH and 23 for Telnet. Some security professionals prefer to use nonstandard port numbers for key services. That obscurity can slow the efforts of black-hat hackers who want to break into a system.

Some services require network access during the boot process. For example, if you keep servers synchronized with the Network Time Protocol (NTP), those servers access external NTP servers during the boot process. The standard NTP port is 123. If you want to lock that port after the boot process is complete, you need to make sure the associated firewall isn't run until the NTP client is synchronized.

# Virtual Physical Security

Virtual machines add another dimension to the challenges of physical security. Standard Linux and group options add security to virtual machines. However, anyone who gains access to a virtual machine can more easily change virtual physical components. For example: a black-hat hacker who adds a CD file to a virtual CD drive would arouse less suspicion than a black-hat hacker who unlocks a CD/DVD drive on an actual physical system.

> NOTE
It's easier to modify virtual physical hardware. Although it takes time to look out or remove CD/DVD drives from physical systems, it's relatively easy to remove a CD/DVD drive from a virtual system. Although it is easier to install Linux from a CD/DVD drive, there is little need for that after installation is complete.

![](bbox=[0.915, 0.195, 0.985, 0.365])

# Linux Security Issues Beyond the Basic Operating System

While Linux distributions include a substantial number of applications and services, the essence of the Linux operating system is the kernel. Many security risks exist in applications and services beyond the kernel.

One of the main advantages of Linux is its structure as a multi-user operating system. When properly configured, Linux runs a black-hat hacker into one service, that user may gain access to the corresponding privileged account. However, that user won't have access to other accounts.

A GUI is also beyond the Linux operating system. If included, a GUI introduces a whole raft of additional security risks, discussed shortly.

# Service Process Security

For the purposes of this chapter, the boot process ends when the Linux kernel is loaded. The startup process then begins automatically, loading and starting a series of services configured in the default runlevel. A runlevel defines the services to be run. The default runlevel defines the services to be run after a system is booted. You'll read about runlevel and service management in Chapter 6.