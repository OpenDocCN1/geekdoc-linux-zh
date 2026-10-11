+   • Add a checksum or CRC. Verify the data of each packet with a data summation. A CRC is more reliable than a checksum, but the checksum is easier to calculate. If the peer discovers that data is corrupted, it asks your program to resend the message.

+   • Use timeouts. You can assume that an expired timeout means failure. Your originator could retransmit the message, and your receiver could send a reminder to the sender.

The Critical and Important data types require the reliability found in TCP or better. Fault- Tolerant requires much more than any of these protocols offer. These outlined steps mimic the reliability of TCP.

UDP relies on IP’s features and services. Each UDP datagram packet receives an IP and a UDP header. Listing 3.3 defines how the UDP structure appears.

# LISTING 3.3 UDP Structure Definition

```
/*********************************************************/
/*** UDP (datagram) structure definition ***
/*** (Formal definition in netinet/udp.h) ***/
/*********************************************************/
typedef unsigned char u8;
typedef unsigned short int u16;

struct UDP_header {
    u16 src_port;      /* Originator's port number */
    u16 dst_port;      /* Destination's port number */
    u16 length;        /* Message length */
    u16 checksum;      /* Message checksum */
    uchar data[];      /* Data message */
};
```

![](bbox=[0.15, 0.68, 0.82, 0.85])

FIGURE 3.4 UDP layout.