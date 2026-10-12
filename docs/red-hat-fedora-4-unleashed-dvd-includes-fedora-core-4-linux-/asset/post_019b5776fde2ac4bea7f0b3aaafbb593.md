
The first octet usually determines what class the network belongs to. There are three classes of networks. The classes are

- **Class A**—Consists of networks with the first octet ranging from 1 to 126. There are only 126 Class A networks—each composed of up to 16,777,214 hosts. (If you are doing the math, there are potentially 16,777,216 addresses, but no host portion of an address can be all zeros or 255s.) The “10.” network is reserved for local network use, and the “127.” network is reserved for the loopback address of 127.0.0.1. Loopback addressing is used by TCP/IP to enable Linux network-related client and server programs to communicate on the same host. This address will not appear and is not accessible on your LAN.
- **Class B**—Consists of networks defined by the first two octets with the first ranging from 128 to 191. The “128.” network is also reserved for local network use. There are 16,382 Class B networks—each with 65,534 possible hosts.
- **Class C**—Consists of a network defined by the first three octets with the first ranging from 192 to 223. The “192.” network is another that is reserved for local network use. There are a possible 2,097,150 Class C networks of up to 254 hosts each.

> **NOTE**
>
> Notice that zero is not included in Class A. The zero address is used for network-to-network broadcasts. Also, note that there are two other classes of networks, Classes D and E. Class D networks are reserved for multicast addresses and not for use by network hosts. Class E addresses are deemed experimental, and thus are not open for public addressing.

No host portion of an IP address can be all zeros or 255s. These addresses are reserved for broadcast addresses. IP addresses with all zeros in the host portion are reserved for network-to-network broadcast addresses. IP addresses with all 255s in the host portion are reserved for local network broadcasts. Broadcast messages are not typically seen by users.

These classes are the standard, but a netmask also determines what class your network is in. The netmask determines what part of an IP address represents the network and what part represents the host. Common netmasks for the different classes are:

- Class A—255.0.0.0
- Class B—255.255.0.0
- Class C—255.255.255.0

Because of the allocation of IP addresses for Internet hosts, it is now impossible to get a Class A network. It is also nearly impossible to get a Class B network (all the addresses have been given out, but some companies are said to be willing to sell theirs), and Class C network availability is dropping rapidly with the current growth of Internet use worldwide. See the following sidebar.

## Limits of Current IP Addressing

The current IPv4 address scheme is based on 32-bit numbering and limits the number of available IP addresses to about 4.1 billion. Many companies and organizations (particularly in the United States) were assigned very large blocks of IP addresses in the early stages of the growth of the Internet, which has left a shortage of “open” addresses. Even with careful allocation of Internet-connected host IP addresses and the use of *network address translation* (NAT) to provide communication to and from machines behind an Internet-connected computer, the Internet might run out of available addresses.

To solve this problem, a newer scheme named IPv6 (IP version 6) is being implemented. It uses a much larger addressing solution based on 128-bit addresses, with enough room to include much more information about a specific host or device, such as Global Positioning Server (GPS) or serial numbering. Although the specific details about the entire contents of an IPv6 address have yet to be finalized, all Internet-related organizations appear to agree that something must be done to provide more addresses. According to Vint Cerf, one of the primary developers of the TCP/IP protocol, “There will be nearly 2.5 billion devices on the Internet by 2006, and by 2010 half the world’s population will have access to the Internet.”

You can get a good overview of the differences between IPv4 and IPv6, policies regarding IP address assignments, and the registration process of obtaining IP addresses by browsing to http://www.arin.net/library/index.html. Read the Linux IPv6 HOWTO by browsing to http://tldp.org/HOWTO/Linux+IPv6-HOWTO/.

Fedora supports the use of IPv6 and includes a number of networking tools conforming to IPv6 addressing. Support for IPv6 can be configured by using settings and options in the file named *network* under the `/etc/sysconfig` directory, along with changes to related network configuration files, such as `/etc/hosts`. Many IPv6-based tools, such as *ipcalc6*, *ping6*, and *traceroute6*, are available for Fedora. See various files under the `/usr/share/doc/initscripts` directory for more information specific to setting up IPv6 addressing with Linux and Fedora.

Migration to IPv6 is slow in coming, however, because the majority of computer operating systems, software, hardware, firmware, and users are still in the IPv4 mindset. Supporting IPv6 will require rewrites to many networking utilities, portions of operating systems currently in use, and firmware in routing and firewall hardware.

### Using IP Masquerading in Fedora

Three blocks of IP addresses are reserved for use on internal networks and hosts not directly connected to the Internet. The address ranges are from `10.0.0.0` to `10.255.255.255`, or 1 Class A network; from `172.16.0.0` to `172.31.255.255`, or 16 Class B networks; and from `192.168.0.0` to `192.168.255.255`, or 256 Class C networks. Use these IP addresses when building a LAN for your business or home. Which class you choose can depend on the number of hosts on your network.

Internet access for your internal network can be provided by a PC running Fedora or other broadband or dial-up router. The host or device is connected to the Internet and is used as an Internet gateway to forward information to and from your LAN. The host should also be used as a *firewall* to protect your network from malicious data and users while functioning as an Internet gateway. A PC used in this fashion will typically have at least two network interfaces. One is connected to the Internet, with the other connected to the computers on the LAN (via a hub or switch). Some broadband devices also incorporate four or more switching network interfaces. Data is then passed between the LAN and the Internet using NAT, better known in Linux circles as IP Masquerading. See Chapter 33, “Securing Your Machines,” for more information.

> **NOTE**
>
> Do not rely on a single point of protection for your LAN, especially if you use wireless networking, provide dial-in services, or allow mobile (laptop or PDA) users internal or external access to your network. Companies, institutions, and individuals relying on a “moat mentality” have often discovered to their dismay that such an approach to security is easily breached. Make sure that your network operation is accompanied by a security policy that stresses multiple levels of secure access, with protection built into every server and workstation—something easily accomplished when using Linux.

## Ports

Most servers on your network have more than one task. For example, web servers have to serve both standard and secure pages. You might also be running an FTP server on the same host. For this reason, applications are provided ports to use to make “direct” connections for specific software services. These ports help TCP/IP distinguish services so that data can get to the correct application. If you check the file `/etc/services`, you will see the common ports and their usage. For example, for FTP, HTTP, and Post Office Protocol (email retrieval server), you will see:

```
ftp     21/tcp
http    80/tcp     www www-http    # WorldWideWeb HTTP
pop3    110/tcp    pop-3           # POP version 3
```

The ports defined in `/etc/services` in this example are 21 for FTP, 80 for HTTP, and 110 for POP3. Other common port assignments are 25 for Simple Mail Transport Protocol (SMTP) and 22 for secure shell (SSH) remote login. Note that these ports are not set in stone, and you can set up your server to respond to different ports. For example, although port 22 is listed in `/etc/services` as a common default for SSH, the `sshd` server can be configured to listen on a different port by editing its configuration file `/etc/ssh/sshd_config`. The default setting (commented out with a pound sign) looks like this:

```
#Port 22
```

Edit the entry to use a different port, making sure to select an unused port number, such as Port 2224.

Save your changes, and then restart the `sshd` server. (Refer to Chapter 14, “Automating Tasks,” to see how to restart a service.) Remote users must now access the host through port 2224, which can be done using `ssh`’s `-p` (port) option like so:

```
$ ssh -p 2224 remote_host_name_or_IP
```
