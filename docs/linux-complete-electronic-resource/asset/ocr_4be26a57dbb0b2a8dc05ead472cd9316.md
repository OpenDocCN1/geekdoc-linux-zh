# IP Aliasing

This feature of the Linux kernel provides the possibility of setting multiple network addresses on the same low-level network device driver (e.g. two IP addresses on one Ethernet card). This is typically used for services that act differently based on the address they listen on (e.g. “multihosting,” “virtual domains,” or “virtual hosting services”).

A related IP Aliasing HOWTO can be found at http://MetaLab.unc.edu/mdw/HOWTO/mini/IP- Alias.html.

# Traffic Shaping

The traffic shaper is a virtual network device that makes it possible to limit the rate of outgoing data flow over another network device. This is specially useful in scenarios (as ISPs) in which it is desirable to con- trol and enforce policies regarding how much bandwidth is used by each client. Another alternative (for web services only) may be certain Apache modules that restrict the number of IP connections by client or the band- width used.

# Firewall

A firewall is a device that protects a private network from the public part (the Internet as a whole). It is designed to control the flow of packets based on the source, destination, port, and packet type information con- tained in each packet.

Different firewall toolkits exist for Linux as well as built-in support in the kernel. Other firewalls are TIS and SOCKS. These firewall toolkits are very complete and combined with other tools allow blocking/redirection of all kinds of traffic and protocols. Different policies can be implemented via configuration files or GUI programs.

The TIS home page can be found at http://www.tis.com. SOCKS can be found at http://www.socks.nec.com/socksfaq.html. And the firewall HOWTO can be found at http://metahub.unc.edu/LDP/.

# Port Forwarding

An increasing number of Web sites are becoming interactive by having cgi-bin or Java applets that access some database or other service. Since this access may pose a security problem, the machine containing the database should not be directly connected to the Internet.

![](bbox=[0.9, 0.5, 0.98, 0.65])