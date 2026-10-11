The Internet Protocol (IP) (RFC791) requires a packet to have three basic elements: source, destination, and data. (The data payload includes its length.) These elements provide the packet a level of autonomy. No matter where a packet is, you can identify where it came from, where it’s going, and how big it is.

The packet’s autonomy is an important feature of the Internet. As long as the packet is *alive* (the data is timely and relevant), routers can move data to its destination when the packet is launched onto the network.

# Packet Aliasing

Packet autonomy also has a downside. While a packet provides a way of getting to anywhere from anywhere, a malicious programmer can easily trick the network. The network does not require that the source host’s address be validated. *Aliasing or spoofing* (masking the true identity and assuming a different one) the hardware address is difficult, but programs can alias other IDs. Please note that later Linux kernels do not allow spoofing.

As discussed in Chapter 2, “TCP/IP Network Language Fluency,” the network packet is in network byte (or big endian) order. With that in mind, take a look at a structure definition of how the network packet appears in Listing 3.1, and Figure 3.2 displays the physical layout.

# LISTING 3.1   IP Structure Definition

```
```
/**** IP Packet definition                          ***/
/****   ***********  *   *    ***   ******  **     */

	typedef unsigned int uint;
	typedef unsigned char uchar;

	struct ip_packet {
	int  version:4;   /* 4-bit version [note] */
	int  header_len:4; /* header length in words [note] */
	int  serve_type:8; /* how to service packet [note] */
	int  packet_len:16;/* total size of packet in bytes */
	int  packet_ID:16; /* packet ID [note] */
	int  __reserved:1; /* always zero */
	int  dont_frag:1;  /* flag to permit fragmentation */
	int  more_frags:1; /* flag for "more frags to follow" */
	int  frag_offset:13;/* to help reassembly */
	int  time_to_live:8;/* permitted router hop cnt [note] */
	int  protocol:8;   /* ICMP, UDP, TCP [note] */
	... 
	};
```
```