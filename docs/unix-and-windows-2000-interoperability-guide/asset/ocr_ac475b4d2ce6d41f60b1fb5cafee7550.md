# The Network Interface Layer

Now that we have a basic understanding of both UNIX and Windows 2000, let's move to the foundation of interoperability: networking. In recent years, the computing market place has moved to a number of standards that make networking between disparate operating systems much easier than in the early days of LANs. With the explosive growth of the Internet, one of these standards is the TCP/IP protocol suite. TCP/IP is often described using a four-layer model, depicted in Figure 3–1). Using that as our guide, we will begin our discussion with the lowest layer, the layer upon which all the other layers depend to function: the network interface layer.

# 3.1 Network Interface Cards and Drivers

From the viewpoint of the system administrator, the network interface layer deals primarily with network interface cards, cabling, and the operating system drivers that make these physical components work. It concerns the physical and electrical properties of a network medium, such things as voltages, currents, impedances, cable shielding, and distance limitations. It is also concerned with sending data to and receiving data from a network medium, usually in the form of frames (data encapsulated between headers and trailers). Each network interface technology in use today defines these and related characteristics. These technologies, found on both UNIX and Windows 2000 systems, include

+   Ethernet
Token Ring
FDDI
ATM
ISDN
PPP over RS-232
Fibre Channel