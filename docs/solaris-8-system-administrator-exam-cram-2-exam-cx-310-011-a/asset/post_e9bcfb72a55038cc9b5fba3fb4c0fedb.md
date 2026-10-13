
## Features and Functions of Ethernet

The TCP/IP model’s Data Link layer controls data transfer across network media. In an Ethernet local area network (LAN), the Ethernet frame is used at the Data Link layer to package and transmit the data.

The hosts on an Ethernet LAN are assigned unique addresses that are associated with the Data Link layer. These addresses are referred to as *Ethernet addresses*, *hardware addresses*, *physical addresses*, or *MAC addresses*.

Typically, the vendor that manufactures the network interface card (NIC) assigns these addresses, and a unique address is associated with each NIC. Therefore, the Ethernet address is associated with a NIC, not with a system. A system with two NICs (such as a router attached to two networks) has two Ethernet addresses.

The Ethernet address consists of 48 bits (6 bytes of data). Typically, an Ethernet address is shown as six two-digit hexadecimal numbers separated by colons. For example, 00:40:05:37:9d:db is the Ethernet address for the system used to generate most of the code examples in this book.

The Ethernet frame transmitted on the LAN contains the Ethernet address of the NIC that should receive and respond to the frame. Any received frames with an Ethernet address matching the NIC’s Ethernet address are read and processed.

Ethernet addresses are used only on the LAN and do not pass through routers. Therefore, any Ethernet frame sent to a host not on the current LAN uses the router’s Ethernet address as its destination. Likewise, an Ethernet frame sent from a router to a host has the router’s Ethernet address as its source.

All TCP/IP applications use IP addresses. However, to communicate across the LAN, it is necessary to find a system’s Ethernet (or MAC) address, given its IP address. Because each host has a unique IP address and a unique Ethernet address, a process is needed to map between these two types of addresses.

## The Address Resolution Protocol and the Reverse ARP

The process of mapping between Ethernet and IP addresses is referred to as *address resolution*. The protocol for mapping from an IP address to an Ethernet address is called the Address Resolution Protocol (ARP). The details of this process are specified in Request for Comment (RFC) 826, “An Ethernet Address Resolution Protocol.”

In some cases, an Ethernet address is known, but the IP address needs to be determined. This process is known as the Reverse Address Resolution Protocol (RARP). The details of this process are specified in RFC 903, “A Reverse Address Resolution Protocol.”

A host that needs to resolve an Ethernet address broadcasts an ARP request containing the IP address as data. The message basically asks “What is the Ethernet address of the host with this IP address?” Note that the ARP request is an Ethernet broadcast. That is, the destination Ethernet address of the Ethernet frame is all ones (FF:FF:FF:FF:FF:FF). The host that matches the specified IP address responds with an ARP reply containing its Ethernet address.

The same process is used to resolve an IP address when the Ethernet address is known. An RARP request is broadcast (destination Ethernet address of FF:FF:FF:FF:FF:FF) that contains an Ethernet address in the data. The appropriate host responds with an RARP reply containing the requested IP address.

Sometimes it might be necessary for a system to respond to an ARP or RARP request on behalf of another system. This process is referred to as *proxy ARP*; some protocol stacks (typically on routers) are designed with this capability.

## Classes of IP Networks

In the TCP/IP network model, the IP address at the Transport layer is used to segregate networks into classes. The three most commonly used IP network classes are A, B, and C. Table 13.1 summarizes the characteristics of these IP network classes.

**Table 13.1  IP Network Classes**

| Class | First Octet | Default Subnet Mask | Maximum Theoretical Hosts |
|---|---|---|---|
| A | 1 through 126 | 255.0.0.0 | 16,777,216 |
| B | 128 through 191 | 255.255.0.0 | 65,536 |
| C | 192 through 223 | 255.255.255.0 | 256 |

Addresses with a first octet of 127 are not considered part of Class A or Class B. This octet is dedicated for a special use referred to as “loopback.” The subnet mask separates the network portion of an IP address from the host portion.

## TCP/IP Configuration Files

Solaris 8 uses several files to configure the TCP/IP environment. These files are used to identify the system’s hostname and IP address. The three files, described in the following sections, are used to configure TCP/IP:

- `/etc/inet/hosts`
- `/etc/nodename`
- `/etc/hostname.interface`

### The /etc/inet/hosts File

The /etc/hosts file (which is a symbolic link to /etc/inet/hosts) contains a listing of hostnames and their associated IP addresses. This file is used to convert hostnames to IP addresses. Table 13.2 summarizes the format of the /etc/inet/hosts file.

**Table 13.2 — /etc/inet/hosts File Format**

| Column | Description |
|---|---|
| IP Address | IP address in dotted decimal notation |
| Host Name | Hostname or node name of the system |
| Alias | Alternative hostnames for the system |

The columns are separated by one or more tab or space characters. If more than one alias is defined, you should separate them with spaces or tabs.

![](img/b957f979417d9f16274c2eb52c8f2c9f_315_0.png)

At a minimum, the /etc/inet/hosts file should contain an entry for the localhost (IP address 127.0.0.1) and an entry for each network interface installed on the system.

Entries for other systems can be added to the /etc/inet/hosts file. If a name service is not being used, doing so makes it possible to access remote systems by using hostnames instead of IP addresses.

### The /etc/nodename File

The /etc/nodename file contains only one entry: the local system’s default hostname. You should assign the hostname or node name in accordance with RFC 952, “DOD Internet Host Table Specification.”

### The /etc/hostname.interface File

One `/etc/hostname.interface` file exists for each network interface installed on the system. The *interface* portion of the filename reflects the manufacturer and type of network interface. For example, if an Intel x86-based system has a single 3COM Etherlink III NIC installed, the filename is `/etc/hostname.le0`. For a SPARC 5 platform with two network interfaces, the filenames are `/etc/hostname.le0` and `/etc/hostname.le1`.

The `/etc/hostname.interface` file(s) should contain only one entry: the hostname or the IP address assigned to that interface.

![](img/b957f979417d9f16274c2eb52c8f2c9f_316_0.png)

> If a hostname is used, it must also be listed in the `/etc/inet/hosts` file. Also note that if more than one network interface is installed on the system, the `/etc/hostname.interface` files will contain different hostnames. Only the hostname (or IP address) matching the hostname defined in the `/etc/nodename` file is considered the default hostname for the system.

## Checking Network Connectivity

Solaris 8 provides two commands for checking network connectivity between systems and the proper operation of the network interfaces on both systems: the `ping(1M)` command and the `spray(1M)` command.

### The ping Command

The `/usr/sbin/ping` command uses the Internet Control Message Protocol (ICMP) to send ECHO_REQUEST datagrams to another host. When a host receives an ECHO_REQUEST datagram, it responds with an ECHO_REPLY datagram. This basic echo mechanism is used to verify the connectivity between two hosts and the proper operation of the network interfaces and protocol stacks (of both hosts) up to the Network or Internet layer, which includes the Internet Protocol (IP). The following example sends one ICMP ECHO_REQUEST datagram by using the ping command:

```text
$ /usr/sbin/ping solaris8
solaris8 is alive
$
```

Table 13.3 lists some of the more frequently used command-line arguments supported by the **ping** command. See the **ping(1M)** manual page for more details.
