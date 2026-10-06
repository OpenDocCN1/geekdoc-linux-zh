# 24.4 Protocol Mechanisms for Data Exchange 505

| A | B |
| 1 | PSH, ACK, seq=1, len=1024, ack=1, win=4096 |
| 2 | PSH, ACK, seq=1025, len=1024, ack=1, win=4096 |
| 3 | PSH, ACK, seq=2049, len=1024, ack=1, win=4096 |
| 4 | PSH, ACK, seq=3073, len=1024, ack=1, win=4096 |
| | 5 | ACK=1025 |
| | 6 | ACK=1025 |
| | 7 | ACK=1025 |
| 8 | PSN, ACK, seq=1025, len=1024, ack=1, win=4096 |
| | 9 | ACK=seq=5121 |
| 10 | PSH, ACK, seq=5121, len=1024, ack=1, win=4096 |
| 11 | PSH, ACK, seq=6145, len=1024, ack=1, win=4096 |
| 12 | FIN, PSH, ACK, seq=7169, len=1024, ack=1, win=4096 |
| | 13 | ACK, ack=8, win=0 |

24-17
Detecting a single packet loss by duplicate acknowledements (segments 5 to 7) and handling by fast retransmission.

sending duplicate acknowledements, because it is now receiving packets out of order. Figure 24-17 shows such a situation.

The sender can see from the duplicate acknowledements it received that a segment must have been lost, but other segments still made their way to the receiver. This means that a massive congestion is unlikely. The sender retransmits the segment that follows the sequence number of the duplicate acknowledements without waiting for the retransmission timer to trigger.

A new slow-start phase would be the normal response to a packet loss: that reaction would significantly reduce the transmission rate. Given duplicate acknowledgments, however, TCP detects that there is no serious congestion. For this reason, the fast-recovery method was introduced as an extension of the fast-retransmission algorithm. After a retransmission, the congestion window is not set to a minimum value, but instead cut in half, and,, increased linearly directly in the congestion-avoidance phase.

We will next discuss how these algorithms compete in the TCP instance of the Linux kernel⁴.

When three acknowledgement duplicates are received, the variable tp->snd_ssthresh is set to half of the current transmit window. The missing segment is retransmitted, and the congestion window tp->snd_cwnd takes the value tp->ssthresh + 3 * MSS, where MSS denotes the maximum segment size.

> ⁴We will keep our discussion short, because the implementation of these two algorithms is extensive and distributed over many positions within the TCP instance.