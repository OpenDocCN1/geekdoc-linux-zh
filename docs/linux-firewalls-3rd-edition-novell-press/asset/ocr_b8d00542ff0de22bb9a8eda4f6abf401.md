Query lookup requests are normally done over UDP, both for client-to-server lookups and for peer-to-peer server lookups. The UDP communication can fail for a lookup if the information being returned is too large to fit in a single UDP DNS packet. The server sets a flag bit in the DNS message header indicating that the data is truncated. In this case, the protocol allows for a retry over TCP. Figure 4.4 shows the relationship between UDP and TCP during a DNS lookup. In practice, TCP isn't normally needed for queries. TCP is conventionally used for administrative zone transfers between primary and secondary name servers.

# **FIGURE 4.4**
DNS client-to-server lookup.

![](bbox=[0.25, 0.32, 0.78, 0.78])

Zone transfers are the transfer of a name server's complete information about a network, or the piece (zone) of a network, that the server is authoritative for (that is, the official server). The authoritative name server is referred to as the primary name server. Secondary, or backup, name servers can periodically request zone transfers from their primary to keep their DNS caches up-to-date.