| | Ethernet | 10Base2 | 10Base5 | 10BaseT | 10BaseFL | 100BaseT |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Topology** | Bus | Bus | Bus | Star | Pt-to-Pt | Bus |
| **Data Transfer Rate** | 10 Mbps | 10 Mbps | 10 Mbps | 10 Mbps | 10 Mbps | 100 Mbps |
| **Maximum Segment Length** | 500 Meters | 185 Meters | 500 Meters | 100 Meters | 2,100 Meters | 100 Meters |
| **Media Type** | Thick Coax | Thin Coax | Thick Coax | Unshielded Twisted Pair | Fiber Optic | Unshielded Twisted Pair |

Figure 6.5 Ethernet option specifications for cable design.

| Start Delimiter | Access Control | End Delimiter |
| :--- | :--- | :--- |

Figure 6.6 The Token Frame format.

# Token Ring

For quick frame resolution reference during sniffer capture analyses, refer to the two Token Ring frame formats, Token Frame and Data/Command Frame, shown in Figures 6.6 and 6.7, respectively.

A Token Frame consists of Start Delimiter, Access Control Byte, and End Delimiter fields, described here:

+   *   Start Delimiter. Announces the arrival of a token to each station.
+   *   Access Control. The prioritization value field:
+   *   000 Normal User Priority
+   *   001 Normal User Priority
+   *   010 Normal User Priority
+   *   011 Normal User priority
+   *   100 Bridge/Router
+   *   101 Reserved IBM
+   *   110 Reserved IBM
+   *   111 Station Management
+   *   End Delimiter. Indicates the end of the token or data/command frame.