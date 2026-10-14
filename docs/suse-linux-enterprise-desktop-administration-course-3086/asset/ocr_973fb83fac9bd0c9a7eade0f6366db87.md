In addition, IP is an unreliable protocol because it has no mechanisms for error detection or error correction. In other words, IP cannot guarantee delivery of data. However, if data arrives at the destination host, the data is correct. This is guaranteed by the Network Access layer.

The following basic tasks are performed by IP:

+   - Specifies datagrams that form the basic units for transferring data on the Internet
+   - Defines the addressing scheme
+   - Routes, exchanges, and transfers datagrams through the network
+   - Fragments and assembles datagrams

Every packet or datagram transmitted over the TCP/IP network has an IP header. Figure B-15 shows how the header of an IP datagram is constructed.

![](bbox=[0.08, 0.55, 0.9, 0.78])

Figure B-15

The IP header has the following elements:

+   - *Version (4 bits)*—Specifies the format of the IP packet header.
+   - *IHL (Internet Header Length, 4 bits)*—Specifies the length of the IP packet header.
+   - *TOS (Type of Services, 8 bits)*—Specifies the parameters for the type of service requested, such as priority, reliability, and monetary cost.
+   - *Total length (16 bits)*—Contains the length of the datagram.
+   - *Identification (16 bits)*—Identifies the fragments of the datagram.
+   - *Flags (3 bits)*—Include the following:
+     - *R (Reserved, 1 bit)*—Is reserved for future use.
+     - *DF (Don't Fragment, 1 bit)*—Controls the fragmentation of the datagram.
+     - *MF (More Fragments, 1 bit)*—Indicates if the datagram contains additional fragments.