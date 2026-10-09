When you run this program a few times, you may notice that the path seems to change a lot. This is normal and not a bug. Refer to Chapter 2, "TCP/IP Network Language Fluency," for an explanation of the network's dynamics.

# **Summary: Making the Raw Decisions**

The raw socket gives you the capability of working with the error messaging protocols (ICMP) that the IP subsystem uses. It also allows you to create your own protocols. The primary advantage of raw sockets is its sheer speed, being only one abstraction layer above the physical network frame.

The most common introductory raw socket programs are ping and traceroute. When you understand how these work and the risks involved in datagram messaging, you can choose the best approach to meet the requirements of your program.

# Chapter 19. IPv6: The Next Generation to IP

# IN THIS CHAPTER

+   - Current Addressing Problems
- Trying Out IPv6
- IPv6 Pros and Cons
- Summary: Moving Your Code into the Future

The Internet contains much of the network traffic in today's world. It has a great deal of power and flexibility. It bases its power and flexibility on the IP packet. This packet eases getting messages from here to there. However it has certain limitations, limitations based primarily on growth and extensibility.

This chapter digs deeply into the next generation of IP: IPng (yes, "IP Next Generation") or IPv6. Throughout this book, you have worked entirely in the IPv4 arena, and most of that knowledge is applicable in IPv6. You only need to know few extra tips and tricks to ensure longevity in your creative projects.

# Current Addressing Problems

The IPv4 primarily focuses on addressing a set of computers within a subnet. As described in Chapter 2, "TCP/IP Network Language Fluency," the number is composed of 4-byte values (or a 32-bit number). Furthermore, the addresses are grouped into network classes. When companies buy blocks of addresses, they get them in these classes. These classes range from a few hundred to a few million addresses.

The number of addresses being assigned and used has alarmed the Internet Activities Board (IAB). The board has discovered that less than 1% of the numbers assigned are really associated with a node on the network. The result: a dwindling supply of available addresses.

The IAB expects the number of computers connected to the Internet to increase as much as a hundredfold within the next few years. IPv4 simply does not have enough available addresses to meet the demand.