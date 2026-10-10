```
ICMP:      ----- ICMP header -----
ICMP:      Type = 0 (Echo reply)
ICMP:      Code = 0
ICMP:      Checksum = 505C (correct)
ICMP:      Identifier = 768
ICMP:      Sequence number = 512
ICMP:      [32 bytes of data]
ICMP:
ICMP:      [Normal end of "ICMP header".]

ICMP:      ----- ICMP header -----
ICMP:      Type = 3 (Destination unreachable)
ICMP:      Code = 1 (Host unreachable)
ICMP:      Checksum = 46BA (correct)
ICMP:
ICMP:      [Normal end of "ICMP header".]
ICMP:
ICMP:      IP header of originating message (description follows)
ICMP:      ----- IP Header -----
ICMP:      Version = 4, header length = 20 bytes
ICMP:      Type of service = 00
ICMP:              000. ... . = routine
ICMP:              ...0 ... . = normal delay
ICMP:              .... 0... . = normal throughput
ICMP:              ..... .0.. . = normal reliability
ICMP:      Total length      = 56 bytes
ICMP:      Identification    = 58963
ICMP:      Flags
ICMP:              .0.. ... . = may fragment
ICMP:              ..0. ... . = last fragment
ICMP:      Fragment offset = 0 bytes
ICMP:      Time to live    = 125 seconds/hops
ICMP:      Protocol        = 17 (UDP)
ICMP:      Header checksum = CEBF (correct)
ICMP:      Source address  = [205.243.70.66]
ICMP:      Destination address = [198.49.174.58]
```

Figure 1.22 ICMP header sniffer capture.

**Information Request (Type 15)/Information Reply (Type 16).** As an alternative to RARP (described previously), stations use Type 15 and Type 16 to obtain an Internet address for a network to which they are attached. The sending station will emit the message, with the network portion of the Internet address, and wait for a response, with the host portion (its IP address) filled in.

+   * **Address Mask Request (Type 17)/Address Mask Reply (Type 18).** Similar to an Information Request/Reply, stations can send Type 17 and Type 18 messages to obtain the subnet mask of the network to which they are attached. Stations may submit this request to a known node, such as a gateway or router, or broadcast the request to the network.

**Hacker's Note** If a machine sends ICMP redirect messages to another machine in the network, it could cause an invalid routing table on the other machine. If a machine acts as a router and gathers IP datagrams, it could gain control and send these datagrams wherever programmed to do so. These ICMP-related security issues will be discussed

31