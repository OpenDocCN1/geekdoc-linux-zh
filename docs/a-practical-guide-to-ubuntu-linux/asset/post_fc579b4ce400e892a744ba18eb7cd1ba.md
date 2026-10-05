
# CHAPTER SUMMARY 635

```
mysql SELECT * FROM people
-> WHERE password=PASSWORD(person);
```

| person | password | created | readperm | writeperm | executeperm |
| :--- | :--- | :--- | :--- | :--- | :--- |
| topsy | *8E5E773768B8F36F58A... | 2010-03-05 | 1 | 1 | 1 |

```
1 row in set (0.00 sec)
```

Use an UPDATE statement to give Topsy a NULL password:

```mysql
mysql> UPDATE people
-> SET password=NULL
-> WHERE person="topsy";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1 Changed: 1 Warnings: 0
```

```mysql
mysql> SELECT person,password
-> FROM people
-> WHERE password IS NULL;
```

| person | password |
| :--- | :--- |
| max | NULL |
| zach | NULL |
| topsy | NULL |

```
3 rows in set (0.00 sec)
```

# CHAPTER SUMMARY

The users-admin utility adds new users and groups to work with the system and modifies existing users' accounts. You can also use the equivalent command-line tools (useradd, usermod, userdel, groupadd, groupmod) to work with user accounts.

Backing up files on the system is a critical but often-overlooked part of system administration. Linux includes the tar, dump, cpio, and restore utilities to back up and restore files. You can also use more sophisticated packages such as amanda and various commercial products.

The scheduling daemon, cron, periodically executes scheduled tasks. You can schedule tasks using crontab and at.

System reports provide information on the health of the system. Two useful tools that generate these reports are vmstat, which details virtual memory, I/O, and CPU usage, and top, which reports on how the system is performing from moment to moment and can help you figure out what might be slowing it down.

Another aspect of system administration is solving problems. Linux has several tools that can help track down system problems. One of the most important of these tools is syslogd, the system log daemon. Using /etc/syslog.conf, you can control which error messages appear on the console, which are sent as email, and which go to one of several log files.

System administrators are frequently called upon to set up and administrate databases. MySQL is the M in LAMP (Linux, Apache, MySQL, PHP/Perl/Python), an open-source enterprise software stack. Many programming languages provide an interface to MySQL (e.g., C, PHP, Perl).

# EXERCISES

- 1. How would you list all the processes running vi?
2. How would you use kill to cause a server process to reread its configuration files?
3. From the command line, how would you create a user John Doe who has the username id and belongs to group 65535?
4. How would you notify users that you are going to reboot the system in ten minutes?
5. Give a command that creates a level 0 dump of the /usr filesystem on the first device on the system. Which command would you use to take advantage of a drive that supports compression? Which command would place a level 3 dump of the /var filesystem immediately after the level 0 dump on the tape?

# ADVANCED EXERCISES

- 1. If the system is less responsive than normal, what is a good first step in figuring out the problem is?
2. A process stores its PID number in a file named process.pid. Write a command line that terminates this process.
3. Working with root privileges, you are planning to delete some files but want to make sure the wildcard expression you use is correct. Suggest two ways to make sure you delete the correct files.
4. Create a crontab file that will regularly perform the following backups:
   a. Perform a level 0 backup once per month.
   b. Perform a level 2 dump one day per week.
   c. Perform a level 5 dump every day on which neither a level 0 nor a level 2 dump is performed.

In the worst-case scenario, how many restore commands would you have to give to recover a file that was dumped using this schedule?

# CONFIGURING AND MONITORING A LAN

IN THIS CHAPTER

- Setting Up the Hardware ....................... 638
Routers ..................................................... 638
NIC: Network Interface Card .................... 639
Configuring the Systems ................................ 641
Setting Up Servers ....................................... 646
Introduction to Cacti ....................................... 647

Networks allow computers to communicate and share resources. A local area network (LAN) connects computers at one site, such as an office, home, or library, and can allow the connected computers to share an Internet connection, files, and a printer. Of course, the most important reasons to set up a LAN is to allow systems to communicate while users enjoy multiplayer games.

This chapter covers the two aspects of configuring a LAN: setting up the hardware and configuring the software. It is not necessarily organized in the order that you will perform the tasks involved in setting up a particular LAN. Instead, read the chapter through, figure out how you will set up your LAN, and then read the parts of the chapter in the order appropriate to your setup. The final section discusses how to monitor devices on a network using Cacti.

# SETTING UP THE HARDWARE

Each system, or *node*, on a LAN must have a network interface card (NIC). Each system must connect to a central hub.

# CONNECTING THE COMPUTERS

Each system, or *node*, on a LAN must have a network interface card (NIC). Each system must connect to a central hub. If the LAN is connected to another network, such as the Internet, it must also have a router.

The simple network shown in Figure 17-1, four computers are connected to a switch. Assume computers 1 and 2 are communicating. With a hub (page 375), each conversation is limited by the slowest node. With a switch (page 375), each conversation can theoretically use the full bandwidth.

Hubs are usually less expensive than switches, although switches are getting cheaper. If you plan to use a wireless network, a hub is likely to be fast.

Wireless access point (WAP) A wireless access point (WAP) connects a wireless network to a wired one. Typically a WAP acts as a transparent bridge. In a wireless network, the bandwidth is shared among nodes.

# ROUTERS

A router (page 377) connects a LAN to another network, such as the Internet. A router can perform several functions, the most common of which is allowing systems to share an Internet connection and IP address (NAT, page 881). When a router uses NAT, the packets from each system on the LAN appear to come from a single IP address. A router can also act as a firewall.

You have several choices for routers:

- A simple hardware router is relatively cheap and does most of the things required by a small network.

# SETTING UP THE HARDWARE 639

![](img/45ffcd21497435daa35084a84b95d07_689_0.png)

Figure 17-1 A simple network

- You can set up an Ubuntu system as a router. The Linux kernel can use guard (page 876) or iptables (page 880) to implement a firewall to protect a system.
- You can use a special-purpose distribution/operating system tailored as a router. For example, SmoothWall (www.smoothwall.org), pfSense (www.pfsense.com), and m0n0wall.ch/wall provide browser-based configurations in the style of a hardware router.

# NIC: NETWORK INTERFACE CARD

Each system's NIC may be a separate Ethernet card (wired or wireless) or the NIC may be built into the motherboard.

Supported NICs Linux supports most wired and wireless Ethernet NICs.
Unsupported wireless NICs If a wireless network card is not supported under Linux directly, you may be able to work it with NdisWrapper (sourceforge.net/projects/ndiswrapper; ndiswrapper-common, ndiswrapper-utils-1.9, and ndisgtk packages), which use Win32 drivers. NdisWrapper is a kernel module that provides a subset of the Windows network driver API. See help.ubuntu.com/Community/Wifi/NdisWrapper for instructions on installing a Windows driver.

Wireless bridge An alternative to a wireless NIC is a wireless bridge. A wireless bridge forwards packets between wired and wireless interfaces, eliminating the need for wireless drivers. This simple device has an Ethernet port that plugs into a NIC and an 802.11 (wireless) controller. While carrying a bridge is usually not feasible for mobile users, a wireless bridge is an easy way to migrate a desktop computer to a wireless configuration.
