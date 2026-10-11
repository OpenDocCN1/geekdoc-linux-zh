
## CHAPTER SUMMARY

The system-config-users utility adds new users and groups to the system and modifies existing users' accounts. You can also use the equivalent command-line tools (useradd, usermod, userdel, groupadd, and groupmod) to work with user accounts. Backing up files on the system is a critical and often overlooked part of system administration. Linux includes the tar, cpio, dump, and restore utilities to back up files to tape or to another system and restore files. You can also use more sophisticated packages such as amanda and various commercial products.

The system scheduling daemon, *cron*, periodically executes scheduled tasks. You can schedule tasks using *crontab* and *at*. System reports present information on the health of the system. Two useful tools that generate these reports are *vmstat*, which details virtual memory, I/O, and CPU statistics, and *top*, which reports on how the system is performing from moment to moment and can help you figure out what might be slowing it down.

Another aspect of system administration is solving problems. Linux includes several tools that can help you track down system problems. One of the most important of these tools is *rsyslogd*, the system log daemon. Using */etc/rsyslogd.conf*, you can control which error messages appear on the console and which go to one of several log files.

System administrators are frequently called upon to set up and administrate *MySQL* databases. *MySQL* is the M in *LAMP* (Linux, Apache, *MySQL*, PHP/Perl/Python), an open-source enterprise software stack. Many programming languages provide an interface to *MySQL* (e.g., C, PHP, Perl).

### EXERCISES

- 1. How would you list all the processes running vi?
- 2. How would you use *kill* to cause a server process to reread its configuration files?
- 3. From the command line, how would you create a user named John Doe who has the username *jd* and who belongs to group *65535*?
- 4. How would you notify the users of the system that you are going to reboot the system in 10 minutes?
- 5. Give a command that will create a level 0 dump of the /usr filesystem on the first tape device on the system. Which command would you use to take advantage of a drive that supports compression? Which command would place a level 3 dump of the /var filesystem immediately after the level 0 dump on the tape?

### ADVANCED EXERCISES

- 6. If the system is less responsive than normal, what is a good first step in figuring out where the problem is?
- 7. A process stores its PID in a file named *process.pid*. Write a command line that will terminate the process.
- 8. **Working as root**, you are planning to delete some files but want to make sure that the wildcard expression you will use is correct. Suggest two ways you could make sure that you deleted the correct files.
- 9. Create a cron file that will regularly perform the following backups:
  - a. Performs a level 0 backup once per month.
  - b. Performs a level 2 dump one day per week.
  - c. Performs a level 5 dump every day that neither a level 0 nor a level 2 dump is performed.

In the worst case, how many restores would you have to perform to recover a file that was dumped using the preceding schedule?

## 17 CONFIGURING AND MONITORING A LAN

### IN THIS CHAPTER

- Setting Up the Hardware . . . . . . . . 596
- Gateways and Routers . . . . . . . . 597
- NIC: Network Interface Card . . . . . . 597
- Configuring the Systems . . . . . . . . 598
- The Network Configuration Window (system-config-network) . . . . . . 601
- iwconfig: Configures a Wireless NIC . . . . . . . . 605
- Setting Up Servers . . . . . . . . . 606
- Introduction to Cacti . . . . . . . . . 607

Networks allow computers to communicate and share resources. A local area network (LAN) connects computers at one site, such as an office, home, or library, and can allow the connected computers to share an Internet connection and a printer. Of course, one of the most important reasons to set up a LAN is to allow systems to communicate while users enjoy multiplayer games.

This chapter covers the two aspects of configuring a LAN: setting up the hardware and configuring the software. This chapter is not necessarily organized in the order you will perform the tasks involved in setting up a particular LAN: Read the chapter through, figure out how you will set up your LAN, and then read the parts of the chapter in the order appropriate to your setup. The final section discusses how to monitor a network using Cacti.

### SETTING UP THE HARDWARE

Each system, or node, on a LAN must have a network interface card (NIC). NICs can be connected to the network with cables or radio waves (wireless); in either case, each system must connect to a central hub. If the network is connected to another network, such as the Internet, it must also have a router, or gateway. The router can be either one of the systems on the LAN or a dedicated piece of hardware.

### CONNECTING THE COMPUTERS

A modern Ethernet-based LAN has a connection between each computer and a central hub. Two kinds of hubs exist: passive (sometimes just called a hub) and switching (called a switch). A passive hub simply connects all systems together and shares the network bandwidth among the systems. A switching hub puts each system on its own network with the switch and routes packets between those networks, providing each system with the full network bandwidth.

In the simple network shown in Figure 17-1, four computers are connected to a single hub. Assuming the hub is passive, when computers 1 and 2 are communicating at the same time as computers 3 and 4, each conversation is limited to a maximum of half the network bandwidth. If the hub were a switch, each conversation could use the full network bandwidth.

Usually hubs are less expensive than switches. If you plan to use the network for sharing an Internet connection and light file sharing, a hub is likely to be fast enough. If systems on the network will exchange files regularly, a switch may be more appropriate. Refer to “Ethernet” on page 361 for a discussion of switches, hubs, and cables.

![](img/f28adb66a7398a382f0505e0ba74a872_636_0.png)

Each computer on a LAN must be connected to the hub. If you are using more than one hub, connect the port labeled **uplink** on one hub to a normal port on another hub.

- **Wireless access point (WAP)**
  - A wireless access point (WAP) connects a wireless network to a wired one. Typically a WAP acts as a transparent bridge, forwarding packets between the two networks as if they were one. If you connect multiple WAPs in different locations to the same wired network, wireless clients can roam transparently between the WAPs.
  - Wireless networks do not require a hub, although a WAP can optionally fill a similar role. In a wireless network, the bandwidth is shared among all nodes within range of one another; the maximum speed is limited by the slowest node.

### GATEWAYS AND ROUTERS

If the LAN you are setting up is connected to another network, such as the Internet, you need a router, sometimes called a gateway. A router can perform several functions, the most common of which is allowing several systems to share a single Internet connection and IP address (NAT; page 820). When a router uses NAT, the packets from each system on the LAN appear to come from a single IP address; return packets are passed back to the correct system.

You have several choices for routers:

- A simple hardware router is relatively cheap and does most things required by a small network.
- You can set up a Fedora/RHEL system as a router. The Linux kernel can use iptables (page 819) to route packets between network adapters.
- You can use a Linux distribution tailored for use as a router. For example, SmoothWall (www.smoothwall.org) provides a browser-based configuration in the style of a hardware router.

### NIC: NETWORK INTERFACE CARD

Each system's NIC may be a separate Ethernet card (wired or wireless) or the NIC may be built in to the motherboard.

- **Supported NICs**
  - Linux supports most wired Ethernet NICs. Fewer wireless NICs are supported. See “More Information” on page 617 for references.
- **Unsupported wireless NICs**
  - If a wireless network card is not supported under Linux directly, you may be able to get it to work using NdisWrapper (ndiswrapper.sourceforge.net; also available as an rpm file from the Fedora and RHEL5 repositories at rpmfusion.org), which uses Win32 drivers. NdisWrapper is a kernel module that provides a subset of the Windows network driver API. No Fedora/RHEL package contains this program.
- **Wireless bridge**
  - An alternative to a wireless NIC is a wireless bridge. A wireless bridge forwards packets between wired and wireless interfaces, eliminating the need for wireless drivers. This simple device contains an Ethernet port that plugs into a NIC and an 802.11 (wireless) controller. While carrying a bridge around is usually not feasible for mobile users, it is an easy way to migrate a desktop computer to a wireless configuration.
