
| Device Type | TCP/IP Protocols |
| --- | --- |
| 3Com CoreBuilder switch | HTTP, FTP, Telnet, and SNMP |
| 3Com RMON probe | TFTP and SNMP |
| Cisco 7000 router | HTTP, FTP, Telnet, and SNMP |
| Brocade fibre channel switch | HTTP, Telnet, and SNMP |
| Lexmark laser printer | FTP and SNMP |

TCP/IP is independent of the datalink protocol and can be used with many different networking technologies, including FDDI, Ethernet, ATM, TokenRing, Frame Relay, and SMDS. TCP/IP makes it possible to build a truly heterogeneous network consisting of products and network technologies from many different vendors and sources. In fact, the Internet, which is considered the world's largest network, consists of devices from many networking vendors that operate together. That's not to say the Internet doesn't have its share of networking issues or problems, but, for the most part, many would agree that interoperability between equipment vendors isn't a major factor for the established core set of TCP/IP protocols.

From a management standpoint, many of the tools used to administer TCP/IP systems are consistent across most UNIX operating system versions. These tools are described in Chapter 6, “Network Management Agents.” However, one issue that can be a problem is that each UNIX operating system vendor can and does implement non-protocol details differently. For example, how the IP address information is stored on each network device is not covered by any RFC standard, nor should it be. The present TCP/IP suite provides a mechanism to dynamically assign IP addresses to devices, and it also mandates that they be uniquely assigned to each device attached to the network. However, IP addresses are stored on a local system and are not a protocol matter, but rather a network management or system configuration issue, which is traditionally resolved at the operating system level. Each operating system vendor provides its own solutions to how IP address information or other operating system parameters are to be stored.

## OSI Model

Networking protocols including TCP/IP can be mapped to a general network model. This model defines the relationship and services that each protocol will provide to other associated protocols, services, and applications. The most common standard network model is based on Open Systems Interconnection. The OSI seven-layer model is represented by a series of layers stacked one upon another, which, when viewed collectively, represent the operation of an entire network. Each layer represents a unique view of the elements that make up the network. The layers of the OSI model consist of the following:

- application
- presentation
- session
- transport
- network
- datalink
- physical

### Application Layer

Provides services to users that include file transfer, electronic email, remote host access, and many other services.

### Presentation Layer

Is used to provide a common interface for applications to the lower layers and implement common services that might include encryption, reformatting, and compression.

### Session Layer

Provides the mechanism to establish, maintain, and terminate sessions between cooperating applications.

### Transport Layer

Ensures reliable, transparent data transfer, flow control, and data error detection and recovery between two endpoints.

### Network Layer

Provides upper-layer protocol transparency because different network communication methodologies may be used. This layer is responsible for establishing, maintaining, and terminating connections for different networks.

### Datalink Layer

Provides data transfer service on the physical link using frames; handles error detection, flow control, and related services. Some common frame types include Ethernet, FDDI, and TokenRing.

### Physical Layer

Addresses the mechanism connectivity requirements (such as cables and connectors) and provides transmission of a bit stream that involves controlling voltage characteristics to produce the appropriate signals. Examples include cabling for Ethernet, Fast Ethernet, FDDI, and TokenRing.

## TCP/IP Protocol Architecture

Placing or overlaying the TCP/IP suite on the OSI model helps demonstrate TCP/IP's protocol operation and its relationship to other protocols. Figure 3.1 shows a pictorial view of where TCP/IP fits into the OSI model.

As shown in Figure 3.1, the TCP/IP model consists of four layers. Each layer maps to one or more of the OSI layers, which include:

- process
- host-to-host
- Internet
- network access

Except for network access, the other three component layers are software-based and consist of programmed modules that provide

![](img/f265c9d1f2610aca197c430cbfcd51f5_93_0.png)

Figure 3.1 *TCP/IP over the OSI networking model.*

the required functionality. Typically, these components are incorporated into operating systems to provide generalized access.

### Process Layer

This layer provides user applications and interfaces with the host-to-host layer. Additional protocols and services are also found on this layer. The process layer maps to the presentation and application layers, which are defined within the OSI model. Applications on this layer include Telnet, FTP, SMTP, and many others.

### Host-to-host Layer

This layer is responsible for ensuring that data is reliable and that each higher-level service obtains the correct information from the sending entity. The protocol supported on this layer is TCP. The layer maps to the OSI transport layer. The term used to describe information on the host-to-host layer is *segment*.

### Internet Layer

This layer provides an unreliable flow of information from one network to another. From an OSI standpoint, this layer is defined as the network layer. The Internet layer (or network) is responsible for routing between different IP networks. The protocol supported on this layer is IP. The term used to describe the information processed on this layer is *packet*.

### Network Access Layer

The network access layer involves physical attachment to the network, which traditionally requires a hardware interface from the network to a computer's internal bus. This layer includes both physical and datalink layers from the OSI model. The network access component defines the network architecture and topology. Some examples include Ethernet, FDDI, and TokenRing. The term used to describe the information processed on this layer is *frame*. A small driver program, which is provided by the interface manufacturers, is also needed to interface the hardware to the operating system.

The TCP/IP and associated protocols can also be placed on the OSI seven-layer model, as shown in Figure 3.2. Here, we can see how the protocols and services relate to the model. The next few pages further describe the many additional services provided by the TCP/IP protocol suite.

### Process Layer Services

The TCP/IP services on the process layer include end-user tools, additional protocols, and system services. Found on different UNIX platforms, TCP/IP provides a common mechanism to share files, send/receive Email, access systems remotely, transfer files between systems, and accomplish other networking tasks. Although the TCP/IP protocol and application suite is large, many UNIX system vendors provide a smaller subset of these services. Table 3.2 lists many of the core TCP/IP services generally available on UNIX systems.

![](img/f265c9d1f2610aca197c430cbfcd51f5_95_0.png)

Figure 3.2 TCP/IP protocol suite.

### End-User Tools

The end-user tools, which are common to many UNIX system implementations of TCP/IP, are applications that are generally available to normal system users. As a result, these tools do not require system root privileges for operation. For example, general users without any special consideration from an administration standpoint can invoke the Telnet and FTP commands. Some services within the TCP/IP suite refer to both end-user applications and protocols. Telnet is a good example of this because it represents both a user tool and a communication protocol. In practice, however, this isn’t a big problem, because end-user applications on UNIX are lower case (such as telnet) and protocols are generally written in upper case.

It is interesting to note that certain organizations disable some TCP/IP services as a way of tightening security. One organization in particular did not want its users to have the ability to send or receive Email on core development systems and removed the SMTP servers from those systems. Another way that organizations
