# ### The Coming of IPv6

Another alternative protocol stack is actually an extension of TCP/IP. The IP portion of TCP/IP has been at version 4 for many years. A major upgrade to this is underway, however, and it goes by the name IPv6, for IP version 6. IPv6 adds several features and improvements to TCP/IP, including standard support for more secure connections and support for many more addresses. Check http://playground.sun.com/ipv6/html/ ipng-main.html or http://www.ipv6forum.com for detailed information about IPv6.

TCP/IP supports a theoretical maximum of about 4 billion addresses. Although this may sound like plenty, those addresses have not been allocated as efficiently as possible. Therefore, as the Internet has expanded, the number of truly available addresses has been shrinking at a rapid rate. IPv6 raises the number of addresses to 2$^{128}$, or 3.4 × 10$^{38}$. This is enough to give every square millimeter of land surface on Earth 2.2 × 10$^{8}$ addresses.

IPv6 is starting to emerge as a real networking force in many parts of the world. The United States, though, is lagging behind on IPv6 deployment. The Linux kernel includes IPv6 support, and most distributions now attempt to automatically configure IPv6 networking in addition to IPv4. Chances are that by the time the average office will need IPv6, it will be standard. Configuring a system for IPv6 is somewhat different from configuring it for IPv4, which is what this chapter emphasizes.

# ## Using Network Addresses

Consider an Ethernet network. When an Ethernet frame leaves one computer, it's normally addressed to another Ethernet card. This addressing is done using low-level Ethernet features, independent of the protocol stack in question. Recall, however, that the Internet is composed of many different networks that use many different low-level hardware components. A user may have a dial-up telephone connection (through a serial port) but connect to one server that uses Ethernet and another that uses Token Ring. Each of these devices uses a different type of low-level network address. TCP/IP requires something more to integrate across different types of network hardware. In total, three types of addresses are important when you're trying to understand network addressing: network hardware addresses, numeric IP addresses, and text-based hostnames.

# ### Addressing Hardware

One of the characteristics of dedicated network hardware such as Ethernet or Token Ring cards is that they have unique *hardware addresses*, also known as *Media Access Control (MAC) addresses*, programmed into them. In the case of Ethernet, these addresses are 6 bytes in length, and they're generally expressed as hexadecimal (base 16) numbers separated by