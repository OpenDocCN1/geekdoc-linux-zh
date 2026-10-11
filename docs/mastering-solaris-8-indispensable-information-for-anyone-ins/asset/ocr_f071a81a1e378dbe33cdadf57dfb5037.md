cat /etc/release The cat command, when applied to the release file, prints very detailed information on the current version of the operating system.

ifconfig -a Use this command to display the network configuration information about all the network interfaces that are configured and that the operating system is aware of. Installed devices that aren't properly configured appear when you use the dmesg command. The ifconfig command also displays the status of the network card (IP, BROADCASTING, etc.), the Maximum Transmission Unit (MTU), the IP address, the subnet mask in hexadecimal, the broadcast address, and the Ethernet address.

arp -a Display the current arp table (Ethernet to IP).

prtconf List all peripherals and device drivers used to manage the peripherals. Included in the output of the prtconf command are the device path of the console frame buffer, firmware device derived from the PROM, information on pseudo devices, platform-dependent PROM information, PROM firmware version on the system, the actual hardware memory, and the machine architecture.

There are several files in the /etc directory that contain important network configuration information that you should examine in detail and keep records of. You might want to keep a printout of these files so that you can reestablish their values should something go wrong with your system. Although these files are described more fully in Chapters 9 and 14, they are briefly presented to you here:

hosts IP address to hostname table, which is a symbolic link to the /etc/inet/hosts file.

netmasks The netmask applied to the system, which is a symbolic link to the /etc/inet/netmasks file.

defaultgateway The default router.

nsswitch.conf Where the system gathers information.

resolv.conf The IP addresses of the DNS servers.

nodename The node name of the system.

hostname (Ethernet name) The hostname attached to an interface. Two examples of interfaces names are hostname.hme0 and hostname.1a0.

dhcp (Ethernet name) Present if the client is controlled by Dynamic Host Configuration Protocol (DHCP).

# # The file Command

There are situations in which a system administrator will come across a mystery file. One of the most useful commands with Solaris is the file command. This command performs a series of tests on a file to determine what type of file it is. The