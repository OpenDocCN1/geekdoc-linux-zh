# Figure 1.2 An illustration of a client-server TCP connection shows how the sequence numbers are incremented.

![](bbox=[0.22, 0.25, 0.85, 0.65])

# IP Spoofing — continued

The TCP protocol uses a handshake between the two parties. Thus, whenever the spoofer sends a packet to the server, the server will send an acknowledgement back to the "real" client. This real client does not know what to do with this ACK, and sends a message back to the server. The spoofer may try to flood the real client with dummy packets at such a rate that its buffers will overflow; thus, the ACK from the server will be lost.

Under some circumstances, a spoofing attack can be detected. If the machine has two network interfaces, one for a trusted network and one for an untrusted network, a spoofing attack can be detected as follows. For each connection request arriving on the machine, the receiving application must check the sender address. If this address does not match with the interface on which it was received (e.g., a message from a trusted host on the untrusted interface), the connection request should be refused, and the event should be logged. If needed, the administrator can be warned that such an event has occurred.