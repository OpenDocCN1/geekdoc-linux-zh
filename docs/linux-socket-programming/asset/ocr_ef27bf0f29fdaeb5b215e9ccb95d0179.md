The packet types most likely to be of interest are TCP, UDP, ICMP, and raw. Knowing the advantages and disadvantages of each type can help you choose the most appropriate for your application. Each packet type has different benefits, as summarized in Table 3.2.

Table 3.2, Packet Type Benefits

| | Raw | ICMP | UDP | TCP |
| Overhead (bytes) | 20-60 | 20-60+[4] | 20-60+[8] | 20-60 +[20-60] |
| Message Size (bytes) | 65,535 | 65,535 | 65,535 | (unlimited) |
| Reliability | Low | Low | Low | High |
| Message Type | Datagram | Datagram | Datagram | Stream |
| Throughput | High | High | Medium | Low |
| Data Integrity | Low | Low | Medium | High |
| Fragmentation | Yes | Yes | Yes | Low |

In this table, notice that each packet type contains comparisons. A reliability of Low value only means that you cannot rely on the protocol to help reliability. While the differences may seem extreme, remember that they are merely comparisons.

# ### Considering the Packet's Issues

Each protocol addresses issues in the transmission. The following sections define each issue and associated category from Table 3.2. This information can help you see why certain protocols implement some features and skip others.

# #### Protocol Overhead

Protocol overhead includes both the header size in bytes and the amount of interaction the protocol requires. High packet overhead can reduce throughput, because the network has to spend more time moving headers and less time reading data.

Strong protocol synchronization and handshaking increase interaction overhead. This is more expensive on WANs because of the propagation delays. Table 3.2 does not include this measurement.

# #### Protocol Message Size

To calculate network throughput, you need to know the packet size and the protocol's overhead. The transmission size gives you the maximum size of a sent message. Since all but TCP use a single-shot message, this limitation is typically due to the limits of IP packet (65,535 bytes). The amount of data your program transmits per packet is the transmission size less the headers.

# #### Protocol Reliability

Part of the problem with networks is the possibility of lost messages. A message could be corrupted or dropped as it moves from one host or router to another, or the host or router could crash or fail. In each case, a message may simply be lost, and your program may need to follow up.

Also, you may need to make sure that the destination processes the packets in the correct order. For example, you may compose a message that does not fit in one packet. If the second packet arrives before the first, the receiver must know how to recognize and correct the problem. However, the order is not important when each message is independent and self-contained.