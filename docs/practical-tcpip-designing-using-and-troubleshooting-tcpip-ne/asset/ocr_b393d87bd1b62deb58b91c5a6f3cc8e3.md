# ## 24.4 Stateful packet inspection and resource usage

Let's look at a specific example of how an SPI firewall can block a particular type of attack, using its state information. A common denial of service (DoS) attack is the “SYN Flood.” Here's how it works. When a TCP connection is being established, client and server go through the normal SYN, SYN/ACK, ACK three-way handshake (Module 10.8). When the server receives the initial SYN from the client, it replies with SYN/ACK and creates an entry in an internal table saying it's awaiting an ACK from the client to complete the connection establishment (Figure 24.5).

![](bbox=[0.22, 0.26, 0.78, 0.41])

Figure 24.5 Server awaiting an ACK to complete connection establishment

When the client sends the answering ACK, the server removes the entry from the “awaiting ACK” table because the connection is now fully established (Figure 24.7).

![](bbox=[0.22, 0.52, 0.78, 0.67])

Figure 24.6 Connection established — three-way handshake completed

In a SYN flood, the attacker sends a large number of SYNs in quick succession and never completes the connection establishment. The server's internal table fills up (Figure 24.7) so it's unable to accept connections from any other, real clients. In this way it has denied service to legitimate users.

SPI firewalls can protect servers from this type of attack. Instead of passing the initial SYN through to the server, the firewall itself sends the SYN/ACK, and awaits the establishing ACK. If the client is legitimate and sends the ACK, the firewall then performs its own three-way handshake with the server (Figure 24.8); when that's complete, it passes all traffic from the legitimate client to the server as normal. However, if the client is a hacker attempting a SYN flood, the real server is never contacted; the firewall detects the attack, recognizing the abnormal load of incomplete connection establishments and discarding them. The firewall may also raise an alert to inform the network manager of the attack.