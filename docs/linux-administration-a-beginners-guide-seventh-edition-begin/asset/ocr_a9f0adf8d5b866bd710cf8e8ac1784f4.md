# 406 Linux Administration: A Beginner's Guide

In Chapter 14, you learned that exploit vectors are of two types: those in which the vulnerability is exploitable locally and in which the vulnerability is exploitable over a network. The latter case is covered in this chapter.
Network security addresses the problem of attackers sending malicious network traffic to your system with the intent of making your system unavailable (denial-of-service, or DoS) or exploiting weaknesses in your system to gain access or control of the system or others. Network security is not a substitute for the good local security practices discussed in the previous chapter. Both local and network security approaches are necessary to keep things working in the expected manner.
This chapter covers four aspects of network security: tracking services, monitoring network services, handling attacks, and tools for testing. These sections should be used in conjunction with the information in Chapters 13 and 14.

# TCP/IP and Network Security

The following discussion assumes you have experience configuring a system for use on TCP/IP network. Because the focus here is network security and not an introduction to networking, this section discusses only those parts of TCP/IP affecting your system's security. If you're curious about TCP/IP's internal workings, read Chapter 11.

# The Importance of Port Numbers

Every host on an IP-based network has at least one IP address. In addition, every Linux-based host has many individual processes running. Each process has the potential to be a network client, a network server, or both. With more than one process able to act as a server on a single system, using an IP address to identify a network connection is not enough.

To solve this, TCP/IP adds a component identifying TCP Datagram Protocol (UDP) port. Every connection from one host to another has a source and destination port. Each port is labeled with an integer between 0 and 65533.
To identify every unique connection possible between two hosts, the operating system keeps track of four pieces of information: the source IP address, the destination IP address, the source port, and the destination port number. The combination of these four values is guaranteed to be unique for all-to-host connections. (Actually, the operating system tracks a myriad of connection information, but only these elements are needed for identifying a connection.)

The host initiating a connection specifies the destination IP address and port number. Otherwise, the source IP address is already known. But the source port number, the value that will make the connection unique, is assigned by the source operating system. It searches through its list of open connections and the next available port number.

By convention, the port number is always greater than 1024 (port numbers from 0 to 1023 are reserved for system use and well-known services. Technically, the source