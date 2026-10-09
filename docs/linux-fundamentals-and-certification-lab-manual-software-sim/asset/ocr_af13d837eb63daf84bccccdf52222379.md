• **Take advantage of your friends and relatives** Do you know someone that is already using Linux? Don't be shy about asking for help. Most Linux users not only are willing to answer your questions but will offer to help. One great thing about using Linux is its network accessibility. If you ask someone for help, they can easily give them access to your system through SSH where they can check or change your Linux operating system remotely.

# ## SUMMARY

Troubleshooting is a skill that is learned and requires practice. The first technique of troubleshooting is to collect information about the problem. This can be done by interviewing users, evaluating configuration files, and making physical inspections.

After collecting information, you analyze the symptoms to determine the area of the problem. The problem is then localized to specific hardware or software. After the problem is determined and corrected, the system should be tested to ensure that no other problems exist.

Log files, in the /var/log directory, are a good source of information when troubleshooting a problem. The primary files to view are /var/log/messages, /var/log/secure, and individual application logs. The /etc/syslog.conf file is the configuration file for system log files.

Information about processes can be discovered with the ps and top programs. Viewing a list of currently running processes may help determine where a problem lies. The top program can be used to view how the system is performing.

Disk drive problems can be repaired with the fsck program. To prevent disk drive problems from causing system downtime, consider using a RAID system. Ensure that you can start the system regardless of hard drive problems by having a current emergency boot disk.

EIDE/ATA hard drive performance can be improved by using the hdparm program. The hdparm program is used to evaluate hard drive performance.

Network servers depend on services running on the Linux operating system. Services can stop, hang up, or stop responding. Use the service command to start, stop, restart, and view the status of running services.

Network problems are evaluated by using the OSI model. Physical layer problems are evaluated first, then data-link layer problems, network layer problems, and so on. To help isolate network problems, network testers can be used to check cables and other network components. The commands ping, telnet, tracert, traceroute, nstat, nstat, ifconfig, and dig can be used to check all layers of the network.

To find files in the file system, use the commands find, whereis, locate, and which. The find command is one of the most versatile file finding programs, allowing you to search for not only filenames but file characteristics as well.

Patching the kernel should be done with care. Patching can provide updated device drivers and fixes to operating system exploits. Make sure that a backup is completed and an emergency disk is available before replacing the kernel.

# ## SELF-TEST

+   1. The configuration file that contains the location of log files and what they will contain is _______________.
	a. /var/log/messages
	b. /var/log/secure
	c. /etc/syslog.conf
	d. /etc/logs.conf