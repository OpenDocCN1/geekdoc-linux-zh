
## 8. The Linux resolver:
- a. resolves a host or domain name to an IP address and vice versa
- b. resolves conflicts between multiple IP addresses on the same host
- c. resolves contention between multiple Ethernet cards in the same computer
- d. resolves authorization issues for X clients

## 9. Which is not a valid configuration file mentioned in this chapter?
- a. /etc/host.conf
- b. /etc/nsswitch
- c. /etc/resolv.conf
- d. /etc/hosts

## 10. The /etc/hosts file is checked before contacting a DNS server only if:
- a. The /etc/host.conf or /etc/nsswitch file says to use /etc/hosts first.
- b. A DNS server cannot be contacted.
- c. The search keyword in /etc/resolv.conf indicates a local domain name.
- d. A graphical tool was used to configure both /etc/resolv.conf and /etc/hosts.

## 11. Networking devices differ from other Linux devices in that:
- a. Networking devices use a different set of major and minor device numbers than devices that do not rely on kernel modules.
- b. Networking devices can transmit data much faster than other types of devices.
- c. Networking devices are not directly visible in the /dev subdirectory but are created on the fly when a networking device module is loaded into the kernel.
- d. Networking devices can only be accessed via shell scripts.

## 12. Which is not a valid ifconfig command?
- a. ifconfig eth0 up
- b. ifconfig eth0 192.168.100.1 netmask 255.255.255.0 broadcast 255.255.255.0
- c. ifconfig
- d. ifconfig eth0 ifup

## 13. Which information field is not part of the output of the route command?

## 14. Which statement is true about the following command:
```
route add -net 192.168.20.0 netmask 255.255.255.0 gw 192.168.10.1 dev eth0.
```
- a. It is valid and defines the router that can reach network 192.168.20.0.
- b. It is valid and defines a default gateway for all traffic not destined for network 192.168.20.0.
- c. It is invalid because it does not specify the host IP address of the source of the packets to be routed.
- d. It is invalid in format because it lacks needed dashes before command-line options.

## 15. You would use the arp command to:
- a. Send a hardware address to a remote host per an ARP protocol request.
- b. Turn on and off ARP functionality for your network.
- c. Collect host name-to-IP address mappings for each of the hosts on your local network.
- d. View or modify the ARP cache containing hardware address to IP address mappings.

## 16. A correct device designation for an IP alias to the first Ethernet card is:
- a. eth00
- b. eth0:1
- c. Ethernet II
- d. eth1:0

## 17. IP forwarding is enabled by the following command:
- a. ifconfig eth0 ip_forward
- b. arp ip_forward
- c. route add default ip_forward -net 192.168.10.0 netmask 255.255.255.0
- d. echo 1 > /proc/sys/net/ipv4/ip_forward

## 18. Each time a user prints a file, a ______________ is created.

## 20. Printer definitions, or print queue definitions, are stored in which file?
a. /var/spool/lpd/lp
b. /var/adm/acct
c. /etc/printcap
d. /etc/lpd.conf

## 21. The graphical utility provided in Red Hat Linux and Fedora to configure a printer definition is:
a. printconf-gui
b. lpc
c. cupsd
d. lpoptions

## 22. Print filters are used to:
a. Convert graphics formats before printing images.
b. Prepare documents in a printer-specific format.
c. Remove unprintable characters from documents.
d. Compress print job files before transfer to a remote print server.

## 23. Multiple options in the printcap file are separated by:
a. an equals sign
b. two colons
c. a carriage return/new line
d. a tab

## 24. The CUPS printing architecture does not allow system administrators to:
a. Use the same printing system on diverse UNIX and Linux systems.
b. Check the status of print jobs on a remote server using a browser-based interface.
c. Use multiple instances of a printer that include specific sets of printing options.
d. Graphically configure features specific to one model of printer, such as duplex printing or dots-per-inch settings.

## 25. Explain the difference between the lpc commands up, enable, and start.

## 26. CUPS management is accomplished:
a. by contacting a Web server-type server using port 631
b. by using a browser to reach linuxprinting.org
c. by using port 631 of printconf-gui or the KDE Control Center
d. by using any standard Web server on a system with cupsd and the appropriate PPD files installed

## 27. The _____________ utility displays the owner, size, and submission time for print jobs.
a. lpq
b. lprm
c. lpc
d. lpd

## 28. A CUPS class lets you:
a. Aggregate print jobs for multiple printers using a single name for increased end-user convenience.
b. Specify options that apply to a printer definition when you indicate the class name as the selected printer.
c. Specify the features that a printer model supports, such as duplex printing, color printing options, scaling, or multiple paper trays.
d. Control print jobs that were submitted to a remote printer.

## 29. Which lpc command stops the printing of the current print job?
a. lpc abort
b. lpc cancel
c. lpc stop
d. lpc disable

## 30. Describe how both LPRng and CUPS can be supported by the same commands such as lpr and lpq.

## Hands-On Projects

## Project 12-1

In this project, you explore the Address Resolution Protocol (ARP). To complete this project, you should have a network connection configured with at least one other host on the network. An Internet connection is used for the last part of the project but is not strictly necessary.

- 1. Log in to Linux and open a command-line window. Change to root access using the su - command.
- 2. Enter the command arp -a to display the contents of the ARP cache on your Linux system. The result may be nothing—the cache is probably empty at this point if you have not done any networking in the last few minutes. Each entry is saved only for about two minutes.
- 3. If the ARP cache is not empty, note the contents carefully. See if you can identify a neighbor on the network (in your computer lab, for example) that is not listed in the output of the command. Obtain that neighbor's IP address.
- 4. Ping your neighbor using a command such as this (substitute the neighbor's IP address for 192.168.100.45):
  `ping 192.168.100.45`
- 5. Press Ctrl+c to exit the ping command. Run the arp command a second time:
  `arp -a`
  You should see your neighbor's system listed (as indicated by an IP address that you recognize).
- 6. Ping an Internet site such as 155.99.1.2 or 192.20.4.70. Press Ctrl+c to exit the ping command.
- 7. Run arp -a again. Why is no additional entry included for the new site that you pinged? Close all windows and log off.

![](img/43f64015de86d989e30eff5bb284fb96_595_0.png)

## Project 12-2

In this project, you create an IP alias by adding a second IP address to your Ethernet card. To complete this project, you must be connected to an Ethernet network using a static IP address (not DHCP) and have been assigned a second IP address for this project by your instructor or system administrator. You must be logged in as root to complete this project.

- 1. Log in to Linux and open a command-line window.
- 2. Enter su - to change to root access.
- 3. Enter ifconfig without any parameters to see that you have a correctly configured Ethernet (eth0) interface.
- 4. Change to the directory /etc/sysconfig/networking/devices using this command:
  `cd /etc/sysconfig/network-scripts`
- 5. Copy the configuration file for the eth0 interface as a basis for creating a new interface called eth0:1, which will be an IP alias to the same physical Ethernet card:
  `cp ifcfg-eth0 ifcfg-eth0:1`
- 10. Create a link from the new device definition you created in each of the networking configuration directories where the network management scripts expect to find them. Enter these two commands while still working in the /etc/sysconfig/network-scripts directory:
  ln ifcfg-eth0:1 ../networking/device/
  ln ifcfg-eth0:1 ../networking/profiles/default
- 11. Restart networking by entering service network restart.
- 12. Run the ifconfig | less command. Notice that you now have a new, third interface: eth0:1.
- 13. Ping the IP address of your eth0 interface. Ping the IP address of your eth0:1 interface. You could now use these independent interfaces to set up two separate Web sites or FTP servers on the same computer.
- 14. Delete the three files you created, confirming the deletion if prompted (these commands assume you are still working in the /etc/sysconfig/network-scripts directory):
  rm ifcfg-eth0:1
  rm ../networking/device/ifcfg-eth0:1
  rm ../networking/profiles/default/ifcfg-eth0:1
- 15. Restart networking again: service network restart
- 16. Run the ifconfig command to verify that you once again have only two networking devices: lo and eth0. Close all windows and log off.

## Project 12-3

In this project, you use the ping command to explore how the Linux resolver operates in conjunction with the configuration files you learned about in this chapter. To complete this project, you need Internet access and access to the root account on your Linux system. For each of the ping commands described in this project, you only need to let two or three response lines appear to verify that the command works, then press Ctrl+c to interrupt ping and continue with the next step.

- 1. Log in to Linux and open a command-line window.
- 2. Enter su - to change to root access.
- 3. Choose a site that allows you to ping it and execute the ping command to see that it is alive. We’ve used the University of Utah (one of the Internet’s foundational members) as an example:
  `ping www.utah.edu`
- 4. As the ping packets are returned, note how the domain name and a corresponding IP address for the site are shown on each line. Write down the IP address.
