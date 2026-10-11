You can configure many different network protocols in Linux, including but not limited to the following list:

+   * TCP/IP (Transmission Control Protocol/Internet Protocol)
+   * UDP/IP (User Datagram Protocol/Internet Protocol)
+   * IPX/SPX (Internetwork Packet Exchange/Sequenced Packet Exchange)
+   * AppleTalk
+   * DLC (Data Link Control)
+   * DECnet (Digital Equipment Corporation network)

![](bbox=[0.15, 0.17, 0.19, 0.21])

# **NOTE**

The most common LAN protocol used today is TCP/IP. It is the standard protocol used to transmit information across the Internet and the one discussed in this chapter.

When transmitting information across a WAN, you might also use a WAN protocol in addition to a specific LAN protocol to format packets for safer transmission. The two most common WAN protocols are Serial Line Internet Protocol (SLIP) and Point-to-Point Protocol (PPP).

Although many media access methods are available, the most common one used to send TCP/IP packets onto network media is called **Ethernet**. It ensures that any TCP/IP packets are retransmitted onto the network if a network error occurs. Another popular media access method is called **Token Ring**, which gives the computer that has a special token the ability to transmit information on a network; the token is passed from computer to computer to allow multiple computers to communicate. The media access method is usually contained within the hardware on the NIC or modem.

# ## The TCP/IP Protocol

To participate on a TCP/IP network, your computer must have a valid **Internet Protocol (IP) address** and **subnet mask**. Optionally, you can configure a **default gateway** to participate on larger networks such as the Internet.

# ### IP Addresses

An IP address is a unique number assigned to the computer that identifies itself on the network, similar to a unique postal address that identifies your location in the world. If any two computers have the same IP address, it is impossible for information to be correctly delivered to them. Directed communication from one computer to another single computer using TCP/IP is referred to as a **unicast**.