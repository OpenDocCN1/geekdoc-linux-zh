
| Competency | Location in This Book (Chapter, Heading) |
|---|---|
| 2.5.50.1 Configuration files | |
| 2.5.50.2 Modules | |
| 2.5.50.3 Virtual hosts | |
| 2.5.50.4 Virtual e-mail | |
| 2.5.60 Configuration of X Window Desktops | Chapter 15, "X Window System Advanced Configuration" |
| 2.5.60.1 fvwm95 | |
| 2.5.60.2 AfterStep | |
| 2.5.60.3 Window maker | |
| 2.5.60.4 KDE | |
| 2.5.60.5 Gnome | |
| 2.5.70 Benchmarks | Chapter 15, "Security Issues" |

## 2.6 Troubleshooting

| Competency | Location in This Book (Chapter, Heading) |
|---|---|
| 2.6.10 Daemons | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.20 File system | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.30 Hardware | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.40 Log files | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.50 Core dump control | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.60 Ul limit in bash | Chapter 15, "Troubleshooting and Recovery" |
| 2.6.70 Limit in tcsh or rlimit ksh | Chapter 15, "Troubleshooting and Recovery" |

## Course 3X0-103 Linux Networking

![](img/43f64015de86d989e30eff5bb284fb96_831_0.png)

As noted at the beginning of this appendix, this book doesn't cover these objectives. They are provided for information only. Additional detail on these advanced topics can be found in Course Technology's Guide to Linux Networking and Security.

## 3.1 Theory of Operation

### 3.1.10 LAN/WAN and the Internet

3.1.10.1 Contrast LAN with point-to-point transmission

3.1.10.2 Describe the speed/distance tradeoff for copper versus fiber-optic cables

3.1.10.3 Describe the LAN/WAN boundary and Internet subnet characteristics

### 3.1.20 Communication Technology

3.1.20.1 Define the IPv4 address format

3.1.20.2 Describe IPv4 address classes and design tradeoff

3.1.20.3 Describe IPv4 classless address conservation

3.1.20.4 Contrast IPv4 and IPv6 design tradeoffs

### 3.1.30 Network Physical versus Logical Topology

3.1.30.1 Define Ethernet singlecast, multicast, and broadcast routing

3.1.30.2 Describe store and forward point-to-point networking with explicit routing

3.1.30.3 Describe point-to-point emulation of broadcast and its tradeoff

3.1.30.4 Define subnet addressing and logical versus physical broadcasting

3.1.30.5 Contrast multicast protocol and network topology

### 3.1.40 Internet Architecture Networking Protocols

3.1.40.1 Describe IP host-to-host addressing

3.1.40.1 Describe host-relative ports or program-to-program addressing

3.1.40.2 Contrast the functions of TCP with UDP

3.1.40.3 Describe the role of the boundary zone and contrast network IP, ICMP, and ARP

### 3.1.50 Network adapter and software relationships

### 3.1.60 Domain Name Service (DNS)

3.1.60.1 Describe the role and general structure of the boot.named configuration file

3.1.60.2 Describe the record look up mechanism and explain the role of the dot (.) operator

3.1.60.3 Contrast A, CNAME, PTR, and NS resource records

3.1.60.4 Contrast authoritative resource records, non-authoritative resource records, and name updates

### 3.1.70 Manual address assignment

3.1.70.1 Describe the reverse name lookup and route table configuration problem

3.1.70.2 Contrast adding hosts, subnets, and gateways

3.1.70.3 Describe default route creation when routing multiple subnets

### 3.1.80 UUCP subsystem

3.1.80.1 Describe the overall design and tradeoff of using UUCP

3.1.80.2 Contrast uucico and uucp

### 3.1.90 Short Message Block (SMB)

3.1.90.1 Describe the overall design of SMB

3.1.90.2 Contrast smbd and nmbd servers

3.1.90.3 Describe the general structure of the smb.conf file

### 3.1.100 Describe the overall design of IPX and Novell compatibility

3.1.100.1 Describe general IPX interface configuration and detection issues

3.1.100.2 Describe general IPX router specification with RIP & SAP protocols

### 3.1.110 Describe the overall design of the Network File System (NFS)

3.1.110.1 Contrast the role of the /etc/fstab versus exports configuration files

3.1.110.2 Display and interpret NFS statistics

3.1.110.3 Show the mount information for an NFS server

## 3.2 Base System

### 3.2.10 Network device configuration

3.2.10.1 Describe BIOS device enabling

3.2.10.2 Describe how to confirm kernel recognition of network devices

3.2.10.3 Describe run-time network device driver installation

3.2.10.4 Describe the relationship between logical device names and network drivers

3.2.10.5 Describe the role of the ifconfig and route utilities

### 3.2.20 Network Interfaces

3.2.20.1 Contrast ISDN, DSL, Cable modem, and T1 digital services

3.2.20.2 Contrast Serial with parallel computer to computer interconnection

3.2.20.3 Describe how to confirm serial port operation and configuration

3.2.20.4 Define PPP, describe vmdial and pppd

3.2.20.5 Describe an Ethernet device, and contrast logical and physical addresses

### 3.2.30 Logical network address configuration

3.2.30.1 Describe the role of the ARP table, and explain how to interpret its content

3.2.30.1.a Describe how to install routing shortcuts into the ARP table

3.2.30.2 Describe the role of the routing table

3.2.30.2.a Describe how to install a new network device into the routing table

3.2.30.2.b Describe how to add a subnet to the routing table

3.2.30.2.c Describe how to add a default route to the routing table

3.2.30.2.d Describe how to add additional subnets that use one default path

### 3.2.40 Describe the overall operation of a proxy IP Firewall

3.2.40.1 Contrast the ACCEPT, DENY, REJECT, MASQ, REDIRECT, and RETURN operators

3.2.40.2 Contrast the incoming, masquerade, and outgoing tables

### 3.2.50 Private networks

3.2.50.1 Describe the ipchains commands that establish a private network

3.2.50.2 Describe how to configure combined multi-private and multipublic subnets

3.2.50.3 Describe how to allow access to private network servers from the Internet

### 3.2.60 Proxy application servers

3.2.60.1.a Describe the role of squid and give its design tradeoff

3.2.60.1.b Describe the role of samba and give its design tradeoff

### 3.2.70 Describe IGMP Multicast

## 3.3 Shells and Commands

3.3.10 Contrast domain name service, named, and configuration

3.3.20 Describe host name lookup in with nslookup

3.3.30 Explain the problem with DNS and network troubleshooting

3.3.40 Interpret netstat's output to describe the state of network connections

3.3.50 Describe how to construct network connections

3.3.60 Explain how to view and manipulate routes

3.3.70 Explain how to view and manipulate logical to physical address translations

3.3.80 Explain how to attach network addresses to a device driver

3.3.90 Explain how to load a NIC device driver

3.3.100 Describe the use of /etc/resolv.conf for DNS

3.3.110 Describe the use /etc/hosts for shorthand names

3.3.120 Explain how to configure firewalls and private networks

3.3.130 Explain Point-to-Point Protocol (PPP) configuration

## 3.4 System Services

### 3.4.10 Describe the domain name service (DNS) and give its tradeoff

3.4.10.1 Top-level domain names and root servers

3.4.10.2 SOA and forward versus reverse names

3.4.10.3 Multiple domains (zones) and transfers

3.4.10.4 Primary, secondary, and tertiary servers

### 3.4.20 FTP

3.4.20.1 Anonymous

3.4.20.2 Incoming

3.4.20.3 /etc/ftpaccess

### 3.4.30 NFS

3.4.30.1 /etc/exports

### 3.4.40 Internet super server

3.4.40.1 daemon (inetd)

3.4.40.2 /etc/inetd.conf

3.4.40.3 /etc/services

3.4.40.4 TCP/UDP wrappers

### 3.4.50 Samba

- 3.4.50.1 Server file/printer sharing
- 3.4.50.2 Client file/printer access
- 3.4.60 Sendmail, smail, qmail
- 3.4.60.1 /etc/aliases
- 3.4.60.2 mail lists
- 3.4.60.3 mail loops
- 3.4.60.4 newaliases
- 3.4.70 Pop3, Imap
- 3.4.80 News
- 3.4.80.1 INN
- 3.4.80.2 cnews
- 3.4.90 Mail list servers
- 3.4.90.1 Listproc
- 3.4.90.2 Majordomo
- 3.4.90.3 Smartlist
- 3.4.90.4 Listserve
- 3.4.100 Apache server
- 3.4.100.1 CGI scripts
- 3.4.100.2 Modules
- 3.4.100.3 Virtual hosting
- 3.5 Applications
- 3.5.10 Mail, pine
- 3.5.20 Browsers
- 3.5.30 Netscape
- 3.5.40 Lynx
- 3.6 Troubleshooting
- 3.6.10 Ping
- 3.6.20 Netstat
- 3.6.30 Traceroute
