
|  | Ethernet | 10Base2 | 10Base5 | 10BaseT | 10BaseFL | 100BaseT |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Topology** | Bus | Bus | Bus | Star | Pt-to-Pt | Bus |
| **Data Transfer Rate** | 10 Mbps | 10 Mbps | 10 Mbps | 10 Mbps | 10 Mbps | 100 Mbps |
| **Maximum Segment Length** | 500 Meters | 185 Meters | 500 Meters | 100 Meters | 2,100 Meters | 100 Meters |
| **Media Type** | Thick Coax | Thin Coax | Thick Coax | Unshielded Twisted Pair | Fiber Optic | Unshielded Twisted Pair |

Figure 6.5 Ethernet option specifications for cable design.

| Start Delimiter | Access Control | End Delimiter |
| :--- | :--- | :--- |

Figure 6.6 The Token Frame format.

## Token Ring

For quick frame resolution reference during sniffer capture analyses, refer to the two Token Ring frame formats, Token Frame and Data/Command Frame, shown in Figures 6.6 and 6.7, respectively.

A Token Frame consists of Start Delimiter, Access Control Byte, and End Delimiter fields, described here:

- Start Delimiter. Announces the arrival of a token to each station.
- Access Control. The prioritization value field:
    - 000 Normal User Priority
    - 001 Normal User Priority
    - 010 Normal User Priority
    - 011 Normal User priority
    - 100 Bridge/Router
    - 101 Reserved IBM
    - 110 Reserved IBM
    - 111 Station Management
- End Delimiter. Indicates the end of the token or data/command frame.

The Data/Command Frame format is composed of nine fields, defined in the following list.

- Start Delimiter. Announces the arrival of a token to each station.
- Access Control. The prioritization value field:
    - 000 Normal User Priority
    - 001 Normal User Priority
    - 010 Normal User Priority
    - 011 Normal User priority
    - 100 Bridge/Router
    - 101 Reserved IBM
    - 110 Reserved IBM
    - 111 Station Management
- Frame Control. Indicates whether data or control information is carried in the frame.
- Destination Address. A 6-byte field of the destination node address.
- Source Address. A 6-byte field of the source node address.
- Data. Contains transmission data to be processed by receiving station.
- Frame Check Sequence (FCS). Similar to a CRC (described in Chapter 3), the source station calculates a value based on the frame contents. The destination station must recalculate the value based on a successful frame transmission. The frame is discarded if the FCS of the source and destination do not match.
- End Delimiter. Indicates the end of the Token or Data/Command frame.
- Frame Status. A 1-byte field specifying a data frame termination, and address-recognized and frame-copied indicators.

| Start Delimiter | Access Control | Frame Control | Destination Address | Source Address | Data | Frame Check Sequence | End Delimiter | Frame Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 6.7 The Data/Command Frame format.

### Token Ring and Source Route Bridging

When analyzing Token Ring *source route bridging* (SRB) frames, it is important to be able to understand the frame contents to uncover significant route discovery information. To get right down to it, in this environment, each source station is responsible for preselecting the best route to a destination (hence the name *source route bridging*). Let’s investigate a real-world scenario and then analyze the critical frame components (see Figure 6.8).

Assuming that Host A is required to preselect the best route to Host B, the steps are as follows:

1. Host A first sends out a local test frame on its local Ring 0x25 for Host B. Host A assumes that Host B is local, and thus transmits a test frame on the local ring.
2. Host A sends out an explorer frame to search for Host B. No response from Host B triggers Host A to send out an explorer frame (with the first bit in MAC address or multicast bit set to 1) in search for Host B. Each bridge will forward a copy of the explorer frame. As Host B receives each explorer, it will respond by adding routes to the frame from the different paths the particular explorer traveled from Host A.
3. Host A has learned the different routes to get to Host B. Host A will receive responses from Host B with two distinct routes:
    - Ring 0x25 to Bridge 0xA to Ring 0x26 to Bridge 0xB to Ring 0x27 to Host B
    - Ring 0x25 to Bridge 0xC to Ring 0x28 to Bridge 0xD to Ring 0x27 to Host B

Communication will begin, as Host A knows how to get to Host B, typically choosing the first route that was returned after the explorer was released. In this case, the chosen router would be Route 1: Ring 0x25 to Bridge 0xA to Ring 0x26 to Bridge 0xB to Ring 0x27 to Host B.

Let’s examine two significant fields of our new Token Ring frame, shown in Figure 6.9, and defined here:

- Route Information Indicator (RII). When this bit is turned on (set to 1), it indicates that the frame is destined for another network, and therefore includes a route in the Route Information Field (RIF).

| Access Control | Frame Control | Destination Address | Route Information Indicator (RII) | Source Address | Route Information Field (RIF) | Data | CRC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 6.9 New Token Ring Frame format.

- Route Information Field (RIF). The information within this field is critical, as it pertains to the route this frame will travel to reach its destination. Let’s examine the RIF subfields and then compute them in our previous example in Figure 6.10.

The RIF will contain the following fields: **Routing Control** and three **Route Descriptors**.

- **Routing Control**. This field is broken down into the following five segments (see Figure 6.11):
    - **Type.** Indicates one of three types of routes in the frame:
        - 000: Specific Route (as in our example).
        - 110: Single Route Broadcast/Spinning Tree Explorer (for example, as used by NetBIOS); only bridges in local spanning tree will forward this.
        - 100: All Routes Explorer (as used by the National Security Agency [NSA]); an all routes broadcast.
    - **Length.** Indicates the total RIF size (2 to 18).
    - **Direction.** A result of the frame's direction, forward or backward; specifies which direction the RIF should be read (0=left to right, 1=right to left).
    - **MTU.** Specifies the MTU in accordance to each receiving node along the path:
        - 000–516 and lower
        - 001–1500 (Ethernet standard)
        - 010–2052
        - 011–4472 (Token Ring standard)
        - 100–8144
        - 101–11407
        - 110–17800
        - 111: For all broadcast frames only
    - **Route Descriptor**. This field is broken down into two segments: Ring Number and Bridge Number.

| Routing Control | Route Descriptor | Route Descriptor | Route Descriptor |
| :--- | :--- | :--- | :--- |

Figure 6.10 The RIF subfields.

| Type (3 bits) | Length (5 bits) | Direction (1 bit) | MTU (3 bits) | 4 bits (not used) |
| :--- | :--- | :--- | :--- | :--- |

Figure 6.11 Routing Control segments.

Now we're ready to compute the RIF we should see in the previous scenario. To summarize: Communication will begin, as Host A knows how to get to Host B, with the following chosen route:

Given from Figure 6.12:

![](img/ba85bb40c695c02adae8cbd6666f2e0c_191_0.png)

Figure 6.8 Token Ring source route bridging scenario.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_193_0.png)

Figure 6.12 Given RIF route.

- A to (Ring 0×25 to Bridge 0×A) to (Ring 0×26 to Bridge 0×B) to (Ring 0×27) to B.

The three sets of parentheses indicate the information that correlates with the three Route Descriptor fields in our RIF.

- **RIF:** Host A to (Ring 0×25 to Bridge 0×A) to (Ring 0×26 to Bridge 0×B) to (Ring 0×27) to Host B.

In this scenario, our RIF calculation will include the following hexadecimal values (see Figure 6.13).

From this analysis, we can conclude that as Host A travels to Host B using the route Host A to (Ring 0×25 to Bridge 0×A) to (Ring 0×26 to Bridge 0×B) to (Ring 0×27) to Host B, the RIF would consist of the following values in hex:

- 0830.025A.026B.0270
