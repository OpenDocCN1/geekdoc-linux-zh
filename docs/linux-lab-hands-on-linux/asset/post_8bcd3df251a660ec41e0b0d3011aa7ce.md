
## NOTES

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

### 15 LAB: Dynamic Host Configuration Protocol Server

**OBJECTIVES**

1. To install and configure DHCP server
2. Assignment of fixed IP addresses to Servers
3. Configure client for DHCP

**REQUIREMENTS**

P-IV class PC, with installed Fedora/RHEL, with NIC, Linux distribution CD/DVD etc.

**CONCEPT**

Each computer in the TCP/IP network must have IP address, subnetmask, IP address of gateway and, IP address of a DNS server. The DHCP server is used to send these basic configurations automatically to the computers in the network.

DHCP is a client-server protocol. The DHCP server assigns two types of address leases, manual and dynamic. In manual lease, the DHCP server explicitly assigns an IP address manually by associating a client hardware address with specific IP address. Whereas in dynamic lease, DHCP assigns any available IP address to the client from range of IP address mentioned in a configuration file.

#### Configuration Files

The server side configuration files are as follows:

- /etc/dhcpd.conf: Main configuration file of DHCP server.
- /var/lib/dhcp/dhcpd.leases: Stores the leased clients IP addresses details
- /usr/share/doc/dhcp-version//dhcpd.conf.sample: Sample DHCP configuration file
- Client Side:
- /etc/sysconfig/network-scripts/ifcfg-eth0: change to DHCP

#### Steps to Install and configure DHCP Server:

1. Install the DHCP package by using the following command:

```
[root@netmon tmp]$ rpm -ivh dhcp-3.0.1-1.i386.rpm
```

2. Copy sample file by using the following command:

```
[root@netmon tmp]# cp /usr/share/doc/dhcp-3.0pl1/dhcpd.conf.sample /etc/dhcpd.conf
```

3. Edit the dhcpd.conf file by using the following command:

```
### This is sample dhcp configuration file: ddns-update-style interim ignore client-updates subnet 192.168.1.0 netmask 255.255.255.0 { # The range of IP addreses the server # will issue to DHCP enabled PC clients # booting up on the network range 192.168.1.201 192.168.1.220; # Set the amount of time in seconds that a client may keep the IP address default-lease-time 86400;max-lease-time 86400; # Set the default gateway to be used by # the PC clients option routers 192.168.1.1; # Don't forward DHCP requests from this # NIC interface to any other NIC # interfaces option ip-forwarding off; # Set the broadcast address and subnet mask # to be used by the DHCP clients option broadcast-address 192.168.1.255; option subnet-mask 255.255.255.0; # Set the DNS server to be used by the # DHCP clients option domain-name-servers 192.168.1.100; # Set the NTP server to be used by the # DHCP clients option ntp-server 192.168.1.100; # If you specify a WINS server for your windows clients, # you need to include the following option in the dhcpd.conf file: option netbios-name-servers 192.168.1.100; # You can also assign specific IP addresses based on the clients' # ethernet MAC address as follows (Host's name is "laser-printer"): host laser-printer { hardware ethernet 08:00:2b:4c:59:23; fixed-address 192.168.1.222; } #List an unused interface here subnet 192.168.2.0 netmask 255.255.255.0 { }
```

![](img/f3b9cff79e19317416c12eaf5ded7245_163_0.png)

*Suggested modification in above dhcpd.conf file are as follows:*

1. Change the subnet IP address as per your network subnet id
   `subnet 172.16.0.0 netmask 255.255.0.0 {`
2. Specify range of IP addresses that you want to assign to a client of the network.
   `range 172.16.0.1 172.16.0.100;`
3. Specify default gateway to be used by the client:
   `option routers 172.16.1.1;`
4. Specify DNS server IP address
   `option domain-name-servers 192.168.1.100;`
5. Start DHCP server by using the following commands:

```
[root@netmon tmp]# touch /var/lib/dhcpd/dhcpd.leases
[root@netmon tmp]# chkconfig --level 345 dhcpd on
[root@netmon tmp]# service dhcpd start
[root@netmon tmp]# service dhcpd stop
[root@netmon tmp]# service dhcpd restart
```

6. Test the DHCP server:
   You can also test whether the DHCP process is running with the following command; you should get a response of plain old process ID numbers:

```
[root@netmon tmp]# pgrep dhcpd
```

#### Setup LINUX CLIENTS TO USE DHCP

You can configure a Linux NIC interface to obtain its IP address by using DHCP.

```
[root@netmon tmp]# nano /etc/sysconfig/network-scripts/ifcfg-eth0
Change to                    BOOTPROTO=dhcp
[root@netmon tmp]# service network restart
```

Figure 1 is showing the Linux client for DHCP.

![](img/f3b9cff79e19317416c12eaf5ded7245_164_0.png)

#### Setup Windows Clients To Use DHCP

Let's perform the following steps to setup windows clients:

1. Go to →Network/Neighbourhood→Right Click→Properties→TCP/IP.
2. Select Obtain an IP address automatically radio button to obtain IP address automatically. Figure 2 is showing Windows client configuration dialog box to use the DHCP server.

![](img/f3b9cff79e19317416c12eaf5ded7245_165_0.png)

Let's summarize key points learned in this Lab.

### Summary

In this lab, you have learned to install and configure DHCP server. You also learned to configure client for DHCP.

## NOTES

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

...

### 16 LAB: Network File System Protocol (NFS)

**OBJECTIVES** To install and configure NFS protocol server and client.

**REQUIREMENTS** P-IV class PC with Fedora/RHEL and Linux distribution CD/DVD.

**CONCEPT** NFS is a distributed filesystem. An NFS server has one or more files systems that are mounted by NFS clients. NFS file systems are mounted using the standard UNIX mount command. All Unix utilities work just as well with NFS-mounted files as they do with files on local disks.
NFS stands for Network File System and it is the standard method to share files between the Linux and Unix-like systems. The systems administrator has to define the directories that need to be activated or exported for access by the NFS clients on the NFS server. In addition, it defines both the NFS server and the subset of its exported directories on the clients.

#### Important NFS Daemons

The NFS server requires the following specific daemons and utilities:

- portmap: Refers to the primary daemon on which all the others rely. It manages connections for applications that use the RPC specification. By default, portmap listens to TCP port 111 on which an initial connection is made. This is then used to negotiate a range of TCP ports, usually above port 1024, to be used for subsequent data transfers. You need to run portmap on both the NFS server and client.
- nfs: Starts the RPC processes needed to serve shared NFS file systems. The nfs daemon is run on the NFS server only.
- nfslock: Allows the NFS clients to lock files on the server via RPC processes. The nfslock daemon needs to be run on both the NFS server and client.
- netfs: Allows RPC processes run on NFS clients to mount NFS file systems. The netfs daemon is run on the NFS client only.

#### Steps to Install and Configure NFS Server/Client

Perform the following NFS steps to install and configure NFS server/client:

1. Installing nfs

Red Hat Linux installs nfs by default and it also gets activated by default when the system boots. Run the following commands to check whether the nfs related packages are installed or not.
