
## Red Hat Linux and Networking

Red Hat Linux 9 comes bundled with lots of networking applications and utilities that will help you meet your networking requirements. We can categorize and list the networking applications that come with Red Hat Linux 9 as follows:

| Application Type | Applications |
|---|---|
| Web server | httpd – the widely used Apache HTTP server |
| FTP server | vsftpd – a very secure ftp server |
| File server | samba – the SAMBA server, which provides file sharing between SMB-enabled machines (such as Windows and Linux machines) |
| | samba-client – the SAMBA client programs, designed to access SMB shares |
| Print server | cups – CUPS printing service and the drivers to use it |
| Mail server | sendmail – a widely used mail transport agent |
| DHCP server | dhcp – a DHCP server and relay agent |

Over the course of this chapter, we will discuss some of these applications and help you to get your Linux machine acting as a full-fledged network server.

### Why Is Linux Good for Networking?

One of the most significant factors in choosing the hardware and software for a network is the **total cost of ownership** (TCO). This is the cost of purchase, setup and configuration, and also maintenance. If you sit down and analyze the requirements of different parts of network architecture, you’ll quickly find that the free, open nature of Linux systems lends itself better to some parts of network than others.

Linux is a particularly good choice for supporting network applications (such as file servers, web servers, and mail servers):

- Of course, the cost of purchase (both of the operating system and the software itself) is low. Cost of setup should generally also be favorable, particularly given the advances both in recent releases of network applications and in Red Hat Linux 9 itself, and the vast body of knowledge in the open source community that is available via web sites, news groups and local Linux users’ groups. (Many enterprise level solutions companies like Red Hat, IBM, Hewlett Packard, and Sun Microsystems have also started providing commercial level support for Linux servers.)
- The stability and reliability of the operating system is also influential, because an unstable or unreliable system brings maintenance costs. Linux is a good choice for network applications because it makes the grade in these areas. Moreover, Linux is ready for high-availability environments (see http://www.ibiiblio.org/pub/Linux/ALPHA/linux-ha).
- Other factors influencing TCO include the scalability, flexibility, and security of the system:
  - By choosing a Linux operating system and open source networking applications, you have access to the source code of both the system and the application. This puts you in a position to adapt the applications to achieve whatever aims you need.
  - We've already seen evidence, earlier in this chapter, that Linux is capable of being deployed in both small- and large-scale networks.
  - Red Hat Linux installs by default with a minimum of good-practice security, and (as we'll see in Chapter 12) be further enhanced with a combination of open source security tools and good practice.

Linux is also great for services that can be replicated (for example, DNS). You can configure such machines cheaply, and replicate them. Then, if one machine fails, it doesn't matter; it should be possible to replace it cheaply. In the meantime, the replicate servers keep on working to provide the service.

By contrast, Linux is not a common choice for basic infrastructure, such as routers, hubs, and switches. While Linux is capable in this area, it's desirable only when the low cost of cheap (or cast off) PCs is the major selection criteria. In a more business critical role, where reliability will count for more than minimum purchase price, dedicated hardware is still the most popular choice.

You can find more information about TCO comparison between Red Hat Linux and other Unix flavors at http://www.redhat.com/whitepapers/services/tco.pdf.

## Assumptions for Network Setup

In the demonstrations in this chapter, we've used a network setup that may not be the same as your own environment. You can choose your own server, connectivity devices (switch, hub, and direct cable connection), IP address scheme, and hostname to set up networking in a way that suits your own requirements. In this section, we'll note the network settings that we've used. In order to facilitate, we'll begin with an explanation of the terms that we'll use.

The network topology refers to the shape or layout of the network. It defines how different systems in a network are connected and communicate with each other. The ideal topology of a network depends on the size of the network, the requirements of its users, and the policies of the company or organization.

The following diagram shows an ideal network topology:

![](img/b852150740856958b10aff9e8c9d2adc_344_0.png)

This diagram shows a client machine (in the form of a Windows 2000 laptop), and a server (running Red Hat Linux 9, and supporting some of the services described in this chapter. They are connected via an internal network, and protected from the Internet by a hub and a firewall. Of course, your network topology might look different than this.

For example, if you have a smaller network, then it’s possible that you don’t have a hub, and that your firewall is not a dedicated machine but a piece of software hosted by your Linux server machine. If you have only a single machine, then it can double as both the server and client machines in this diagram (being a client of its own services!). We’ve used a topology like this one in this chapter.

Note that both the end-user’s laptop and the server machine have been assigned an **IP address** – this is used to uniquely identify the computer (or other device) within a TCP/IP network. An IP address is a 32-bit binary address in the form of four decimal values. Each of these four decimals represents an 8-bit value (an octet), and hence is in the range 0 to 255. This format is known as **dotted quad notation**.

In fact, the TCP/IP network is divided into different class networks. The important classes are defined below:

| Class | Values | Description |
|---|---|---|
| Class A | 1.x.x.x to 127.x.x.x | The first octet specifies the network number, and the remaining octets specify the host within the network. This class supports about 1.6 million hosts per network. |
| Class B | 128.0.x.x to 191.255.x.x | The first two octets specify the network number, and the remaining octets specify the host within the network. This class supports 16,320 networks with 65,024 hosts each. |
| Class C | 192.0.0.x to 223.255.255.x | The first three octets specify the network number, and the remaining octets specify the host within the network. This class supports nearly two million networks with up to 254 hosts each. |
| Class D | 224.0.0.0 to 239.255.255.255 | These are reserved for multicast groups |
| Class E | 240.0.0.0 to 254.255.255.254 | These are reserved for special purpose use. |

The TCP/IP networks can also be divided by public and private IP addresses:

- Your public IP address is assigned to you by your Internet service provider (ISP). In fact, this IP address is allocated to the ISP by the Internet Assigned Numbers Authority (IANA – http://www.iana.org). It’s your public IP address that identifies you on the Internet.
- Private IP addresses are those (like the addresses used in the diagram above) that identify a device within a private or non-Internet connected network. There are three TCP/IP network address ranges reserved for use in private networks: 10.0.0.0–10.255.255.255, 172.16.0.0–172.31.255.255, and 192.168.0.0–192.168.255.255.

A **netmask** is a 32-bit string that hides the network part of an IP address, so that only the host (computer) part of the address remains. For example, the netmask 255.255.255.0 looks like an IP address, but in fact hides the first 24 bits of the IP address so that only the last 8 bits remain (recall that 255 is the decimal representation of the binary 11111111). Hence, the netmask 255.255.255.0 is commonly used for Class C IP addresses to reveal the specific host computer address publicly.
