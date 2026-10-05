# Maximum transfer unit

# Exhibit B A typical network packet⁴

| Ethernet header | IPv4 header | UDP header | Application data | Ethernet CRC |
|---|---|---|---|--|
| 14 bytes | 20 bytes | 8 bytes | 100 bytes | 4 bytes |
| UDP packet (108 bytes) | | | | |
| IPv4 packet (128 bytes) | | | | |
| Ethernet frame (146 bytes) | | | | |

# Ethernet framing

One of the main chores of the link layer is to add headers to packets and to put separators between them. The headers contain each packet's link-layer addressing information and checksums, and the separators ensure that receivers can tell where one packet stops and the next begins. The process of adding these extra bits is known generically as framing.

The link layer is actually divided into two parts: the MAC, the Media Access Control sublayer, and LLC, the Link Layer sublayer. The MAC layer deals with the media and transmits packets onto the wire. The LLC layer handles the framing.

Today, a single standard for Ethernet framing is in common use: DIX Ethernet II. Historically, slightly different standards based on IEEE 802.2 were also used, especially on Novell networks.

# Maximum transfer unit

The size of packets on a network may be limited by hardware specifications and by protocol conventions. For example, a standard Ethernet frame is traditionally 1,500 bytes. The size limit is associated with the link-layer protocol and is called the maximum transfer unit or MTU. Table 14.1 shows some typical values for the MTU.

# Table 14.1 MTUs for various types of network

| Network type | Maximum transfer unit |
|---|---|
| Ethernet | 1,500 bytes (1,492 with 802.2 framing)ᵃ |
| FDDI | 4,470 bytes (4,352 for IP/FDDI) |
| Token ring | Configurableᵇ |
| PPP modem link | Configurable, often 512 or 576 bytes |
| Point-to-point WAN links (T1, T3) | Configurable, often 1,500 or 4,500 bytes |

> ᵃ See page 541 for some comments on "jumbo" packets.
ᵇ Common values are 552; 1,064; 2,088; 4,508; and 8,232. Sometimes 1,500 to match Ethernet.

+   4. For specificity, RFCs that describe protocols often use the term "octet" instead of "byte.".