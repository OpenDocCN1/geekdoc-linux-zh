plugging in an Ethernet cable into the back of the card and then configuring Linux's networking settings. Once these settings are activated, the Linux box can then communicate to other machines.

Linux normally uses **TCP/IP** when talking to other machines, whether across the Internet or via a LAN connection. The OS can be configured to use other protocols as well, including **IPX** when communicating on Novell networks, but Linux defaults to the **TCP/IP** stack. **TCP/IP** is a method of connecting and linking software from one machine to the other. Several ingredients comprise the entire **TCP/IP** suite of protocols. These include the following protocols:

+   * **Internet Protocol (*IP*)** is the protocol that transmits raw data, stripped of any additional information, from one machine to the next.
+   * **Internet Control Message Protocol (*ICMP*)** is the low-level support function for **IP**. It transmits error messages, helps in routing packets, and echoes requests. **ICMP** is normally used with the **ping** command.
+   * **Address Resolution Protocol (*ARP*)** translates hardware addresses or **MAC** addresses to network addresses. A **MAC** address is an identification number assigned to a network card. The address helps servers recognize individual machines.
+   * **User Datagram Protocol (*UDP*)** sends data from one program to the next using **IP**. **UDP** does not verify the transmission of individual messages.
+   * **Transmission Control Protocol (*TCP*)** builds on top of **UDP** and certifies that each message has been received.

Given this basic overview of the networking principles that make up the physical and application layers of data transmission between machines, let us now look at how these individual parts of data or packets are moved back and forth among computers.

# ## Packaging Data into Packets

Linux supports a variety of physical networking methods; the most common today is that of *Ethernet*. Linux also supports *token ring*, *ARCNet*, and *modem-based* networking protocols, such as **SLIP** and **PPP**. For now, this chapter will deal with **LAN**-based network connections. One of the quickest methods of moving data between two machines is via a network interface that utilizes an