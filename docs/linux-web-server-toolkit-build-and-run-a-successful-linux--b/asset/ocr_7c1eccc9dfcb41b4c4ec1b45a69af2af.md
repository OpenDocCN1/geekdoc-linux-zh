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

All you do is to use an IP address that begins with 192.168 as the first two numbers (larger Private Internet address ranges are also available). You're probably thinking: If I'm not connected to anything, I can use any IP address I want. This is true, but there's a problem—when you connect to the Internet (assume for a moment you will), the sky will fall in on your network, because the IP addresses conflict with "real" hosts on the net. The computers that legitimately use the IP addresses you picked from thin air may crash, and the owners of those computers will call you mean names for stealing their addresses. The 192.168 addresses that are reserved for internal use won't be routed by any system on the