# **Internet Layer**

This layer provides an unreliable flow of information from one network to another. From an OSI standpoint, this layer is defined as the network layer. The Internet layer (or network) is responsible for routing between different IP networks. The protocol supported on this layer is IP. The term used to describe the information processed on this layer is *packet*.

# **Network Access Layer**

The network access layer involves physical attachment to the network, which traditionally requires a hardware interface from the network to a computer's internal bus. This layer includes both physical and datalink layers from the OSI model. The network access component defines the network architecture and topology. Some examples include Ethernet, FDDI, and TokenRing. The term used to describe the information processed on this layer is *frame*. A small driver program, which is provided by the interface manufacturers, is also needed to interface the hardware to the operating system.

The TCP/IP and associated protocols can also be placed on the OSI seven-layer model, as shown in Figure 3.2. Here, we can see how the protocols and services relate to the model. The next few pages further describe the many additional services provided by the TCP/IP protocol suite.

# **Process Layer Services**

The TCP/IP services on the process layer include end-user tools, additional protocols, and system services. Found on different UNIX platforms, TCP/IP provides a common mechanism to share files, send/receive Email, access systems remotely, transfer files between systems, and accomplish other networking tasks. Although the TCP/IP protocol and application suite is large, many UNIX system vendors provide a smaller subset of these services. Table 3.2 lists many of the core TCP/IP services generally available on UNIX systems.