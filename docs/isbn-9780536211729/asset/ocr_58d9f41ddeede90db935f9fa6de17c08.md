# 7.4.1 Allowing DNS (UDP/TCP Port 53) 

DNS uses a communication protocol that relies on both UDP and TCP. Connection modes include regular client-to-server connections, peer-to-peer traffic between forwarding servers and full servers, and primary and secondary name server connections.

Query lookup requests are normally done over UDP, both for client-to-server lookups and for peer-to-peer server lookups. The UDP communication can fail for a lookup if the information returned is too large to fit in a single UDP DNS packet. The server sets a flag bit in the DNS message header indicating that the data is truncated. In this case, the protocol allows for a retry over TCP. Figure 7.4 shows the relationship between UDP and TCP during a DNS lookup. In practice, TCP isn' normally needed for queries. TCP is conventionally used for administrative zone transfers between primary and secondary name servers.

![](bbox=[0.275, 0.31, 0.725, 0.755])

Figure 7.4 DNS client-to-server lookup.

Zone transfers are the transfer of a name server's complete information about a network, or the piece (zone) of a network, that the server is authoritative for (that is, the official server). Secondary, or backup, name servers can periodically request zone transfers from their primary to keep their DNS caches up-to-date.