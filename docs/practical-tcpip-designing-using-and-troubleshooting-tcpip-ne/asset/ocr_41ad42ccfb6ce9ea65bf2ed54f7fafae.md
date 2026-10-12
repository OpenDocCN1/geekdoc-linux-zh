# **2.3 Ethernet networking: moving packets along the local wire**

TCP/IP is a software standard – it defines what a piece of networking software in one machine must do to communicate successfully with the networking software in another. To work, TCP/IP has to use some underlying network-hardware system. Ethernet is by far the most common system nowadays for LANs so that’s what we deal with in the rest of this chapter. Note that Ethernet is *not* part of TCP/IP.

+   - lots of network software that isn’t TCP/IP uses Ethernet
+   - TCP/IP runs over many different types of hardware that are not Ethernet, e.g. token ring, dial-up phone lines, packet radio, etc.

TCP/IP just interacts with Ethernet (which is the network access layer) to use its capabilities to move the packets along the physical wire.

Ethernet defines the standard for electrical interface, cable types, connector configurations, etc. and how the hardware sends an Ethernet packet from one machine to another on the same wire or Ethernet *segment*. TCP/IP knows nothing about these lower-level details of cabling, Ethernet transmission, and so on – it’s not its business.

# **Ethernet addressing**

+   - Ethernet uses Ethernet addresses, also called *MAC* addresses (*Media Access Control* or *Medium Access Control*) or hardware addresses
+   - Ethernet addresses consist of six bytes, written in hexadecimal. On Linux, these are shown in uppercase, separated by colons, e.g.
+   		00:D0:B7:B6:3D:F6
+   
+   	On Windows they are shown in lowercase, separated by dashes, e.g.
+   
+   		00-d0-b7-b6-3d-f6
+   
+   - Ethernet addresses are globally unique, and are allocated by the Institute of Electrical and Electronic Engineers (IEEE) in the USA. Ethernet hardware manufacturers purchase fixed-size blocks of numbers; if they need more addresses, they buy more blocks. The IEEE publishes a list of allocated blocks, so from an Ethernet address of a device, you can tell who manufactured it (or at least the Ethernet card in it). For example,
+   
+   		00:50:73:38:CE:26 is a Cisco address
+   		08:00:20:0A:74:AA is a Sun Microsystems address
+   		
+   	(A tool on our Web site lets you enter an address and gives you the name of the owner of that Ethernet address block.)

# **Sending data over Ethernet**

For my machine to send some data to yours, on the same local Ethernet, the software in my machine first constructs an Ethernet packet in memory. It:

+   - inserts the data to be sent in the data (“payload”) area of the packet