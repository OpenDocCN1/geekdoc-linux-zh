Solving the first problem helps prepare the receiver to track each packet of a message. If there appears to be a sequencing problem, the receiver could request a specific packet. Also, the sender could expect an acknowledgment of each packet.

One method you could use is to assign a unique sequence number to each packet (like TCP’s acknowledgment mechanism). As each packet arrives, your beefed-up UDP code checks it off. If a packet is lost, your program may request a retransmission with the specific packet number. The main problem with this method is that one party must retain a record of all the packets it sent. It could drop off very old packets, but that packet history could become very long.

A way to solve lengthy packet histories is to acknowledge each packet. This method solves the second problem and requires the receiver to reply to each packet with its own message indicating what it successfully received by sequence number. This technique is in essence what TCP does. However, using this technique, your program experiences some of the performance hit that TCP has.

The problem is that most physical networks are not truly bi-directional. Each transmission takes up some of the network bandwidth, keeping others from transmitting. Also, each packet has the IP header and the UDP header (28-byte minimum). If the receiver replies to each packet individually, most of the acknowledgment is header overhead (4 or 5 bytes for your sequence ID acknowledgment and 28 bytes for the UDP/IP header). Therefore, keeping the receiver silent as long as possible helps reduce network congestion.

A solution could be to group the acknowledgments into a few packets. For example, if each packet is 1,024 bytes and the sender has to transmit a 1MB message, the receiver could get about 1,000 packets. Within that 1,024-byte limit, the receiver could easily acknowledge 10 packets at a time. This limits the history to 10×1,024 bytes. You need to know the network performance and the host memory limitations in order to implement this property.

This introduces another problem: How does the receiver know when the sender is done? For instance, if the receiver acknowledges every tenth packet and the sender only has five packets, you may run into two problems:

+   - The receiver may never send an acknowledgment.
+   - The sender may assume that the receiver never got the packets, so it retransmits.

To solve this, you could tell the receiver the total number of packets to expect. When the receiver gets the last packet, it transmits the shortened acknowledgment message.

![](bbox=[0.78, 0.55, 0.82, 0.9])