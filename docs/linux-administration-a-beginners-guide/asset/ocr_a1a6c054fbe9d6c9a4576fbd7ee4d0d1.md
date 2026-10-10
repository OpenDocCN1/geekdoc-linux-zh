Knowing how to configure your network services by hand can be terribly important for multiple reasons. First and foremost is that when things are breaking and you can’t start your favorite GUI, being able to handle network configuration from the command line is crucial. Another reason is remote administration: you may not be able to run a graphical configuration tool from a remote site. Issues such as firewalls and network latency will probably restrict your remote administration to command line only. Finally, it’s always nice to be able to perform network configuration through scripts, and command-line tools are best suited for scriptability.

In this chapter, we will tackle the two tools necessary for performing command-line administration of your network interface: 1conf ig and route.

# ## NETWORKING 101

In this section, we go over some of TCP/IP’s fundamentals, which should be enough for you to understand the nature of IP addresses, broadcasts, and routing. If you are looking for more depth, take a look at texts dedicated to networking. Two particularly good books are TCP/IP Network Administration by Craig Hunt (O’Reilly & Associates) and TCP/IP Illustrated, volume 1, by Richard Stevens (Addison-Wesley).

> **NOTE:** This section assumes that you are already somewhat familiar with an IP address. The focus of this chapter is to explain in more detail the nature of IP and its properties. If you need some more basic information first, take a look at TCP/IP for Dummies by Marshall Wilesky and Candace Laden (IDG Books), which assumes nothing and builds up to a more technical level over several chapters rather than several pages.

# ## IP Addresses

The Internet is a large group of interconnected networks. All of these networks have agreed to connect with some other network, thus allowing everyone to connect to one another. Each of these component networks are assigned a network address.

Traditionally, in a 32-bit IP address, the network component typically takes up either 8, 16, or 24 bits to encode a class A, B, or C network, respectively. Since the remainder of the bits in the IP address are used to enumerate the host within the network, the fewer bits that are used to describe the network, the more bits that are available to enumerate the hosts. Class A networks, for example, have 24 bits left for the host component, which means there can be upwards of 16,777,214 hosts within that network. (Classes B and C have 65,534 and 254 nodes, respectively.)

To better organize the various classes of networks, it was decided early in IP’s life that the first few bits would decide which class the address belonged to. For the sake of readability, the first octet of the IP address specifies the class.