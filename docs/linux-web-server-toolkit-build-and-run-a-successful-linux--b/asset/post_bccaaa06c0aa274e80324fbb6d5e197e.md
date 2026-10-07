
# Linux Web Server Toolkit

- Network address: This is the address of the local network of which the computer is a part. It will be similar to the IP address for the system you are installing, but the last or two numbers of the four will be different, depending on the class of network that you are part of. It is often the same as the IP address of the system with 0 as the last number.

- Netmask: This used by the routers on your network to separate the address of the network from the address of a single computer in order to determine how to route network traffic. It often has several 255 numbers.

- Broadcast address: This is the address used to send a message to everyone on your network. It is like a regular host address, but is reserved for the special purpose.

- Gateway: This is the machine that routes network traffic to the Internet or to other networks at your site. It is often the same address as the IP address of the machine you are installing on, except the number is 1 or 254.

- Name server's IP address: This is the IP address of the computer that provides DNS services to the machine you are installing. (Remember, DNS enables your computer to translate from names, such as www.rb.com, or IP numbers, such as 197.23.45.1) This IP address may refer to a computer at your ISP if you are not providing DNS services locally; it may point to a computer on your local network; or it may be the same as the IP address of the machine you are installing if you intend to have DNS on the Web server (which is uncommon—this is covered in more detail in Chapter 7).

- Network's domain name: This is the name of the network as it is known to Domain Name Services. Examples are things like example.com or byu.edu. The domain name forms parts of the fully qualified name (FQDN) of the computer you are installing Linux on.

- Hostname: This is the name of the computer on which you are installing Linux. It is used with the domain name to make the FQDN of the new system. You, or more likely your network administrator, can choose anything you want for the hostname. Just remember that it will be broadcast around the network. It's common to use a theme in an organization for most hostnames. Names of cities, authors, sports, mountains, lakes, adjectives... you get the idea. Just don't use special characters (like a tilde: ~), don't make the name too long (under ten characters is best), and don't pick one you regret later: it's best not to change the hostname after installation is complete.

# Chapter 5: Installing Linux

Table 5-2 provides an example of the information you'll need during network installation.

# Table 5-2 Examples of the Networking Information Needed for Installation

| Item needed | Example |
| --- | --- |
| IP address | 192.12.45.22 |
| Network address | 192.12.45.0 |
| Broadcast address | 192.12.45.128 |
| Netmask | 255.255.255.0 |
| Gateway address | 192.12.45.254 |
| Name server address | 192.12.45.1 |
| Domain name | travelbuddies.com |
| Hostname | rome |

Your network interface needs a lot of numbers. But as you can see from the examples in Table 5-2, the numbers are all similar, and they should be easy to obtain from your network administrator. The next section covers the network addresses relative to intranet Web servers, which are internal information sources for individual organizations.

# WORD ABOUT INTRANETS

Information for the masses isn't the only reason to have a Web server. If you're creating a Web server for internal use only, commonly referred to as an intranet, there's a special feature of IP addressing that might be useful to you.

Networks without an Internet connection can use a special IP address that is reserved for internal use in organizations. You can treat this IP address as if you have a complete Class C IP address all to yourself. (A Class C address provides address space for 255 nodes.)

All you do is to use an IP address that begins with 192.168 as the first two numbers (larger Private Internet address ranges are also available). You're probably thinking: If I'm not connected to anything, I can use any IP address I want. This is true, but there's a problem—when you connect to the Internet (assume for a moment you will), the sky will fall in on your network, because the IP addresses conflict with "real" hosts on the net. The computers that legitimately use the IP addresses you picked from thin air may crash, and the owners of those computers will call you mean names for stealing their addresses. The 192.168 addresses that are reserved for internal use won't be routed by any system on the Linux at large, so if you eventually connect to the Internet, you're safe until you switch to giving hosts valid Internetwide IP addresses.

With a clear understanding of your hardware and how it will be used by the Linux operating system, you can begin to prepare a place to install Linux. The next section describes how to prepare your hard disk with a separate partition in which you will install Linux.

## Preparing Your Hard Disk

Linux uses a filesystem format that is different from DOS and Windows (of any version). Because of this, it requires a separate partition on your hard disk. This section describes how to prepare your hard disk with a separate partition in which you will install Linux.

## Getting to Know Your Hard Disk

A partition is like a slice of hard disk. Each partition has a type assigned to it. When your computer boots, instructions in the Master Boot Record are read and executed. One of the partitions on the hard disk is marked as active. These instructions generally start the operating system.

One of the popular boot loader (and the one included with Linux) is called LIL, for Linux Loader. I'll say more about it later.
