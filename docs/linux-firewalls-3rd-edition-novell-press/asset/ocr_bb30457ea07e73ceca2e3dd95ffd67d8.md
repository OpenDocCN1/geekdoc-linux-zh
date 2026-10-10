The IP header consists of a number of fields and totals 20 bytes, not including optional option fields that can be included as part of the header. The IP header is shown in Figure 1.2.

# **FIGURE 1.2**  
The IP header.

| | |
|---|---|
| **Version** | **Hdr Len** |
| **TOS** | **Total Datagram Len** |
| **Packet ID** | **Fl** |
| **Fragment Offset** | |
| **TTL** | **Protocol** |
| **Header Checksum** | |
| **Source Address** | |
| **Destination Address** | |
| **(IP Options)** | **(Padding)** |

The IP header begins with 4 bits indicating the version, currently version 4, followed by the length of the header, which is normally 20 bytes plus optional options. The maximum length of the IP header is 60 bytes. The next field, type-of-service or TOS, contains 3 bits for precedence (not used), 4 bits for the TOS itself, and one bit that must be set to 0. These are the four possible values for TOS:

+   - Minimize delay
+   - Maximize throughput
+   - Maximize reliability
+   - Minimize monetary cost

Under normal conditions these 4 bits are all zero, but certain applications might use various bits depending on their needs. For example, an SSH session might set the minimize delay bit because it is interactive by nature.

The first number of an IP address indicates the class of the address. Because each number within the dotted decimal notation is 8 bits, the possible values for each number are **0** through **255**. The class indicates the default number of bits devoted to the network portion of the address versus the number of bits devoted to the host identification with a given address. The division between the network portion of the address versus the host portion of the address is important because it is the basis of subnet addressing.