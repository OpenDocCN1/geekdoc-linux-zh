LAN card. This section shows tools for checking the behavior of the networking protocols, primarily those in the TCP/IP protocol suite.

This section describes monitoring for the network and transport layers of the OSI seven-layer networking model. These layers include the protocols for data transmission, routing, sequencing, and flow control. In a LAN environment, error detection and recovery are the responsibility of the transport layer. A variety of key resources need to be monitored at these layers, such as the IP addresses being used by each client and server, the number of active connections to a server, and error statistics for each protocol.

# ### Using SNMP Instrumentation

The MIB-II was discussed earlier because of its ability to report status information for each network interface. The MIB-II also contains information for some key networking protocols, such as IP, ICMP (Internet Control Message Protocol), TCP, ARP, and UDP.

If you have access to a MIB Browser, then you may want to browse this MIB to see the interesting statistics that you can access. For example, for IP, you can check the amount of data being sent or discarded, and the amount being received, and get an idea of the fragmentation, reassembly, or delivery errors that are occurring. For ICMP, you can determine the number of times a destination was unreachable. For TCP, you can look at the number of connection attempts and see the current connections. For UDP, you can see the number of open sockets.

This section is brief, because very similar information is provided by the netstat command, which is discussed in detail later in this section. Unless you are monitoring the MIB variables of multiple systems through a network management product, you probably want to use the netstat command.

# ### Using Standard Commands and Tools

Common UNIX commands for obtaining network and transport protocol information are included in this section.

# **ping**

The ping command uses ICMP echo to test connectivity to a remote node and record round-trip times and routes for network packets. The percentage of packets lost is also shown. Because ICMP uses IP for its data transmission, ping not only tests the link itself, but it also tests for correct network protocol behavior. Transport protocols such as TCP and UDP are not involved in a ping. Listing 6-6 shows an example of the ping command. Note that ping can be used with an IP address or system name. If used with a name, ping can determine whether the name resolution service is working properly.

If the ICMP sequence numbers are not in numerical order, a hardware problem may be present. If no response is made to a ping, a variety of problems are possible. If other systems can be pinged, especially systems with the same route, then the remote system might have failed. If no system can be pinged, it could be a sign that the local system is not connected to the network.