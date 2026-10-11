
## 12. Which utility is used to change the IP address of a network interface?
- A. ipconfig
- B. ifconfig
- C. hostname
- D. netstat

## 13. Which two utilities can be used to view the routing table?
- A. netstat
- B. traceroute
- C. route
- D. ifconfig

## 14. On a Debian system, which file contains the hostname of the local machine?
- A. /etc/hosts
- B. /etc/HOSTS
- C. /etc/hostname
- D. /etc/HOSTNAME

## 15. Which file contains the name servers to be used by the local machine for hostname resolution?
- A. /etc/hosts
- B. /etc/resolv.conf
- C. /etc/services/
- D. /etc/network/interfaces

## 16. Which of the following is a correct entry in the /etc/hosts file?
- A. dee dee 10.254.90.135/ip
- B. nameserver 10.254.90.131
- C. search the-nashes.net
- D. 10.254.90.135 dee dee.the-nashes.net

## 17. Chat scripts are used to perform which of the following functions?
- A. Specify connection device
- B. Configure a PPP connection
- C. Establish a PPP connection
- D. Specify idle timeout of a PPP connection

## 18. The `pppd` application must receive its IP address via DHCP.
- A. True
- B. False

## 19. Which of the following is NOT a valid option of the `pppd` command?
- A. reconnect
- B. connect
- C. disconnect
- D. holdoff

## 20. Which of the following utilities is used to stop a network interface?
- A. ifconfig
- B. netstat
- C. down
- D. stop

# Scenarios

## 1. Your company has decided to install a small network in a remote office. This office will not be connected to the Internet, so you decide to use the 192.168.1.0 network address. Which subnet mask would allow you to have 32 computers on each subnet of the network? How many subnets would this address allow?

# Answers to Chapter Questions

# Chapter Pre-Test

- 1. Each host on the Internet is known by a unique IP address.
- 2. The ICMP protocol handles error reporting.
- 3. The NetBIOS session service uses port 139.
- 4. The Telnet application provides terminal emulation.
- 5. The `/etc/hosts` file provides manual IP address-to-hostname mappings.
- 6. The `traceroute` tool allows you to view the path of a packet through the network.
- 7. DHCP is used to automatically configure a workstation's IP information.
- 8. The `ifconfig` tool is used to assign an IP address to a network adapter.
- 9. A chat script is used to supply information such as telephone number, user name, and password that are used when making a PPP connection.
- 10. The `holdoff` option is used to automatically reconnect a PPP connection in the case of an interruption.

# Assessment Questions

- 1. **D.** The address 192.168.90.131 is a class C address between the ranges of 192.0.0.0 and 223.0.0.0. See the “Dividing networks with subnet masks” section for more information.
- 2. **subnet mask**. The subnet mask is anded with the IP address to provide the network ID and the host ID. See the “Dividing networks with subnet masks” section for more information.
- 3. **B.** There are 4,094 available network IDs provided by 12 bits. The formula for calculation is $2^{12} - 2$. See the “Dividing networks with subnet masks” section for more information.
- 4. **C.** The TCP protocol is connection-oriented, using sessions to provide reliable transfer of packets. See the “Transmission Control Protocol” section for more information.
- 5. **C.** By default, SMTP operates on port 25. See the “Ports” section for more information.
- 6. **ARP**. ARP provides hardware address-to-IP address mapping and translation. See the “Address Resolution Protocol” section for more information.
- 7. **A.** The `put` command is used to upload files to an FTP server. See the “FTP” section for more information.
- 8. **D.** The `host` utility allows you to view the host and domain name when an IP address is entered. See the “host” section for more information.
- 9. **traceroute**. The `traceroute` utility displays every hop between the local and remote hosts. See the “traceroute” section for more information.
- 10. **D.** The `whois` utility provides information about the registration, name servers, and contacts for the specified domain. See the “whois” section for more information.
- 11. **A.** The `dhcpd` daemon allows a Linux server to provide DHCP information to clients. See the “DHCP” section for more information.
- 12. **B.** The `ifconfig` utility is used to change the IP address of a network interface. The `ipconfig` utility is used by Windows-based systems. See the “ifconfig” section for more information.
- 13. A and C. The routing table can be viewed using the `route` command and using `netstat -r`. See the "route" and "netstat" sections for more information.
- 14. D. Debian systems use the `/etc/HOSTNAME` file to store the hostname of the local machine. The `/etc/hostname` file is used by Red Hat. See the “`/etc/HOSTNAME` and `/etc/hostname`” section for more information.
- 15. B. The `/etc/resolv.conf` file contains the domain search listing and the name servers to use for hostname resolution. See the “`/etc/resolv.conf`” section for more information.
- 16. D. Entries in the `/etc/hosts` file contain an IP address followed by the corresponding hostname. See the “`/etc/hosts`” section for more information.
- 17. C. Chat scripts are used to establish a PPP connection; `pppd` is used to configure the connection. See the “`pppd`” section for more information.
- 18. B. `pppd` can utilize either static or dynamic IP addresses. See the “`pppd`” section for more information.
- 19. A. `reconnect` is not a valid option of `pppd`. See the “`pppd`” section for more information.
- 20. A. The `ifconfig` utility is used to stop a network interface. See the “`ifconfig`” section for more information.

# Scenarios

- 1. The 192.168.1.0 network address uses the default mask of 255.255.255.0 to allow for 254 hosts on one subnet. Five bits allow for only 30 hosts, so six bits must be used for hosts. This allows for up to 62 hosts on a subnet. The two bits that are left for subnets will allow for two possible subnets. This would appear as 1100 0000 and would create the subnet mask of 255.255.255.192.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_631_0.png)

# Managing Network Services

## EXAM OBJECTIVES

Exam 102 ✦ General Linux, Part 2

### **1.12 Networking Fundamentals**

- **Fundamentals of TCP/IP.** Demonstrate an understanding of network masks and what they mean (i.e. determine a network address for a host based on its subnet mask), understand basic TCP/IP protocols (TCP, UDP, ICMP) and also PPP, demonstrate an understanding of the purpose and use of the more common ports found in /etc/services (20, 21, 23, 25, 53, 80, 110, 119, 139, 143, 161), demonstrate a correct understanding of the function and application of a default route. Execute basic TCP/IP tasks: FTP, anonymous FTP, telnet, host, ping, dig, traceroute, whois.

### **1.13 Networking Services**

- **Configure and Manage inetd and related services.** Configure what services are available through inetd, use tcp-wrappers to allow or deny services on a host-by-host basis, manually start, stop, and restart internet services, configure basic network services including telnet and ftp. Includes managing inetd.conf, hosts.allow, and hosts.deny.

*(Continued)*

# EXAM OBJECTIVES (CONTINUED)

### **1.13 Networking Services** *(Continued)*

- **Operate and perform basic configuration of sendmail.** Modify simple parameters in sendmail config files (modify the DS value for the “Smart Host” if necessary), create mail aliases, manage the mail queue, start and stop sendmail, configure mail forwarding (forward), perform basic troubleshooting of sendmail. Does not include advanced custom configuration of sendmail. Includes commands mailq, sendmail, and newaliases. Includes aliases and mail/ config files.
- **Operate and perform basic configuration of apache.** Modify simple parameters in apache config files, start, stop, and restart httpd, arrange for automatic restarting of httpd upon boot. Does not include advanced custom configuration of apache. Includes managing httpd conf files.
- **Properly manage the NFS, smb, and nmb daemons.** Mount remote filesystems using NFS, configure NFS for exporting local filesystems, start, stop, and restart the NFS server. Install and configure Samba using the included GUI tools or direct edit of the /etc/smb.conf file (Note: This deliberately excludes advanced NT domain issues but includes simple sharing of home directories and printers, as well as correctly setting the nmbd as a WINS client).
- **Setup and configure basic DNS services.** Configure hostname lookups by maintaining the /etc/hosts, /etc/resolv.conf, /etc/host.conf, and /etc/nsswitch.conf files, troubleshoot problems with local caching-only name server. Requires an understanding of the domain registration and DNS translation process. Requires understanding key differences in config files for bind 4 and bind 8. Includes commands nslookup, host. Files: named.boot (v.4) or named.conf (v.8)
